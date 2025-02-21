---
title: Indexación
description: Obtenga información sobre cómo  [!DNL Live Search] indexa las propiedades de atributos de productos.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '739'
ht-degree: 0%

---

# Indexación

El proceso de indexación [!DNL Live Search] lee el catálogo en busca de atributos de productos y genera un índice para que los productos puedan buscarse, filtrarse y presentarse rápidamente.

Las propiedades de atributos del producto (metadatos) determinan:

* Uso de un atributo en el catálogo
* Su aspecto y comportamiento en la tienda
* Los datos que se incluyen en las operaciones de transferencia de datos

El ámbito de los metadatos de atributo es `website/store/store view`.

La API [!DNL Live Search] permite que un cliente ordene por cualquier atributo de producto que tenga la propiedad [storefront](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/product-attributes) `Use in Search` establecida en `Yes` en el administrador de Adobe Commerce. Cuando está habilitado, se puede establecer `Search Weight` para el atributo.

[!DNL Live Search] no indiza los productos eliminados o los productos establecidos en `Not Visible Individually`.

>[!NOTE]
>
> Los clientes de Commerce con [!DNL Live Search] pueden aprovechar las actualizaciones de precios más rápidas y el tiempo de sincronización en sus sitios web con el [indexador de precios SaaS](../price-index/price-indexing.md).

## Indexando canalización

El cliente llama al servicio de búsqueda desde la tienda para recuperar metadatos de índice (filtrables, ordenables). El servicio de búsqueda solo puede llamar a los atributos de producto que permiten búsqueda con la propiedad *Usar en navegación por capas* establecida en `Filterable (with results)` y *Usar para ordenar en lista de productos* establecida en `Yes`.

Para construir una consulta dinámica, el servicio de búsqueda necesita saber qué atributos se pueden buscar y su [peso](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search-results). [!DNL Live Search] respeta los pesos de búsqueda de Adobe Commerce (1-10, donde 10 es la prioridad más alta). La lista de datos sincronizados y compartidos con el servicio de catálogo se encuentra en el esquema, que se define en:

`vendor/magento/module-catalog-data-exporter/etc/et_schema.xml`

![[!DNL Live Search] indexando diagrama de búsqueda de cliente](assets/indexing-pipeline.svg)

1. Compruebe si el comerciante tiene derechos para [!DNL Live Search].
1. Obtenga vistas de la tienda con cambios en los metadatos de atributos.
1. Almacenar atributos de indexación.
1. Reindexe el índice de búsqueda.

### Índice completo

Si [!DNL Live Search] se configura y sincroniza durante la incorporación, el índice inicial puede tardar hasta 60 minutos en generarse. Los catálogos grandes pueden tardar más en indexarse. El proceso comienza después de que `cron` envíe la fuente y termina de ejecutarse.

Los siguientes eventos almacenan en déclencheur una sincronización completa y la generación de índices:

* Incorporando [sincronización de datos del catálogo](install.md#synchronize-catalog-data)
* Cambios en los metadatos de atributos

Por ejemplo, al cambiar la propiedad `Use in Search` del atributo `color` de `No` a `Yes`, los metadatos del atributo se cambian a `searchable=true` y se déclencheur una sincronización y reindexación completas. El siguiente déclencheur de metadatos de atributo genera una sincronización y reindexación completas cuando se cambia:

* `filterableInSearch`
* `searchable`
* `sortable`
* `visibleInSearch`

### Transmisión de actualizaciones de productos

Una vez que se haya creado el índice inicial durante la [incorporación](install.md#synchronize-catalog-data), las siguientes actualizaciones incrementales del producto se sincronizan y reindexan continuamente:

* Nuevos productos añadidos al catálogo
* Cambios en los valores de atributos del producto

Por ejemplo, agregar un nuevo valor de muestra al atributo `color` se administra como una actualización de producto de flujo continuo.

Flujo de trabajo de actualización de streaming:

1. Los productos actualizados se sincronizan desde la instancia de Adobe Commerce al servicio de catálogo.
1. El servicio de indexación busca continuamente actualizaciones de productos del servicio de catálogo. Los productos actualizados se indexan a medida que llegan al servicio de catálogo.
1. La actualización de un producto puede tardar hasta 15 minutos en estar disponible en [!DNL Live Search].

#### Actualizaciones que afectan a la visibilidad del producto

Cuando se actualizan las opciones de configuración de administración de [!DNL Live Search], las opciones de configuración de administración de Adobe Commerce o los datos del catálogo, es probable que se produzca un retraso antes de que los cambios aparezcan en la tienda.

En la tabla siguiente se describen varios cambios y el tiempo de espera aproximado antes de que aparezcan en la tienda.

| Actualizaciones | Retraso hasta que sea visible en la tienda |
|---|---|
| [!DNL Live Search] cambios de administrador en las facetas, la configuración de precios, las reglas de comercialización de categoría o búsqueda. | 15-20 minutos. |
| [!DNL Live Search] cambios de administrador que requieren reindexación: configuración de idioma o sinónimos. | Hasta 15 minutos después de que se haya completado la reindexación. |
| Cambios del administrador de Adobe Commerce que requieren una reindexación completa: metadatos de atributo que se pueden buscar, ordenar o filtrar | Hasta 15 minutos después de que se haya completado la reindexación. |
| Cambios incrementales en los datos del catálogo que no necesitan reindexación: inventario de productos, precio, nombre, etc. | Hasta 15 minutos después de que el índice de búsqueda elástica se actualice con los datos más recientes. |

## Búsqueda de clientes

La API [!DNL Live Search] permite a un cliente ordenar por cualquier atributo de producto ordenable estableciendo la propiedad [storefront](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/product-attributes), *usada para ordenar en listas de productos* a `Yes`. Según el tema, esta configuración hace que el atributo se incluya como opción en el control de paginación [Ordenar por](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/navigation/navigation) en las páginas del catálogo. [!DNL Live Search] puede indizar hasta 200 atributos de productos, con [propiedades de tienda](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/product-attributes) en las que se pueden realizar búsquedas y filtros.

Los metadatos de índice se almacenan en la canalización de indexación y el servicio de búsqueda puede acceder a ellos.

![[!DNL Live Search] diagrama de API de metadatos de índice](assets/index-metadata-api.svg)

### Flujo de trabajo de atributos ordenables

1. El cliente llama al servicio de búsqueda.
1. El servicio de búsqueda llama al servicio de administración de búsquedas.
1. El servicio de búsqueda llama a la canalización de indexación.

## Indexado para todos los productos

El orden de los campos de esta lista refleja el orden típico de las columnas en los datos de productos exportados.

* `environment_id`
* `website_code`
* `store_code`
* `store_view_code`
* `product_id`
* `sku`
* `name`
* `type`
* `displayable`
* `deleted`
* `url`
* `currency`
* `meta_description`
* `meta_keyword`
* `meta_title`
* `description`
* `short_description`
* `weight`
* `image`
* `small_image`
* `thumbnail_image`
* `prices`
* `in_stock`
* `low_stock`

El siguiente campo está indexado para todos los productos configurables:

* `childrenSkus`
