---
title: Referencia de esquema de tabla de fuentes
description: Obtenga información acerca del esquema de tabla de fuentes que usa  [!DNL Adobe Commerce Optimizer Connector]  para hacer un seguimiento del estado del elemento de fuente, el estado de exportación y los detalles del error.
autotag-review: '2026-06-23T00:00:00.000Z'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2: id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: c32adafa-ed01-4b31-997e-2413013911b0id: cc250cf1-34eb-4863-80d0-d170d45ea067
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 19de20caafd45e3a00896d0d4b29b7e96dfe94e1
workflow-type: tm+mt
source-wordcount: 324
ht-degree: 0%

---


# Referencia de esquema de tabla de fuentes

Cada fuente tiene una tabla MySQL dedicada en la base de datos [!DNL Adobe Commerce]. Todas las tablas de fuentes comparten la misma estructura de columnas.

## Fuentes compatibles

Para obtener la lista completa de fuentes admitidas con extremos de API, límites de lotes, nombres de indizador y nombres de tabla de fuentes, consulte [Módulos de conector y extremos de fuente](connector-reference.md#supported-feeds).

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
| `status` | INT | Código de estado de envío del último intento de exportación. Consulte [Envío de fuentes y administración de errores](../connector-sync-pipeline.md#feed-submission-and-error-handling). |
| `errors` | TEXTO | Detalles de error con codificación JSON devueltos por la API [!DNL Commerce Optimizer] para este elemento |
| `metadata` | JSON | Indicadores de sincronización interna e información de metadatos de bloqueo utilizados por el marco de exportación |

## Consultas de diagnóstico comunes

Utilice las siguientes consultas SQL para inspeccionar directamente el estado de la tabla de fuentes. La columna `feed_data` almacena datos en el formato de API [!DNL Adobe Commerce Optimizer]. Reemplace valores de marcador de posición como `<SKU>`, `<ATTRIBUTE_CODE>`, `<SLUG>` y `<PRICE_BOOK_ID>` por valores reales de su entorno.

**Fuente de productos - por SKU:**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.sku') AS 'SKU',
       JSON_EXTRACT(f.feed_data, '$.source.locale') AS 'locale',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_products_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.sku') IN ('<SKU>');
```

**Fuente de atributos de producto - por código de atributo:**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.code') AS 'code',
       JSON_EXTRACT(f.feed_data, '$.source.locale') AS 'locale',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_product_attributes_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.code') IN ('<ATTRIBUTE CODE>');
```

Fuente de **categorías - por ruta de dirección URL:**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.slug') AS 'slug',
    JSON_EXTRACT(f.feed_data, '$.source.locale') AS 'locale',
    f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_categories_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.slug') IN ('<SLUG>');
```

**Fuente de precios - por SKU:**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.sku') AS 'SKU',
       JSON_EXTRACT(f.feed_data, '$.priceBookId') AS 'price book ID',
       f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_product_prices_feed f
WHERE JSON_EXTRACT(f.feed_data, '$.sku') IN ('<SKU>');
```

**Fuente de libros de precios - por identificador de libro de precios:**

```sql
SELECT JSON_EXTRACT(f.feed_data, '$.priceBookId') AS 'price book ID',
    JSON_EXTRACT(f.feed_data, '$.name') AS 'name',
    JSON_EXTRACT(f.feed_data, '$.parentId') AS 'parent price book ID',
    JSON_EXTRACT(f.feed_data, '$.currency') AS 'currency',
    f.status, f.modified_at, f.is_deleted, f.errors
FROM cde_price_books_feed f
WHERE JSON_UNQUOTE(JSON_EXTRACT(f.feed_data, '$.priceBookId'))  IN ('<PRICE_BOOK_ID>');
```

>[!MORELIKETHIS]
>
>- [Módulos de conector y extremos de fuente](connector-reference.md)
>- [Canalización de sincronización de conectores](../connector-sync-pipeline.md)
>- [Administrar sincronización](../data-sync-manage.md)
>- [Asignación de campos para fuentes de conectores](field-mapping.md)
