# Configuración de la Integración WooCommerce en MEGA

Conecte su tienda WooCommerce a MEGA para ver los pedidos de cada cliente directamente en la conversación.

Con la integración activa, los agentes ven en la barra lateral de la conversación los pedidos recientes del contacto: número de pedido, estado, fecha y total. Cada número de pedido abre el pedido en el panel de administración de WordPress. De forma opcional, MEGA también puede avisar en la conversación cada vez que cambia el estado de un pedido.

La configuración consta de **3 pasos** (el tercero es opcional).

## Prerrequisitos

Antes de comenzar, asegúrese de tener:

1. **Tienda WooCommerce publicada con HTTPS** y accesible desde internet (MEGA consulta la tienda desde sus servidores, no desde su navegador)
2. **Enlaces permanentes activados** en WordPress: en **Ajustes → Enlaces permanentes** debe estar elegida cualquier opción distinta de **Simple**. Sin esto, la API de WooCommerce (`/wp-json/...`) no responde
3. **Acceso de administrador** en WordPress / WooCommerce
4. **Acceso de administrador** en su cuenta de MEGA
5. **La integración WooCommerce habilitada en su plan**

> **📌 Nota:** WooCommerce es una funcionalidad premium. Si no ve la tarjeta **WooCommerce** en **Ajustes → Integraciones**, su plan no la incluye todavía. Pida a su proveedor de MEGA que la habilite para su cuenta.

## Paso 1 — Crear las claves de la API en WooCommerce

1. En WordPress, vaya a **WooCommerce → Ajustes → Avanzado → API REST**
2. Haga clic en **Añadir clave**
3. Complete los campos:
   - **Descripción**: ej. "MEGA"
   - **Usuario**: un usuario administrador o gestor de la tienda
   - **Permisos**: **Lectura**
4. Haga clic en **Generar clave de API**
5. Copie y guarde en un lugar seguro:
   - **Clave del cliente** (Consumer key), empieza con `ck_`
   - **Clave secreta de cliente** (Consumer secret), empieza con `cs_`

> **⚠️ Importante**
> WooCommerce muestra la clave secreta **una sola vez**. Si la pierde, revoque la clave y genere una nueva.

> **🔒 Seguridad:** MEGA solo lee pedidos, nunca los modifica. El permiso **Lectura** es suficiente; no otorgue **Lectura/Escritura**.

## Paso 2 — Conectar la tienda en MEGA

1. En MEGA, vaya a **Ajustes → Integraciones**
2. Busque **WooCommerce** y haga clic en **Conectar**
3. Complete el formulario:
   - **Store URL**: la dirección de su tienda, ej. `https://www.mitienda.com`
   - **Consumer Key**: la clave `ck_...` del Paso 1
   - **Consumer Secret**: la clave `cs_...` del Paso 1
4. Guarde

### Cómo escribir la Store URL

- Use **exactamente** la **Dirección del sitio (URL)** que figura en WordPress, en **Ajustes → Generales**
- Respete `https://` y el `www` tal como aparecen allí: `https://mitienda.com` y `https://www.mitienda.com` cuentan como tiendas distintas
- No agregue `/wp-admin`, `/shop` ni otras rutas. La barra final da igual
- Si WordPress está instalado en una subcarpeta (ej. `https://mitienda.com/tienda`), incluya la subcarpeta

> **📌 Nota:** MEGA no prueba las claves al guardar. La forma de comprobar que todo funciona es abrir una conversación (ver el paso siguiente).

### Comprobar la conexión

1. Abra una conversación de un cliente que ya haya comprado en la tienda
2. En la barra lateral derecha, despliegue la sección **Pedidos de WooCommerce**
3. Debería ver sus pedidos recientes, cada uno con:
   - **Pedido n.º** (haga clic para abrirlo en WordPress)
   - **Estado**: Pendiente, Procesando, En espera, Completado, Cancelado, Reembolsado o Fallido
   - **Fecha** y **total** con su moneda

### Cómo encuentra MEGA los pedidos de un contacto

- MEGA busca los pedidos por el **correo electrónico** y por el **teléfono** del contacto, y muestra los resultados juntos, sin repetir pedidos
- **Por correo**: el correo del contacto debe coincidir con el de facturación del pedido
- **Por teléfono**: MEGA reconoce el teléfono de facturación aunque el cliente lo haya escrito con espacios, guiones o sin código de país (ej. `011 1234-5678`), usando el país de facturación del pedido. Así coincide con el formato internacional del contacto (ej. `+5491112345678`)
- Se muestran los **10 pedidos más recientes**
- Si el contacto no tiene correo ni teléfono, la sección indica **No se encontraron pedidos**

> **💡 Consejo:** Puede reordenar o contraer la sección **Pedidos de WooCommerce** dentro de la barra lateral, igual que las demás secciones.

## Paso 3 — Avisos de cambio de estado (opcional)

Con este paso, cada vez que cambia el estado de un pedido, MEGA agrega una nota en la conversación del cliente, por ejemplo:

> El estado del pedido 1234 se actualizó a completed

El estado aparece tal como lo envía WooCommerce (`pending`, `processing`, `on-hold`, `completed`, `cancelled`, `refunded`, `failed`).

### Crear el webhook en WooCommerce

1. En WordPress, vaya a **WooCommerce → Ajustes → Avanzado → Webhooks**
2. Haga clic en **Añadir webhook**
3. Complete los campos:
   - **Nombre**: ej. "MEGA - pedidos"
   - **Estado**: **Activo**
   - **Tema**: **Pedido actualizado**
   - **URL de entrega**: `https://SU-DOMINIO-MEGA/woocommerce/callback` (reemplace `SU-DOMINIO-MEGA` por la dirección con la que entra a MEGA, ej. `https://app.miempresa.com/woocommerce/callback`)
   - **Secreto**: puede dejar el valor que propone WooCommerce
   - **Versión de la API**: **WP REST API Integration v3**
4. Haga clic en **Guardar webhook**

> **💡 Consejo:** Si también quiere un aviso cuando se crea un pedido, repita los pasos con el tema **Pedido creado**.

### Cómo funcionan los avisos

- MEGA identifica la tienda por su dirección, por eso la **Store URL** del Paso 2 debe coincidir con la dirección del sitio en WordPress
- El cliente se busca por el **correo de facturación** del pedido y, si no hay coincidencia, por el **teléfono de facturación**, en cualquier formato (se interpreta con el país de facturación)
- La nota se agrega en la **conversación más reciente** del cliente. Si el cliente no tiene ninguna conversación en MEGA, no se agrega nada
- La sección **Pedidos de WooCommerce** se actualiza al abrir la conversación. Si la tiene abierta cuando llega el aviso, vuelva a abrirla para ver el estado nuevo

## Solución de problemas

| Problema | Causa probable | Solución |
|---|---|---|
| No aparece **WooCommerce** en **Ajustes → Integraciones** | Su plan no incluye la integración | Pida a su proveedor de MEGA que la habilite |
| La sección **Pedidos de WooCommerce** no aparece en la conversación | La integración no está conectada, o la sección está oculta | Revise el Paso 2 y las secciones de la barra lateral |
| La sección muestra un error al cargar los pedidos | Claves incorrectas o revocadas, Store URL mal escrita, enlaces permanentes en **Simple**, o un firewall / plugin de seguridad bloquea `/wp-json/` | Revise las claves y la Store URL; active los enlaces permanentes; permita el acceso a `/wp-json/wc/v3/` en su firewall, Cloudflare o plugin de seguridad |
| **No se encontraron pedidos** para un cliente que sí compró | Ni el correo ni el teléfono del contacto coinciden con los de facturación del pedido | Corrija o agregue el correo o el teléfono en el contacto |
| No llegan los avisos de cambio de estado | Webhook inactivo, URL de entrega incorrecta, Store URL distinta de la dirección del sitio, o el cliente no tiene conversación en MEGA | Revise el Paso 3. En **WooCommerce → Estado → Registros** busque los registros `webhooks-delivery` para ver las respuestas |
| El webhook aparece como **Desactivado** | WooCommerce lo desactiva solo tras varios envíos fallidos | Corrija la URL de entrega y vuelva a ponerlo en **Activo** |

## Desconectar la integración

1. En MEGA, vaya a **Ajustes → Integraciones → WooCommerce** y elimine la integración
2. En WordPress, vaya a **WooCommerce → Ajustes → Avanzado → API REST** y **revoque** la clave creada para MEGA
3. Si creó webhooks, elimínelos en **WooCommerce → Ajustes → Avanzado → Webhooks**
