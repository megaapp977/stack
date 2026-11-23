# 🚀 MEGA - Plataforma de Comunicación Omnicanal

## Mega Assistant

Los administradores pueden preguntar qué contactos enviaron más mensajes en un período reciente. Mega Assistant cuenta los mensajes públicos entrantes de todas las conversaciones de cada contacto y resume los temas observados en una muestra claramente indicada de textos recientes. El buscador de herramientas encuentra acciones por significado y muestra los parámetros necesarios para consultarlas o proponer cambios.

Al revisar las cajas de entrada, Mega Assistant distingue los canales sin consulta de salud de una conexión WhatsApp Cloud que requiere reautorizar su credencial; muestra esos resultados como diagnósticos y evita repetir la misma consulta sin cambios.

Antes de proponer un cambio, Mega Assistant comprueba que los datos estén completos y sean válidos. Si falta algo, lo corrige o lo pregunta en la misma respuesta, así no aparecen tarjetas de confirmación que después fallarían. Tampoco repite consultas que ya hizo ni duplica una propuesta pendiente.

Mega Assistant resuelve en una sola consulta los pedidos más frecuentes: conversaciones que esperan respuesta, la ficha completa de un contacto con sus conversaciones y últimos mensajes, un período comparado con el anterior por canal y el estado de Captain con sus asistentes, bandejas y escenarios. Para pedidos de varias partes arma primero un plan y responde por cada punto. Mientras trabaja muestra qué está consultando (bandeja, contacto, estado, período), calcula “hoy” y “la semana pasada” en la zona horaria del navegador y responde en el idioma de tu último mensaje. Varias propuestas de una misma respuesta se pueden confirmar o cancelar juntas. Los planes y las cuentas pueden elegir un modelo para tareas complejas, que atiende los pedidos de varias partes, diagnósticos y reportes comparativos y sirve de respaldo si el modelo principal falla.

Cuando un cambio se aplica a muchas conversaciones a la vez (resolverlas, asignarlas o etiquetarlas), al confirmarlo se aplica conversación por conversación y la tarjeta muestra cuántas cambiaron, cuántas ya lo tenían y cuáles no se pudieron cambiar y por qué, con un enlace a cada conversación. Puedes seguir conversando mientras se aplica, y el asistente informa el resultado al terminar.

Para pedidos sobre muchos registros (todas las conversaciones de un período, los mensajes que mencionan un pedido, todos los contactos con una etiqueta), Mega Assistant los selecciona todos en el servidor, hasta 5.000, da el total exacto y guarda la selección para los pasos siguientes: las conversaciones de esos mensajes, los contactos de esas conversaciones, preguntas de seguimiento sobre el mismo conjunto, o un solo cambio para todos que confirmas una vez.

Para juzgar lo que dicen las conversaciones (qué clientes pidieron un reembolso, cuáles son las más urgentes, cómo se sienten), Mega Assistant revisa las conversaciones seleccionadas una por una en segundo plano, las 100 más recientes por pedido, y una tarjeta muestra cuánto avanzó. Al terminar responde en el chat con lo que encontró, cuántas leyó y cuántas faltan, y ofrece continuar con las 100 siguientes. Las conversaciones que coinciden se pueden usar en el paso siguiente, como listar sus contactos o etiquetarlas todas. Cada conversación revisada se cobra al precio en AI Actions del modelo de la revisión; la revisión se detiene si la cuenta se queda sin ellas.

Mega Assistant sabe qué estás mirando. Con una conversación o un contacto abierto, “resume esto”, “transfiere esta conversación a Ventas” o “agrega una nota a este contacto” funcionan sin escribir ningún identificador; con conversaciones seleccionadas en la lista, “resuelve estas” actúa exactamente sobre esa selección. Solo se comparten referencias (el registro, los filtros de la lista y las conversaciones seleccionadas, nunca el texto de la página), y cada una se valida contra tus permisos antes de que el asistente la vea. Una línea sobre el campo de mensaje muestra qué va a usar el asistente, con un botón para ignorarlo. Las tarjetas de confirmación indican el registro que cambian, marcan cuando salió de tu pantalla y te avisan si ya no lo estás viendo; un cambio sobre un registro eliminado o al que perdiste acceso no se puede confirmar. También reconoce el tablero y la tarea de Kanban, el flujo abierto en el Flow Builder, la bandeja cuya configuración estás editando, los contactos que seleccionaste en la lista y el registro de las páginas de uno solo: el asistente de Captain, la sala de chat, la empresa, el portal del Centro de ayuda (con su idioma), el reporte de una campaña, de un agente, una bandeja, un equipo o una etiqueta, la app del panel, la política de capacidad, el monitor y la importación de datos. Cuando le pedís agendar algo, distingue un mensaje programado, una campaña, una tarea, un evento del calendario o posponer una conversación según lo que tiene que pasar en ese momento, y pregunta si no queda claro.

También sabe qué formulario tenés abierto encima de la página aunque la dirección no cambie: crear o editar una respuesta rápida, un atributo personalizado, un bot, una automatización, una campaña o un mensaje programado, y en Captain un asistente nuevo, una pregunta frecuente, un documento, un escenario, una regla, una herramienta o un servidor MCP. “Completá este formulario” o “cambiá esta campaña” se refieren a lo que tenés abierto, y si volvés a otra página deja de usarlo. Además puede cambiar lo que antes solo podía consultar: la encuesta de satisfacción de una bandeja (y crear su plantilla de WhatsApp), las plantillas de mensajes, las dashboard apps, los monitores de Captain, las ofertas de Kanban y tu propio perfil (nombre, nombre visible y firma; el email, la contraseña y la verificación en dos pasos se cambian en la página de perfil). Como todo cambio, primero te lo propone y lo confirmás.

Al confirmar un cambio, Mega Assistant vuelve a comprobar que todavía puedas hacerlo: si la función se desactivó o ya no tenés el rol que ese cambio requiere, no lo aplica. Si alguien modificó los valores que la tarjeta mostraba como actuales desde que se propuso, tampoco los pisa: te dice qué cambió y te lo propone de nuevo solo si todavía lo querés.

Después de aplicar un cambio confirmado, Mega Assistant vuelve a leer el registro y comprueba que haya quedado con los valores que envió. La tarjeta dice “Cambio aplicado y comprobado en el registro” o avisa si el registro muestra otros valores, y el asistente te lo cuenta en el chat sin afirmar más de lo que comprobó.

Antes de explicarte cómo configurar algo o de ofrecerte hacerlo, Mega Assistant consulta en tu cuenta si esa función está habilitada, si tu rol puede cambiarla y si existe una herramienta para hacerlo desde el chat. Si está desactivada o requiere otro rol, te lo dice y te explica quién puede habilitarla, sin prometerte configurarla; si no hay herramienta, te guía paso a paso en su pantalla. “¿Qué me podés configurar?” se responde con la lista real de módulos de tu cuenta y su estado.

Podés contarle lo que querés lograr con tus palabras, por ejemplo “quiero automatizar la atención por WhatsApp, responder preguntas frecuentes, detectar oportunidades de venta y derivar a una persona cuando haga falta”. Mega Assistant lo separa en necesidades, revisa qué módulos tenés disponibles y qué ya está configurado para reutilizarlo, te recomienda una solución explicando por qué, arma el plan y te pide solo los datos que faltan. Después lo configura paso a paso, con tu confirmación, comprobando cada resultado y siguiendo con el próximo paso.

Cuando preguntás “¿cómo funciona…?”, Mega Assistant responde desde la documentación funcional de cada módulo, que viaja con la aplicación y dice qué es, cómo funciona, sus requisitos, límites, cómo configurarlo y ejemplos, con la fecha en que se revisó y la sección de la documentación del producto de donde sale. Solo lee el módulo del que hablás, y si un módulo no tiene documentación lo dice en lugar de inventar menús u opciones.

Cuando una consulta se convierte en una configuración de varios pasos (“dale, configurémoslo”), Mega Assistant anota en el chat el objetivo, las decisiones que tomaste y los pasos que faltan. En los mensajes siguientes, al volver al chat o en una llamada de voz, sigue desde ahí con tus decisiones y solo te pregunta lo que falta; si cambiás de opinión, actualiza la decisión, y al terminar o abandonar la configuración la cierra. En Captain anota cada fase de la configuración y retoma en la primera pendiente. Es la memoria del chat, no un permiso: cada cambio se sigue proponiendo y confirmando.

Si retomás una configuración que dejaste hace días, Mega Assistant primero te confirma si todavía la querés y vuelve a leer cómo está configurado todo antes de seguir.

En una llamada de voz, cuando la respuesta muestra tarjetas, tablas o gráficos, la voz recibe también sus valores: dice las cifras que responden a lo que pediste (no solo que está en pantalla) y contesta preguntas de seguimiento como “¿y las resoluciones?” con esos mismos datos.

En el Flow Builder, Mega Assistant cambia un flujo existente bloque por bloque: agrega, modifica o quita solo los bloques y conexiones que le pedís y deja el resto exactamente como estaba. Antes de proponerlo revisa que el flujo siga siendo válido, y si alguien lo editó mientras tanto, confirmar el cambio no pisa esa edición. Nunca publica por su cuenta: publicar requiere que lo pidas y lo confirmes.

Para medir cómo funciona el asistente en cada cuenta, cada respuesta guarda cuánto tardó, cuántas herramientas usó, cuáles fallaron o fueron rechazadas por permisos, los módulos que se consultaron estando desactivados, sin permiso o sin documentación, y cómo terminó. Un reporte por cuenta junta eso con el costo de los modelos y con el resultado de los cambios confirmados (aplicados, rechazados al confirmar y comprobados en el registro).

Los administradores lo ven en la página del asistente, en la pestaña Métricas del historial (el ícono de gráfico), para los últimos 7, 30 o 90 días: respuestas, fallidas, sin fuente (respuestas largas que no leyeron datos ni documentación, una estimación), tiempo promedio y de las más lentas, costo, cambios aplicados, no aplicados, comprobados y con otros valores, y las herramientas y módulos que más fallan o se rechazan.

Las tarjetas de confirmación muestran qué hace cada cambio en términos simples (a quién se asigna una conversación, qué etiquetas se agregan o quitan, la tarea o el flujo que crea o modifica) y te dejan ajustar el equipo, el agente o las etiquetas antes de confirmar. Cada ajuste, tuyo o del asistente cuando dices “mejor a Soporte”, se convierte en una nueva revisión de la misma tarjeta, y solo la última se puede confirmar. Las tablas, los gráficos y otros resultados aparecen apenas están listos, se pueden actualizar en respuestas posteriores y se abren en una vista más grande. Los formularios y los pasos sugeridos envían exactamente lo que elegiste, validado contra el formulario que mostró el asistente.

Voz: el micrófono del campo de mensaje graba lo que dices, lo transcribe y lo envía como tu mensaje. El botón de ondas abre una conversación por voz en tiempo real: un círculo animado muestra si el asistente escucha, piensa o habla, puedes seguir escribiendo, silenciarte o cortar con la X. Lo que pides hablando pasa por el mismo asistente del chat, con las mismas herramientas, tarjetas y propuestas, y queda en el hilo como un mensaje escrito; el asistente te resume la respuesta en voz alta. Un “sí” hablado a una propuesta inicia en su tarjeta una cuenta regresiva de 5 segundos que puedes cancelar con la voz o con un clic; borrados, fusiones y cambios masivos siempre requieren el clic. La voz se cobra por bloques de 5 minutos en AI Actions y cada pedido cuenta como un mensaje. En Ajustes → Captain eliges la voz (Marin y Cedar recomendadas), la velocidad y, si tienes una, tu voz personalizada de OpenAI. Si refrescas la página durante una llamada, la siguiente reemplaza a la anterior. Durante una llamada puedes cambiar de pantalla: la llamada sigue en la mascota o, si no está abierta, en un pequeño control que ocupa el lugar de la mascota, con la mascota adentro y un aro de color (verde cuando escucha o habla, ámbar cuando trabaja, espera tu confirmación o el micrófono está silenciado), que dice «Llamada con …» y qué está haciendo, con silenciar, «Abrir chat» y colgar; se arrastra desde la mascota o el texto y mueve la mascota con él; solo termina cuando la cortas. La voz sabe en qué pantalla estás y recuerda lo que ya se habló en el chat, también en una llamada nueva. Conoce los nombres de la cuenta (tus contactos recientes, bandejas, equipos, agentes y etiquetas) para escribirlos como están guardados aunque suenen parecido, y si un nombre dicho no aparece, el asistente prueba cómo lo oyó la transcripción y sus partes antes de decir que no existe. El asistente puede abrir cualquier pantalla del panel para guiarte (por ejemplo, la configuración de una bandeja, un contacto o un asistente de Captain), por chat o por voz, solo entre las páginas que tienes permiso para ver y que la cuenta tiene habilitadas. Si un pedido tarda, la voz te va contando qué está haciendo (por ejemplo, que está buscando el contacto) en lugar de quedarse en silencio, sin hablarte encima. Mientras busca, un “gracias” recibe una respuesta breve sin cortar la tarea, “esperá” lo deja en silencio, una corrección (“solo las de WhatsApp”) se aplica apenas termina y “cancelá” detiene la búsqueda en el servidor. Cada usuario puede ponerle su propio nombre al asistente (en su perfil o pidiéndoselo: «de ahora en adelante quiero llamarte Río», que se guarda al confirmar), y el administrador puede darle un nombre para toda la cuenta en Ajustes → Captain; el mismo nombre se usa en la pantalla, en el chat y en la voz. Al conectar la llamada, el asistente saluda una sola vez con su nombre. Lo que dices en la llamada y lo que la voz te responde se escriben en el chat de la llamada, así el chat, el asistente escrito y la próxima llamada lo recuerdan (un pedido hablado queda como su mensaje de pedido; el saludo y los avisos de progreso no se escriben). Si confirmas o cancelas una propuesta con un clic durante la llamada, la voz se entera y te dice el resultado real. Mientras hay una llamada, el panel muestra siempre su chat: el botón de voz te lleva a ese chat en lugar de crear uno vacío. Si durante la llamada escribís un mensaje o adjuntás un archivo en el chat, es como si se lo dijeras: la voz te responde en voz alta, como el mismo asistente del chat (escribís "hola" y te contesta "¡Hola! ¿Qué tal?"), lee el archivo si hace falta y su respuesta queda escrita en el chat; lo que decís queda con tus palabras y lo que escuchás es lo mismo que queda escrito, en frases cortas; la voz sabe en qué pantalla estás mientras te movés por el panel; al retomar un chat, la llamada saluda nombrando de qué venían hablando.

Preferencias del asistente: en tu perfil eliges, solo para la cuenta en la que estás, el idioma de las respuestas (el de tu mensaje, o siempre español, inglés o portugués), el estilo (equilibrado, breve o detallado), cómo ver las listas de registros (automático, tabla o tarjetas) y si la llamada de voz empieza con un saludo hablado. Son opcionales y valen para el chat y la voz; son pistas de estilo, nunca permisos: no cambian lo que el asistente puede ver o hacer. El administrador puede escribir el saludo de la llamada en Ajustes → Captain, en la sección de voz: texto simple de hasta 200 caracteres, donde {name} se reemplaza por el nombre del asistente.

Privacidad y retención: tus preferencias y el nombre que le diste al asistente se guardan en tu usuario, separados por cuenta; solo se guarda lo que cambiaste, nunca se aprenden solas de tus conversaciones y se borran con «Borrar mis preferencias» (el nombre, dejándolo vacío). Como forman parte de los datos de tu usuario, otros miembros de la cuenta pueden leerlas a través de la API de agentes. De una llamada de voz guardamos el registro de la sesión (inicio, fin, modelo y bloques cobrados), los pedidos que la voz le pasó al asistente y sus respuestas escritas, y el texto de lo que dijiste y de lo que la voz respondió, como mensajes del hilo; los ves tú y los administradores de la cuenta, y se borran al borrar el hilo. El audio no se guarda. El audio viaja directo de tu navegador a OpenAI, y su retención sigue la política de datos de la API de OpenAI.

Los administradores ven junto a cada respuesta cuánto costó en llamadas al modelo, incluida cualquier revisión que haya iniciado. Mega Assistant además sabe qué significa cada estado y prioridad de conversación y juzga la urgencia o el tema leyendo las conversaciones, no solo por el campo de prioridad.

En pedidos que mezclan preguntas y cambios, reserva espacio para dejar los cambios propuestos aunque ya haya usado todas sus consultas, y responde cada punto pedido: resuelto, propuesto o pendiente y por qué. Si una consulta falla en el servidor, sigue con el resto en lugar de cortar la respuesta.

### Comportamiento actual (septiembre de 2026)

Este bloque tiene prioridad sobre los párrafos anteriores de esta sección.

- **Quién lo usa:** los administradores de la cuenta y los miembros cuyo rol personalizado incluye “Usar el asistente de IA”. Los administradores pueden leer los chats de su equipo con el asistente (solo lectura) desde la pestaña Equipo de la página completa; los chats ya no son privados de su dueño.
- **Historial:** buscador, Fijados, Hoy, Últimos 7 días y Anteriores, igual en la página completa y en el panel flotante. Un punto ámbar marca los chats con una acción esperando confirmación.
- **Acciones:** cada propuesta muestra una tarjeta con título, estado, destinatario, enlace a la conversación y vista previa del texto y los archivos que se van a enviar, o los campos que cambian con su valor actual y el nuevo. Los mensajes de texto se pueden enviar o dejar como borrador en el cuadro de respuesta.
- **Progreso y errores:** mientras responde, el asistente muestra las herramientas que usa. Las respuestas fallidas dicen el motivo (sin modelo de IA disponible, el servicio de IA no respondió).
- **Respuestas enriquecidas:** cuando pides un informe, una tabla, un gráfico o una comparación, el asistente responde con bloques visuales debajo del texto: texto, markdown, tabla (ordenable y exportable a CSV), métricas, tarjeta, gráfico (barras, línea, área, torta, dona), línea de tiempo, contacto, conversación, kanban, formulario, acciones sugeridas e informe HTML. Un informe ejecutivo se arma en el chat con bloques (métricas, gráfico, hallazgos, tabla) y el asistente ofrece la versión PDF como acción sugerida; el informe HTML solo se genera cuando lo pides, se abre solo en el canvas de la página completa y se descarga o se guarda como PDF desde la impresión del navegador. Los formularios y las acciones sugeridas responden en el mismo chat, así que el asistente mantiene el contexto. En el pet los bloques se adaptan al ancho: métricas en 2×2, tabla con 3 columnas ampliable y kanban deslizable. Los informes y los archivos PDF, HTML, Markdown y de texto se abren en un canvas: en la página completa es una columna a la derecha del chat (se puede seguir conversando) y en el pet se abre sobre la pantalla, con vista previa o código, descarga e impresión.
- **Planes y AI Actions:** cada respuesta completada descuenta las AI Actions del modelo que respondió (la respuesta automática después de confirmar no). Sin AI Actions, los mensajes se rechazan y los administradores ven un enlace para comprar un paquete; los administradores ven el saldo. Los planes pueden incluir el asistente solo para consultas o con acciones. Los administradores de cuentas sin el asistente ven qué ofrece y un enlace a los planes.

El sidebar de la página completa separa Fijados de Recientes: cada sección se contrae de forma independiente y los chats fijados no se repiten en Recientes. Fijados aparece solo cuando contiene chats; ambos grupos mantienen el orden por actividad más reciente.

Cada fila del historial en la página completa ofrece Renombrar, Fijar/Desfijar y Eliminar mediante un menú de tres puntos, disponible al pasar el cursor, enfocar con el teclado o tocar. Los títulos (1–100 caracteres sin espacios externos) y los chats fijados se conservan. Los fijados aparecen primero y cada grupo se ordena por actividad reciente descendente, con un máximo de 50 chats. Solo se pueden administrar los chats privados del usuario actual en la cuenta actual, con la función Mega Assistant habilitada. Eliminar requiere confirmación y borra permanentemente el chat, sus mensajes, acciones y archivos adjuntos. No se puede eliminar un chat mientras genera una respuesta o ejecuta una acción. Eliminar el chat seleccionado inicia uno nuevo y limpia su borrador y archivos; administrar otro chat conserva el chat y borrador actuales.

El historial del asistente comienza con Nuevo chat, seguido de una sección Recientes que se puede contraer y expandir, con los chats fijados primero y actividad descendente dentro de cada grupo. Abrir o renombrar una conversación antigua no cambia su orden por actividad; los nuevos mensajes actualizan su posición.

El nombre del asistente sigue tu Custom Branding: Brand Name + “Assistant”, por ejemplo “Acme Assistant”. Tu marca aparece de forma consistente en el sidebar, el chat y la ayuda de atajos. Sin un nombre configurado, se utiliza “Mega Assistant”.

La mascota muestra la imagen de Mega Assistant Pet configurada en Custom Branding, conservando sus proporciones y controles de arrastre. Usa por defecto la imagen incluida de Mega Assistant y es independiente del Logo Thumbnail.

El botón flotante de Copilot se oculta en la página completa de Mega Assistant y sigue disponible en el resto del dashboard.

El atajo solo aparece en la ayuda cuando la cuenta actual tiene habilitada la feature Mega Assistant, igual que el sidebar. No se ejecuta con la feature desactivada; abrir el chat también requiere disponibilidad del asistente.

Alt + Shift + M alterna el asistente flotante: si su chat está abierto, lo cierra y oculta la mascota; si no, la recupera y abre el chat. En la página completa enfoca el editor existente sin salir de la conversación.

Alt + Shift + M recupera la mascota oculta y abre su chat en las páginas del dashboard donde el asistente está disponible. En la página del asistente enfoca el editor existente. El control de cierre tiene una X más grande y contrastada; el atajo figura en la ayuda de teclado.

La mascota se puede ocultar con su propia X y volver a habilitar desde el encabezado de la página del asistente. El botón de expandir del chat flotante abre esa página con la misma conversación, borrador y adjuntos seleccionados. La preferencia de visibilidad se guarda en este navegador; el traslado del chat ocurre solo en memoria y no sobrevive a una recarga.

Al iniciar un chat vacío, la página centra el saludo y el editor. El replybox compartido usa la superficie sólida y el borde del editor de conversaciones, con relieve sutil y foco visible; al aparecer mensajes, permanece abajo.

El sidebar principal incluye una página completa del asistente con historial y conversación centrada. Comparte el editor redondeado con adjuntos con el panel flotante; la mascota se oculta mientras esta página está abierta.

Mega Assistant comienza con herramientas nombradas para contactos, conversaciones, conteos, bandejas de entrada y lecturas de Captain. Puede descubrir cualquier otra herramienta nombrada elegible de la cuenta en páginas explícitas y mantiene como máximo 40 herramientas nombradas activas a la vez. Las consultas de configuración requieren leer las APIs correspondientes, no solo enumerar rutas; una búsqueda vacía o parcial se informa como tal, no como prueba de que no exista un registro o capacidad. Captain se identifica como el módulo de IA de la plataforma; los resultados de lectura y los cambios propuestos quedan en el historial privado de acciones de la conversación.

En cada chat privado, Mega Assistant reutiliza las herramientas elegibles y mantiene estable el contexto inicial entre respuestas para que los proveedores compatibles puedan usar caché y reducir el costo.

Cuando una respuesta propone una acción, primero aparece el mensaje del asistente y, al terminar de mostrarse, la tarjeta de confirmación debajo.

La conversación acompaña a la mascota al moverla, se abre hacia el espacio disponible cerca de los bordes y mantiene ambos dentro de la pantalla. La cabecera compacta permite abrir el historial o iniciar una conversación; las sugerencias completan el mensaje sin enviarlo automáticamente.

Mega Assistant es un asistente privado de cuenta con mascota móvil, redimensionable y accesible por teclado, y un panel basado en Copilot. Descubre operaciones de la cuenta, responde con resultados de APIs autenticadas y propone cambios para confirmación explícita. Los conteos usan totales de API, no tamaños de página. No requiere servidor MCP, token ni permiso de API pública.

Los proveedores se asignan independientemente a Captain y Mega Assistant. Las tarjetas de modelos de la cuenta en Super Admin seleccionan chat, imágenes/PDF y transcripción de audio por cuenta. Permite hasta cinco imágenes, PDF, documentos de texto o audios (20 MB cada uno) con el botón +, arrastrándolos y soltándolos sobre el cuadro de texto o pegándolos (por ejemplo, una captura de pantalla). Los archivos e historiales son privados para su propietario. Las acciones confirmadas muestran su resultado real y no se ejecutan dos veces. Si un servidor se reinicia mientras el asistente responde, la respuesta se retoma sola en pocos minutos en lugar de quedar colgada. Incluye dictado y voz en tiempo real (ver Voz); no incluye telefonía.

## Tu Centro de Comando para la Atención al Cliente del Futuro

Las tarjetas de proveedores IA resumen cantidad de modelos, capacidades verificadas y avisos de saldo. Modelos y pruebas abre un modal con los usos asignados, el estado y los errores guardados de cada modelo, sin expandir la cuadrícula. Se conservan las acciones de probar, editar y eliminar con sus protecciones.

Razonamiento y herramientas funcionan juntos en todos los proveedores: cada modelo recibe el razonamiento en el formato que acepta su API (un nivel, un presupuesto de razonamiento o nada si no razona), y los modelos de OpenAI se llaman por la Responses API. Los proveedores compatibles con OpenAI eligen un preset: OpenRouter, xAI, DeepSeek, Mistral, Perplexity, Ollama y GPUStack usan su propia integración, mientras que Groq, Together, Fireworks, DeepInfra, Cerebras, SambaNova, Qwen, Z.ai, vLLM, LM Studio o cualquier gateway personalizado se conectan como gateway genérico, y la prueba de capacidades detecta por modelo qué API usan (Responses o Chat Completions).

El formulario de proveedores está centrado. Un botón visible de carga múltiple abre un modal para pegar modelos y elegir capacidades; Cancelar o Escape lo cierra sin agregar filas.

Agregar/editar proveedor utiliza conexión en dos columnas y una tabla compacta de modelos. La carga múltiple acepta nombres separados por líneas o comas y capacidades compartidas; los nombres existentes se combinan sin duplicar filas.

Las selecciones del catálogo antiguo siguen disponibles para sus funciones originales al editar un proveedor importado. Las nuevas selecciones calificadas por proveedor requieren capacidades asignadas y verificadas. PDF/audio legacy resuelven las credenciales actuales de OpenAI nativo y recurren a la configuración de instalación si no existe un proveedor nativo activo. Audio prioriza la integración OpenAI de la cuenta; el respaldo de Captain requiere la función habilitada y cuota disponible. Las grabaciones conservan su flujo especializado.

Una corrección de actualización recupera una sola vez las entradas faltantes `whisper-1`, `gpt-4o-mini-transcribe` y `text-embedding-3-small` en el proveedor nativo con identificador `openai`. Conserva credenciales, modelos personalizados, asignaciones existentes, resultados de pruebas y selecciones de cuentas. Las entradas recuperadas quedan configuradas, no verificadas automáticamente; seleccionarlas con identificador de proveedor sigue requiriendo pruebas. La corrección puede recuperar una entrada base eliminada anteriormente, pero no vuelve a agregarla al guardar normalmente. No agrega modelos marcados como próximos.

Los modelos que OpenAI retira (la serie GPT-4.1, `gpt-4o`, `whisper-1`, `gpt-4o-mini-transcribe` y `gpt-4o-transcribe`) se reemplazan por GPT-6 Luna en texto y por GPT Transcribe en audio. Las funcionalidades de Captain usan Luna por defecto (Copilot usa GPT-5.1) y la ejecutan sin razonamiento salvo que AI Providers indique otro esfuerzo para el modelo. Una migración pasa a Luna o GPT Transcribe las elecciones guardadas en cuentas, planes y configuración de la instalación; una elección con proveedor solo pasa al mismo proveedor si este ya verificó el reemplazo, y el Mega Assistant conserva su elección hasta que se verifique. Los proveedores OpenAI reciben ambos modelos con precio (GPT Transcribe US$0,0045 por minuto) y sin verificar: hay que probarlos en AI Providers. La transcripción con diarización de llamadas sigue en `gpt-4o-transcribe-diarize` porque OpenAI no publicó un reemplazo. Las listas de modelos de Captain y de IA también ofrecen GPT-6 Sol y GPT-6.1 Terra.

La regeneración de FAQ conserva las respuestas existentes ante errores o resultados vacíos. Solo reemplaza respuestas no editadas cuando hay resultados válidos, en una transacción que revierte el reemplazo si falla alguna inserción. Para PDF legacy, comprueba el archivo remoto y, únicamente ante un 404, vuelve a subir el original conservado usando las mismas credenciales de la generación. Los errores de permisos, saldo o conexión no provocan otra subida; si falta el original, se conserva el conocimiento anterior.

El formulario muestra cada modelo una sola vez, con casillas de Chat, PDF, Audio y Embeddings. Solo se prueban las capacidades marcadas. Se conservan las selecciones y verificaciones existentes; los modelos sin capacidad muestran una indicación para seleccionarla. Cambiar credenciales o endpoint requiere verificar nuevamente.

Las pruebas usan un PDF válido de una página y un WAV PCM de un segundo. La muestra de audio silenciosa comprueba la aceptación del archivo, no la precisión de la transcripción.

Las pruebas de modelos muestran en la card el saldo insuficiente o la cuota agotada informados por el proveedor. Estos resultados no demuestran incompatibilidad del modelo; recarga o revisa la facturación y vuelve a probar.

Las grabaciones de llamadas Twilio Voice se pueden transcribir opcionalmente, mostrar junto a la grabación y encontrar en la búsqueda de conversaciones.

**Versión:** Enterprise
**Basado en:** Plataforma MEGA y funcionalidades exclusivas de MEGA
**Última Actualización:** 1 de septiembre de 2026

---

### APIs verificadas e listas para Postman

Swagger/OpenAPI 3.1 mantiene paridad automática con las rutas soportadas y genera una colección Postman separada por token de cuenta, token de aplicación de plataforma y rutas públicas.

## 📋 Índice

1. [Canales de Comunicación](#-canales-de-comunicación)
2. [Gestión de Conversaciones](#-gestión-de-conversaciones)
3. [Comunicación Interna del Equipo](#-comunicación-interna-del-equipo)
4. [Automatización e IA](#-automatización-e-ia)
5. [CRM y Gestión de Contactos](#-crm-y-gestión-de-contactos)
6. [Campañas Masivas](#-campañas-masivas)
7. [Centro de Ayuda (Help Center)](#-centro-de-ayuda-help-center)
8. [Reportes y Analíticas](#-reportes-y-analíticas)
9. [Gestión de Equipos](#-gestión-de-equipos)
10. [Integraciones](#-integraciones)
11. [Funcionalidades Enterprise](#-funcionalidades-enterprise)
12. [Funcionalidades Exclusivas Mega](#-funcionalidades-exclusivas-mega)

---

## 📱 Canales de Comunicación

- **Identificación clara de bandejas** *(Mega)* - Las listas y la barra lateral muestran el nombre de cada bandeja junto a su identificador público (teléfono, email o URL). Los IDs de página de Facebook y de perfil de X siguen disponibles para operaciones del proveedor, pero no se muestran. La búsqueda también admite los identificadores visibles.
- **Identidad social conservada** *(Mega)* - Las bandejas de Facebook, Instagram y TikTok guardan el nombre de su página o usuario de proveedor sin sobrescribir el nombre personalizado de la bandeja al reconectar el canal.

### WhatsApp Business

- **Contactos brasileños sin duplicados** *(Mega)* - Cloud, coexistencia, Twilio WhatsApp y llamadas Cloud reutilizan contactos móviles existentes cuando el proveedor omite el noveno dígito; las coincidencias exactas tienen prioridad y los teléfonos fijos no generan alternativas móviles.

Conecta con tus clientes a través del canal de mensajería más popular del mundo.

- **WhatsApp Cloud API** - Integración oficial de Meta con todas las funcionalidades empresariales
- **Recuperación del registro de WhatsApp Cloud** *(Mega)* - Completa la conexión desde la misma bandeja con pasos separados para verificar el número por SMS o llamada y registrar su PIN de dos pasos. Si no hay PIN guardado, se solicita uno; un PIN olvidado se recupera en Meta. El estado de conexión refleja el estado del número informado por Meta.
- **Conectividad premium para llamadas Cloud** *(Mega)* - Las empresas con redes restrictivas pueden usar STUN/TURN administrado como relay para las llamadas WebRTC de WhatsApp Cloud
- **Configuración manual guiada de WhatsApp** *(Mega)* - Los administradores pueden preparar su propia aplicación de Meta, validar un número de producción, el ID de WABA y un token permanente antes de crear una bandeja Cloud; el flujo muestra el estado del webhook/suscripción y permite reintentar el webhook sin salir de la configuración
- **Registro integrado para coexistencia con WhatsApp Business App** *(Mega)* - El registro integrado permite dar de alta un número de WhatsApp Business App, incluidas finalizaciones de coexistencia sin ID de número de teléfono, mientras MEGA configura la conexión y los webhooks requeridos
- **Mega Hub para WhatsApp** *(Mega)* - Conexión opcional con apps compartidas desde Super Admin, usando credenciales dedicadas del Hub, webhooks reenviados, salud basada en el forward y sin configuración manual de callback/token
- **WhatsApp Evolution** *(Mega)* - Conexión directa sin API oficial, ideal para cuentas personales
- **WhatsApp WAHA** *(Mega)* - Proveedor alternativo con soporte completo de mensajes multimedia
- **WhatsApp Uazapi** *(Mega)* - Solución de bajo costo para múltiples líneas
- **Alertas de salud de conexión** *(Mega)* - Los problemas de token y sesión aparecen en listas de bandejas, barra lateral principal y configuración de la bandeja con acceso directo a configuración de sesión
- **Resiliencia de salud del número** *(Mega)* - La salud del número de Cloud API sigue disponible cuando no se pueden actualizar los datos de la cuenta empresarial vinculada
- **Perfil comercial de WhatsApp en Salud de la cuenta** *(Mega)* - Salud de la cuenta muestra el perfil comercial de solo lectura que ven los clientes, orientación clara sobre la revisión del nombre y el límite de mensajería compartido por el portafolio
- **Reconexión manual de WhatsApp** *(Mega)* - Las bandejas elegibles del registro integrado se pueden reconectar a tu propia aplicación de Meta mediante un flujo guiado que conserva la bandeja y su historial de atención
- **Reconfiguración del registro integrado** *(Mega)* - Los administradores pueden actualizar las credenciales y la configuración de WhatsApp Business de una bandeja Cloud existente conectada por registro integrado sin habilitar una función de cuenta; la función de creación se mantiene solo para bandejas nuevas
- **Arquitectura multi-servidor** *(Mega)* - Configura varios servidores por proveedor con resolución automática de credenciales
- **Capacidad por servidor** *(Mega)* - Define límites por servidor para distribuir carga operativa
- **Soporte BSUID** *(Mega)* - Identificación robusta del contacto y envío confiable incluso sin `wa_id` tradicional
- **Llamadas y adjuntos más confiables en WhatsApp Cloud** - Los adjuntos se suben a Meta antes de enviarse (menos fallos por límite de descargas), las llamadas llegan también a contactos que solo tienen BSUID, Messenger recibe los botones de Get Started y la etiqueta HUMAN_AGENT se usa solo cuando corresponde
- **Mensajes no soportados por proveedor** *(Mega)* - Distingue contenido no compatible de mensajes no disponibles por coexistencia; solo estos últimos indican revisar WhatsApp Business
- **Mensajes de plantilla** - Envía mensajes fuera de la ventana de 24 horas con plantillas aprobadas; las automatizaciones bloquean localmente el texto libre en ese estado y muestran una indicación para usar una plantilla
- **Direct Send de WhatsApp Cloud (beta)** *(Mega)* - Con la bandeja habilitada por Meta en la beta, el botón de WhatsApp de la caja de respuesta y de nueva conversación permite elegir entre plantilla y Direct Send: un formulario para enviar un mensaje de utilidad sin elegir plantilla, también fuera de la ventana de 24 horas, con hasta 3 botones de respuesta, un botón de enlace o un botón para llamar por WhatsApp, encabezado de texto, imagen, video o documento, pie opcional y plazo de entrega. Meta crea las plantillas por su cuenta. Por API también se puede fijar el nombre de la plantilla y enviar códigos de verificación (mensajes de autenticación) cuando Meta los habilita en la cuenta. La Salud de la Cuenta indica si la bandeja probablemente califica (límite de mensajes de 100.000 o ilimitado); el switch solo aparece en ese caso y Direct Send se apaga si la bandeja deja de calificar. El texto libre sigue necesitando plantilla fuera de la ventana. Se activa por bandeja
- **Mensajes interactivos de WhatsApp Cloud** *(Mega)* - Mientras la ventana de 24 horas está abierta, el botón de WhatsApp de la caja de respuesta y del formulario de nueva conversación ofrece "Mensaje interactivo": un formulario con vista previa estilo WhatsApp para enviar hasta 3 botones de respuesta, una lista de hasta 10 opciones con descripción, un botón de enlace, un carrusel de 2 a 10 tarjetas con imagen o video, un cobro Pix (código copia e cola con monto, para Brasil) o un pedido de ubicación, con encabezado de texto, imagen, video o documento y pie opcionales. Los archivos se suben desde el mismo formulario o se pega una URL pública. Todos los campos aceptan las variables de la plataforma (`{{contact.first_name}}`, atributos personalizados, etc.). En la conversación se muestran como los templates, con su encabezado, pie y botones, la lista se puede desplegar, el carrusel se desliza y el Pix permite copiar el código. También disponibles por API de mensajes, Outbound Messages (`type: interactive`), MCP y Mega Assistant, documentados en Swagger/OpenAPI y Postman.
- **Mensajes interactivos de WAHA** *(Mega)* - Las bandejas WAHA envían mensajes interactivos en cualquier momento, sin ventana de 24 horas: botones de respuesta (hasta 3), botones de acción (abrir enlace, llamar o copiar código, hasta 5), lista, carrusel con imagen por tarjeta, cobro Pix (el cliente escribe el monto), pedido con "Revisar y pagar" (productos, descuento, total y clave Pix), encuesta (una o varias respuestas), ubicación, evento con fecha y lugar, y respuesta a un mensaje de botones (solo por API). El ícono de WhatsApp de la caja de respuesta y de nueva conversación abre el mismo formulario con vista previa que WhatsApp Cloud, en escritorio y teléfono, con encabezado de texto, imagen, video o documento. Carrusel, Pix, pedido y evento necesitan el motor GOWS. Solo en chats directos: en grupos la opción no aparece. En la conversación se muestran como los templates, y las respuestas del cliente (botón tocado, opción de lista, voto de encuesta o respuesta al evento) entran como mensajes. Se habilita por servidor WAHA en Super Admin → Proveedores WA (interruptor *Mensajes interactivos*) o para toda la instalación con `WAHA_INTERACTIVE_MESSAGES=true`, y por cuenta con la feature *WAHA Interactive Messages*. También por API de mensajes, Outbound Messages y MCP, con los 10 ejemplos en Swagger/OpenAPI, Postman y la documentación de la API del Super Admin.
- **Mensajes interactivos de UazAPI** *(Mega)* - Las bandejas UazAPI envían mensajes interactivos en cualquier momento, sin ventana de 24 horas, en chats directos y grupos: botones de respuesta, botones de acción (abrir enlace, llamar o copiar código), lista con secciones, encuesta, carrusel con imagen, video o documento por tarjeta, botón Pix, solicitud de pago con "Revisar y pagar" (monto, producto, factura, clave Pix, boleto, enlace de pago y PDF adjunto), evento con fecha, lugar, enlace y recordatorio, y pedido de ubicación. El ícono de WhatsApp de la caja de respuesta y de nueva conversación abre el mismo formulario con vista previa, en escritorio y teléfono; los botones llevan encabezado de imagen, video o documento. En la conversación se muestran como los templates; las respuestas del cliente (botón tocado, opción de lista, voto de encuesta, respuesta al evento) entran como mensajes que citan el original, y el agente puede enviar al cliente el estado del pedido (pago solicitado, en preparación, enviado, entregado, completado o cancelado, pagado o pendiente) desde la burbuja de la solicitud de pago. El adicional puede venderse por toda la cuenta o por bandeja: en ese caso cada unidad activa los mensajes interactivos en una bandeja (switch *Mensajes interactivos* en la configuración de la bandeja) y las demás lo muestran bloqueado hasta comprar otra unidad; lo mismo vale para los interactivos de WAHA. Se habilita por servidor UazAPI en Super Admin → Proveedores WA (interruptor *Mensajes interactivos*) o para toda la instalación con `UAZAPI_INTERACTIVE_MESSAGES=true`, y por cuenta con la feature *UazAPI Interactive Messages*. También por API de mensajes, Outbound Messages, MCP de cuenta y Mega Assistant, con 11 ejemplos en Swagger/OpenAPI, Postman y la documentación de la API del Super Admin.
- **Marcar chats como leídos en WhatsApp (UazAPI)** *(Mega)* - Opción por bandeja UazAPI, apagada por defecto, en la tarjeta *Chats* de la configuración: cuando un agente abre una conversación con mensajes sin leer o se envía una respuesta al cliente, el chat queda como leído en el celular de la línea (se limpia el contador de no leídos). El contacto ve los tildes azules solo si la cuenta de WhatsApp tiene activadas las confirmaciones de lectura en su privacidad.
- **Id de la opción elegida en las respuestas de WhatsApp** *(Mega)* - Cuando el cliente elige una opción de lista o toca un botón de respuesta (WhatsApp Cloud, WAHA y UazAPI), el mensaje guarda el id con que se envió esa opción, además de su texto. Las integraciones que mandan listas o botones por la API o por Outbound Messages reciben ese id en el webhook y en la API de mensajes y saben exactamente qué opción se eligió. Documentado en Swagger/OpenAPI, Postman y la documentación de la API del Super Admin. Los botones de respuesta también pueden llevar un id propio (`{ id, title }`), no solo las listas.
- **Sincronización de contactos** - Mantén tu base de datos actualizada automáticamente
- **Compartir contactos** *(Mega)* - Envía un contacto guardado como tarjeta de contacto nativa de WhatsApp desde el cuadro de respuesta (Cloud, WAHA, Uazapi, NotificaMe y Twilio WhatsApp); los contactos recibidos se reenvían con nombre y teléfono
- **Soporte de grupos** - Gestiona conversaciones de grupos de WhatsApp directamente

**Tracking de Anuncios WhatsApp:**

Mide el ROI de tu publicidad de WhatsApp:

- **Anuncios Click-to-WhatsApp** - Detecta conversaciones originadas desde anuncios de Facebook/Instagram
- **Captura de datos del anuncio** - Guarda automáticamente la fuente, campaña e información creativa
- **Indicador visual** - Ve la tarjeta de información del anuncio en la conversación
- **Atribución** - Conecta leads con campañas publicitarias específicas

**Gestión de Miembros de Grupos:** *(Mega)*

Control completo de los grupos de WhatsApp directamente desde MEGA:

- **Lista de miembros** - Visualiza todos los participantes del grupo con su rol y estado
- **Sincronización automática** - Los miembros se sincronizan automáticamente al crear la conversación
- **Añadir participantes** - Agrega nuevos miembros al grupo desde la plataforma
- **Eliminar participantes** - Remueve miembros del grupo sin salir de MEGA
- **Cambiar roles** - Asciende o degrada miembros a administrador
- **Menciones en grupo** - Usa @ para mencionar miembros específicos en mensajes, incluso al editar mensajes de grupos WAHA
- **Búsqueda de miembros** - Encuentra rápidamente participantes en grupos grandes
- **Paginación inteligente** - Carga eficiente para grupos con muchos miembros
- **Avatares de miembros** - Visualiza la foto de perfil de cada participante
- **Sincronización en segundo plano** - Actualización periódica de nombres y fotos
- **Soporte multi-proveedor** - Funciona con Evolution, WAHA, Uazapi y Cloud API

### Instagram Direct

Conecta con tu audiencia de Instagram y convierte seguidores en clientes desde el lugar donde ya interactúan con tu marca.

**¿Por qué Instagram?**

Con más de 2 mil millones de usuarios activos, Instagram es esencial para marcas visuales. El 90% de los usuarios siguen al menos una empresa, y los DMs son el canal preferido para consultas.

**Tipos de interacciones soportadas:**

- **Mensajes directos (DMs)** - Responde a consultas privadas de tus seguidores
- **Mega Hub para Instagram** *(Mega)* - Conecta Instagram mediante apps compartidas del Hub, usando credenciales dedicadas configuradas en Mega Hub
- **Respuestas a Stories** - Atiende a quienes reaccionan a tus historias
- **Respuestas a Stories con contenido** - Ve imágenes y videos adjuntos cuando responden a tus stories
- **Menciones en Stories** - Recibe alertas cuando te mencionan
- **Reacciones** - Visualiza cuando reaccionan a tus mensajes

**Tracking de anuncios:**

Una funcionalidad poderosa para medir el ROI de tu publicidad en Instagram:

- **Origen del lead** - Detecta automáticamente si el mensaje viene de un anuncio
- **Datos de la campaña** - Guarda qué anuncio generó cada conversación
- **Atribución automática** - Conecta ventas con campañas específicas
- **Métricas claras** - Sabe exactamente cuántos leads genera cada anuncio

**Ventana de respuesta extendida:**

- **7 días para responder** - En lugar de las 24 horas estándar, tienes hasta 7 días para responder
- **Activación automática** - Se aplica sin configuración adicional

**Contenido multimedia:**

- **Imágenes y videos** - Envía y recibe contenido visual
- **Respuestas rápidas** - Botones para que el cliente elija opciones
- **Catálogos de productos** - Envía productos directamente en el chat
- **Sugerencias de conversación** - Ayuda al cliente a iniciar la charla

**Beneficios para tu negocio:**

- Convierte seguidores en compradores
- Atención al cliente donde ya están tus fans
- Mide el impacto de tu publicidad en Instagram

### Facebook Messenger

Atiende a tus clientes directamente desde la app de mensajería más utilizada del mundo, integrada con tus páginas de Facebook.

**¿Por qué Facebook Messenger?**

Con más de 1.3 mil millones de usuarios activos, Messenger es el canal preferido para que los clientes contacten a las empresas. Tus clientes pueden escribirte desde tu página de Facebook, anuncios o directamente desde la app.

**Funcionalidades principales:**

- **Conexión en minutos** - Vincula tu página de Facebook con un par de clics, sin configuración técnica
- **Mega Hub para Messenger** *(Mega)* - Usa apps compartidas del Hub como alternativa configurable con credenciales dedicadas del Hub
- **Múltiples páginas** - Gestiona todas tus páginas de Facebook desde una sola plataforma
- **Nombres de contacto fieles** - Conserva el nombre proporcionado por Facebook sin inventar partes faltantes
- **Confirmaciones de lectura** - Sabe cuándo el cliente leyó tu mensaje
- **Confirmaciones de entrega** - Verifica que tus mensajes llegaron correctamente
- **Mensajes de bienvenida** - Saluda automáticamente a los clientes que te escriben por primera vez
- **Integración con bots** - Combina respuestas automáticas con atención humana de forma fluida
- **Vinculación con Instagram** - Conecta tu cuenta de Instagram asociada para gestionar ambos canales

**Beneficios para tu negocio:**

- Responde donde tus clientes ya están
- Historial completo de conversaciones con cada cliente
- Transición fluida entre chatbots y agentes humanos
- Métricas de rendimiento por canal

### Comentarios de Facebook e Instagram *(Mega)*

Atiende los comentarios de tus publicaciones, reels y anuncios desde la misma bandeja donde ya respondes los mensajes directos.

**Funcionalidades principales:**

- **Comentarios en la conversación** - Cada comentario llega como un mensaje en la conversación de quien lo escribió, junto a sus mensajes directos, con la tarjeta de la publicación (foto, texto y enlace para abrirla, guardada en la plataforma para que no se pierda), como los anuncios de WhatsApp
- **Respuesta pública desde el comentario** - Responde desde el menú del mensaje («Responder comentario») y la respuesta se publica debajo de él, visible para todos
- **Mensaje privado** - Pasa la conversación al privado con un mensaje directo a quien comentó (uno por comentario, dentro de los 7 días)
- **Moderación** - Oculta, vuelve a mostrar o elimina comentarios sin salir de la plataforma
- **API, MCP y Mega Assistant** - Responde en público o en privado, oculta y elimina comentarios por la API (también con `comment_reply` en Outbound Messages, solo con el id del comentario), desde el servidor MCP de la cuenta y con Mega Assistant; todo documentado en OpenAPI/Swagger y Postman, visible en la documentación de la API de Super Admin
- **Del comentario al DM con Flow Builder** - Un flujo puede empezar con cada comentario (por publicación o por palabras clave), y los flujos de "Mensaje recibido" y los bots pueden atender también los comentarios; desde el flujo se responde en público, se envía el mensaje privado, se oculta o se elimina el comentario
- **Activación por bandeja** - Cada bandeja de Facebook o Instagram decide si recibe comentarios con "Recibir comentarios de publicaciones y reels" (apagado por defecto; sin él, los comentarios no entran) y si solo toma los comentarios principales
- **Conversaciones para el bot o para el equipo** - Una conversación que abre un comentario queda pendiente cuando el bot de Flow Builder de la bandeja incluye comentarios; si no, se abre para los agentes

### TikTok Business

Conecta con la audiencia más joven y dinámica del mundo a través de TikTok, la red social de mayor crecimiento.

**¿Por qué TikTok?**

Con más de mil millones de usuarios activos, TikTok se ha convertido en una plataforma esencial para llegar a las generaciones Z y Millennials. Ahora puedes atender consultas de clientes que te contactan a través de mensajes directos.

**Funcionalidades principales:**

- **Mensajes de texto** - Envía y recibe mensajes con tus seguidores
- **Imágenes** - Comparte y recibe contenido visual
- **Stickers** - Visualiza los stickers que te envían tus clientes
- **Posts compartidos** - Cuando un cliente comparte un post contigo, lo ves directamente en la conversación
- **Respuestas a mensajes específicos** - Responde en contexto a mensajes anteriores
- **Perfil social del contacto** - Ve el perfil de TikTok del cliente directamente en sus datos
- **Mensajes no soportados** - Indicadores claros cuando se recibe contenido no compatible
- **Versión de API configurable** - Flexibilidad para adaptarse a diferentes versiones de la API

**Beneficios para tu negocio:**

- Llega a la audiencia más joven donde pasan su tiempo
- Convierte interacciones sociales en oportunidades de venta
- Conexión segura y oficial mediante la API de TikTok Business
- El acceso para conectar TikTok se controla por cuenta; las cuentas alojadas sin acceso pueden solicitarlo al soporte desde la configuración del inbox.
- Sincronización completa de mensajes en tiempo real

### Email

El email sigue siendo uno de los canales más importantes para la comunicación empresarial. Gestiona todos tus correos como si fueran conversaciones de chat.

**¿Por qué integrar Email?**

Muchos clientes prefieren el email para consultas formales, documentación o seguimiento. Con MEGA, todos tus emails se gestionan junto con el resto de canales.

**Funcionalidades principales:**

- **Email más confiable** - Sin correos duplicados cuando se solapan las descargas IMAP, nombres de remitente con comas que ya no rompen el envío, SMTP sin necesidad de IMAP (bandejas por reenvío) y búsqueda por asunto, que además se ve en el encabezado de la conversación
- **Bandeja unificada** - Todos los correos aparecen como conversaciones junto a WhatsApp, redes sociales y más
- **Respuestas enriquecidas** - Envía emails con formato, imágenes y adjuntos
- **Archivos grandes por email** *(Mega)* - El Super Admin define el tamaño máximo de adjunto en respuestas de email; lo que pasa de 20 MB en total llega al cliente como link de descarga y el editor se lo avisa al agente
- **Archivos grandes al iniciar una conversación por email** *(Mega)* - La ventana de nueva conversación usa el mismo tamaño máximo de adjunto que las respuestas de email, sube los archivos directo al almacenamiento cuando la subida directa está activa y avisa cuando los adjuntos pasan de 20 MB y llegarán como enlaces de descarga; los adjuntos también se pueden arrastrar y soltar sobre la ventana
- **Imágenes inline redimensionables** - Inserta imágenes en el cuerpo del email y ajusta su tamaño visualmente
- **Imágenes dentro del email** *(Mega)* - Las imágenes del cuerpo y de la firma del agente viajan dentro del email de respuesta, así Outlook y otros clientes que bloquean imágenes remotas las muestran sin pedir permiso; las que superan el límite siguen como enlace
- **Tablas en respuestas de email** - Inserta una tabla desde el menú del editor, edítala en el lugar y envíala como una tabla con bordes que se ve igual en Gmail y Outlook, claro u oscuro
- **Reenviar por email** - Desde cualquier mensaje de una conversación de email, reenvíalo a nuevos destinatarios (Para, Cc, Cco) con tu nota, el email original que puedes editar y los adjuntos que conserves; sale como un email nuevo (Fwd:), el contacto no lo recibe y las respuestas de cada destinatario abren su propia conversación. El Reenviar a contactos de siempre sigue igual
- **Asunto personalizado** - Las respuestas de email muestran un campo Asunto con "Re: <asunto>" (o el último asunto que cambiaste); edítalo para enviar esa respuesta con otro asunto
- **Otros destinatarios en CC** - Al responder un email dirigido a varias personas, los demás destinatarios del campo Para de ese email quedan en CC, así nadie sale del hilo
- **Firmas personalizadas** - Configura firmas profesionales por agente o por bandeja
- **Cualquier proveedor** - Conecta Gmail, Outlook, tu servidor propio o cualquier email
- **Configuración guiada** - Detecta Gmail u Outlook desde tu dominio para sugerir la integración correcta
- **Verificación de conexión Gmail** - Comprueba IMAP y SMTP en vivo, consulta la actividad reciente y reconecta la cuenta desde la configuración de la bandeja
- **Eliminación permanente sincronizada con Gmail** - Al eliminar un correo o conversación de una bandeja Gmail, también se elimina permanentemente en Gmail
- **Historial completo** - Todo el hilo de correos visible en una sola conversación
- **Respuestas citadas** - Con las respuestas citadas activas en la cuenta, cada respuesta de email lleva el hilo anterior detrás de una vista previa "…" contraída bajo el editor; quítalo en un mensaje y recupéralo con Cmd/Ctrl+Z. El texto citado del cliente nunca se evalúa como variables

**Beneficios para tu negocio:**

- Un solo lugar para emails y mensajería instantánea
- Los agentes no necesitan cambiar entre aplicaciones
- Métricas unificadas de todos los canales

### Widget Web (Live Chat)

Ofrece atención instantánea a los visitantes de tu sitio web con un chat en vivo elegante y completamente personalizable.

**¿Por qué Live Chat?**

Los visitantes de tu web quieren respuestas inmediatas. Un chat en vivo aumenta las conversiones hasta un 40% y mejora la satisfacción del cliente.

**Configuración del formulario:**

- **Widget más liviano y privado** - El pedido de email ya no se duplica, los crawlers no crean contactos, las páginas públicas no dejan cookie de sesión y el panel no aparece en buscadores
- **Formulario pre-chat** - Recolecta nombre, email y teléfono antes de iniciar
- **Campos personalizados** - Añade los campos que necesites para tu negocio
- **Validación automática** - Asegura que los datos ingresados son correctos; las casillas obligatorias deben estar marcadas antes de enviar
- **Modo offline** - Recibe mensajes incluso cuando no hay agentes disponibles

**Personalización visual completa:**

- **Colores de tu marca** - Ajusta colores primarios y de fondo
- **Tu logo** - Muestra tu marca en el widget
- **Posición flexible** - Esquina izquierda o derecha
- **Icono personalizado** - Cambia el botón flotante
- **Mensaje de bienvenida** - Saluda proactivamente a los visitantes

**Funcionalidades avanzadas:**

- **Identificación de usuarios** - Reconoce usuarios logueados en tu sitio
- **Datos del contacto protegidos** - El widget no recibe el email, el nombre ni el teléfono guardados del contacto: solo sabe cuáles existen, para decidir qué pedir en el formulario pre-chat. Los mensajes que envía el visitante tampoco llevan sus datos.
- **Contactos identificados protegidos** - Si un visitante escribe en el formulario pre-chat o en el pedido de email un email o teléfono que pertenece a un contacto identificado por tu sitio, los contactos no se fusionan y ese dato no se guarda: los agentes ven una nota privada en la conversación con el dato y un enlace al contacto que coincide. La fusión solo ocurre cuando el visitante llega identificado con el mismo identificador.
- **Transcripción por email** - El cliente puede solicitar el historial de la conversación; los reenvíos se deshabilitan temporalmente después de un envío exitoso
- **Modo oscuro** - Se adapta a las preferencias del visitante
- **Mensajes del visitante con formato** - Las listas que envía el visitante muestran sus viñetas y números
- **Help Center integrado** - Muestra artículos de ayuda directamente en el widget
- **Mensajes predefinidos** - Inicia conversaciones con contexto
- **Imágenes inline en respuestas** - Envía capturas o recursos visuales dentro del cuerpo del mensaje y ajusta su tamaño
- **Dominios permitidos** - Restringe el widget a dominios autorizados para mayor seguridad
- **Mostrar nombre del agente** - Configura por inbox si el nombre del agente se muestra al visitante
- **Control de autoasignacion por respuesta** - Desactiva por inbox si las conversaciones sin responsable se asignan al agente cuando envia un mensaje
- **Protección de conversaciones resueltas** - Cuando un inbox no permite mensajes después de resolver, el widget rechaza reintentos y nuevos envíos de texto o adjuntos para esa conversación; el visitante puede iniciar una conversación nueva
- **Capas y fondos corregidos** - Mejor renderizado visual entre launcher y portal, incluyendo modo oscuro

**Beneficios para tu negocio:**

- Convierte visitantes en clientes mientras navegan
- Reduce el abandono del carrito de compras
- Ofrece soporte inmediato sin que el cliente salga de tu web

### SMS

Llega a tus clientes incluso cuando no tienen internet o apps de mensajería, con mensajes de texto tradicionales.

**¿Por qué SMS?**

El SMS tiene una tasa de apertura del 98%, mucho mayor que cualquier otro canal. Es ideal para notificaciones urgentes, confirmaciones y comunicación con clientes que no usan apps.

**Funcionalidades principales:**

- **Envío y recepción** - Comunícate bidireccionalmente con tus clientes
- **Números virtuales** - Configura múltiples líneas telefónicas
- **Integración con Twilio** - Proveedor líder mundial de SMS
- **Webhooks de Twilio verificados** - Los mensajes y estados que Twilio envía para SMS y WhatsApp se comprueban con la firma de Twilio. Cada bandeja empieza solo registrando y, desde el primer aviso con firma válida, rechaza los que no la traen; así una configuración que todavía no firma sigue funcionando. Las bandejas conectadas con API Key sin el auth token de la cuenta no se verifican.
- **Salud de bandejas Twilio WhatsApp** - Salud de la cuenta también cubre las bandejas Twilio WhatsApp: verifica los webhooks de mensajería y voz y muestra el estado del remitente de WhatsApp, su nombre visible, la calificación de calidad y el límite de mensajes; registrar el webhook también funciona para ellas
- **Bandwidth con OAuth** - Las bandejas SMS de Bandwidth se conectan con el Client ID y el Client Secret de Bandwidth, que se verifican antes de guardar. Bandwidth deja de aceptar las credenciales de usuario de API el 2 de diciembre de 2026: en las bandejas existentes, un administrador debe guardar el Client ID y el Client Secret en la configuración de la bandeja antes de esa fecha.
- **Webhooks de Bandwidth protegidos** - La URL de callback de cada bandeja de Bandwidth lleva un token secreto. Un administrador la copia desde la pestaña Configuración de la bandeja y la pega en la aplicación de Bandwidth. Hasta que Bandwidth llama por primera vez a la URL con token, los avisos sin token se siguen aceptando y quedan registrados; desde entonces se rechazan.
- **Campañas masivas** - Envía mensajes a toda tu base de contactos

**Beneficios para tu negocio:**

- Alcanza a clientes sin smartphones o sin datos
- Notificaciones que realmente se leen
- Ideal para recordatorios y confirmaciones

### Telegram

Conecta con los millones de usuarios que prefieren Telegram por su velocidad, seguridad y funcionalidades avanzadas.

**¿Por qué Telegram?**

Telegram es especialmente popular entre usuarios tech-savvy y en regiones como Europa del Este, Medio Oriente y partes de Latinoamérica. Es conocido por su velocidad y privacidad.

**Funcionalidades principales:**

- **Configuración en minutos** - Conecta tu bot de Telegram fácilmente
- **Mensajes con formato** - Envía texto con negritas, cursivas y más
- **Multimedia completa** - Imágenes, videos, documentos y más
- **Botones interactivos** - Ofrece opciones de respuesta rápida a tus clientes
- **Respuestas contextuales** - Responde a mensajes específicos para mayor claridad
- **Telegram Business** - Soporte para cuentas empresariales de Telegram

**Beneficios para tu negocio:**

- Fotos de perfil automáticas de los contactos
- Sin límites de tamaño para archivos
- Mensajes que llegan instantáneamente

### API Channel

Para empresas con necesidades únicas: integra cualquier sistema de mensajería propio o de terceros.

> **Disponibilidad:** El acceso mediante tokens de API y la entrega saliente de Webhooks requieren acceso a API y Webhooks para la cuenta en planes alojados. Siguen disponibles en instalaciones autogestionadas.

**¿Cuándo usar API Channel?**

Si tienes un sistema propio de mensajería, una app móvil con chat, o necesitas conectar una plataforma que no está integrada nativamente, API Channel te da la flexibilidad total.

**Funcionalidades principales:**

- **Integración personalizada** - Conecta cualquier fuente de mensajes
- **Webhooks entrantes** - Recibe mensajes de sistemas externos
- **API de respuesta** - Envía respuestas de vuelta a tu sistema
- **Validación de identidad (HMAC)** - En las bandejas con validación de identidad obligatoria, cada llamada de la API pública sobre un contacto (el contacto, sus conversaciones y sus mensajes) debe incluir el `identifier_hash` que firma el identificador de ese contacto; si falta o no coincide, se rechaza. En la API de la cuenta, la verificación HMAC se calcula en el servidor a partir de `identifier` e `identifier_hash`, y se ignora un `hmac_verified` enviado por el cliente.
- **Envío universal para integraciones** *(Mega)* - Con una sola petición autenticada identifica al destinatario por teléfono, email, contacto o ID del proveedor, prepara automáticamente contacto y conversación, y envía texto, multimedia o plantillas de WhatsApp por cualquier bandeja compatible. Las plantillas multimedia de WhatsApp Cloud pueden cargar su archivo en la misma petición y su contenido renderizado queda visible en la conversación. Las claves de idempotencia hacen seguros los reintentos.
- **Sin límites** - Adapta la plataforma a cualquier canal imaginable

**Casos de uso:**

- Apps móviles con chat propio
- Portales de clientes
- Sistemas legacy de mensajería
- Integraciones con proveedores no soportados nativamente

### LINE

Conecta con usuarios de LINE, la app de mensajería líder en Japón, Taiwán, Tailandia e Indonesia con más de 200 millones de usuarios activos.

**¿Por qué LINE?**

Si tu negocio atiende clientes en Asia, LINE es imprescindible. En Japón, el 90% de los usuarios de smartphones usan LINE diariamente.

**Funcionalidades principales:**

- **Configuración sencilla** - Conecta tu cuenta LINE Official en minutos
- **Mensajes de texto** - Comunicación fluida con tus clientes
- **Stickers y multimedia** - Envía contenido visual atractivo
- **Seguridad** - Credenciales protegidas con cifrado avanzado

**Beneficios para tu negocio:**

- Acceso al mercado asiático
- Usuarios altamente comprometidos
- Ideal para comercio electrónico internacional

### Twitter / X

Atiende consultas y gestiona la reputación de tu marca en la red social donde ocurren las conversaciones públicas más importantes.

**¿Por qué Twitter/X?**

Twitter es donde los clientes expresan quejas, hacen preguntas y buscan soporte público. Una respuesta rápida y profesional puede convertir una queja en una reseña positiva.

**Funcionalidades principales:**

- **Mensajes directos (DMs)** - Gestiona conversaciones privadas con tus clientes
- **Menciones públicas** - Opción de monitorear cuando te mencionan
- **Creación automática de contactos** - Los perfiles de Twitter se guardan automáticamente
- **Conexión segura** - Autenticación oficial con la API de X
- **Eventos firmados** - Solo se aceptan los eventos de X que llegan con una firma válida de la app (`TWITTER_CONSUMER_SECRET`); el resto se rechaza.

**Beneficios para tu negocio:**

- Responde rápidamente a quejas públicas
- Convierte interacciones en oportunidades
- Mejora la percepción de tu marca
- Identifica tendencias y feedback de clientes

### Canal de Voz - Twilio *(Enterprise)*

Transforma tu equipo en un centro de llamadas profesional con telefonía VoIP integrada directamente en la plataforma usando Twilio Voice SDK.

**¿Por qué agregar llamadas a tu operación?**

Algunos clientes prefieren hablar por teléfono, especialmente para asuntos urgentes o complejos. Con el Canal de Voz, tus agentes pueden recibir y hacer llamadas sin salir de MEGA.

**Stack Tecnológico:**

- **Twilio Voice SDK** - Proveedor VoIP líder en la industria
- **WebRTC** - Llamadas desde el navegador, sin software
- **TwiML Apps** - Manejo personalizado de llamadas y enrutamiento
- **Provisión de números** - Obtén números en 100+ países

**Llamadas Entrantes:**

- **Recepción inteligente** - Las llamadas crean conversaciones automáticamente
- **Identificación de llamante** - Reconoce contactos existentes por su número
- **Nuevos contactos automáticos** - Si el número es nuevo, se crea el contacto
- **Números ocultos** - También se atienden las llamadas con identificador de llamada oculto: cada una crea un contacto "Llamante desconocido" con su propia conversación, donde los botones de llamada se ocultan y solo se pueden escribir notas privadas
- **Historial unificado** - Llamadas y mensajes en el mismo timeline
- **Gestión de colas** - Maneja alto volumen de llamadas

**Experiencia de quien llama y enrutamiento** *(Mega, pestaña Voz de la bandeja)*:

> **Opcional:** el saludo, el horario de atención, el límite de timbre y el enrutamiento de un agente a la vez vienen apagados en bandejas existentes y nuevas; mientras no se activen, las llamadas suenan para todos los agentes que pueden verlas, sin límite de tiempo, como hasta ahora.

- **Saludo** - Quien llama escucha un mensaje de bienvenida, dicho en el idioma de la cuenta, mientras suena para los agentes, y después música de espera
- **Llamadas solo en horario de atención** - Con el horario de atención de la bandeja activado, una llamada que llega con la bandeja cerrada escucha un mensaje de fuera de horario y termina sin sonar para nadie; queda registrada como perdida con la marca "Fuera del horario de atención". Las excepciones del horario de atención no se aplican a las llamadas
- **Límite de tiempo de timbre** - Una llamada sin atender termina después de los segundos que elijas (de 10 a 600), quien llama escucha un mensaje opcional y la llamada queda registrada como perdida
- **Un agente a la vez** - Las llamadas suenan para un agente libre a la vez con la misma política que las llamadas de WhatsApp Cloud: primero el asignado de la conversación, después los agentes en línea de la bandeja por turnos y por último los administradores que activaron las notificaciones de llamadas. El tiempo de escalamiento, los intentos, qué hacer cuando el asignado está en otra llamada y el tiempo de timbre del último agente usan la configuración de llamadas de WhatsApp. Si nadie puede atender, la llamada termina con el mensaje de llamada no atendida y la marca "Sin agentes disponibles". La conversación conserva su asignado: no hay devolución al terminar la llamada
- **Ocupado en cualquier llamada** - Un agente en una llamada de Twilio cuenta como ocupado para las llamadas de WhatsApp, y un agente en una llamada de WhatsApp cuenta como ocupado para el enrutamiento de Twilio
- **Rechazos que se mantienen** - Cada llamada registra para quién suena. Un agente que la rechaza deja de escucharla en todas sus pestañas abiertas y la llamada no vuelve al recargar; una llamada que todavía suena para el agente vuelve a mostrarse al recargar la página (hasta una hora)

**Llamadas Salientes:**

- **Click-to-call** - Llama a cualquier contacto con un solo clic
- **Desde el perfil del contacto** - Sin marcar números manualmente
- **Errores de llamada claros** - Cuando una llamada no puede iniciarse, el agente ve el motivo, por ejemplo un contacto sin número de teléfono
- **Llamadas en conferencia** - Conecta agente y cliente fácilmente
- **Personalización de Caller ID** - Muestra tu número de empresa

**Seguimiento completo:**

- Registro de todas las llamadas (contestadas, perdidas, ocupadas)
- Duración y timestamps de cada llamada
- Identificación de llamadas entrantes vs salientes
- Todo el historial visible en la conversación del cliente
- Grabación nativa opcional de Twilio con aceptación explícita del costo de storage
- Grabaciones descargables en la conversación y en reportes de llamadas

**Funciones del Agente:**

- **Webphone en navegador** - Contesta llamadas directamente en MEGA
- **Mute/Unmute** - Controla el micrófono durante llamadas
- **Espera y retomar** - El agente en la llamada pone a quien llama en espera (escucha música de espera) y retoma la llamada; mientras tanto la llamada muestra "En espera"
- **Teclado en llamada** - Envía tonos del teclado durante una llamada conectada, para menús telefónicos y extensiones; también en llamadas de WhatsApp Cloud
- **Conversaciones de llamada abren en nota privada** - Una conversación cuyo último mensaje es una llamada abre la caja de respuesta en Nota privada, para anotar sobre la llamada; si se cambia a Responder, se mantiene durante esa visita
- **Transferir llamadas** - Enruta a otro agente o departamento
- **Solo quien atiende cuelga** - Solo el agente que aceptó la llamada puede cortarla; una llamada entrante que todavía suena y nadie aceptó puede rechazarla cualquier agente de la bandeja.

**Beneficios para tu negocio:**

- Canal adicional sin cambiar de herramienta
- Contexto completo del cliente al contestar
- Métricas de llamadas junto con otros canales
- Escalable de 1 a 1000+ agentes
- Precios pago-por-uso con Twilio

### Llamadas WhatsApp Cloud *(Enterprise/Mega)*

Realiza y recibe llamadas de voz a través de WhatsApp usando la Cloud API de Meta con tecnología WebRTC.

> **Disponibilidad:** Las llamadas no están disponibles para números de WhatsApp Cloud conectados mediante coexistencia con WhatsApp Business App. Continúan en la aplicación WhatsApp Business y no se muestran en MEGA.

**¿Por qué Llamadas WhatsApp?**

Muchos clientes prefieren la comunicación por voz para temas complejos. Las Llamadas WhatsApp permiten a tus agentes manejar llamadas de voz directamente en la plataforma, usando el mismo número de WhatsApp que para mensajes.

**Llamadas Entrantes:**

- **Notificaciones en tiempo real** - Los agentes reciben alertas de llamada instantáneas
- **Aceptar/Rechazar desde el navegador** - Maneja llamadas sin ninguna app externa
- **Asignación inteligente de agentes** - Llamadas enrutadas, una por vez, a los miembros del inbox que están online, aunque la auto-asignación esté desactivada; los administradores que activaron las notificaciones de llamadas se usan solo como respaldo
- **Auto-rechazo cuando no hay disponibles** - Comportamiento configurable
- **Agente asignado en otra llamada** - Configurable por inbox: la llamada suena a otro agente disponible (predeterminado) o solo al agente asignado. Si el mismo contacto vuelve a llamar durante una llamada en curso, esa llamada no se interrumpe
- **Llamadas solo en horario de atención** - Opcional por inbox en la configuración de llamadas: con el horario de atención de la bandeja activo, WhatsApp solo permite que los clientes llamen dentro de ese horario, en la zona horaria de la bandeja, y la pausa del almuerzo queda cerrada. Si Meta rechaza el horario, la configuración de llamadas se guarda igual y el motivo se muestra debajo del interruptor
- **Identificación del llamante** - Ve información del contacto antes de contestar

**Llamadas Salientes (Business-Initiated):**

- **Click-to-call** - Inicia llamadas desde la conversación o el perfil de un contacto, incluso si aún no tiene una conversación
- **Sistema de permisos** - Solicita y rastrea permisos de llamada dentro de la ventana de atención de 24 horas
- **Una llamada por agente** - Evita iniciar una segunda llamada mientras el agente ya tiene una activa, incluso desde otra pestaña
- **Plantillas de permiso de llamada** - Usa templates aprobados con solicitud de permiso desde el ReplyBox, permite definir uno predeterminado por inbox y muestra el envío en el historial de la conversación
- **Estado de permisos** - Distingue visualmente entre sin permiso, permiso temporal de 7 días y permiso permanente; confirma el estado y la disponibilidad de inicio de llamada con WhatsApp y registra cada cambio, incluida la fecha de vencimiento temporal, en la actividad de la conversación
- **Tono de ringback** - Audio de feedback mientras se conecta

**Funciones durante la llamada:**

- **WebRTC nativo** - Audio de alta calidad sin SDKs externos
- **Conectividad adaptativa** - Usa servidores STUN/TURN configurados para llamadas premium cuando una red restringida impide la conexión directa
- **Asignación protegida** - Desde que se acepta la llamada hasta que termina, no se puede cambiar el agente ni el equipo de la conversación; mientras solo timbra, la reasignación sigue disponible
- **Mute/Unmute** - Alterna el micrófono durante llamadas
- **Teclado en llamada** - Envía tonos del teclado durante la llamada, para menús telefónicos y extensiones (WhatsApp Cloud y Twilio; no WAHA)
- **Duración de llamada** - Temporizador en tiempo real visible
- **Solo quien atiende cuelga** - Solo el agente que hizo o atendió la llamada puede cortarla; una llamada entrante que nadie atendió puede cortarla cualquiera que vea la conversación.
- **Audio en el servidor (beta)** - Se activa por cuenta desde Super Admin (feature "Voice Engine") cuando la instalación tiene el motor desplegado; la cuenta no puede activarlo por su cuenta y, una vez activo, vale para sus bandejas de WhatsApp Cloud y WAHA: el motor de voz de Mega atiende la llamada, así recargar la página del agente ya no corta al cliente y el agente vuelve a entrar a la llamada
- **Música de espera** - Con el audio en el servidor, cada bandeja de WhatsApp Cloud elige lo que escucha el cliente en espera: una de cinco melodías incluidas o un archivo de audio propio (MP3, WAV, OGG o M4A, hasta 10 MB y 10 minutos), con reproductor de prueba en la configuración
- **Transferencia de llamadas** - Con el audio en el servidor, el agente en la llamada se la pasa a otro agente disponible de la bandeja (con buscador por nombre) sin cortar al cliente: el cliente escucha la música de espera mientras la llamada le suena al otro agente (en todas sus pestañas y dispositivos, con quién se la transfiere). Si la toma, la llamada y la conversación pasan a ese agente; si la rechaza, no contesta en 30 segundos o el primer agente cancela, el cliente vuelve con el primer agente
- **Transferencia consultiva** - Antes de pasar la llamada, el agente puede consultar a otro agente: el cliente escucha la música de espera mientras los dos agentes hablan, y después el primer agente le transfiere la llamada o vuelve con el cliente. Si el otro agente rechaza, no contesta en 30 segundos o corta la consulta, el cliente vuelve con el primer agente
- **Grabación de llamadas en el servidor** - Con el audio en el servidor cada llamada atendida se graba en el servidor, con los dos lados (incluida la música de espera y el agente al que se transfirió la llamada), y queda en la conversación como nota privada con el audio, igual que las demás grabaciones de llamadas. Recargar la página o transferir no la corta
- **Audio en el servidor en WAHA** - Con la feature activa, las bandejas WAHA también usan el audio en el servidor: las llamadas entrantes y salientes pasan por el motor de voz de Mega, así el agente vuelve a entrar tras recargar y puede poner al cliente en espera con la música de la bandeja y transferir la llamada (directa o después de consultar a otro agente). Puede haber varias llamadas WAHA en curso al mismo tiempo. La grabación la sigue haciendo WAHA
- **Menú de llamadas (IVR)** - Un flujo del Flow Builder que arranca con "Llamada recibida" atiende las llamadas de WhatsApp (Cloud o WAHA) de una bandeja con audio en el servidor como un menú telefónico: el cliente escucha audios que subió la cuenta (MP3, WAV, OGG o M4A) o que generó con IA a partir de un texto, eligiendo el modelo de voz y la voz entre los proveedores de IA de la cuenta (reutilizables entre flujos; se generan una vez al guardar, y de nuevo si cambia el texto, el modelo o la voz), marca una tecla ("marcá 1 para ventas, 2 para soporte") y el flujo transfiere la llamada a toda la bandeja o a un equipo, reproduce otro audio o cuelga. Vuelve a preguntar tras una tecla equivocada o el silencio, y los chequeos de horario de atención y agentes disponibles funcionan en estos flujos. Si no hay agentes libres, la llamada puede esperar en una cola con la música de espera y sonar al primer agente que se libere, en el orden en que llegaron las llamadas, hasta una espera máxima que se configura en el bloque. Cada paso queda en las ejecuciones del flujo Las bandejas de voz de Twilio también pueden usar el menú: reproducir audios, pedir una tecla, transferir a toda la bandeja o a un equipo, y colgar (sin cola de espera ni IA por ahora).
- **IA en llamadas** - En un flujo de llamadas, "Atender con IA" pone a un agente de IA a conversar con el cliente en tiempo real y resolver la llamada por sí mismo: mantiene una conversación natural, responde con el asistente de Captain de la bandeja (su conocimiento y herramientas) o con instrucciones escritas en el bloque, y pasa a una persona solo cuando el cliente lo pide o no puede ayudar. En el saludo avisa que es un asistente virtual (activado por defecto). Lo que se habló queda en la conversación como nota privada. "Preguntar por voz" permite contestar un menú hablando ("¿ventas o soporte?") en lugar de marcar teclas, que es como funcionan los menús en WAHA; devuelve el saludo y confirma la opción con una frase amable ("Claro, con gusto, un momento") antes de pasar la llamada, y el agente de IA que sigue ya atiende en el idioma en que habló el cliente. Se cobra en AI Actions cada 5 minutos de conversación
- **Optimización VoIP** - Audio optimizado para llamadas de voz

**Historial de Llamadas:**

- **Llamadas contestadas** - Con duración y timestamp
- **Llamadas perdidas** - Detección automática
- **Devolver llamada** - La última llamada perdida o fallida muestra la línea por la que entró y un botón para devolverla desde el chat
- **Llamadas rechazadas** - Rastrea llamadas declinadas
- **Integración en timeline** - Todas las llamadas aparecen en el historial

**Requisitos Técnicos:**

- Inbox de WhatsApp Cloud API
- Número de teléfono empresarial configurado con Meta
- Ventana de atención abierta o plantilla aprobada para reabrir la conversación antes de solicitar permiso
- Navegador moderno con soporte WebRTC

---

### Llamadas WhatsApp WAHA *(Mega)*

Recibe y realiza llamadas de voz de WhatsApp desde MEGA con números conectados por WAHA, usando el mismo widget de llamadas que WhatsApp Cloud.

**Disponibilidad:**

- Se habilita por instalación con `WAHA_VOICE_CALL=true` o por servidor WAHA en Super Admin → Proveedores WA (interruptor *Llamadas de voz*); los servidores no compatibles no muestran nada
- Luego se activa por cuenta (feature *WAHA Voice Calls*) y por bandeja en la configuración de sesión → Apps → *Llamadas de voz*

**Llamadas Entrantes:**

- **Mismo widget que Cloud** - Aviso en tiempo real, aceptar o rechazar desde el navegador y asignación al agente de la conversación o por round-robin
- **Ajustes de llamadas como en Cloud** - En Apps → *Llamadas de voz* → *Ajustes de llamadas*: escalar al siguiente agente, qué hacer si el agente asignado está en otra llamada (sonar a otro agente disponible o solo al asignado), auto-rechazo y mensajes de no disponible
- **La conversación vuelve a su dueño** - Cuando una llamada suena para otro agente porque el asignado está en otra llamada o no atendió, la conversación muestra a quién pasó y por qué, y vuelve a su agente asignado al terminar la llamada
- **Llamadas de grupo rechazadas** - Solo las llamadas directas llegan a los agentes
- **Historial en la conversación** - Cada llamada queda como mensaje: completada con su duración, no atendida o rechazada
- **Grabación automática** - WAHA graba las llamadas atendidas (entrantes y salientes) y la grabación se adjunta a la conversación como nota privada

**Llamadas Salientes:**

- **Click-to-call** - Botón de llamada en el panel del contacto (o en el selector de métodos si la bandeja tiene varios)
- **Una llamada por agente** - No permite iniciar una segunda llamada mientras hay una activa
- **Las llamadas no atendidas terminan solas** - Si WAHA nunca avisa el fin de una llamada no atendida, Mega la termina a los 2 minutos y el agente puede hacer la siguiente

**Seguridad:**

- El navegador no recibe ninguna credencial de WAHA: Mega negocia el audio con WAHA y el agente solo puede abrir el audio de la llamada que atendió o inició
- Solo el agente que hizo o atendió la llamada puede cortarla; una llamada entrante que nadie atendió puede cortarla cualquiera que vea la conversación

**Requisitos:**

- Servidor WAHA con motor GOWS, app `voice-calls` y WebRTC habilitado (`WAHA_CALLS_WEBRTC_PUBLIC_IP` y el puerto UDP abierto; en Docker Swarm, publicado con `mode: host`)
- Navegador moderno con soporte WebRTC, en HTTPS

---

## 💬 Gestión de Conversaciones

### Bandeja de Entrada Inteligente

- **Vista unificada** - Todas las conversaciones en un solo lugar
- **Filtros avanzados** - Por estado, inbox, agente, equipo, etiquetas
- **Atributos numéricos** - Los atributos personalizados numéricos se filtran por igual, distinto, presente, mayor o menor; si eliges *Contiene*, el filtro te avisa en lugar de fallar
- **Ordenar resultados filtrados** - Las búsquedas con filtros avanzados y las carpetas se pueden ordenar igual que la lista normal (más recientes, más antiguas, prioridad, tiempo de espera)
- **Filtros de fecha en tu hora local** - Los filtros por fecha de creación o de última actividad usan el día de tu zona horaria, igual que los reportes, y los contadores de un filtro ya no vuelven a mostrar los totales generales
- **Indicador de adjuntos en e-mails** - Las conversaciones de correo muestran un 📎 en la lista cuando el cliente envió archivos, con tooltip de cantidad y tipos (ej. "2 adjuntos: CDR, PDF"); las imágenes inline de firma no cuentan y el filtro **Adjuntos de correo** las segmenta
- **Filtros multi-selección** - Selecciona múltiples bandejas o equipos simultáneamente
- **Filtros de etiquetas con lógica AND** - Filtra por múltiples etiquetas que deben cumplirse todas
- **Vistas personalizadas** - Guarda filtros frecuentes como vistas rápidas
- **Búsqueda potente** - Encuentra conversaciones por contenido, contacto o metadatos
- **Filtros rápidos en sidebar** - Navega directo a No Leídas, Menciones, Participando, Grupos y No atendidas desde la barra lateral
- **Contadores reactivos de no leídos** - Menciones, Participando, Grupos y No Leídas muestran badges actualizados en tiempo real sin recargar
- **Fecha y hora exactas al pasar el cursor** - Las fechas relativas muestran la fecha y hora completas en la lista de conversaciones, mensajes, contactos, búsqueda, reportes y tarjetas relacionadas del dashboard

### Integraciones con atributos personalizados

Las integraciones pueden actualizar solo las claves enviadas de los atributos personalizados de una conversación o reemplazarlos por completo. También pueden eliminar claves específicas sin alterar el resto de la información.

### Búsqueda de Mensajes en Conversación

Encuentra mensajes específicos dentro de una conversación:

- **Búsqueda de texto** - Busca palabras o frases dentro de todos los mensajes
- **Búsqueda en transcripciones de audio** - Encuentra notas de voz por palabras o frases contenidas en su transcripción
- **Filtro por fechas** - Acota la búsqueda a un rango de fechas específico
- **Resaltado de resultados** - Los mensajes encontrados se destacan visualmente
- **Scroll automático** - Navega instantáneamente al mensaje encontrado
- **Paginación de resultados** - Navega entre múltiples coincidencias fácilmente
- **Contexto preservado** - Ve el mensaje en su contexto original de conversación

### Estados de Conversación

- **Abierta** - Conversaciones que requieren atención
- **Pendiente** - En espera de respuesta del cliente
- **Resuelta** - Conversaciones finalizadas
- **Pospuesta (Snooze)** - Programa reactivación automática con lenguaje natural: escribe "mañana a las 3pm", "en 2 horas", "próximo lunes" o cualquier expresión de tiempo y el sistema interpreta la fecha automáticamente; también disponible con selector de fecha clásico
- **Una conversación activa por contacto** - Si el contacto ya tiene una conversación abierta o pendiente en el mismo inbox, no se puede reabrir ni responder una resuelta: el sistema indica cuál es la conversación activa para continuar ahí. La búsqueda muestra el estado de cada conversación con su color

### Priorización

- **Niveles de prioridad** - Urgente, Alta, Media, Baja
- **Ordenamiento inteligente** - Por actividad reciente, tiempo de espera, prioridad
- **Orden por no leídas** - Prioriza conversaciones con mensajes sin leer desde el selector de orden
- **Indicadores visuales** - Identifica rápidamente conversaciones críticas
- **Cuenta regresiva de la ventana de respuesta** - En WhatsApp Cloud, 360dialog, NotificaMe y los demás canales con ventana de respuesta (Messenger, Instagram, TikTok, WhatsApp por Twilio, API con tiempo de respuesta), la cabecera de la conversación muestra "Ventana abierta · cierra en 3 h 12 min" con la hora exacta al pasar el cursor, y cada tarjeta de la lista muestra el tiempo restante: ámbar con menos de 2 horas, rojo al cerrar. Si cierra con la conversación abierta, el editor pasa solo a plantillas de mensaje

### Colaboración en Equipo

- **Asignación de agentes** - Manual o automática
- **Asignación de equipos** - Deriva a departamentos específicos
- **Menciones (@)** - Notifica a compañeros en conversaciones
- **Notas privadas** - Comunícate internamente sin que el cliente vea
- **Menciones en nota privada con contador** - Las menciones internas elevan el contador del filtro Menciones en el sidebar

### Participantes de Conversación

Múltiples agentes pueden colaborar en una sola conversación:

- **Añadir participantes** - Incluye agentes adicionales en conversaciones
- **Notificaciones de participantes** - Todos los participantes reciben alertas de mensajes
- **Fijar conversaciones** - Los participantes pueden fijar conversaciones importantes
- **Lista de participantes** - Ve todos los agentes involucrados en una conversación
- **Remover participantes** - Quita agentes cuando ya no sean necesarios
- **Auto-participantes** - Los agentes que interactúan se añaden automáticamente

### Atajos del editor de respuesta

- Los atajos de envío no acumulan acciones duplicadas al cambiar de conversación. Se mantienen las preferencias de Enter/Ctrl/Cmd+Enter y el cierre de menciones con Escape.
- Escribir "/" en la caja de respuesta o en cualquier otro campo de texto de la página de búsqueda se queda en ese campo; "/" solo salta a la caja de búsqueda cuando ningún campo de texto tiene el foco.
- Los selectores de respuestas predefinidas y macros mantienen la opción resaltada cuando su lista se actualiza en segundo plano.

### Cuadro de respuesta contraíble

- En escritorio y tablet, el cuadro de respuesta se contrae para dejar más espacio a la lectura de la conversación: con el botón de contraer junto al de ampliar, o arrastrando el tirador de tamaño por debajo de su altura mínima.
- Abajo queda una barra fina con **Responder** y **Nota privada** (Alt+L / Alt+P, ⌥ en Mac); muestra "Borrador sin enviar" cuando hay texto o adjuntos pendientes. Responder a un mensaje, insertar contenido, una acción de Captain o pegar un archivo también vuelven a abrir el cuadro.
- El borrador, los adjuntos y el modo elegido se conservan mientras está contraído. La preferencia se recuerda para el agente en todas las conversaciones y dispositivos.
- En el teléfono se mantiene el compositor flotante de una fila y nunca se contrae.

### Respuestas Predefinidas (Canned Responses)

Plantillas rápidas con atajos para respuestas más ágiles:

- **Respuestas personales** - Visibles solo para ti
- **Respuestas compartidas** - Disponibles para todo el equipo
- **Activación por atajo** - Escribe / para acceder a respuestas
- **Sustitución de variables** - Placeholders dinámicos para info del contacto
- **Soporte de adjuntos** - Incluye imágenes, documentos y archivos con respuestas
- **Múltiples adjuntos** - Adjunta múltiples archivos a una sola respuesta predefinida
- **Adjuntos también en nueva conversación** - Reutiliza archivos de respuestas predefinidas incluso al iniciar conversaciones nuevas
- **Buscador con vista previa** - Busca por atajo y contenido, previsualiza la respuesta renderizada y conserva variables sin resolver para el backend
- **Búsqueda instantánea en caché** - Carga las respuestas una vez por cuenta y filtra localmente mientras la invalidación en tiempo real mantiene los datos actualizados
- **Contenido enriquecido** - Formatea texto con soporte markdown

### Grabador de Voz

- **Notas de audio** - Graba y envía mensajes de voz
- **Grabación fácil** - Un clic para iniciar/detener
- **Vista previa** - Escucha antes de enviar

### Otras Herramientas de Productividad

- **Adjuntos multimedia** - Imágenes, videos, documentos
- **Soporte para archivos PFX** - Adjunta certificados `.pfx` con reconocimiento visual y de tipo adecuado
- **Emojis y GIFs** - Comunicación más cercana
- **Respuesta citada (Reply-to)** - Responde a mensajes específicos
- **Borradores de mensajes** - Guarda automáticamente borradores mientras escribes, se restauran al volver a la conversación
- **Editor de respuesta redimensionable** - Ajusta manualmente la altura del cuadro de respuesta para trabajar mejor en conversaciones largas
- **Editar mensajes enviados** - Corrige mensajes después de enviarlos (según proveedor)
- **Eliminar mensajes enviados** - Elimina mensajes para todos (según proveedor)

### Conversaciones Fijadas

Mantén las conversaciones importantes en la parte superior de tu lista:

- **Fijar conversaciones** - Fija cualquier conversación arriba
- **Desfijar cuando quieras** - Quita el fijado cuando ya no sea necesario
- **Fijados por agente** - Cada agente tiene su propia lista de fijados
- **Indicador visual** - Las conversaciones fijadas están claramente marcadas

### Filtros Personalizados (Carpetas)

Guarda tus filtros de uso frecuente para acceso rápido:

- **Crear carpetas** - Guarda combinaciones de filtros como carpetas personalizadas
- **Filtros de conversación** - Filtra conversaciones por cualquier criterio
- **Filtros de contacto** - Filtra contactos por atributos
- **Acceso rápido** - Un clic para aplicar filtros guardados
- **Editar y eliminar** - Gestiona tus carpetas fácilmente
- **Límites por usuario** - Cada usuario puede crear múltiples carpetas
- **Multi-etiqueta consistente** - Normalización de valores para filtros con múltiples etiquetas

### Resolución Automática

- **Auto-resolve** - Cierra conversaciones inactivas automáticamente
- **Temporizadores configurables** - Define tiempos por inbox
- **Limpieza de conversaciones huérfanas** - Elimina automáticamente conversaciones sin contacto asociado

### Acciones en Lote (Bulk Actions)

Realiza operaciones masivas sobre múltiples conversaciones simultáneamente:

- **Resolver en lote** - Cierra múltiples conversaciones de una vez
- **Reabrir en lote** - Reabre conversaciones resueltas
- **Posponer en lote** - Aplica snooze a varias conversaciones
- **Estado de lectura en lote** - Marca las conversaciones seleccionadas como leídas o no leídas, incluso en selecciones grandes
- **Asignar en lote** - Asigna agente o equipo a múltiples chats
- **Etiquetar en lote** - Aplica etiquetas masivamente
- **Atajos de teclado** - Ejecuta acciones bulk con hotkeys

### Acciones sobre Contactos (Bulk)

- **Fusionar contactos** - Combina contactos duplicados
- **Etiquetar contactos** - Aplica etiquetas a múltiples contactos
- **Eliminar contactos** - Borrado masivo con confirmación

### Command Bar (Barra de Comandos)

Acceso rápido a cualquier acción mediante teclado:

- **Activación rápida** - Abre con `Cmd/Ctrl + K`
- **Búsqueda de acciones** - Encuentra comandos escribiendo
- **Navegación** - Ir a conversaciones, contactos, configuración
- **Cambio de apariencia** - Modo claro, oscuro o sistema
- **Asignación rápida** - Asigna agentes o equipos
- **Cambio de estado** - Resuelve, reabre, pospone
- **Acciones AI** - Accede a funciones de Captain
- **Ejecución de macros** - En una conversación abierta, elige **Ejecutar una macro** para usar las mismas macros ordenadas de la barra lateral

### Modo Oscuro (Dark Mode)

- **Tema oscuro** - Interfaz optimizada para ambientes con poca luz
- **Tema claro** - Interfaz tradicional clara
- **Modo sistema** - Sigue la preferencia del sistema operativo
- **Widget adaptable** - El widget también soporta dark mode

---

## 💬 Comunicación Interna del Equipo

### Salas de Chat (Chat Rooms) *(Mega)*

Sistema de salas de chat internas para comunicación fluida del equipo sin salir de la plataforma. Perfecto para coordinación, preguntas rápidas y discusiones internas.

**¿Por qué Salas de Chat Internas?**

Mantén a tu equipo conectado y productivo. En lugar de usar herramientas externas como Slack o Teams para comunicación interna, gestiona todo en un solo lugar junto a las conversaciones con clientes.

**Funcionalidades Principales:**

**Gestión de Salas (Settings):**

- **Crear salas** - Los administradores pueden crear salas con nombre y descripción; el nombre conserva las mayúsculas ingresadas y sigue siendo único en la cuenta sin distinguir mayúsculas de minúsculas
- **Canales públicos y privados** - Define visibilidad y audiencia según el flujo del equipo
- **Categorías** - Agrupa canales por tema, equipo o departamento
- **Agregar usuarios** - Selección múltiple de miembros del equipo de tu cuenta
- **Editar salas** - Actualizar nombre, descripción y miembros desde el menú de tres puntos del encabezado
- **Eliminar salas** - Borrar salas con confirmación de seguridad
- **Avatares de sala** - Imágenes personalizadas opcionales para cada sala
- **Llamadas de audio y video** - Comunicación WebRTC entre miembros en DMs, grupos y canales, con tonos e historial de llamadas en curso, perdidas y completadas
- **Disponibilidad selectiva de llamadas** - Las llamadas requieren la feature de cuenta independiente `chat_room_calls`, deshabilitada por defecto y habilitable solo para cuentas seleccionadas; la mensajería de Chat Rooms continúa disponible sin ella
- **Conectividad ICE administrable** - Super Admin > Call ICE permite configurar STUN/TURN y sus credenciales sin reiniciar; las variables de entorno `MEGA_CALL_*` siguen siendo compatibles cuando no hay valores guardados
- **Conectividad premium por cuenta** - `chat_room_calls` usa Google STUN para llamadas P2P normales; la feature premium `premium_call_connectivity` cambia esa cuenta a Call ICE y habilita TURN como respaldo cuando la configuración global está completa
- **Experiencia nativa de llamadas** - El audio conserva el widget compacto de WhatsApp/Twilio; el video usa un espacio amplio acotado o una ventana flotante dentro de Mega, con cámara y pantalla simultáneas, escenario de presentación, rail de participantes, avatares y mute autorizado por el iniciador para grupos pequeños controlados
- **Ubicación** - Accesible desde Settings > Chat Rooms

> **Nota:** Los ajustes de Salas de chat gestionan únicamente canales (públicos y privados). Los mensajes directos (DM) son conversaciones personales que se gestionan desde la barra lateral de chat y no aparecen ni pueden editarse/eliminarse en Settings.

**Permisos y Visibilidad:**

- **Administradores** - Ven TODAS las salas de la cuenta en el sidebar, pueden crear/editar/eliminar cualquier canal, pueden participar en todas las salas
- **Agentes y Roles Personalizados** - Solo ven las salas donde son miembros en el sidebar, solo pueden participar en sus salas asignadas, no pueden crear/editar/eliminar salas

**Interfaz de Chat:**

- **Ubicación en el sidebar** - Conversations > Rooms
- **Búsqueda integrada** - Encuentra canales, mensajes directos y mensajes dentro de salas
- **Filtros rápidos** - Todo, canales, mensajes directos, borradores y archivadas
- **Secciones visuales** - Borradores, favoritos, mensajes directos, canales y archivadas
- **Creación rápida** - Crear canales, categorías y mensajes directos desde la lista
- **Vista de sala** - Header con nombre de sala + lista de mensajes + input de envío
- **Diseño limpio** - 100% Tailwind CSS, moderno y responsivo

**Tipos de Mensajes:**

- **Mensajes de texto** - Comunicación de texto simple
- **Multimedia** - Imágenes, videos, archivos de audio, documentos
- **Reply** - Responder a mensajes específicos (cita el original)
- **Hilos de respuesta** - Abrir un panel lateral por mensaje, responder dentro del hilo y opcionalmente publicar también en el canal
- **Reacciones** - Responder rápidamente a mensajes con emoji
- **Mensajes fijados** - Mantener información importante visible en la sala
- **Encuestas** - Crear votaciones con múltiples opciones desde el composer
- **Borradores** - Recuperar texto no enviado por usuario y sala
- **Estados de escritura** - Ver cuando otros miembros están escribiendo
- **Grabación de audio** - Grabador de audio integrado para notas de voz

**Diseño Inteligente de Mensajes:**

- **Lado derecho** - Tus propios mensajes (salientes)
  - Color de fondo diferente
  - Tu avatar mostrado
- **Lado izquierdo** - Mensajes de otros usuarios (entrantes)
  - Avatar del remitente mostrado
  - Identificación clara del remitente

**Notificaciones en Tiempo Real:**

- **Integración WebSocket** - Usando Action Cable para entrega instantánea
- **Actualizaciones en vivo** - Los mensajes aparecen inmediatamente sin refrescar
- **Eventos de sala** - Actualización, eliminación, lectura, unread, reacciones, encuestas y escritura
- **Broadcast inteligente** - Los administradores reciben eventos de todas las salas, los usuarios regulares solo de sus salas
- **Seguimiento de eventos** - Eventos de mensaje creado y actualizado

**Seguridad y Validaciones:**

- **Acceso solo para miembros** - Solo los miembros de la sala pueden ver y enviar mensajes
- **Controles de administrador** - Solo los administradores pueden gestionar salas
- **Validación de cuenta** - La membresía de sala se valida contra la cuenta
- **Nombres únicos** - Los nombres de sala deben ser únicos por cuenta

**Beneficios para tu equipo:**

- No necesitas cambiar entre herramientas para comunicación interna
- Discusiones contextuales sin salir de la vista de clientes
- Comunicación organizada por tema o departamento
- Historial completo de mensajes y archivo buscable
- Control de acceso seguro basado en permisos

---

## 🤖 Automatización e IA

### Reglas de Automatización

Configura flujos automáticos basados en eventos y condiciones:

- **Reglas con espera** - Ejecuta acciones entre 10 minutos y 30 días después, mientras la conversación siga en un estado seleccionado, el cliente no responda o no responda un miembro del equipo. Pueden combinar condiciones adicionales con `AND`; una respuesta, cambio de estado o condición incumplida cancela la ejecución pendiente.

**Eventos disponibles:**

- Conversación creada
- Conversación actualizada
- Mensaje recibido
- Mensaje creado

**Condiciones:**

- Estado, inbox, etiquetas, idioma
- País, navegador, email
- Atributos personalizados
- Contenido del mensaje
- Nota privada (mensaje interno)

**Acciones:**

- Enviar mensaje automático
- Asignar agente/equipo
- Asignar al último agente que respondió
- Quitar asignación de agente/equipo
- Añadir/quitar etiquetas
- Cambiar estado o prioridad
- Enviar webhook
- Enviar transcripción por email
- Silenciar conversación
- Redistribuir a agentes en línea

### Flow Builder *(Mega)*

Diseña conversaciones automáticas con bloques que muestran lo que va a recibir el cliente, al estilo ManyChat.

- **Tarjetas con vista previa** - Cada bloque muestra en el lienzo su contenido real: el texto con las variables como etiquetas, adjuntos, plantilla y un botón por fila
- **Edición en panel lateral** - Al tocar un bloque se edita en un panel a la derecha sin tapar el flujo; sin selección, el panel muestra la biblioteca de bloques con búsqueda
- **Opciones con salida propia** - Enviar mensaje admite hasta 10 opciones; cada una abre su propio camino y el cliente puede responder con el número o el texto de la opción. Una respuesta que no coincide sigue por "Otra respuesta"
- **Si la respuesta no es válida** - Un mensaje con opciones puede volver a preguntar cuando el cliente responde algo que no es una opción (texto, imagen, audio o una ubicación que no se pidió): envía un mensaje propio, si se quiere reenvía las opciones y espera de nuevo, de 1 a 5 veces; después sigue por "Otra respuesta". La respuesta inválida no se guarda en el campo del contacto
- **Volver a un bloque** - Un camino puede volver a un bloque anterior (por ejemplo, al menú) con una conexión o con el bloque "Volver a un paso de este flujo", que elige el paso de una lista con búsqueda y lo resalta en el lienzo, siempre que pase por un mensaje que espera la respuesta del cliente; así el flujo nunca se repite solo
- **Tres formas de enviar el mensaje** - Arriba del panel se elige "Texto", "Interactivo" o "Plantilla". "Texto" (por defecto, en cualquier canal) escribe las opciones debajo del mensaje como "🔷 1 - Consultorios Médicos", con viñeta y numeración ("1 -", "1." o "1)") a elección. "Interactivo" usa el mismo formato y los mismos campos que el formulario de interactivos de la conversación, con todos sus tipos: botones de respuesta, lista, enlace, botones de acción, pedido de ubicación, carrusel, encuesta, Pix, pedido, solicitud de pago, evento, ubicación y botón para llamar por WhatsApp (Direct Send), con el encabezado de texto o archivo y el pie que ofrece cada proveedor. Solo aparece, y solo con los tipos de su proveedor, donde alguna bandeja del inicio puede enviar interactivos (WhatsApp Cloud, o WAHA/UazAPI con los mensajes interactivos activos en el servidor, la cuenta y la bandeja); con todas las bandejas, mientras alguna pueda. Botones, filas, respuestas rápidas del carrusel y respuestas de la encuesta abren un camino cada una (la encuesta sigue con el primer voto del cliente), el pedido de ubicación sale por "Ubicación recibida" y los tipos que no esperan respuesta siguen enseguida. Un bloque interactivo en una bandeja sin interactivos se avisa en el panel y en la tarjeta ("Se enviará como texto", con "Pasar a texto") y se envía como texto con el encabezado en negrita, las opciones, el pie y el archivo del encabezado. "Plantilla" aparece donde el Reply Box ofrece plantillas en alguna bandeja del inicio (plantillas de Meta de la bandeja o plantillas de contenido de Twilio); si varias las ofrecen, primero se elige la bandeja. Se elige la plantilla aprobada, el archivo del encabezado, las variables y los parámetros de los botones, y cada respuesta rápida de la plantilla abre su propio camino
- **El bot espera la respuesta** - El flujo se detiene en el mensaje y sigue cuando el cliente contesta; puede guardar la respuesta en un campo personalizado del contacto
- **Sin respuesta** - Si el cliente no contesta en el tiempo elegido, el flujo sigue por la salida "Sin respuesta"
- **Las mismas variables de toda la plataforma** - "+ Variable" ofrece las variables de campañas, respuestas rápidas y Reply Box (`{{contact.first_name}}`, `{{contact.phone}}`, `{{agent.name}}`, `{{inbox.name}}`, atributos personalizados) con los mismos valores, más los datos del flujo (último mensaje). Funcionan en el texto, las opciones, todos los campos del interactivo y las variables de plantilla
- **Vista previa en vivo** - El panel muestra arriba el mensaje como lo verá el cliente (texto con opciones, burbuja interactiva o plantilla) con las variables completadas con datos de ejemplo, y en el teléfono cada sección se abre en su propia pantalla
- **Grabar audio** - El bloque graba una nota de voz con el mismo grabador del Reply Box, permite escucharla, volver a grabarla o quitarla. Si el bloque también tiene texto, la nota de voz sale primero y el texto con sus opciones en un mensaje aparte
- **Probar como chat** - Simula la conversación en el panel tocando los botones y eligiendo el camino de cada condición; no envía nada al cliente. La prueba con una conversación real sigue disponible en el menú
- **Bloques** - Enviar mensaje, Condición, Según el valor, Esperar, Dividir al azar, Recorrer una lista, Volver a un paso de este flujo, Iniciar otro flujo, Petición HTTP, Acciones, Kanban, Buscar cards, Tarea, Evento, Avisar al equipo, Transferir a un agente, Responder con Captain, Terminar y, en Avanzado, Código. Terminar cierra el flujo sin resolver la conversación: para resolverla, pon antes la acción Resolver
- **Condiciones legibles** - Se leen como una frase ("Si las etiquetas de la conversación incluyen vip") y combinan varias reglas con Todas o Alguna, con salidas Sí y No. El campo dice de qué es ("Conversación · Estado", y los atributos personalizados dicen si son del contacto o de la conversación) y el valor se elige de una lista con datos reales: estados, prioridades, etiquetas de la cuenta, equipos, agentes, etapas del embudo con su color y las opciones de los atributos de lista; el texto libre (o una variable) queda para los campos de texto, y los operadores cambian según el campo. También preguntan si la bandeja está en horario, cuántos agentes hay en línea (en la bandeja o en un equipo), qué tareas tiene la conversación, en qué embudo y etapa, estado o etiquetas está el card, y si el último mensaje trae un adjunto
- **Acciones en orden** - Un bloque Acciones ordena la conversación con una o varias acciones de Automation (asignar, etiquetar, prioridad, estado, notas, aplicar un SLA si la cuenta tiene SLA activo, enviar un correo a equipos, participantes, webhook), de arriba hacia abajo. Kanban, enviar mensajes o archivos y responder comentarios tienen ahora su propio bloque: las filas guardadas siguen funcionando y, cuando son la única acción del bloque, el panel ofrece convertirlas. Si una acción falla, las demás corren igual y el bloque sale por "Si una acción falla" cuando esa salida está conectada; buscar "esperar" o "estado" en el selector indica el bloque Esperar y las acciones de estado
- **Esperar** - Pausa el flujo minutos, horas o días antes de seguir
- **Dividir al azar** - Reparte a los contactos entre caminos por porcentaje
- **Según el valor** - Compara un valor (con variables) con varios casos en orden, con los mismos campos, listas de valores y operadores que la Condición, y sigue por el primero que coincide o por "Ninguno coincide"; cada caso puede tener nombre y se reordena, y sus salidas muestran el nombre del equipo, el agente o la etapa
- **Bloques antiguos que siguen funcionando** - Horario de atención, Agentes disponibles, Etapa Kanban y ¿Tiene tarea abierta? ahora son filas de la Condición; Actualizar tarea y Reprogramar o cancelar evento, opciones de Tarea y Evento; y Avisar en el chat interno, la opción Sala del chat de Avisar al equipo. Ya no están en la biblioteca, pero los flujos que los usan siguen funcionando igual. En el panel, "Convertir en Condición" (o en Tarea, Evento o Avisar al equipo) los pasa al bloque nuevo manteniendo sus conexiones; nada se convierte solo
- **Recorrer una lista** - Repite un camino por cada elemento de una lista (una variable con una lista o texto separado por comas o líneas), con el elemento actual, su número y el total como variables en mensajes, campos y condiciones; el camino vuelve al bloque y al terminar sigue por "Terminado". El panel ofrece las listas de los bloques anteriores (los cards de Buscar cards, las suscripciones o facturas de Stripe) y las etiquetas de la conversación. Hasta 25 elementos por vuelta, también en "Probar"
- **Código (JavaScript)** - En el grupo Avanzado de la biblioteca, ejecuta JavaScript con los datos del flujo (contacto, conversación, último mensaje, bandeja, agente, elemento de la lista y resultados anteriores) y guarda el objeto que devuelve con un nombre (por ejemplo `codigo1`) para leerlo después como `{{ vars.codigo1.clave }}` en mensajes, campos y condiciones. Corre aislado, sin red, archivos ni temporizadores, con límites de 1 segundo, 32 MB, 10.000 caracteres y 32 KB de resultado; si falla sale por "Error". En "Probar" eliges si salió bien y escribes un resultado de ejemplo. Solo aparece si el servidor tiene el motor de JavaScript instalado
- **Petición HTTP** - Llama a una API: primero eliges el método (GET, POST, PUT, PATCH o DELETE) y la URL, y después, si hace falta, una credencial guardada, parámetros, encabezados y cuerpo JSON o de texto, todos con variables. Guarda la respuesta con un nombre (por ejemplo `respuesta1`) para leerla después como `{{ vars.respuesta1.status }}` o `{{ vars.respuesta1.body.campo }}`; después de "Probar petición", los bloques siguientes ya pueden elegir los campos de la respuesta. Sale por "Éxito" con una respuesta 2xx y por "Error" en los demás casos. Bloquea direcciones de red privada, espera hasta 30 segundos y acepta respuestas de hasta 1 MB. "Probar petición" la envía en el momento con datos de ejemplo; en las pruebas del flujo solo se envían las GET
- **Conexiones** - Guardan una vez la URL base, la autenticación (Bearer, Básica o API key) y los encabezados de una API para usarlos en cualquier bloque Petición HTTP. Los secretos se guardan cifrados y nunca se vuelven a mostrar; solo los administradores las gestionan, desde Flow Builder o desde el propio bloque. Una conexión que usa algún flujo no se puede eliminar
- **Respuestas fuera del historial** - Con "No guardar la respuesta en el historial", los bloques siguientes leen la respuesta de una Petición HTTP durante la ejecución y, al terminar, su cuerpo queda guardado como [redacted] en el historial de ejecuciones. La instalación también puede fijar cuántos días se guardan las ejecuciones terminadas (por defecto, para siempre)
- **Responder con Captain** - Pasa la conversación al asistente de Captain de la bandeja y el flujo termina; el panel avisa cuando una bandeja del inicio no tiene asistente
- **Transferir a un agente** - En "¿A quién?" eliges si la conversación queda para la bandeja (con sus reglas de asignación), para un equipo o para un agente de la bandeja. Con "Terminar el flujo", activado en los bloques nuevos, el flujo termina ahí; desactivado, sigue después de transferir. Los bloques guardados antes siguen como estaban
- **Kanban** - Crea el card de la conversación, lo mueve de etapa (corriendo las automatizaciones de la etapa), lo marca ganado, perdido o abierto o lo elimina; también le asigna un agente, le agrega una nota y agrega, quita o reemplaza sus etiquetas. "¿Sobre qué card?" elige el card de la conversación (si quieres, el que tiene en un embudo, una etapa, un estado o con unas etiquetas), el card que inició el flujo, el card del recorrido o, en avanzado, otro card desde una variable; sin card sale por "Sin card". Dentro de un recorrido, eliminar pide confirmación. Aparece solo con Kanban activo
- **Buscar cards** - Busca los cards de la cuenta por embudo, etapa, estado, etiquetas, horas en la etapa o cambio de estado reciente, hasta 100 (20 por defecto), primero los que llevan más tiempo en su etapa, y sigue por "Con cards" o "Sin cards". Con Recorrer una lista se trabaja cada card; no necesita conversación, así que sirve en un flujo Programado
- **Iniciar otro flujo** - Inicia otro flujo publicado de la cuenta en la conversación de un card (por ejemplo el del recorrido) o en esta, con datos de entrada que el otro flujo lee como `{{ inputs.clave }}`, y sigue sin esperar. El flujo llamado empieza en el bloque que sigue a su inicio, sin mirar las condiciones de ese inicio. Las ejecuciones dicen si el otro flujo se pidió, se omitió (no había conversación o no se encontró el card) o se rechazó porque ya había demasiados flujos llamándose entre sí
- **Pregunta Sí/No a Captain** - En el grupo Captain e IA, Captain responde Sí o No a una pregunta leyendo el último mensaje y la conversación; usa créditos de Captain y tiene su propia salida si no puede responder. En "Probar" no se consulta a la IA: el probador elige la rama
- **Actualizar contacto o conversación** - Cambia nombre, email, teléfono y atributos personalizados del contacto o de la conversación, con variables
- **Ejecutar macro** - Ejecuta una macro pública como el agente que la creó; "Crear macro" abre Configuración → Macros en otra pestaña y la lista se recarga al volver
- **Tarea y Evento** - Tarea crea una actividad (con vencimiento y prioridad, y si quieres vinculada al card) o completa, cancela o reabre una; Evento agenda un evento de calendario (con duración y, con Google Calendar conectado, enlace de Meet) dentro de un tiempo, en una fecha fija o en la fecha de una variable, o lo reprograma o lo cancela. Lo que crean recuerda al flujo, así que un bloque de una ejecución posterior encuentra la tarea o el evento que este flujo dejó en la conversación; si no hay, sale por "No encontrada" o "No encontrado". Se crean para un Responsable: el asignado de la conversación, un agente fijo o un rotativo por equipo o lista de agentes (opcionalmente solo en línea), con un agente de respaldo
- **Programar mensaje** - Deja programado un mensaje de la conversación, con archivos y variables, para después de un tiempo o para una fecha y hora con su zona horaria (elegidas en el calendario o tomadas de una variable), una vez o repetido como en Mensajes programados. Se envía en nombre del agente elegido (el asignado de la conversación, uno fijo o un rotativo, con respaldo) y aparece en Mensajes programados, donde el equipo puede editarlo o cancelarlo. Si la fecha no sirve o el mensaje no se puede programar, sale por "Error" cuando esa salida está conectada. Requiere la función de mensajes programados
- **Cancelar mensajes programados** - Cancela los mensajes programados de la conversación que aún no se enviaron, incluidos los que se repiten: "Solo los de este flujo" (así empiezan los bloques nuevos) o "Todos los pendientes", también los que los agentes programaron a mano. Sigue por "Cancelados" o por "Ninguno pendiente". Requiere la función de mensajes programados
- **Pedir CSAT** - Envía la encuesta de satisfacción de la bandeja con sus mismas reglas (conversación resuelta, CSAT activo, una sola vez por conversación, plantilla o ventana de respuesta) y sigue por "Enviada" o por "No enviada" con el motivo, que una Condición puede leer. Con "Resolver antes", primero resuelve la conversación si todavía no lo está. Aparece solo si la bandeja del flujo tiene CSAT activo
- **Agregar participante** - Acción del bloque Acciones: suma un agente como participante de la conversación, como el panel de participantes (recibe su notificación); un agente sin acceso a la bandeja queda como error y las demás acciones siguen
- **Nota de contacto** - Acción del bloque Acciones: agrega una nota al contacto, como el panel de notas del contacto, con variables del flujo y de la plataforma; si el texto queda vacío se registra como error y las demás acciones siguen
- **Asociar empresa** - Busca la empresa por dominio (o por su nombre exacto si no hay dominio), la crea si no existe y asocia el contacto a ella, como el panel de contactos de la empresa; el dominio puede venir de un sitio web o de un correo, con variables. Sigue por "Encontrada" o "Creada". Aparece solo si la cuenta tiene Empresas activo
- **Buscar contacto** - Busca otro contacto de la cuenta por correo, teléfono, identificador o un atributo personalizado (valor fijo o con variables), con las mismas reglas del filtro de Contactos. Sigue por "Encontrado", con sus datos disponibles en el grupo "Resultados" del selector de variables, o por "No encontrado"
- **Checklist del card** - El bloque Kanban agrega un ítem al checklist del card o marca como hecho el primer ítem abierto con ese texto, como el checklist del card, con variables; el panel ofrece los ítems que las etapas de los embudos agregan a sus cards. Sin card sale por "Sin card"; sin ese ítem el flujo sigue. Aparece solo con Kanban activo
- **Elegir opción con IA** - Captain lee el último mensaje y la conversación y elige entre 2 y 10 opciones descritas en lenguaje natural; cada opción tiene su salida, más "Ninguna" y "No pudo responder" (también sin créditos). Usa créditos de Captain; en "Probar" no se consulta a la IA: el probador elige la opción
- **Sugerir etiquetas o prioridad con IA** - Captain lee la conversación y, como las sugerencias de la barra lateral, elige hasta 3 etiquetas de la conversación o del contacto, o la prioridad; el flujo las aplica y sigue, o sale por "No pudo responder" (también sin créditos). En "Probar" no se consulta a la IA
- **Resumir conversación** - Captain escribe un resumen de la conversación (como la opción Resumir del editor) que los bloques siguientes leen como variable en "Resultados" y, si se activa, lo agrega como nota privada; sale por "No pudo responder" sin créditos o si Captain falla. En "Probar" se usa un resumen de ejemplo
- **Traducir** - Captain traduce un texto con variables (por ejemplo el último mensaje) al idioma elegido o al idioma del contacto (el que se detectó en la conversación), como la acción Traducir de un mensaje, y los bloques siguientes leen la traducción en "Resultados"; sale por "No pudo responder" sin créditos o si Captain falla. Solo aparece cuando la traducción automática está activa y Captain es el servicio de traducción de la cuenta. En "Probar" se usa una traducción de ejemplo
- **Herramienta de Captain** - Llama a una herramienta personalizada de Captain (su dirección, autenticación y plantillas) con parámetros fijos o con variables y deja la respuesta en "Resultados"; sale por "Éxito" o "Error". El panel marca los parámetros obligatorios y su tipo, y si uno queda vacío la herramienta no se llama y el bloque sale por "Error". Solo en bandejas con asistente de Captain; no ofrece herramientas apagadas, con correo verificado ni de riesgo alto. En pruebas y en "Probar" no se llama: el probador escribe una respuesta de ejemplo
- **Extraer datos del contacto con IA** - Captain lee el contacto y la conversación con el asistente de la bandeja, como lo hace su memoria: en modo Atributos sugiere los datos que menciona la conversación y que el contacto todavía no tiene, y los bloques siguientes los leen en "Resultados"; puedes limitarlos a una lista cerrada de atributos y, con "Guardar en el contacto", escribirlos en el contacto; en modo Notas escribe notas del contacto. Sale por "No pudo responder" sin créditos, sin asistente o cuando Captain falla. "Probar" nunca le pregunta a la IA
- **Consultar cliente en Stripe** - Con Stripe conectado en Integraciones, busca el correo del contacto en el Stripe de la cuenta, como la barra lateral de la conversación, y los bloques siguientes leen el nombre, correo, teléfono, id y estado de la última suscripción del cliente en "Resultados"; sale por "Encontrado", "No encontrado" (sin correo o sin cliente) o "Error" (Stripe falló o hay que volver a conectar la clave). Las pruebas y "Probar" nunca llaman a Stripe
- **Pasar a Typebot / Dialogflow** - La conversación pasa a uno de los bots de Typebot de la cuenta (asignada como cuando un agente asigna un bot, pendiente, con el mensaje del cliente) o al agente de Dialogflow conectado a la bandeja (queda pendiente, con el mensaje del cliente), y el flujo termina: desde ahí responde el bot. Muestra solo los bots que la cuenta tiene activos, y el panel nombra las bandejas del inicio que no tienen Dialogflow. Las pruebas y "Probar" no cambian nada
- **Avisar al equipo** - En "¿Cómo avisar?" eliges Notificación o Sala del chat. Notificación envía a un agente (por defecto el asignado de la conversación, un agente elegido o una rotación, con respaldo) un aviso sobre la conversación con un texto con variables: aparece en sus notificaciones y sale por push y correo según su configuración de notificaciones (preferencia "Un flujo te envía un aviso", push activado por defecto); el agente tiene que poder ver la conversación, si no el paso falla. Sala del chat publica el mensaje en una de las salas del chat de la cuenta a nombre de ese agente, que tiene que ser miembro de la sala. El flujo sigue enseguida. Las pruebas y "Probar" no avisan a nadie
- **Videollamada Dyte** - Inicia una videollamada de Dyte en la conversación como el botón de videollamada de la caja de respuesta, a nombre de un agente (por defecto el asignado de la conversación), y sale por "Error" si Dyte no puede crearla. Solo en bandejas de sitio web y API con Dyte conectado; el panel nombra las bandejas del inicio donde no funciona. Las pruebas y "Probar" no crean ninguna reunión
- **Leer datos de la cuenta (avanzado)** - Lee lo que ninguna variable ni otro bloque trae (las conversaciones y notas de un contacto, una conversación, sus mensajes con tipo, remitente y si son privados, las etiquetas, las respuestas predefinidas o una búsqueda de empresas) a nombre de un agente elegido que puede usar el asistente Mega, y los bloques siguientes leen la respuesta en "Resultados". En "¿De qué contacto?" o "¿De qué conversación?" eliges el del flujo o una variable, sin escribir ids. No se cambia ni se borra nada, y los bloques guardados con otras lecturas siguen funcionando. Solo los administradores editan flujos. Las pruebas y "Probar" no ejecutan nada
- **Solo bloques disponibles** - La biblioteca muestra solo los bloques cuya función está activa en la cuenta (Kanban, actividades, calendario, macros, Captain); si una función se apaga después, el bloque avisa en su panel y su paso falla sin repetir lo anterior
- **Ventana de 24 horas** - Fuera de la ventana de atención de WhatsApp (y de Messenger e Instagram) un mensaje que no es plantilla no se envía: el bloque sale por "Ventana cerrada" si está conectada o el flujo termina ahí
- **Una vez por conversación** - Un inicio por eventos puede limitarse para que el flujo no vuelva a empezar con cada mensaje (activado en los flujos nuevos); en modo Agente bot el flujo responde cada mensaje
- **Se pausa cuando interviene una persona** - Si un agente responde o la conversación se resuelve, el flujo que estaba esperando se cancela
- **Ordenar** - Acomoda el flujo automáticamente de izquierda a derecha
- **En el teléfono** - El flujo se lee como una lista de pasos agrupada por botón o condición, y cada bloque se edita en una hoja inferior
- **Borradores y publicación versionada** - Edita sin afectar la versión publicada; las conversaciones que están esperando siguen con la versión con la que empezaron
- **Activación y pausa por switch** - Activa o pausa flujos publicados desde el listado o el editor; al pausar se cancelan las conversaciones que estaban esperando
- **Validación antes de publicar** - Detecta ciclos que no esperan la respuesta del cliente ni son el camino de vuelta de Recorrer una lista, conexiones rotas, botones de más de 20 caracteres, repartos que no suman 100 y bloques incompletos. El aviso nombra el bloque y "Ver bloque" lo abre; los bloques con avisos se marcan en el lienzo. Una salida conectada a dos bloques es un error (solo se seguiría el primero); al conectar una salida que ya tiene destino, la conexión se mueve al nuevo bloque. Avisa de los bloques a los que ningún camino desde el Inicio llega (contando Ir a bloque). Que "Otra respuesta" de un mensaje con opciones de texto, o "Sin respuesta" de un mensaje con tiempo de espera, quede sin conectar es solo una sugerencia en el propio bloque
- **Cuatro tipos de inicio** - El Inicio es un Evento (empieza cuando algo pasa: un mensaje, un cambio en la conversación, un comentario o un card actualizado), un Agente bot (el flujo es el bot de sus bandejas y responde cada mensaje hasta pasar la conversación al equipo), Programado (corre en los horarios que elijas, sin conversación) o Webhook (corre cuando un CRM o formulario externo envía datos a la URL propia del flujo). Cada tipo se explica en una línea con un ejemplo, y los filtros finos van en una Condición después del inicio
- **Inicio Programado** - Corre cada tantos minutos (desde 5), horas, días o semanas a una hora, o con una expresión cron, en la zona horaria de reportes de la cuenta, y muestra sus próximas ejecuciones mientras lo configuras. Un horario que no se cumplió (el servidor estaba caído o la ejecución anterior seguía en curso) no se recupera, pero queda registrado en Ejecuciones. Como no hay conversación, usa bloques que no la necesitan, como Petición HTTP, Código, Condición, Según el valor, Recorrer una lista, Buscar cards, Kanban sobre un card elegido, Iniciar otro flujo y Leer datos de la cuenta. Ej. cada día hábil a las 9:00, buscar los cards ganados ayer e iniciar un flujo de seguimiento para cada uno
- **Inicio Webhook** - El flujo tiene su propia URL con un secreto (en la URL o en un encabezado) que puedes copiar, ver con un ejemplo de `curl` listo para usar y cambiar cuando quieras. Un CRM o formulario externo envía cualquier JSON o campos de formulario, recibe respuesta al instante y el flujo corre en segundo plano; los datos enviados quedan disponibles en los campos de expresión, ej. `{{ webhook.body.telefono }}`. Una clave de idempotencia opcional (ej. teléfono + email) evita que el mismo lead, enviado dos veces, corra el flujo dos veces. Cada llamada aparece en Ejecuciones con el cuerpo recibido, para ver qué falló
- **Mensaje saliente** - Elige la bandeja, busca o crea el contacto por teléfono (con y sin el 9.º dígito de Brasil; en WAHA resuelve el `@lid`), abre la conversación y envía un texto o una plantilla. Desde ahí el flujo trabaja sobre esa conversación, así cualquier otro bloque puede seguir (etiquetas, asignación, esperar la respuesta). Hasta que corre, un flujo Webhook o Programado solo usa los bloques que no necesitan conversación. Ej. llega un lead del CRM, el flujo lo saluda por WhatsApp y pasa la conversación al equipo de ventas
- **Card actualizado** - El flujo empieza en la conversación del card cuando el card se crea, cambia de etapa o de embudo, o pasa a ganado, perdido o abierto, y `{{ kanban.change }}` dice qué cambió. Un card sin conversación no inicia nada. Para seguir solo con un embudo, una etapa o un estado, pon una Condición después del inicio
- **Mensaje enviado por el equipo** - El flujo empieza cuando un agente envía un mensaje público (no un bot, otro flujo ni una campaña) y los bloques leen ese mensaje en `{{ message.* }}`; nunca continúa un flujo que espera una respuesta
- **Cambios de otros flujos** - Con "Empieza con cambios de otros flujos", el inicio también responde cuando otro flujo cambia la conversación o un card. Nunca con sus propios cambios, y una cadena de flujos se detiene a los 3 saltos
- **Una ejecución a la vez por contacto** - Si el flujo ya está corriendo para ese contacto, el nuevo inicio espera su turno (hasta un minuto aprox.). Un inicio que no llega a correr queda en Ejecuciones como error con su motivo, y una respuesta o un temporizador que esperaban nunca se pierden
- **Inicio tipo AgentBot** - El inicio puede vincularse a una o varias bandejas para atenderlas como bot nativo, con exclusividad frente a AgentBot, Dialogflow u otros flujos activos en cada una. Major puede compartir la bandeja con el flujo: el flujo responde primero y su bloque «Responder con Captain» le pasa la conversación a Major; las conversaciones nuevas de esa bandeja no se asignan a Major
- **Ignorar contactos** - El inicio puede dejar fuera a los grupos de WhatsApp y a contactos concretos, que se buscan por nombre, teléfono o email: el flujo no empieza para ellos y, si atiende la bandeja como bot, la conversación queda abierta para los agentes.
- **Inicio por eventos en algunas bandejas** - Un inicio por eventos corre en todas las bandejas o solo en las que se elijan; "Probar" usa una conversación de una de ellas
- **Flujo como AgentBot** - En modo AgentBot el flujo actúa como un Agent Bot de la plataforma: tiene su propio bot, con el nombre del flujo, y las conversaciones que atiende quedan pendientes y asignadas a ese bot, sin tomar las que ya están asignadas a una persona. Sus mensajes salen como ese bot y el bloque "Transferir a un agente" pasa la conversación al equipo igual que el handoff de un Agent Bot. El bot no aparece en Configuración → Bots ni en los selectores de bots, y queda como historial de lo que hizo el flujo cuando este se pausa, pasa a eventos o se elimina
- **Historial visual de ejecuciones en vivo** - Reproduce cada ejecución en el lienzo, marca los bloques con éxito, error o en espera y abre cada bloque para revisar entrada, salida y errores
- **Panel más amplio y biblioteca compacta** - El panel lateral es más amplio y más claro: la biblioteca muestra los bloques en dos columnas con filtros por grupo (la descripción aparece abajo al pasar el mouse), y cada bloque explica en una frase qué hace y hacia dónde sigue cada salida. El bloque Acciones busca y agrupa las acciones dentro del mismo panel
- **Probar con recorrido** - Probar muestra tu flujo como un chat de WhatsApp. Ves cada paso marcado entre los mensajes y el recorrido pintado sobre el lienzo. Donde el flujo decide con datos reales, eliges tú por dónde sigue
- **Lista de flujos** - La lista de flujos sigue el diseño de las páginas de configuración: toca cualquier fila para abrir el flujo y verás de un vistazo su estado, qué lo activa, en qué bandeja corre, cuántos bloques tiene y cuántas veces se ejecutó hoy. En el teléfono, las filas son grandes y creas un flujo con el botón flotante
- **Ejecuciones** - Cada recorrido se ve sobre las mismas tarjetas del editor: qué bloques se ejecutaron, cuánto tardaron y por qué salida siguió el flujo. Filtra por ejecuciones con error o en espera y lee cada paso en lenguaje simple, con los datos técnicos a un toque. Nada se pierde en silencio: un inicio que no pudo correr y un horario programado que no se cumplió quedan como ejecuciones con error ("No se inició") que dicen por qué, y los pasos omitidos se ven aparte de los que fallaron. Por la API y el MCP, cada ejecución dice por qué se detuvo, cuáles pasos fallaron o se omitieron, y qué flujo la inició o qué flujos inició
- **Comentario recibido** - Un inicio arranca el flujo con cada comentario de Facebook o Instagram; el mismo comentario nunca inicia el flujo dos veces. Para responder solo algunos (una plataforma, una publicación, unas palabras, sin respuestas), agrega una Condición después del inicio con los campos de Comentario; un inicio que guardó esos filtros los sigue aplicando hasta que tocas "Mover a una Condición". Los bloques de comentarios responden en público, envían la respuesta privada (una por comentario, dentro de los 7 días), ocultan o eliminan el comentario, y los mensajes leen `{{comment.text}}`, `{{comment.platform}}`, `{{comment.permalink}}`, `{{comment.post_caption}}`, `{{comment.is_ad}}` y `{{comment.username}}`. Enviar mensaje manda un mensaje directo con su ventana de 24 horas, que un comentario no abre
- **Comentarios en "Mensaje recibido" y en bots** - Los inicios "Mensaje recibido" y AgentBot suman la opción "Incluir comentarios de publicaciones (Facebook/Instagram)" para que los comentarios también inicien el flujo. Se activa sola al guardar o publicar un flujo que usa la condición Tipo, un bloque o una acción de comentarios, o un bloque Enviar mensaje que responde al comentario, y nunca se apaga sola. Cada comentario inicia el flujo una sola vez: "una vez por conversación" sigue aplicando solo a los mensajes directos. Un comentario nunca continúa un flujo que espera una respuesta
- **Condición Tipo** - En el bloque Condición, el grupo "Último mensaje" suma "Tipo" (`{{ message.kind }}`), que distingue un mensaje directo (`direct_message`) de un comentario (`comment`); el valor se elige de una lista
- **Bloques de comentarios** - La biblioteca suma el grupo "Comentarios (Facebook e Instagram)" con "Responder comentario", "Mensaje privado al comentario", "Ocultar comentario" y "Eliminar comentario", cada uno listo para usar
- **Enviar como** - Los bloques Enviar mensaje guardados como "Respuesta pública al comentario" o "Mensaje privado al comentario" siguen funcionando (solo texto con variables, sin depender de la ventana de 24 horas; si la ejecución no empezó con un comentario, siguen por la salida normal sin enviar) y el panel ofrece "Convertir en bloque de comentario". Los bloques nuevos envían un mensaje directo; los comentarios se responden con los bloques de Comentarios, y el panel avisa cuando uno está en un flujo cuyo inicio no recibe comentarios
- **API, MCP y Mega Assistant** - Los administradores pueden gestionar los flujos fuera del editor: todos los endpoints de Flow Builder están en la documentación de la API (Swagger/OpenAPI y la colección de Postman, con ejemplos, desde Super Admin → Documentación API), y el servidor MCP de la cuenta y Mega Assistant pueden listar, crear, editar, revisar, probar, publicar y pausar flujos, ver sus ejecuciones y gestionar las conexiones. Para armar un flujo desde cero consultan una referencia con la configuración, las salidas y un ejemplo de cada bloque. Solo con Flow Builder activo en la cuenta y solo para administradores

### Macros

Ejecuta múltiples acciones con un solo clic:

- **Macros personales** - Visibles solo para ti
- **Macros globales** - Disponibles para todo el equipo
- **Acciones en cadena** - Combina múltiples operaciones
- **Acceso desde el editor** - Escribe `#` para buscar, previsualizar y ejecutar macros sin salir de la conversación
- **Atajo en la barra de comandos** - Abre `Cmd/Ctrl + K` en una conversación para seleccionar la misma macro ordenada; los atributos requeridos usan el diálogo compartido de resolución
- **Macros en lote** - Selecciona varias conversaciones en la lista y ejecuta una macro en todas desde la barra de selección (en el teléfono, **Más** → **Ejecutar macro**), tras una confirmación

### Agent Bots

- **Bots de webhook** - Conecta con lógica externa vía HTTP
- **Integración Typebot** - Conecta con flujos conversacionales de Typebot
- **Handover a humanos** - Transferencia fluida a agentes reales
- **Handover inteligente** - Si un humano responde en conversación pendiente del bot, se transfiere automáticamente
- **Respuestas humanas en el webhook** *(Mega)* - Opcional por bot Webhook: recibe también las respuestas del agente, desde el panel o desde el celular en WhatsApp, para que el bot conserve el contexto de la atención humana. Desactivado por defecto
- **Vencimiento con handover** - Al vencer una sesión de Webhook, la conversación se abre, libera al bot e intenta la asignación automática a un agente elegible; si no hay nadie disponible queda abierta y sin asignar
- **Bots por inbox** - Configura bots específicos por canal
- **Propiedad explícita del bot** - Las conversaciones gestionadas por un Agent Bot conectado quedan pendientes y asignadas al bot; una apertura, handover humano o desconexión del bot libera esa propiedad sin reemplazar asignaciones humanas explícitas
- **El bot se calla tras el traspaso** - Un Agent Bot Webhook solo recibe los mensajes del cliente mientras la conversación está pendiente (o asignada a él); cuando se traspasa al equipo deja de recibirlos, así que no puede seguir respondiendo una conversación que ya tomó una persona. Sigue enterándose cuando la conversación se abre, se resuelve o cambia de estado, pero no de los cambios del equipo como etiquetas o asignado, y los bots configurados para recibir respuestas humanas siguen acompañando toda la conversación
- **Cola sin asignar humana** - Las conversaciones asignadas a un Agent Bot no aparecen en la cola Sin asignar; solo incluye conversaciones sin agente humano ni bot
- **Toma de control desde el panel** - Mientras un Agent Bot gestiona una conversación pendiente, el compositor queda en nota privada y muestra una acción para tomar el control, reabrir la conversación y asignarla al agente actual
- **Asignación manual restringida por inbox** - El selector de agente solo ofrece Agent Bots activos configurados en el inbox de la conversación
- **Indicador de escritura** - Los bots pueden activar y desactivar el indicador "escribiendo..." para una experiencia más natural
- **Opciones avanzadas de webhook** *(Enterprise)* - Configura timeout personalizado para peticiones del bot, reintentos automáticos ante fallos, y manejo de errores granular; mejora la fiabilidad de integraciones con sistemas externos lentos o inestables
- **Firmas de webhook por canal** - Permite firmar eventos salientes de Agent Bots y canales API para validar autenticidad extremo a extremo

### Typebot *(Mega — Opciones Avanzadas)*

Además de la integración estándar de Typebot, MEGA extiende sus capacidades con comandos especiales:

- **Asignación de agente vía MEGA_CMD** - Usa el comando `MEGA_CMD:assign_agent:email@empresa.com` en Typebot para asignar automáticamente la conversación a un agente específico
- **Asignación de equipo vía MEGA_CMD** - Usa `MEGA_CMD:assign_team:nombre_equipo` para derivar la conversación al equipo correspondiente desde el flujo del bot
- **Placeholders de lista** - Inyecta listas dinámicas de agentes o equipos como variables Typebot para crear menús de selección personalizados
- **Primer mensaje multimedia** - Si la primera interacción llega solo con media, la conversación se abre correctamente
- **Reacciones de WhatsApp ignoradas** - Las reacciones no inician el flujo ni se envían como mensajes al Typebot
- **Ubicación compatible** - Reenvío de coordenadas en formato de enlace de mapas para continuidad del flujo
- **Delay por defecto estable** - Mejor consistencia en tiempos de espera cuando el bot no define delay explícito
- **Sin código adicional** - Todo se configura directamente en el flujo de Typebot, sin modificar el bot de MEGA

### Captain *(Enterprise)*

- **Nombre del asistente de IA con tu marca** - Captain se muestra como **Major** por defecto, y cada instalación puede ponerle su propio nombre desde Super Admin (Configuración → Captain). El nombre aparece en todo el panel, en el servidor MCP para cualquier IA conectada y en Mega Assistant, sin cambiar integraciones, API ni herramientas existentes.
- **Captain más seguro al responder y toma de control** - Captain ya no envía al cliente texto técnico de herramientas: reintenta una vez y, si sigue mal, deriva a un humano sin cobrar crédito. Los agentes pueden tomar el control de conversaciones de Captain con un clic y quedan asignados ellos, sin que la asignación automática se la pase a otro.
- **Sugerencias de etiquetas y prioridad** - Captain sugiere hasta tres etiquetas existentes para la conversación o el contacto, y una prioridad según los mensajes públicos recientes. Los agentes pueden aceptar o descartar las sugerencias; al volver a solicitarlas, el modelo genera una respuesta nueva. Si la prioridad recomendada ya está aplicada, la barra lateral lo indica; al aceptar etiquetas, descarta la sugerencia anterior. Habilita `captain_classifier` para la cuenta y selecciona el modelo de clasificación de conversaciones en la configuración de Captain de la cuenta o del plan; la solicitud no consume créditos de respuestas de Captain. Funciona con el Captain Decision Router: la clasificación puede usar un modelo de decisión como Jev (vía OpenRouter), que responde con probabilidades en milisegundos y a muy bajo costo, o cualquier modelo de chat (OpenAI, Anthropic, Gemini o compatibles).
- **Ruteo inteligente de Captain y Mega Assistant** - El Captain Decision Router puede elegir el escenario de Captain que atiende cada mensaje, las herramientas personalizadas más útiles cuando hay muchas, y en Mega Assistant las guías que necesita el pedido y si conviene el modelo de tareas complejas. Entiende lo que se pide aunque no se usen las palabras exactas, y vuelve a decidir en cada mensaje: si el cliente cambia de tema, la conversación pasa al escenario que corresponde en vez de quedarse en el primero que respondió. Se configura en la sección Captain Decision Router de cada cuenta en Super Admin: se elige un modelo (por ejemplo Jev o cualquier modelo de chat) y un modo, Solo medir para comparar sin cambiar respuestas o Activo para aplicarlo; apagado o sin modelo se mantienen las reglas por palabras clave.

Asistente de IA avanzado impulsado por modelos de lenguaje para automatización inteligente del servicio al cliente.

**Captain Assistants:**

- **Capacidades por proveedor** - Los superadministradores declaran modelos de chat, embeddings, transcripción de audio y PDF/documentos por proveedor. Gemini admite las cuatro rutas nativas y Anthropic chat y PDF/documentos; los endpoints compatibles con OpenAI solo se pueden seleccionar para capacidades configuradas explícitamente. La capacidad Decisiones marca los modelos que responden en la API System One (por ejemplo `typesafe/jev-1.13` en OpenRouter).

Crea y configura asistentes de IA adaptados a las necesidades de tu negocio:

- **Múltiples asistentes** - Crea diferentes asistentes para diferentes propósitos
- **Configuración personalizada** - Ajusta temperatura, modelo y parámetros de comportamiento
- **Modelos por función** - Configura modelos separados para Assistant, Copilot, sugerencias, generación de FAQs desde documentos y PDFs
- **Historial del Copilot y aviso de créditos** - El Copilot guarda tus chats anteriores para retomarlos, y los administradores reciben un email cuando se usó la mayor parte de las AI Actions del período
- **Condiciones de Captain en automatizaciones** - Describe con tus palabras qué debe detectar una regla ("el cliente quiere cancelar") y Captain revisa cada conversación o mensaje; cada revisión descuenta las AI Actions de su modelo, y solo cuando la respuesta importa
- **Valores predeterminados de proveedor** - Los superadministradores configuran de forma segura OpenAI, Anthropic y Gemini, eligen el proveedor/modelo predeterminado de Captain y cada cuenta puede heredarlo o seleccionar un modelo disponible por función; Captain hereda las opciones compatibles guardadas para el modelo seleccionado
- **Enrutamiento de modelos internos** - Los superadministradores pueden configurar por separado el evaluador de conversaciones inactivas; la sobrescritura de cuenta tiene prioridad sobre el modelo de instalación en entornos autohospedados, mientras las preferencias de Captain para clientes mantienen ocultas las funciones internas
- **Sugerencias de FAQ desde conversaciones** - Las conversaciones resueltas con respuestas reutilizables de agentes humanos se agrupan en sugerencias de FAQ revisables; los agentes solo revisan sugerencias y conversaciones fuente a las que tienen acceso, y pueden editar, aprobar o descartar sugerencias abiertas para publicar FAQ confiables
- **Entrenamiento con conocimiento** - Entrena asistentes con los documentos de tu negocio
- **Asignación a inbox** - Vincula asistentes a canales específicos
- **Avatar propio** - Sube una imagen para cada asistente, que se muestra junto a sus respuestas en el widget de chat; al quitarla vuelve el logo por defecto
- **Ajustes para administradores** - Las páginas de ajustes y escenarios del asistente se abren solo para administradores; los agentes siguen trabajando con Major en sus conversaciones
- **Asignación manual de conversaciones** - Las cuentas con Captain habilitado pueden seleccionar el asistente configurado para el inbox de la conversación; al asignarlo queda pendiente y, al quitarlo o asignar una persona, la conversación se abre. Reabrir una conversación (a mano, en lote, con una macro o al terminar una posposición) se la quita a Major, y una macro o automatización que asigna un agente la abre como una asignación directa. Major solo toma y responde conversaciones mientras la cuenta tenga Captain habilitado
- **Un bot por bandeja** - Cada bandeja la atiende un solo proveedor de bots: un Agent Bot, Dialogflow, un flujo del Flow Builder en modo AgentBot o Major. Conectar un segundo se rechaza con un mensaje que indica cuál desconectar primero; las bandejas que ya tenían dos siguen funcionando. La excepción es un flujo con Major: el flujo responde primero y su bloque «Responder con Captain» le pasa la conversación a Major. Major no responde ni programa resoluciones automáticas en bandejas con un Agent Bot o Dialogflow
- **Resumen del asistente** - El resumen de Captain combina insights del período con métricas de resultados, flujo y tendencia de resolución, CSAT de Captain, calidad del runtime, uso y cobertura de conocimiento; filtra por días, esta semana o la pasada, o por mes, y haz clic en una métrica, un motivo de transferencia o el flujo de resolución para ver las conversaciones detrás (administradores)
- **Detalles de generación** - Abre el indicador “Generado por Captain” en una respuesta del asistente o nota privada de transferencia para ver sus pasos de herramientas y escenarios, fuentes de la base de conocimientos y razonamiento; el modelo y los créditos solo están disponibles para superadministradores
- **Citas confiables** - Captain V2 muestra únicamente enlaces web públicos validados por el servidor, registra las fuentes realmente seleccionadas y mantiene las URLs renderizadas fuera del historial enviado al modelo; las sesiones anteriores conservan sus fuentes existentes
- **Runtime acotado** - Captain V2 limita el contexto de conversación y las capacidades activas por ejecución, usa un resumen semántico compacto con respaldo seguro cuando se omite historial, rechaza coincidencias de conocimiento irrelevantes, registra métricas seguras de runtime y protege las herramientas de escritura contra ejecuciones obsoletas o repetidas. Los detalles de generación exponen diagnóstico seguro por ejecución de contexto y resumen; el panel de calidad mide latencia y respaldos del resumen, mientras los casos golden configurados se ejecutan diariamente sin ejecutar herramientas.
- **Runtime único** - Toda cuenta con Captain usa Captain V2; el runtime anterior, su verificación de falsas promesas y su clasificador de acciones se retiraron, así que los asistentes se configuran solo con escenarios, pautas y guardrails
- **Comprensión de imágenes** - El asistente puede analizar imágenes enviadas en las conversaciones
- **Soporte multimodal** - Procesa texto e imágenes simultáneamente para respuestas contextuales
- **Ignorar grupos** - Configura el asistente para no responder en conversaciones grupales
- **Objetivos ignorados** - Define conversaciones o contactos específicos que el asistente debe omitir
- **Audiencia y horario** - Limita las respuestas a contactos que cumplan condiciones configurables y elige si el asistente responde siempre, durante el horario laboral o fuera de él; las conversaciones fuera de esas reglas pasan a la cola humana. "Espera antes de responder" (hasta 10 segundos) permite que el asistente conteste con una sola respuesta a los clientes que dividen un pedido en varios mensajes
- **Resolución por inactividad** - Con Captain V2, cada asistente elige si Captain revisa la conversación, siempre la resuelve o espera al cliente; los modos que resuelven usan un temporizador de 5 minutos a 24 horas y pueden enviar un mensaje de cierre opcional. La revisión tiene tres resultados: la conversación está completa, espera al cliente o necesita una persona. Cuando el siguiente paso es del cliente, Captain resuelve la conversación en lugar de transferirla, con el mensaje de cierre en el idioma del cliente y sin encuesta CSAT; si el cliente vuelve a escribir, la conversación vuelve a pendiente y una resolución posterior envía la encuesta como siempre

**Captain Documents:**

Sube documentos para entrenar tu asistente de IA:

- **Carga de documentos** - Añade PDFs, archivos de texto y más (hasta 10MB)
- **Procesamiento automático** - Los documentos se procesan e indexan automáticamente
- **Campos de auto-sincronización** - Guarda estado y fecha de sincronización para mantener fuentes documentales alineadas
- **Auto-sincronización escalonada** - Actualiza fuentes web según el plan con ejecución distribuida para evitar picos de carga
- **Respuestas relacionadas** - Ve qué respuestas usan cada documento
- **Detalles del documento** - Revisa el contenido rastreado, los metadatos de origen y el
  recuento de preguntas frecuentes generadas
- **Uso en conversaciones** - Los administradores pueden ver las conversaciones distintas que usaron un documento o una FAQ creada por un usuario, ordenar documentos por uso y abrir la lista de conversaciones; se excluyen transferencias y conversaciones eliminadas
- **Gestión masiva** - Añade y elimina documentos fácilmente

**Captain Scenarios:**

Configura escenarios y flujos de trabajo específicos:

- **Instrucciones personalizadas** - Define comportamiento para situaciones específicas
- **Asignación de herramientas** - Asigna herramientas específicas por escenario
- **Gestión de estado** - Los administradores pueden habilitar o deshabilitar escenarios; los deshabilitados siguen disponibles para administrarlos, pero Captain no los ejecuta
- **Creación completa por MCP** - Las IA conectadas al MCP de la cuenta pueden guardar y actualizar IDs de herramientas integradas, personalizadas y MCP; los IDs no disponibles se rechazan explícitamente
- **Reglas de activación** - Define cuándo aplica cada escenario
- **Ordenamiento por prioridad** - Controla la precedencia de escenarios

**Captain Custom Tools:**

Crea herramientas personalizadas para tu asistente de IA:

- **Contratos tipados completos** - Las tools personalizadas y MCP conservan objetos, arrays, enums y campos anidados; solo se ofrecen al escenario cuando están habilitadas y conectadas

- **Integraciones HTTP** - Conecta con APIs externas (GET/POST/PUT/PATCH/DELETE)
- **Autenticación** - Soporte para Basic, Bearer y API Key
- **Mapeo de parámetros** - Define parámetros de entrada/salida
- **Activar/desactivar** - Alterna herramientas según necesites
- **Desactivación segura** - Los administradores reciben una advertencia antes de desactivar una herramienta usada por escenarios habilitados; las herramientas deshabilitadas siguen visibles y conservan las referencias guardadas sin ejecutarse
- **Verificación de correo para herramientas sensibles** - Una herramienta puede exigir que el cliente confirme su correo con un código de 6 dígitos antes de que Captain la use. Captain envía el código por correo (con el nombre de tu bandeja), pide al cliente que lo escriba en el chat y recién entonces ejecuta la herramienta. Un parámetro "correo verificado" envía esa dirección confirmada a tu API, así nadie puede consultar la cuenta de otra persona escribiendo su correo. Las herramientas nuevas que modifican datos empiezan con la opción activada

**Captain MCP Servers:**

Conecta servidores MCP (Model Context Protocol) para ampliar las capacidades de tu asistente:

- **MCP nativo por cuenta** - Crea servidores MCP propios por cuenta con endpoint dedicado
- **MCP pensado para agentes** *(Mega)* - Cada herramienta indica su módulo, su intención (buscar, leer, crear, enviar, programar, diagnosticar), sus efectos y lo que necesita, y las herramientas parecidas explican cuándo usar cada una; los errores traen un código estable, si se pueden reintentar y un identificador de la solicitud; los envíos y las programaciones aceptan una clave de idempotencia opcional: un reintento con la misma clave no se envía dos veces, y una llamada sin clave se envía siempre, como antes (la protección es optativa); `account_context` dice qué puede hacer el servidor y por qué no; las ejecuciones y los flujos de Flow Builder se leen sin el grafo completo (una ejecución de 10 pasos: de 151 KB a 1,7 KB). Todo es aditivo: los clientes existentes siguen funcionando igual
- **Acceso seguro y flexible** - Compatible con autenticación OAuth y token estático
- **Archivos para cualquier proveedor de IA** - ChatGPT descubre su selector nativo; Claude y otros clientes pueden usar URL temporal HTTPS, base64, multipart o signed ID sin exigir una URL pública permanente
- **Carga directa autenticada** - Los clientes MCP JSON pueden solicitar destinos firmados mediante la API sin depender de CSRF del navegador
- **Outbound universal por MCP** - Inicia texto, multimedia o plantillas para teléfono, email, contacto o identificador del proveedor; admite archivos directos también en cabeceras multimedia de plantillas y rechaza referencias inválidas antes del envío
- **Catálogo de uso cotidiano** - Publica herramientas listas para operaciones diarias de la cuenta
- **Cobertura operativa ampliada** - Incluye programación, tareas, campañas, SLA, calendario, reportes, notificaciones y chat interno; no expone importación ni exportación de datos
- **Help Center por MCP** - Consulta, busca y obtiene artículos y categorías desde agentes conectados
- **Asignación a asistentes** - Vincula servidores MCP a asistentes específicos
- **Acciones nativas atribuidas a Captain** - Las ejecuciones MCP nativas firmadas conservan al asistente como remitente y confirman mensajes entregados sin duplicados ni handoff accidental
- **Playground fiel a producción** - El catálogo permanece disponible para configurar escenarios. Con Captain V2, el playground prueba handoffs reales y carga solo las tools asignadas al escenario; el flujo legacy prueba el asistente base sin selección directa
- **Configuración de prueba del Playground** - Prueba en el Playground escenarios guardados (incluso desactivados) o temporales, pautas de respuesta, límites y hasta 10.000 caracteres de conocimiento pegado sin cambiar el asistente; los administradores pueden guardar un elemento temporal o el conocimiento pegado (como documento Markdown) con un clic, y cada respuesta muestra quién respondió, las tools que llamó, las llamadas fallidas y su duración. Las respuestas del Playground usan créditos de Captain
- **Gestión centralizada** - Administra todos tus servidores MCP desde la configuración

**Captain Auto-Resolve Mode:**

Configura cómo Captain maneja la resolución automática de conversaciones:

- **Modo evaluado** - Captain analiza el contexto, incluido el estado de la conversación y los roles de los participantes, y decide autónomamente si la conversación está completa, espera al cliente (en ambos casos se resuelve; un cierre a la espera del cliente no envía encuesta CSAT) o necesita una persona (se transfiere); las transferencias y seguimientos pendientes se mantienen sin resolver
- **Mensajes en el idioma del cliente** - Si el asistente no tiene un mensaje de transferencia o de resolución propio, el texto por defecto llega en el idioma en que escribe el cliente, no en el de la cuenta, y al transferir por inactividad el cliente también recibe el aviso
- **Modo legado** - Comportamiento anterior: resuelve automáticamente conversaciones pendientes según el temporizador
- **Modo deshabilitado** - Captain no resuelve conversaciones automáticamente
- **Por asistente** - Cada asistente guarda su propia política; los asistentes sin política guardada conservan la configuración de cuenta como compatibilidad

**Captain Copilot:**

Asistencia de IA en tiempo real para tus agentes:

- **Hilos de Copilot** - Conversaciones persistentes con la IA
- **Contexto inteligente** - La IA entiende el contexto de la conversación
- **Herramientas de agente** - Busca conversaciones, contactos, artículos
- **Sugerencias** - Sugerencias de respuesta impulsadas por IA
- **Borradores guiados por asistente** - Al sugerir una respuesta, Copilot usa las instrucciones, FAQs, citas y herramientas GET del asistente seleccionado; el agente revisa y edita el borrador antes de enviarlo
- **Sugerencias legibles** - Las sugerencias largas expanden el editor de respuesta hasta 350 px sin reemplazar el tamaño elegido manualmente
- **Panel más cómodo** - El chat de Copilot sigue la respuesta mientras llega, pero no te mueve si subiste a leer; puedes pegar texto mientras se envía el mensaje anterior, y en celulares el teclado no se abre solo
- **Detener y ampliar** - Un botón Detener en la caja de texto corta la respuesta que Copilot está preparando, sin cobrar una AI Action por ella; un botón para ampliar ensancha el panel en pantallas grandes, y el panel también entra junto al resumen de Major
- **Límite de uso marcado como fallido** - Cuando se agotan las AI Actions, el aviso de Copilot se guarda como mensaje fallido, para que las integraciones no lo tomen como una respuesta
- **Acceso a atributos de contacto** - Captain puede leer y usar los atributos personalizados del contacto para respuestas más precisas

**Flujos de trabajo de Copilot *(premium, requiere los flags `captain_integration` y `copilot_workflows`)*:**

Copilot resuelve pedidos de varios pasos sobre los datos de la cuenta:

- **Trabajo de varios pasos** - Copilot planifica y ejecuta varios pasos para un pedido, muestra cada paso en el panel y sigue trabajando aunque cierres el panel; la respuesta te espera al volver
- **Reportes del dashboard** - Lee los mismos números que muestran las páginas de reportes (conversaciones, resoluciones, tiempos de primera respuesta, resolución y respuesta, mensajes, resoluciones y derivaciones de bots) por día, semana, mes o año, por agente, bandeja, equipo o etiqueta, ordenados por la métrica pedida, con gráficos cuando se piden
- **Directorio y datos de la cuenta** - Encuentra agentes, bandejas, equipos y etiquetas por nombre, y cuenta, agrupa y filtra los registros de la cuenta (conversaciones, contactos, mensajes, CSAT, artículos y una lista permitida de otras tablas de la cuenta); las columnas secretas, como tokens y credenciales, y las claves JSON con nombre de secreto quedan fuera de lo que Copilot lee
- **Revisión de conversaciones en lote** - Revisa cientos de conversaciones en segundo plano según la pregunta del agente, con una tarjeta de progreso, la cobertura (revisadas, coincidentes, fallidas, restantes) y un enlace a cada conversación que cita; los números y enlaces que ninguna herramienta devolvió se verifican y los enlaces desconocidos se quitan
- **Cambios con tarjeta de aprobación** - Copilot propone cambios y una tarjeta de aprobación muestra qué va a cambiar antes de hacer nada; al aprobar, cada registro se vuelve a verificar con los permisos del agente que aprueba. 17 acciones: cambiar estado, prioridad, agente, equipo, etiquetas, atributos personalizados y SLA, agregar participantes, notas privadas y respuestas, silenciar o reactivar, y en contactos agregar etiquetas, notas y atributos o bloquear y desbloquear
- **Bloques visuales bajo la respuesta** - Copilot puede mostrar tablas, métricas destacadas, gráficos, tarjetas, líneas de tiempo, tarjetas de contactos y conversaciones y botones de seguimiento bajo su respuesta, con el mismo diseño que Mega Assistant; los contactos y conversaciones solo aparecen si el agente puede abrirlos, y un botón de seguimiento envía su pregunta como el siguiente mensaje del agente, nunca un cambio
- **Detener rechaza las aprobaciones pendientes** - Al pulsar Detener el flujo termina y se rechazan los cambios que esperaban aprobación; una aprobación sin respuesta vence a los 5 minutos
- **Modelos desde Super Admin** - La ruta de modelo `copilot_workflows` elige el modelo de los flujos y `copilot_screening` el que filtra conversaciones antes de una revisión; el filtrado queda apagado hasta que se le asigne un modelo

**Acciones de IA:**

- **Sugerencias de respuesta** - La IA genera respuestas sugeridas
- **Resumen de conversación** - Obtén contexto rápidamente
- **Búsqueda de FAQs** - Encuentra FAQs relevantes automáticamente
- **Handoff** - Transferencia inteligente a agentes humanos
- **Etiquetado automático** - La IA sugiere etiquetas para conversaciones
- **Actualizaciones de prioridad** - La IA recomienda cambios de prioridad
- **Notas privadas** - La IA puede añadir notas internas

**Monitores de conversaciones** *(Enterprise/Mega)*:

Sigue los temas que importan en tus conversaciones, descritos con tus palabras:

- **Condiciones en lenguaje natural** - Describe qué buscar (pedidos de reembolso, problemas para iniciar sesión, intención de cancelar...) y Captain revisa cada conversación con esa condición
- **Diez plantillas** - Empieza con monitores listos para soporte, ventas, producto, finanzas y operaciones
- **Vista previa antes de guardar** - Prueba una condición en hasta cinco conversaciones recientes
- **Historial y actualizaciones en vivo** - Un monitor nuevo revisa las conversaciones de los últimos siete días y luego cada mensaje nuevo de clientes o agentes
- **Informe por monitor** - Conversaciones que coinciden por hora, seis horas o día, con las conversaciones de cada barra para administradores; el informe se actualiza solo
- **Pausar y reanudar** - Pausa sin perder resultados; reanuda revisando el periodo en pausa o desde ahora
- **Automatizaciones** - El nuevo evento *Monitor encuentra una conversación* ejecuta acciones la primera vez que un monitor encuentra una conversación con actividad nueva
- **Alertas en Slack** - Elige un canal de Slack por monitor para recibir un mensaje la primera vez que encuentra una conversación por actividad nueva en vivo; al desconectar Slack se apagan las alertas. Las alertas mantienen la revisión en vivo encendida, lo que puede usar más AI Actions
- **Tu modelo, tus AI Actions** - Super Admin elige el modelo (un modelo de decisión como Jev o cualquier modelo de chat); cada conversación revisada consume las AI Actions de ese modelo y los monitores esperan mientras la cuenta no tenga
- **Dónde** - Ajustes › Captain › Monitores, también en el menú de Captain; escritorio y celular

**Transcripción de Audio:**

Transcribe automáticamente mensajes de audio a texto:

- **Transcripción automática** - Convierte notas de voz en texto legible
- **Control de grabaciones de llamadas** - Activa o desactiva la transcripción de grabaciones por proveedor (WhatsApp Cloud y WaVoIP)
- **Diarización de llamadas** - Separa las grabaciones por turno usando el nombre del contacto y del agente asignado
- **Transcripción manual** - Permite encolar la transcripción desde el menú contextual cuando un audio aún no tiene texto
- **Major sigue respondiendo** - Si el proveedor rechaza una nota de voz (archivo inválido o bloqueado por sus filtros de contenido), Major responde igual sin esa transcripción en vez de reintentar o quedarse en silencio
- **Modelos OpenAI** - Usa GPT-4o Mini Transcribe por defecto para notas de voz, con Whisper disponible como override por cuenta; para grabaciones de llamadas normaliza el audio y combina GPT-4o diarizado con GPT-4o Transcribe para mejorar fidelidad
- **Multi-idioma** - Soporte para múltiples idiomas
- **Contexto en conversaciones** - Los agentes pueden leer el contenido de los audios rápidamente

**Proveedores de IA soportados:**

- **OpenAI** - GPT-4o, GPT-4, GPT-3.5 Turbo
- **Anthropic** - Claude (Sonnet, Opus, Haiku)
- **Google** - Gemini (Pro, Flash)
- **Azure OpenAI** - Implementaciones de OpenAI en Azure
- **Amazon Bedrock** - Modelos alojados en AWS
- **DeepSeek** - Modelos de IA de código abierto

---

## 👥 CRM y Gestión de Contactos

### Perfiles de Contacto

- **Información completa** - Nombre, email, teléfono, ubicación
- **Avatar automático** - Foto de perfil cuando disponible
- **Última actividad** - Seguimiento de interacciones
- **Tipo de contacto** - Visitante, Lead, Cliente; un contacto pasa a lead cuando tiene email, teléfono, identificador o ID de WhatsApp, cuando inicia una conversación, o cuando se crea desde el panel, la API o una importación, y nunca vuelve a visitante
- **Historial del contacto en la conversación** - Al inicio de una conversación, una píldora abre la conversación anterior del contacto; la siguiente aparece en conversaciones resueltas o mientras la lista muestra a ese contacto. **Ver todas las conversaciones** en el panel de contacto (**Historial** en el teléfono) limita la lista de conversaciones al contacto, de la más reciente a la más antigua, y el botón de limpiar vuelve a la lista completa
- **Modo lectura en conversaciones anteriores** - Abrir una conversación anterior desde el hilo limita la lista al contacto; las conversaciones antiguas se abren con el cuadro de respuesta plegado en **Responder a esta conversación anterior** (con **Ir a la última conversación**), para que nadie responda un hilo viejo por error. La barra, un atajo de respuesta o cualquier acción de escritura abre el editor; la última conversación conserva el editor normal y al limpiar el filtro se vuelve a ella

### Atributos Personalizados

- **Campos flexibles** - Crea atributos para contactos y conversaciones
- **Tipos de datos** - Texto, número, lista, fecha, checkbox, enlace
- **Integración con automatizaciones** - Usa atributos como condiciones
- **Visibilidad configurable** *(Enterprise)* - Define qué roles pueden ver cada atributo; oculta campos sensibles a agentes de menor nivel
- **Copiar tal como se ve** - Al copiar un atributo de fecha se copia la fecha tal como se muestra

### Etiquetas

- **Organización flexible** - Categoriza contactos y conversaciones
- **Etiquetas de conversación** - Clasifica por tema o estado
- **Búsqueda rápida al asignar** - Filtra etiquetas de forma difusa desde el menú contextual de una conversación, con las ya asignadas primero
- **Etiquetas de contacto** - Segmenta tu base de clientes
- **Colores personalizados** - Identificación visual rápida

### Empresas/Companies *(Enterprise)*

- **Agrupa contactos** - Organiza contactos por empresa
- **Selector de empresa en contactos** - Asigna, limpia o crea una empresa directamente desde el formulario del contacto
- **Acceso por rol personalizado** - Los administradores pueden otorgar el permiso "Administrar empresas" a los roles personalizados para que vean y gestionen el menú Empresas
- **Dominio automático** - Asociación por dominio de email
- **Vista unificada** - Historial de todas las conversaciones de la empresa
- **Favicon automático** - El sistema descarga automáticamente el favicon del dominio de la empresa para mostrar como avatar; funciona con cualquier sitio web que tenga favicon configurado
- **Enriquecimiento de empresas** *(premium, desactivado por defecto)* - Con la función Company Enrichment y la clave de Context.dev de la instalación, una empresa nueva con dominio recibe automáticamente su descripción, industria, tamaño, ubicación, teléfono y redes sociales (una consulta por dominio); los administradores pueden actualizarlo desde la página de la empresa

### Notas

- **Notas por contacto** - Documenta información importante
- **Historial interno** - Mantén contexto entre interacciones
- **Notas largas desde la conversación** - La caja de notas del panel de contacto de la conversación no tiene contador de caracteres, así que se pueden escribir notas largas ahí

### Importación de Datos

- **CSV Upload** - Importa contactos masivamente
- **Mapeo de campos** - Asocia columnas con atributos
- **Importación histórica de Intercom y Freshdesk** - Los administradores pueden importar contactos, conversaciones y mensajes históricos de Intercom o Freshdesk en segundo plano. Las importaciones resisten cortes de conexión con la base de datos (tres reintentos con espera creciente), y las de Freshdesk usan la versión en texto plano de cada mensaje y omiten solo el mensaje cuyo HTML está demasiado anidado, en lugar de fallar la importación
- **Monitoreo de importación** - Revisa el progreso, registros omitidos, errores y descarga los registros de omisiones
- **Reintento de importación detenida** - Reintenta una importación detenida de Intercom o Freshdesk tras 15 minutos sin perder su progreso
- **Validación automática** - Detecta errores antes de importar
- **Acceso controlado** - Importación y exportación disponibles para administradores y responsables de contactos
- **Exportación segura** - Los valores que comienzan con caracteres de fórmula se exportan como texto para impedir su ejecución en hojas de cálculo

### Bloqueo de Contactos

- **Bloqueo manual** - Evita mensajes de contactos problemáticos
- **Filtrado automático** - No aparecen en la bandeja principal
- **Bloqueo activo en WhatsApp** - Los mensajes entrantes de contactos bloqueados se descartan automáticamente antes de abrir conversación

### Preferencias de Mensajes por Contacto *(Mega)*

- **Omitir saludo** - El contacto no recibe el mensaje de bienvenida del inbox
- **Omitir CSAT** - El contacto no recibe la encuesta de satisfacción al resolver la conversación
- **Omitir nombre del agente** - Los mensajes enviados al contacto no llevan el nombre del agente al inicio
- **Guardadas en el contacto** - Se mantienen en conversaciones nuevas y reaperturas
- **Proveedores** - Aplican en inboxes de WhatsApp con Evolution, WAHA y UAZAPI; se editan desde el panel de la conversación o la ficha del contacto

### CRM V2 *(Beta)*

Gestión de contactos mejorada con mayor flexibilidad:

- **Contactos sin identificadores** - Permite contactos sin email o teléfono
- **Búsqueda mejorada** - Mejor descubrimiento y filtrado de contactos
- **Búsqueda por empresa** - Encuentra contactos por nombre de empresa/compañía
- **Contactos resueltos** - Lógica más inteligente para identificar contactos reales
- **Compatibilidad con exportación** - Funciona con todas las funciones de exportación
- **Scroll infinito** - Carga automática de más contactos al desplazarte
- **Paginación inteligente** - Indicador de más resultados disponibles

---

## 📢 Campañas Masivas

Sistema completo de campañas para comunicación proactiva con clientes a través de múltiples canales.

### Tipos de Campañas

#### Campañas Ongoing (Live Chat)

Mensajes proactivos para visitantes de tu sitio web:

- **Triggers por URL** - Activa campañas en páginas específicas
- **Triggers por tiempo** - Muestra mensaje después de X segundos en la página
- **Triggers por eventos** - Activa según comportamiento del usuario
- **Horarios de negocio** - Solo dispara durante horario laboral
- **Habilitación/deshabilitación** - Activa o pausa campañas fácilmente

#### Campañas One-Off (Envío Único)

Envíos masivos a una audiencia segmentada:

- **WhatsApp** - Campañas vía WhatsApp Business
- **SMS (Twilio)** - Mensajes de texto masivos
- **SMS (Bandwidth/otros)** - Proveedores SMS alternativos
- **API Channel** - Campañas a través de canales personalizados

### Audiencia y Segmentación

**Selección de contactos:**

- **Por contactos individuales** - Selecciona contactos específicos
- **Por etiquetas** - Incluye todos los contactos con ciertas etiquetas
- **Importación por CSV** - En campañas de WhatsApp y Channel API, sube un CSV con teléfonos (nombre y email opcionales): se crean los contactos nuevos, todos reciben una etiqueta y esa etiqueta se suma a la audiencia. Los contactos que ya existían (mismo teléfono, incluidas las variantes de Brasil, México y Argentina, o mismo email) conservan sus datos y etiquetas: solo se les suman las nuevas. Una columna opcional `etiquetas` (separadas por comas) agrega además etiquetas propias a cada contacto, creándolas si no existen, para segmentar después; la audiencia de la campaña sigue siendo la etiqueta del panel. Admite listas de hasta 50.000 filas, se procesa en segundo plano y muestra el progreso y un resumen de nuevos, existentes, repetidos y rechazados
- **Combinación** - Mezcla contactos directos y etiquetas
- **Deduplicación automática** - Evita duplicados por número de teléfono

**Filtrado inteligente:**

- Excluye contactos sin número de teléfono
- Deduplicación por teléfono (toma el primer contacto)
- Contador de audiencia pre-envío

### En la conversación

- **Etiqueta de campaña** - Cada mensaje enviado por una campaña muestra arriba de la burbuja un megáfono con el nombre de la campaña y la burbuja va en violeta, para distinguirla de los mensajes de agentes, bots y automatizaciones; los administradores lo tocan para abrir su reporte
- **Del reporte al mensaje** - En el reporte de la campaña, el nombre de cada contacto abre su conversación con el mensaje de la campaña resaltado

### Programación

- **Envío inmediato** - Ejecuta la campaña al momento
- **Envío programado** - Agenda para fecha y hora específica
- **Solo en horario laboral** - Pausa envíos fuera de horario y retoma automáticamente
- **Zona horaria del inbox** - Respeta la configuración de cada inbox

### Contenido de Campañas

**Mensajes de texto:**

- Mensaje personalizable con texto libre
- Soporte de emojis
- **Spintax** - Variaciones automáticas de texto usando sintaxis `{Hola|Buenos días} {amigo|compañero}` para mensajes únicos por destinatario

**Archivos adjuntos** *(Evolution/WAHA/Uazapi/API)*:

- Imágenes (JPEG, PNG, WebP)
- Videos (MP4, 3GP)
- Documentos (PDF, Office, etc.)
- Múltiples archivos por campaña

**Plantillas de WhatsApp** *(Cloud API/Notificame)*:

- Templates aprobados por Meta
- Parámetros dinámicos por contacto
- Componentes de header, body y buttons
- Multi-idioma

### Constructor de Plantillas Meta *(Mega)*

Crea y gestiona tus plantillas de WhatsApp directamente desde MEGA, sin necesidad de acceder al Meta Business Manager:

**Gestión de plantillas:**

- **Lista centralizada** - Ve todas las plantillas de todos tus inboxes de WhatsApp en un solo lugar
- **API unificada de plantillas cacheadas** - Las integraciones pueden listar plantillas cacheadas de inboxes WhatsApp nativos y Twilio, filtrarlas por el nombre exacto del proveedor y consultar el último intento de sincronización sin contactar al proveedor
- **Estado de aprobación** - Monitorea si cada plantilla está aprobada, pendiente o rechazada por Meta
- **Cambios de categoría de Meta** - Avisa cuando Meta recategoriza una plantilla (por ejemplo, de Utilidad a Marketing) o anuncia que lo hará en 24 horas, con acceso directo para solicitar la revisión
- **Métricas de uso** - Ve cuántas veces fue entregada cada plantilla y su tasa de lectura
- **Filtros avanzados** - Filtra por estado, categoría, idioma, canal y rango de fechas
- **Búsqueda** - Encuentra plantillas rápidamente por nombre o contenido
- **Eliminar plantillas** - Elimina plantillas individuales o en lote con confirmación
- **Activar o desactivar plantillas** - Oculta una plantilla de los agentes (respuesta, nueva conversación y mensajes programados) sin borrarla en Meta; las campañas y automatizaciones pueden seguir usándola. Útil para las plantillas de ejemplo de Meta o las pensadas solo para campañas
- **Sincronizar plantillas** - Botón de sincronización para traer plantillas nuevas desde Meta
- **Sincronización inicial automática** - Al crear el canal, se ejecuta una sincronización inicial de plantillas
- **Prevención de duplicados** - Validaciones de inserción para evitar duplicados durante sincronizaciones
- **Tabla responsive** - Mejor visualización de metadata de plantillas en desktop y móvil

**Constructor visual:**

- **Crear plantilla paso a paso** - Flujo guiado con pasos: Info Básica → Constructor
- **Header opcional** - Agrega encabezado de texto o multimedia (imagen, video, documento)
- **Cuerpo del mensaje** - Editor con soporte de negritas `*texto*`, cursivas `_texto_`, variables `{{1}}`, `{{2}}`
- **Barra de formato** - Botones de formato (negrita, cursiva) e inserción de variables con un clic
- **Footer opcional** - Texto de pie de mensaje (hasta 60 caracteres)
- **Botones de acción** - Visitar sitio web, llamar por teléfono, respuesta rápida o copiar código
- **Vista previa en tiempo real** - Ve cómo quedará la plantilla antes de enviarla
- **Valores de ejemplo** - Define ejemplos para las variables para facilitar la aprobación de Meta
- **Categorías** - Marketing, Utilidad, Autenticación
- **Multi-idioma** - Crea plantillas en cualquier idioma soportado por WhatsApp

**Edición de plantillas:**

- **Editar plantilla existente** - Modifica una plantilla ya creada
- **Nueva versión** - Al editar, el sistema crea una nueva versión y la envía a aprobación
- **Estado de versión** - Sigue el historial de aprobación de cada versión
- **Vista de detalle** - Consulta una plantilla completa antes de pasar a modo edición
- **Carga de media optimizada** - Ajustes en subida de archivos multimedia para edición/envío

### Multi-Inbox (Rotación de Líneas) *(Mega)*

Envía campañas desde múltiples líneas de WhatsApp para maximizar el alcance y evitar límites:

- **Distribución automática** - Los mensajes se reparten entre tus líneas
- **Rotación configurable** - Define cuántos mensajes enviar por cada línea antes de cambiar
- **Edición de la rotación** - En campañas de WhatsApp con Evolution, WAHA o Uazapi y del canal API, conserva las cajas seleccionadas, agrega o quita cajas y desactiva la rotación al guardar una campaña editable
- **Evita bloqueos** - Al distribuir la carga, reduces el riesgo de límites por línea
- **Mayor velocidad** - Envía más mensajes en menos tiempo usando varias líneas

### Control de Velocidad *(Mega)*

Envío inteligente que protege tus líneas de WhatsApp:

- **Pausas automáticas** - El sistema hace pausas entre mensajes para simular envío humano
- **Velocidad adaptable** - Configuración optimizada según el proveedor
- **Prevención de bloqueos** - Evita que WhatsApp detecte comportamiento de spam
- **Sin configuración manual** - Valores óptimos preconfigurados

### Estados de Campaña

| Estado | Descripción |
| -------- | ------------- |
| **Active** | Campaña lista para ejecutarse |
| **Running** | Campaña en ejecución |
| **Completed** | Campaña finalizada exitosamente |
| **Error** | Campaña con errores críticos |

### Métricas y Seguimiento

Monitorea el rendimiento de tus campañas en tiempo real:

- **Contador de audiencia** - Sabe a cuántos contactos llegará tu campaña
- **Mensajes enviados** - Seguimiento en tiempo real del progreso
- **Mensajes fallidos** - Identifica problemas de entrega
- **Reporte de errores** - Descarga detalle de envíos fallidos para corrección
- **Diagnóstico de entrega** *(Mega)* - Los reportes y CSV incluyen el código y motivo del proveedor; una intervención de inbox o plantilla pausa la campaña sin marcar como fallidos los contactos no intentados
- **Embudo de entrega** *(Mega)* - El reporte cuenta los contactos enviados, entregados, leídos y fallidos con sus tasas de envío, entrega y lectura, marca cada contacto como Enviado, Entregado, Leído o Fallido y filtra por paso; entregados y leídos salen de las confirmaciones del proveedor, así que una línea que nunca informa lecturas no muestra ninguna
- **Eliminar una campaña** - Borra la campaña y su informe de envíos; los mensajes que ya envió se quedan en sus conversaciones, sin la etiqueta de la campaña
- **Progreso en tiempo real** *(Mega)* - Barra de progreso en vivo que se actualiza automáticamente mientras la campaña se ejecuta
- **ETA estimada** *(Mega)* - Tiempo estimado de finalización visible durante la ejecución de la campaña

### Protección Anti-Spam

El sistema incluye múltiples protecciones para mantener la calidad de tus envíos:

- **Sin duplicados** - No envía dos veces al mismo contacto
- **Detección automática** - Omite contactos que ya recibieron la campaña
- **Historial de envíos** - Cada mensaje queda vinculado a su campaña

### Remitente y Conversaciones

- **Asigna un agente** - Las respuestas de la campaña llegan al agente seleccionado
- **Reutilización inteligente** - Si ya existe conversación con el contacto, se usa la misma
- **Cierre automático** - Opción de cerrar la conversación después del envío

### Canales Soportados

| Canal | Tipo | Templates | Adjuntos | Multi-inbox |
| ------- | ------ | ----------- | ---------- | ------------- |
| Website (Live Chat) | Ongoing | ❌ | ❌ | ❌ |
| WhatsApp Cloud | One-off | ✅ | ✅ (en template) | ✅ |
| WhatsApp Notificame | One-off | ✅ | ✅ (en template) | ✅ |
| WhatsApp Evolution | One-off | ❌ | ✅ | ✅ |
| WhatsApp WAHA | One-off | ❌ | ✅ | ✅ |
| WhatsApp Uazapi | One-off | ❌ | ✅ | ✅ |
| Twilio SMS | One-off | ❌ | ❌ | ❌ |
| SMS | One-off | ❌ | ❌ | ❌ |
| API Channel | One-off | ❌ | ✅ | ❌ |

### Gestión de Campañas

- **Crear y editar** - Interfaz intuitiva para configurar campañas
- **Pausar y reanudar** *(Mega)* - Pausa una campaña en ejecución y reanúdala en cualquier momento sin perder el progreso
- **Editar antes de enviar** *(Mega)* - Modifica el contenido, audiencia y configuración de campañas que aún no fueron enviadas o que están pausadas
- **Ver métricas** - Dashboard con estadísticas en tiempo real
- **Exportar reportes** - Descarga detalles de la campaña

---

## 📚 Centro de Ayuda (Help Center)

### Portales de Conocimiento

- **Slugs editables y sin duplicados** - Cambia la URL de un artículo desde sus propiedades con validación, sin artículos duplicados al crearlos y con un portal público más prolijo (idioma del logo, autores eliminados, tablas en vistas previas)
- **Múltiples portales** - Crea bases de conocimiento por producto/marca
- **Dominio personalizado** - Aloja en tu propio dominio
- **Diseño configurable** - Colores, logo, texto de cabecera
- **Integraciones analíticas** - Los administradores pueden conectar Google Analytics 4, Google Tag Manager, Microsoft Clarity, Hotjar, Plausible, Amplitude y Meta Pixel; los scripts se publican solo con un identificador válido
- **Layouts seleccionables** - Elige entre una portada clásica o una navegación tipo documentación con barra lateral
- **Multi-idioma** - Artículos en múltiples idiomas
- **Artículo original** - Cada traducción se vincula a su artículo original desde las propiedades del artículo; una familia tiene un solo artículo por idioma, y la traducción con IA no puede escribir sobre el idioma del original
- **Contenido recomendado por idioma** - Selecciona y ordena hasta 3 categorías y 6 artículos destacados para cada idioma; si no se configura, se muestran los contenidos populares predeterminados
- **Quitar un idioma con su contenido** - Al quitar un idioma se borran sus artículos y categorías, tras una confirmación que muestra cuántos son; el idioma por defecto no se puede quitar
- **Noruego** - El noruego aparece con su nombre entre los idiomas del centro de ayuda
- **Logo para modo oscuro** - Agrega un segundo logo que el centro de ayuda público muestra en modo oscuro
- **Gestionado por administradores** - El menú del Centro de ayuda se muestra a administradores y a roles que gestionan la base de conocimiento; los agentes siguen insertando artículos en sus respuestas
- **Embeds GuideJar** - Inserta guías interactivas de GuideJar dentro del contenido del Help Center

### Organización de Contenido

- **Categorías** - Agrupa artículos por tema
- **Subcarpetas** - Organización jerárquica
- **Artículos** - Contenido rico con markdown
- **Filtrar por autor** - La lista de artículos filtra por cualquier compañero (con búsqueda) en lugar de la pestaña "Mis artículos", y los conteos por estado siguen al autor elegido
- **Aviso de versión más reciente** - Si un compañero u otra pestaña cambia el artículo que estás editando, el editor ofrece *Cargar la última versión*
- **Crear desde categoría** - Inicia artículos nuevos directamente desde la vista de cada categoría
- **Redimensionado de imágenes** - Ajusta imágenes dentro del editor para mejorar la maquetación de artículos
- **Menú slash en editor** - Inserta bloques y comandos rápidamente escribiendo /
- **Menú slash seguro en tablas** - Dentro de las celdas, usa solo formatos inline que Markdown conserva, con navegación por flechas y Ctrl+N/P contenida en el menú
- **Videos desde el menú slash** - Inserta enlaces de video compatibles (YouTube, Vimeo, Loom, Wistia, Arcade, Bunny, CodePen, GuideJar y MP4) o sube un MP4 con progreso, cancelación, reintento y vista previa redimensionable en el editor y el artículo publicado
- **Cargas de medios confiables** - Las imágenes aparecen en el cursor mientras se cargan en segundo plano; las cargas fallidas se pueden reintentar o eliminar sin perder el borrador
- **Separadores desde el menú slash** - Inserta un separador horizontal desde el menú del editor para dividir secciones del artículo
- **Tablas nativas en editor** - Crea y edita tablas directamente en el editor de artículos
- **Tablas Markdown** - Renderizado correcto de tablas en artículos del portal
- **Posicionamiento** - Ordena artículos manualmente
- **Reordenamiento de categorías** - Arrastra y suelta para reordenar categorías en el portal; el orden se guarda automáticamente

### Estados de Artículos

- **Borrador** - En preparación
- **Publicado** - Visible para usuarios
- **Archivado** - Oculto pero conservado; el centro de ayuda público no lo muestra, ni siquiera desde su enlace directo
- **Borrador por idioma** - Cada traducción de un artículo puede estar en estado borrador independientemente; publica solo los idiomas listos sin afectar los demás
- **Ediciones sin publicar** - Los cambios de un artículo publicado quedan en borrador hasta revisarlos y publicarlos explícitamente; se pueden comparar con la versión visible o descartar

### SEO y Acceso

- **Meta descripciones** - Optimiza para buscadores
- **URLs amigables** - Slugs personalizables
- **Widget integrado** - Conecta portal con chat en vivo
- **Ocultar de los buscadores** - Desde Ajustes › SEO un centro de ayuda puede quedar fuera de Google y otros buscadores mientras sigue funcionando para los visitantes; cada artículo también se puede ocultar desde sus propiedades
- **Imágenes en tu dominio** - Las imágenes de los artículos y las fotos de los autores siguen el dominio actual del centro de ayuda, también con dominios propios

### Generación de Contenido con IA *(Enterprise)*

- **FAQs desde PDF** - Sube documentos PDF para generar borradores de preguntas frecuentes con IA
- **Contexto adicional** - Añade instrucciones opcionales para orientar la generación del contenido
- **Publicación asistida** - Revisa y publica solo las entradas generadas que quieras conservar

### Insertar Artículos en Conversaciones

- **Búsqueda de artículos** - Busca artículos desde la caja de respuesta
- **Vista previa** - Visualiza el artículo antes de insertar
- **Insertar como enlace** - Añade el link del artículo al mensaje
- **Resultados en popover** - Búsqueda de artículos restaurada y estable desde el panel de conversación
- **Copiar enlace** - Copia la URL del artículo al portapapeles
- **Acceso rápido** - Botón dedicado en el panel de respuesta

### Búsqueda por Embeddings *(Enterprise)*

- **Búsqueda semántica** - Encuentra artículos por significado, no solo palabras clave
- **IA contextual** - Sugiere artículos relevantes en conversaciones
- **Enlaces reales a los artículos** - Cuando Major lee un artículo publicado, recibe su enlace público del centro de ayuda, así comparte la URL correcta

---

## 📊 Reportes y Analíticas

### Reportes de Conversaciones

- **Volumen** - Nuevas, resueltas, pendientes
- **Tiempo de resolución** - Promedio y distribución
- **Primera respuesta** - Tiempo de respuesta inicial
- **Tendencias** - Evolución temporal
- **Drilldown de barras** - Abre cada barra del gráfico para revisar conversaciones o mensajes que componen la métrica, con navegación entre buckets y conteos del resultado; para el conteo de conversaciones, Ver todas abre una lista filtrada en una nueva pestaña

### Reportes de Agentes

- **Productividad individual** - Conversaciones manejadas
- **Tiempo de respuesta** - Por agente
- **Satisfacción** - CSAT por agente
- **Disponibilidad** - Tiempo online/offline

### Reportes de Inbox

- **Comparativa de canales** - Rendimiento por inbox
- **Distribución de carga** - Balance entre inboxes
- **Horarios pico** - Identifica momentos de mayor demanda

### Reportes de Equipos

- **Performance por equipo** - Métricas grupales
- **Distribución** - Carga de trabajo entre equipos

### Reportes de Etiquetas

- **Uso de etiquetas** - Frecuencia y tendencias
- **Categorización** - Análisis por clasificación

### Reportes de Bot

Monitorea el rendimiento de tu IA y bots:

- **Dashboard de métricas de bot** - Analíticas completas de bots
- **Resueltas por bot** - Conversaciones resueltas completamente por IA/bots
- **Respuestas del bot** - Cuenta solo los mensajes públicos enviados por bots (AgentBot, Captain y flujos de Flow Builder que actúan como bot); las respuestas de agentes y las notas privadas en conversaciones con bot ya no cuentan, por lo que los totales pueden ser menores que antes
- **Handoffs de bot** - Conversaciones transferidas a agentes humanos
- **Tasa de resolución** - Porcentaje de resoluciones automatizadas
- **Ahorro de tiempo** - Tiempo de agente ahorrado por automatización
- **Filtros** - Por rango de fechas, inbox, tipo de bot

### Reportes de Llamadas *(Enterprise)*

Analíticas completas del canal de voz:

- **Dashboard de llamadas** - Estadísticas completas de llamadas
- **Total de llamadas** - Resumen de todas las llamadas
- **Llamadas contestadas** - Llamadas conectadas exitosamente
- **Llamadas perdidas** - Llamadas entrantes no contestadas
- **Llamadas en progreso** - Llamadas actualmente activas
- **Entrantes/Salientes** - Desglose por dirección
- **Métricas de duración** - Tiempos totales y promedio
- **Métricas de cola** - Llamadas entrantes abandonadas (el contacto cortó antes de ser atendido), espera promedio hasta que un agente atiende, % atendidas dentro del SLA y llamadas resueltas en el flujo de llamada sin pedir un agente
- **SLA por bandeja** - Cada bandeja define en cuántos segundos una llamada cuenta como atendida a tiempo (20 por defecto)
- **Transferencias por agente** - Cuántas transferencias le llegaron a cada agente y cuántas tomó
- **Filtros** - Por fecha, inbox, agente, estado, dirección
- **Grabaciones en el reporte** - Las llamadas con grabación (WAHA, WhatsApp Cloud o Twilio) se reproducen en un reproductor compacto con barra de posición, velocidad (1x, 1.5x, 2x) y descarga; las llamadas sin grabación muestran "Sin grabación"
- **Ancho completo** - Los reportes de llamadas y de actividades usan todo el ancho de la pantalla

### Encuestas CSAT

- **Satisfacción del cliente** - Encuestas post-conversación
- **Ratings 1-5** - Escala de satisfacción
- **Comentarios** - Feedback cualitativo
- **Filtros** - Por agente, inbox, equipo, fecha
- **Notas de revisión** *(Enterprise)* - Añade notas internas a las respuestas CSAT para seguimiento de calidad
- **CSAT vía Plantillas WhatsApp** *(Mega)* - Envía encuestas CSAT usando plantillas oficiales de WhatsApp en lugar del mensaje clásico en chat; requiere aprobación de Meta; el sistema crea y gestiona automáticamente la plantilla con versionado; configurable por inbox con toggle entre modo clásico y modo plantilla
- **Visibilidad del feedback para agentes** *(Mega)* - Permite ocultar por inbox los comentarios escritos de CSAT a los agentes manteniendo visibles las calificaciones; los administradores conservan acceso completo y por defecto se mantiene la visibilidad actual

### Reportes Resumidos

- **Métricas consolidadas** - Vista general de las métricas clave en un solo lugar
- **Filtros por período** - Filtra por rango de fechas personalizado
- **Agrupación** - Agrupa datos por agente, equipo o inbox

### Exportación

- **CSV/Excel** - Descarga datos para análisis externo
- **Filtros personalizados** - Exporta exactamente lo que necesitas
- **Formato regional mejorado** - Exportación CSV con UTF-8 BOM y separador `;` para compatibilidad con hojas de cálculo locales

---

## 👨‍👩‍👧‍👦 Gestión de Equipos

### Agentes

- **Roles** - Administrador, Agente
- **Permisos granulares** - Control de acceso por funcionalidad
- **Perfil personalizado** - Avatar, nombre, firma
- **Avatar específico por cuenta** - Un usuario compartido mantiene un solo selector mientras cada cuenta guarda y muestra su propia foto de perfil
- **Sesiones de navegador nombradas** - Los agentes pueden etiquetar sesiones activas para reconocer equipos, perfiles de navegador o contextos de prueba
- **Control fiable de sesiones del navegador** - Las pestañas de un perfil comparten una sesión lógica; cerrar sesión la elimina, mientras otro navegador, perfil o ventana privada usa un espacio diferente. El login solo se interrumpe cuando un navegador nuevo alcanza el límite configurado
- **Estado de disponibilidad** - Online, Busy, Offline
- **Conversaciones, llamadas o ambas** - Desde el menú del perfil, cada agente elige por cuenta si recibe conversaciones, llamadas o ambas (al menos una queda activada). La asignación automática omite a los agentes con conversaciones apagadas y las llamadas de WhatsApp y Twilio no suenan para los agentes con llamadas apagadas; la asignación manual sigue funcionando. Los interruptores aparecen cuando una bandeja de la cuenta recibe llamadas; ambos vienen activados
- **Salida guiada de agentes** - Antes de eliminar un agente puedes dejar sus conversaciones sin asignar o reasignarlas en lote
- **Invitaciones protegidas** - Las invitaciones de nuevos agentes respetan el límite diario de correos de la cuenta, sin bloquear la incorporación de usuarios existentes
- **Ajustes en panel lateral** - Agentes, equipos (con sus miembros), etiquetas, macros, SLA, roles personalizados, políticas de asignación, webhooks, apps del panel e integraciones como Dialogflow se ven, crean y editan desde un mismo panel lateral, también en el teléfono

### Equipos

- **Departamentos** - Ventas, Soporte, Facturación, etc.
- **Asignación automática** - Round-robin dentro del equipo
- **Restricción de visibilidad** - Miembros ven solo sus conversaciones
- **Identificación visual** - Configura un emoji o icono con color por equipo para reconocerlo en listas y selectores de asignación

### Inboxes y Miembros

- **Acceso por inbox** - Asigna agentes a canales específicos
- **Ver conversaciones** - Cada inbox en Ajustes › Inboxes, y el encabezado de sus ajustes, tiene un enlace que abre sus conversaciones
- **Capacidad límite** - Máximo de conversaciones por agente
- **Políticas de asignación** - Configura reglas de distribución

### Políticas de Asignación

Configura distribución inteligente de conversaciones:

- **Round Robin** - Distribuye conversaciones equitativamente entre agentes
- **Distribución justa** - Límite configurable (por defecto 100) por ventana de tiempo
- **Ventana de distribución** - Período de tiempo personalizable (por defecto 3600 segundos)
- **Prioridad de conversación** - Primera creada o más tiempo esperando
- **Múltiples inboxes** - Aplica la misma política a múltiples canales
- **Activar/desactivar** - Alterna políticas según necesites

### Políticas de Capacidad de Agente *(Enterprise)*

Define límites de conversaciones por agente:

- **Límites de capacidad** - Máximo de conversaciones activas por agente
- **Límites por inbox** - Capacidad diferente por tipo de canal
- **Reglas de exclusión** - Reglas basadas en JSON para excluir ciertos casos
- **Distribución balanceada** - Selector inteligente para balance óptimo de carga
- **Ajuste en tiempo real** - Los cambios de capacidad toman efecto inmediatamente

### Roles Personalizados *(Enterprise)*

- **Permisos a medida** - Crea roles con permisos específicos
- **Gestión de conversaciones** - Todas, no asignadas, o solo participando
- **Acceso a funcionalidades** - Contactos, empresas, reportes, campañas, etc.
- **Permisos de CSAT** - Controla qué roles pueden ver y gestionar encuestas de satisfacción
- **Un rol por miembro** - Dar un rol personalizado a un administrador lo convierte en agente con ese rol, y hacer administrador a un miembro le quita el rol personalizado. La cuenta siempre conserva al menos un administrador

### Horarios de Trabajo

- **Disponibilidad por inbox** - Define horarios de atención
- **Zonas horarias** - Soporte multi-región
- **Mensajes fuera de horario** - Respuestas automáticas
- **Excepciones del mensaje fuera de horario** *(Mega)* - En Horario de atención, cada inbox puede dejar sin el mensaje de no disponible a los grupos de WhatsApp, a números o identificadores puntuales y a los contactos con ciertas etiquetas, con las mismas reglas que los robots
- **Pausa de almuerzo** - Configura intervalos de descanso dentro del horario laboral
- **Horarios por día** - Define horarios diferentes para cada día de la semana

### Web Push operativo

- **Entrega con la página cerrada** - Los recordatorios de Calendario, asignaciones en notas de Kanban, automatizaciones de etapa, vencimientos de checklist y Tareas pueden llegar a navegadores suscritos aunque el dashboard esté cerrado
- **Acceso directo** - Las acciones de la notificación abren el evento, elemento Kanban o Tarea exacta que originó el aviso
- **Control del canal** - Los agentes configuran estas categorías operativas solo para Push; los popups en primer plano siguen disponibles cuando MEGA está abierto

### Configuración de Notificaciones

Cada agente puede personalizar exactamente cuándo y cómo recibir alertas:

**Tipos de notificación:**

- Nueva conversación creada
- Conversación asignada a ti, incluso si está pendiente
- Nuevo mensaje en tus conversaciones
- Cuando te mencionan en una conversación
- Mensajes en conversaciones donde participas

**Canales de notificación:**

- **Email** - Recibe alertas en tu correo electrónico
- **Push** - Notificaciones instantáneas en navegador o app móvil
- **Personalización total** - Elige qué tipo de alerta recibir por cada canal

### Posponer Notificaciones

Pausa temporalmente las notificaciones de conversaciones específicas:

- **Opciones de posposición** - 1 hora, 3 horas, 1 día, 1 semana o tiempo personalizado
- **Reapertura automática** - La notificación se reactiva después del período
- **Acceso desde barra de comandos** - Pospón rápidamente con atajo de teclado
- **Por notificación** - Pospón notificaciones individuales sin afectar otras
- **Indicador visual** - Ve cuándo una notificación está pospuesta

---

## 🔌 Integraciones

### Webhooks

Conecta MEGA con cualquier sistema externo mediante notificaciones automáticas:

> **Disponibilidad:** La entrega saliente de Webhooks requiere acceso a API y Webhooks para la cuenta en planes alojados. Sigue disponible en instalaciones autogestionadas.

- **Eventos en tiempo real** - Recibe alertas instantáneas cuando algo sucede
- **Integración con tu CRM** - Sincroniza datos automáticamente
- **Automatizaciones externas** - Activa flujos en otras herramientas
- **Flexibilidad total** - Configura qué eventos te interesan
- **Normalización de suscripciones** - Validación consistente de eventos y aliases de suscripción
- **Payload enriquecido de adjuntos** - Incluye `content_type` y extensión de archivos en eventos webhook
- **Evento de actualización de Agent Bot** - Dispara webhook cuando se actualiza una conversación gestionada por bot
- **Evento `inbox_updated`** - Notifica cambios relevantes de la bandeja, incluyendo desconexiones del canal
- **Alias de suscripción** - Asigna nombres descriptivos a cada suscripción de webhook para facilitar la gestión
- **Secreto global de webhook** *(Enterprise)* - Configura una firma de seguridad a nivel de instalación para verificar la autenticidad de todos los eventos webhook; los payloads se firman con HMAC-SHA256 usando el secreto configurado

### Tareas *(Mega)*

Planifica y controla el trabajo interno desde vistas compartidas de calendario y lista:

- **Activación controlada** - Los superadministradores habilitan el feature de la cuenta y los administradores conectan Tareas desde Configuración -> Integraciones
- **Tipos personalizados** - Los administradores definen categorías reutilizables y colores semánticos para el trabajo del equipo
- **Retirar en lugar de borrar** - Un tipo puede desactivarse para que deje de ofrecerse en tareas nuevas mientras las existentes lo conservan; al intentar eliminar un tipo con tareas se ofrece esa opción, y eliminar un tipo o desactivar Tareas siempre pide confirmación
- **Paleta coherente** - Los tipos usan los mismos 22 colores visuales de Google Calendar y conservan el color elegido en el calendario, los detalles y los listados, sin que el estado lo reemplace
- **Permisos por alcance** - Los administradores controlan todas las tareas; un rol personalizado puede recibir gestión de tareas propias/asignadas, lectura global e informes como permisos independientes; los agentes estándar solo ven y gestionan las tareas que crearon o tienen asignadas
- **Vistas calendario y lista** - La cabecera de Mensajes programados: búsqueda, panel de filtros (hoja en teléfonos), cambio calendario/lista, actualizar y Nueva tarea (botón flotante en teléfonos). El mes usa el control ‹ mes › y la cuadrícula del módulo Calendario, con hasta tres tareas por día y su estado como icono (vencida, en curso, tachada si está cerrada); la lista es una agenda agrupada por día. En teléfonos el mes muestra puntos y las tareas del día elegido debajo. Ambas abren el mismo detalle
- **Filtros operativos** - Busca por título, filtra por responsable —incluido sin responsable—, tipo y hoy, semana o próximos 30 días; un único selector de estado comienza en Todas las tareas y permite pendientes, en curso, vencidas, completadas o canceladas; ordena la lista por inicio, vencimiento, título, prioridad, estado o responsable
- **Tareas de varios días** - Una tarea se muestra en cada día del calendario que intersecta su programación, incluso si comenzó antes del mes visible
- **Experiencia móvil** - En pantallas pequeñas, los filtros se reorganizan sin comprimir el calendario mensual; los formularios y detalles mantienen acciones visibles sin tapar el contenido
- **Lectura antes de editar** - Al abrir una tarea se muestra su detalle; concluir y cancelar están en el encabezado con resumen obligatorio, mientras editar y, solo para administradores, eliminar con confirmación quedan en el pie
- **Responsabilidad clara** - Asigna una tarea a un agente de la cuenta o déjala sin responsable
- **Historial resistente** - Si se elimina el contacto, la conversación, el ítem Kanban o el responsable, la tarea conserva sus nombres y contexto históricos, limpia referencias vivas y resincroniza su proyección de Google sin duplicar la cascada
- **Estados operativos** - Gestiona tareas pendientes, en curso, completadas o canceladas; las vencidas se detectan automáticamente al superar la fecha límite
- **Cierre documentado** - Completar o cancelar exige un resumen del resultado para conservar qué ocurrió y los próximos pasos
- **Aviso al responsable** - Al alcanzar la fecha límite, solo el agente responsable recibe un popup y una notificación para abrir la tarea y concluirla, cancelarla o editarla; puede marcar el aviso como visto o posponerlo para que reaparezca automáticamente, y las tareas sin responsable no generan avisos. El aviso se ve como una tarjeta de evento de Google Calendar: color y nombre del tipo, cuánto hace que venció, fecha, contacto con su conversación, prioridad alta o urgente y el inicio de la descripción, con un botón Posponer que pospone en un clic; con varios avisos muestra cuántos quedan. El aviso de eventos del Calendario usa el mismo diseño, con lugar y enlace de Google Meet
- **Tareas recurrentes** - Repite tareas por día, semana, mes o año, con intervalo, días semanales y finalización por fecha o hasta 100 repeticiones
- **Contexto conectado** - Vincula opcionalmente contacto y conversación, o crea un ítem en un funnel y etapa sin exigir un cliente
- **Creación desde conversaciones** - El ReplyBox muestra una acción junto al calendario cuando Tareas está habilitada y conectada; abre el formulario con contacto, conversación, responsable actual y cualquier ítem Kanban relacionado precargados
- **Seguimiento por contacto** - El ContactPanel incluye un acordeón propio de Tareas con el mismo formato del calendario, identifica cada conversación vinculada por su número visible estable y conserva visibles las pendientes, en curso y vencidas del contacto aunque se abra una conversación nueva
- **Kanban condicionado** - El vínculo y la creación de ítems Kanban solo aparecen cuando `kanban_board` está habilitado en la cuenta
- **Tareas dentro del ítem** - Cuando Tareas está habilitada y conectada, el detalle Kanban separa el historial técnico de una pestaña operativa para crear, consultar y abrir las tareas vinculadas al ítem
- **Trazabilidad en Kanban** - El historial del ítem registra cuándo una tarea vinculada se crea, actualiza, inicia, concluye, cancela, reabre, vincula, desvincula o elimina, incluyendo estado y responsable
- **Participantes y prioridad** - Define prioridad, responsable, participantes de la cuenta e invitados externos
- **Google Calendar opcional** - Sincroniza inicio, fin y asistentes en un único evento, mostrando cualquier fallo sin perder la tarea local
- **Informes de tareas** - Los administradores y roles personalizados con el permiso específico de informes consultan tareas por fecha, responsable, tipo y estado; el permiso general de informes no lo habilita
- **API para desarrolladores** - Usa los CRUD de Tareas y Tipos de tarea con alcance de cuenta desde Swagger/OpenAPI o la colección Postman generada, incluidos búsqueda, intersección de rango, ordenamiento, paginación opcional y campos de workflows vinculados

### Google Calendar *(Mega)*

- **Recordatorios personales** - El creador recibe un aviso dentro de MEGA y por push del navegador, puede posponerlo con intervalos predefinidos y volver a abrir el diálogo compartido. Los eventos nuevos agregan como invitados, sin duplicados, al creador y al contacto cuando nacen desde una conversación.

Conecta Google Calendar como integración de productividad a nivel de cuenta, no como inbox/canal:

- **OAuth por cuenta** - Los administradores conectan el calendario desde Configuración -> Integraciones -> Google Calendar
- **Acceso por rol personalizado** - Los administradores pueden otorgar a un agente asignado el permiso “Acceder al Calendario” para Calendario, ReplyBox y ContactPanel
- **Disponibilidad condicionada** - El espacio `/calendar`, el icono del compositor y los eventos del panel de conversación solo aparecen cuando la cuenta está conectada y tiene un calendario seleccionado; los controles de sincronización Kanban requieren la misma configuración de cuenta
- **Creación minimalista** - Usa un editor de dos columnas inspirado en Google Calendar con zonas seleccionables, invitados removibles, Google Meet y contexto con la marca de instalación visible al buscar conversaciones
- **Selección de calendario** - Importa por defecto todos los calendarios accesibles o limita la entrada a uno; MEGA conserva un destino saliente concreto y la configuración nueva inicia en sync bidireccional
- **Capa interna de eventos** - MEGA guarda eventos internos y rastrea IDs externos de Google por separado
- **Calendario operativo de MEGA** - Los agentes gestionan vistas de dia, semana, mes y lista desde `/calendar`; la vista mensual limita los eventos visibles por dia y ofrece `+N más` o menú contextual para abrir acciones sin ocultar eventos. Los eventos admiten color y el borrado permanente, restringido a administradores, también elimina el evento vinculado de Google
- **Formulario completo de evento** - Los eventos manuales soportan zona horaria, ubicacion, invitados, recordatorios, recurrencia simple, disponibilidad, visibilidad y Google Meet
- **Vinculos MEGA buscables** - Al crear o editar eventos, los agentes buscan y seleccionan contacto, conversacion e item Kanban sin escribir IDs internos
- **Controles por módulo** - Habilita sincronización para calendario interno, Kanban, conversaciones y recordatorios desde un solo lugar
- **Sync al guardar** - Cuando la sincronizacion saliente esta habilitada, MEGA crea o actualiza el evento en el calendario Google seleccionado conservando el estado interno
- **Polling automatico de Google** - Cada cinco minutos MEGA importa solo eventos modificados desde el ultimo poll exitoso de cada calendario; `/calendar` lee datos locales y conserva sync manual como respaldo
- **Estado de conexión** - Ve la identidad conectada, reconecta cuando haga falta y desconecta sin borrar eventos internos
- **Sincronización de eliminaciones** - Cuando Google informa que un evento sincronizado fue eliminado, MEGA borra automáticamente su entrada local vinculada; las tareas y los ítems Kanban relacionados se conservan
- **Puente con Kanban** - Ítems con fecha programada o deadline pueden crear eventos internos y sincronizarlos al calendario seleccionado
- **Agenda y envío desde conversaciones** - Los agentes usan desde el compositor el mismo formulario con capacidades Google, contacto y conversación precargados, y el botón “Crear y enviar” comparte el horario, ubicación, detalles y enlace Google Meet generado
- **Seguimiento en conversaciones** - El panel lista eventos vinculados con un punto pulsante verde (<50%), amarillo (50–90%) o rojo (≥90%) según el avance de Inicio a Fin, opaca los vencidos y reabre el editor compartido
- **Importación y backfill** - Los administradores pueden importar eventos desde Google y migrar IDs legacy de Kanban al modelo global de calendario

### Apps de Dashboard

Embebe aplicaciones personalizadas en la vista de conversación:

- **iFrames personalizados** - Embebe apps externas en conversaciones
- **Contexto de apps sincronizado** - Las apps embebidas reciben las definiciones de atributos personalizados y el tema claro/oscuro efectivo; el contexto se actualiza al cambiar estos datos o reabrir la pestaña, y las solicitudes de actualización se responden solo al iframe solicitante.
- **Contexto dinámico** - Pasa información de conversación y contacto a la app
- **Apps por usuario** - Las apps pueden configurarse por agente
- **Múltiples apps** - Añade varias apps al mismo inbox
- **Seguro** - Las apps corren en iframes aislados
- **Datos en tiempo real** - Las apps reciben actualizaciones de conversación en vivo
- **Gestión administrativa** - Las apps de toda la cuenta solo pueden crearse, editarse y eliminarse por administradores; los agentes autenticados conservan el acceso de lectura
- **Scripts de dashboard (Super Admin)** *(Mega)* - Publica personalizaciones globales en paneles sin tocar el código base. El listado muestra el orden de carga de cada script, los dominios externos desde los que carga código, su tamaño y un interruptor para activarlo, con búsqueda en vivo y filtro por estado; un único formulario crea y edita el script con números de línea, contador de longitud y una vista previa del panel real de una cuenta que inyecta el código sin guardar e informa errores. En móvil cada script es una tarjeta, con navegación compacta y editor adaptado al ancho de pantalla
- **Agent Bots (Super Admin)** *(Mega)* - Gestiona los bots de agente de toda la instalación. El listado muestra quién puede conectar cada bot (global o de una cuenta), su tipo, el dominio al que envía eventos y cuántas bandejas lo usan, con búsqueda en vivo por nombre, URL o cuenta y filtro por alcance; la ficha reúne sus detalles, las bandejas conectadas con su cuenta y estado, la URL del webhook, el secreto de firma y el token de API ocultos con copia, y la eliminación; el formulario elige la cuenta con un buscador (vacío = bot global). En móvil cada bot es una tarjeta
- **Apps de plataforma (Super Admin)** *(Mega)* - Gestiona las apps que usan la API de plataforma. El listado muestra a cuántas cuentas llega cada app y los usuarios y bots que creó, con búsqueda en vivo; la ficha lista las cuentas con búsqueda, filtro con/sin acceso y paginación para dar o revocar acceso una por una o dar acceso a todas, y reúne el token de API oculto con copia, los registros que gestiona y la eliminación; el formulario tiene un interruptor de acceso a todas las cuentas que nunca revoca accesos. Avisa que las cuentas creadas después no se agregan solas. En móvil cada app es una tarjeta
- **Banners de la plataforma (Super Admin)** *(Mega)* - El listado muestra cada banner con el color de su tipo, quién lo ve, cuándo y si está visible ahora, programado, finalizado o desactivado, con un interruptor por fila, búsqueda en vivo y filtro por estado; la ficha reúne el mensaje, el público y las fechas, las cuentas elegidas, la actividad (incluye cuántos agentes lo cerraron) y la misma vista previa que el formulario, con aviso si está programado o finalizado. En el formulario el tipo se elige por color y la vista previa sigue el tipo, el título, el mensaje y el estado mientras se edita, con el color del panel real. En móvil cada banner es una tarjeta
- **Anuncios de novedades** *(Mega)* - Super Admin anuncia una funcionalidad nueva con una imagen o un video y un texto corto: un enlace de YouTube, Vimeo, Loom, Arcade, Bunny, Guidejar o CodePen, el enlace de un archivo o un archivo subido desde el mismo formulario creando un banner de tipo Novedad, con las mismas cuentas, roles y fechas que los demás banners. Al entrar al panel los agentes lo ven como una ventana sobre el dashboard; con varios anuncios activos pasan de uno a otro con las miniaturas, los puntos, las flechas del teclado o deslizando en pantallas táctiles. Al cerrarlo deja de aparecer en todos sus dispositivos hasta que el anuncio se edite, y un anuncio nuevo o editado aparece en vivo sin recargar. En el formulario la imagen o el video solo se piden para este tipo y la vista previa muestra el panel con la imagen
- **Proveedores de WhatsApp (Super Admin)** *(Mega)* - Los servidores de Evolution API, WAHA y Uazapi se muestran en una grilla de tarjetas con su proveedor y slot, el uso de bandejas frente a la capacidad, el host de la API, de dónde salen las credenciales (guardadas, del entorno o faltantes), llamadas de voz y estado, con búsqueda en vivo y filtro por proveedor; la ficha muestra el uso, las bandejas que aloja con su cuenta, la conexión con las variables de entorno que lee el slot y si están definidas, la configuración y la eliminación (bloqueada para el slot legacy o si tiene bandejas). El formulario por secciones elige el proveedor con opciones y muestra en vivo qué variables de entorno lee el slot elegido. En móvil cada servidor es una tarjeta a todo el ancho
- **Diagnóstico de push (Super Admin)** *(Mega)* - Herramienta en tres pasos para revisar por qué un usuario no recibe notificaciones: se busca al usuario por nombre, email o #id (cada resultado indica cuántos dispositivos tiene), se eligen sus suscripciones, que muestran el navegador (Chrome, Firefox, Safari, Edge) o la app móvil, el final del endpoint o token y la última actualización, o se eliminan las suscripciones rotas. Al lado, el mensaje de prueba muestra una vista previa en vivo de la notificación con el ícono y el nombre de la instalación, contadores de largo para título y cuerpo, un texto por defecto en el idioma del Super Admin que se puede restaurar y un botón que indica a cuántos dispositivos se enviará. El push de prueba por navegador ahora incluye el cuerpo, no solo el título. Los resultados muestran por dispositivo si el servicio de push lo aceptó, falló o se omitió, con la respuesta cruda; los fallos se abren solos. En móvil cada dispositivo es una tarjeta
- **Páginas de configuración (Super Admin)** *(Mega)* - Cada página de Configuraciones (General, SAML SSO, Marca propia, Facturación, Captain, Email, Messenger, Instagram, TikTok, Google, Microsoft, Linear, Notion, Slack, WhatsApp embebido, Shopify, EvolutionAPI, QuepasaAPI, Mega Hub y Call ICE) muestra el ícono, el nombre y la descripción de la función, y agrupa sus valores en secciones con título y explicación (por ejemplo App, Webhooks y Opciones en los canales, o Imágenes, Identidad, Colores, Legal y Web en la marca). Cada valor muestra el nombre de su variable; los secretos van ocultos con opción de ver, las imágenes muestran su vista previa y se pueden subir, y los colores tienen selector. Se guarda desde la barra fija con un aviso traducido. En móvil las secciones quedan en una columna con la barra de guardar abajo
- **Proveedores de IA (Super Admin)** *(Mega)* - La lista muestra cada proveedor en una tarjeta con su tipo de conexión y host, si está activo, si es el predeterminado de Captain o de Mega Assistant, cuántos modelos tiene y el estado de cada capacidad (verificada, con fallas o sin probar), además de avisos de saldo o cuota del proveedor. La página del proveedor reúne la tabla de modelos con el resultado de cada capacidad, AI Actions, razonamiento y precios, las pruebas con falla y su mensaje, la conexión, dónde se usa (incluidas las cuentas que lo eligieron) y la eliminación; desde ahí se prueban los modelos. El formulario se divide en Conexión, Disponibilidad y Modelos: cada modelo es una fila con sus usos como opciones y su precio y razonamiento plegados debajo. En móvil las tarjetas y las tablas pasan a una columna
- **Funcionalidades de los planes (Super Admin)** *(Mega)* - Al crear o editar un plan, las funcionalidades se muestran igual que en la pestaña de funcionalidades de la cuenta: una tarjeta por categoría con cuántas incluye el plan, cada funcionalidad con su nombre, su interruptor y la etiqueta Premium, filtros Todas / Incluidas / No incluidas con sus totales y búsqueda. Las acciones Usar por defecto, Seleccionar todo y Limpiar selección siguen disponibles y en el celular ocupan el ancho de la pantalla.
- **Inicio de sesión de Super Admin** *(Mega)* - Un panel de marca en el color primario de la instalación acompaña al formulario: el logo, qué cubre la consola (cuentas y usuarios, planes y cobranza, salud de la instancia) y, al pie y en tono discreto, un mensaje de Mega elegido al azar, con el dominio y la versión. En el celular queda solo el formulario, con el mensaje sobre el selector de idioma y de tema. El login permite elegir idioma y tema antes de entrar, y el idioma elegido se mantiene al iniciar sesión. Muestra el logo de la instalación (`LOGO`, o `LOGO_DARK` en el panel y en tema oscuro). Un email o contraseña incorrectos se avisan en el idioma del usuario, conservando el email y con el cursor en la contraseña. El botón de mostrar contraseña cambia de ícono, el de entrar indica que está entrando y no envía dos veces, y al entrar se vuelve a la página que se había pedido o al Dashboard.
- **Modo claro y oscuro en Super Admin** *(Mega)* - El menú de la cuenta, en la barra lateral, tiene un selector de tema: Claro, Oscuro o Sistema (sigue al sistema operativo). La elección es la misma del panel de agentes, así que los dos cambian juntos, y se aplica en todas las páginas, el inicio de sesión (con el logo oscuro si está configurado), los diálogos, los gráficos y la vista previa de scripts, sin parpadeo al cargar.
- **Consola Super Admin rediseñada** *(Mega)* - Menú lateral agrupado por sección (se contrae a íconos) y, en celulares, menú desplegable con barra superior; formularios por secciones, listados que pasan a tarjetas en móvil, vista previa en vivo de los banners globales y precios de adicionales por moneda con un solo botón para completar desde USD. La lista de cuentas filtra por estado de facturación con pestañas que muestran su porcentaje y combina ese filtro con uno de estado u origen (activas, suspendidas, cortesía, pago manual, recientes…); se ordena por nombre, agentes o fecha de creación, filtra mientras se escribe, busca también por el email de los usuarios de la cuenta y en el celular muestra tarjetas con medidores de uso, modo de selección para acciones masivas y un panel inferior de filtros y orden. En la ficha de la cuenta, Suscripción y pagos se divide en subpestañas (suscripción, facturas, consumo de IA, movimientos de AI Actions e historial), las acciones de la suscripción van en una barra al pie de su tarjeta y en el celular las facturas, los usuarios y las funcionalidades se muestran en filas que entran en la pantalla. Suspender o reactivar la cuenta se hace desde el Resumen (tarjeta Estado de la cuenta) o el menú ⋯, con la categoría y el motivo que pide la suspensión, sin entrar a Editar
- **Vista previa y activación por script** *(Mega)* - Prueba cambios de forma segura y activa/desactiva scripts de manera independiente

### Platform Apps

Construye y conecta aplicaciones externas con acceso completo a la API:

- **Acceso completo a API** - Acceso programático completo a la plataforma
- **Permissibles** - Control granular sobre qué recursos puede acceder la app
- **Gestión de cuentas** - Crea y gestiona cuentas programáticamente
- **Gestión de usuarios** - Administra usuarios vía API
- **Integración de bots** - Conecta bots personalizados vía Platform Apps
- **Tokens seguros** - Tokens de API con permisos delimitados
- **Alcance respetado** - Una app de plataforma solo obtiene usuarios existentes que ya gestiona, y solo crea o mueve bots a cuentas a las que tiene acceso
- **Casos de uso** - Integraciones CRM, dashboards personalizados, sistemas de automatización

### Slack

Gestiona conversaciones de clientes directamente desde Slack, sin cambiar de herramienta:

- **Sincronización automática** - Las conversaciones aparecen en canales de Slack
- **Responde desde Slack** - Contesta a clientes sin abrir MEGA
- **Solo alertas** - Mantén los hilos de Slack para discusión interna sin enviar respuestas al cliente
- **Notas privadas** - Comunícate con tu equipo sin que el cliente vea
- **Vinculación de perfiles** - Conecta usuarios de Slack con agentes de MEGA
- **Canales privados** - Organiza por equipo o tipo de conversación
- **Alertas de reconexión** - Aviso si la integración necesita renovarse

### Dialogflow

- **Bot de NLU** - Conecta con agentes de Dialogflow
- **Intents y entidades** - Procesamiento de lenguaje natural

### OpenAI / GPT

Funcionalidades de IA avanzada con modelos GPT:

- **Asistente de escritura** - Mejora y corrige tus respuestas
- **Resumen de conversación** - Genera resúmenes automáticos
- **Traducción automática** - Traduce mensajes a cualquier idioma
- **Tono de respuesta** - Ajusta el tono (formal, amigable, etc.)
- **Expansión de texto** - Desarrolla ideas cortas en respuestas completas
- **Simplificación** - Simplifica textos complejos

### Dyte (Video Calls)

Videollamadas integradas directamente en la conversación:

- **Crear reunión** - Inicia una videollamada con un clic
- **Unirse a reunión** - Clientes pueden unirse desde el widget
- **Botón en reply box** - Acceso rápido desde la caja de respuesta
- **Mensajes de tipo video** - Las llamadas aparecen en el timeline

### Google Translate

Traducción automática de mensajes en conversaciones:

- **Traducción automática** - Traduce mensajes entrantes a tu idioma configurado
- **Detección de idioma** - Identifica automáticamente el idioma del mensaje
- **Traducción en contexto** - Los mensajes traducidos se muestran inline en la conversación
- **Soporte multi-idioma** - Compatible con todos los idiomas de Google Translate
- **Clave verificada** - La clave de cuenta de servicio de Google (`type: service_account`) se valida con Google al conectar la integración y cada vez que se cambia

### Traducción automática *(Enterprise)*

Habla con cada cliente en su idioma, sin importar qué idiomas hable tu equipo:

- **Lee en tu idioma** - Los mensajes del contacto y las respuestas de bots se muestran en el idioma del panel de cada agente, con *Ver original* para leer lo que escribió el cliente
- **Responde en el suyo** - Las respuestas de los agentes, los saludos, los mensajes fuera de horario y las encuestas CSAT salen en el idioma del cliente; el texto original del agente queda a un clic, también para el cliente en el widget web
- **Sigue al cliente** - El idioma se detecta en cada mensaje, así que un cliente que cambia de idioma recibe las respuestas en el nuevo. Un mensaje de una o dos palabras (el nombre de una ciudad, un error de tipeo) no cambia el idioma de la conversación
- **Captain o Google Translate** - Elige el servicio en Configuración → Flujo de conversación → Traducción; Captain es el servicio recomendado, porque lee toda la conversación y mantiene respuestas cortas como "ok" en el idioma correcto; Google Translate queda en *Usar otros proveedores* y lo factura Google en la cuenta de Google Cloud. Las cuentas con Google Translate conectado lo siguen usando hasta que elijan, con un botón *Cambiar a Captain*. Con Captain cada traducción usa AI Actions (detectar el idioma es gratis) y el modelo se elige en la configuración de Captain
- **Tal cual cuando hace falta** - Las notas privadas, plantillas de WhatsApp, Direct Send, mensajes interactivos, campañas y mensajes reenviados nunca se traducen; una respuesta que no se puede traducir se envía como se escribió y queda marcada para el agente. Si el servicio de traducción falla, la respuesta igual se envía
- **Apágala en una conversación** - Desde el menú de la conversación (*Desactivar traducción automática*) un agente la apaga solo en esa conversación: ni sus mensajes ni las respuestas se traducen hasta que se vuelva a activar desde el mismo menú. La conversación muestra quién la apagó o la volvió a activar
- **Desactivada por defecto** - Se habilita por cuenta (función *Auto Translate* en Super Admin) y la activa el administrador de la cuenta

### Linear *(Enterprise)*

- **Gestión de tickets** - Crea issues desde conversaciones
- **Sincronización** - Mantén estados actualizados
- **Desvinculación segura** - Desde una conversación solo se pueden desvincular los issues vinculados a esa misma conversación

### Shopify *(Enterprise)*

- **Datos del cliente** - Visualiza historial de compras
- **Pedidos recientes** - Contexto de e-commerce

### WooCommerce *(Enterprise/Mega)*

Integración completa con WooCommerce:

- **Conexión de tienda** - Vincula tu tienda WooCommerce
- **Historial de pedidos** - Ve pedidos del cliente en contexto
- **Búsqueda por email y teléfono** - Encuentra pedidos por email y por teléfono, aunque la tienda haya guardado el teléfono en formato local
- **Webhooks de WooCommerce** - Recibe eventos de la tienda
- **Panel de pedidos** - Vista de pedidos en la conversación

### Stripe en el panel del contacto

Vista de solo lectura de tu propia facturación de Stripe junto a cada conversación (independiente de la facturación de suscripciones de Mega):

- **Tu propia cuenta de Stripe** - Un administrador la conecta con una clave de API restringida, guardada cifrada
- **Cliente por correo** - Se busca el cliente de Stripe por el correo del contacto; si hay varios, el agente elige uno
- **Suscripciones** - Las últimas cinco, con estado, precio, cantidad, renovación, fin de prueba y cancelación programada
- **Facturas recientes** - Número, fecha, importe y estado de las últimas cinco facturas
- **Control de acceso** - Solo los agentes que ven la conversación ven sus datos de facturación; la clave la gestionan los administradores
- **Escritorio y teléfono** - Una sección del panel del contacto, y una página de la hoja del contacto en teléfonos

### Notion *(Enterprise)*

- **Documentación** - Conecta páginas de Notion
- **Base de conocimiento** - Acceso rápido a recursos

### CRM (LeadSquared)

- **Sincronización de leads** - Envía contactos a tu CRM
- **Historial unificado** - Vista 360 del cliente

### Plantillas de Email

Personaliza las comunicaciones por email con tu marca:

- **Plantillas personalizadas** - Crea plantillas de email con tu marca
- **Plantillas por cuenta** - Diferentes plantillas para cada cuenta
- **Variables Liquid** - Contenido dinámico con sustitución de variables
- **Plantillas de instalación** - Plantillas predeterminadas para toda la instalación
- **Tipos de plantilla** - Soporte para diferentes tipos de email (notificaciones, transcripciones, etc.)
- **Layouts de respuesta con marca** - Los administradores pueden configurar un HTML Liquid de respaldo por cuenta y una sobrescritura por bandeja de Email; debe incluir `{{ content_for_layout }}` y admite hasta 262.144 caracteres.

---

## 💎 Funcionalidades Enterprise

### SLA (Acuerdos de Nivel de Servicio)

- **Políticas configurables** - Define tiempos objetivo
- **Primera respuesta** - Tiempo máximo para responder; su reloj activo termina después de la primera respuesta del agente y los incumplimientos permanecen en los reportes SLA
- **Siguiente respuesta** - Tiempo entre respuestas
- **Resolución** - Tiempo total de atención
- **Incumplimientos congelados** - Al resolver una conversación, la duración del incumplimiento queda registrada y deja de aumentar
- **Horarios de negocio** - Deadlines calculados en backend respetando horas hábiles del inbox
- **Contactos bloqueados** - Conversaciones con contactos bloqueados quedan fuera de asignación, procesamiento, reportes e indicadores de SLA hasta desbloquearse
- **Alertas y notificaciones** - Aviso antes de incumplir
- **Reportes de SLA** - Cumplimiento y tendencias
- **Crear automatización** - Después de crear un SLA, un atajo abre una nueva regla de automatización que ya lo aplica (cuentas con automatizaciones)

### Logs de Auditoría

- **Registro completo** - Toda acción queda registrada
- **Quién, qué, cuándo** - Trazabilidad total
- **Cumplimiento** - Para requisitos regulatorios
- **Búsqueda rápida de eventos** - Filtra por tipo de evento y rango de días completos, busca por nombre o correo del usuario que realizó la acción y ordena por fecha; los filtros se pueden compartir mediante la URL
- **Evidencia de eliminaciones (Super Admin)** *(Mega)* - Un informe de solo lectura filtra por cuenta las auditorías retenidas de destrucción de bandejas, conversaciones, contactos y mensajes; las entradas de Message conservan el contenido original como evidencia, pero la API de logs omite ese contenido y el payload del mensaje en los listados. La cuenta se elige con un buscador; una búsqueda en vivo (nombre, email, teléfono, IP o ID) y un filtro por tipo de registro con conteos acotan la lista, que se agrupa por día y despliega cada auditoría para ver y copiar todo lo que retuvo; en móvil cada auditoría es una tarjeta

### SAML/SSO

Single Sign-On empresarial para autenticación centralizada:

**Proveedores soportados:**

- **Okta** - Integración completa con Okta
- **Azure AD** - Microsoft Entra ID
- **Google Workspace** - Google como proveedor de identidad
- **OneLogin** - Soporte completo
- **Auth0** - Integración disponible
- **SAML 2.0 genérico** - Cualquier proveedor compatible

**Funcionalidades:**

- **Provisionamiento automático** - Crea usuarios automáticamente en el primer login
- **Aislamiento por cuenta** - Un usuario que pertenece a varias cuentas puede usar SAML solo si todas confían en el mismo proveedor de identidad; si no, se rechazan la invitación y el ingreso por SAML
- **Mapeo de grupos** - Sincroniza grupos/equipos del IdP
- **Forzar SSO** - Exige SSO para todos los usuarios de la cuenta
- **Múltiples dominios** - Configura SSO para diferentes dominios de email
- **Logout único** - Single Logout (SLO) soportado
- **URL de metadatos del IdP** - Pega la URL de metadatos del proveedor de identidad en lugar de copiar a mano la URL SSO, el ID de entidad y el certificado. Mega los lee de la URL, toma el certificado nuevo cuando el actual está por vencer y el botón Actualizar metadatos los vuelve a leer cuando quieras. El formulario manual sigue disponible

**Seguridad:**

- **Autenticación centralizada** - Gestión de acceso unificada
- **Políticas de contraseña en IdP** - Usa las reglas de contraseña corporativas
- **MFA en IdP** - Multi-factor authentication del proveedor
- **Revocación instantánea** - Elimina acceso desactivando en el IdP

### Asignación Avanzada (V2)

- **Capacidad por agente** - Límites dinámicos
- **Balanceo inteligente** - Distribución óptima de carga
- **Reglas complejas** - Lógica de asignación personalizada

### Búsqueda Avanzada

- **Indexación completa** - Búsqueda en todos los mensajes
- **Resultados con transcripciones** - Encuentra audios transcritos en los resultados de mensajes y su conversación asociada
- **Filtros combinados** - Múltiples criterios simultáneos
- **Resultados instantáneos** - Performance optimizada

### Atributos Requeridos de Conversación

Obliga a los agentes a completar atributos específicos antes de resolver conversaciones:

- **Campos obligatorios** - Define qué atributos personalizados deben llenarse
- **Validación al resolver** - Bloquea la resolución hasta completar los campos requeridos
- **Macros seguras** - Las macros que resuelven solicitan los atributos requeridos; si se omiten, ejecutan las demás acciones pero mantienen la conversación abierta
- **Mejora la calidad de datos** - Asegura que toda conversación tenga la información necesaria

### Conferencias de Voz

Conferencias de llamadas de voz entre agentes y clientes:

- **Llamadas múltiples** - Conecta a varios participantes en una sola llamada
- **Gestión de conferencia** - Controles completos de la conferencia
- **Integrado en conversaciones** - Las conferencias se asocian a conversaciones existentes

### Custom Branding (Marca Personalizada)

Personaliza completamente la apariencia de tu plataforma:

- **Logo personalizado** - Tu logo en lugar del logotipo predeterminado de la plataforma
- **Logo modo oscuro** - Logo específico para dark mode
- **Logo thumbnail** - Imagen cuadrada de la aplicación para favicon, ícono PWA instalable y splash, con respaldo en el ícono de notificaciones
- **Ícono de notificaciones** - Imagen cuadrada independiente para alertas Push del sistema, badges y el indicador temporal de pestaña oculta; usa `/favicon-badge-16x16.png` por defecto y el logo thumbnail como respaldo
- **Nombre de marca** - Cambia el nombre mostrado en toda la plataforma
- **Nombre de instalación** - Nombre para la instancia específica
- **Color primario** - Define tu color corporativo principal
- **Fondo de ícono PWA** - Configura el color de fondo del ícono instalable sin recompilar la imagen
- **URL de marca** - Enlace de tu empresa
- **URL del widget** - Enlace en el widget de chat
- **Términos y privacidad** - URLs personalizadas para páginas legales
- **Meta descripción** - SEO personalizado para tu instalación

### Deshabilitar Branding

- **Widget sin marca** - Elimina la atribución de la plataforma del chat en vivo
- **Emails sin marca** - Correos salientes sin branding de la plataforma
- **Portales limpios** - Help Center sin referencias a la plataforma

### Roles Personalizados

Crea roles a la medida de tu organización con control granular de permisos:

**Controla el acceso a:**

- **Conversaciones** - Quién puede ver y gestionar qué conversaciones
- **Contactos** - Acceso a datos de clientes
- **Empresas** - Acceso al menú Empresas y a los registros de empresa
- **Reportes** - Quién ve las estadísticas
- **Campañas** - Permisos para crear y enviar campañas
- **Centro de Ayuda** - Gestión de artículos y portales
- **Datos sensibles** - Control sobre números de teléfono visibles

**Ejemplos de roles:**

- **Supervisor** - Ve reportes y métricas sin editar configuración
- **Agente Senior** - Puede tomar conversaciones no asignadas
- **Agente Básico** - Solo trabaja con sus conversaciones asignadas
- **Analista** - Acceso exclusivo a reportes y estadísticas
- **Community Manager** - Gestiona campañas y contenido del Help Center

---

## ⭐ Funcionalidades Exclusivas Mega

### 🧭 Onboarding Guiado

- **Configuración inicial dedicada** - Completa los datos de la cuenta mediante un flujo administrativo específico
- **Teléfono en el registro** *(Mega)* - El formulario de creación de cuenta pide un teléfono opcional (WhatsApp) para que el equipo contacte al cliente durante la activación; Super Admin lo muestra en la cabecera de la cuenta con un enlace directo a WhatsApp
- **Sitio web normalizado** - Guarda la dirección con protocolo para integraciones y automatizaciones posteriores
- **Conexión guiada de Instagram** - Retoma la configuración de la bandeja después de autorizar Instagram desde onboarding

### 📅 Mensajes Programados

Programa el envío automático de mensajes en tus conversaciones:

- **Programación flexible** - Elige fecha y hora exacta para enviar el mensaje
- **Recurrencia** - Programa mensajes recurrentes: diario, semanal, mensual o anual
- **Series que no se cortan** - Las series semanales salen los días elegidos en la zona horaria de la cuenta (Configuración → General). Si el siguiente envío no se puede crear, el mensaje enviado muestra el motivo en vez de cortar la serie en silencio; los adjuntos pasan a cada envío
- **Plantillas** - Usa plantillas de mensajes predefinidas para envíos programados
- **Adjuntos** - Incluye imágenes, documentos y archivos en mensajes programados
- **Estados de seguimiento** - Monitorea el estado: pendiente, enviado, fallido, cancelado
- **Cancelación** - Cancela mensajes programados antes de que se envíen
- **Recuperación y reenvío** - Reintenta o reprograma un mensaje fallido, y vuelve a programar una copia editable de uno ya enviado, conservando destinatario y adjuntos
- **Programación universal por API** - Programa un mensaje para un teléfono, email o identificador de proveedor y crea o reutiliza el contacto automáticamente
- **Múltiples por conversación** - Programa varios mensajes en la misma conversación
- **Historial** - Consulta el historial de mensajes programados y su estado
- **Calendario y lista** - Calendario mensual en la hora local, con la hora y el título de cada envío, y lista agrupada por día que muestra primero los próximos envíos y debajo los anteriores (o un rango a elección). Búsqueda y filtros por estado, bandeja y agente en las dos vistas, en escritorio y teléfono
- **Adjuntos al editar** - Al editar un mensaje pendiente se ven sus archivos, se pueden quitar y agregar otros (hasta 15)
- **Detalle con acciones** - El detalle muestra el error del proveedor y ofrece las acciones del estado: cancelar o editar un pendiente, reintentar o reprogramar un fallido, enviar de nuevo uno enviado
- **Desde la conversación y el Kanban** - El botón del panel del contacto y la pestaña del Kanban muestran los programados de esa conversación con las mismas acciones, y usan el mismo formulario que la página

### 🔒 Placeholder de Mensaje Eliminado

Configura por inbox si los agentes ven el texto original y los adjuntos junto al aviso de eliminación:

- **Retención para agentes** - Puede mostrar el texto original y los adjuntos debajo de "Este mensaje fue eliminado" dentro del dashboard
- **Configurable por inbox** - Cada canal puede tener su propia configuración
- **Protección del contacto** - La API pública y los eventos en tiempo real dirigidos al contacto entregan solo el aviso de eliminación, sin metadatos ni URLs de adjuntos

### Proveedores WhatsApp Alternativos

MEGA incluye múltiples proveedores de WhatsApp además de la API oficial de Meta, permitiendo flexibilidad en costos, funcionalidades y casos de uso.

**Gestión multi-servidor (Mega):**

- **Múltiples servidores por proveedor** - Configura más de un servidor por canal para continuidad operativa
- **Capacidad configurable** - Define límites por servidor para distribuir volumen de mensajes
- **Edición parcial de servidores legacy** - Ajusta configuraciones existentes sin recrear la conexión completa
- **Servidor asignado visible** - Visualiza qué servidor está vinculado a cada inbox desde la configuración

---

### 📱 WhatsApp Evolution

Conexion directa a WhatsApp sin necesidad de API oficial, ideal para empresas que buscan flexibilidad y ahorro de costos.

**Ventajas principales:**

- **Conexión por QR** - Vincula tu WhatsApp en segundos escaneando un código
- **Sin plantillas obligatorias** - Envía mensajes libremente sin aprobaciones
- **Sin ventana de 24 horas** - Inicia conversaciones cuando quieras
- **Sin costos por mensaje** - Evita las tarifas de la API oficial de Meta

**Todo tipo de contenido:**

- Textos, imágenes, videos, documentos
- Audio y notas de voz
- Stickers
- Soporte para grupos de WhatsApp

**Ideal para:**

- Empresas que buscan reducir costos
- Operaciones que necesitan flexibilidad en mensajes
- Equipos que ya usan WhatsApp personal o business app

- **Recepción de mensajes grupales** - Atiende grupos directamente desde MEGA
- **Identificación de participantes** - Ve quién envía cada mensaje

---

### 📱 WhatsApp WAHA

Solución robusta y de alta disponibilidad para operaciones exigentes que requieren máxima estabilidad.

**Ventajas principales:**

- **Alta disponibilidad** - Diseñado para producción con reconexión automática
- **Múltiples números** - Gestiona varias líneas en una instalación
- **Muy estable** - Ideal para operaciones 24/7

**Contenido multimedia completo:**

- Textos, imágenes, videos, documentos
- Audio y notas de voz
- Stickers y reacciones, incluido envío de reacciones con token de API
- Soporte completo de grupos

**Funciones avanzadas:**

- Estado de presencia (escribiendo, en línea)
- Confirmaciones de lectura
- Mensajes editados y eliminados
- Autorización con passkey durante la vinculación de WhatsApp mediante el flujo de extensión de navegador de WAHA, con estados de sesión dedicados, aviso preventivo si la extensión no está instalada y confirmación manual por código cuando WhatsApp lo solicita
- Sincronización global y por conversación bajo demanda de mensajes recientes, con protección de concurrencia por cuenta y procesamiento dedicado opcional para instalaciones de alto volumen
- Descarga diferida de multimedia de grupos WAHA (lazy media) opcional por bandeja: la multimedia entrante de grupos se guarda como adjunto pendiente con un placeholder genérico y solo se descarga cuando un agente la solicita desde la conversación; las conversaciones individuales conservan la descarga inmediata
- Proxy por sesión con servidor `host:puerto` y credenciales opcionales, que puede eliminarse para volver a conexión directa
- Apps de WAHA por sesión: interruptores para activar o desactivar Números de teléfono de Brasil, Argentina y México, y Llamadas de voz cuando están disponibles, que reflejan el estado actual de cada app
- Pantalla de configuración de sesión común a WAHA, Evolution y Uazapi: estado de conexión claro, vinculación por QR o código sin ventanas emergentes, interruptores que se guardan solos y confirmación antes de recrear o desconectar la sesión

**Ideal para:**

- Operaciones de alto volumen
- Empresas que necesitan máxima estabilidad
- Equipos con múltiples líneas de WhatsApp

---

### 📱 WhatsApp Uazapi

Solución económica y escalable para operaciones de alto volumen.

**Ventajas principales:**

- **Precio competitivo** - Ideal para alto volumen de mensajes
- **Conexión flexible** - Por QR o código de emparejamiento
- **Múltiples líneas** - Cada número con su propia configuración
- **Control de velocidad** - Evita bloqueos con envío controlado

**Contenido soportado:**

- Textos, imágenes, videos
- Audio y notas de voz
- Documentos
- Sincronización global y por conversación bajo demanda de mensajes recientes, con recuperación de multimedia histórica

**Configuración de filtros de chat:**

Define qué conversaciones deseas recibir en la plataforma:

- **Filtrar por tipo** - Recibe solo chats individuales, grupos, o ambos
- **Lista de exclusión** - Ignora números específicos
- **Lista de inclusión** - Recibe solo de números específicos
- **Configuración desde UI** - Gestiona filtros directamente desde la configuración del canal

**Proxy regional:**

- **Selección de ciudad brasileña** - Guarda una ciudad opcional de proxy administrado en la configuración del canal
- **Aplicación en conexiones nuevas** - La ubicación guardada se usa al generar QR, vincular con código y recrear sesiones
- **Proxy personalizado o sin proxy** - Alterna a una URL de proxy propia o quita por completo el proxy activo

**Ideal para:**

- Empresas con presupuesto ajustado
- Operaciones de alto volumen
- Equipos que necesitan múltiples líneas a bajo costo

---

### 📱 WhatsApp Notificame

Proveedor brasileño que combina la API oficial de WhatsApp Business con facilidad de uso.

**Ventajas principales:**

- **API oficial de Meta** - Toda la confiabilidad de la API oficial
- **Plantillas aprobadas** - Envía mensajes fuera de la ventana de 24h
- **Sincronización automática** - Tus plantillas aprobadas se importan automáticamente
- **Múltiples líneas** - Gestiona varios canales desde una cuenta
- **Respuestas desde el celular** - Lo que respondes desde el celular o WhatsApp Web aparece en la conversación como mensaje enviado

**Contenido soportado:**

- Textos y plantillas con parámetros personalizados
- Imágenes, videos y documentos
- Ubicaciones compartidas

**Ideal para:**

- Empresas en Brasil o Latinoamérica
- Operaciones que requieren plantillas oficiales
- Equipos que necesitan la confiabilidad de la API oficial

---

### 🎙️ Integración WaVoIP (Webphone) *(Evolution/WAHA/Uazapi)*

Realiza llamadas de voz por WhatsApp directamente desde la plataforma usando proveedores alternativos:

**¿Qué es WaVoIP?**

WaVoIP permite llamadas de voz a través de WhatsApp para proveedores que no usan la Cloud API oficial de Meta (Evolution, WAHA, Uazapi). Es un servicio de terceros que conecta las llamadas de voz a tu navegador.

**Características principales:**

- **Llamadas entrantes y salientes** - Soporte completo de voz sobre WhatsApp
- **Webphone intuitivo** - Widget flotante fácil de usar en tu navegador
- **Controles completos** - Silenciar, colgar, aceptar, rechazar llamadas
- **Duración en tiempo real** - Cronómetro visible durante la llamada
- **Indicador de calidad** - Monitorea la calidad de conexión en vivo
- **Sesión persistente del dispositivo** - Conserva autenticación y estado por bandeja para simplificar reconexiones
- **Grabación automática** - Grabación automática con opción de descarga
- **Almacenamiento de grabaciones** - Grabaciones guardadas y adjuntadas a conversaciones

**Cómo funciona:**

1. Configura tus credenciales de cuenta WaVoIP
2. Habilita la función WaVoIP en tu cuenta
3. El widget webphone aparece cuando llegan llamadas
4. Acepta/rechaza llamadas directamente desde el navegador
5. Realiza llamadas salientes desde el perfil del contacto

**Beneficios:**

- Llamadas de voz sin API oficial de WhatsApp Business
- Funciona con números personales de WhatsApp
- Sin cargos por llamada de Meta
- Historial completo de llamadas en la conversación

---

### 🔄 Migración de Inbox

Cuando necesites reorganizar tus canales:

- **Transfiere conversaciones** - Mueve chats entre canales sin perder historial
- **Conserva todo el contexto** - Mensajes, archivos y notas se mantienen
- **Operaciones masivas** - Migra múltiples conversaciones a la vez
- **Progreso a la vista** - Elige origen y destino con búsqueda, recibe el aviso de que la migración no se puede deshacer y sigue en vivo los contactos, conversaciones y mensajes migrados

### Historial de Conversación Unificado

Contexto completo de cada cliente sin importar por dónde te contactó:

- **Vista 360°** - Todo el historial del contacto en un lugar
- **Todos los canales** - WhatsApp, email, redes sociales, todo junto
- **Contexto inmediato** - Entiende al cliente antes de responder
- **Respuestas de WhatsApp** - Las respuestas citadas pueden referenciar mensajes de conversaciones anteriores cuando el historial está activo y conservan el contexto en coexistencia entre identificadores WAMID de teléfono y BSUID

### Controles de Privacidad

Configura qué pueden ver y acceder tus agentes:

- **Solo mis conversaciones** - Agentes ven únicamente sus chats asignados
- **Ocultar contactos** - Restringe acceso a la base de datos completa
- **Interfaz simplificada** - Oculta opciones que no necesitan usar
- **Control granular** - Configura permisos por cuenta

---

### 📝 Edición y Eliminación de Mensajes *(Evolution/WAHA/Uazapi)*

Edita y elimina mensajes de WhatsApp después de enviarlos:

**Editar Mensajes:**

- **Ventana de 15 minutos** - Edita mensajes enviados dentro de 15 minutos
- **Sincronización de actualizaciones** - Las ediciones entrantes se sincronizan automáticamente desde WhatsApp Cloud y Notificame sin duplicar el mensaje original
- **Contexto del remitente grupal** - Las ediciones entrantes de grupos conservan visibles el número y nombre del participante bajo el indicador de edición
- **Indicador de edición** - Los mensajes editados muestran la etiqueta "editado"
- **Todos los proveedores** - Funciona con Evolution, WAHA y Uazapi

**Eliminar Mensajes:**

- **Eliminar para todos** - Quita mensajes enviados
- **Confirmación** - Confirmación de seguridad antes de eliminar
- **Actualización de estado** - Los mensajes eliminados se muestran como eliminados en la conversación

---

### 🧩 Tablero Kanban Comercial *(Mega)*

Gestiona oportunidades comerciales en un pipeline visual conectado al historial omnicanal:

- **Embudos con etapas personalizables** - Crea múltiples embudos y define una etapa predeterminada por embudo
- **Vista tablero y vista lista** - Alterna entre pipeline visual y listado operativo según el flujo del equipo
- **Lista completa por carga progresiva** - La vista lista carga 30 oportunidades por página y permite traer las siguientes sin perder las ya mostradas
- **Búsqueda y filtros de la lista en todo el embudo** - En la vista lista, la búsqueda y los filtros (incluida la fecha) buscan en todas las tarjetas del embudo, no solo en las ya cargadas, y siguen cargando resultados de a 30
- **Filtros avanzados por inbox/canal/actividad** - Segmenta oportunidades por origen y movimiento reciente
- **Filtros por etiquetas** - Filtra por etiquetas de conversación en tablero y lista, con impacto en métricas por etapa
- **Columnas configurables por usuario** - Muestra u oculta columnas y conserva preferencias localmente
- **Ficha 360 del ítem** - Incluye checklist, notas, adjuntos, agentes asignados, ofertas y atributos personalizados
- **Campos globales por API** - Las integraciones pueden crear o actualizar atributos del embudo con un arreglo estructurado o un objeto indexado por nombre; el objeto usa únicamente los campos configurados en el embudo
- **Notas extensas legibles** - Abre el texto completo con formato y adjuntos en una vista desplazable, con edición directa cuando tengas permiso
- **Búsqueda en relaciones del ítem** - Encuentra conversaciones vinculadas con búsqueda remota al gestionar relaciones
- **Moneda predeterminada por cuenta** - La moneda base del tablero se define desde configuración de cuenta (`default_currency`)
- **Zona horaria de la cuenta** - Configuración → General elige la zona horaria de la cuenta (`settings.reporting_timezone`, UTC si queda vacía) que usan reportes, tareas, horarios de Flow Builder y mensajes programados recurrentes
- **Moneda consistente en todo Kanban** - Tarjetas, detalle, ofertas, actividades e historial respetan la prioridad oferta → ítem → cuenta → idioma; cada lado de un cambio histórico conserva su propia moneda
- **Totales por moneda en cada etapa** - El encabezado separa PYG, USD, EUR y cualquier otra moneda sin convertirlas ni sumarlas entre sí; el tooltip incluye todas las ofertas filtradas, aunque todavía no estén cargadas por paginación
- **Moneda por oferta custom (override)** - En ofertas manuales de tipo producto/servicio el usuario puede elegir moneda por oferta
- **Sin moneda en ítems sin ofertas** - Si un ítem no tiene ofertas, el valor se muestra como placeholder y no contamina totales monetarios
- **Descargas fieles de reportes Kanban** - Los CSV incluyen todas las tarjetas autorizadas que coinciden con los filtros activos de embudo, fecha, agente e inbox; preservan el texto libre de forma segura para hojas de cálculo y usan el idioma seleccionado, las etapas configuradas y la moneda de la tarjeta o cuenta
- **Etiquetas al crear y desde el ítem** - Selecciona etiquetas existentes al crear un ítem, o añádelas y quítalas directamente desde su tarjeta
- **Relaciones nativas con contacto y conversación** - Mantén el contexto comercial conectado con el chat real del cliente
- **Puente con Google Calendar** - Ítems con fecha programada o deadline pueden crear eventos de calendario de MEGA cuando la sincronización Kanban está habilitada a nivel de cuenta
- **Automatizaciones por etapa** - Dispara acciones al entrar o mover etapas, incluyendo mensajes rápidos y reglas operativas
- **Seguimientos por falta de respuesta** - Después de la espera configurada, envía texto o multimedia subida a la conversación principal del ítem solamente si el contacto no respondió. El editor autocompleta variables del ReplyBox para datos del contacto, conversación, inbox, agente y atributos personalizados. En inboxes configurados de WhatsApp Cloud también permite templates aprobados y mantiene bloqueados los mensajes libres fuera de la ventana de 24 horas
- **Entrada sin grupos** - Cada etapa de entrada puede excluir conversaciones de grupos de WhatsApp para que no se creen ítems ni se inicien sus flujos automáticos
- **Entrega automática de plantillas** - Las plantillas automáticas de una etapa se envían una sola vez por ítem de forma predeterminada, evitando mensajes duplicados al volver a entrar en una etapa. El editor sugiere variables como `{{contact.name}}` al escribir `{{` y las completa al enviar; cada plantilla puede habilitar explícitamente el reenvío en cada reingreso; los mensajes rápidos manuales no tienen esta restricción
- **Mensaje rápido desde la tarjeta** - Con el interruptor *Mensaje rápido* del embudo activo, el menú de la tarjeta (⋯), el panel de la tarjeta y la pantalla de detalle en el teléfono ofrecen *Mensaje rápido*: envía una de las plantillas de la etapa que aplican a la tarjeta, o un mensaje personalizado, a su conversación vinculada sin abrirla
- **Alertas Kanban** - Notifica a miembros de equipos seleccionados y agentes asignados desde automatizaciones de etapa, y al agente responsable cuando una tarea de checklist llega a su fecha límite; las alertas descartadas reaparecen después del intervalo configurado en el funnel solo mientras esa tarea siga pendiente. Agrupa alertas en un banner no bloqueante y no envía email
- **Consultas optimizadas** - Los contadores del selector de funnels usan consultas ligeras; las estadísticas conservan los totales por moneda y oferta, y búsquedas e informes reutilizan datos relacionados para reducir consultas repetidas.
- **Vencimientos al crear o duplicar** - Las tareas de checklist con fecha límite y responsable programan su aviso al guardarse, también al copiarse a otro card; las copias notifican desde el card de destino.
- **Sincronización en tiempo real** - Cambios de etapa y datos del ítem se reflejan al instante en lista de chats y panel del contacto
- **Negocios abiertos del contacto** - Cada embudo puede habilitar desde Configuración Avanzada la visualización de sus ítems Kanban abiertos en todas las conversaciones del contacto actual; la opción está desactivada por defecto, conserva las reglas de visibilidad e identifica las conversaciones relacionadas
- **Paneles autorizados** - El bloque Kanban del panel de conversación y la entrada del sidebar se ocultan cuando el usuario no tiene ítems visibles ni funnels disponibles para agregar negocios
- **Detalle Kanban desde conversación** - Los iconos de canal de una tarjeta muestran cada tipo de inbox vinculado: abren directamente su única conversación o un selector limitado a ese canal si tiene varias, sin recargar el tablero; en móvil, el detalle muestra primero la información comercial y abre el perfil del ítem desde un panel lateral. El panel de contacto del drawer oculta las conversaciones anteriores para mantener el contexto del ítem
- **Mensajes no leídos en la tarjeta** - Cada botón de canal muestra cuántos mensajes entrantes sin leer tienen sus conversaciones vinculadas, con el mismo criterio de la lista de conversaciones y solo para las conversaciones que el usuario puede ver. Si varias conversaciones comparten canal (por ejemplo dos inboxes de WhatsApp), el botón suma sus contadores y el selector muestra el de cada una, primero las no leídas. Los botones quedan alineados con el menú de acciones y siguen visibles con la tarjeta comprimida. El contador sube en tiempo real con cada mensaje entrante y vuelve a cero al abrir la conversación desde el tablero. Cada embudo puede desactivarlo en Configuración Avanzada → Card
- **Acceso Kanban en tiempo real** - Al agregar o remover agentes del funnel, el sidebar, la lista de funnels y los ítems visibles se actualizan sin recargar
- **Múltiples conversaciones vinculadas** - Un mismo ítem Kanban puede relacionarse con varias conversaciones; la primera queda como vínculo principal y las adicionales se muestran en la pestaña de relaciones, con selector limitado a los inboxes del funnel e íconos de canal
- **Historial de vínculos por conversación** - Cada conversación vinculada o desvinculada genera su propio evento; el vínculo muestra la bandeja de la misma cuenta y el texto de la acción respeta el idioma de la interfaz
- **Una oportunidad abierta por contacto y funnel** - La creación automática reutiliza el ítem abierto del contacto y vincula allí sus nuevas conversaciones de Instagram, WhatsApp u otros inboxes habilitados; cada funnel se evalúa por separado y una oportunidad ganada o perdida permite iniciar otra
- **Histórico sin relación rota** - Si se elimina una conversación vinculada, el ítem Kanban se conserva como histórico y se limpia el vínculo
- **Acceso por rol y permiso Kanban** - Los administradores administran todos los embudos e ítems; agentes y roles con `kanban_view` trabajan los ítems autorizados; `kanban_manage` además crea y edita los embudos asignados, sin eliminar, definir el predeterminado ni cambiar la visibilidad
- **Autoasignación administrativa** - El administrador puede asignarse y removerse de cualquier ítem aunque no figure entre los agentes o inboxes del embudo; los demás usuarios conservan las reglas normales de elegibilidad
- **Visibilidad controlada de ítems** - El creador siempre puede ver su ítem; con una conversación vinculada válida el responsable solo lo ve si también está seleccionado en el funnel, y los agentes asignados manualmente al ítem lo ven; un vínculo stale queda solo para administrador y creador. El modo del embudo `everyone` permite a todos sus agentes ver todos los ítems, mientras `assigned_only` restringe la vista a los agentes autorizados.
- **Agentes flexibles por embudo** - Cualquier miembro de la cuenta con acceso Kanban puede agregarse al embudo, con o sin inboxes seleccionados; un rol personalizado requiere `kanban_view` o `kanban_manage`. Con inboxes configurados, las asignaciones manuales de ítems requieren acceso a por lo menos uno. Al mover un ítem, sus responsables se agregan automáticamente al embudo destino sin cambiar sus permisos de inbox
- **Configuración y automatizaciones protegidas** - La configuración global es de solo lectura para los actores Kanban; sus cambios y las automatizaciones globales son exclusivos de administradores. `kanban_manage` administra únicamente los funnels que tiene asignados

---

### 📊 Resumen del Año (Year in Review)

Estadísticas e insights anuales para tu cuenta:

- **Resumen anual** - Vista completa del rendimiento de tu año
- **Métricas clave** - Conversaciones, mensajes, tiempos de resolución
- **Día más ocupado** - Identifica tu día de mayor actividad
- **Tipo de personalidad** - Categorización divertida basada en tus patrones de trabajo
- **Slides interactivos** - Presentación atractiva de tus estadísticas
- **Resultados en caché** - Carga rápida para vistas repetidas
- **Compartir** - Comparte tus logros con tu equipo

---

### 💳 Suscripciones nativas (planes, adicionales y AI Actions)

El operador define y vende sus propios planes desde Super Admin, sin depender de un catálogo fijo. Funciona igual en la nube y en instalaciones auto-hospedadas.

**Planes a tu medida**

- Cada plan define agentes e inboxes incluidos, features habilitadas, AI Actions mensuales y documentos de Captain.
- Precios mensuales, semestrales y anuales por moneda (USD, BRL, EUR), cargados por el operador; "Sugerir desde USD" ayuda a completarlos con el tipo de cambio del día.
- Prueba gratuita configurable por plan (15 días por defecto), sin pedir tarjeta y con avisos 7, 3 y 1 día antes de vencer.
- **Duplicar plan** - Desde el menú de un plan, "Duplicar" crea una copia independiente con sus límites, precios, pasarelas, funcionalidades, adicionales y modelos de IA, para armar variaciones sin cargar todo de nuevo. La copia se crea inactiva, con el nombre "(copia)", "(copia 2)"…, y se abre para editarla antes de activarla.
- Tras el registro, el administrador ve una pantalla de activación con la cuenta, un progreso de 3 pasos y cierre de sesión, un selector mensual/semestral/anual (solo con los intervalos que tienen precio), tarjetas de planes y una tabla comparativa por grupos (equipo, canales, IA, productividad, plataforma). El plan predeterminado va primero y destacado, con sus métodos de pago y 4 beneficios resumidos. Cada plan público con días de prueba ofrece la suya: su tarjeta muestra los días gratis y su fecha de fin, el botón para empezar la prueba antes de "Pagar ahora" y las condiciones debajo de los botones. Al vencer sin pago, la cuenta se suspende. Sin plan predeterminado se muestra el catálogo público; si ningún plan tiene días de prueba, se exige pagar para activar la cuenta. El idioma usado durante el registro se conserva en Facturación.

**Cobros con Stripe y Asaas**

- Métodos de pago configurables en Super Admin: Stripe (internacional) y Asaas (Brasil, con nota fiscal emitida por Asaas). Las suscripciones de Asaas se pueden pagar con tarjeta, PIX o boleto: Super Admin elige cuáles ofrece la pasarela, el cliente elige al suscribirse y puede cambiar después, y con PIX o boleto paga cada cobro, adicionales y upgrades incluidos, en la página de su factura.
- **Método de pago personalizado** - Cualquier proveedor con API HTTP se conecta desde Super Admin sin esperar una integración nativa: se completa cómo autenticar (clave API u OAuth con botón Conectar), la petición que crea el cobro con variables como `{{amount}}` o `{{customer.tax_id}}`, dónde vienen el id y el link de pago, y la URL de webhook que Mega entrega para pegar en el proveedor. Para proveedores sin webhook, Mega consulta el estado cada 10 minutos. Cada cobro (suscripción, renovación, prorrateo, adicionales, AI Actions, cobros de servicios) es un link de pago; el botón Probar envía un cobro real y muestra la respuesta para configurar los campos.
- Cada moneda apunta a una pasarela; el país elegido en el registro define la moneda de la cuenta (Brasil en BRL, zona euro en EUR y el resto en la moneda por defecto, USD), siempre que una pasarela la cobre y haya planes con precio en ella; sin conversiones al cobrar.
- Mejorar de plan se cobra al instante con el prorrateo; bajar de plan se aplica al final del período y nunca borra agentes ni inboxes.
- **Planes exclusivos por cuenta** - Super Admin reserva un plan para una o más cuentas, por ejemplo con un precio negociado: solo esas cuentas lo ven en Facturación y lo contratan por la pasarela, con adicionales y cambios de plan. Las demás cuentas no lo ven ni pueden contratarlo llamando a la API.

**Adicionales y paquetes de AI Actions**

- Los adicionales recurrentes se cobran a su precio completo al contratarlos, sin importar lo que quede del período, y desde la próxima renovación se suman al plan en la misma factura.
- Al quitar un adicional sigue activo hasta el fin del período pagado, sin reembolso; la pantalla de billing muestra "Se da de baja el <fecha>" con un botón **Mantener** que cancela la baja hasta entonces. Se rechaza una baja que deje en uso más agentes, bandejas, llamadas o bandejas WAHA de las que quedan. Un adicional que la cuenta tiene sigue listado aunque ya no se venda, así siempre se puede quitar. Super Admin ve las bajas programadas en la pestaña de facturación de la cuenta y puede dar de baja o mantener un adicional desde ahí.
- Tampoco se puede quitar un adicional del que depende otro que sigue contratado (WAHA mientras quedan llamadas WAHA): hay que quitar primero el dependiente o los dos juntos. Si la cuenta cambia a un plan que ya incluye la funcionalidad de un adicional, ese adicional se da de baja solo al fin del período y no se vuelve a cobrar.
- Los adicionales por unidades muestran cuántas están en uso ("En uso: 1 de 2") en la pantalla de billing y en la ficha de la cuenta en Super Admin.
- Catálogo único de adicionales que cada plan puede ofrecer con un máximo opcional, con cuatro tipos: agente extra, inbox extra, **funcionalidad** (activa la funcionalidad elegida al crearlo, se cobra con la suscripción como los agentes adicionales y no se ofrece en planes que ya la incluyen) y **personalizado** (texto libre para cualquier servicio que venda el operador, cobrado mensualmente con la suscripción o como pago único).
- Un adicional de funcionalidad también puede venderse por unidades: **por bandeja** (llamadas WAHA: cada unidad activa las llamadas en una bandeja; en las demás aparecen bloqueadas con "Comprar otra unidad") o **con bandeja incluida** (WhatsApp WAHA, Evolution o Uazapi: cada unidad suma una bandeja que solo puede usar ese proveedor, aparte del límite del plan, y activa el proveedor). Un adicional puede requerir otra funcionalidad (las llamadas solo se ofrecen a cuentas con WAHA), y las unidades en uso no se pueden quitar hasta liberar las bandejas. Los planes, el límite normal de bandejas y las excepciones de Super Admin siguen funcionando igual.
- Cuando la cuenta no tiene más bandejas, la pantalla de nueva bandeja muestra los canales bloqueados ("Sin bandejas disponibles") con un aviso para comprar una bandeja adicional; WhatsApp sigue abierto solo para los proveedores cuyo adicional todavía tiene una bandeja libre.
- Los adicionales personalizados de pago único se compran desde la pantalla de billing eligiendo la cantidad; una vez pagados aparecen en Super Admin en "Entregas pendientes" y en el panel de atención del dashboard de facturación hasta que el operador los marca como entregados.
- Paquetes de AI Actions de pago único que se suman al saldo del mes, se acumulan y vencen a los 90 días.
- **Un precio por modelo** - Cada modelo de IA tiene un solo precio en AI Actions, el que carga el operador en AI Providers (o el predeterminado del modelo). Es el que la cuenta ve al elegir modelo en Captain, el que muestra el formulario del plan y el que se descuenta: cada función cobra con el modelo que realmente usó.
- **Las tareas grandes cobran lo que hacen** - Los flujos de trabajo del Copilot cobran cada paso, cada conversación revisada y cada decisión del filtro previo; las revisiones de conversaciones de Mega Assistant, cada conversación revisada; la transcripción de llamadas, cada pasada del modelo; los audios, por minuto empezado; la voz, por bloques de 5 minutos.
- **Saldo negativo visible** - Lo que ya empezó termina aunque se acabe el saldo; si cuesta más de lo que quedaba, el saldo queda en negativo, se ve en la pantalla de billing y en Super Admin, y se descuenta primero del próximo plan, paquete o ajuste. Con el saldo en cero o negativo no empieza trabajo de IA nuevo, tampoco el que no cobra por sí mismo (sugerencias del clasificador, voz generada, FAQs, notas de contacto, dictado).
- Los adicionales no suman AI Actions: las AI Actions vienen del plan, de los paquetes y de los ajustes de Super Admin.
- En una instalación propia, las cuentas sin un plan nativo no descuentan AI Actions y no ven créditos al elegir modelo.
- Medidor de consumo por origen (plan, paquetes y ajustes) en la pantalla de billing.
- El historial de pagos aparece antes del catálogo y muestra las cuatro facturas más recientes por página, con filtros combinables por estado y concepto.

**Administración**

- Asignación manual de planes: cortesía, pago manual y prueba, individual o masiva con vista previa del impacto por cuenta.
- Cuentas existentes quedan en modo Legacy: conservan features y límites actuales hasta que se les asigne un plan.
- Pago vencido: 7 días de gracia con aviso permanente para administradores y, al vencer, suspensión con reactivación automática al pagar.
- **Cobros de servicios** - Desde la ficha de la cuenta (o la Platform API), Super Admin crea un cobro único por el monto que necesite, por ejemplo consultoría, implantación o migración de datos, con descripción, vencimiento opcional y nota interna. Los administradores de la cuenta reciben un email, ven un banner en toda la app y lo pagan desde el banner de Facturación o el historial de pagos con la pasarela de su moneda (Stripe, Asaas con tarjeta, PIX o boleto, dLocal Go o PayPal). Si no se paga, pasa a vencido sin suspender la cuenta; mientras no se pague, se puede anular. La página de Facturación y los banners se actualizan en tiempo real cuando se crea, paga o anula un cobro o cambia la suscripción.
- **Consumo de IA** - Super Admin muestra las AI Actions cobradas, llamadas, tokens y costo del proveedor por período, proveedor, cuenta, modelo y función; también incluye proyección mensual y costo por acción.
- **Resultado de IA** - El dashboard de consumo, el de facturación y la ficha de cada cuenta muestran el mismo estado de resultados en USD: lo cobrado por paquetes, lo estimado de los planes, las cortesías aparte (sin sumar al ingreso), el uso que no descontó AI Actions y el resultado final. Incluye la rentabilidad de cada paquete con su precio mínimo, las AI Actions sugeridas por modelo según su costo real (también junto a cada modelo en AI Providers) y Mega Assistant desglosado por característica (Captain, reportes, contactos, conversaciones, etc.). Los dashboards de consumo de IA (Resumen, Rentabilidad, Cuentas y Desglose) y de facturación (Resumen, Planes e IA) se organizan en pestañas. Facturación explica qué cifras son actuales y cuáles mensuales, distingue las suscripciones de pago del total de la instalación y muestra acciones junto a créditos usados. Su pestaña IA solo ofrece el selector de mes porque sus resultados abarcan toda la instalación en USD. La lista de cuentas tiene buscador y paginación. En la ficha de cada cuenta, cada factura dice qué cobró (plan e intervalo, add-ons y cantidades, paquete de AI Actions o a qué plan cambió un prorrateo), con filtros por concepto y estado, y los movimientos de AI Actions tienen buscador, filtros por tipo, bolsa, función y fechas, y paginación. El resumen de consumo de IA presenta primero resultado, ingreso y costo total del LLM, y después distingue acciones cobradas, créditos usados y cortesías. Sus pestañas explican qué cifras siguen el período seleccionado y cuáles usan precios actuales o los últimos 30 días.
- **Ingresos** - Super Admin muestra el MRR por moneda (los precios semestrales y anuales se reparten en 6 y 12 meses), lo cobrado y lo pendiente de cobro, la tendencia de cobros de 12 meses por suscripciones, adicionales, AI Actions y servicios, MRR por plan, suscripciones por estado, cobros por pasarela y tipo de factura, altas y bajas del período y las facturas vencidas más antiguas.

---

## 🔐 Seguridad y Cumplimiento

- **Auditoría más completa** - Los inicios y cierres de sesión muestran la ubicación por IP y el historial de suspensiones indica quién suspendió cada cuenta
- **Contenido HTML seguro** - Los mensajes Markdown, instrucciones de Captain y enlaces de términos del registro filtran contenido peligroso; se conservan los enlaces internos de herramientas y las incrustaciones confiables de artículos.
- **Aviso de suplantación** - Cuando un Super Admin entra como otro usuario, el panel lo indica con un banner y permite salir con un clic
- **Conexión de canales solo para administradores** - Solo los administradores de la cuenta pueden conectar o reconectar páginas de Facebook y números de WhatsApp (registro integrado, WAHA y Evolution)
- **Nombres siempre como texto** - Los nombres de contactos (también al fusionarlos), respuestas predefinidas y macros, y el contenido de las notificaciones se muestran como texto y nunca se interpretan como HTML

### Autenticación

- **2FA/MFA** - Autenticación de dos factores
- **2FA en Super Admin** - Los super administradores que tienen activada la autenticación de dos factores ingresan el código de su app después de la contraseña. El paso del código vence a los 5 minutos y se cancela tras 5 códigos incorrectos. La consola no ofrece páginas propias de recuperación de contraseña, registro ni confirmación.
- **Enlaces de restablecimiento con vencimiento** - Los enlaces para restablecer la contraseña vencen a las 6 horas; los de una invitación, a los 7 días. Si la nueva contraseña se rechaza, la invitación sigue pendiente.
- **Cambio de email con contraseña** - Cambiar el email del perfil pide la contraseña actual, igual que cambiar la contraseña; el campo aparece al editar el email.
- **2FA obligatorio por cuenta** - Desde Configuración → Seguridad (disponible en todos los tipos de instalación), los administradores pueden exigir la autenticación de dos factores a todos los miembros. Quien no la tenga la configura en la misma pantalla de inicio de sesión (código QR, código y códigos de respaldo) en su próximo acceso con contraseña; los accesos con Google y SAML quedan exentos, y nadie puede desactivar su propio 2FA mientras sea obligatorio. Los tokens de API, MCP y OAuth de los miembros que no lo activaron dejan de funcionar en esa cuenta hasta que lo hagan
- **Verificación de dispositivos nuevos (Cloud)** - Al habilitarla, los accesos con contraseña desde un dispositivo desconocido requieren un código de seis dígitos por correo. Los dispositivos verificados pueden recordarse durante 30 días; cambiar la contraseña o el correo revoca esa confianza. SSO y 2FA conservan sus propios flujos.
- **SAML/SSO** - Single Sign-On empresarial
- **Tokens de API** - Acceso programático seguro
- **Soporte en cuenta suspendida** - Los usuarios suspendidos ven el aviso de política con una acción directa para contactar soporte; los administradores en Cloud también pueden abrir facturación para regularizar el pago y restaurar el acceso. Los superadministradores registran una categoría y un motivo por cada suspensión, y pueden consultar o corregir la última entrada desde los detalles de la cuenta.
- **Cancelación programada de suscripción** - Facturación Cloud muestra la fecha en que terminará una suscripción de Stripe y mantiene el plan activo hasta el cierre de ese período.
- **Reenvío de confirmación** - Los superadministradores pueden reenviar el correo de confirmación a un usuario pendiente desde sus detalles, sin exponer enlaces ni tokens.

### Privacidad

- **GDPR Ready** - Cumplimiento de regulaciones
- **Eliminación de datos** - Derecho al olvido
- **Baja de cuenta desde Super Admin** - Elimina a los usuarios que solo pertenecían a esa cuenta; conserva los usuarios compartidos y los Super Admin
- **Exportación** - Portabilidad de datos

### Infraestructura

- **Encriptación en tránsito** - HTTPS obligatorio
- **Encriptación en reposo** - Datos protegidos
- **Backups automáticos** - Recuperación ante desastres
- **Autoescalado de workers por cola** - Publicación opcional en CloudWatch de latencia, profundidad, trabajos encolados y utilización de Sidekiq para ajustar la capacidad según el backlog
- **Colas sin consumidor** - Alerta en Super Admin y error en log/Sentry cuando hay jobs de Sidekiq esperando en una cola que ningún worker lee, como una cola nueva que falta en un Sidekiq dividido
- **Protección de licencia** *(Mega)* - Verificación de integridad para reforzar control de despliegues
- **Observabilidad de release** - Mejor trazabilidad de errores por versión en monitoreo
- **Super Admin en tu idioma** *(Mega)* - Cada super administrador elige español, inglés o portugués (Brasil) desde el menú lateral; la preferencia se comparte con su perfil del panel de agentes

---

## 📱 Aplicaciones

### Aplicación Web Progresiva (PWA) *(Mega)*

MEGA funciona como una **Progressive Web App** completa: instálala en cualquier dispositivo y obtén una experiencia idéntica a una app nativa, sin pasar por tiendas de aplicaciones.

**Instalación y Experiencia Nativa:**

- **Instalable en un toque** - Banner inteligente que aparece automáticamente en dispositivos móviles invitando a instalar la app
- **Escritorio y móvil** - Funciona en Chrome, Edge, Safari (iOS/macOS) y cualquier navegador compatible con PWA
- **Pantalla completa** - Se ejecuta en modo standalone, sin barra de direcciones del navegador
- **Gestos en la lista de conversaciones** - En el teléfono, deslizar una conversación a la izquierda muestra Asignar (primero se elige agente o equipo), Etapa si tiene un deal abierto, Posponer si está abierta y Resolver; deslizarla a la derecha muestra Eliminar (solo administradores), que pide confirmación antes de borrarla; mantenerla presionada la selecciona, como en WhatsApp, y arriba aparecen Fijar/Desfijar y Eliminar (solo administradores, con confirmación) junto a las acciones de la barra inferior
- **Splash screen personalizado y ágil** - Pantalla de carga con tu marca que se retira apenas Vue pinta la interfaz, con un límite de seguridad si el arranque falla
- **Esqueletos de carga en todas partes** - En cualquier ancho de pantalla, cada página muestra la forma de su contenido mientras carga; la pantalla de conversaciones (lista, chat y panel de contacto) aparece toda junta cuando todo está listo, y el arranque recuerda si el panel de contacto estaba abierto
- **Atajos rápidos** - Accede directamente a Conversaciones o Notificaciones desde el menú contextual del ícono de la app
- **Ícono dinámico** - El ícono de la app se genera desde el logo thumbnail configurado, con respaldo en el ícono de notificaciones, en todos los tamaños necesarios (48px a 512px)
- **Fondo de ícono configurable** - Usa un color propio para el ícono instalable manteniendo blanco como valor por defecto
- **Badge monocromático** - Ícono badge optimizado con silueta monocromática para notificaciones del sistema

**Notificaciones Push Avanzadas:**

- **Notificaciones push nativas** - Recibe alertas instantáneas incluso con la app cerrada, directamente en el sistema operativo
- **Indicador en la pestaña** - Si llega un mensaje con la pestaña oculta o sin foco, el favicon cambia al ícono de notificaciones y vuelve al normal al regresar
- **Respuesta rápida inline** - Responde mensajes directamente desde la notificación sin abrir la app
- **Marcar como leído** - Marca notificaciones como leídas desde la propia notificación con un toque
- **Apilamiento de mensajes** - Los mensajes de la misma conversación se apilan en una sola notificación (estilo WhatsApp) mostrando hasta 10 mensajes
- **Contador de no leídos** - El badge del ícono de la app muestra el número exacto de notificaciones sin leer
- **Timestamp de caché preciso** - Invalidación consistente de assets del Service Worker para evitar contenido desactualizado
- **Activación inteligente** - Prompt automático al abrir la PWA por primera vez para activar notificaciones con flags preconfigurados (asignación, mención, mensaje nuevo)
- **Ciclo de suscripción confiable** - La desactivación por usuario y dispositivo persiste al recargar, el logout revoca el vínculo del navegador y los cambios de clave VAPID se renuevan automáticamente
- **Sonido configurable** - Alertas de audio que funcionan incluso en iOS, con desbloqueo automático de AudioContext al primer toque
- **Sonido diferido** - Si la app está en segundo plano y no puede reproducir audio, lo reproduce automáticamente cuando vuelves a la app
- **Vibración** - Patrón de vibración personalizado en dispositivos móviles al recibir notificaciones

**Funcionamiento Offline:**

- **Página offline personalizada** - Cuando no hay conexión, muestra una página elegante con el logo de tu marca y botón de reintento
- **Caché inteligente** - Solo se guardan assets Vite con fingerprint, dentro de un caché de ejecución acotado para acelerar cargas repetidas
- **Navegación offline segura** - Las páginas autenticadas y APIs nunca se persisten; cuando no hay red se usa la página offline pública
- **Limpieza automática** - El Service Worker elimina versiones obsoletas y limita los assets fingerprinted retenidos

**Personalización de Marca (White-label):**

- **Manifiesto dinámico** - El manifiesto PWA se genera dinámicamente con el nombre, descripción, colores y logo de tu instalación
- **Soporte SVG** - Los logos SVG se convierten a PNG de alta resolución mediante librsvg o libvips antes de componer los assets finales
- **Íconos para Apple** - Generación automática de apple-touch-icons en todos los tamaños requeridos por iOS
- **Splash screens iOS** - 14 resoluciones de splash screen pre-generadas para todos los modelos de iPhone y iPad
- **Colores de marca** - El theme-color y background-color del manifiesto usan tu color primario configurado

### Aplicación Móvil *(En desarrollo)*

- **iOS y Android** - Atiende clientes desde tu teléfono
- **Notificaciones push** - Alertas instantáneas de nuevas conversaciones
- **Funcionalidad completa** - Todas las herramientas en tu bolsillo

---

## 📞 Soporte y Recursos

- **Centro de Ayuda** - Documentación completa y guías paso a paso
- **Comunidad activa** - Conecta con otros usuarios
- **Soporte Enterprise** - Atención prioritaria y dedicada para clientes empresariales

---

*MEGA - Transformando la forma en que las empresas se comunican con sus clientes.*

**© 2026 MEGA - Todos los derechos reservados**

- **Alertas al transferir del bot a un agente** - Una conversación pendiente transferida a atención humana activa el sonido y el indicador de la pestaña tras una breve espera. Respeta los filtros de asignación y visibilidad configurados en Alertas de audio; las notas privadas de Captain no generan un segundo aviso.
