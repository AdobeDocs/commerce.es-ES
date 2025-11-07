---
title: Tutorial de extensión de clasificaciones
description: Obtenga información sobre cómo crear una extensión de clasificaciones de productos para Adobe Commerce as a Cloud Service mediante App Builder y las herramientas de desarrollo asistido por IA.
role: Developer
hide: true
hidefromtoc: true
source-git-commit: 453b21f89d2024a8d6927fa082affdd5abb6e5cd
workflow-type: tm+mt
source-wordcount: '1337'
ht-degree: 0%

---

# Adobe Developers Live: libro de trabajo de Adobe Commerce lab

Este laboratorio lo guiará a través del proceso de creación de una extensión de clasificaciones de productos para [!DNL Adobe Commerce as a Cloud Service] mediante [!DNL Adobe App Builder] y las herramientas de desarrollo asistido por IA.

## Comprobar requisitos previos

Compruebe que están instalados los siguientes requisitos previos:

```bash
# Check Node.js version (should be 22.x.x)
node --version

# Check npm version (should be 9.0.0 or higher)
npm --version

# Check Git
git --version

# Check Bash
bash --version
```

## Inicie sesión en Adobe Developer Console

1. Vaya a [Adobe Developer Console](https://developer.adobe.com/console){target="_blank"}.
1. Si ya iniciaste sesión, haz clic en el icono de tu perfil en la esquina superior derecha y luego haz clic en el botón **Cerrar sesión**.
1. Inicie sesión con el ID de correo electrónico y la contraseña de laboratorio proporcionados para su puesto.
1. Si se le pide que agregue una dirección de correo electrónico o un número de teléfono secundarios, haga clic en **No ahora**.
1. Cuando se le pida que seleccione un perfil de organización, seleccione **Adobe Commerce Labs**.

   ![select-organization](./assets/select-org.png){width="600" zoomable="yes"}

1. Si se le pide que acepte los términos y condiciones, haga clic en el vínculo para leer los términos y, a continuación, haga clic en **Aceptar y continuar**.

   ![aceptar-términos](./assets/accept-terms.png){width="600" zoomable="yes"}

## Ejecutar el script de configuración

Si los [requisitos previos](#verify-prerequisites) están instalados y ha iniciado sesión en Adobe Developer Console, descargue y ejecute el script de instalación. También puede configurar manualmente el script siguiendo los [requisitos previos de laboratorio](workbook-prerequisites.md) pasos.

1. Clone el repositorio que contiene el script de configuración:

   ```bash
   git clone https://github.com/adobe-commerce/commerce-adl-2025.git
   ```

   >[!NOTE]
   >
   >Si el script falla, consulte [requisitos previos](workbook-prerequisites.md) y continúe donde el script encontró un error.

1. Vaya al repositorio:

   ```bash
   cd commerce-adl-2025
   ```

1. Ejecute el script de configuración:

   ```bash
   bash adl-setup.sh
   ```

   Mientras se ejecuta el script, se le pedirá que introduzca su nombre de usuario y contraseña, que se proporcionarán durante el laboratorio. Su nombre de usuario reflejará su ubicación y número de asiento. Por ejemplo, si se encuentra en San José, CA, puesto 123, su nombre de usuario será `sjc-adl-123@adobeeventlab.com`.

   Además, debe seleccionar el proyecto que corresponda al número de puesto y al espacio de trabajo **stage**. El nombre de su proyecto reflejará su ubicación y número de puesto. Por ejemplo, si se encuentra en San José, CA, puesto 123, el nombre del proyecto será `SJC ADL 123`.

## Desarrollo de extensiones

Esta sección le guía a través del proceso de desarrollo de una extensión de clasificación para Adobe Commerce as a Cloud Service mediante herramientas de desarrollo asistido por IA.

### Instalación de herramientas de IA de extensibilidad

Configure las herramientas de desarrollo asistido por IA en la carpeta `extension`:

```bash
cd extension
```

```bash
aio commerce extensibility tools-setup
```

![Instalar herramientas de IA](./assets/install-ai-tools.png){width="600" zoomable="yes"}

### Abrir cursor

>[!NOTE]
>
>Al trabajar con herramientas de desarrollo asistido por IA, habrá variaciones naturales en el código y las respuestas generadas por el agente.
>Si tiene algún problema con el código, siempre puede pedir al agente que le ayude a depurarlo.

Abra la aplicación [!DNL Cursor] y vaya a la carpeta `extension` o, si tiene instalado [Cursor CLI](https://cursor.com/docs/configuration/shell#installing-cli-commands), introduzca el siguiente comando en el terminal:

```bash
cursor .
```

![Abrir cursor](./assets/open-cursor.png){width="600" zoomable="yes"}

En este momento, todas las reglas de [!DNL Cursor] están instaladas en la carpeta `.cursor/rules`. Puede encontrar herramientas de MCP en **Configuración de MCP** en [!DNL Cursor]. Compruebe que el conjunto de herramientas `commerce-extensibility` esté habilitado sin errores. Si hay errores, active o desactive el conjunto de herramientas.

![Configuración del cursor](./assets/cursor-settings.png){width="600" zoomable="yes"}

Si se ha añadido documentación al contexto del cursor, se debe desactivar. Vaya a [!UICONTROL **Cursor**] > [!UICONTROL **Configuración**] > [!UICONTROL **Configuración del cursor**] > [!UICONTROL **Indexación y documentos**] y elimine cualquier documentación enumerada.

![Deshabilitar documentación](./assets/disable-documentation.png){width="600" zoomable="yes"}

### Generación de código

En esta sección se muestra cómo utilizar herramientas asistidas por IA para generar código para una extensión de clasificación de productos.

#### Definición de requisitos

Implementará una extensión que sirve clasificaciones de productos como API. La extensión [!DNL App Builder] responde con detalles de clasificación para un SKU determinado.

**Mensaje inicial:**

Utilice la siguiente solicitud en [!DNL Cursor]:

1. Abra la ventana de conversación en Cursor.
1. Seleccione el modo **Agente**.
1. Introduzca la siguiente solicitud:

   ```text
   Implement an Adobe Commerce as a Cloud Service extension to handle Product Ratings.
   Implement a REST API to handle GET ratings requests.
   GET requests will have to support the following query parameters:
   
   sku -> product SKU
   ```

1. Si el agente solicita buscar en la documentación, permita.

![Escriba el mensaje en el cursor](./assets/enter-prompt.png){width="600" zoomable="yes"}

El agente investiga los requisitos y hace preguntas aclaratorias. Responda las preguntas del agente con precisión para ayudarle a generar el mejor código.

![El agente hace preguntas que aclaran](./assets/agent-questions.png){width="600" zoomable="yes"}

**Mensaje de respuesta:**

Utilice la siguiente respuesta para responder a las preguntas del agente:

```text
Yes, this headless extension is for Adobe Commerce as a Cloud Service storefront,
but we do not need any authentication for the GET API because guest users should be able to use it on the storefront.
This extension will be called directly from the storefront,
no async invocation, such as events or webhooks, is required.
Let's start with just the GET API for now,
we will implement other CRUD operations at a later time.
We do not need a DB or storage mechanism right now,
just return random ratings data between 1 and 5 and a ratings count between 1 and 1000.
The API should only return the average rating for the product and the total number of ratings.
We do not need to add tests right now.
```

El agente crea un archivo de `requirements.md` que sirve como origen de la verdad para la implementación.

![Archivo de requisitos creado](./assets/requirements-file.png){width="600" zoomable="yes"}

#### Verifique los requisitos y planifique la arquitectura

1. Revise el archivo `requirements.md`.
1. Si todo parece correcto, indique al agente que pase a **Phase 2 - Architecture Planning**.
1. Revise el plan de arquitectura.
1. Indique al agente que continúe con la generación de código.

![Planificación de arquitectura](./assets/architecture-planning.png){width="600" zoomable="yes"}

#### Generar código

El agente genera el código necesario y proporciona un resumen detallado de los pasos siguientes.

![Resumen de generación de código](./assets/code-generation-summary.png){width="600" zoomable="yes"}

![Pasos siguientes](./assets/next-steps.png){width="600" zoomable="yes"}

### Pruebas locales

Pida al agente que le ayude a probar el código localmente.

```text
Test the ratings API locally on a dev server using cURL.
```

Siga las instrucciones del agente y confirme que la API funciona localmente.

![Pruebas locales](./assets/local-testing.png){width="600" zoomable="yes"}

![Resultados de pruebas locales](./assets/local-testing-1.png){width="600" zoomable="yes"}

### Implementación de la extensión

Después de comprobar el código generado, está listo para implementar la extensión mediante el siguiente mensaje:

```text
Deploy the ratings API.
```

#### Evaluación previa a la implementación

El agente realiza una evaluación de la preparación previa al despliegue antes de este.

![Evaluación previa a la implementación](./assets/pre-deployment-assessment.png){width="600" zoomable="yes"}

#### Implementar

Cuando confíe en los resultados de la evaluación, indique al agente que continúe con el despliegue. El agente utiliza el kit de herramientas de MCP para verificar, crear e implementar automáticamente.

![Implementación](./assets/deployment-process.png){width="600" zoomable="yes"}

### Prueba de la API

Puede probar la API antes de integrarla en la tienda.

El agente proporciona la ubicación de la nueva acción y una estrategia de prueba.

![Estrategia de prueba](./assets/testing-strategy.png){width="600" zoomable="yes"}

#### Realizar pruebas manualmente con cURL

Pruebe la API manualmente mediante cURL en un terminal:

```bash
curl -s "https://<your-site>.adobeioruntime.net/api/v1/web/ratings/ratings?sku=TEST-SKU-123"
```

![prueba cURL](./assets/curl-test.png){width="600" zoomable="yes"}

### Integración con Edge Delivery Services

Para integrar la API de clasificaciones con una tienda [!DNL Adobe Commerce] con tecnología [!DNL Edge Delivery Services], pídale al agente que cree un contrato de servicio con los requisitos para la API de clasificaciones:

```text
Create a service contract for the ratings api that I can pass on to the storefront agent. Name it RATINGS_API_CONTRACT.md
```

![Contrato de servicio](./assets/create-contract.png){width="600" zoomable="yes"}

![Detalles del contrato de servicio](./assets/contract.png){width="600" zoomable="yes"}

Vuelva al terminal y ejecute el siguiente comando en la carpeta `extension` para copiar el archivo en la carpeta `storefront`:

```bash
cp RATINGS_API_CONTRACT.md ../storefront
```

## Conectar con la tienda

Esta sección le ayudará a implementar características de tienda reales, mostrándole cómo comunicarse de manera efectiva con los agentes de IA al trabajar con [!DNL Adobe Commerce] listas desplegables y [!DNL Edge Delivery Services].

>[!NOTE]
>
>Las indicaciones proporcionadas son puntos de partida, debe sentirse libre de tener una conversación natural con el agente. Al trabajar con herramientas de desarrollo asistido por IA, habrá variaciones naturales en el código y las respuestas generadas por el agente.
>
>Si tiene algún problema con el código, siempre puede pedir al agente que le ayude a depurarlo.

### Implementar estrellas de clasificación y recuento de críticas

1. Vaya a la carpeta `storefront`:

   ```bash
   cd storefront
   ```

1. Abra la carpeta de la tienda en una nueva ventana Cursor. Si tiene instalado [CLI de cursor](https://cursor.com/docs/configuration/shell#installing-cli-commands), introduzca el siguiente comando en el terminal:

   ```bash
   cursor .
   ```

1. Inicie el servidor de desarrollo local:

   ```bash
   npm run start
   ```

1. En un explorador, vaya a la página Ropa:

   ```text
   http://localhost:3000/apparel
   ```

1. Observe el diseño de la interfaz de usuario de tienda de plantillas.

1. Utilice el siguiente mensaje con su agente:

   ```text
   Implement product ratings to the storefront.
   Add a 5-star rating display with a review count underneath each product name on the product list page, product details page, and product recommendations.
   Use the dropin slot system where available.
   
   Use the @RATINGS_API_CONTRACT.md to understand how to use the ratings api.
   ```

   >[!NOTE]
   >
   >Si se le pide que inicie el servidor de desarrollo local, informe al agente de que ya se está ejecutando.

1. Observe los cambios en la base del código y vea la página Ropa para ver las actualizaciones.

**Resultado esperado:**

* Se crea automáticamente un &quot;componente&quot; de clasificación de productos.
* El componente está integrado en los bloques de detalles del producto, lista de productos, página y recomendaciones de productos mediante Ranuras.
* Las estrellas se muestran con las proporciones de relleno adecuadas en función de los valores de clasificación de prueba.

![Implementación de clasificación de productos](./assets/product-ratings-implementation.png){width="600" zoomable="yes"}

### Cambiar los colores de las estrellas

Utilice el siguiente mensaje para informar a su agente:

```text
Change the star fill color to red.
```

**Resultado esperado:**

Las estrellas se cambian a rojo.

![Colores Estrella Rojos](./assets/red-star-colors.png){width="600" zoomable="yes"}

## Resumen de tienda

A lo largo de este tutorial, hemos tratado los siguientes temas:

* **Implementación de características**: Cómo describir la nueva funcionalidad a un agente de IA.
* **Cambios iterativos**: realizando modificaciones rápidas en el código existente.
* **Componentes complejos de la interfaz de usuario**: Generando características interactivas con referencias visuales.
* **Integración de Dropin**: Trabajando con [!DNL Adobe Commerce] contenedores y ranuras de Dropin.
* **Reutilización de componentes**: creando componentes compartidos usados en varios bloques.

## Pasos siguientes

Si el tiempo lo permite, puede personalizar aún más la extensión de clasificación añadiendo las siguientes funciones:

### Agregar modal de distribución de clasificación (opcional)

Los siguientes pasos muestran cómo gestiona el agente las funciones complejas de la interfaz de usuario con referencias visuales.

1. **Antes de comenzar:** Guarde la siguiente imagen ficticia y péguela en el chat con su agente de tienda.

   ![Máscara de distribución de clasificación](./assets/rating-distribution-mockup.png){width="600" zoomable="yes"}

1. Siga estos pasos para guiarle en la creación del modal de distribución de clasificaciones basado en la imagen de referencia:

   * Actualice la API para devolver datos adicionales que representen la distribución de clasificación.
   * Actualice el contrato de API.
   * Actualice el contacto en la base de código de la tienda.
   * Pida al agente de tienda que utilice la imagen de referencia y el contrato de API actualizado para añadir la distribución de clasificaciones a la página PDP.

1. Observe los siguientes cambios en la base de código y vea la página Ropa para ver las actualizaciones:

   * Cómo interpreta el agente la maqueta visual
   * Si utiliza la estructura de HTML adecuada para la accesibilidad
   * Cómo gestiona los estados de posicionamiento e interacción

**Solución de problemas:**

* Si el modal no aparece, compruebe si hay errores en la consola del explorador.
* Si el posicionamiento está desactivado, puede pedir al agente que:

  ```text
  adjust the modal position to be...
  ```

![Modal de distribución de clasificación](./assets/rating-distribution-modal.png){width="600" zoomable="yes"}
