# Despliegue seguro de MEGA en Docker Swarm

Las migraciones deben terminar antes de que los procesos Rails y Sidekiq de una nueva versión comiencen a trabajar. Un worker que arranca mientras una migración está pendiente puede conservar en memoria un esquema obsoleto aunque la base de datos se actualice después.

## Procedimiento de actualización

1. Reserve una ventana de despliegue exclusiva: no ejecute dos actualizaciones del mismo stack en paralelo. Inventarie el servicio Rails y todos los servicios Sidekiq antes de comenzar.

   ```bash
   docker stack services <stack> --format '{{.Name}} {{.Image}} {{.Replicas}}'
   ```

2. Elija una imagen inmutable. Use un tag nuevo y fije el digest publicado; no reutilice ni sobrescriba tags existentes.

   ```bash
   docker pull sendingtk/chatwoot:vX.Y.Z
   docker image inspect sendingtk/chatwoot:vX.Y.Z \
     --format '{{range .RepoDigests}}{{println .}}{{end}}' | grep '^sendingtk/chatwoot@sha256:'
   ```

   Debe obtener exactamente el digest de `sendingtk/chatwoot`. Reemplace todas las referencias `image:` de Rails y Sidekiq por ese mismo valor `sendingtk/chatwoot@sha256:...` antes de continuar.

3. Confirme que la migración es compatible con la versión que sigue activa durante la ventana. Si no lo es, drene primero todos los procesos Rails y Sidekiq afectados según el plan de mantenimiento; no migre mientras esos procesos continúan leyendo o escribiendo.

   Ejecute una tarea de migración única con la imagen nueva y con el mismo acceso a PostgreSQL que usa el stack. El siguiente ejemplo solo es válido cuando todas las credenciales necesarias están disponibles en el archivo de variables y la red overlay es conectable:

   ```bash
   docker run --rm \
     --network <red-overlay-conectable> \
     --env-file <variables-de-produccion> \
     sendingtk/chatwoot@sha256:<digest> \
     bundle exec rails db:mega_prepare
   ```

   La red overlay debe haberse creado con `--attachable` para usar `docker run`. Si la aplicación obtiene credenciales mediante secretos, configs o mounts de Swarm, cree la tarea como un job one-shot de Swarm con esos mismos recursos; no sustituya secretos faltantes por valores escritos en el comando o en el repositorio:

   ```bash
   docker service create \
     --name <servicio-migracion> \
     --mode replicated-job \
     --replicas 1 \
     --restart-condition none \
     --network <red-overlay> \
     --env-file <variables-de-produccion> \
     --secret <secreto-requerido> \
     --config <config-requerida> \
     sendingtk/chatwoot@sha256:<digest> \
     bundle exec rails db:mega_prepare
   docker service ps <servicio-migracion> --no-trunc
   docker service logs <servicio-migracion>
   docker inspect <id-tarea-migracion> \
     --format '{{.Status.State}} {{.Status.ContainerStatus.ExitCode}}'
   ```

   Obtenga `<id-tarea-migracion>` de `docker service ps -q --no-trunc <servicio-migracion>`. Continúe únicamente cuando la tarea figure como `complete` y el código de salida sea `0`; cualquier otro estado o código bloquea el despliegue.

   Espere la finalización y conserve el log. Si la migración devuelve un código distinto de cero, mantenga bloqueado el despliegue: no inicie la nueva imagen. Revise `rails db:migrate:status` y defina una corrección hacia adelante o una restauración validada antes de reanudar; una migración parcialmente aplicada no se corrige reiniciando workers.

4. Después de una migración exitosa, despliegue una sola vez el stack con el digest nuevo. El cambio de digest debe actualizar el servicio Rails y todos los servicios Sidekiq, incluidos los workers divididos.

   ```bash
   docker stack deploy --with-registry-auth --resolve-image always -c <archivo-stack.yml> <stack>
   ```

   No ejecute inmediatamente un segundo rollout con `docker service update --force`: el cambio de digest ya reinicia los servicios. Use `--force` únicamente para un servicio que, tras verificar su especificación, no haya cambiado de digest; primero determine por qué quedó fuera del archivo desplegado. Si un servicio falla durante el rollout, detenga las siguientes operaciones y resuelva mediante rollback compatible o corrección hacia adelante; no acepte una flota dividida como estado final.

5. Espere a que cada servicio alcance todas sus réplicas y compruebe tanto la especificación como todas las tareas activas:

   ```bash
   docker stack services <stack>
   docker stack ps <stack> --no-trunc
   docker stack ps <stack> --filter desired-state=running --no-trunc
   docker service inspect <servicio-rails> --format '{{.Spec.TaskTemplate.ContainerSpec.Image}}'
   docker service inspect <servicio-sidekiq> --format '{{.Spec.TaskTemplate.ContainerSpec.Image}}'
   docker service ps <servicio-rails> --filter desired-state=running --no-trunc
   docker service ps <servicio-sidekiq> --filter desired-state=running --no-trunc
   ```

   La salida sin filtro de `docker stack ps` conserva tareas fallidas, rechazadas o reemplazadas; distinga por fecha las del rollout actual de fallos históricos ya resueltos. Repita ambos comandos `docker service inspect` y `docker service ps` para cada worker inventariado en el primer paso. En cada nodo, `docker inspect` del contenedor activo permite confirmar el `Image` ejecutado. No dé por terminado el despliegue si el rollout actual tiene tareas rechazadas, réplicas incompletas, servicios omitidos o imágenes con tags/digests distintos.

## Aislamiento de la cola WhatsApp

Cuando existe un worker dedicado con `bundle exec sidekiq -q whatsapp`, los workers genéricos deben usar `WHATSAPP_IN_MAIN_SIDEKIQ=false`. Así se evita que réplicas con perfiles diferentes compitan por la misma cola. Los templates divididos de este directorio ya incluyen esa variable; manténgala al copiar variables a otros stacks.

El retry de Sidekiq protege errores transitorios, pero no sustituye este procedimiento: si toda la flota conserva un esquema obsoleto, todos los intentos pueden fallar.
