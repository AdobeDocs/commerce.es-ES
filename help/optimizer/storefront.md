---
title: Configurar tu tienda
description: Aprenda a configurar su  [!DNL Adobe Commerce Optimizer] tienda.
role: Developer
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a Adobe Commerce as a Cloud Service y  [!DNL Adobe Commerce Optimizer] proyectos (infraestructura SaaS administrada por Adobe)."
exl-id: 2b4c9e98-a30c-4a33-b356-556de5bd721a
source-git-commit: e46c55cba21501c6fa12db6c130493b99de0e4da
workflow-type: tm+mt
source-wordcount: '1351'
ht-degree: 0%

---

# Configurar tu tienda

Esta guía le explica cómo configurar una tienda para la instancia de [!DNL Adobe Commerce Optimizer] mediante los servicios de entrega de Adobe Edge. Su tienda incluye código de plantillas, contenido de muestra y compatibilidad con páginas de detalles de productos y descubrimiento de productos (búsqueda y filtrado).

**Tiempo estimado para finalizar:** 30-45 minutos

## Requisitos previos

* **Cuenta de GitHub** que puede crear repositorios y está configurada para el desarrollo local (github.com)
* **[!DNL Adobe Commerce Optimizer]instancia** con datos de ejemplo y vistas de catálogo y directivas configuradas
   * Consulte [Agregar datos de ejemplo](get-started.md#add-sample-data) para obtener instrucciones de configuración.

### Datos de instancia requeridos

Antes de empezar, recopile la siguiente información de su instancia de [!DNL Adobe Commerce Optimizer]:

* **ID de inquilino** (también denominado ID de instancia)
   * Disponible en la [página de detalles de instancia](get-started.md#manage-instances)
* **Punto final de GraphQL** para su instancia
   * Disponible en la [página de detalles de instancia](get-started.md#manage-instances)
* **Id. de vista de catálogo** para la vista de catálogo global
   * Disponible en la [página de detalles del catálogo](./setup/catalog-view.md#manage-catalog-view)
* **Configuración regional de Source** para su vista de catálogo
   * El valor predeterminado para los datos de ejemplo es `en-US`

>[!NOTE]
>
>Los clientes de acceso de prueba pueden encontrar el punto final de GraphQL en el correo electrónico de bienvenida recibido cuando se creó la instancia. Las instancias de prueba vienen preconfiguradas con datos de muestra, vistas de catálogo y directivas.

## Configuración de pasos

1. **[Crea tu proyecto de tienda](#create-your-storefront-project)**-Usa la [herramienta de creador de sitios](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator) para crear un nuevo proyecto de tienda con código de plantillas, contenido de muestra y un archivo de configuración.

1. **[Personalizar la configuración de la tienda](#customize-the-storefront-configuration)**: actualice el archivo `config.json` en su repositorio para conectarse a su instancia de [!DNL Adobe Commerce Optimizer].

1. **[Compruebe su configuración](#verify-your-setup)** (10 minutos)
   * Previsualización del sitio de la tienda
   * Prueba de las páginas de detalles del producto y funcionalidad de búsqueda

## Cree su proyecto de tienda

La herramienta Creador de sitios crea un proyecto de tienda completo con los siguientes componentes:

* **Sitio**: página de aterrizaje de tienda con contenido de plantillas
* **Código**: repositorio con archivos de origen de plantillas
* **Contenido**: entorno de creación de documentos con archivos de contenido de sitio
* **Configuración de Commerce**: `config.json` archivo para configuración específica de instancia

### Paso 1: Generación del proyecto

1. Abrir la [herramienta Creador de sitios](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator)

   ![[!DNL Site Creator tool]](./assets/storefront-setup-site-creator.png){width="700" zoomable="yes"}

1. Seleccione **Crear nuevo sitio (código y contenido)**.

1. Complete la configuración del sitio:

   * **Nombre de organización/usuario de GitHub**: escriba su nombre de usuario u organización de GitHub
   * **Nombre del sitio**: elige un nombre descriptivo para tu tienda
   * **Punto final de Commerce GraphQL (opcional)**: escriba el punto final de GraphQL para su instancia de [!DNL Adobe Commerce Optimizer]

1. Haga clic en **Crear sitio** para crear el repositorio de GitHub con el código de plantilla de tienda.

   Cuando se crea el repositorio, el creador del sitio actualiza y le solicita que instale la aplicación de sincronización de código.

### Paso 2: Instalar la aplicación de sincronización de código

1. Haga clic en **[!UICONTROL Install AEM Code Sync App]** para abrir el programa de instalación de sincronización de código en una pestaña nueva.

1. Configure la aplicación de sincronización de código:
   * Seleccione su organización de GitHub y haga clic en **[!UICONTROL Configure]**.
   * En la interfaz de sincronización de código, haga clic en **[!UICONTROL Only select repositories]**.
   * Haga clic en el menú **[!UICONTROL Select repositories]** y, a continuación, seleccione el repositorio de código de tienda que ha creado.
   * Haga clic en **[!UICONTROL Save]** para registrar su repositorio.

1. Vuelva a la ventana del explorador donde está abierto el Creador del sitio y haga clic en **Crear sitio**.

   El creador del sitio copia el contenido de las plantillas de tienda en el entorno de creación de documentos. Este proceso tarda de 1 a 2 minutos.

### Paso 3: guardar los vínculos del proyecto

1. En la sección Detalles del sitio, revise los vínculos del proyecto de tienda:

   ![[!DNL Storefront setup complete]](./assets/storefront-setup-complete.png){width="700" zoomable="yes"}

   Use estos vínculos para administrar el código, el contenido y la configuración de la tienda.

1. Copie y guarde estos vínculos para referencia futura: haga clic en **[!UICONTROL Copy].

## Configurar tu tienda

Actualice la configuración de la tienda para conectarse a la instancia de [!DNL Adobe Commerce Optimizer].

1. Abra el archivo `config.json` en el repositorio de código de plantillas.

   `https://github.com/<username or org>/<repo name>/config.json`

1. Busque la sección `cs` (servicio de catálogo) en la configuración.

1. Reemplace los valores de marcador de posición por los valores de la instancia. Consulte [Requisitos previos](#prerequisites).

   ```json
   "cs": {
      "AC-View-ID": "{catalogViewId}",
      "AC-Source-Locale": "en-US",
      "AC-Price-Book-ID": "{priceBookId}"
   }
   ```

   >[!NOTE]
   >
   >Para encontrar el ID de la libreta de precios, consulte los [detalles de configuración de la vista del catálogo](./setup/catalog-view.md) en Adobe Commerce Optimizer para ver los libros de precios asignados. Si no se ha asignado ningún libro de precios, puede eliminar esta cabecera del fichero de configuración. Vuelva a añadirlo cuando se haya asignado un libro de precios a la vista de catálogo.

1. Guarde el archivo de configuración.

   Los cambios de configuración pueden tardar unos minutos en propagarse. Si no ve los datos inmediatamente, espere de 2 a 3 minutos antes de solucionar el problema.

## Verifique su configuración

Pruebe la tienda para asegurarse de que está conectada correctamente a la instancia de [!DNL Adobe Commerce Optimizer].

### Paso 1: Ver la página principal de tu tienda

1. Vaya a la URL de vista previa activa:

   `https://main--{SITE}--{ORG}.aem.live`

   Reemplace `{ORG}` y `{SITE}` por su organización de GitHub y el nombre del sitio.

1. **Criterios de éxito**: debería ver la página principal de la tienda con contenido de plantillas.

   ![[!DNL ACO storefront site with boilerplate]](./assets/aco-storefront-site-boilerplate.png){width="700" zoomable="yes"}

### Paso 2: Probar las páginas de detalles del producto

Consulte la página de detalles predeterminada del producto para comprobar que los datos del producto se cargan correctamente.

1. Vaya a una página de producto de ejemplo:
   `https://main--{SITE}--{ORG}.aem.live/products/placeholder/{sku}`

   Utilice cualquier SKU de los datos de ejemplo:
   `https://main--{SITE}--{ORG}.aem.live/products/placeholder/aur-flu-tir-std-2017`

   Para la tienda predeterminada, puede usar el valor `placeholder` en la ruta para ver el producto. Cuando empiece a personalizar la tienda, puede personalizar el código de la tienda para establecer la ruta a la página de detalles del producto en función de las rutas del producto definidas en el catálogo.

   >[!TIP]
   >
   >Ver los SKU disponibles de la página [Sincronización de datos](./setup/data-sync.md) en tu instancia de [!DNL Adobe Commerce Optimizer].

1. **Criterios de éxito**: La página debería mostrar:
   * Nombre, descripción y precios del producto
   * Imágenes de productos
   * Funcionalidad Añadir al carro
   * Datos recuperados de su instancia de [!DNL Adobe Commerce Optimizer]

   ![[!DNL Default product detail page showing a product from the sample data]](./assets/storefront-boilerplate-product-page.png){width="700" zoomable="yes"}

### Paso 3: Probar la funcionalidad de búsqueda predeterminada

Pruebe las funciones de producto predeterminadas, incluidas la búsqueda y el filtrado.

1. En la página de inicio de la tienda, haga clic en el icono de lupa del encabezado.

1. Escriba la cadena de búsqueda `tires` y presione **Intro**.

1. **Criterios de éxito**: debería ver:
   * Página de resultados de búsqueda con productos de neumáticos
   * Opciones de filtrado en la barra lateral
   * Listados de productos con imágenes y precios

   ![[!DNL View search results page]](./assets/storefront-with-aco-search-results-page.png){width="675" zoomable="yes"}

1. Haga clic en cualquier producto de neumático para ver su página de detalles.

   ![[!DNL View product details page]](./assets/storefront-with-aco-pdp-page.png){width="675" zoomable="yes"}

## Resolución de problemas

Si se producen problemas durante la configuración, utilice la consola del inspector de páginas web para comprobar si hay errores. Además, intente borrar la caché del explorador o utilice un explorador diferente.

Siga estas directrices para comprobar problemas comunes:

### Problemas comunes

| Problema | Síntomas | Solución |
|-------|----------|----------|
| **Error en la instalación de sincronización de código** | No se puede completar la configuración de sincronización de código | <ul><li>Asegúrese de que tiene acceso de administrador a su organización de GitHub.</li><li>Intente utilizar un repositorio personal en lugar de una organización.</li><li>Compruebe los permisos de GitHub e inténtelo de nuevo.</li></ul> |
| **El sitio no se carga** | 404 o errores de conexión | <ul><li>Compruebe el formato de la dirección URL del sitio: `https://main--{SITE}--{ORG}.aem.live`</li><li>Compruebe que la aplicación de sincronización de código esté correctamente instalada.</li><li>Asegúrese de que el repositorio sea público o esté configurado correctamente.</li></ul> |
| **No se mostraron datos del producto** | Las páginas de producto muestran marcadores de posición o errores | <ul><li>Compruebe sus valores de configuración en `config.json`</li><li>En la instancia [!DNL Adobe Commerce Optimizer], compruebe la página Sincronización de datos para comprobar que se han cargado los productos de ejemplo. Si no hay productos disponibles, vuelva a cargar los datos de ejemplo o agregue un producto mediante la [API de ingesta de datos](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/using-the-api/#make-your-first-request). Espere unos minutos para que los cambios de configuración se propaguen.</li><li>Intente recuperar los detalles del producto mediante la consulta de [productos](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/use-cases/#return-product-details) del servicio de comercialización utilizando los mismos encabezados configurados en el archivo `config.json`. Si puede recuperar los datos, es probable que haya un problema con la configuración de la vista del catálogo o un error de índice.</li></ul> |
| **La búsqueda no devuelve resultados** | Página de resultados de búsqueda vacía | <ul><li>Compruebe que puede recuperar los resultados de la búsqueda de productos usando la consulta [productSearch](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/use-cases/#product-search) de los servicios de comercialización con los mismos encabezados configurados en el archivo `config.json`. Si puede recuperar los datos, es probable que haya un problema con la configuración de la vista del catálogo o un error de índice.</li><li>Confirme que el identificador de vista de catálogo del archivo `config.json` coincide con el identificador de vista de catálogo de [!DNL Adobe Commerce Optimizer].</li><li>En Adobe Commerce Optimizer, compruebe la configuración de las directivas, la configuración regional y los libros de precios que utilizó en la configuración del encabezado de tienda.</li><li>Compruebe que la configuración de [metadatos de atributo](https://developer.adobe.com/commerce/services/reference/rest/#operation/createProductMetadata) esté establecida correctamente para la búsqueda.</li></ul> |

### Lista de comprobación de validación

Antes de continuar con los siguientes pasos, verifica lo siguiente para asegurarte de que tu tienda funcione correctamente:

![Lista de comprobación](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) Los valores de configuración coinciden con la configuración de la instancia<br>
![Lista de comprobación](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) La página principal de la tienda se carga sin errores<br>
![Lista de comprobación](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) Al menos una página de detalles del producto muestra información completa<br>
![La funcionalidad de búsqueda Checklist](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) devuelve resultados relevantes<br>
![Lista de comprobación](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) Las imágenes del producto se están cargando correctamente<br>
![Lista de comprobación](/help/assets/icons/Smock_CheckmarkCircleOutline_18_N.svg) Los valores de configuración coinciden con la configuración de la instancia<br>

### Obtener ayuda

Si los problemas persisten:

* Revise la [documentación de Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=es)
* Consulte la [guía para desarrolladores de Adobe Commerce Optimizer](https://developer.adobe.com/commerce/services/optimizer/)
* Visite los [recursos de soporte de Adobe Commerce](https://experienceleague.adobe.com/es/docs/commerce-knowledge-base/kb/overview)

## Pasos siguientes

Después de configurar y comprobar la tienda, puedes:

1. **[Instalar Sidekick](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/?lang=es#install-and-configure-sidekick)**: extensión de explorador para editar, previsualizar y publicar contenido directamente desde el sitio web

2. **[Configurar un entorno de desarrollo local](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/?lang=es#set-up-local-environment)**: crea un entorno local para personalizar el código y el contenido de tu tienda

### Aprender y explorar

* **[Completar el caso de uso de extremo a extremo](./use-case/admin-use-case.md)**: obtenga más información acerca de la configuración de la tienda y la administración del catálogo mediante [!DNL Adobe Commerce Optimizer]

* **[Explorar la personalización de tiendas](https://experienceleague.adobe.com/developer/commerce/storefront/setup/?lang=es)**: aprende las opciones avanzadas de configuración

* **[Use complementos de Commerce para personalizar la experiencia de la tienda](https://experienceleague.adobe.com/developer/commerce/storefront/dropins/all/introduction/?lang=es)**: agregue componentes creados previamente para mejorar su experiencia con la tienda

>[!MORELIKETHIS]
>
> Consulte la [documentación de Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=es) para obtener más información sobre la actualización del contenido del sitio y la integración con los componentes de front-end y los datos del back-end de Commerce.
