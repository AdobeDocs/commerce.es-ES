---
title: Asignación de campos para  [!DNL Adobe Commerce Optimizer Connector] fuentes
description: Obtenga información acerca de la asignación de campos  [!DNL Adobe Commerce Optimizer Connector] de [!DNL Adobe Commerce] datos de catálogo a [!DNL Adobe Commerce Optimizer] formatos de API de ingesta para todas las fuentes.
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."
autotag-review: '2026-06-09T15:49:03.934Z'
TQID: 'https://experienceleague.adobe.com/SOWOnguudhqzX-r66nGUqc-WKet5qq6GRV11ADx0Me4'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: e7dae43f-215c-4cdf-90d3-c5a461a6e669id: c32adafa-ed01-4b31-997e-2413013911b0
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: e0eb8757-182f-49f3-94a4-1587d16f5094id: b23e006f-0a29-4f1d-8fd0-77aa56f3d12b
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 665
ht-degree: 0%

---


# Asignación de campos para fuentes de conector

Esta página documenta cómo [!DNL Adobe Commerce Optimizer Connector] transforma los campos del catálogo [!DNL Adobe Commerce] en el formato requerido por [!DNL Commerce Optimizer] [!DNL Catalog Data Ingestion API]. Consulte la [referencia de conector](connector-reference.md#supported-feeds) para ver la lista de fuentes admitidas y sus extremos de API.

## Productos

La fuente `products` envía datos al extremo [Products](https://developer.adobe.com/commerce/services/reference/rest/#tag/Products){target="_blank"}.

| [!DNL Adobe Commerce] campo | Campo de API [!DNL Commerce Optimizer] | Notas |
| ----------------------------------------------- | -------------- | ------- |
| `sku` | `sku` | |
| `storeViewCode` | `source/locale` | |
| `name` | `name` | |
| `urlKey` | `slug` | |
| `productId` | `externalIds[0].id` | `origin` se corrigió a `"AdobeCommerce"` |
| `status` | `status` | En mayúsculas; se establece en `DISABLED` para productos compuestos sin elementos secundarios asignados |
| `description` | `description` | |
| `shortDescription` | `shortDescription` | |
| `visibility` | `visibleIn` | Dividir y asignar valores separados por comas: `Catalog`→`CATALOG`, `Search`→`SEARCH`; valores no asignados quitados |
| `metaTitle` | `metaTags/title` | |
| `metaDescription` | `metaTags/description` | |
| `metaKeyword` | `metaTags/keywords` | Cadena delimitada por una nueva línea dividida en matriz |
| `inStock`, `lowStock`, `weight`, `weightUnit` | `attributes[].code = "aco_ac_attributes"` | Objeto con codificación JSON `{inStock, lowStock, weight, weightType}`; siempre presente como la primera entrada de atributo |
| `attributes[]` | `attributes[]` | Se excluyen todas las entradas asignadas a `{code, values[], variantReferenceId}`; `inStock`, `lowStock`, `weight`, `weightType` (van a `aco_ac_attributes`) |
| `images[]` | `images[]` | `url`, `label`; funciones estándar asignadas: `image`→`BASE`, `small_image`→`SMALL`, `thumbnail`→`THUMBNAIL`, `swatch_image`→`SWATCH`; las funciones no estándar van a `customRoles[]` |
| `categoryData[].categoryPath` | `routes[].path` | |
| `categoryData[].productPosition` | `routes[].position` | |
| `links[].type` + `links[].sku` | `links[]` | `type` en mayúscula; se perdieron las entradas sin `sku` |
| `parents[].productType` + `parents[].sku` | `links[]` | Tipo asignado: `configurable`→`VARIANT_OF`, `bundle`/`bundle_fixed`→`IN_BUNDLE` |
| `configurable options` | `configurations[]` | `id`→`attributeCode`, `label`; tipo de opción `SWATCH` cuando `swatchType` está establecido; de lo contrario, `CONFIGURABLE`; variante predeterminada de `isDefault`; los valores incluyen `variantReferenceId`, `label`, `colorHex`, `imageUrl` |
| `bundle options` | `bundles[]` | `label`→`group`; `required`; `renderType` `checkbox`/`multi`→`multiSelect: true`; SKU predeterminadas de `isDefault`; los elementos incluyen `sku`, `qty`, `userDefinedQty` (`qtyMutability`) |

## Metadatos de atributos de producto

La fuente `productAttributes` envía datos a [extremo de metadatos](https://developer.adobe.com/commerce/services/reference/rest/#tag/Metadata){target="_blank"}.


| [!DNL Adobe Commerce] campo | Campo de API [!DNL Commerce Optimizer] | Notas |
| --------------- | -------------- | ------- |
| `attributeCode` | `code` | |
| `storeViewCode` | `source/locale` | |
| `label` | `label` | |
| `dataType` + `frontendInput` | `dataType` | Consulte la tabla de conversión a continuación |
| `visible` | `visibleIn: "PRODUCT_DETAIL"` | Se agregó a la matriz al `true` |
| `visibleInSearch` | `visibleIn: "SEARCH_RESULTS"` | Se agregó a la matriz al `true` |
| `visibleInListing` | `visibleIn: "PRODUCT_LISTING"` | Se agregó a la matriz al `true` |
| `visibleInCompareList` | `visibleIn: "PRODUCT_COMPARE"` | Se agregó a la matriz al `true` |
| `filterable` | `filterable` | |
| `sortable` | `sortable` | |
| `searchable` | `searchable` | |
| `searchWeight` | `searchWeight` | |
| `searchTypes` | `searchTypes` | |

### Conversión de tipo de datos

El conector deriva la API `dataType` de los campos Commerce `dataType` y `frontendInput` de la tabla de asignación anterior. La siguiente tabla muestra las reglas de conversión que aplica el conector.

| [!DNL Adobe Commerce] `dataType` | [!DNL Adobe Commerce] `frontendInput` | [!DNL Commerce Optimizer] API `dataType` |
| -------------------- | -------------------------- | ------------------- |
| `int` | `boolean` | `BOOLEAN` |
| `int` | `text` o `select` | `TEXT` |
| `int` | cualquier otro | `INTEGER` |
| `decimal` | - | `DECIMAL` |
| `text`, `varchar`, `static`, `datetime` | - | `TEXT` |
| `OBJECT` | - | `OBJECT` |
| cualquier otro | - | `TEXT` |

>[!NOTE]
>
>Cuando la `dataType` de un atributo se establece en `OBJECT`, la API de [productos](https://developer.adobe.com/commerce/services/reference/graphql/#products){target="_blank"} trata el valor del atributo como un objeto estructurado en lugar de como una cadena sin formato. En el momento de la consulta, la API intenta analizar el valor almacenado como JSON. Si el análisis se realiza correctamente, el resultado se devuelve como un objeto anidado en la respuesta. **Este comportamiento es especialmente útil** cuando se proporcionan atributos personalizados de forma dinámica, por ejemplo, para transportar datos estructurados o de varios campos que no se pueden representar como un valor escalar. Para obtener instrucciones, consulte [Agregar atributos de producto dinámicamente](../../data-export/add-attribute-dynamically.md).

## Libros de precios

La fuente `priceBooks` envía datos al [extremo de libros de precios](https://developer.adobe.com/commerce/services/reference/rest/#tag/Price-Books){target="_blank"}.

A diferencia de otras fuentes de conector, la fuente `priceBooks` no la recopila un indizador [!DNL SaaS Data Export] en [!DNL Adobe Commerce]. El conector genera esta fuente a partir del sitio web y la configuración del grupo de clientes en el Administrador.

Se crea un **libro de precios base** por sitio web, más un **libro de precios secundario** por par de grupo de sitio web-cliente.

**Fórmula de id. de libro de precios:**

- **Base** (precios normales): `priceBookId = websiteCode`
- **Secundario** (grupo de clientes o catálogo compartido): `priceBookId = websiteCode::sha1(customerGroupId)` donde `sha1(customerGroupId)` es el resumen hexadecimal SHA-1 del identificador entero del grupo de clientes

La fuente de precios utiliza la misma fórmula al resolver a qué libro de precios pertenece una entrada de precio. Para saber cómo resuelven las tiendas el(la) `priceBookId` de una sesión de cliente, consulte [Integración de tiendas sin encabezado](../headless-storefront.md#graphql-commerceoptimizer-query).

| Campo generado | Campo de API [!DNL Commerce Optimizer] | Notas |
| ---------------- | -------------- | ------- |
| `websiteCode`, `customerGroupId` | `priceBookId` | |
| Nombre del sitio web | `name` | Precio base libro: nombre del sitio web. Secundario: `"Group Name (Website Name)"` |
| `websiteCode` | `parentId` | Presente solo en libros de precios para niños; señala al libro de precios base |
| Moneda base del sitio web | `currency` | Presente solo en libros de precio base; heredado por los niños |

## Precios

La fuente `prices` envía datos al extremo [Prices](https://developer.adobe.com/commerce/services/reference/rest/#tag/Prices){target="_blank"}.

| [!DNL Adobe Commerce] campo | Campo de API [!DNL Commerce Optimizer] | Notas |
| --------------- | -------------- | ------------------------------------------------------------------------------- |
| `sku` | `sku` | |
| `websiteCode`, `customerGroupId` | `priceBookId` | |
| `regular` | `regular` | |
| `discounts[]` | `discounts[]` | ejemplo de descuentos: precio especial, precio de regla de catálogo, precio de catálogo compartido |
| `tierPrices[]` | `tierPrices[]` | |

## Categorías

La fuente `categories` envía datos al extremo [Categories](https://developer.adobe.com/commerce/services/reference/rest/#tag/Categories){target="_blank"}.

Los elementos con un `urlPath` vacío (categorías raíz lógicas) se omiten y nunca se envían.

| [!DNL Adobe Commerce] campo | Campo de API [!DNL Commerce Optimizer] | Notas |
| --------------- | -------------- | ------- |
| `storeViewCode` | `source/locale` | |
| `name` | `name` | |
| `urlPath` | `slug` | |
| `description` | `description` | |
| `metaTitle` | `metaTags/title` | |
| `metaDescription` | `metaTags/description` | |
| `metaKeywords` | `metaTags/keywords` | Cadena delimitada por una nueva línea dividida en matriz |
| `image` | `images[].url` | Matriz de un solo elemento; `roles: ["BASE"]` |
| `isActive` + `includeInMenu` | `families` | `["top_menu"]` cuando ambos `true`, `[]` en caso contrario |

>[!MORELIKETHIS]
>
> - [Ingesta de datos de productos y precios con la API de ingesta de datos](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/){target="_blank"}: conozca el modelo de datos de catálogo para metadatos, productos, categorías, libros de precios y precios
> - [Referencia de API de REST de ingesta de datos de catálogo](https://developer.adobe.com/commerce/services/reference/rest/){target="_blank"}: revise los esquemas de solicitud y respuesta para cada extremo de fuente
> - [Cómo funciona [!DNL Commerce Optimizer Connector] con [!DNL Adobe Commerce]](../overview.md#how-the-connector-works-with-adobe-commerce): descubre cómo las vistas de tiendas, los sitios web y los grupos de clientes se asignan a los orígenes de catálogo y a los libros de precios
> - [Libros de precios en [!DNL Commerce Optimizer]](/help/optimizer/setup/pricebooks.md): administre los libros de precios creados por la exportación del conector
> - [Integración de tienda sin encabezado](../headless-storefront.md#graphql-commerceoptimizer-query) — Resolver `priceBookId` para sesiones de clientes
