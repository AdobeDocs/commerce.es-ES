---
title: Tutorial de extensión de críticas de productos
description: Obtenga información sobre cómo crear una extensión de revisiones de productos y preguntas y respuestas para Adobe Commerce as a Cloud Service mediante App Builder, Edge Delivery Services y herramientas de desarrollo asistido por IA.
solution: Commerce
feature: App Builder, Cloud
feature-set: Commerce
role: Developer
level: Intermediate
type: Tutorial
hide: true
hidefromtoc: true
source-git-commit: 9c76bae29c05909406a40ca03a2b3d242db05f3f
workflow-type: tm+mt
source-wordcount: '2470'
ht-degree: 0%

---

# Tutorial de extensión de críticas de productos

Este tutorial le guiará a través del proceso de creación de una extensión que permite a los clientes enviar una revisión del producto y contenido de preguntas y respuestas (preguntas y respuestas) para tiendas con un back-end de [!DNL Adobe Commerce as a Cloud Service] mediante [!DNL Adobe App Builder] y herramientas de desarrollo asistido por IA. La extensión proporciona puntos finales de API de REST para que los compradores vean y envíen contenido de revisión de producto, preguntas y respuestas y lo muestren en la página de detalles del producto (PDP).

Se construyen dos partes:

- **Extensión de App Builder**: una API de REST con operaciones de GET y POST para crear y ver contenido de revisión de productos y preguntas y respuestas con validación, paginación y persistencia en `aio-lib-state`.
- **Integración de tienda**: un bloque de revisión de producto en el PDP que muestra críticas y preguntas y respuestas, con formularios para que los compradores envíen críticas, preguntas y respuestas.

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

Si alguno de los comandos anteriores no devuelve los resultados esperados, vea los [requisitos previos](./tutorial-prerequisites.md) para obtener instrucciones.

Además, compruebe lo siguiente:

- Tiene una instancia de [!DNL Adobe Commerce as a Cloud Service] con datos del producto. Ver [instancias del servicio Commerce Cloud](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/overview){target="_blank"}.
- Tiene un proyecto de tienda conectado a la instancia [!DNL Commerce]. Si no tienes una, sigue los pasos de [Crear una tienda](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/){target="_blank"}.
- La CLI `aem` está instalada:

  ```bash
  npm install -g @adobe/aem-cli
  ```

## Desarrollo de extensiones

Esta sección le guía a través del desarrollo de una extensión para enviar y ver la revisión del producto y el contenido de preguntas y respuestas para la extensión de tiendas con un back-end [!DNL Adobe Commerce as a Cloud Service] mediante herramientas de desarrollo asistido por IA. La extensión proporciona una API de REST para enviar y ver la revisión del producto y el contenido de preguntas y respuestas, y para mostrarlo en la PDP.

1. Vaya a la configuración de MCP del agente de codificación. Por ejemplo, en Cursor, vaya a **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**. Compruebe que el conjunto de herramientas `commerce-extensibility` esté habilitado sin errores. Si hay errores, active o desactive el conjunto de herramientas.

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
I want to build an Adobe Commerce as a Cloud Service extension that allows shoppers to submit and view product review and question and answer (Q&A) content that displays on product detail pages (PDP).

## Product Reviews
The application has REST API endpoints that can be called by a storefront to retrieve and submit product reviews for a given SKU.

The GET endpoint accepts the following query parameters:
- sku (string, required): The SKU of the product to fetch reviews for
- limit (integer, optional): The maximum number of reviews to return (default: 10)
- offset (integer, optional): The number of reviews to skip for pagination (default: 0)

The POST endpoint accepts the following JSON body parameters:
- sku (string, required): The SKU of the product to submit a review for
- rating (integer, required): The rating for the product (1-5)
- review (string, optional): The text of the review
- user (string, optional): The name of the user submitting the review

The POST endpoint validates the input and returns appropriate error responses for invalid data. The reviews are stored and associated with the corresponding product SKU.

## Questions and Answers
The application has REST API endpoints that can be called by a storefront to retrieve and submit questions and answers for a given SKU.

The GET endpoint accepts the following query parameters:
- sku (string, required): The SKU of the product to fetch questions and answers for
- limit (integer, optional): The maximum number of questions and answers to return (default: 10)
- offset (integer, optional): The number of questions and answers to skip for pagination (default: 0)

The POST endpoint accepts the following JSON body parameters:
- sku (string, required): The SKU of the product to submit a question or answer for
- type (string, required): The type of submission ("question" or "answer")
- questionId (string, required if type is "answer"): The ID of the question being answered
- content (string, required): The text of the question or answer
- user (string, optional): The name of the user submitting the question or answer

The POST endpoint validates the input and returns appropriate error responses for invalid data. The questions and answers are stored and associated with the corresponding product SKU. Answers are also associated with the corresponding question.

Do not require Adobe IMS authentication for these endpoints. They will be called directly from the storefront.

STOP and ask me any clarifying questions you have about the requirements before you do any work.
```

>[!TIP]
>
>Si le dice al agente que PARE y haga preguntas antes de continuar, podrá dirigir la implementación desde el principio del proceso. Esto garantiza que las suposiciones clave y los requisitos que faltan se identifiquen anticipadamente y son necesarios para iniciar el flujo de trabajo guiado en este tutorial.

### Paso 2: Responda las preguntas del agente

El agente regresa con una serie de preguntas que debe responder antes de que pueda comenzar a formar una solución. El siguiente ejemplo muestra preguntas y respuestas típicas. Su agente puede hacer diferentes preguntas, pero los temas generalmente son los mismos.

**Ejemplo de preguntas del agente:**

1. **API de REST — host y consumidores** — ¿Debería la API de REST de CRUD formar parte de esta aplicación de App Builder (acciones web en Adobe I/O Runtime) a la que llaman las tiendas? ¿Quién lo llamará (tienda EDS, tienda personalizada/sin encabezado o ambas)? ¿Necesita CORS, acceso público (no autenticado) o los llamadores utilizarán claves API o OAuth?
1. **Modelo de datos**: ¿Qué debe representar una &quot;revisión&quot; o una &quot;pregunta&quot;? ¿Identificador de cliente (solo correo electrónico o también ID de cliente)? ¿Identificador de producto (solo SKU o SKU + vista de tienda)? ¿Puede el mismo cliente enviar varias revisiones para el mismo SKU?
1. **Persistencia**: ¿Es `aio-lib-state` el lugar adecuado para mantener las críticas y las preguntas y respuestas, o bien tiene una tienda externa? ¿Debe el diseño suponer que hay varios inquilinos o un solo inquilino?
1. **Semántica de paginación**: para GET de preguntas y respuestas, ¿se aplica `limit` solo a preguntas (con respuestas anidadas) o al recuento total de preguntas más respuestas?

**Respuestas de ejemplo:**

```shell-session
1. The REST API should be part of this App Builder app. It will be called by the EDS Storefront. No authentication — public access for both GET and POST.
2. For reviews: sku, rating (1-5), optional review text, optional user name. For Q&A: sku, type (question or answer), content, optional user. Answers linked to questions via questionId. Allow multiple reviews per SKU from the same user.
3. Use aio-lib-state. Single tenant for now.
4. Pagination by question — limit and offset apply to questions; each question includes its nested answers.
```

>[!NOTE]
>
>Su agente puede hacer diferentes preguntas. Utilice estas respuestas como guía para dirigir al agente hacia el mismo resultado funcional: una API de REST pública con revisiones y preguntas y respuestas, persistencia de `aio-lib-state` y sin autenticación.

### Paso 3: Revisar los requisitos y la arquitectura

El agente genera requisitos y documentos de arquitectura para que los revise. Compruebe que los requisitos coinciden con las respuestas proporcionadas y que la arquitectura cubre lo siguiente:

- Cuatro acciones web: `reviews-get`, `reviews-post`, `qa-get`, `qa-post`
- Persistencia usando `aio-lib-state` con claves que se ajustan al patrón permitido (`[a-zA-Z0-9-_.]` — sin dos puntos)
- Valores de estado almacenados como cadenas JSON (no como objetos sin procesar ni matrices)
- Paquete independiente: código compartido (utilidades, constantes) dentro del paquete `product-reviews`, no a través de `../../` rutas que escapan del paquete

>[!NOTE]
>
>Los agentes de IA son no deterministas y sus comportamientos difieren según el modelo y el IDE. Puede obtener un conjunto diferente de preguntas que producen un conjunto diferente de requisitos y arquitectura. Si es así, intente dirigir el agente en la dirección tal que la implementación coincida estrechamente con lo que se presenta en este tutorial antes de continuar.

### Paso 4: Selección de un plan de implementación

El agente le da la opción de crear un plan de implementación detallado o de completar una implementación directa.

- Si desea un plan revisable que se pueda ejecutar por fases con más control, seleccione la primera opción.
- Si desea que el agente realice la implementación completa con una intervención mínima, seleccione la segunda opción.

### Paso 5: Implementación de la extensión

Una vez que el agente haya completado la implementación, implemente la extensión:

```bash
aio app deploy
```

Si el agente agregó `require-adobe-auth: true` a las acciones, pídale que quite la autenticación para poder llamar a los extremos directamente desde la tienda:

```shell-session
Remove the requirement to provide a valid Adobe IMS access token from all product-reviews actions.
```

A continuación, vuelva a implementar:

```bash
aio app deploy
```

### Paso 6: Crear datos ficticios y rellenarlos previamente para realizar pruebas

Cree un archivo de datos ficticios y utilice curl para rellenar previamente la API y obtener contenido de revisión de muestra y preguntas y respuestas para probarlo en la CLI y en la tienda.

1. Cree un archivo `docs/mock-product-reviews-data.json` (o similar) con datos de ejemplo. Por ejemplo:

   ```json
   {
     "reviews": [
       { "sku": "ADB153", "rating": 5, "review": "Great product, highly recommend!", "user": "shopper@example.com" },
       { "sku": "ADB153", "rating": 4, "review": "Good value for money.", "user": "buyer@example.com" }
     ],
     "questions": [
       { "sku": "ADB153", "type": "question", "content": "Does this come in other colors?", "user": "curious@example.com" }
     ]
   }
   ```

1. Utilice curl para PUBLICAR los datos en la API implementada.

   Reemplace `<your-runtime-url>` con su URL de tiempo de ejecución de App Builder (por ejemplo, `https://1172492-prodreviewqa135-stage.adobeioruntime.net`):

   ```bash
   API_URL="https://<your-runtime-url>/api/v1/web/product-reviews"
   
   # Submit reviews
   curl -s -X POST "$API_URL/reviews-post" \
     -H "Content-Type: application/json" \
     -d '{"sku":"ADB153","rating":5,"review":"Great product, highly recommend!","user":"shopper@example.com"}'
   
   curl -s -X POST "$API_URL/reviews-post" \
     -H "Content-Type: application/json" \
     -d '{"sku":"ADB153","rating":4,"review":"Good value for money.","user":"buyer@example.com"}'
   
   # Submit a question (save the returned id for the answer)
   curl -s -X POST "$API_URL/qa-post" \
     -H "Content-Type: application/json" \
     -d '{"sku":"ADB153","type":"question","content":"Does this come in other colors?","user":"curious@example.com"}'
   
   # Submit an answer (replace <QUESTION-UUID> with the id from the question response)
   curl -s -X POST "$API_URL/qa-post" \
     -H "Content-Type: application/json" \
     -d '{"sku":"ADB153","type":"answer","questionId":"<QUESTION-UUID>","content":"Yes, it comes in blue and red.","user":"seller@example.com"}'
   ```

1. Compruebe los datos con solicitudes de GET:

   ```bash
   curl -s "$API_URL/reviews-get?sku=ADB153"
   curl -s "$API_URL/qa-get?sku=ADB153"
   ```

>[!TIP]
>
>Use el SKU `ADB153` para un producto que tenga contenido de reseñas y preguntas y respuestas, y `ADB152` para un producto sin reseñas. Esta configuración de datos permite probar estados rellenados y vacíos en la tienda.

### Paso 7: Prueba de la extensión

Pida al agente que proporcione los pasos de prueba o utilice los ejemplos de curl del paso anterior. Los siguientes ejemplos muestran comandos de prueba típicos.

**Enviar una revisión:**

```bash
API_URL="https://<your-runtime-url>/api/v1/web/product-reviews"
curl -s -X POST "$API_URL/reviews-post" \
  -H "Content-Type: application/json" \
  -d '{"sku":"ADB153","rating":5,"review":"Excellent!","user":"test@example.com"}'
```

**Enumerar críticas:**

```bash
curl -s "$API_URL/reviews-get?sku=ADB153"
```

**Enviar una pregunta:**

```bash
curl -s -X POST "$API_URL/qa-post" \
  -H "Content-Type: application/json" \
  -d '{"sku":"ADB153","type":"question","content":"Is this dishwasher safe?","user":"test@example.com"}'
```

**Enviar una respuesta** (usar `id` de la respuesta a la pregunta como `questionId`):

```bash
curl -s -X POST "$API_URL/qa-post" \
  -H "Content-Type: application/json" \
  -d '{"sku":"ADB153","type":"answer","questionId":"<QUESTION-UUID>","content":"Yes, it is.","user":"support@example.com"}'
```

### Creación del contrato de servicio

Ahora que la implementación del servicio ha finalizado, pídale al agente que cree un contrato de servicio para el trabajo de la tienda:

```shell-session
Create a service contract for the Product Review and Q&A application that defines the API endpoints, request and response formats, and any necessary data models. Ensure that the service contract is clear and detailed enough for a frontend developer to implement the storefront integration without needing to ask additional questions about the API. Name this file PRODUCT_REVIEW_QA_CONTRACT.md
```

Copie este archivo en su proyecto de tienda para que el agente de tienda pueda hacer referencia a él.

## Conectar con la tienda

Esta sección lo guiará a través de la implementación de la parte de tienda de las revisiones de productos y la extensión de preguntas y respuestas mediante [!DNL Edge Delivery Services] y las herramientas de desarrollo asistido por IA. Agregue un bloque de revisión de producto al PDP que muestre el contenido de revisión y preguntas y respuestas, y permita a los compradores enviar contenido nuevo.

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
- El archivo `PRODUCT_REVIEW_QA_CONTRACT.md` se copió en el proyecto de tienda

### Paso 1: Validar el entorno

Abra el archivo `config.json` y compruebe que los valores de `commerce-core-endpoint` y `commerce-endpoint` apuntan al extremo de GraphQL [!DNL Adobe Commerce as a Cloud Service].

```json
"commerce-core-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
"commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
```

### Paso 2: Proporcione la solicitud inicial

Con el contrato de servicio ya en el proyecto, solicite al agente que implemente el bloque de revisión del producto. Utilice el modo **Plan** si está disponible en su agente, para evitar que el agente continúe sin un plan.

```shell-session
Analyze @PRODUCT_REVIEW_QA_CONTRACT.md and build a product review block using the API specified in the contract. The block displays both reviews and Q&A content on the product detail page, with forms for shoppers to submit reviews, questions, and answers. Use the project manager skill to plan this implementation.
```

>[!TIP]
>
>Solicitud específica para utilizar los déclencheur de aptitudes del administrador de proyectos en el flujo de trabajo por fases que le ayuda a dirigir la implementación. Esto garantiza que las suposiciones clave y los requisitos que faltan se identifiquen al principio del proceso.

### Paso 3: Responder preguntas aclaratorias

El agente regresa con una serie de preguntas que debe responder antes de que pueda comenzar a formar una solución. El siguiente ejemplo muestra preguntas y respuestas típicas. Su agente puede hacer diferentes preguntas, pero los temas generalmente son los mismos.

**Ejemplo de preguntas del agente:**

1. **URL base de API** — ¿Cómo debería obtener la tienda la URL base de API de revisiones de productos? Las opciones pueden incluir un bloque de configuración (por ejemplo, una tabla con `apiBaseUrl`), marcadores de posición globales u otro método.
1. **Origen del SKU**: ¿el bloque debe leer el SKU desde el contexto de PDP (producto actual) o desde la configuración de bloque?
1. **Comportamiento del formulario**: después de un envío correcto, ¿debe ocultarse el formulario, mostrar un mensaje de éxito o permanecer visible pero deshabilitado?

**Respuestas de ejemplo:**

```shell-session
1. Block table config with apiBaseUrl (required). Each block instance can point to its own deployment.
2. From block table if set; otherwise use getProductSku() so it works on PDP without authoring a SKU.
3. Show a success message above the form; keep the form visible but disabled.
```

>[!NOTE]
>
>Reemplace el marcador de posición en la configuración del bloque por la dirección URL de tiempo de ejecución de App Builder (por ejemplo, `https://1172492-prodreviewqa135-stage.adobeioruntime.net`).
>
>Su agente puede hacer diferentes preguntas. Utilice estas respuestas como guía:
>
>- La dirección URL base de la API debe proceder de la tabla de bloques para que se pueda cambiar sin realizar modificaciones en el código.
>- SKU de la tabla de bloques si está establecida; de lo contrario, del producto actual en la PDP.
>- Después de un envío correcto, mostrar un mensaje de éxito y deshabilitar el formulario.

### Paso 4: Revisar los requisitos y la arquitectura

El agente actualiza el documento de requisitos para que lo revise. Compruebe que:

- El bloque representa críticas (con clasificación, usuario, fecha, texto) y preguntas y respuestas (preguntas con respuestas anidadas).
- Forms se utiliza para enviar críticas, preguntas y respuestas.
- La paginación es compatible tanto para el contenido de revisión como para el de preguntas y respuestas.
- La integración de la API de utiliza la dirección URL base de la tabla de bloques.
- Los estados de éxito y error se gestionan según el contrato.

>[!NOTE]
>
>Los agentes de IA son no deterministas y sus comportamientos difieren según el modelo y el IDE. Puede obtener un conjunto diferente de preguntas que producen un conjunto diferente de requisitos y arquitectura. Si es así, intente dirigir el agente en la dirección tal que la implementación coincida estrechamente con lo que se presenta en este tutorial antes de continuar.

### Paso 5: Selección de un plan de implementación

El agente le da la opción de crear un plan de implementación detallado o de completar una implementación directa.

- Si desea un plan revisable que se pueda ejecutar por fases con más control, seleccione la primera opción.
- Si desea que el agente realice la implementación completa con una intervención mínima, seleccione la segunda opción.

Durante la implementación, el agente crea y modifica archivos de bloque. Observe el código que se está generando y haga preguntas o redirija el agente según sea necesario. Si el bloque no se procesa, pídale al agente que analice la decoración de la sección y el patrón de detección de bloques: el elemento de bloque debe ser un elemento secundario directo de la sección para que el marco de trabajo pueda encontrarlo.

### Paso 6: Añadir el bloque a la página de producto en la creación de documentos

Agregue el bloque de revisión de producto a la plantilla de página de producto para que aparezca en todos los PDP. Utilice el servicio Document Authoring (da.live) para añadir y configurar el bloque.

1. Abra el servicio de creación de documentos, por ejemplo [da.live](https://da.live/)

1. Haga clic en el espacio del proyecto, abra la carpeta **products** y seleccione **default** (`products/default`).

1. Agregue una nueva sección de bloque.

   En la tabla de bloques, agregue una fila con el nombre de bloque **product-review** (o el nombre de bloque que creó su agente).

1. Configure el bloque con la configuración requerida:
   - **apiBaseUrl**: su URL de tiempo de ejecución de App Builder (por ejemplo, `https://<namespace>-<app-name>-stage.adobeioruntime.net`).
   - **sku**: déjelo vacío para usar el SKU del producto actual en el PDP o escriba un SKU específico para mostrar solo las críticas de ese producto.

1. Haga clic en **[!UICONTROL Publish]** para publicar los cambios.

### Paso 7: Inicio del servidor y prueba

Después de agregar el bloque a la página de producto en Document Authoring, inicie el servidor de desarrollo y pruebe el bloque.

1. Inicie el servidor de desarrollo local:

   ```bash
   npm run start
   ```

1. En un explorador, vaya a una página de producto que tenga revisiones rellenadas previamente y contenido de preguntas y respuestas. Por ejemplo:

   ```shell-session
   http://localhost:3000/products/<product-slug>/ADB153
   ```

1. Compruebe que el bloque de revisión del producto muestra revisiones y contenido de preguntas y respuestas, y que los formularios de envío funcionan.

Puede realizar pruebas manuales o pedir al agente que utilice sus capacidades de explorador para realizar pruebas:

```shell-session
Run complete browser testing. Use the following product page 'http://localhost:3000/products/<product-slug>/ADB153'
```

### Paso 8: Limpieza

Después de omitir o completar la prueba, el agente le pedirá que continúe con la fase final de **Limpieza**. Tras la confirmación, el agente archiva todos los artefactos de documentación creados durante la implementación.

## Resolución de problemas

Utilice las siguientes sugerencias si encuentra problemas durante el tutorial.

### Servidor (App Builder)

| Síntoma | Causa | Fix |
|---------|-------|-----|
| GET o POST devuelven 500 &quot;No se encuentra el módulo&quot; | Las acciones de revisiones de productos utilizan `require("../../utils")` o `require("../../constants")`, que escapan del paquete de paquetes. Estos archivos no se incluyen cuando se implementa el paquete. | Haga que el paquete de revisiones de productos sea independiente. Agregue `actions/product-reviews/lib/constants.js` y `actions/product-reviews/lib/utils.js`, y actualice las cuatro acciones para requerir de `../lib/...` en lugar de `../../`. |
| GET devuelve 500 con &quot;la clave debe coincidir con el patrón&quot; | Las claves de estado utilizan dos puntos (por ejemplo, `reviews:ADB153`). `aio-lib-state` solo permite `[a-zA-Z0-9-_.]`. | Cambie los prefijos de `reviews:` y `qa:` a `reviews.` y `qa.`. Agregue un asistente de `stateKey(prefix, sku)` que limpie el SKU (reemplace los caracteres no válidos por `_`). |
| POST devuelve 500 con &quot;el valor debe ser una cadena&quot; | `aio-lib-state` solo acepta valores de cadena. El código pasa matrices u objetos a `state.put()`. | Serialice con `JSON.stringify()` al escribir y `JSON.parse()` al leer. Actualice las cuatro acciones. |

{style="table-layout:auto"}

### Tienda (Edge Delivery Services)

| Síntoma | Causa | Fix |
|---------|-------|-----|
| El bloque no se procesa en la página de prueba | El elemento de bloque está anidado dentro de un elemento `div` adicional, por lo que después de `decorateSections` el selector de bloque (`div.section > div > div`) no coincide. | Convierta el bloque en un elemento secundario directo de la sección. Estructura: `section > div.product-review` (o clase de bloque equivalente). Evite `section > div > div.product-review`. |
| Tokens CSS no válidos | El bloque utiliza tokens de diseño que no existen en `styles/styles.css` (por ejemplo, `--color-error-100`, `--type-detail-font-size`). | Pida al agente que valide los tokens con los `styles/styles.css` del proyecto y reemplace los tokens no válidos por los existentes (por ejemplo, `--color-alert-*`, `--type-details-caption-*`). |

{style="table-layout:auto"}

## Resumen del tutorial

A continuación se muestra un resumen de los temas tratados en este tutorial:

- **Desarrollo de extensiones:** Describe la funcionalidad para crear y ver contenido de reseñas de productos y preguntas y respuestas en una tienda con un servidor de Adobe Commerce as a Cloud Service en un agente de IA y cómo implementar esta funcionalidad generando una API de REST que funcione con cuatro extremos usando [!DNL App Builder].
- **Persistencia:** con `aio-lib-state` con formato de clave correcto y valores serializados en JSON.
- **Datos ficticios y rellenado previo:** Creación de un archivo de datos ficticios y uso de curl para rellenar previamente la API para las pruebas de CLI y de tienda.
- **Contratos de servicio:** Creación de contratos de API que vinculan extensiones backend e implementaciones de tienda.
- **Integración de tienda por fases:** Trabajando con los requisitos, la arquitectura y la implementación con habilidades asistidas por IA.
- **Bloque de PDP:** Agregar un bloque de revisión de producto al PDP que muestra revisiones y preguntas y respuestas con formularios de envío y paginación.

## Pasos siguientes

Utilice las siguientes sugerencias para ampliar el servicio de revisiones de productos:

- **Agregar moderación:** Implemente un flujo de trabajo de moderación para el contenido de revisión y preguntas y respuestas antes de que se publique.
- **Añadir autenticación:** Requiere que los compradores inicien sesión para enviar críticas o contenido de preguntas y respuestas, y asociar envíos con cuentas de clientes.
- **Agregar una página de administración de suscripciones:** Cree una página de tienda donde los compradores puedan ver y editar sus críticas.
- **Admitir implementaciones de varios inquilinos:** Amplíe la administración de estado para admitir varios inquilinos de Commerce en una sola aplicación de App Builder.
- **Agregar limitación de velocidad:** Implemente límites de velocidad en la API para evitar abusos.
