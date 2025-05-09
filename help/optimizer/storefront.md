---
title: Configurar tu tienda
description: Aprenda a configurar su  [!DNL Adobe Commerce Optimizer] tienda.
role: Developer
exl-id: 2b4c9e98-a30c-4a33-b356-556de5bd721a
source-git-commit: f1aa8439d6322e5278ab787f5cd096e16b7813a2
workflow-type: tm+mt
source-wordcount: '2150'
ht-degree: 0%

---

# Configurar tu tienda

>[!NOTE]
>
>Esta documentación describe un producto en desarrollo de acceso anticipado y no refleja todas las funcionalidades pensadas para una disponibilidad general.

Este tutorial muestra cómo configurar y usar [Adobe Commerce Storefront con tecnología Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/?lang=es) para crear una tienda Commerce segura, escalable y de rendimiento con tecnología de datos de tu instancia de [!DNL Adobe Commerce Optimizer].


## Requisitos previos

* Asegúrese de que tiene una cuenta de GitHub (github.com) que puede crear repositorios y que está configurada para el desarrollo local.

* Obtenga información acerca de los conceptos y el flujo de trabajo para desarrollar tiendas Commerce en Adobe Edge Delivery Services revisando la [Información general](https://experienceleague.adobe.com/developer/commerce/storefront/get-started?lang=es) en la documentación de Adobe Commerce Storefront.
* Configurar el entorno de desarrollo


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
>Este proceso de configuración de tienda se usa para [!DNL Adobe Commerce Optimizer] con Adobe Commerce Edge Delivery Service Storefront. Hay recursos adicionales disponibles para ampliar y personalizar su solución [!DNL Adobe Commerce Optimizer] mediante [App Builder para Adobe Commerce](https://experienceleague.adobe.com/es/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder) y [API Mesh para Adobe Developer App Builder](https://experienceleague.adobe.com/es/docs/commerce-learn/tutorials/adobe-developer-app-builder/api-mesh/getting-started-api-mesh). Para obtener información de acceso y uso, póngase en contacto con el representante de su cuenta de Adobe.

#### Instalación de Sidekick

Instale la extensión del explorador Sidekick para editar, previsualizar y publicar contenido en la tienda. Ver [instrucciones de instalación de Sidekick](https://www.aem.live/docs/sidekick#installation).


## Crear tu tienda

La tienda que crees para tu proyecto [!DNL Adobe Commerce Optimizer] usa una versión personalizada de la plantilla de Adobe Commerce en Edge Delivery Services Storefront. Las plantillas son un conjunto de archivos y carpetas que proporcionan un punto de partida para el desarrollo de tiendas. Este proceso de configuración es diferente al proceso de configuración estándar para una tienda [Adobe Commerce en Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/?lang=es).

>[!NOTE]
>
>Este tutorial utiliza macOS, Chrome y Visual Studio Code como entorno de desarrollo. Las capturas de pantalla y las instrucciones reflejan esa configuración. Puede utilizar un sistema operativo, un explorador y un editor de código diferentes, pero la interfaz de usuario que ve y los pasos que sigue varían en consecuencia.

### Resumen de flujo de trabajo

Siga estos pasos para configurar una tienda para usarla con [!DNL Adobe Commerce Optimizer].

1. **[Crear una carpeta de contenido](#step-1-create-a-content-folder)**: crea una carpeta de contenido compartido en Google Drive o Sharepoint. Esta carpeta contiene el contenido de muestra y los recursos de la tienda.

1. **[Crear un repositorio de código](#step-2-create-a-code-repository)**: cree un repositorio de GitHub a partir de la plantilla de plantillas de plantillas de Adobe Commerce + Edge Delivery Services. Incluir todas las ramas del repositorio de origen.
1. **[Actualice la plantilla de plantilla de tienda](#step-3-update-the-storefront-boilerplate)**-Actualice la plantilla de plantilla personalizada en la rama `aco` para conectar la carpeta de contenido a la tienda.
1. **[Cargue el código de repetidor de tienda actualizado](#step-4-upload-the-updated-boilerplate-code)**: sobrescriba el código de la rama `main` con el código actualizado de la rama `aco`.
1. **[Agregar la aplicación CodeSync](#step-5-add-the-aem-code-sync-app)**: conecte el repositorio al servicio Edge Delivery. No conecte la aplicación de sincronización de código hasta que haya completado la personalización del código fuente y esté listo para insertar el código en la rama `main`.
1. **[Previsualizar y publicar tu contenido](#step-6-preview-and-publish-your-content)**: utiliza la extensión de Sidekick para previsualizar y publicar el contenido del sitio desde la carpeta de contenido en la tienda.
1. **[Previsualice el sitio y vea datos de ejemplo](#step-7-preview-your-site)**: conéctese al sitio de la tienda para ver el contenido y los datos de ejemplo de la instancia de demostración [!DNL Adobe Commerce Optimizer].
1. **[Desarrolle la tienda en su entorno local](#step-8-develop-the-storefront-in-your-local-environment)**-Instale las dependencias requeridas. Inicie el servidor de desarrollo local y actualice la configuración de la tienda para conectarse a la instancia de [!DNL Adobe Commerce Optimizer] que Adobe le proporcionó.
1. **[Pasos siguientes](#next-steps)**: obtenga más información sobre cómo administrar y mostrar contenido y datos en la tienda.

### Paso 1: Crear una carpeta de contenido

Siga las instrucciones de la documentación de Adobe Commerce Storefront para agregar una carpeta de contenido compartido en Google Drive o Sharepoint y agregar el contenido de ejemplo. El contenido de ejemplo incluye imágenes, texto y otros recursos que conforman el sitio.

* [Crear y compartir una carpeta de Google Drive o Sharepoint](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/?lang=es#create-and-share-folder)
* [Cargue el contenido de muestra](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/?lang=es#add-sample-content) en su carpeta.

### Paso 2: Crear un repositorio de código

Cree un repositorio de código de plantillas de tienda en GitHub con la plantilla de plantillas de Edge Delivery Services + Adobe Commerce.

1. Inicie sesión en su cuenta de GitHub.

1. Vaya al repositorio de GitHub [aem-boilerplate-commerce](https://github.com/hlxsites/aem-boilerplate-commerce).

1. Seleccione **Usar esta plantilla** y, a continuación, seleccione **Crear un nuevo repositorio** en el menú desplegable.

   ![[!DNL Create github repo from storefront boilerplate template]](./assets/storefront-create-github-repo.png){width="700" zoomable="yes"}

   Se muestra la página de configuración del repositorio.

   ![[!DNL Configure github repo to pull all branches from boilerplate repo]](./assets/storefront-configure-github-repo.png){width="700" zoomable="yes"}

1. Complete el formulario de configuración con los siguientes detalles:

   * **Plantilla de repositorio**—`hlxsites/aem-boilerplate-commerce` (predeterminada).
   * **Incluir todas las ramas**: seleccione la opción para incluir todas las ramas.
   * **Propietario**: su organización o cuenta (obligatorio).
   * **Nombre del repositorio**: Un nombre único para su nuevo repositorio (obligatorio).
   * **Descripción**: Una breve descripción de su repositorio (opcional).
   * **Público o privado**: Adobe recomienda público (predeterminado).

1. Seleccione **Crear repositorio**.

   Después de varios minutos, se abre el nuevo repositorio.

   Omita las notificaciones de solicitudes de extracción que se muestren en la interfaz de usuario de GitHub.

### Paso 3: Actualizar la plantilla de la tienda

Necesita la siguiente información para actualizar el código de plantillas de tienda:

* **URL del repositorio de GitHub del paso 2**— `github.com/{ORG}/{SITE}`

   * `{ORG}` es el nombre de organización o de usuario para el repositorio

   * `{SITE}` es su nombre de repositorio

* **URL de carpeta de contenido del paso 1**— `https://drive.google.com/drive/folders/{YOUR_FOLDER_ID}`

  `{YOUR_FOLDER_ID}` es el identificador de la carpeta que creó con los datos de contenido de ejemplo.

#### Actualice el código de las plantillas para conectarse a la carpeta de contenido

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

   1. Abra el archivo de configuración [fstab.yaml](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/?lang=es#vocabulary).

      ```json
      mountpoints:
       /: {YOUR_MOUNTPOINT_URL}
      
      folders:
       /products/: /products/default
      ```

   1. Reemplace `{YOUR_MOUNTPOINT_URL}` por la URL de su carpeta de contenido.

      Por ejemplo, si utiliza Google Drive, el código actualizado debería tener este aspecto.

      ```json
       mountpoints:
        /: https://drive.google.com/drive/folders/1HXPWdQT-EK09IxVQV5HBSHN4QCA1a56Y
      ```

   1. Guarde el archivo.

#### Revise la configuración de la conexión de datos

La configuración de la conexión de datos establece la comunicación entre la tienda y la instancia de [!DNL Adobe Commerce Optimizer] especificada. Esta conexión permite que los datos del catálogo fluyan a la tienda y rellenen varias interfaces de tienda, incluidas las páginas de componentes de búsqueda, listas de productos y detalles del producto.

Para la configuración inicial de la tienda, se conecta a la instancia predeterminada [!DNL Adobe Commerce Optimizer] con datos de ejemplo.

```json
{
  "public": {
    "default": {
      "commerce-core-endpoint": "https://www.aemshop.net/graphql",
      "commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/Fwus6kdpvYCmeEdcCX7PZg/graphql",
      "headers": {
        "cs": {
          "ac-channel-id": "9ced53d7-35a6-40c5-830e-8288c00985ad",
          "ac-environment-id": "Fwus6kdpvYCmeEdcCX7PZg",
          "ac-price-book-id": "west_coast_inc",
          "ac-scope-locale": "en-US"
        }
      },
      "analytics": {
        "base-currency-code": "USD",
        "environment": "Production",
        "store-id": 1,
        "store-name": "ACO Demo",
        "store-url": "https://www.aemshop.net",
        "store-view-id": 1,
        "store-view-name": "Default Store View",
        "website-id": 1,
        "website-name": "Main Website"
      }
    }
  }
}
```

En este archivo, los siguientes valores de clave especifican la instancia de [!DNL Adobe Commerce Optimizer] a la que conectarse y determinan los datos que fluyen a la tienda:

* `commerce-endpoint` especifica la instancia a la que se va a conectar. Se ha configurado para utilizar la instancia predeterminada [!DNL Adobe Commerce Optimizer]. Este extremo se utiliza para recuperar datos de catálogo.
* `ac-environment-id` es el identificador de inquilino de la instancia [!DNL Adobe Commerce Optimizer].
* `headers` determinar los datos que fluyen de la instancia a la tienda.
   * `ac-channel-id` se ha establecido en `west_coast_inc`
   * `ac-price-book-id` se ha establecido en `west_coast_inc`
   * `ac-scope-locale` se ha establecido en `en-US`
   * `ac-price-book-id` se ha establecido en `west_coast_inc`

Estos valores establecen el ID de canal, la configuración regional y el ID del libro de precios para enviar datos de catálogo a un canal de ventas específico y filtrar esos datos en función de la configuración regional y los valores del libro de precios especificados. Posteriormente, actualice el extremo para conectarse a la instancia [!DNL Adobe Commerce Optimizer] que Adobe ha aprovisionado para usted y reemplace los valores del encabezado para recuperar los datos de esa instancia.

#### Configuración de la extensión de Sidekick

Añada la configuración del proyecto para la extensión de Sidekick. Esta configuración garantiza que Sidekick esté disponible para administrar el contenido del proyecto de tienda.

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

   * Reemplace la cadena `{ORG}` por la organización o el nombre de usuario de su repositorio.

   * Reemplazar la cadena `{SITE}` por el nombre del repositorio

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

   +++

1. Guarde el archivo.

### Paso 4: cargar el código de plantillas actualizado

Para usar el código de plantilla de tienda personalizado, sobrescriba el código de la rama `main` con sus actualizaciones.

1. Desde el editor o IDE, confirme y guarde los archivos actualizados.

   ```bash
   git add .
   ```

1. Compruebe que está confirmando los dos archivos actualizados.

   ```bash
   git status
   On branch aco
   Your branch is up to date with 'origin/aco'.
   
   Changes to be committed:
    (use "git restore --staged <file>..." to unstage)
        new file:   fstab1.yaml
        modified:   tools/sidekick/config.json
   ```

1. Confirme los cambios en la rama `aco`.

   ```bash
   git commit -m "Update storefront boilerplate for Adobe Commerce Optimizer"
   ```

1. Sobrescribir la plantilla de la rama `main` con los cambios en la rama `aco`.

   ```bash
   git push origin aco:main -f
   ```

### Paso 5: Añadir la aplicación de sincronización de código de AEM

Conecte el repositorio al servicio de Edge Delivery agregando la aplicación GitHub de sincronización de código de AEM a su repositorio.

>[!IMPORTANT]
>
>No conecte la aplicación de sincronización de código hasta que haya cargado el código de plantillas actualizado en la rama principal del repositorio de GitHub.

1. Abra la página de configuración [aplicación AEM Code Sync](https://github.com/apps/aem-code-sync).

1. Seleccione **Configurar** y luego realice la autenticación con la **organización** o la **cuenta** que contiene el repositorio que creó.

1. En el formulario, elija **Seleccionar solo repositorios** y seleccione el repositorio que creó.

1. Seleccione **Instalar** para agregar la aplicación AEM Code Sync a su repositorio.

   Debería ver un mensaje que indique que la aplicación se ha instalado correctamente.

### Paso 6: Previsualizar y publicar el contenido

Para añadir contenido a la tienda, previsualiza y publica el contenido de la tienda con la extensión Sidekick.

1. En Google Drive o Sharepoint, abra la carpeta de contenido.

1. Para activar Sidekick, haga clic en el icono Sidekick de la barra de herramientas del explorador.

   ![[!DNL Turn on Sidekick from browser toolbar]](./assets/storefront-enable-sidekick-toolbar.png){width="700" zoomable="yes"}

   Si no ve el icono de Sidekick, compruebe que el archivo de configuración de Sidekick, `tools/Sidekick/config.json` en la rama `main` del repositorio de GitHub, esté [configurado correctamente](#configure-the-sidekick-extension).

1. Utilice la barra de herramientas de Sidekick para obtener una vista previa y publicar el contenido.

   ![[Seleccionar archivos para previsualizar y publicar]](./assets/storefront-content-preview-publish.png){width="700" zoomable="yes"}

   Seleccione los archivos de cada carpeta por separado y utilice la barra de herramientas de Sidekick para previsualizar y publicar todos los archivos.

   * **Vista previa**: carga contenido en el entorno de ensayo. Las direcciones URL de ensayo de tienda terminan con `.aem.page`.

   * **Publicar**: carga contenido en el entorno de producción. Las direcciones URL de producción finalizan con `aem.live`.

Para obtener más información, consulte la documentación de Adobe Experience Manager [Sidekick](https://www.aem.live/docs/sidekick).

### Paso 7: Previsualizar el sitio

Compruebe que el contenido de la muestra y los datos de la instancia de demostración de Adobe Commerce Optimizer se muestran correctamente.

* **El contenido de muestra** se suministra desde su carpeta de contenido compartido. Incluye los diseños de página, los titulares y otro contenido que ha publicado con Sidekick.
* **Los datos de muestra** se han obtenido desde la instancia de demostración [!DNL Adobe Commerce Optimizer]. Los datos incluyen datos de productos con atributos de productos, imágenes, descripciones de productos y precios rellenados según los valores de encabezado especificados en el archivo de configuración de tienda, `config.json`.


#### Conéctese al sitio para ver contenido y datos de ejemplo

1. Para conectarse al sitio, vaya a `https://main--{SITE}--{ORG}.aem.live`.

   Reemplace `{ORG}` y `{SITE}` por la organización y el nombre de su repositorio de plantillas.

   ![[!DNL ACO storefront site with boilerplate]](./assets/aco-storefront-site-boilerplate.png){width="700" zoomable="yes"}

   Si la página devuelve un error 404, asegúrese de que ha publicado el contenido con la extensión de Sidekick. Además, compruebe que el punto de montaje del archivo `fstab.yaml` actualizado apunte a la carpeta de contenido que creó.

1. Vea los datos de catálogo de muestra procedentes de la instancia predeterminada de Commerce Optimizer.

   1. Busque `tires` para ver una lista desplegable de productos de neumáticos disponibles.

   ![[!DNL Discover Adobe Commerce Optimizer products]](./assets/storefront-site-with-aco-data.png){width="700" zoomable="yes"}

   El componente de búsqueda forma parte del código de plantillas de tienda. Los datos de los resultados de búsqueda se rellenan según la configuración de la tienda en `config.json`.

   1. Pulse **Intro** para ver la página de la lista de productos.

      ![[!DNL View product details page]](./assets/storefront-with-aco-pdp-page.png){width="675" zoomable="yes"}

   1. Ver una página de detalles del producto seleccionando cualquier producto de neumático en la página.

      Si explora la tienda, verá que algunos de los componentes no funcionan. Por ejemplo, al agregar un producto al carro de compras, se devuelve un error y los componentes de administración de cuentas no funcionan. Estos problemas se producen porque estos componentes no se han configurado para recibir datos de un servidor de Commerce. Los datos de la instancia [!DNL Adobe Commerce Optimizer] rellenan únicamente las páginas de componentes de búsqueda, lista de productos y detalles de productos.

   1. Después de explorar la tienda, continúe con el tutorial.


### Paso 8: desarrollar la tienda en su entorno local

En esta sección, se actualiza la configuración de la tienda desde el entorno de desarrollo local.

* Actualice la configuración de la tienda para conectarse al extremo de GraphQL para la instancia [!DNL Adobe Commerce Optimizer] que Adobe ha aprovisionado para usted.
* Actualice los valores del encabezado para recuperar datos de la instancia.

#### Iniciar desarrollo local

1. En su IDE, compruebe la rama principal del repositorio de código de GitHub.

   ```bash
   git checkout main
   ```

1. Instale las dependencias necesarias.

   ```bash
   npm install
   ```

1. Inicie el servidor de desarrollo local.

   ```bash
   npm start
   ```

   La primera página de la tienda de plantillas debe estar visible en el explorador en `http://localhost:3000`.

![[!DNL Configure github repo to pull all branches from boilerplate repo]](./assets/aco-storefront-local-dev-env.png){width="700" zoomable="yes"}


#### Actualizar la configuración de la tienda

Actualice el archivo de configuración de la tienda y previsualice los cambios en el entorno de desarrollo local.


1. En su IDE, actualice la configuración de la tienda para conectarse a la instancia de [!DNL Adobe Commerce Optimizer] que Adobe ha aprovisionado para usted.

   1. Abra el archivo `config.json`.

   1. Actualice los siguientes valores mediante el extremo de la instancia [!DNL Adobe Commerce Optimizer]:

      * **`commerce-endpoint`**: reemplace el valor existente por su dirección URL de extremo.

        ```json
        "commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/{tenantId}/graphql"
        ```

      * **`ac-environment-id`**: reemplace el valor existente por el ID de inquilino de la dirección URL de extremo.

        ```json
        "ac-environment-id": "{tenantId}"
        ```

   1. Guarde el archivo.

      Si la vista previa local funciona correctamente, las actualizaciones se aplican a la tienda local.

1. Compruebe el sitio para ver los resultados del cambio de configuración.

   1. En el explorador, vaya a `http://localhost:3000` y actualice la página.

   1. En el encabezado de la tienda, haga clic en la lupa para buscar `tires`.

      ![Buscar neumáticos](./assets/storefront-header-empty-search-list.png){width="675" zoomable="yes"}

      Tenga en cuenta que la lista desplegable no se rellena.

   1. Pulse **Intro** para mostrar la página de la lista de productos.

      ![Resultados de búsqueda vacíos con valores de encabezado no válidos](./assets/storefront-configuration-with-incorrect-headers.png){width="675" zoomable="yes"}

      La búsqueda no devuelve ningún resultado porque los valores del encabezado del archivo de configuración de la tienda se basan en la instancia predeterminada. Ahora que la configuración apunta a la instancia [!DNL Adobe Commerce Optimizer] aprovisionada por usted, esos valores no son válidos.

### Pasos siguientes

Consulte el [caso de uso de extremo a extremo del administrador de tiendas y catálogos](./use-case/admin-use-case.md) para obtener más información sobre cómo administrar y mostrar contenido y datos en la tienda.

>[!MORELIKETHIS]
>
>* [Documentación de la tienda Adobe Experience Manager](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=es) para obtener más información sobre cómo actualizar el contenido del sitio e integrarlo con los componentes de front-end y los datos del back-end de Commerce.
></br></br>
>* [Documentación de Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=es) para obtener más información sobre la actualización del contenido del sitio y la integración con componentes de front-end y datos de back-end de Adobe Commerce.
