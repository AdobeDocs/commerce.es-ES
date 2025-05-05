---
title: Configurar tu tienda
description: Aprenda a configurar su  [!DNL Adobe Commerce Optimizer] tienda.
role: Developer
source-git-commit: 425c801a852de566120504563e256b0351df588e
workflow-type: tm+mt
source-wordcount: '2287'
ht-degree: 0%

---

# Configurar tu tienda

>[!NOTE]
>
>Esta documentación describe un producto en desarrollo de acceso anticipado y no refleja todos los funcionalidad destinados a la disponibilidad general.

Este tutorial muestra cómo configurar y usar [Adobe Systems Commerce Storefront con tecnología de Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/) para crear un escaparate de Commerce eficiente, escalable y seguro con datos de su [!DNL Adobe Commerce Optimizer] instancia.


## Requisitos previos

* Asegúrese de tener un cuenta de GitHub (github.com) que pueda crear repositorios y que esté configurado para el desarrollo local.

* Familiarícese con el flujo de trabajo básico y el vocabulario relacionado con la creación de un escaparate para Adobe Edge servicios de entrega revisando la [Información general](https://experienceleague.adobe.com/developer/commerce/storefront/get-started)  en la documentación de Adobe Systems Commerce Storefront.
* Configurar el entorno de desarrollo


### Configurar el entorno de desarrollo

Para configurar el entorno de desarrollo, instale la versión necesaria de Node.js y la extensión Sidekick explorador.

#### Instalación Node.js

Para desarrollar y prueba su [!DNL Adobe Commerce Optimizer] escaparate en el proyecto de Edge Delivery Services localmente, necesita Node.js versión 22.13.1 LTS.

Si es necesario, complete los siguientes pasos para instalar Node Versión Manager (NVM) y la versión de Node.js requerida.

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
>Esta configuración es para desarrollo con [!DNL Adobe Commerce Optimizer] y Adobe Commerce Edge Delivery Service Storefront. Hay recursos adicionales disponibles para ampliar y personalizar su solución [!DNL Adobe Commerce Optimizer] mediante [App Builder para Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder) y [API Mesh para Adobe Developer App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/api-mesh/getting-started-api-mesh). Para obtener información de acceso y uso, póngase en contacto con el representante de su cuenta de Adobe.

#### Instalación de Sidekick

Instale la extensión del explorador Sidekick para editar, previsualizar y publicar contenido de la tienda. Ver [instrucciones de instalación de Sidekick](https://www.aem.live/docs/sidekick#installation).


## Crear tu tienda

La tienda que creas para tu proyecto [!DNL Adobe Commerce Optimizer] se ha creado usando una versión personalizada de la plantilla de Adobe Commerce en Edge Delivery Services Storefront. La plantilla es un conjunto de archivos y carpetas que proporcionan un punto de partida para crear su tienda.

Este proceso de configuración de tienda está personalizado específicamente para [!DNL Adobe Commerce Optimizer] proyectos. El flujo es diferente al flujo para la configuración estándar de [Adobe Commerce en Edge Delivery Services Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/).

>[!NOTE]
>
>Este tutorial utiliza macOS, Chrome y Visual Studio Code como entorno de desarrollo. Las capturas de pantalla y las instrucciones reflejan esa configuración. Puede utilizar un sistema operativo, un explorador y un editor de código diferentes, pero la interfaz de usuario que ve y los pasos que debe seguir varían en consecuencia.

### Resumen de flujo de trabajo

Siga estos pasos para configurar una tienda para usarla con Adobe Commerce Optimizer.

1. **[Crear una carpeta de contenido](#step-1-create-a-content-folder)**: crea una carpeta de contenido compartido en Google Drive o Sharepoint. Esta carpeta contiene los contenido y activos de muestra para su escaparate.

1. **[Crear un código repositorio](#step-1-create-a-code-repository)**–Crear un repositorio de GitHub desde el plantilla repetitivo de Adobe Systems Commerce + Edge Delivery Services. Incluya todas las ramas de la repositorio de origen.
1. **[Actualice el elemento](#step-2-update-the-storefront-boilerplate)** repetitivo del escaparate: actualice el plantilla repetitivo personalizado en la `aco` Rama del repositorio para conectar su carpeta contenido al escaparate y revise la configuración del escaparate que entrega datos del instancia de demostración de Adobe Systems Commerce Optimizer a su escaparate.
1. **[Cargue el código](#step-3-upload-the-updated-boilerplate-code)** repetitivo actualizado del escaparate: sobrescriba el código de la `main` Rama con el código actualizado de la `aco` Rama.
1. **[añadir la aplicación](#step-4-add-the-aem-code-sync-app)** CodeSync: conecte su repositorio al servicio de entrega perimetral. No conecte la aplicación Code Sync hasta que haya completado la personalización del código fuente y esté listo para enviar el código al `main` Rama.
1. **[Previsualizar y publicar tu contenido](#step-5-preview-and-publish-your-content)**: utiliza la extensión de Sidekick para previsualizar y publicar el contenido del sitio desde la carpeta de contenido en la tienda.
1. **[Previsualice el sitio y vea datos de ejemplo](#step-6-preview-your-site-and-view-sample-data)**: conéctese al sitio de la tienda para ver el contenido y los datos de ejemplo de la instancia de demostración [!DNL Adobe Commerce Optimizer].
1. **[Desarrolle la tienda en su entorno local](#step-7-develop-the-storefront-in-your-local-environmentdevelop-the-storefront-in-your-local-environment)**-Instale las dependencias requeridas. Inicio el servidor de desarrollo local y actualice la configuración del escaparate para conectarse al [!DNL Adobe Commerce Optimizer] instancia que Adobe Systems aprovisionado automáticamente.
1. **[Administrar contenido](#step-8-manage-site-content)** del sitio: obtenga más información sobre cómo actualizar y administrar los contenido del sitio.

### Paso 1: Crear una carpeta contenido

Siga las instrucciones de la documentación de Adobe Commerce Storefront para agregar una carpeta de contenido compartido en Google Drive o Sharepoint y agregar el contenido de ejemplo. El contenido de ejemplo incluye imágenes, texto y otros recursos que conforman el sitio.

* [Crear y compartir una carpeta de Google Drive o Sharepoint](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/#create-and-share-folder)
* [Cargue el contenido de muestra](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/#add-sample-content) en su carpeta.

### Paso 2: Crear un repositorio de código

Cree un repositorio de código en GitHub con la plantilla de plantillas de Edge Delivery Services + Adobe Commerce. Esta plantilla proporciona el código de repetidor de la tienda.

1. Inicie sesión en su cuenta de GitHub.

1. Vaya al repositorio de GitHub [aem-boilerplate-commerce](https://github.com/hlxsites/aem-boilerplate-commerce).

1. Seleccione **Usar esta plantilla** y, a continuación, seleccione **Crear un nuevo repositorio** en el menú desplegable.

   ![[!DNL Create github repo from storefront boilerplate template]](./assets/storefront-create-github-repo.png){width="700" zoomable="yes"}

   Esto abre la página de configuración del repositorio.

   ![[!DNL Configure github repo to pull all branches from boilerplate repo]](./assets/storefront-configure-github-repo.png){width="700" zoomable="yes"}

1. Complete el formulario de configuración con los siguientes detalles:

   * **Plantilla de repositorio**—`hlxsites/aem-boilerplate-commerce` (predeterminada).
   * **Incluir todas las ramas**: seleccione la opción para incluir todas las ramas.
   * **Propietario**: su organización o cuenta (obligatorio).
   * **Nombre del repositorio**: Un nombre único para su nuevo repositorio (obligatorio).
   * **Descripción**: Una breve descripción de su repositorio (opcional).
   * **Público o privado**: Adobe recomienda público (predeterminado).

1. Seleccione **Crear repositorio**.

   Después de uno o dos minutos, se abre el nuevo repositorio.

   Ignore las notificaciones de solicitudes de extracción que se muestren en el nuevo repositorio.

### Paso 3: Actualizar la plantilla de la tienda

En esta sección, debe completar las tareas siguientes:

* Consulte los `aco` Rama de su repositorio para actualizar el plantilla repetitivo personalizado para [!DNL Adobe Commerce Optimizer] proyectos
* Conecte su carpeta contenido al escaparate actualizando el `fstab.yaml` archivo para que apunte a su carpeta contenido.
* Revise el archivo de configuración del escaparate, `config.json`
* Configure la extensión Sidekick para editar, previsualización y publicar contenido desde su carpeta de contenido compartida.

Necesita la siguiente información para completar estos pasos:

* **GitHub repositorio URL desde el paso 2**: `github.com/{ORG}/{SITE}`

   * `{ORG}` es el nombre de organización o de usuario del repositorio

   * `{SITE}` es su nombre repositorio

* **La carpeta de contenido URL del paso 1**: `https://drive.google.com/drive/folders/{YOUR_FOLDER_ID}`

  `{YOUR_FOLDER_ID}` es el ID de la carpeta que creó con los datos contenido ejemplo.

#### Actualice el código repetitivo para conectarse a la carpeta contenido

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

1. Actualice el archivo de configuración de la tienda para que indique la dirección URL de contenido.

   1. Abra el archivo de configuración [fstab.yaml](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/#vocabulary).

      ```json
      mountpoints:
       /: {YOUR_MOUNTPOINT_URL}
      
      folders:
       /products/: /products/default
      ```

   1. Reemplace `{YOUR_MOUNTPOINT_URL}` por la URL de su sistema de administración de contenido.

      Por ejemplo, si utiliza Google Drive, el código actualizado debería tener este aspecto.

      ```json
       mountpoints:
        /: https://drive.google.com/drive/folders/{YOUR_FOLDER_ID}
      ```

   1. Guarde el archivo.

#### Revise la configuración de la conexión de datos

La conexión de datos establece la comunicación entre Adobe Commerce Optimizer y la tienda, lo que garantiza que los datos del catálogo fluyan sin problemas a la tienda. Este proceso rellena varias interfaces de tienda, incluidas las páginas de componente de búsqueda, lista de productos y detalles de productos necesarias para [!DNL Adobe Commerce Optimizer].

Para la configuración inicial de la tienda, Adobe proporciona un archivo de configuración predeterminado que se conecta a una instancia de demostración de Adobe Commerce Optimizer con datos de ejemplo.

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

Revise el archivo de configuración de la tienda en el repositorio para comprender cómo se establece la conexión de datos.

1. En el repositorio de código, vaya al directorio raíz.

1. Abra el archivo `config.json`.

   En este archivo, los siguientes valores clave especifican la instancia de Adobe Systems Commerce Optimizer a la que conectarse y determinar los datos que fluyen hacia el escaparate:

   * `commerce-endpoint` define el instancia Adobe Systems Commerce Optimizer para conectarse.
   * `headers` Determine los datos que llegan al escaparate.
      * `ac-channel-id` está configurado como `west_coast_inc`
      * `ac-price-book-id` está configurado como `west_coast_inc`
      * `ac-scope-locale` se ha establecido en `en-US`
      * `ac-price-book-id` se ha establecido en `west_coast_inc`

   Estos valores establecen el ID de canal, la configuración regional y el ID del libro de precios para enviar datos de catálogo a un canal de ventas específico y filtrar esos datos en función de la configuración regional y los valores del libro de precios especificados. Más adelante, aprenderá a cambiar la instancia de Adobe Commerce Optimizer y a actualizar los encabezados para definir qué datos se entregan a la tienda.

1. Después de revisar el archivo, ciérrelo y continúe con el tutorial.


#### Configurar la extensión de la barra de tareas

Añada la configuración del proyecto para la extensión de Sidekick. Sidekick se usa para editar, previsualizar y publicar el contenido de la tienda. Esta configuración garantiza que puede utilizar Sidekick para administrar el contenido tanto en la carpeta de contenido compartido como en las páginas del sitio publicadas en los entornos de ensayo y producción.

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

   * `{ORG}` es el nombre de repositorio o nombre de usuario para su repositorio de código

   * `{SITE}` es el nombre del repositorio

1. Guarde el archivo.

### Paso 4: cargar el código de plantillas actualizado

Para usar el código de plantilla de tienda personalizado, sobrescriba el código de la rama `main` con sus actualizaciones.

1. Desde el editor o IDE, confirme y guarde los archivos actualizados.

   ```bash
   git add .
   ```

   ```bash
   git commit -m "Update storefront boilerplate for Adobe Commerce Optimizer"
   ```

1. Inserte los cambios en la rama `aco` y sobrescriba la rama `main`:

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

### Paso 6: Vista previa y publicar tu contenido

Para agregar contenido a su escaparate, debe previsualización y publicar su contenido usando la extensión Sidekick.

1. Abre tu carpeta contenido en Google Drive o Sharepoint.

1. Para activar la barra de tareas, haga clic en el icono de la barra de tareas en la barra de herramientas de explorador.

   ![[!DNL Turn on Sidekick from browser toolbar]](./assets/storefront-enable-sidekick-toolbar.png){width="700" zoomable="yes"}

1. Utilice la barra de herramientas para previsualización y publicar los contenido.

   ![[Seleccionar archivos para previsualizar y publicar]](./assets/storefront-content-preview-publish.png){width="700" zoomable="yes"}

1. Seleccione los archivos de cada carpeta por separado y utilice la barra de herramientas de la barra de tareas para previsualización y publicar todos los archivos.

   * **Vista previa**: carga contenido en el entorno de ensayo. Las direcciones URL de ensayo de tienda terminan con `.aem.page`.

   * **Publicar**: carga contenido en el entorno de producción. Las direcciones URL de producción finalizan con `aem.live`.

Para obtener más información, consulte la documentación de Adobe Experience Manager [Sidekick](https://www.aem.live/docs/sidekick).

### Paso 7: Previsualizar el sitio

Obtenga una vista previa del sitio para comprobar que el contenido de la muestra y los datos de demostración de Adobe Commerce Optimizer se muestran correctamente.

* **El contenido de muestra** se suministra desde su carpeta de contenido compartido. Incluye los diseños de página, los titulares y otro contenido que ha publicado con Sidekick.
* **Los datos de muestra** se han obtenido desde la instancia de demostración [!DNL Adobe Commerce Optimizer]. Los datos incluyen datos de productos con atributos de productos, imágenes, descripciones de productos y precios rellenados según los valores especificados en el archivo de configuración de tienda `config.json`.


#### Conéctese al sitio para ver contenido y datos de ejemplo

1. Para conectarse al sitio, vaya a `https://main--{SITE}--{ORG}.aem.live`.

   Reemplace `{ORG}` y `{SITE}` por la organización y el nombre de su repositorio de plantillas.

   ![[!DNL ACO storefront site with boilerplate]](./assets/aco-storefront-site-boilerplate.png){width="700" zoomable="yes"}

   Si la página devuelve un error 404, asegúrese de que ha publicado el contenido con la extensión de Sidekick. Además, compruebe que el archivo `fstab.yaml` actualizado usa la dirección URL de la carpeta de contenido.

1. Vea los datos del catálogo de muestra procedentes de la instancia de demostración de Commerce Optimizer.

   1. Busque `tires` para ver una lista desplegable de productos de neumáticos disponibles.

   ![[!DNL Discover Adobe Commerce Optimizer products]](./assets/storefront-site-with-aco-data.png){width="700" zoomable="yes"}

   El componente de búsqueda forma parte del código de plantillas de tienda. Los datos de los resultados de búsqueda se rellenan en función de la configuración de la tienda.

   1. Pulse **Intro** para ver la página de la lista de productos.

      ![[!DNL View product details page]](./assets/storefront-with-aco-pdp-page.png){width="675" zoomable="yes"}

   1. Ver una página de detalles del producto seleccionando cualquier producto de neumático en la página.

      Si explora la tienda, verá que algunos de los componentes no funcionan. Por ejemplo, al agregar un producto al carro de compras, se devuelve un error y los componentes de administración de cuentas no funcionan. Esto se debe a que estos componentes no se han configurado para recibir datos de un servidor de Commerce. Los datos del instancia de Adobe Systems Commerce Optimizer solo rellenan el componente búsqueda, el lista del producto y las páginas de detalles del producto.

   1. Después de explorar el escaparate, continúe con el tutorial.


### Paso 8: Desarrolla el escaparate en tu entorno local

En esta sección, experimentará con la configuración del escaparate en su entorno de desarrollo local conectando el escaparate al [!DNL Adobe Commerce Optimizer] instancia que Adobe Systems aprovisionado para usted.

Para realizar la conexión, necesita el punto final de GraphQL para los servicios de comercialización que se proporcionó en su correo electrónico de incorporación.

```text
https://na1-sandbox.api.commerce.adobe.com/{tenantId}/graphql
```

#### Inicio desarrollo local

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

   La primera Página de su escaparate repetitivo debe estar visible en su explorador en `http://localhost:3000`.

![[!DNL Configure github repo to pull all branches from boilerplate repo]](./assets/aco-storefront-local-dev-env.png){width="700" zoomable="yes"}


#### Actualizar la configuración del escaparate

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

      La búsqueda no devuelve ningún resultado porque los encabezados del archivo de configuración de la tienda utilizan valores de encabezados basados en la instancia de demostración. Ahora que la configuración apunta a la instancia [!DNL Adobe Commerce Optimizer] aprovisionada por usted, esos valores no son válidos.

### Pasos siguientes

Consulte el [caso de uso de extremo a extremo de Storefront y Catalog Administrator](./use-case/admin-use-case.md) para aprender a mostrar contenido en su tienda al actualizar la configuración de la tienda usando los valores de su instancia de [!DNL Adobe Commerce Optimizer].

>[!MORELIKETHIS]
>
>* Si planea usar [!DNL Adobe Commerce Optimizer] sin un back-end de Adobe Commerce, consulte la [documentación de la tienda Adobe Experience Manager](https://experienceleague.adobe.com/developer/commerce/storefront/) para obtener más información sobre cómo actualizar el contenido del sitio y la integración con los componentes de front-end y los datos del back-end de Commerce.
></br></br>
>* Si planea usar [!DNL Adobe Commerce Optimizer] con un servidor de Adobe Commerce, consulte la [documentación de Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/) para obtener información sobre cómo actualizar contenido y configurar componentes de tienda para la administración de cuentas, el cierre de compra y otras funcionalidades.
