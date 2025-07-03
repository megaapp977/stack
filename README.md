# Guía de Instalación y Despliegue

Este repositorio contiene archivos YAML para desplegar servicios en un clúster Docker Swarm.
A continuación se detallan los pasos básicos para configurar el entorno y desplegar Traefik y Portainer.

## 1. Preparación del sistema

```bash
sudo apt-get update && sudo apt-get install -y apparmor-utils
hostnamectl set-hostname nome_rede_interna
```

Edite `/etc/hosts` para asociar `localhost` con el nuevo nombre:

```
127.0.0.1 nome_rede_interna
```

## 2. Instalación de Docker y Swarm

```bash
curl -fsSL https://get.docker.com | bash

docker swarm init
```

Cree la red overlay que utilizarán los servicios:

```bash
docker network create --driver=overlay --attachable nome_rede_interna
```

## 3. Despliegue de Traefik

Copie el contenido de `traefik/traefik.yaml` o cree su propio archivo `traefik.yaml` y ejecútelo con:

```bash
docker stack deploy --prune --resolve-image always -c traefik.yaml traefik
```

## 4. Despliegue de Portainer

Copie el contenido de `portainer/portainer.yaml` en `portainer.yaml` y ejecútelo con:

```bash
docker stack deploy --prune --resolve-image always -c portainer.yaml portainer
```

Una vez desplegado Portainer, acceda a la interfaz web con el dominio configurado y continúe con la instalación de los demás servicios según el orden necesario.
