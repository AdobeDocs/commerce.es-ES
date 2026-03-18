---
title: Tutorial sobre la extensión de notificaciones InStock
description: Obtenga información sobre cómo crear una extensión de notificaciones en stock para Adobe Commerce as a Cloud Service mediante App Builder, Edge Delivery Services y herramientas de desarrollo asistido por IA.
solution: Commerce
feature: App Builder, Cloud
feature-set: Commerce
role: Developer
level: Intermediate
type: Tutorial
hide: true
hidefromtoc: true
source-git-commit: ce8882b8af21198a7bc57bc58124e8a2d1491a50
workflow-type: tm+mt
source-wordcount: '2599'
ht-degree: 0%

---

# Tutorial de extensión de notificaciones en existencia

Este tutorial lo guiará a través del proceso de creación de una extensión de notificación en existencia para [!DNL Adobe Commerce as a Cloud Service] mediante [!DNL Adobe App Builder] y las herramientas de desarrollo asistido por IA. La extensión permite a los compradores suscribirse a productos sin existencias y recibir una notificación cuando el producto vuelve a estar disponible.

Se construyen dos partes:

- **Extensión de App Builder**: una API de REST para administrar suscripciones sin existencias (crear, leer, eliminar) con detección de back-in-stock controlada por eventos y programada.
- **Integración de tienda**: un formulario de suscripción en la página de detalles del producto (PDP) que aparece solamente cuando el producto o la variante seleccionados no tienen existencias.

>[!NOTE]
>
>Los agentes de la IA no son deterministas. Los mensajes, preguntas y resultados de este tutorial son ejemplos. Su agente puede presentar diferentes preguntas, requisitos o propuestas de arquitectura. Utilice los ejemplos de este tutorial para dirigir al agente hacia un resultado similar.

Antes de empezar, complete [requisitos previos](./tutorial-prerequisites.md). Este tutorial utiliza **integration starter kit**. Compruebe que ya lo ha clonado y que ha completado los pasos de configuración descritos en la página de requisitos previos.

## Comprobar requisitos previos

Compruebe que están instalados los siguientes requisitos previos:

```bash
# Check Node.js version (should be 22.x.x)
node --version

# Check npm version (should be 9.0.0 or higher)
npm --version

# Check Git installation
git --version

# Check Bash shell installation
bash --version
```

Si alguno de los comandos anteriores no devuelve los resultados esperados, consulte los [requisitos previos](./tutorial-prerequisites.md) para obtener instrucciones.

Además, compruebe lo siguiente:

- Tiene una instancia de [!DNL Adobe Commerce as a Cloud Service] con datos del producto. Ver [instancias del servicio Commerce Cloud](https://experienceleague.adobe.com/es/docs/commerce/cloud-service/overview){target="_blank"}.
- Tiene un proyecto de tienda conectado a la instancia [!DNL Commerce]. Si no tienes una, sigue los pasos de [Crear una tienda](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/?lang=es){target="_blank"}.
- La CLI `aem` está instalada:

  ```bash
  npm install -g @adobe/aem-cli
  ```

## Desarrollo de extensiones

Esta sección le guiará a través del desarrollo de una extensión de notificación en existencia para [!DNL Adobe Commerce as a Cloud Service] mediante herramientas de desarrollo asistido por IA. La extensión proporciona una API de REST para la administración de suscripciones y detecta cuándo los productos vuelven a estar en stock a través de eventos de Commerce y una comprobación programada.

1. Vaya a la configuración de MCP del agente de codificación.

   Por ejemplo, en Cursor, vaya a **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**. Compruebe que el conjunto de herramientas `commerce-extensibility` esté habilitado sin errores. Si hay errores, active o desactive el conjunto de herramientas.

   >[!NOTE]
   >
   >Cuando trabaje con herramientas de desarrollo asistido por IA, espere variaciones naturales en el código y las respuestas generadas por el agente.
   >Si encuentra algún problema con su código, pídale al agente que le ayude a depurarlo.

1. Si se ha añadido documentación al contexto del cursor, desactívela.

   Vaya a **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Indexing & Docs]** y elimine cualquier documentación enumerada.

### Paso 1: Proporcione la solicitud inicial

Solicite al agente de IA que inicie la implementación. Indicar al agente que se detenga y haga preguntas le ayuda a dirigir la implementación desde el principio.

Introduzca el siguiente mensaje en la ventana de chat del agente:

```shell-session
Implement an Adobe Commerce as a Cloud Service extension to handle out-of-stock notifications for products.

The service should provide REST API endpoints for basic create, read, update, and delete (CRUD) operations on out-of-stock notifications, allowing storefronts to manage notifications for specific product SKUs.

Back-in-stock is detected by an inventory or product event or a scheduled action that checks Commerce API and then calls the REST API to send the notification.

STOP and ask me any clarifying questions you have about the requirements before you do any work.
```

>[!TIP]
>
>Indicar al agente que se DETENGA y haga preguntas antes de continuar le ayuda a dirigir la implementación al principio del proceso. Este proceso garantiza que las suposiciones clave y los requisitos que faltan se identifiquen anticipadamente y que son necesarios para iniciar el flujo de trabajo guiado en este tutorial.

### Paso 2: Responda las preguntas del agente

El agente regresa con una serie de preguntas que necesita antes de que pueda comenzar a formar una solución. El siguiente ejemplo muestra preguntas y respuestas típicas. Su agente puede hacer diferentes preguntas, pero los temas generalmente son los mismos.

**Ejemplo de preguntas del agente:**

1. **API de REST — host y consumidores** — ¿Debería la API de REST de CRUD formar parte de esta aplicación de App Builder (por ejemplo, acciones web en Adobe I/O Runtime) a la que llaman las tiendas? ¿Quién lo llamará (tienda EDS, tienda personalizada/sin encabezado o ambas)? ¿Necesita CORS, acceso público (no autenticado) o los llamadores utilizarán claves de API, OAuth o tokens de Commerce?
1. **Modelo de datos** — ¿Qué debería representar una &quot;notificación&quot;? ¿Identificador de cliente (solo correo electrónico o también ID de cliente)? ¿Identificador de producto (solo SKU o SKU + vista de tienda)? ¿Puede el mismo cliente suscribirse al mismo SKU varias veces o deben deduplicarse las suscripciones?
1. **Detección de volver a existencias: evento frente a programado**. ¿Desea una detección controlada por eventos (reaccionar ante un evento de inventario/producto de Commerce), una detección programada (una acción programada que compruebe existencias periódicamente) o ambas? ¿Qué significa &quot;enviar la notificación&quot; (llamar a un webhook externo, enviar un correo electrónico o registrarlo)?
1. **Volver a estar disponible — Commerce source** — ¿Tiene un nombre de evento preferido o el diseño debe usar el evento actualizado de inventario/existencias que Commerce proporciona? Para las comprobaciones programadas, ¿qué API debe utilizarse para obtener el estado de las existencias por SKU?
1. **Persistencia y multiinquilinos**: ¿Es `aio-lib-state` el lugar adecuado para mantener suscripciones o tiene una tienda externa? ¿Debe el diseño suponer que hay varios inquilinos o un solo inquilino?
1. **Semántica de CRUD y ciclo de vida**: ¿debería &quot;eliminar&quot; significar cancelar la suscripción? ¿Necesita &quot;actualizar&quot;? Después de enviar una notificación de reserva, ¿debe eliminarse automáticamente la suscripción o marcarse como notificada?
1. **No funcional**: ¿Hay límites de tarifa o suscripciones máximas que aplicar? ¿Alguna necesidad de conformidad (doble inclusión, indicador de consentimiento)?

**Respuestas de ejemplo:**

```shell-session
1. The CRUD REST API should be part of thie App Builder app. It will be called by the EDS Storefront. For this implementation there is no need for API keys or security tokens.
2. For this initial implementation the customer identifier will be the email, product is identified by SKU, customer emails should not be able to subscribe to the same SKU multiple times.
3. Implement both. For now instead of sending the notification, log it so I can audit in the Adobe Developer Console.
4. Research and use what the best event to use that commerce already provides. Research the simplest way to get the stock status by SKU.
5. Use the aio-lib-state. Single tenant for now
6. Delete means cancel subscription. Skip Update, it does not apply for this service. After subscription is sent, it should be marked as notified or removed so it won't send again until the user subscribes again.
7. No limits. Implement minimal compliance requirements.
```

>[!NOTE]
>
>Su agente puede hacer diferentes preguntas. Utilice estas respuestas como guía para dirigir el agente hacia el mismo resultado funcional: una API de REST con suscripciones de correo electrónico y SKU, detección de back-in-stock controlada por eventos y programada, persistencia de `aio-lib-state` y notificaciones basadas en registro.

### Paso 3: Revisar los requisitos y la arquitectura

El agente genera requisitos y documentos de arquitectura para que los revise. Compruebe que los requisitos coinciden con las respuestas proporcionadas y que la arquitectura cubre lo siguiente:

- Una acción de API de REST para CRUD de suscripción (crear, leer, actualizar y eliminar)
- Un controlador back-in-stock impulsado por eventos activado por eventos de inventario de Commerce
- Una acción de stock programada como reserva
- Persistencia al utilizar `aio-lib-state`

>[!NOTE]
>
>Los agentes de IA son no deterministas y sus comportamientos difieren según el modelo y el IDE. Puede obtener un conjunto diferente de preguntas que producen un conjunto diferente de requisitos y arquitectura. Si es así, intente dirigir el agente en una dirección tal que la implementación coincida estrechamente con lo que se presenta en este tutorial antes de continuar.

### Paso 4: Selección de un plan de implementación

El agente le da la opción de crear un plan de implementación detallado o de completar una implementación directa.

- Si desea un plan revisable que se pueda ejecutar por fases con más control, seleccione la primera opción.
- Si desea que el agente realice la implementación completa con una intervención mínima, seleccione la segunda opción.

### Paso 5: Implementación, incorporación y suscripción a eventos

Una vez que el agente completa la implementación, proporciona los siguientes pasos para implementar la aplicación, incorporar la instancia de Commerce y suscribirse a eventos mediante los siguientes comandos:

1. Implemente la extensión:

   ```bash
   aio app deploy
   ```

1. Ejecute el script de incorporación para registrar el proveedor de eventos con Commerce:

   ```bash
   npm run onboard
   ```

1. Suscribirse a eventos de Commerce:

   ```bash
   npm run commerce-event-subscribe
   ```

1. Valide la suscripción al evento.

   Vaya a la instancia de Commerce y abra **[!UICONTROL System]** > **[!UICONTROL Event Subscriptions]**.

   Debería ver una tabla de registros de eventos.

   ![Menú de administración de Commerce que resalta la sección Suscripción a evento](../assets/in-stock-event-subscriptions.png){width="600" zoomable="yes"}

   ![Tabla de suscripción de eventos con entradas de eventos registradas](../assets/in-stock-event-table.png){width="600" zoomable="yes"}

### Paso 6: Prueba de la extensión

Pida al agente que proporcione los pasos de la prueba. Como es un servicio API, puede solicitar instrucciones de línea de comandos:

```shell-session
Give me step by step instructions to test the API service from the command line.
```

Siga los pasos que proporcione el agente. Los siguientes ejemplos muestran comandos de prueba típicos.

**Suscribirse a un SKU:**

```bash
API_URL="https://<your-runtime-url>/api/v1/web/notify-out-of-stock/api"; curl -X POST "$API_URL" \
  -H "Content-Type: application/json" \
  -d '{"email":"test@example.com","sku":"ADB153"}'
```

La respuesta es similar a:

```json
{
  "createdAt": "2026-03-06T22:11:00.308Z",
  "email": "test@example.com",
  "id": "b3353bf5-1007-4b10-989d-430892dd4a66",
  "sku": "ADB153"
}
```

**Enumerar todas las suscripciones:**

```bash
curl -X GET "$API_URL"
```

La respuesta devuelve una lista de todas las suscripciones activas:

```json
{
  "subscriptions": [
    {
      "createdAt": "2026-03-06T22:11:00.308Z",
      "email": "test@example.com",
      "id": "b3353bf5-1007-4b10-989d-430892dd4a66",
      "sku": "ADB153"
    }
  ]
}
```

**Probar el flujo de reserva:**

1. Desde la instancia de Commerce, edite un producto para el que haya creado una suscripción.
1. Establezca el estado de existencias del producto en **[!UICONTROL Out of Stock]**.
1. Espere aproximadamente un minuto y cambie el estado de las existencias a **[!UICONTROL In Stock]**.

   ![Página de edición del producto de administración de Commerce que muestra el menú desplegable Estado de stock con las opciones En stock y Sin existencias](../assets/in-stock-product-stock-status-toggle.png){width="600" zoomable="yes"}

1. Espere unos cinco minutos para que el evento déclencheur y se envíe a su servicio.

1. En [!DNL Adobe Developer Console], vaya a la sección Registros de App Builder.

   ![Sección de registros de Adobe Developer Console App Builder](../assets/in-stock-developer-console-logs.png){width="600" zoomable="yes"}

1. En los registros, compruebe que haya entradas que confirmen que el evento se ha procesado y que se ha identificado el par de suscripción de correo electrónico-SKU correcto.

   ![Entradas de registro de App Builder que muestran el procesamiento de eventos de reserva](../assets/in-stock-log-entries.png){width="600" zoomable="yes"}

>[!TIP]
>
>Puede preguntar al agente qué buscar en los registros para comprobar que la acción de notificación se registró correctamente. También puede copiar y pegar las entradas de registro para que el agente realice la verificación.

Después de los procesos del evento de reserva, la solicitud de la lista de suscripciones debe devolver una entrada menos, ya que la suscripción notificada se elimina.

### Creación del contrato de servicio

Ahora que la implementación del servicio ha finalizado, pídale al agente que cree un contrato de servicio para el trabajo de la tienda:

```shell-session
Create an API service contract for the Out of Stock notification service and its endpoints. Ensure that the service contract is clear and detailed enough for a frontend developer to implement the storefront UI integration without needing to ask additional questions about the API. Name this file OUT_OF_STOCK_NOTIFICATION_CONTRACT.md
```

Copie este archivo en su proyecto de tienda para que el agente de tienda pueda hacer referencia a él.

## Conectar con la tienda

Esta sección le guiará a través de la implementación de la parte de tienda de la extensión de notificaciones en existencia mediante [!DNL Edge Delivery Services] y las herramientas de desarrollo asistido por IA. Agrega un formulario de suscripción a la página de detalles del producto (PDP) que aparece únicamente cuando el producto o la variante seleccionados están agotados.

>[!NOTE]
>
>Las indicaciones proporcionadas son puntos de partida. Aunque puede utilizarlas sin modificaciones, considere la posibilidad de mantener una conversación natural con el agente.
>
>Al trabajar con herramientas de desarrollo asistido por IA, siempre hay variaciones naturales en el código y las respuestas generadas por el agente.
>
>Si encuentra algún problema con su código, pídale al agente que le ayude a depurarlo.

### Requisitos previos de Storefront

Antes de iniciar la integración de tienda, comprueba que tienes lo siguiente:

- Un proyecto de tienda conectado a su instancia [!DNL Commerce]
- Herramientas de IA de tienda de Commerce [instaladas con CLI](./tutorial-prerequisites.md#install-the-storefront-ai-tools)
- El archivo `OUT_OF_STOCK_NOTIFICATION_CONTRACT.md` se copió en el proyecto de tienda

### Paso 1: Validar el entorno

Abra el archivo `config.json` y compruebe que los valores de `commerce-core-endpoint` y `commerce-endpoint` apuntan al extremo de GraphQL [!DNL Adobe Commerce as a Cloud Service].

```json
"commerce-core-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
"commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
```

### Paso 2: Proporcione la solicitud inicial

Con el contrato de servicio ya en el proyecto, solicite al agente que cree la interfaz de usuario en la página de detalles del producto. Utilice el modo **Plan** si está disponible en su agente, para evitar que el agente continúe sin un plan.

```shell-session
Analyze @OUT_OF_STOCK_NOTIFICATION_CONTRACT.md. Add a form for subscribing to a notification for when a product is back in stock. Place this form on the product details page, underneath the add to cart and wishlist button. The form only displays when a product is out of stock. 

Use the project manager skill to plan this implementation.
```

>[!TIP]
>
>Solicitud específica para utilizar los déclencheur de aptitudes del administrador de proyectos en el flujo de trabajo por fases que le ayuda a dirigir la implementación al principio del proceso. Este proceso garantiza que las suposiciones clave y los requisitos que faltan se identifiquen antes de tiempo y da al agente la oportunidad de presentarle detalles y requisitos que puede que no haya pensado proporcionar en el mensaje original.

### Paso 3: Responder preguntas de planificación

El agente regresa con una serie de preguntas que debe responder antes de que pueda comenzar a formar una solución. El siguiente ejemplo muestra preguntas y respuestas típicas. Su agente puede hacer diferentes preguntas, pero los temas generalmente son los mismos.

**Ejemplo de preguntas del agente:**

1. **URL base de API** — ¿Cómo debería obtener la tienda la URL base de API de notificación sin existencias? Las opciones pueden incluir un bloque de configuración (por ejemplo, una tabla con `out-of-stock-api-base-url`), marcadores de posición globales o variables de entorno, u otro método.
1. **Copiar**: ¿Debe la implementación usar marcadores de posición para los mensajes de éxito y error (por ejemplo, para la localización) o usar el inglés estático para esta implementación?
1. **Después de la suscripción correcta**: ¿el formulario debe ocultarse y mostrar solo &quot;Está suscrito&quot; (A), mantener el formulario visible pero deshabilitado con un mensaje de éxito encima (B) u otro comportamiento (C)?
1. **Productos configurables** — ¿Debe la visibilidad del formulario basarse en el valor `inStock` de la variante seleccionada, de modo que el formulario se muestre cuando la variante elegida no tiene existencias?

**Respuestas de ejemplo:**

```shell-session
1. Global placeholder with baseurl value of `https://<your-runtime-url>/api/v1/web/notify-out-of-stock/api`
2. Use placeholders with static English fallback
3. B
4. Use selected variant's inStock value
```

>[!NOTE]
>
>Reemplace `<your-runtime-url>` con la URL [!DNL Adobe I/O Runtime] real de su implementación de App Builder.
>
>Su agente puede hacer diferentes preguntas. Utilice estas respuestas como guía:
>
>- Utilice un marcador de posición global para la dirección URL base de la API de modo que se pueda cambiar sin modificaciones de código.
>- Utilice marcadores de posición para la copia orientada al usuario con el inglés estático como alternativa.
>- Después de una suscripción correcta, mantenga el formulario visible pero deshabilitado con un mensaje de éxito encima.
>- Para los productos configurables, utilice el valor `inStock` de la variante seleccionada para controlar la visibilidad del formulario.

### Paso 4: Revisar los requisitos y la arquitectura

El agente actualiza el documento de requisitos para que lo revise. Compruebe que:

- El formulario solo aparece cuando el producto o la variante seleccionada están agotados.
- El formulario se coloca debajo de los botones Agregar al carro y Lista de deseos en la PDP.
- La integración de API de utiliza la dirección URL base de un marcador de posición global.
- Los estados de éxito y error se gestionan según el contrato (201, 409, 400, 503/500).

>[!NOTE]
>
>Los agentes de IA son no deterministas y sus comportamientos difieren según el modelo y el IDE. Puede obtener un conjunto diferente de preguntas que producen un conjunto diferente de requisitos y arquitectura. Si es así, intente dirigir el agente en una dirección tal que la implementación coincida estrechamente con lo que se presenta en este tutorial antes de continuar.

Durante la **Fase 2 (Planificación arquitectónica)**, el agente investiga la documentación y el código base antes de proponer una arquitectura. Se espera que el agente:

- Busque en la documentación de [!DNL Commerce] contenedores de PDP, ranuras y cargas útiles de eventos.
- Analice el directorio `blocks` y la carpeta `scripts/initializers/` en busca de código relacionado con PDP existente.
- Explore las definiciones de TypeScript para los contenedores disponibles y las formas de contexto de ranura.

A continuación, el agente presenta las opciones de arquitectura. Revise el plan e indique al agente que continúe.

### Paso 5: Selección de un plan de implementación

El agente le da la opción de crear un plan de implementación detallado o de completar una implementación directa.

- Si desea un plan revisable que se pueda ejecutar por fases con más control, seleccione la primera opción.
- Si desea que el agente realice la implementación completa con una intervención mínima, seleccione la segunda opción.

Durante la **fase 4 (implementación)**, el agente genera código basado en la arquitectura elegida. Según el enfoque, el agente utiliza varias habilidades especializadas:

- **Modelado de contenido:** Si se necesita un nuevo bloque, el agente diseña una estructura de contenido compatible con el autor.
- **Desarrollo de bloques:** El agente crea archivos de bloque siguiendo las convenciones de [!DNL Edge Delivery Services], incluidas las funciones decorativas de JavaScript, los estilos CSS con ámbito, las etiquetas ARIA para accesibilidad y la administración de estados de carga y error.
- **Personalización de inclusión:** Si la arquitectura usa la personalización de ranura, el agente importa el contenedor correcto, usa una ranura verificada cerca del título del producto y se suscribe a los eventos de datos del producto para el SKU actual.

Observe el código que se está generando y haga preguntas o redirija el agente según sea necesario.

### Paso 6: Inicio del servidor y prueba

Una vez que el agente haya completado la implementación, inicie el servidor de desarrollo y pruebe el formulario.

1. Inicie el servidor de desarrollo local:

   ```bash
   npm run start
   ```

1. En un explorador, vaya a una página de productos sin existencias. Por ejemplo:

   ```shell-session
   http://localhost:3000/products/<out-of-stock-product-slug>/<sku>
   ```

1. Compruebe que el formulario de suscripción aparece debajo de los botones Agregar al carro y Lista de deseos.

Puede realizar pruebas manuales o pedir al agente que utilice sus capacidades de explorador para realizar pruebas:

```shell-session
Run complete browser testing. Use the following out of stock product 'http://localhost:3000/products/<out-of-stock-product-slug>/<sku>'
```

![Página de detalles del producto que muestra el formulario de notificación disponible debajo del botón Agregar al carro de compras](../assets/in-stock-notification-form.png){width="600" zoomable="yes"}

### Paso 7: Limpiar

Después de omitir o completar la prueba, el agente le pedirá que continúe con la fase final de **Limpieza**. Tras la confirmación, el agente archiva todos los artefactos de documentación creados durante la implementación.

## Resolución de problemas

Utilice las siguientes sugerencias si encuentra problemas durante el tutorial:

- **Errores de API:** Utilice la CLI para enviar solicitudes a la API directamente a fin de comprobar los comportamientos. Por ejemplo, use `curl` para probar cada extremo de forma independiente.
- **Errores del agente:** copie y pegue mensajes de error en una sesión de chat del agente para ayudarle a depurar los problemas. El agente puede diagnosticar problemas comunes, como la falta de variables de entorno o acciones mal configuradas.
- **Canalización de eventos:** Si los eventos de reserva no entran en déclencheur, compruebe que ha completado los pasos de incorporación y suscripción de eventos. Compruebe que `workspace.json` se encuentra en la ubicación correcta y que el módulo Eventos de Commerce está habilitado.
- **Carga útil de estado de stock:** Commerce puede enviar `is_in_stock` como una cadena (`"1"`) en lugar de un booleano (`true`). Si no se activa el controlador de reserva, pida al agente que compruebe el código del consumidor para ver si hay comparaciones de tipo estrictas y que lo actualice para administrar ambos formatos.

## Resumen del tutorial

A continuación se muestra un resumen de los temas tratados en este tutorial:

- **Desarrollo de extensiones:** que describe la nueva funcionalidad a un agente de IA y genera una API de REST en funcionamiento con operaciones de CRUD usando [!DNL App Builder].
- **Arquitectura impulsada por eventos:** Configuración de eventos de Commerce y una acción programada para detectar cuándo los productos vuelven a estar disponibles.
- **Pruebas e implementación locales:** Pruebas de la API con `curl` e implementación mediante [!DNL Adobe I/O CLI].
- **Contratos de servicio:** Creación de contratos de API que vinculan extensiones backend e implementaciones de tienda.
- **Integración de tienda por fases:** Trabajando con los requisitos, la arquitectura y la implementación con habilidades asistidas por IA.
- **Integración de inclusión:** Agregar un formulario de suscripción al PDP usando [!DNL Adobe Commerce] contenedores y ranuras de inclusión.

## Pasos siguientes

Utilice las siguientes sugerencias para ampliar el servicio de notificaciones en existencia:

- **Enviar notificaciones reales:** Reemplace la notificación basada en el registro con un servicio de correo electrónico como [!DNL Adobe Campaign] o un proveedor de terceros.
- **Agregar una página de administración de suscripciones:** Cree una página de tienda donde los compradores puedan ver y cancelar sus suscripciones activas.
- **Admitir implementaciones de varios inquilinos:** Amplíe la administración de estado para admitir varios inquilinos de Commerce en una sola aplicación de App Builder.
- **Agregar limitación de velocidad:** Implemente límites de velocidad en la API de suscripción para evitar abusos.
