---
title: Referencia de esquema de tabla de fuentes
description: Obtenga información acerca del esquema de tabla de fuentes que usa [!DNL SaaS Data Export]  para hacer un seguimiento del estado de los elementos de fuente, el estado de exportación y los detalles del error.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Services
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: c70c1643afbf8e9633df89a613d6798416c8eb44
workflow-type: tm+mt
source-wordcount: 429
ht-degree: 0%

---


# Referencia de esquema de tabla de fuentes

Cada fuente tiene una tabla MySQL dedicada en la base de datos [!DNL Adobe Commerce]. Todas las tablas de fuentes comparten la misma estructura de columnas. En la tabla siguiente se muestra cada fuente con su nombre de fuente CLI, ID del indexador y nombre de tabla de fuentes.

## Fuentes compatibles

La lista real de fuentes depende del paquete [!DNL SaaS Data Export] instalado.


| Fuente (`--feed`) | Finalidad | Identificador de indizador | Tabla de fuentes | Modo de exportación |
| --- | ------------------------------------------------------------------- | --- | --- | --- |
| `products` | Catálogo de productos (atributos, categorías, imágenes, etc.) | `catalog_data_exporter_products` | `cde_products_feed` | Inmediato |
| `productAttributes` | Definiciones de atributos y metadatos. Se utiliza para definir el esquema de búsqueda. | `catalog_data_exporter_product_attributes` | `cde_product_attributes_feed` | Inmediato |
| `categories` | Datos de categorías | `catalog_data_exporter_categories` | `cde_categories_feed` | Inmediato |
| `prices` | Precios de productos con precios de grupo de clientes y precios de nivel | `catalog_data_exporter_product_prices` | `cde_product_prices_feed` | Inmediato |
| `variants` | Variantes de producto configurables | `catalog_data_exporter_product_variants` | `cde_product_variants_feed` | Inmediato |
| `scopesWebsite` | Sitio web con códigos de vista de tienda | `scopes_website_data_exporter` | `scopes_website_data_exporter` | Heredado |
| `scopesCustomerGroup` | Definiciones de grupos de clientes | `scopes_customergroup_data_exporter` | `scopes_customergroup_data_exporter` | Heredado |
| `productOverrides` | Permisos de productos calculados | `catalog_data_exporter_product_overrides` | `cde_product_overrides_feed` | Inmediato |
| `categoryPermissions` *(EE)* | Datos de permisos de categoría sin procesar | `catalog_data_exporter_category_permissions` | `cde_category_permissions_feed` | Inmediato |
| `orders` | Estado de pedidos de ventas | `sales_order_data_exporter_v2` | `sales_data_exporter_orders_v2` | Heredado |

La columna **Modo de exportación** indica cómo cada fuente recopila y envía datos:

- **Fuentes en modo inmediato**: recopile datos, omita los elementos sin modificar mediante hashes de contenido (anulación de duplicación de hash) y envíe actualizaciones en la misma ejecución del indizador.
- **Fuentes en modo heredado** (`scopesWebsite`, `scopesCustomerGroup`, `orders`): almacene primero los datos ensamblados en la tabla de fuentes y envíelos mediante un trabajo cron independiente.

Consulte [Modos de sincronización](../sync-overview.md#synchronization-modes).

## Esquema

| Columna | Tipo | Descripción |
| --- | --- | ---------------- |
| `id` | INT (PK) | Incremento automático de la clave principal |
| `source_entity_id` | INT | ID de entidad de la tabla de origen de Commerce (por ejemplo, `catalog_product_entity.entity_id`) |
| `feed_id` | VARCHAR | Identificador único de un elemento de fuente. Se calcula como un hash de los campos de identidad del elemento (por ejemplo, `sku + storeViewCode`), no como un valor de incremento automático. |
| `feed_data` | JSON | Carga útil de fuente para este elemento. Solo se rellena la información mínima como identificador de entidad y ámbito. Cuando se establece `PERSIST_EXPORTED_FEED=1`, se almacena la carga útil completa. |
| `feed_hash` | VARCHAR | Hash de contenido utilizado para la detección de cambios. Calculado desde la carga útil, excluyendo las marcas de tiempo (`modifiedAt`, `updatedAt`). Si el hash coincide con la exportación anterior, el elemento no se vuelve a enviar. |
| `is_deleted` | TINYINT | Marcador de eliminación suave. Se establece en `1` cuando la entidad se elimina en Commerce. |
| `modified_at` | TIMESTAMP | Última vez que se modificó este elemento de fuente |
| `status` | INT | Código de estado de envío del último intento de exportación. Consulte [Envío de fuentes y administración de errores HTTP](../sync-overview.md#feed-submission-and-http-error-handling). |
| `errors` | TEXTO | Detalles de error con codificación JSON devueltos por el servicio SaaS para este artículo |
| `metadata` | JSON | Indicadores de sincronización interna e información de metadatos de bloqueo utilizados por el marco de exportación |

## Consultas de diagnóstico comunes

Utilice las siguientes consultas SQL para inspeccionar directamente el estado de la tabla de fuentes. Reemplace valores de marcador de posición como `<SKU>`, `<ATTRIBUTE_CODE>` y `<CATEGORY_ID>` por valores reales de su entorno. Consulte [Fuentes compatibles](#supported-feeds) para obtener una lista completa de los nombres de las tablas.

**Fuente de productos — por SKU:**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.sku') AS 'SKU',
       JSON_EXTRACT(f.feed_data, '$.storeViewCode') AS 'store view code',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_products_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.sku') IN ('<SKU>');
```

**Fuente de atributos de producto por código de atributo:**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.attributeCode') AS 'code',
       JSON_EXTRACT(f.feed_data, '$.storeViewCode') AS 'store view code',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_product_attributes_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.attributeCode') IN ('<ATTRIBUTE_CODE>');
```

**Fuente de precios — por SKU:**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.sku') AS 'SKU',
       JSON_EXTRACT(f.feed_data, '$.websiteCode') AS 'website code',
       JSON_EXTRACT(f.feed_data, '$.customerGroupCode') AS 'customer group code',
       IFNULL(cg.customer_group_code, '-- (base price)') AS 'AC customer group',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_product_prices_feed f
LEFT JOIN customer_group cg
       ON sha1(cg.customer_group_id) = JSON_EXTRACT(f.feed_data, '$.customerGroupCode')
WHERE JSON_EXTRACT(f.feed_data, '$.sku') IN ('<SKU>');
```

**Fuente de invalidaciones de productos — por SKU:**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.sku') AS 'SKU',
       JSON_EXTRACT(f.feed_data, '$.websiteCode') AS 'website code',
       JSON_EXTRACT(f.feed_data, '$.customerGroupCode') AS 'customer group code',
       IFNULL(cg.customer_group_code, 'NA (deleted)') AS 'AC customer group',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_product_overrides_feed f
LEFT JOIN customer_group cg
       ON sha1(cg.customer_group_id) = JSON_EXTRACT(f.feed_data, '$.customerGroupCode')
WHERE JSON_EXTRACT(f.feed_data, '$.sku') IN ('<SKU>');
```

Fuente de **categorías — por id. de categoría:**

```sql
SELECT JSON_EXTRACT(feed_data, '$.categoryId') AS 'Category ID',
       JSON_EXTRACT(f.feed_data, '$.storeViewCode') AS 'store view code',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_categories_feed f
WHERE JSON_EXTRACT(feed_data, '$.categoryId') IN (<CATEGORY_ID>);
```

**Fuente de variantes — por SKU de producto configurable:**

```sql
SELECT JSON_EXTRACT(feed_data, '$.parentSku') AS 'configurable SKU',
       JSON_EXTRACT(feed_data, '$.productSku') AS 'Variant SKU',
       JSON_EXTRACT(f.feed_data, '$.optionValues') AS 'options',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_product_variants_feed f
WHERE JSON_EXTRACT(feed_data, '$.parentSku') = '<SKU>';
```


>[!MORELIKETHIS]
>
>- [Sincronizar datos con la exportación de datos SaaS](../sync-overview.md)
>- [Ver y administrar la sincronización](../data-sync-manage.md)
>- [Sincronizar fuentes usando la CLI de Commerce](../data-export-cli-commands.md)
