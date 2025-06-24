---
title: Configurar tu tienda
description: Aprenda a configurar su  [!DNL Adobe Commerce Optimizer] tienda.
role: Developer
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
source-git-commit: 3131cc27a25d1bf958071b973f1d4bf1a68be152
workflow-type: tm+mt
source-wordcount: '923'
ht-degree: 0%

---

# Configurar tu tienda

Este tutorial muestra cómo configurar y usar [Adobe Commerce Storefront con tecnología Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/) para crear una tienda Commerce segura, escalable y de rendimiento con tecnología de datos de tu instancia de [!DNL Adobe Commerce Optimizer].


## Requisitos previos

- Asegúrese de que tiene una cuenta de GitHub (github.com) que puede crear repositorios y que está configurada para el desarrollo local.

- Obtenga información acerca de los conceptos y el flujo de trabajo para desarrollar tiendas Commerce en Adobe Edge Delivery Services revisando la [Información general](https://experienceleague.adobe.com/developer/commerce/storefront/get-started) en la documentación de Adobe Commerce Storefront.
- Configurar el entorno de desarrollo


### Configurar el entorno de desarrollo

Instale Node.js y la extensión del explorador Sidekick necesaria para desarrollar y probar la tienda [!DNL Adobe Commerce Optimizer] en Edge Delivery Services.

#### Instalar Node.js

Instale el administrador de versiones de nodos (NVM) y la versión requerida de Node.js (22.13.1 LTS).

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

1. Compruebe la instalación.

   ```bash
   npm -v
   ```

>[!TIP]
>
>Hay recursos adicionales disponibles para ampliar y personalizar su solución [!DNL Adobe Commerce Optimizer] mediante [App Builder para Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder) y [API Mesh para Adobe Developer App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/api-mesh/getting-started-api-mesh). Para obtener información de acceso y uso, póngase en contacto con el representante de su cuenta de Adobe.

#### Instalación de Sidekick

Instale la extensión del explorador Sidekick para editar, previsualizar y publicar contenido en la tienda. Ver [instrucciones de instalación de Sidekick](https://www.aem.live/docs/sidekick#installation).

## Crear tu tienda

La tienda que crees para tu proyecto [!DNL Adobe Commerce Optimizer] usa una versión personalizada de la plantilla de Adobe Commerce en Edge Delivery Services Storefront. Las plantillas son un conjunto de archivos y carpetas que proporcionan un punto de partida para el desarrollo de tiendas. Este proceso de configuración es diferente al proceso de configuración estándar para una tienda [Adobe Commerce en Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/).

>[!NOTE]
>
>Este tutorial utiliza macOS, Chrome y Visual Studio Code como entorno de desarrollo. Las capturas de pantalla y las instrucciones reflejan esa configuración. Puede utilizar un sistema operativo, un explorador y un editor de código diferentes, pero la interfaz de usuario que ve y los pasos que sigue varían en consecuencia.

### Resumen de flujo de trabajo

Siga estos pasos para configurar una tienda para usarla con [!DNL Adobe Commerce Optimizer].

1. **[Crear un repositorio de código](#step-1-create-site-code-repository)**: cree un repositorio de GitHub a partir de la plantilla de plantillas de plantillas de Adobe Commerce + Edge Delivery Services. Incluir todas las ramas del repositorio de origen.
1. **[Actualice la plantilla de plantilla de tienda](#step-2-update-the-storefront-boilerplate)**-Actualice la plantilla de plantilla personalizada en la rama `aco` para conectar la carpeta de contenido a la tienda.
1. **[Implementar cambios](#step-3-deploy-changes)**: sobrescriba el código de la rama `main` con el código actualizado de la rama `aco`.
1. **[Agregar la aplicación CodeSync](#step-5-add-the-aem-code-sync-app)**: conecte el repositorio al servicio Edge Delivery. No conecte la aplicación de sincronización de código hasta que haya completado la personalización del código fuente y haya insertado el código en la rama `main`.
1. **[Agregar contenido](#step-6-add-content)**: use la herramienta de clonación de contenido de demostración para crear e inicializar el contenido de la tienda en el entorno de Document Author alojado en `https://da.live`.
1. **[Vista previa del sitio de demostración](#step-7-preview-demo-site)**: conéctese al sitio de la tienda para ver el contenido y los datos de ejemplo de la instancia de demostración [!DNL Adobe Commerce Optimizer].
1. **[Desarrolle en su entorno local](#step-8-develop-in-your-local-environment)**-Instale las dependencias requeridas. Inicie el servidor de desarrollo local y actualice la configuración de la tienda para conectarse a la instancia de [!DNL Adobe Commerce Optimizer] que Adobe le proporcionó.
1. **[Pasos siguientes](#next-steps)**: obtenga más información sobre cómo administrar y mostrar contenido y datos en la tienda.


### Paso 1: Crear repositorio de código de sitio

Cree un repositorio de GitHub para el código de plantillas de sitio de su tienda con la plantilla de plantillas de Edge Delivery Services + Adobe Commerce.

1. Inicie sesión en su cuenta de GitHub.

1. Vaya al repositorio de GitHub [aem-boilerplate-commerce](https://github.com/hlxsites/aem-boilerplate-commerce).

1. Seleccione **Usar esta plantilla** y, a continuación, seleccione **Crear un nuevo repositorio** en el menú desplegable.

   ![[!DNL Create github repo from storefront boilerplate template]](./assets/storefront-create-github-repo.png){width="700" zoomable="yes"}

   Se muestra la página de configuración del repositorio.

   ![[!DNL Configure github repo to pull all branches from boilerplate repo]](./assets/storefront-configure-github-repo.png){width="700" zoomable="yes"}

1. Complete el formulario de configuración con los siguientes detalles:

   - **Plantilla de repositorio**—`hlxsites/aem-boilerplate-commerce` (predeterminada).
   - **Incluir todas las ramas**: seleccione la opción para incluir todas las ramas.
   - **Propietario**: su organización o cuenta (obligatorio).
   - **Nombre del repositorio**: Un nombre único para su nuevo repositorio (obligatorio).
   - **Descripción**: Una breve descripción de su repositorio (opcional).
   - **Público o privado**: Adobe recomienda público (predeterminado).

1. Seleccione **Crear repositorio**.

   Después de varios minutos, se abre el nuevo repositorio.

   Omita las notificaciones de solicitudes de extracción que se muestren en la interfaz de usuario de GitHub.

### Paso 2: Actualizar la plantilla de la tienda

Necesita la siguiente información para actualizar el código de plantillas de tienda:

- **URL del repositorio de GitHub del paso 2**— `github.com/{ORG}/{SITE}`
   - `{ORG}` es el nombre de organización o de usuario para el repositorio
   - `{SITE}` es su nombre de repositorio
- **URL de carpeta de contenido del paso 1**— `https://drive.google.com/drive/folders/{YOUR_FOLDER_ID}`
   - `{YOUR_FOLDER_ID}` es el identificador de la carpeta que creó con los datos de contenido de ejemplo.

#### Vincule el repositorio al entorno de Document Author

1. Clone el repositorio en el equipo local.

   ```bash
   git clone https://github.com/{ORG}/{SITE}.git
   ```

   Si encuentra errores al clonar el repositorio, consulte [Solucionar errores de clonación](https://docs.github.com/en/repositories/creating-and-managing-repositories/troubleshooting-cloning-errors) en la documentación de GitHub.

1. Abra el repositorio en su terminal o IDE.

1. Consulte la rama `aco`

   ```bash
   git checkout aco
   ```

1. Cree su archivo de configuración copiando el archivo `default-fstab.yaml` en `fstab.yaml`.

   ```bash
   cp default-fstab.yaml fstab.yaml
   ```

1. Actualice el punto de montaje en el archivo de configuración de la tienda para que apunte a la dirección URL de contenido.

   1. Abra el archivo de configuración [fstab.yaml](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/#vocabulary).

      ```yaml
      mountpoints:
        /:
          url: https://content.da.live/{org}/{site}/
          type: markup
      
      folders:
       /products/: /products/default
      ```

   1. Reemplace las cadenas `{ORG}` y `{SITE}` por los valores del repositorio de GitHub que creó para su código de plantillas.

      Por ejemplo, el código actualizado debería tener este aspecto.

      ```yaml
      mountpoints:
        /:
          url: https://content.da.live/owner-name/aco-storefront/
          type: markup
      ```

   1. Guarde el archivo.

#### Configuración de la extensión de Sidekick

1. Añada la configuración del proyecto para la extensión de Sidekick. Esta configuración garantiza que Sidekick esté disponible para administrar el contenido del proyecto de tienda.

>[!NOTE]
>
>Asegúrese de que ha instalado la [extensión de Sidekick](https://www.aem.live/docs/sidekick#installation) en su explorador.

1. Abra el archivo `tools/sidekick/config.json`.

   +++Archivo de configuración Sidekick

   ```json
   {
     "project": "Boilerplate",
     "plugins": [
       {
         "id": "cif",
         "title": "Commerce",
         "environments": [
           "edit"
         ],
         "url": "https://main--{SITE}--{ORG}.aem.live/tools/picker/dist/index.html",
         "isPalette": true,
         "paletteRect": "top: 54px; left: 5px; bottom: 5px; width: 300px; height: calc(100% - 59px); border-radius: var(--hlx-sk-button-border-radius); overflow: hidden; resize: horizontal;"
       },
       {
         "id": "personalisation",
         "title": "Personalisation",
         "environments": [
           "edit"
         ],
         "url": "https://main--{SITE}--{ORG}.aem.live/tools/segments/dist/index.html",
         "isPalette": true,
         "paletteRect": "top: 54px; left: 5px; bottom: 5px; width: 300px; height: calc(100% - 59px); border-radius: var(--hlx-sk-button-border-radius); overflow: hidden; resize: horizontal;"
       }
     ]
   }
   ```

   Consulte la [documentación de la biblioteca Sidekick](https://www.aem.live/docs/sidekick-library) para obtener más información.

   +++

1. Actualice los valores de clave `url` con los valores del repositorio de GitHub.

   - Reemplace la cadena `{ORG}` por la organización o el nombre de usuario de su repositorio.

   - Reemplazar la cadena `{SITE}` por el nombre del repositorio

   +++Ejemplo de archivo de configuración actualizado

   Si el nombre del repositorio de GitHub es `aco-storefront` y la organización es `early-adopter`, la URL actualizada debería tener el aspecto siguiente:

   ```json
   {
     "project": "Boilerplate",
     "plugins": [
       {
         "id": "cif",
         "title": "Commerce",
         "environments": [
           "edit"
         ],
         "url": "https://main--aco-storefront--early-adopter.aem.live/tools/picker/dist/index.html",
         "isPalette": true,
         "paletteRect": "top: 54px; left: 5px; bottom: 5px; width: 300px; height: calc(100% - 59px); border-radius: var(--hlx-sk-button-border-radius); overflow: hidden; resize: horizontal;"
       },
       {
         "id": "personalisation",
         "title": "Personalisation",
         "environments": [
           "edit"
         ],
         "url": "https://main--aco-storefront--early-adopter.aem.live/tools/segments/dist/index.html",
         "isPalette": true,
         "paletteRect": "top: 54px; left: 5px; bottom: 5px; width: 300px; height: calc(100% - 59px); border-radius: var(--hlx-sk-button-border-radius); overflow: hidden; resize: horizontal;"
       }
     ]
   }
   ```
