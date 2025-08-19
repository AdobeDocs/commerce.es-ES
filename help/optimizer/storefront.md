---
title: Configurar tu tienda
description: Aprenda a configurar su  [!DNL Adobe Commerce Optimizer] tienda.
role: Developer
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
exl-id: 2b4c9e98-a30c-4a33-b356-556de5bd721a
source-git-commit: 2b35e822e192bdac316379f55c3bc924d62ca008
workflow-type: tm+mt
source-wordcount: '1855'
ht-degree: 0%

---

# Configurar tu tienda

Este tutorial proporciona instrucciones detalladas para configurar y usar [Adobe Commerce Storefront con tecnología Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/) para crear una tienda Commerce segura, escalable y de rendimiento con tecnología de datos de tu instancia de [!DNL Adobe Commerce Optimizer].


>[!TIP]
>
>Realice un seguimiento rápido del proceso de configuración de la tienda mediante la herramienta Creador de sitios para configurar el repositorio de código de la tienda y el entorno de creación de documentos
>&#x200B;>automáticamente. A continuación, puede seguir estas instrucciones para comprender cómo se creó la tienda y obtener más información acerca de los componentes disponibles.

## Requisitos previos

* Asegúrese de que tiene una cuenta de GitHub (github.com) que puede crear repositorios y que está configurada para el desarrollo local.

* Obtenga información acerca de los conceptos y el flujo de trabajo para desarrollar tiendas Commerce en Adobe Edge Delivery Services revisando la [Información general](https://experienceleague.adobe.com/developer/commerce/storefront/get-started) en la documentación de Adobe Commerce Storefront.
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
1. **[Actualizar la plantilla de plantilla de tienda](#step-2-update-the-storefront-boilerplate)**: actualiza la plantilla de plantilla personalizada para conectar la carpeta de contenido a la tienda.
1. **[Implementar cambios](#step-3-deploy-changes)**: confirma y envía la personalización de las plantillas a GitHub para aplicar los cambios.
1. **[Agregar la aplicación CodeSync](#step-5-add-the-aem-code-sync-app)**: conecte el repositorio al servicio Edge Delivery. No conecte la aplicación de sincronización de código hasta que haya completado la personalización del código fuente y lo haya insertado en el repositorio de GitHub.
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

   * **Plantilla de repositorio**—`hlxsites/aem-boilerplate-commerce` (predeterminada).
   * **Propietario**: su organización o cuenta (obligatorio).
   * **Nombre del repositorio**: Un nombre único para su nuevo repositorio (obligatorio).
   * **Descripción**: Una breve descripción de su repositorio (opcional).
   * **Público o privado**: Adobe recomienda público (predeterminado).

1. Seleccione **Crear repositorio**.

   Después de varios minutos, se abre el nuevo repositorio.

   Omita las notificaciones de solicitudes de extracción que se muestren en la interfaz de usuario de GitHub.

### Paso 2: Actualizar la plantilla de la tienda

Necesita la siguiente información para actualizar el código de plantillas de tienda:

* **URL del repositorio de GitHub del paso 2**— `github.com/{ORG}/{SITE}`

   * `{ORG}` es el nombre de organización o de usuario para el repositorio

   * `{SITE}` es su nombre de repositorio

* **URL de carpeta de contenido del paso 1**— `https://drive.google.com/drive/folders/{YOUR_FOLDER_ID}`

  `{YOUR_FOLDER_ID}` es el identificador de la carpeta que creó con los datos de contenido de ejemplo.

#### Vincule el repositorio al entorno de Document Author

1. Clone el repositorio en el equipo local.

   ```bash
   git clone https://github.com/{ORG}/{SITE}.git
   ```

   Si encuentra errores al clonar el repositorio, consulte [Solucionar errores de clonación](https://docs.github.com/en/repositories/creating-and-managing-repositories/troubleshooting-cloning-errors) en la documentación de GitHub.

1. Abra el repositorio en su terminal o IDE.

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

1. Cree un nuevo directorio `tools/sidekick`.

   ```shell
   mkdir tools/sidekick
   ```

1. Copie el archivo `demo-sidekick.json` en el directorio raíz al directorio `tools/sidekick` y cambie su nombre a `config.json`.

   ```shell
   cp demo-sidekick.json tools/sidekick/config.json
   ```

1. Personalice la configuración de Sidekick para su sitio.

   Desde el directorio `tools/sidekick/`, edite el archivo `config.json`.

   +++Archivo de configuración de Sidekick

   ```json
   {
     "project": "My Project",
     "editUrlLabel": "Document Authoring",
     "editUrlPattern": "https://da.live/edit#/{{org}}/{{site}}{{pathname}}"
   }
   ```

1. Actualice los valores de clave `url` con los valores del repositorio de GitHub.

   * Reemplace la cadena `{{ORG}}` por la organización o el nombre de usuario de su repositorio.

   * Reemplace la cadena `{{SITE}}` por el nombre del repositorio.

   * El sistema ha rellenado la variable `pathname`.

   +++Ejemplo de archivo de configuración actualizado

   Si el nombre del repositorio de GitHub es `aco-storefront` y la organización es `early-adopter`, la URL actualizada debería tener el aspecto siguiente:

   ```json
   {
     "project": "My Project",
     "editUrlLabel": "Document Authoring",
     "editUrlPattern": "https://da.live/edit#/aco-storefront/early-adopter{{pathname}}"
   }
   ```

   +++

1. Guarde el archivo.

### Paso 3: Implementar cambios

Para usar el código de plantilla de tienda personalizado, sobrescriba el código de la rama `main` con sus actualizaciones.

1. Desde el editor o IDE, confirme y guarde los archivos actualizados.

   ```bash
   git add .
   ```

1. Compruebe que está confirmando los dos archivos actualizados.

   ```bash
   git status
   On branch main
   Your branch is up to date with 'origin/main'.
   
   Changes to be committed:
    (use "git restore --staged <file>..." to unstage)
        new file:   fstab1.yaml
        modified:   tools/sidekick/config.json
   ```

1. Confirme los cambios.

   ```bash
   git commit -m "Update storefront boilerplate for Adobe Commerce Optimizer"
   ```

1. Aplique los cambios.

   ```bash
   git push
   ```

### Paso 5: Añadir la aplicación de sincronización de código de AEM

Conecte el repositorio al servicio de Edge Delivery agregando la aplicación GitHub de sincronización de código de AEM a su repositorio.

>[!IMPORTANT]
>
>No conecte la aplicación de sincronización de código hasta que haya cargado el código de plantillas actualizado en la rama principal del repositorio de GitHub.

1. Abra la página de configuración [aplicación AEM Code Sync](https://github.com/apps/aem-code-sync).

1. Seleccione **Configurar** y luego realice la autenticación con la **organización** o la **cuenta** que contiene el repositorio que creó.

1. En el formulario, elija **Seleccionar solo repositorios** y, a continuación, seleccione el repositorio que creó.

1. Seleccione **Instalar** para agregar la aplicación AEM Code Sync a su repositorio.

   Debería ver un mensaje que indique que la aplicación se ha instalado correctamente.

### Paso 6: Añadir contenido

Cree e inicialice el contenido de la tienda en el entorno de creación de documentos alojado en `https://da.live` con la herramienta de creación de sitios. Esta herramienta importa el contenido de ejemplo en el entorno de creación de documentos y completa el proceso de vista previa y publicación de contenido para todos los documentos del contenido de ejemplo. El contenido de ejemplo incluye los diseños de página, titulares, etiquetas y otros elementos para rellenar la tienda.

1. Abrir la [herramienta de creación de sitios](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator)

1. Configure el repositorio:

   * Seleccione **[!UICONTROL Use Existing Repository]**.
   * Escriba **[!UICONTROL Organization/Username]** para el proyecto de plantillas de tienda.
   * Escriba **[!UICONTROL Repository Name]**.

1. Importe, previsualice y publique el contenido en el entorno de creación de documentos seleccionando **Crear sitio**.

   ![[!DNL AEM demo content clone tool]](./assets/storefront-edit-initial-content.png){width="700" zoomable="yes"}

   Una vez creado el sitio, puede utilizar los vínculos de las secciones [!UICONTROL Edit content] y [!UICONTROL View Site] para explorar la tienda de demostración.

   Los vínculos principales a su contenido y sitio siguen estos formatos:

   * **Carpeta de contenido raíz**— `https://da.live/#/{ORG}/{SITE}`
   * **Vista previa del sitio**—   `https://main--{SITE}--{ORG}.aem.page/`
   * **Producción del sitio:**— `https:/main--{SITE}--{ORG}.ae.live/`

1. Abra el vínculo de la carpeta de contenido raíz para ver el contenido.

   ![[!DNL Storefront Document Author environment]](./assets/storefront-document-author-environment.png){width="700" zoomable="yes"}

   >[!TIP]
   >
   >En la navegación lateral, usa los vínculos [!UICONTROL **Aprender**] y [!UICONTROL **Descubrir**] para acceder a recursos de aprendizaje y administrar el sitio y el contenido del mismo.

### Paso 7: Previsualizar el sitio de demostración

Compruebe que el contenido de la muestra y los datos de la instancia de demostración de Adobe Commerce Optimizer se muestran correctamente.

* **El contenido de muestra** se proporciona desde la carpeta de contenido en el entorno de Document Author. Incluye los diseños de página, los titulares y las etiquetas del sitio.
* **Los datos de muestra** se han obtenido desde la instancia de demostración [!DNL Adobe Commerce Optimizer]. Los datos incluyen datos de productos con atributos de productos, imágenes, descripciones de productos y precios rellenados según los valores de encabezado especificados en el archivo de configuración de tienda, `config.json`.

#### Conéctese al sitio para ver contenido y datos de ejemplo

1. Para ver el sitio, vaya a `https://main--{SITE}--{ORG}.aem.live`.

   Reemplace `{ORG}` y `{SITE}` por la organización y el nombre de su repositorio de plantillas.

   ![[!DNL ACO storefront site with boilerplate]](./assets/aco-storefront-site-boilerplate.png){width="700" zoomable="yes"}

   Si la página devuelve un error 404, compruebe lo siguiente:

   * [El punto de montaje del archivo `fstab.yaml` señala a la dirección URL de contenido correcta](#link-the-repository-to-the-document-author-environment): `https://content.da.live/{ORG}/{SITE}/`
   * [Ha configurado la aplicación de sincronización de código para conectarse a su repositorio de GitHub](#step-5%3A-add-the-aem-code-sync-app).
   * [Ha publicado el contenido en el entorno de Document Author mediante la herramienta de clonación de contenido de demostración](#step-6%3A-add-content-documents-for-your-storefront).


1. Vea los datos de catálogo de muestra procedentes de la instancia predeterminada de Commerce Optimizer.

   1. En el encabezado de la tienda, haga clic en la lupa para buscar `tires`.

      ![[!DNL View product list page]](./assets/storefront-site-with-aco-data.png){width="675" zoomable="yes"}

   1. Pulse **Intro** para ver la página de resultados de la búsqueda.

      ![[!DNL View search results page]](./assets/storefront-with-aco-search-results-page.png){width="675" zoomable="yes"}

      Los componentes de página de resultados de búsqueda se definen en el documento de contenido `search`. Los datos de los resultados de búsqueda se rellenan según la configuración de la tienda en `config.json`.

   1. Vea la página de detalles del producto seleccionando cualquier producto de neumático en la página.

      ![[!DNL View product details page]](./assets/storefront-with-aco-pdp-page.png){width="675" zoomable="yes"}

      Los componentes de la página de detalles del producto están definidos por el documento de contenido `default` en la carpeta `product`.

### Paso 8: Desarrollo en su entorno local

En esta sección, se actualiza la configuración de la tienda desde el entorno de desarrollo local.

* Actualice la configuración de la tienda para conectarse al extremo de GraphQL para la instancia [!DNL Adobe Commerce Optimizer] que Adobe ha aprovisionado para usted.
* Actualice los valores del encabezado para recuperar datos de la instancia.

#### Iniciar desarrollo local

1. En el IDE, cierre la rama principal y restablézcala a la última confirmación de la rama remota.

   ```bash
   git checkout main
   git reset --hard origin/main
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

   1. Pulse **Intro** para mostrar la página de resultados de la búsqueda.

      ![Resultados de búsqueda vacíos con valores de encabezado no válidos](./assets/storefront-configuration-with-incorrect-headers.png){width="675" zoomable="yes"}

      La búsqueda no devuelve ningún resultado porque los valores del encabezado del archivo de configuración de la tienda se basan en la instancia predeterminada. Ahora que la configuración apunta a la instancia [!DNL Adobe Commerce Optimizer] aprovisionada por usted, esos valores no son válidos.

### Pasos siguientes

Consulte el [caso de uso de extremo a extremo del administrador de tiendas y catálogos](./use-case/admin-use-case.md) para obtener más información sobre cómo administrar y mostrar contenido y datos en la tienda.

>[!MORELIKETHIS]
>
> Consulte la [documentación de Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/) para obtener más información sobre la actualización del contenido del sitio y la integración con los componentes de front-end y los datos del back-end de Commerce.
