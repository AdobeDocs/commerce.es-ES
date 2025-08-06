---
title: Configurar tu tienda
description: Aprenda a ejecutar la herramienta de andamiaje para configurar su tienda  [!DNL Adobe Commerce as a Cloud Service] Storefront.
role: Developer
exl-id: 02928dc4-1777-483e-b0ee-b04fc813864d
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
source-git-commit: 47eb8ee55bb093767f76aa23df8bb347ee280aae
workflow-type: tm+mt
source-wordcount: '737'
ht-degree: 0%

---

# Configurar tu tienda

Los siguientes pasos muestran cómo configurar rápidamente su tienda de Adobe Commerce con tecnología Edge Delivery mediante el comando `aio commerce init`. Este proceso configura lo siguiente:

* [Tienda Commerce con tecnología Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/): Una tienda con rendimiento, escalable y segura que usa Edge Delivery Services de Adobe.
* [Mesh de API para Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/mesh/): una plataforma de API que permite a los desarrolladores combinar varias fuentes de datos en un único extremo de GraphQL. API Mesh organiza la API de terceros con la API de Adobe a través de una sola puerta de enlace. Una consulta al único extremo de GraphQL puede devolver resultados de varios orígenes.
* [Adobe Developer Console](https://developer.adobe.com/developer-console/docs/guides/): una colección de herramientas para desarrolladores con acceso a API, eventos, funciones de tiempo de ejecución y complementos que puede usar para generar proyectos para aplicaciones de Adobe.
* [Adobe I/O Runtime](https://developer.adobe.com/runtime/docs/): un motor sin servidor para implementar código personalizado que responde a eventos y ejecuta funciones en la nube.

## Requisitos previos

Antes de ejecutar el comando `aio commerce init`, debe completar los siguientes requisitos previos:

1. Instale el administrador de versiones de nodos (NVM).

   ```bash
   curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash
   ```

1. Instale Node.js y NPM. Para obtener más información, consulte [Node.js](https://nodejs.org/en/).

   ```bash
   nvm install 22
   ```

   ```bash
   npm install -g npm
   ```

1. Instale [Adobe I/O Runtime CLI](https://developer.adobe.com/runtime/docs/guides/tools/cli_install/).

   ```bash
   npm install -g @adobe/aio-cli
   ```

1. Instale el complemento Adobe I/O API Mesh.

   ```bash
   aio plugins:install @adobe/aio-cli-plugin-api-mesh
   ```

1. Instale el complemento Adobe I/O Commerce.

   ```bash
   aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce
   ```

1. Actualice los complementos existentes.

   ```bash
   aio plugins:update
   ```

1. Inicie sesión en su cuenta de Adobe Experience Cloud.

   ```bash
   aio login
   ```

   Si el comando `aio login` no inicia una ventana del explorador, consulte la sección [Solución de problemas](#troubleshooting).

1. Seleccione la organización de IMS, el proyecto y el espacio de trabajo. Use las teclas de dirección y presione **Intro** para realizar la selección. Para obtener más información sobre los comandos de `aio`, consulte la [documentación de CLI de Adobe I/O](https://github.com/adobe/aio-cli-plugin-console?tab=readme-ov-file#commands).

   ```bash
   aio console org select
   ```

   ```bash
   aio console project select
   ```

   ```bash
   aio console workspace select
   ```

1. Si aún no lo ha hecho, acepte las Condiciones de uso del desarrollador en la consola de Adobe Developer. Para ello, vaya a https://developer.adobe.com/console/home, haga clic en **Aceptar y continuar**.

## Ejecutar el comando `aio commerce init`

Al ejecutar el siguiente comando, se creará un andamiaje para la tienda de Commerce. Este andamiaje es un buen punto de partida para crear y comprender tu tienda. Para obtener más información sobre cómo trabajar con la tienda, consulte la [documentación de Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/).


1. Ejecute el comando `init`:

   ```bash
   aio commerce init
   ```

1. Si ya inició sesión en GitHub, ingrese `Y` para crear el repositorio con su nombre de usuario.

1. Introduzca el nombre del repositorio que desea crear.

1. Seleccione una de las siguientes opciones:

   * **Usar el inquilino de demostración de Adobe Commerce**: use un inquilino de demostración.
      * Si selecciona esta opción, se le pedirá que instale el bot de sincronización de código de AEM en una ventana del explorador. Debe especificar el repositorio que ha creado y autorizar el bot. Vuelva a la CLI e introduzca `y` para confirmar la instalación del bot de sincronización de código de AEM.
   * **Elegir un inquilino de Adobe Commerce disponible**: seleccione un inquilino de Commerce existente en la organización seleccionada.
      * Si selecciona esta opción, debe seleccionar el proyecto y el espacio de trabajo en los que desea crear una malla.
   * **Proporcione su propia URL de API de inquilino de Adobe Commerce**. Seleccione esta opción si participa en el programa de acceso de prueba. Introduzca la URL de API proporcionada en el correo electrónico de incorporación de Adobe.

   >[!NOTE]
   >
   >Si selecciona la opción `Pick an available API (Mesh -> SaaS)`, debe tener un proyecto y un Workspace existentes en Adobe Developer Console. [Al crear un proyecto con plantilla](https://developer.adobe.com/developer-console/docs/guides/projects/projects-template/) y seleccionar App Builder, se crearán automáticamente los espacios de trabajo necesarios.

1. Una vez completado el proceso, puede personalizar la tienda mediante los siguientes métodos:

   * Personalice su código: `https://github.com/<username or org>/<repo name>`
   * Edite el contenido: `https://da.live/#/<username or org>/<repo name>`
   * Administrar su configuración: `https://da.live/sheet#/<username or org>/<repo name>/configs-stage`
   * Vista previa de tu tienda: `https://main--<repo name>--<username or org>.aem.page/`
   * Ejecutar localmente: `aio commerce:dev`

Para personalizar tu tienda, consulta la [documentación de Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/).

## Resolución de problemas

Si tiene problemas con el comando `aio login`, Adobe recomienda cerrar la sesión por completo de CLI y del explorador y volver a iniciarla.

1. Para cerrar la sesión de la CLI, ejecute lo siguiente:

   ```bash
   aio logout
   ```

1. En el explorador, ve a [Adobe Developer Console](https://developer.adobe.com/console), haz clic en el icono de tu perfil en la esquina superior derecha y selecciona **Cerrar sesión**.

1. Vuelva a la CLI y ejecute de nuevo el comando `aio login`, que debería iniciar una ventana del explorador para iniciar sesión. A continuación, puede seleccionar su organización, proyecto y espacio de trabajo.

   ```bash
   aio console org select
   ```

   ```bash
   aio console workspace select
   ```

   ```bash
   aio console project select
   ```

## Pasos siguientes

Consulte los siguientes artículos para obtener más información:

* Para obtener más información sobre cómo administrar y mostrar contenido y datos en la tienda, consulta [actualizar contenido de la tienda](./use-cases.md#update-storefront-content).
* Para obtener más información sobre las características de experimentación contextual, vea [experimentación contextual](./use-cases.md#contextual-experimentation).
* Para obtener más información sobre el uso de la IA generativa para automatizar la generación de contenido de alta calidad, consulte [Generar variaciones](./use-cases.md#generate-variations).
* Para obtener más información sobre cómo actualizar el contenido del sitio e integrar con componentes de front-end y datos de back-end de Commerce, consulte la [documentación de Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/).
