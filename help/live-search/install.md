---
title: Introducción a  [!DNL Live Search]
description: Conozca los requisitos del sistema y los pasos de instalación para  [!DNL Live Search] desde Adobe Commerce.
role: Admin, Developer
exl-id: 45b985f1-9afb-4a07-93e8-f2fe231c5400
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."
source-git-commit: 3ccf5a7a072505a9b7b3625f5faaac1d38917521
workflow-type: tm+mt
source-wordcount: '3137'
ht-degree: 0%

---

# Configurado correctamente con [!DNL Live Search]

Adobe Commerce [!DNL Live Search] y [[!DNL Catalog Service]](../catalog-service/guide-overview.md) trabajan juntos para proporcionar una solución de búsqueda eficaz, relevante e intuitiva que permita a sus clientes encontrar rápidamente lo que necesitan exactamente. Específicamente, [!DNL Catalog Service] muestra los datos del catálogo para servicios SaaS, como [!DNL Live Search] para usar.

Este artículo proporciona instrucciones paso a paso para implementar [!DNL Live Search] con [!DNL Catalog Service].

## Público

Este artículo está dirigido al desarrollador o integrador de sistemas de su equipo, responsable de instalar y configurar la instancia de Adobe Commerce.

## Requisitos

- [Adobe Commerce](https://business.adobe.com/products/magento/magento-commerce.html) 2.4.4+
- PHP 8.1, 8.2 u 8.3
- [!DNL Composer]
- Ejecución de trabajos cron e indexadores

>[!IMPORTANT]
>
>Antes de implementar [!DNL Live Search], consulte la sección [Límites y límites](boundaries-limits.md) para asegurarse de que [!DNL Live Search] se adapta a sus necesidades comerciales.

## Actualizaciones importantes

- A partir de [!DNL Live Search] 3.0.2, la extensión [!DNL Catalog Service] está empaquetada con la instalación.

- Debido al anuncio de fin de soporte de Elasticsearch 7 para agosto de 2023, Adobe recomienda que todos los clientes de Adobe Commerce migren al motor de búsqueda OpenSearch 2.x. Para obtener información sobre cómo migrar el motor de búsqueda durante una actualización de producto, consulte [Migración a OpenSearch](https://experienceleague.adobe.com/es/docs/commerce-operations/upgrade-guide/prepare/opensearch-migration) en la _Guía de actualización_.

## Plataformas compatibles

- Adobe Commerce en la nube (ECE) : 2.4.4+
- Adobe Commerce local (EE) : 2.4.4+

## Resumen de flujo de trabajo

En un nivel superior, la incorporación de [!DNL Live Search] requiere que:

1. [Instalar](#1-install-the-live-search-extension) la extensión [!DNL Live Search]
1. [Configurar](#2-configure-api-keys) las claves API
1. [Sincronizar](#3-sync-your-catalog-data) los datos del catálogo
1. [Verificar](#4-verify-that-the-data-was-exported) que se exportaron los datos del catálogo
1. [Configurar](#5-configure-the-data) los datos
1. [Probar](#6-test-the-connection) la conexión
1. [Verificar](#7-validate-events-are-capturing-data) que los eventos están capturando datos
1. [Personalizar](#8-customize-for-your-storefront) tu tienda

## &#x200B;1. Instale la extensión [!DNL Live Search]

[!DNL Live Search] está instalado como una extensión desde [Adobe Marketplace](https://commercemarketplace.adobe.com/magento-live-search.html) hasta [Composer](https://getcomposer.org/). Después de instalar y configurar [!DNL Live Search], Adobe [!DNL Commerce] comienza a compartir los datos de la búsqueda y del catálogo con los servicios SaaS. En este punto, los usuarios de *Admin* pueden configurar, personalizar y administrar las facetas de búsqueda, los sinónimos y las reglas de comercialización.

>[!BEGINTABS]

>[!TAB Nueva instancia de Commerce]

Siga estas instrucciones si va a instalar [!DNL Live Search] en una nueva instancia de Commerce.

1. Confirme que se están ejecutando [trabajos cron](https://experienceleague.adobe.com/es/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs) y [indexadores](https://experienceleague.adobe.com/es/docs/commerce-admin/systems/tools/index-management).

1. Use Compositor para añadir el módulo de Live Search al proyecto:

   ```bash
   composer require magento/live-search --no-update
   ```

1. Actualice las dependencias e instale la extensión:

   ```bash
   composer update magento/live-search --with-dependencies
   ```

1. Deshabilite [!DNL OpenSearch] y los módulos relacionados temporalmente e instale [!DNL Live Search].

   ```bash
   bin/magento module:disable Magento_ Magento_Elasticsearch8 Magento_Elasticsearch7 Magento_OpenSearch Magento_ElasticsearchCatalogPermissions Magento_InventoryElasticsearch Magento_ElasticsearchCatalogPermissionsGraphQl
   ```

   [!DNL Elasticsearch] continúa administrando solicitudes de búsqueda desde la tienda mientras el servicio [!DNL Live Search] sincroniza los datos del catálogo e indexa los productos en segundo plano.

1. Instale las actualizaciones.

   ```bash
   bin/magento setup:upgrade
   ```

1. Compruebe que los siguientes [indexadores](https://experienceleague.adobe.com/es/docs/commerce-admin/systems/tools/index-management) estén configurados en &quot;Actualizar según lo programado&quot;:

   - Fuente de productos
   - Fuente de variante del producto
   - Fuente de atributos de catálogo
   - Fuente de precios de productos
   - Fuente de datos del sitio web Ámbitos
   - Fuente de datos de grupos de clientes ámbitos
   - Fuente de categorías
   - Fuente de permisos de categoría

Después de comprobar los indizadores, el siguiente paso es [configurar las claves API](#2-configure-api-keys).

>[!TAB Instancia de Commerce existente]

Siga estas instrucciones si está instalando [!DNL Live Search] en una instancia de Commerce existente.

1. Confirme que se están ejecutando [trabajos cron](https://experienceleague.adobe.com/es/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs) y [indexadores](https://experienceleague.adobe.com/es/docs/commerce-admin/systems/tools/index-management).

1. Use Compositor para añadir el módulo de Live Search al proyecto:

   ```bash
   composer require magento/live-search --no-update
   ```

1. Actualice las dependencias e instale la extensión:

   ```bash
   composer update magento/live-search --with-dependencies
   ```

1. Deshabilite los módulos [!DNL Live Search] que sirven a los resultados de búsqueda de tienda.

   ```bash
   bin/magento module:disable Magento_LiveSearchAdapter Magento_LiveSearchStorefrontPopover Magento_LiveSearchProductListing
   ```

   [!DNL Elasticsearch] continúa administrando solicitudes de búsqueda desde la tienda mientras el servicio [!DNL Live Search] sincroniza los datos del catálogo e indexa los productos en segundo plano.

1. Instale las actualizaciones.

   ```bash
   bin/magento setup:upgrade
   ```

1. Compruebe que los siguientes [indexadores](https://experienceleague.adobe.com/es/docs/commerce-admin/systems/tools/index-management) estén configurados en &quot;Actualizar según lo programado&quot;:

   - Fuente de productos
   - Fuente de variante del producto
   - Fuente de atributos de catálogo
   - Fuente de precios de productos
   - Fuente de datos del sitio web Ámbitos
   - Fuente de datos de grupos de clientes ámbitos
   - Fuente de categorías
   - Fuente de permisos de categoría

1. Habilite la extensión [!DNL Live Search] y deshabilite [!DNL OpenSearch] (módulos Magento Elasticsearch y OpenSearch).

   ```bash
   bin/magento module:enable Magento_LiveSearchAdapter Magento_LiveSearchStorefrontPopover  Magento_LiveSearchProductListing
   ```

   ```
   bin/magento module:disable Magento_Elasticsearch Magento_Elasticsearch6 Magento_Elasticsearch7 Magento_Elasticsearch8 Magento_OpenSearch Magento_ElasticsearchCatalogPermissions Magento_InventoryElasticsearch Magento_ElasticsearchCatalogPermissionsGraphQl
   ```

   >[!NOTE]
   >
   >El comando disable incluye la lista de módulos de Commerce que admiten OpenSearch. Si la instancia de Commerce no tiene un módulo instalado, verá un error de `module does not exist`.

1. Instale las actualizaciones.

   ```bash
   bin/magento setup:upgrade
   ```

Después de comprobar los indizadores, el siguiente paso es [configurar las claves API](#2-configure-api-keys).

>[!ENDTABS]

### Instalar la versión beta [!DNL Live Search]

>[!IMPORTANT]
>
>La siguiente función está en versión beta. Para participar en la versión beta, envía una solicitud por correo electrónico a [commerce-storefront-services](mailto:commerce-storefront-services@adobe.com).

Esta versión beta admite tres nuevas funciones en la consulta [`productSearch` ](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/):

- **Búsqueda por niveles** - Buscar en otro contexto de búsqueda - Con esta capacidad, puede realizar hasta dos niveles de búsqueda para sus consultas de búsqueda. Por ejemplo:

   - **Búsqueda de nivel 1** - Busque &quot;motor&quot; en &quot;product_attribute_1
   - **Búsqueda de nivel 2** - Busque &quot;número de pieza 123&quot; en &quot;product_attribute_2&quot;. En este ejemplo se busca &quot;número de pieza 123&quot; dentro de los resultados para &quot;motor&quot;.

  La búsqueda por capas está disponible tanto para la indexación de búsqueda `startsWith` como para la indexación de búsqueda `contains`, tal como se describe a continuación:

- **comienza con la indexación de búsqueda** - La búsqueda usa la indexación `startsWith`. Esta nueva capacidad permite:

   - Búsqueda de productos en los que el valor del atributo empieza con una cadena determinada.
   - Configuración de una búsqueda &quot;termina con&quot; para que los compradores puedan buscar productos en los que el valor del atributo termine con una cadena en particular. Para habilitar una búsqueda &quot;termina con&quot;, el atributo del producto debe ingerirse a la inversa, y la llamada de API también debe ser una cadena invertida.

- **contiene indización de búsqueda**: la búsqueda de un atributo mediante contiene indización. Esta nueva capacidad permite:

   - Búsqueda de una consulta dentro de una cadena más grande. Por ejemplo, si un comprador busca el número de producto PE-123 en la cadena HAPE-123.

     >[!NOTE]
     >
     >Este tipo de búsqueda es diferente de la [búsqueda de frases](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#phrase) existente, que realiza una búsqueda de autocompletar. Por ejemplo, si el valor de atributo del producto es &quot;pantalones de exterior&quot;, una búsqueda de frase devuelve una respuesta para &quot;sin bandeja&quot;, pero no devuelve una respuesta para &quot;u hormigas&quot;. Sin embargo, una búsqueda contiene sí devuelve una respuesta para &quot;o hormigas&quot;.

Estas nuevas condiciones mejoran el mecanismo de filtrado de consultas de búsqueda para restringir los resultados de búsqueda. Estas nuevas condiciones no afectan a la consulta de búsqueda principal.

Puede implementar estas nuevas condiciones en la página de resultados de búsqueda. Por ejemplo, puede agregar una nueva sección en la página donde el comprador pueda restringir aún más los resultados de búsqueda. Puede permitir que los compradores seleccionen atributos de producto específicos, como Fabricante, Número de pieza y Descripción. Desde allí, buscan dentro de esos atributos utilizando las condiciones `contains` o `startsWith`. Consulte la Guía de administración para obtener una lista de [atributos](https://experienceleague.adobe.com/es/docs/commerce-admin/catalog/product-attributes/attributes-input-types) en los que se pueden realizar búsquedas.

1. Para instalar la versión beta, agregue la siguiente dependencia al proyecto:

   ```bash
   composer require magento/module-live-search-search-types:"^1.0.0-beta1"
   ```

1. Confirme e inserte los cambios en los archivos de `composer.json` y `composer.lock` en su proyecto de nube. [Más información](https://experienceleague.adobe.com/es/docs/commerce-cloud-service/user-guide/configure-store/extensions#upgrade-an-extension).

   Esta versión beta agrega **[!UICONTROL Search types]** casillas de verificación para **[!UICONTROL Autocomplete]**, **[!UICONTROL Contains]** y **[!UICONTROL Starts with]** en el Administrador. También actualiza la API de GraphQL [`productSearch`](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-using-search-capability) para incluir estas nuevas funciones de búsqueda.

1. En el Administrador, [establezca un atributo de producto](https://experienceleague.adobe.com/es/docs/commerce-admin/catalog/product-attributes/product-attributes-add#step-5-describe-the-storefront-properties) en el que se pueda buscar y especifique la capacidad de búsqueda para ese atributo, como **Contiene** (predeterminado) o **Comienza con**. Puede especificar un máximo de seis atributos que se habilitarán para **Contiene** y seis atributos que se habilitarán para **Comienza con**. Para la versión beta, tenga en cuenta que el administrador no aplica esta restricción, pero sí en las búsquedas de API.

   ![Especificar la capacidad de búsqueda](./assets/search-filters-admin.png)

1. Consulte la [documentación para desarrolladores](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-using-search-capability) para obtener información sobre cómo actualizar las llamadas a la API [!DNL Live Search] mediante las nuevas funciones de búsqueda `contains` y `startsWith`.

### Descripciones de campos

| Campo | Descripción |
|--- |--- |
| `Autocomplete` | Habilitado de forma predeterminada y no se puede modificar. Con `Autocomplete`, puede usar `contains` en el [filtro de búsqueda](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering). En este caso, la consulta de búsqueda de `contains` devuelve una respuesta de búsqueda de tipo autocompletar. Adobe recomienda utilizar este tipo de búsqueda para los campos de descripción, que generalmente tienen más de 50 caracteres. |
| `Contains` | Habilita una búsqueda &quot;de texto contenido en una cadena&quot; verdadera en lugar de una búsqueda autocompletada. Use `contains` en el [filtro de búsqueda](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-using-search-capability). Consulte [Limitaciones](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#limitations) para obtener más información. |
| `Starts with` | Cadenas de consulta que comienzan con un valor en particular. Use `startsWith` en el [filtro de búsqueda](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-using-search-capability). |

## &#x200B;2. Configurar las claves API

La clave de API de Adobe Commerce y su clave privada asociada son necesarias para conectar [!DNL Live Search] a una instalación de Adobe Commerce. La clave de API se genera y se mantiene en la cuenta del titular de la licencia [!DNL Commerce], que puede compartirla con el desarrollador o el integrador de sistemas. A continuación, el desarrollador puede crear y administrar los espacios de datos SaaS en nombre del titular de la licencia. Si ya tiene un conjunto de claves API, no es necesario que las vuelva a generar.

Aprenda a configurar las claves API en el artículo [Conector de servicios de Commerce](../landing/saas.md).

## &#x200B;3. Sincronizar los datos del catálogo

[!DNL Live Search] mueve los datos del catálogo a la infraestructura SaaS de Adobe. Los datos se indexan y los resultados de búsqueda se envían desde este índice directamente a la tienda. Según el tamaño y la complejidad, la indexación puede tardar entre 30 minutos y un par de horas.

Para comenzar la sincronización inicial de los datos del catálogo con los servicios SaaS, ejecute los siguientes comandos en este orden:

```bash
bin/magento saas:resync --feed productattributes
bin/magento saas:resync --feed products
bin/magento saas:resync --feed scopesCustomerGroup
bin/magento saas:resync --feed scopesWebsite
bin/magento saas:resync --feed prices
bin/magento saas:resync --feed productoverrides
bin/magento saas:resync --feed variants
bin/magento saas:resync --feed categories
bin/magento saas:resync --feed categoryPermissions
```

Al ejecutar estos comandos, comienza la sincronización inicial de los datos del catálogo con los servicios SaaS.

>[!WARNING]
>
>Las operaciones de búsqueda y exploración de categorías no están disponibles durante la sincronización. El proceso puede tardar más de 1 hora según el tamaño del catálogo.

### Monitorización del progreso de sincronización

Use [Tablero de administración de datos](https://experienceleague.adobe.com/es/docs/commerce-admin/systems/data-transfer/data-dashboard) para supervisar el progreso de sincronización. Este tablero proporciona información valiosa sobre la disponibilidad de los datos del producto en su tienda, lo que garantiza que se puedan mostrar rápidamente a los clientes.

![Panel de administración de datos](assets/data-management-dashboard.png)

También puede ejecutar comandos de sincronización y solucionar problemas del proceso de sincronización mediante la [CLI de Commerce](../data-export/data-export-cli-commands.md#troubleshooting) y los registros de extensión de exportación de datos.

#### Futuras actualizaciones de productos

Después de la sincronización inicial, las actualizaciones incrementales de productos pueden tardar hasta 15 minutos en estar disponibles para la búsqueda de tiendas. Para obtener más información, consulte [Actualizaciones de productos de transmisión](indexing.md) en la documentación de indexación.

## &#x200B;4. Compruebe que los datos se han exportado

Para comprobar si los datos del catálogo se han exportado desde Adobe Commerce y se han sincronizado con [!DNL Live Search], tiene algunas opciones:

- Busque entradas en las tablas siguientes:

   - `cde_products_feed`
   - `cde_product_attributes_feed`

  >[!NOTE]
  >
  >Si recibe un error de `table does not exist`, busque las entradas en las tablas `catalog_data_exporter_products` y `catalog_data_exporter_product_attributes`. Estos nombres de tabla se usan en [!DNL Live Search] versiones anteriores a la 4.2.1.

- Use el [área de reproducción de GraphQL](https://experienceleague.adobe.com/es/docs/commerce/live-search/live-search-admin/graphql) con la consulta predeterminada (consulte [referencia de GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/) para obtener más información) para comprobar lo siguiente:

   - El recuento de productos devuelto está cerca de lo que se espera en la vista de la tienda.
   - Se devuelven las facetas.

Para obtener ayuda adicional, consulte [[!DNL Live Search] catálogo no sincronizado](https://experienceleague.adobe.com/es/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-catalog-data-sync) en la Base de conocimiento de soporte técnico.

## &#x200B;5. Configurar los datos

Configurar correctamente los datos del producto garantiza buenos resultados de búsqueda para los clientes. En esta sección, se habilitan los widgets de la lista de productos y se asignan categorías.

### Habilitar widgets de lista de productos

Al instalar [!DNL Live Search] 4.0.0+, los widgets de listas de productos se habilitan de forma predeterminada. Cuando los widgets están habilitados, se utiliza un componente de interfaz de usuario diferente para los resultados de búsqueda y las páginas de lista de productos de exploración de categorías. Este componente de interfaz de usuario realiza llamadas directas a la [API del servicio de catálogo](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/), lo que resulta en tiempos de respuesta más rápidos.

Si tiene una versión de [!DNL Live Search] anterior a la 4.0.0 o posterior, debe habilitar manualmente el widget de lista de productos.

1. Desde *Admin*, vaya a **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**.
1. En **[!UICONTROL Live Search]**, seleccione **[!UICONTROL Storefront Features]**.
1. Establezca **[!UICONTROL Enable Product Listing Widgets]** en `Yes`.

   ![Habilitar widgets de lista de productos](assets/ls-admin-enable-widget.png)

Al cambiar esta configuración, aparece el mensaje `Page cache is invalidated`. Debe vaciar la caché de Magento para guardar el cambio.

1. Para tener acceso a la página [Administración de caché](https://experienceleague.adobe.com/es/docs/commerce-admin/systems/tools/cache-management), siga uno de estos procedimientos:

   - Haga clic en el vínculo **[!UICONTROL Cache Management]** en el mensaje situado encima del área de trabajo.
   - En la barra lateral _Admin_, vaya a **[!UICONTROL System]** > _[!UICONTROL Tools]_>**[!UICONTROL Cache Management]**.

1. Seleccione la **configuración** [!UICONTROL Cache Type] y haga clic en **[!UICONTROL Flush Magento Cache]**.

   Los cambios en la tienda son inmediatos después de vaciar la caché.

### Asignar categorías

Los productos devueltos en [!DNL Live Search] deben asignarse a una [categoría](https://experienceleague.adobe.com/es/docs/commerce-admin/catalog/categories/categories). En Luma, por ejemplo, los productos se clasifican en categorías como &quot;Hombres&quot;, &quot;Mujeres&quot; y &quot;Equipos&quot;. También se configuran subcategorías para &quot;Tops&quot;, &quot;Bottom&quot; y &quot;Watches&quot;. Estas asignaciones de categoría mejoran la granularidad al filtrar.

## &#x200B;6. Compruebe la conexión

Con los datos del catálogo ahora en SaaS, pruebe para asegurarse de que los datos del producto se devuelvan en los siguientes casos:

- La casilla [!UICONTROL Search] devuelve los resultados correctamente
- La exploración de categorías devuelve los resultados correctamente
- Las facetas están disponibles como filtros en las páginas de resultados de búsqueda

Si todo funciona correctamente, [!DNL Live Search] está instalado, conectado y listo para usarse.

Si encuentra problemas en la tienda, compruebe en el archivo `var/log/system.log` si hay errores de comunicación de API o errores en el lado de los servicios.

Para permitir que [!DNL Live Search] pase a través de un firewall, agregue `commerce.adobe.io` a la lista de permitidos.

## &#x200B;7. Compruebe que los eventos capturan datos

Asegúrese de que los eventos de tienda implementados en el sitio funcionen. Esta comprobación es especialmente importante para implementaciones sin encabezado.

- Revise los [eventos](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#live-search) necesarios para [!DNL Live Search].
- Asegúrese de que el [tablero de Live Search](performance.md) muestre los datos de los entornos que no son de producción.
- [Verificar la colección de eventos](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/verify/).

## &#x200B;8. Personalizar para tu tienda

Ha instalado la extensión [!DNL Live Search], ha sincronizado, validado y configurado los datos. El siguiente paso es garantizar que los widgets de [!DNL Live Search] se ajusten al aspecto y la presentación de la tienda.

Puede aplicar estilo a los widgets de ventana emergente y PLP definiendo reglas CSS personalizadas según sea necesario. Ver [Elementos emergentes de estilo](storefront-popover.md#styling-popover-example) y [widget de página de lista de productos](plp-styling.md#styling-example).

Si desea ampliar la funcionalidad de los widgets, el código fuente de cada uno está disponible en un repositorio público.
En esta situación, puede personalizar JavaScript para sus propias necesidades y, a continuación, alojar su código personalizado en su CDN. Este script personalizado se comunica con el servicio [!DNL Live Search] y devuelve los resultados como de costumbre, lo que le permite controlar la funcionalidad del widget.

- [repositorio de widget PLP](https://github.com/adobe/storefront-product-listing-page)
- [Repositorio de la barra de búsqueda](https://github.com/adobe/storefront-search-as-you-type)

## Actualizando [!DNL Live Search]

Antes de actualizar [!DNL Live Search], compruebe la versión de [!DNL Live Search] que se instaló con Composer.

```bash
composer show magento/module-live-search | grep version
```

Para actualizar [!DNL Live Search], ejecute lo siguiente desde la línea de comandos:

```bash
composer update magento/live-search --with-dependencies
```

Para actualizar a una versión principal como de la 3.1.1 a la 4.0.0, edite el archivo raíz [!DNL Composer] `.json` del proyecto de la siguiente manera:

1. Si su versión de `magento/live-search` instalada actualmente es `3.1.1` o inferior y está actualizando a la versión `4.0.0` o superior, ejecute el siguiente comando antes de la actualización:

   ```bash
   bin/magento module:enable Magento_AdvancedSearch
   ```

   Para obtener información acerca de la versión de `magento/live-search` instalada actualmente, ejecute el siguiente comando:

   ```bash
   composer show magento/live-search
   ```

1. Abra el archivo raíz `composer.json` y busque `magento/live-search`.

1. En la sección `require`, actualice el número de versión de la siguiente manera:

   ```json
   "require": {
      ...
      "magento/live-search": "^4.0",
      ...
    }
   ```

1. Guardar `composer.json`. A continuación, ejecute lo siguiente desde la línea de comandos:

   ```bash
   composer update magento/live-search --with-dependencies
   ```

## Desinstalando [!DNL Live Search]

Para desinstalar [!DNL Live Search], consulte [Desinstalar módulos](https://experienceleague.adobe.com/es/docs/commerce-operations/installation-guide/tutorials/uninstall-modules).

## [!DNL Live Search] paquetes

La extensión [!DNL Live Search] consta de los siguientes paquetes:

| Paquete | Descripción |
|--- |--- |
| `module-live-search` | Permite a los comerciantes definir la configuración de búsqueda para facetas, sinónimos, reglas de consulta, etc., y proporciona acceso a un área de reproducción de GraphQL de solo lectura para probar consultas de *Admin*. |
| `module-live-search-adapter` | Enruta las solicitudes de búsqueda de la tienda al servicio [!DNL Live Search] y procesa los resultados en la tienda. <br /> - Examen de categorías - Enruta las solicitudes desde la tienda [navegación superior](https://experienceleague.adobe.com/es/docs/commerce-admin/catalog/catalog/navigation/navigation-top) al servicio de búsqueda.<br /> - Búsqueda global: enruta las solicitudes del campo [búsqueda rápida](https://experienceleague.adobe.com/es/docs/commerce-admin/catalog/catalog/search/search) al servicio [!DNL Live Search]. El campo de búsqueda rápida se encuentra en la esquina superior derecha de la página de la tienda. |
| `module-live-search-storefront-popover` | Una ventana emergente de &quot;búsqueda mientras escribe&quot; reemplaza la búsqueda rápida estándar y devuelve datos y miniaturas de los resultados de búsqueda principales. |

## Dependencias de [!DNL Live Search]

El metapaquete [!DNL Composer] para instalar la extensión [!DNL Live Search] incluye las siguientes dependencias de módulo.

- `magento/module-saas-catalog`
- `magento/module-saas-category`
- `magento/module-saas-category-permissions`
- `magento/module-saas-product-override`
- `magento/module-saas-product-variant`
- `magento/module-saas-price`
- `magento/module-saas-scopes`
- `magento/module-bundle-product-data-exporter`
- `magento/module-catalog-inventory-data-exporter`
- `magento/module-catalog-url-rewrite-data-exporter`
- `magento/module-configurable-product-data-exporter`
- `magento/module-parent-product-data-exporter`
- `magento/module-gift-card-product-data-exporter`
- `magento/module-bundle-product-override-data-exporter`
- `data-services`
- `services-id`

## Conceptos avanzados

Las secciones siguientes proporcionan temas más avanzados al utilizar [!DNL Live Search] y [!DNL Catalog Service].

### Extremo

[!DNL Live Search] se comunica a través del extremo en `https://catalog-service.adobe.io/graphql`.

Como [!DNL Live Search] no tiene acceso a la base de datos de productos completa, las API de GraphQL y Commerce Core GraphQL de [!DNL Live Search] no tienen paridad completa.

Adobe recomienda llamar a las API de SaaS directamente, específicamente al punto final del servicio de catálogo.

- Obtenga rendimiento y reduzca la carga del procesador omitiendo el proceso de Graphql/base de datos de Commerce
- Aproveche la federación [!DNL Catalog Service] para llamar a [!DNL Live Search], [!DNL Catalog Service] y [!DNL Product Recommendations] desde un único extremo.

En algunos casos de uso, es mejor llamar a [!DNL Catalog Service] para obtener detalles del producto y casos similares. Consulte [refineProduct](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/) para obtener más información.

Si tiene una implementación personalizada sin encabezado, consulte las implementaciones de referencia de [!DNL Live Search]:

- [widget PLP](https://github.com/adobe/storefront-product-listing-page)
- [[!DNL Live Search] campo](https://github.com/adobe/storefront-search-as-you-type)

La recopilación automática de datos de interacción del usuario no funciona de forma predeterminada si no se utilizan componentes estándar como el adaptador de búsqueda, los widgets de Luma o los widgets de CIF de AEM. Adobe Sensei utiliza estos datos recopilados para la comercialización inteligente y el seguimiento del rendimiento. Para resolver este problema, debe desarrollar una solución personalizada para implementar esta recopilación de datos de forma directa.

La última versión de [!DNL Live Search] ya usa [!DNL Catalog Service].

### Compatibilidad de idiomas

[!DNL Live Search] widgets admiten los siguientes idiomas:

|  |  |  |  |
|--- |--- |--- |--- |
| Idioma | Región | Código de idioma | Configuración regional de Magento |
| Búlgaro | Bulgaria | bg_BG | bg_BG |
| Catalán | España | ca_ES | ca_ES |
| Checo | República Checa | cs_CZ | cs_CZ |
| Danés | Dinamarca | da_DK | da_DK |
| Alemán | Alemania | de_DE | de_DE |
| Griego | Grecia | el_GR | el_GR |
| Inglés | Reino Unido | en_GB | en_GB |
| Inglés | Estados Unidos | en_US | en_US |
| Español | España | es_ES | es_ES |
| Estonio | Estonia | et_EE | et_EE |
| Vasco | España | eu_ES | eu_ES |
| persa | Irán | fa_IR | fa_IR |
| Finés | Finlandia | fi_FI | fi_FI |
| francés | Francia | fr_FR | fr_FR |
| Gallego | España | gl_ES | gl_ES |
| Hindi | India | hi_IN | hi_IN |
| Húngaro | Hungría | hu_HU | hu_HU |
| Indonesio | Indonesia | id_ID | id_ID |
| Italiano | Italia | it_IT | it_IT |
| Coreano | Corea del Sur | ko_KR | ko_KR |
| Lituano | Lituania | lt_LT | lt_LT |
| Letón | Letonia | lv_LV | lv_LV |
| Noruego | Noruega Bokmal | nb_NO | nb_NO |
| Neerlandés | Países Bajos | nl_NL | nl_NL |
| Polaco | Polonia | pl_PL | pl_PL |
| Portugués | Brasil | pt_BR | pt_BR |
| Portugués | Portugal | pt_PT | pt_PT |
| Rumano | Rumanía | ro_RO | ro_RO |
| Ruso | Rusia | ru_RU | ru_RU |
| Sueco | Suecia | sv_SE | sv_SE |
| Tailandés | Tailandia | th_TH | th_TH |
| Turco | Turquía | tr_TR | tr_TR |
| Chino | China | zh_CN | zh_Hans_CN |
| Chino | Taiwán | zh_TW | zh_Hant_TW |

Si el widget detecta que la configuración del idioma de administración de Commerce coincide con un idioma compatible, establece de forma predeterminada ese idioma. De lo contrario, el widget se establece en inglés de forma predeterminada. En el Administrador, la configuración de idioma se establece navegando hasta _[!UICONTROL Stores]_> [!UICONTROL Settings] >_[!UICONTROL Configuration]_ > _[!UICONTROL General]_> [!UICONTROL Country Options].

Los administradores también pueden establecer el idioma de [índice de búsqueda](settings.md#language) para garantizar mejores resultados de búsqueda.

### Repositorio de código Widget

El código del widget de página de lista de productos y del widget de campo [!DNL Live Search] está disponible para su descarga en GitHub.

Los desarrolladores que tienen acceso al código pueden personalizar completamente su funcionamiento y aspecto. Alojan el código en sus propios servidores pero siguen usando el servicio [!DNL Live Search].

- [widget PLP](https://github.com/adobe/storefront-product-listing-page)
- [Barra de búsqueda](https://github.com/adobe/storefront-search-as-you-type)

### Extensión de Data Export

Una vez habilitado [!DNL Live Search], la extensión de exportación de datos sincroniza los datos de Commerce entre la aplicación de Commerce y [!DNL Live Search]. Este proceso garantiza que los datos de Commerce más actuales estén disponibles en la tienda. En Admin, puede comprobar el estado de la sincronización mediante el panel de control de Data Management. Puede administrar y solucionar problemas del proceso de exportación de datos mediante la CLI de Commerce y los registros. Para obtener más información, consulte la [Guía de exportación de datos](../data-export/overview.md).

### Inventory management

[!DNL Live Search] admite las funciones de [Inventory management](https://experienceleague.adobe.com/es/docs/commerce-admin/inventory/introduction) en Commerce (anteriormente conocido como Multi-Source Inventory o MSI). Para habilitar la compatibilidad total, debe [actualizar](install.md#updating-live-search) el módulo de dependencia `commerce-data-export` a la versión 102.2.0+.

[!DNL Live Search] devuelve un valor booleano que indica si un producto está disponible en Inventory management, pero no contiene información sobre el origen que tiene las existencias.

### Indexador de precios

Los clientes de [!DNL Live Search] pueden usar el [indexador de precios SaaS](../price-index/price-indexing.md), que proporciona actualizaciones de cambio de precios y tiempo de sincronización más rápidos.

### Tarifa soportada

[!DNL Live Search] widgets admiten la mayoría de los tipos de precios admitidos por Adobe Commerce, pero no todos.

Actualmente, se admiten precios básicos. Los precios avanzados que no son compatibles son:

- Coste
- Precio Mínimo Anunciado

Consulte [Malla de API](../catalog-service/mesh.md) para cálculos de precios más complejos.

El formato de precio admite la configuración regional en la instancia de Commerce: *Tiendas* > Configuración > *Configuración* > General > *General* > Opciones locales > Configuración regional.

### Compatibilidad con tienda sin encabezado

Opcionalmente, es posible que tenga que instalar el módulo `module-data-services-graphql` que expande la cobertura de GraphQL existente de la aplicación para incluir los campos necesarios para la recopilación de datos de comportamiento de la tienda.

```bash
composer require magento/module-data-services-graphql
```

Este módulo agrega contextos adicionales a las consultas de GraphQL:

- `dataServicesStorefrontInstanceContext`
- `dataServicesMagentoExtensionContext`
- `dataServicesStoreConfigurationContext`

### Compatibilidad con B2B

[!DNL Live Search] admite [funcionalidad B2B](https://experienceleague.adobe.com/es/docs/commerce-admin/b2b/guide-overview) con [limitaciones](boundaries-limits.md#b2b-and-category-permissions) adicionales.

### Compatibilidad con PWA

[!DNL Live Search] funciona con PWA Studio, pero los usuarios pueden ver pequeñas diferencias en comparación con otras implementaciones de Commerce. La funcionalidad básica, como la página de búsqueda y la lista de productos, funciona en Venia, pero es posible que algunas permutaciones de Graphql no funcionen correctamente. También puede haber diferencias de rendimiento.

- La implementación actual de PWA de [!DNL Live Search] requiere más tiempo de procesamiento para devolver resultados de búsqueda que [!DNL Live Search] con la tienda nativa de Commerce.
- [!DNL Live Search] en PWA no admite [administración de eventos](https://developer.adobe.com/commerce/services/shared-services/storefront-events/sdk/). Como resultado, los informes de búsqueda y la comercialización inteligente no funcionan en las tiendas de PWA.
- Al usar [PWA Studio](https://developer.adobe.com/commerce/pwa-studio/), GraphQL no admite el filtrado directamente en `description`, `name`, `short_description`, pero estos campos se pueden devolver con un filtro más general.

Para usar [!DNL Live Search] con PWA Studio, los integradores también deben:

1. Instalar [livessearch-storefront-utils](https://www.npmjs.com/package/@magento/ds-livesearch-storefront-utils).
1. Establezca `environmentId` en el objeto `storeDetails`.

   ```javascript
   const storeDetails: StoreDetailsProps = {
       environmentId: <Storefront_ID>,
       websiteCode: "base",
       storeCode: "main_website_store",
       storeViewCode: "default",
       searchUnitId: searchUnitId,
       config: {
           minQueryLength: 5,
           pageSize: 8,
           currencySymbol: "$",
           },
       };
   ```

### Cookies

[!DNL Live Search] recopila datos de interacción del usuario para mejorar la funcionalidad de búsqueda y almacena esta información en cookies del explorador. Esta recopilación de datos requiere el consentimiento del usuario cuando las restricciones de cookies están habilitadas. [!DNL Live Search] y [!DNL Product Recommendations] comparten el mismo mecanismo de recopilación de datos y administración de cookies. Para obtener más información sobre las restricciones de cookies y el cumplimiento de la privacidad, consulte [Administrar restricciones de cookies](../product-recommendations/setting-cookie.md).
