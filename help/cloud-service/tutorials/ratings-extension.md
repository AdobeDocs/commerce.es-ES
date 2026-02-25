---
title: Tutorial de extensión de clasificaciones
description: Obtenga información sobre cómo crear una extensión de clasificaciones de productos para Adobe Commerce as a Cloud Service mediante App Builder y las herramientas de desarrollo asistido por IA.
feature: App Builder, Cloud
role: Developer
level: Intermediate
source-git-commit: fb3595284761e9478c819150c27d06631de67e18
workflow-type: tm+mt
source-wordcount: '603'
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

1. Si se ha añadido documentación al contexto del cursor, desactívela:

   - Vaya a [!UICONTROL **Cursor**] > [!UICONTROL **Configuración**] > [!UICONTROL **Configuración del cursor**] > [!UICONTROL **Indexación y documentos**] y elimine cualquier documentación enumerada.

   ![Indexación de cursor y configuración de documentos con lista de documentación vacía](../assets/disable-documentation.png){width="600" zoomable="yes"}

1. Genere un código para una extensión de clasificación de productos:
   - En la ventana de conversación Cursor, seleccione el modo [!UICONTROL **Agente**].
   - Introduzca la siguiente solicitud:

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

### Pruebas locales

1. Pida al agente que le ayude a probar el código localmente.

   ```shell-session
   Test the ratings API locally on a dev server using cURL.
   ```

1. Siga las instrucciones del agente y confirme que la API funciona localmente.

   ![Instrucciones del agente de IA para pruebas de API locales](../assets/local-testing.png){width="600" zoomable="yes"}

   ![El terminal muestra resultados correctos de prueba de API local con cURL](../assets/local-testing-1.png){width="600" zoomable="yes"}

### Implementación de la extensión

1. Después de verificar el código generado, implemente la extensión mediante el siguiente mensaje:

   ```shell-session
   Deploy the ratings API.
   ```

   El agente realiza una evaluación de la preparación previa al despliegue antes de este.

   ![lista de comprobación de evaluación de preparación previa al despliegue del agente de IA](../assets/pre-deployment-assessment.png){width="600" zoomable="yes"}

1. Cuando confíe en los resultados de la evaluación, indique al agente que continúe con el despliegue.

   El agente utiliza el kit de herramientas de MCP para verificar, crear e implementar automáticamente.

   ![Proceso de implementación y compilación del kit de herramientas de MCP](../assets/deployment-process.png){width="600" zoomable="yes"}

### Posterior a la implementación

Puede probar la API antes de integrarla en la tienda. El agente debe proporcionar la ubicación de la nueva acción y una estrategia de prueba.

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
<!-- 
Return to the terminal and run the following command in the `extension` folder to copy the file to the `storefront` folder:

```bash
cp RATINGS_API_CONTRACT.md ../storefront
``` -->

### Pasos siguientes

Ahora que tiene el contrato de API de clasificación, puede empezar a crear la parte de tienda (front-end) de la extensión de clasificación.

<!-- 
## Connect to the storefront

This section teaches you how to implement real storefront features and communicate effectively with AI agents when working with [!DNL Adobe Commerce] dropins and [!DNL Edge Delivery Services].

>[!NOTE]
>
>The prompts provided are starting points. Although you can use them without modification, consider having a natural conversation with the agent.
>
>When working with AI-assisted development tools, there are always natural variations in the code and responses generated by the agent.
>
>If you encounter any issues with your code, ask the agent to help you debug it.

### Ratings stars and review count implementation

1. Navigate to the `storefront` folder:

   ```bash
   cd storefront
   ```

1. Open the storefront folder in a new Cursor window.

    Alternatively, if you have the [Cursor CLI](https://cursor.com/docs/configuration/shell#installing-cli-commands) installed, open the window by using the following command in your terminal:

   ```bash
   cursor .
   ```

1. Start the local development server:

   ```bash
   npm run start
   ```

1. In a browser, navigate to the Apparel page:

   ```shell-session
   http://localhost:3000/apparel
   ```

1. Observe the boilerplate storefront UI layout and note the lack of visual product ratings.

1. Use the following prompt with your agent:

   ```shell-session
   Implement product ratings in the storefront.

   Add a 5-star rating display with a review count underneath each product name on the product list page, product details page, and product recommendations.

   Use the dropin slot system where available.

   Use @RATINGS_API_CONTRACT.md to understand how to use the ratings API.
   ```

1. Observe the changes in the codebase, and watch the Apparel page for updates.

   You should see the following changes in your development environment and browser:

   * A product rating "component" is automatically created.
   * The component is integrated into product-details, product-list-page, and product-recommendations blocks using [dropin slots](https://experienceleague.adobe.com/developer/commerce/storefront/dropins/customize/slots).
   * Stars display with proper fill proportions based on mock rating values.

![Product Ratings Implementation](../assets/product-ratings-implementation.png){width="600" zoomable="yes"}

## Tutorial recap

Here is a summary of the topics covered in this tutorial:

* **Feature implementation**: How to describe new functionality to an AI agent.
* **Iterative changes**: Making quick modifications to existing code.
* **Complex UI components**: Building interactive features with visual references.
* **Dropin integration**: Working with [!DNL Adobe Commerce] dropin containers and slots.
* **Component reusability**: Creating shared components used across multiple blocks.

## Next steps

For further experimentation with this tutorial, use the following suggestions to further customize your ratings extension, or create your own modifications:

### Change the star colors

Use the following prompt to your agent:

```shell-session
Change the star fill color to red.
```

**Expected outcome:**

The stars are changed to red.

![Red Star Colors](../assets/red-star-colors.png){width="600" zoomable="yes"}

### Add rating distribution modal

The following steps show how the agent handles complex UI features with visual references.

1. **Before starting:** Save the following mock image and paste it into the chat with your storefront agent.

   ![Rating Distribution Mockup](../assets/rating-distribution-mockup.png){width="600" zoomable="yes"}

1. Follow these steps to create the ratings distribution modal using the reference image as a guide:

   * Update the API to return additional data representing the ratings distribution.
   * Update the API Contract.
   * Update the contact in the storefront codebase.
   * Ask the storefront agent to use the reference image and updated API Contract to add the ratings distribution to the PDP page.

1. Observe the following changes in the codebase, and watch the Apparel page for updates:

   * How the agent interprets the visual mockup
   * Whether it uses appropriate HTML structure for accessibility
   * How it handles the positioning and interaction states

#### Troubleshooting

* If the modal does not appear, check the browser console for errors.
* If positioning is off, ask the agent to fix it using the following format:

   ```shell-session
   adjust the modal position to be...
   ```

![Rating Distribution Modal](../assets/rating-distribution-modal.png){width="600" zoomable="yes"}
 -->
