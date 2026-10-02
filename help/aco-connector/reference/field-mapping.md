---
title: Asignación de campos para fuentes de [!DNL Adobe Commerce Optimizer Connector]
description: Obtenga información acerca de la asignación de campos [!DNL Adobe Commerce Optimizer Connector] desde los datos del catálogo [!DNL Adobe Commerce] a los formatos de API de ingesta [!DNL Adobe Commerce Optimizer] para todas las fuentes.
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."
autotag-review: '2026-06-09T15:49:03.934Z'
TQID: 'https://experienceleague.adobe.com/SOWOnguudhqzX-r66nGUqc-WKet5qq6GRV11ADx0Me4'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
  - id: b23e006f-0a29-4f1d-8fd0-77aa56f3d12b
    internal-label: Data modeling
source-git-commit: 1e34df4f07f9043675104fce55c58e0617463b33
workflow-type: tm+mt
source-wordcount: '1023'
ht-degree: 2%
---

# Asignación de campos para fuentes de conector

Esta página documenta cómo [!DNL Adobe Commerce Optimizer Connector] transforma los campos del catálogo [!DNL Adobe Commerce] en el formato requerido por [!DNL Commerce Optimizer] [!DNL Catalog Data Ingestion API]. Consulte la [referencia de conector](connector-reference.md#supported-feeds) para ver la lista de fuentes admitidas y sus extremos de API.

## Productos

La fuente `products` envía datos al extremo [Products](https://developer.adobe.com/commerce/services/reference/rest/#tag/Products){target="_blank"}.

| [!DNL Adobe Commerce] campo | Campo de API [!DNL Commerce Optimizer] | Detalles de asignación |
| ----------------------------------------------- | -------------- | ------- |
| `sku` | `sku` | |
| `storeViewCode` | `source/locale` | |
| `name` | `name` | |
| `urlKey` | `slug` | |
| `productId` | `externalIds[0].id` | Establece `origin` en `"AdobeCommerce"` |
| `status` | `status` | Convierte el estado a mayúsculas. Utiliza `DISABLED` si falta el estado o si un producto configurable o agrupado no tiene valores de opción. |
| `description` | `description` | Utiliza una cadena vacía si falta la descripción. |
| `shortDescription` | `shortDescription` | Utiliza una cadena vacía si falta la descripción breve. |
| `visibility` | `visibleIn` | Divide el valor separado por comas y asigna `Catalog` a `CATALOG` y `Search` a `SEARCH`. Elimina otros valores. |
| `metaTitle` | `metaTags/title` | |
| `metaDescription` | `metaTags/description` | |
| `metaKeyword` | `metaTags/keywords` | Divide las palabras clave separadas por una nueva línea en una matriz y recorta el espacio en blanco. |
| `inStock`, `lowStock`, `weight`, `weightUnit` | `attributes[].code = "aco_ac_attributes"` | Agrega siempre una entrada `aco_ac_attributes` como primer atributo. Su valor JSON incluye `inStock` y `lowStock` como cadenas. Incluye `weight` y `weightType` cuando esos valores están disponibles. |
| `attributes[]` | `attributes[]` | Asigna cada entrada a su código de atributo, valores de cadena e ID de referencia de variante coincidente cuando está disponible. Omite `inStock`, `lowStock`, `categories`, `weight` y `weightType`. Los valores de inventario se incluyen en `aco_ac_attributes`. Las categorías se exportan como rutas. |
| `images[]` | `images[]` | Omite imágenes sin dirección URL.<br>Exporta `url`, `label` (vacío si falta) y `sortOrder` (entero, valor predeterminado `0`).<br>Ordena las imágenes por `sortOrder` en orden ascendente.<br>Asigna roles estándar: `image` a `BASE`, `small_image` a `SMALL`, `thumbnail` a `THUMBNAIL` y `swatch_image` a `SWATCH`. Exporta otros roles como `customRoles[]`. |
| `categoryData[].categoryPath` | `routes[].path` | Omite las entradas con una ruta de categoría vacía. |
| `categoryData[].productPosition` | `routes[].position` | Usa `0` si falta la posición del producto. |
| `links[].type` + `links[].sku` | `links[]` | `type` en mayúscula; se perdieron las entradas sin `sku` |
| `parents[].productType` + `parents[].sku` | `links[]` | Asigna a `configurable` a `VARIANT_OF`, y a `bundle` o `bundle_fixed` a `IN_BUNDLE`. Convierte otros tipos de productos a mayúsculas. Omite elementos principales sin SKU. |
| `configurable options` | `configurations[]` | Exporta opciones que tienen un ID y al menos un valor.<br>Asigna `id` a `attributeCode`. Establece `type` en `SWATCH` cuando `swatchType` está presente y en `CONFIGURABLE` en caso contrario.<br>Utiliza el identificador del valor predeterminado como `defaultVariantReferenceId`.<br>Asigna cada valor a `variantReferenceId`, `label`, `colorHex` y `imageUrl`. |
| `bundle options` | `bundles[]` | Exporta opciones que contienen al menos un elemento.<br>Utiliza la etiqueta de opción como `group` o `Bundle group` si la etiqueta está vacía. Copia `required` en el resultado.<br>Establece `multiSelect` en `true` para los tipos de procesamiento `checkbox` y `multi`.<br>Muestra los SKU predeterminados en `defaultItemSkus`. Cada elemento incluye `sku`, `qty` (el valor predeterminado es `0`) y `userDefinedQty` (de `qtyMutability`, el valor predeterminado es `false`). |

## Metadatos de atributos de producto

La fuente `productAttributes` envía datos a [extremo de metadatos](https://developer.adobe.com/commerce/services/reference/rest/#tag/Metadata){target="_blank"}.

| [!DNL Adobe Commerce] campo | Campo de API [!DNL Commerce Optimizer] | Detalles de asignación |
| --------------- | -------------- | ------- |
| `attributeCode` | `code` | |
| `storeViewCode` | `source/locale` | |
| `label` | `label` | |
| `dataType` + `frontendInput` | `dataType` | Consulte la tabla de conversión a continuación |
| `dataType` y `frontendInput` | `dataType` | Utiliza las reglas de conversión siguientes. |
| `visible`, `visibleInSearch`, `visibleInListing`, `visibleInCompareList` | `visibleIn[]` | Cuando un indicador es `true`, agrega su valor correspondiente:<br>`visible` → `PRODUCT_DETAIL`<br>`visibleInSearch` → `SEARCH_RESULTS`<br>`visibleInListing` → `PRODUCT_LISTING`<br>`visibleInCompareList` → `PRODUCT_COMPARE` |
| `filterable` | `filterable` | |
| `sortable` | `sortable` | |
| `searchable` | `searchable` | |
| `searchWeight` | `searchWeight` | |
| `searchTypes` | `searchTypes` | |

### Conversión de tipo de datos

Cuando `dataType` es `int`, el conector comprueba `frontendInput`. Para otros tipos de datos, `frontendInput` no afecta a la conversión.

| Entrada `dataType` | Entrada `frontendInput` | Salida `dataType` |
| ---------------- | --------------------- | ----------------- |
| `int` | `boolean` | `BOOLEAN` |
| `int` | `text` o `select` | `TEXT` |
| `int` | Cualquier otro valor, incluido un valor que falta | `INTEGER` |
| `decimal` | No se usa | `DECIMAL` |
| `text`, `varchar`, `static`, `datetime` | No se usa | `TEXT` |
| `OBJECT` | No se usa | `OBJECT` |
| Cualquier otro valor | No se usa | `TEXT` |

>[!NOTE]
>
>Cuando un atributo usa el tipo de datos `OBJECT`, la [API de productos](https://developer.adobe.com/commerce/services/reference/graphql/#products){target="_blank"} intenta analizar su valor almacenado como JSON. Si el análisis se realiza correctamente, la API devuelve el valor como un objeto anidado. Use `OBJECT` para datos de atributos estructurados que no se puedan representar como un valor único. Para obtener instrucciones, consulte [Agregar atributos de producto dinámicamente](../../data-export/add-attribute-dynamically.md).

## Libros de precios

La fuente `priceBooks` envía datos al [extremo de libros de precios](https://developer.adobe.com/commerce/services/reference/rest/#tag/Price-Books){target="_blank"}.

A diferencia de otras fuentes de conector, la fuente `priceBooks` no la recopila un indizador [!DNL SaaS Data Export] en [!DNL Adobe Commerce]. El conector genera esta fuente a partir del sitio web y la configuración del grupo de clientes en el Administrador.

Para cada sitio web, el conector crea un libro de precios base y un libro de precios secundario para cada grupo de clientes.

Usar estas fórmulas para `priceBookId`:

- Libros de precios base para precios regulares: `priceBookId = websiteCode`.
- Libros de precios secundarios para grupos de clientes: `priceBookId = websiteCode::sha1(customerGroupId)`, donde `sha1(customerGroupId)` es el resumen hexadecimal SHA-1 del identificador entero del grupo de clientes.

La fuente de precios utiliza la misma fórmula para asignar cada entrada de precio a un libro de precios. Para obtener información sobre cómo resuelve una tienda `priceBookId` para una sesión de cliente, consulte [Integración de tienda sin encabezado](../headless-storefront.md#graphql-commerceoptimizer-query).


| Campo o valor de Source | Campo de API [!DNL Commerce Optimizer] | Detalles de asignación |
| ---------------- | -------------- | ------- |
| `websiteCode` | `parentId` | Añade este campo a los libros de precios secundarios. Su valor identifica el libro de precios base. |
| Nombre del sitio web | `name` | Utiliza el nombre del sitio web para los libros de precios base. Utiliza `Customer group name (Website name)` para los libros de precios secundarios. |
| `websiteCode` | `parentId` | Presente solo en libros de precios para niños; señala al libro de precios base |
| Moneda base del sitio web | `currency` | Incluye este campo sólo en los libros de precio base. Los libros de precios para niños lo omiten. |

## Precios

La fuente `prices` envía datos de [!DNL Adobe Commerce] al extremo [Prices](https://developer.adobe.com/commerce/services/reference/rest/#tag/Prices){target="_blank"}.

| Campo de entrada de fuente | Campo de API [!DNL Commerce Optimizer] | Detalles de asignación |
| --------------- | -------------- | ------------------------------------------------------------------------------- |
| `sku` | `sku` | Pasa el SKU sin cambiar. |
| `websiteCode`, `customerGroupCode` | `priceBookId` | Combina `websiteCode` con el hash SHA-1 del identificador del grupo de clientes en `customerGroupCode`. Si `customerGroupCode` es `0`, solo usa `websiteCode`. |
| `regular` | `regular` | Pasa el precio normal sin cambiar. |
| `discounts[]` | `discounts[]` | Si el valor de origen es `null`, exporta una matriz vacía.<br>Para las entradas con `code` establecido en `special_price` y un `percentage`, establece `percentage` en `100 - percentage` cuando el valor está entre `0` y `100`. Lo establece en `0` dentro o fuera de ese intervalo.<br>Pasa sin cambios otras entradas, incluidos los precios especiales basados en precios. |
| `tierPrices[]` | `tierPrices[]` | Usa una matriz vacía si falta el valor de origen o `null`. |

## Categorías

La fuente `categories` envía datos de [!DNL Adobe Commerce] al extremo [Categories](https://developer.adobe.com/commerce/services/reference/rest/#tag/Categories){target="_blank"}.

Los elementos con un `urlPath` vacío (categorías raíz lógicas) se omiten y nunca se envían.

| [!DNL Adobe Commerce] campo | Campo de API [!DNL Commerce Optimizer] | Detalles de asignación |
| --------------- | -------------- | ------- |
| `storeViewCode` | `source/locale` | |
| `name` | `name` | |
| `urlPath` | `slug` | |
| `description` | `description` | |
| `position` | `position` | Exporta la posición de la categoría cuando está presente. Omite el campo cuando falta. |
| `metaTitle` | `metaTags/title` | |
| `metaDescription` | `metaTags/description` | |
| `metaKeywords` | `metaTags/keywords` | Cadena delimitada por una nueva línea dividida en matriz |
| `image` | `images[].url` | Matriz de un solo elemento; `roles: ["BASE"]` |
| `isActive` + `includeInMenu` | `families` | `["top_menu"]` cuando ambos `true`, `[]` en caso contrario |

| `metaKeywords` | `metaTags/keywords` | Divide las palabras clave delimitadas por una nueva línea en una matriz y recorta el espacio en blanco. |
| `image` | `images[].url` | Cuando `image` está presente, exporta una imagen con el rol `BASE`. Exporta una matriz vacía cuando la imagen está vacía o falta. |
| `isActive` + `includeInMenu` | `families` | Agrega `top_menu` solo cuando ambos valores son `true`. De lo contrario, exporta una matriz vacía. |
| `attributes[]` | `attributes[]` | Exporta entradas con un `attributeCode` no vacío como `{code, values[]}`. Convierte los valores en cadenas. Omite `attributes` cuando no existen entradas aptas. |

>[!MORELIKETHIS]
>
> - [Ingesta de datos de productos y precios con la API de ingesta de datos](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/){target="_blank"}: conozca el modelo de datos de catálogo para metadatos, productos, categorías, libros de precios y precios
> - [Referencia de API de REST de ingesta de datos de catálogo](https://developer.adobe.com/commerce/services/reference/rest/){target="_blank"}: revise los esquemas de solicitud y respuesta para cada extremo de fuente
> - [Cómo funciona [!DNL Commerce Optimizer Connector] con [!DNL Adobe Commerce]](../overview.md#how-the-connector-works-with-adobe-commerce): descubre cómo las vistas de tiendas, los sitios web y los grupos de clientes se asignan a los orígenes de catálogo y a los libros de precios
> - [Libros de precios en [!DNL Commerce Optimizer]](/help/optimizer/setup/pricebooks.md): administre los libros de precios creados por la exportación del conector
> - [Integración de tienda sin encabezado](../headless-storefront.md#graphql-commerceoptimizer-query) — Resolver `priceBookId` para sesiones de clientes
