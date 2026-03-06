---
title: Tutorial de extensión de clasificaciones
description: Obtenga información sobre cómo crear una extensión de clasificaciones de productos para Adobe Commerce as a Cloud Service mediante App Builder y las herramientas de desarrollo asistido por IA.
solution: Commerce
feature: App Builder, Cloud
feature-set: Commerce
role: Developer
level: Intermediate
type: Tutorial
source-git-commit: 33ba97fd6766c9d11baea74170a7119d72e06379
workflow-type: tm+mt
source-wordcount: '1701'
ht-degree: 0%

---

# Tutorial de extensión de clasificaciones

Este tutorial lo guiará a través del proceso de creación de una extensión de clasificaciones de productos para [!DNL Adobe Commerce as a Cloud Service] mediante [!DNL Adobe App Builder] y las herramientas de desarrollo asistido por IA.

Antes de empezar, complete [requisitos previos](./tutorial-prerequisites.md).

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

## Desarrollo de extensiones

Esta sección le guía a través del desarrollo de una extensión de clasificación para Adobe Commerce as a Cloud Service mediante herramientas de desarrollo asistido por IA.

1. Vaya a **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]** y compruebe que el conjunto de herramientas `commerce-extensibility` esté habilitado sin errores. Si hay errores, active o desactive el conjunto de herramientas.

   ![Configuración del IDE de cursor que muestra el conjunto de herramientas de extensibilidad comercial MCP habilitado](../assets/cursor-settings.png){width="600" zoomable="yes"}

   >[!NOTE]
   >
   >Cuando trabaje con herramientas de desarrollo asistido por IA, espere variaciones naturales en el código y las respuestas generadas por el agente.
   >Si tiene algún problema con el código, siempre puede pedir al agente que le ayude a depurarlo.

1. Deshabilite cualquier documentación en el contexto del cursor:

   * Vaya a **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Indexing & Docs]** y elimine cualquier documentación enumerada.

   ![Indexación de cursor y configuración de documentos con lista de documentación vacía](../assets/disable-documentation.png){width="600" zoomable="yes"}

1. Genere un código para una extensión de clasificación de productos:
   * En la ventana Cursor chat, seleccione el modo **[!UICONTROL Agent]**.
   * Introduzca la siguiente solicitud:

   ```shell-session
   Implement an Adobe Commerce as a Cloud Service extension to handle Product Ratings.
   
   Implement a REST API to handle GET ratings requests.
   
   GET requests will have to support the following query parameters:
   
   sku -> product SKU
   ```

   >[!NOTE]
   >
   >Si el agente solicita buscar en la documentación, permita.

1. Responda las preguntas del agente con precisión para ayudarle a generar el mejor código.

   ![Ventana de chat del cursor en el modo Agente con el mensaje de extensión ingresado](../assets/enter-prompt.png){width="600" zoomable="yes"}

   ![Agente de IA haciendo preguntas aclaratorias sobre los requisitos de extensión](../assets/agent-questions.png){width="600" zoomable="yes"}

1. Utilice el siguiente texto de ejemplo para responder a las preguntas del agente con el fin de configurar datos de clasificación aleatorios:

   ```shell-session
   Yes, this headless extension is for Adobe Commerce as a Cloud Service storefront,
   but we do not need any authentication for the GET API because guest users should be able to use it on the storefront.
   
   This extension is called directly from the storefront, no async invocation, such as events or webhooks, is required.
   
   Start with just the GET API for now, we will implement other CRUD operations at a later time.
   
   We do not need a DB or storage mechanism right now, just return random ratings data between 1 and 5 and a ratings count between 1 and 1000.
   
   The API should only return the average rating for the product and the total number of ratings.
   We do not need to add tests right now.
   ```

   El agente crea un archivo de `requirements.md` que sirve como origen de la verdad para la implementación.

   ![Archivo Requirements.md creado por un agente de IA con detalles de implementación](../assets/requirements-file.png){width="600" zoomable="yes"}

1. Revise el archivo `requirements.md` y compruebe el plan.

   Si todo parece correcto, indique al agente que pase a **Phase 2 - Architecture Planning**.

1. Revise el plan de arquitectura.

1. Indique al agente que continúe con la generación de código.

   El agente genera el código necesario y proporciona un resumen detallado de los pasos siguientes.

   ![Plan de arquitectura de fase 2 del agente de IA para la API de clasificaciones](../assets/architecture-planning.png){width="600" zoomable="yes"}

   ![Resumen de archivos y estructura de código generados](../assets/code-generation-summary.png){width="600" zoomable="yes"}

   ![Agente de IA que proporciona los siguientes pasos para la prueba y la implementación](../assets/next-steps.png){width="600" zoomable="yes"}

### Prueba de la extensión localmente

Los siguientes pasos explican cómo comprobar el funcionamiento de la extensión antes de implementarla.

1. Pida al agente que le ayude a probar el código localmente.

   ```shell-session
   Test the ratings API locally on a dev server using cURL.
   ```

1. Siga las instrucciones del agente y confirme que la API funciona localmente.

   ![Instrucciones del agente de IA para pruebas de API locales](../assets/local-testing.png){width="600" zoomable="yes"}

   ![El terminal muestra resultados correctos de prueba de API local con cURL](../assets/local-testing-1.png){width="600" zoomable="yes"}

### Implementación de la extensión

Despliegue la extensión en [!DNL Adobe I/O Runtime] mediante el agente.

1. Después de verificar el código generado, implemente la extensión mediante el siguiente mensaje:

   ```shell-session
   Deploy the ratings API.
   ```

   El agente realiza una evaluación de la preparación previa al despliegue antes de este.

   ![lista de comprobación de evaluación de preparación previa al despliegue del agente de IA](../assets/pre-deployment-assessment.png){width="600" zoomable="yes"}

1. Cuando confíe en los resultados de la evaluación, indique al agente que continúe con el despliegue.

   El agente utiliza el kit de herramientas de MCP para verificar, crear e implementar automáticamente.

   ![Proceso de implementación y compilación del kit de herramientas de MCP](../assets/deployment-process.png){width="600" zoomable="yes"}

### Verificar la implementación

Pruebe la API antes de integrarla en la tienda. El agente debe proporcionar la ubicación de la nueva acción y una estrategia de prueba.

![Estrategia de prueba del agente de IA con URL de acción implementada y comandos de prueba](../assets/testing-strategy.png){width="600" zoomable="yes"}

También puede probar la API manualmente utilizando cURL en un terminal:

```bash
curl -s "https://<your-site>.adobeioruntime.net/api/v1/web/ratings/ratings?sku=TEST-SKU-123"
```

![El terminal muestra una prueba de cURL correcta de la API de clasificaciones implementada](../assets/curl-test.png){width="600" zoomable="yes"}

### Integración con Edge Delivery Services

Para integrar la API de clasificaciones con una tienda [!DNL Adobe Commerce] con tecnología [!DNL Edge Delivery Services], pídale al agente que cree un contrato de servicio con los requisitos para la API de clasificaciones:

```shell-session
Create a service contract for the ratings api that I can pass on to the storefront agent. Name it RATINGS_API_CONTRACT.md
```

![Agente de IA creando archivo de contrato de servicio para integración de tienda](../assets/create-contract.png){width="600" zoomable="yes"}

![Clasificaciones del archivo de marcado de contrato de API con detalles de extremo y respuesta](../assets/contract.png){width="600" zoomable="yes"}

Vuelva al terminal y ejecute el siguiente comando en la carpeta `extension` para copiar el archivo de contrato en la carpeta `storefront`:

```bash
cp RATINGS_API_CONTRACT.md ../storefront
```

## Conectar con la tienda

Esta sección le guiará a través de la implementación de la parte de tienda de la extensión de clasificaciones mediante [!DNL Edge Delivery Services] y las herramientas de desarrollo asistido por IA.

>[!NOTE]
>
>Las indicaciones proporcionadas son puntos de partida. Aunque puede utilizarlas sin modificaciones, considere la posibilidad de mantener una conversación natural con el agente.
>
>Al trabajar con herramientas de desarrollo asistido por IA, siempre hay variaciones naturales en el código y las respuestas generadas por el agente.
>
>Si encuentra algún problema con su código, pídale al agente que le ayude a depurarlo.

### Requisitos previos de Storefront

Antes de iniciar la integración de tienda, comprueba que tienes lo siguiente:

* Un proyecto de tienda conectado a su instancia [!DNL Commerce]
* Herramientas de IA de tienda de Commerce [instaladas con CLI](./tutorial-prerequisites.md#install-the-storefront-ai-tools)

### Configurar el espacio de trabajo de la tienda

Prepare su entorno de tienda local para el desarrollo.

1. Vaya a la carpeta `storefront`:

   ```bash
   cd storefront
   ```

1. Abra la carpeta de la tienda en una nueva ventana Cursor.

   Alternativamente, si tiene instalado el [CLI de cursor](https://cursor.com/docs/configuration/shell#installing-cli-commands), abra la ventana usando el siguiente comando en su terminal:

   ```bash
   cursor .
   ```

1. Inicie el servidor de desarrollo local:

   ```bash
   npm run start
   ```

1. En un explorador, vaya a una página de producto:

   ```shell-session
   http://localhost:3000/products/llama-plush-shortie/adb336
   ```

1. Observe la página de detalles del producto (PDP) de la tienda de plantillas y observe la falta de clasificaciones visuales del producto.

### Integración de la API de clasificaciones

Utilice el agente para integrar la API de clasificaciones en la página de detalles del producto de la tienda.

1. Utilice el siguiente mensaje con su agente:

   ```shell-session
   Integrate the ratings API into the PDP to show star ratings and a review count for products. Here's the service contract: @RATINGS_API_CONTRACT.md
   ```

1. El agente evalúa la complejidad de la tarea e invoca un flujo de trabajo por fases. Durante la **fase 1 (recopilación de requisitos)**, el agente crea un documento de requisitos y hace preguntas que aclaran cuestiones como las siguientes:

   * ¿En qué punto del PDP deben aparecer las clasificaciones?
   * ¿Debería ser un nuevo bloque independiente o una personalización de ranura dentro del componente desplegable PDP existente?
   * ¿Cuál debería ser la reserva si la API no está disponible o no devuelve datos?
   * ¿Las clasificaciones también deben aparecer en el PLP (lista de productos) o solo en el PDP?
   * ¿Hay especificaciones de diseño o maquetas?

   Responda estas preguntas en función de los requisitos de su proyecto. El agente actualiza el documento de requisitos y marca la fase como completada.

1. Durante la **Fase 2 (Planificación arquitectónica)**, el agente investiga la documentación y el código base antes de proponer una arquitectura. Se espera que el agente:

   * Busque en la documentación de [!DNL Commerce] contenedores de PDP, ranuras y cargas útiles de eventos.
   * Analice el directorio `blocks` y la carpeta `scripts/initializers/` en busca de código relacionado con PDP existente.
   * Explore las definiciones de TypeScript para los contenedores disponibles y las formas de contexto de ranura.

   A continuación, el agente presenta opciones de arquitectura como:

   * **Opción A:** Personalice una ranura desplegable de PDP existente para insertar clasificaciones cerca del título del producto, un toque más ligero que sea fácil de actualizar.
   * **Opción B:** Cree un nuevo bloque `product-ratings` independiente que obtenga de la API de forma independiente, más flexible y desunido.
   * **Opción C:** Cree un nuevo bloque que también escuche eventos de PDP para el SKU del producto, un enfoque híbrido.

   El plan también incluye detalles sobre la integración de la API, consideraciones de rendimiento (carga diferida, almacenamiento en caché), seguridad (saneamiento de la entrada) y un enfoque de prueba.

   Revise el plan de arquitectura e indique al agente que continúe.

1. Durante la **Fase 3 (Enfoque de implementación)**, el agente le pedirá que elija entre:

   * **Opción A:** Revise un plan de implementación detallado antes de la generación de código (vea primero todos los archivos, patrones y estructura de código).
   * **Opción B:** Continúe directamente con la generación de código.

   Seleccione el método que prefiera.

1. Durante la **fase 4 (implementación)**, el agente genera código basado en la arquitectura elegida. Según el enfoque, el agente utiliza varias habilidades especializadas:

   * **Modelado de contenido:** Si se necesita un nuevo bloque, el agente diseña una estructura de contenido compatible con el autor, como una tabla de configuración con la dirección URL del extremo de API.
   * **Desarrollo de bloques:** El agente crea archivos de bloque siguiendo las convenciones de [!DNL Edge Delivery Services], incluidas las funciones decorativas de JavaScript, los estilos CSS con ámbito, las etiquetas ARIA para accesibilidad y la administración de estados de carga y error.
   * **Personalización de inclusión:** Si la arquitectura usa la personalización de ranura, el agente importa el contenedor correcto, usa una ranura verificada cerca del título del producto y se suscribe a los eventos de datos del producto para el SKU actual.

   Observe el código que se está generando y haga preguntas o redirija el agente según sea necesario. El agente produce un resumen de preparación para la producción cuando finaliza la generación de código.

1. Durante la **fase 4.5 (Pruebas)**, el agente ofrece probar la implementación. Si acepta, el agente:

   * Crea una página de prueba local con los scripts y estilos adecuados.
   * Inicia un servidor de desarrollo.
   * Ejecuta la verificación basada en el explorador para el procesamiento visual, la interactividad, el comportamiento interactivo, la accesibilidad y el rendimiento.
   * Genera un informe de prueba estructurado con los resultados.

   Siga los pasos del explorador para confirmar el comportamiento e informar de cualquier problema.

1. Observe los cambios en la base de código y observe la página de producto para ver las actualizaciones.

   Debería ver los siguientes cambios en su entorno de desarrollo y explorador:

   * Se crea automáticamente un componente de clasificación de productos.
   * El componente está integrado en el PDP mediante [ranuras de colocación](https://experienceleague.adobe.com/developer/commerce/storefront/dropins/customize/slots) o como bloque independiente, según la arquitectura elegida.
   * Las estrellas se muestran con las proporciones de relleno adecuadas en función de los valores de clasificación de la API.

   ![Página de detalles del producto que muestra las clasificaciones en estrellas integradas debajo del título del producto](../assets/product-ratings-implementation.png){width="600" zoomable="yes"}

## Resumen del tutorial

A continuación se muestra un resumen de los temas tratados en este tutorial:

* **Desarrollo de extensiones:** Aprenda a describir la nueva funcionalidad a un agente de IA y a generar una API de REST en funcionamiento mediante [!DNL App Builder].
* **Pruebas e implementación locales:** Prueba de la API localmente e implementación mediante el kit de herramientas de MCP.
* **Contratos de servicio:** Creación de contratos de API que vinculan extensiones backend e implementaciones de tienda.
* **Integración de tienda por fases:** Trabajando con los requisitos, la arquitectura y la implementación con habilidades asistidas por IA.
* **Integración de inclusión:** Uso de [!DNL Adobe Commerce] contenedores y ranuras de inclusión.
* **Reutilización de componentes:** Creación de componentes compartidos usados en varios bloques.

## Pasos siguientes

Utilice las siguientes sugerencias para personalizar la extensión de clasificación o crear sus propias modificaciones:

### Cambiar los colores de las estrellas

Utilice el siguiente mensaje con su agente:

```shell-session
Change the star fill color to red.
```

**Resultado esperado:**

Las estrellas cambian a rojo.

![Clasificaciones de productos mostradas con el color de relleno de estrella rojo](../assets/red-star-colors.png){width="600" zoomable="yes"}

### Agregar un modal de distribución de clasificación

Los siguientes pasos muestran cómo gestiona el agente las funciones complejas de la interfaz de usuario con referencias visuales.

1. **Antes de comenzar:** Guarde la siguiente imagen ficticia y péguela en el chat con su agente de tienda.

   ![Resumen que muestra el desglose de distribución de clasificación por nivel de estrella](../assets/rating-distribution-mockup.png){width="600" zoomable="yes"}

1. Siga estos pasos para crear el modal de distribución de clasificaciones utilizando la imagen de referencia como guía:

   * Actualice la API para devolver datos adicionales que representen la distribución de clasificación.
   * Actualice el contrato de API.
   * Actualice el contrato en la base de código de la tienda.
   * Pida al agente de tienda que utilice la imagen de referencia y el contrato de API actualizado para añadir la distribución de clasificaciones a la página PDP.

1. Observe los siguientes cambios en la base de código y observe la página de producto para ver las actualizaciones:

   * Cómo interpreta el agente la maqueta visual
   * Si utiliza la estructura de HTML adecuada para la accesibilidad
   * Cómo gestiona los estados de posicionamiento e interacción

#### Solucionar problemas del modal de distribución

Si el modal no se comporta como se espera, intente lo siguiente:

* Si el modal no aparece, compruebe si hay errores en la consola del explorador.
* Si el posicionamiento está desactivado, pídale al agente que lo arregle con el siguiente formato:

  ```shell-session
  adjust the modal position to be...
  ```

![Modal que muestra la distribución de clasificación detallada con barras de desglose de nivel de estrella](../assets/rating-distribution-modal.png){width="600" zoomable="yes"}
