---
title: '[!DNL Commerce Storefront Catalog Service Release Notes]'
description: La información de la versión más reciente de  [!DNL Catalog Service]  para Adobe Commerce.
feature: Services, Catalog Service, Release Notes
exl-id: 74f2e46a-5592-4857-a6d7-b95b85d8b4cc
TQID: https://experienceleague.adobe.com/-yxW4sTuk7LPjGy5YsQ65phtkBLiByg8SmBaQPHMevM
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: e1e0219c-f879-479f-8427-888ed2a6e9c2id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: acc520f67bdd1bdafd34b356b59bb32145192497
workflow-type: tm+mt
source-wordcount: 2682
ht-degree: 0%

---

# Notas de la versión [!DNL Commerce Storefront Catalog Service]

Estas notas de la versión cubren las últimas actualizaciones del servicio de catálogo de Commerce, que incluyen:

- **[Versiones del servicio de catálogo de tiendas](#storefront-catalog-service)**

   - Mejoras en el esquema de la API del servicio de catálogo para una recuperación de datos mejorada
   - Mejoras de seguridad, rendimiento y fiabilidad para la API del servicio de catálogo y la infraestructura subyacente.

  Consulte [Esquema de servicios de tienda](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/) en la documentación para desarrolladores de Commerce para obtener más información sobre estas API.

- **[Versiones de metapaquetes del servicio de catálogo](#catalog-service-metapackage)**

   - Dependencias actualizadas para mejorar el rendimiento, la estabilidad y la compatibilidad con otros componentes de Adobe Commerce.

- **[Versiones del instalador del servicio de catálogo](#catalog-service-installer)**

   - Se han actualizado las dependencias para mantener la compatibilidad entre el servicio de catálogo y la pila de Commerce.

>[!NOTE]
>
>Si su proyecto de Commerce usa Adobe Commerce Optimizer para entregar datos de catálogo al servicio de Commerce Edge Delivery o a tiendas sin encabezado, consulte las [notas de la versión de Adobe Commerce Optimizer](../optimizer/release-notes.md) para obtener las últimas actualizaciones de la API.

Las actualizaciones se clasifican por tipo:

![Nuevas](../assets/new.svg) nuevas características
![Corrección](../assets/fix.svg) Correcciones y mejoras
![Error](../assets/bug.svg) Problemas conocidos

Se proporciona soporte para la versión más reciente. Las notas de la versión de las versiones anteriores se incluyen como referencia.

## Servicio de catálogo de tienda

### Mayo de 2026

**Fecha de la versión**: 20 de mayo de 2026
<!-- v1.55 -->

![Nuevo](../assets/new.svg) límite obligatorio máximo de 100 SKU por solicitud para clientes de Adobe Commerce y Adobe Commerce as a Cloud Service según [límites y límites documentados](https://experienceleague.adobe.com/en/docs/commerce/optimizer/boundaries-limits).
<!--DATA-7163-->

**Fecha de la versión**: 13 de mayo de 2026
<!--v1.54-->

![Nuevo](../assets/new.svg) **criterio de ordenación de categorías en GraphQL**: el tipo de GraphQL `CategoryView` ahora incluye un campo de posición, de modo que los escaparates pueden mostrar las categorías en el orden en que los comerciantes las configuran en la jerarquía del catálogo.
<!--DATA-7166-->

**Fecha de la versión**: 4 de mayo de 2026
<!-- v1.53 -->

![Corregir](../assets/fix.svg) Los precios de los productos de tienda ahora muestran el código de moneda correcto (por ejemplo, USD) para todos los tipos de productos. Anteriormente, algunos productos mostraban `NONE` en lugar de la moneda esperada, lo que resultaba en la falta de precios. Esta actualización garantiza un procesamiento de precios coherente y preciso en toda la tienda.<!--DATA-7115-->

### Abril de 2026

**Fecha de publicación**: 29 de abril de 2026
<!--v1.52-->

![Nuevo](../assets/new.svg) límite obligatorio máximo de 100 SKU por solicitud para Adobe Commerce Optimizer y Adobe Commerce as a Cloud Service
clientes según [límites y límites documentados](https://experienceleague.adobe.com/en/docs/commerce/optimizer/boundaries-limits). <!--DATA-7156-->

**Fecha de publicación**: 17 de abril de 2026
<!--v1.51-->

![Nuevo](../assets/new.svg) agregó una nueva consulta de GraphQL `searchCategory` que permite a los clientes buscar categorías por nombre con resultados paginados. La consulta acepta los parámetros `searchTerm` (mínimo 3 caracteres) y `family`, `pageSize` y `currentPage` opcionales. Los resultados incluyen `CategoryTreeView` objetos coincidentes con metadatos de categoría completa, un `totalCount` y `pageInfo` para la paginación. <!--COMOPT-1819-->

Esta consulta solo está disponible para clientes que utilizan Adobe Commerce Optimizer Merchandising Services. Consulte [searchCategory](https://developer.adobe.com/commerce/services/reference/graphql/).

### Marzo de 2026

**Fecha de la versión**: 24 de marzo de 2026
<!--v1.49-->

![Nuevo](../assets/new.svg) Se agregó compatibilidad para calcular y devolver el rango de precios de los paquetes dinámicos.
<!--DATA-7115-->

### Diciembre de 2025

**Fecha de la versión**: 11 de diciembre de 2025
<!-- v1.46 -->

![Corrección](../assets/fix.svg): mejoras de infraestructura y nivel de sistema para mejorar el rendimiento y la estabilidad.
<!--DATA-6852, DATA-6864-->

### Noviembre de 2025

**Fecha de la versión**: 17 de noviembre de 2025
<!-- v1.45 -->

![Nuevo](../assets/new.svg) **Filtrado de atributos por nombre**- La consulta de GraphQL `productSearch` ahora admite el filtrado de atributos de productos con el campo `names`. <!--DATA-6831--> Con este filtro, puede:

- Reduzca el tamaño de la carga útil de respuesta solicitando solo atributos específicos
- Combinar con el filtro `roles` existente para reducir según el rol de visibilidad y el nombre de atributo
- Ejemplos:

  **Solo filtrar por nombres de atributo**

  ```graphql
  query {
    products(skus: ["SKU-001"]) {
      attributes(names: ["color", "size", "material"]) {
        name
        label
        value
      }
    }
  }
  ```

  **Filtrar por roles y nombres:**

  ```graphql
  query {
    products(skus: ["SKU-001"]) {
      attributes(roles: ["visible in PDP"], names: ["eco_collection", "new"]) {
        name
        label
        value
        roles
      }
    }
  }
  ```

>[!NOTE]
>
>Para recuperar todos los atributos sin filtrar, omita el argumento `names` o proporcione una matriz vacía.

**Fecha de la versión**: 6 de noviembre de 2025
<!-- v1.44 -->

![Corrección](../assets/fix.svg): mejoras de infraestructura y nivel de sistema para mejorar el rendimiento y la estabilidad. <!--DATA-6852, DATA-6864-->

![Corregir](../assets/fix.svg) Los productos agrupados ahora se pueden consultar cuando el producto principal no tiene precios; los productos secundarios devuelven sus propias funciones de visibilidad.<!--DATA-6779-->

![Corrección](../assets/fix.svg): mejoras de infraestructura y nivel de sistema para mejorar el rendimiento y la estabilidad. <!--DATA-6721, DATA-6864-->

### Septiembre de 2025

**Fecha de la versión**: 8 de septiembre de 2025
<!-- v1.42 -->

![Nuevo](../assets/new.svg) **Se ha agregado compatibilidad con precios de nivel** para consultar los precios de volumen:<!--DATA-6643-->

Para recuperar los precios de nivel:

1. Utilice la consulta `products` con los SKU que desee
2. Para **SimpleProductView**, obtener acceso a `price.tiers`
3. Para **ComplexProductView**, obtenga acceso a `priceRange.minimum.tiers` y a `priceRange.maximum.tiers`
4. Cada nivel contiene el precio de `tier` con descuento y `quantity` condiciones
5. Definir umbrales de cantidad con `gte` (mayor o igual que) y `lt` (menor que)

**Ejemplo:**

```graphql
query {
  products(skus: ["SKU-001"]) {
    ... on SimpleProductView {
      price {
        regular { amount { value currency } }
        tiers {
          tier { amount { value currency } }
          quantity {
            ... on ProductViewTierRangeCondition { gte lt }
          }
        }
      }
    }
  }
}
```

![Corregir](../assets/fix.svg) **Precios de nivel filtrados por precio mínimo final** <!--DATA-6643-->

La API ahora devuelve solo niveles cuyo precio con descuento sea **menor que** el precio final mínimo del producto. Se omiten los niveles más altos porque el precio final mínimo se aplicaría en la tienda.

Se aplica a:

- **Productos simples**: `price.tiers` solo incluye niveles con `tier.amount.value` &lt; `price.final.amount.value` (mínimo final).
- **Productos complejos**: `priceRange.minimum.tiers` y `priceRange.maximum.tiers` usan la misma regla al generar el rango de precios.

**Fecha de lanzamiento**: 2 de septiembre de 2025
<!-- v1.41 -->

![Corrección](../assets/fix.svg) **Se ha mejorado la administración de errores para la información de precios que falta**: cuando los datos de precios aún no se han recibido, la API devuelve `null` para el campo de precios en lugar de generar un error, lo que permite a los clientes gestionar correctamente los datos que faltan.<!--DATA-6612-->

![Corrección](../assets/fix.svg): mejoras de infraestructura y nivel de sistema para mejorar el rendimiento y la estabilidad.<!--DATA-6671-->

### Julio de 2025

**Fecha de la versión**: 30 de julio de 2025
<!-- v1.40 -->

![Solucionar](../assets/fix.svg) mejoras de infraestructura y nivel de sistema para mejorar la seguridad, el rendimiento y la estabilidad.<!--DATA-6619-->

**Fecha de la versión**: 24 de julio de 2025
<!-- v1.39 -->

![Nuevo](../assets/new.svg) **Recuperar unidades de recomendación por id. de unidad**-El nuevo extremo de GraphQL `recommendationsByUnitIds` recupera unidades de recomendación por su id. único para un acceso más flexible y con objetivo.

- Se requiere `unitIds` (lista de recIds que recuperar).
- Los parámetros de contexto (`currentSku`, `cartSkus`, `userViewHistory`, `userPurchaseHistory`, `category`) se comportan igual que en la consulta de recomendaciones existente.

- **Ejemplo**

  ```graphql
  query {
    recommendationsByUnitIds(
      unitIds: ["11ee89d1-bfae-4582-a921-2ced44ff6bf7"]
      currentSku: "24-MB01"
      cartSkus: ["24-MB01"]
    ) {
      totalResults
      results {
        unitId
        unitName
        totalProducts
        productsView {
          sku
        }
        pageType
        typeId
        storefrontLabel
        displayOrder
      }
    }
  }
  ```

![Solucionar](../assets/fix.svg) mejoras de infraestructura y nivel de sistema para mejorar la seguridad, el rendimiento y la estabilidad.<!--DATA-6316-->

**Fecha de la versión**: 15 de julio de 2025
<!-- v1.38 -->

![Nuevo](../assets/new.svg) **Tipos de productos de tarjetas de regalo**: el servicio de tienda de catálogos ahora admite atributos de productos como objetos o matrices JSON, lo que permite una administración flexible de tipos complejos como tarjetas de regalo.<!--DATA-6573-->

+++Versiones anteriores

### Junio de 2025

**Fecha de la versión**: 20 de junio de 2025
<!-- v1.37 -->

![Nuevo](../assets/new.svg) **Configuración jerárquica del libro de precios**: intervalos de precios precisos para libros de precios principal-secundario. Los cálculos respetan la jerarquía y las reglas heredadas; reduce los errores de asignación de precios cuando se vinculan varios libros de precios. Solo Adobe Commerce Optimizer. Ver [Libros de precios](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/pricebooks).

![Nuevas](../assets/new.svg) **claves que no distinguen entre mayúsculas y minúsculas**: las búsquedas de claves en las consultas ahora no distinguen entre mayúsculas y minúsculas, lo que reduce los errores de mayúsculas y minúsculas. <!--DATA-6494, DCAT-2495-->

**Fecha de la versión**: 20 de junio de 2025
<!-- v1.36 -->

![Nuevos](../assets/new.svg) **eventos de E/S públicos para la tienda de catálogos**: se agregaron eventos de E/S públicos para la integración y la observabilidad en tiempo real (CSS y EDS).<!--DATA-6329-->

![Nuevo](../assets/new.svg) **Procesamiento del lado del servidor (SSR)**: mejoras arquitectónicas para admitir SSR y mejorar el rendimiento, SEO y UX en catálogos grandes.<!--DATA-6278, DATA-6280-->

![Nueva](../assets/new.svg) **infraestructura y seguridad**—Nuevas funciones de AWS, integración de ServiceNow y canalizaciones de CI/CD para el servicio de eventos.

![Nuevos](../assets/new.svg) **formatos y observabilidad de eventos**: cargas útiles optimizadas, supervisión mejorada y datos de eventos de variante mejorados.<!--DATA-6332, DATA-6402, -->

![Solucionar](../assets/fix.svg) mejoras de infraestructura y nivel de sistema para mejorar la seguridad, el rendimiento y la estabilidad.<!--DATA-6404, DATA-6410, -->

**Fecha de la versión**: 13 de junio de 2025
<!-- v1.35 -->

![Nuevo](../assets/new.svg) **Recuperar datos sin caché**-Habilite el encabezado `Magento-Is-Preview` para pasar datos sin caché del extremo del catálogo al servicio de búsqueda.<!--DATA-6345-->

![Nuevo](../assets/new.svg) **Opciones de productos de selección múltiple**: la API de GraphQL ahora indica si las opciones de productos permiten selecciones múltiples (por ejemplo, el paquete &quot;elegir varios elementos&quot;).<!--DATA-6487-->

![Nuevo](../assets/new.svg) Se actualizó la validación de precios en la ingesta de datos para admitir productos sin precios.<!--DATA-6098-->

![Corrección](../assets/fix.svg) Se mejoró la administración de errores para los precios de paquetes simples en Adobe Commerce Optimizer.<!--DATA-6541-->

![Solucionar](../assets/fix.svg) mejoras de infraestructura y nivel de sistema para mejorar la seguridad, el rendimiento y la estabilidad.<!--DATA-6273, DATA-6485, -->

### Abril de 2025

**Fecha de publicación**: 8 de abril de 2025
<!-- v1.34 -->

![Solucionar](../assets/fix.svg) mejoras de infraestructura y nivel de sistema para mejorar la seguridad, el rendimiento y la estabilidad.<!--DATA-5732-->

<!-- v1.33 -->
![Corrección](../assets/fix.svg) La infraestructura ahora admite catálogos extremadamente grandes (hasta ~440 millones de SKU) sin afectar las cargas de trabajo existentes.

### Marzo de 2025

**Fecha de la versión**: 28 de marzo de 2025
<!-- v1.32 -->

![Corregir](../assets/fix.svg) Los atributos sin funciones ya no se indizan de forma predeterminada para el catálogo maquetable, lo que mejora el tiempo de indización y reduce el almacenamiento. El comportamiento heredado se puede volver a habilitar mediante un indicador de funcionalidad.

![Solucionar](../assets/fix.svg) mejoras en la infraestructura y el nivel de sistema para mejorar la seguridad, el rendimiento y la estabilidad.
<!--DATA-6348, DATA-6440, DATA-6446, DATA-6641-->

### Febrero de 2025

**Fecha de publicación**: 18 de febrero de 2025
<!-- v1.31 -->

![Solucionar](../assets/fix.svg) mejoras de infraestructura y nivel de sistema para mejorar la seguridad, el rendimiento y la estabilidad.<!--DATA-6389, DATA-6367, DATA-6373-->

### Diciembre de 2024

**Fecha de la versión**: 9 de diciembre de 2024
<!-- v1.30 -->

Versión principal: [modelo de datos de catálogo maquetable](https://developer.adobe.com/commerce/services/optimizer/) para tiendas sin encabezado, administración de encabezados y administración de datos de productos.

![Nuevo](../assets/new.svg) **Modelo de datos de catálogo maquetable (CCDM)**: admite clientes que usen el catálogo maquetable para tiendas sin encabezado. Los nuevos extremos aceptan la vista de catálogo y los ID de directiva (compatible con versiones anteriores). Detalles y precios configurables del producto con paginación integrada.<!--DATA-6018, DATA-6288-->

![Nuevo](../assets/new.svg) **Administración de encabezado**-`AC-Locale` cambió el nombre a `AC-Scope-Locale` para operaciones de API de catálogo maquetable; se especificaron la asignación de encabezado y los valores predeterminados.<!--DATA-6303, DATA-6078-->

![Nuevo](../assets/new.svg) **Datos y precios del producto**: compatibilidad con el modelo de datos del catálogo maquetable y con la gestión de precios mejorada para los productos configurables.<!--DATA-6279-->

`CurrencyEnum` se actualizó para admitir `NONE` para las consultas de búsqueda de productos, alineándose con la lógica de federación.<!--DATA-6285-->

![Corregir](../assets/fix.svg) **Infraestructura y actualizaciones**: mejoras de nivel de sistema para la seguridad, el rendimiento y la estabilidad.

![Corregir](../assets/fix.svg) Las opciones del paquete de productos ahora solo muestran los productos habilitados.<!--DATA-6347-->

**Fecha de la versión**: 9 de diciembre de 2024
<!-- v1.29 -->

![Nuevo](../assets/new.svg) **orden de imágenes en consultas de productos**: las imágenes de productos en el campo de GraphQL `images` ahora siguen la exportación de catálogos `sortOrder` para un comportamiento coherente de tienda y API.<!--DATA-6258-->

![Solucionar](../assets/fix.svg) mejoras de infraestructura y nivel de sistema para mejorar la seguridad, el rendimiento y la estabilidad.<!--DATA-6619-->

**Fecha de la versión**: diciembre de 2024
<!-- v1.28 -->

![Solucionar](../assets/fix.svg) mejoras en la infraestructura y el nivel de sistema para mejorar la seguridad, el rendimiento y la estabilidad.
<!--DATA-6180, DATA-6230, DATA-6254, DATA-6257-->

### Octubre de 2024

**Fecha de la versión**: 22 de octubre de 2024
<!-- v1.26 -->

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

El esquema ![Nuevo](../assets/new.svg) de GraphQL ahora incluye `lastModifiedAt` en la información del producto para obtener mapas del sitio y reindexación de motores de búsqueda precisos (por ejemplo, Google).
<!--DATA-6209-->

### Septiembre de 2024

**Fecha de la versión**: 26 de septiembre de 2024
<!-- v1.27 -->

![Solucionar](../assets/fix.svg) mejoras en la infraestructura y el nivel de sistema para mejorar la seguridad, el rendimiento y la estabilidad.
<!--DATA-6243-->

### Agosto de 2024

**Fecha de lanzamiento**: 22 de agosto de 2024
<!-- v1.23 -->

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Corrección](../assets/fix.svg): ahora se puede recuperar la información del producto sin los datos de invalidación (precios) del producto. Anteriormente, estas consultas arrojaban: `The following sku does not have product override data in the DB: <SKU value>. Make sure data is synced.`
<!--DATA-6121-->

**Fecha de lanzamiento**: 13 de agosto de 2024
<!-- v1.22 -->

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg) se agregó soporte para recuperar todas las variantes por SKU del producto. Consulte la [Referencia de API del servicio de catálogo](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/).
<!--DATA-6067-->

### Mayo de 2024

**Fecha de la versión**: 23 de mayo de 2024
<!-- v1.19 -->

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores


![Corrección](../assets/fix.svg) El indicador `InStock` para los valores de opción ahora respeta el estado `enabled` de ámbito de la variante del producto.

<!--DATA-5033-->

![Corrección](../assets/fix.svg) Se agregó compatibilidad con precios de productos con hasta 16 dígitos y 4 decimales. Resincronice desde el [panel de administración de datos](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard) o [CLI](../data-export/data-export-cli-commands.md) para aplicar las actualizaciones.
<!--DATA-5033-->

#### Limitaciones conocidas

Las siguientes funciones aún no son compatibles:

- El tamaño máximo de la carga útil de atributos dinámicos es 9 MB.
- El precio del producto del grupo se puede calcular con precios de productos simples.
- En una matriz de imágenes, solo la primera imagen contiene funciones.

Utilice API Mesh y la API principal de GraphQL para lo siguiente:

- Precio Mínimo Anunciado
- Precios de nivel
- Paquete de productos con precios fijos

Para obtener detalles y ejemplos, consulte [Servicio de catálogo y malla de API](mesh.md).

### Abril de 2024

**Fecha de publicación**: 11 de abril de 2024
<!-- v1.18 -->

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg) agregó compatibilidad con PHP 8.3.

![Nuevas](../assets/new.svg) Las consultas [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/) y [`refineProduct`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/) ahora devuelven datos de opciones personalizables para productos simples y complejos.<!--DATA-5538-->

### Febrero de 2024

**Fecha de publicación**: 22 de febrero de 2024
<!-- v1.17 -->

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg) [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html) ya está disponible para las secuencias de datos (Recomendaciones de productos, Live Search, Servicio de catálogo). Requiere `catalog-service` metapackage v3.1.0+.

**Fecha de publicación**: 13 de febrero de 2024
<!-- v1.16 -->

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

La API del servicio de catálogo admite ahora ![nuevos](../assets/new.svg) vídeos de producto.
![Corrección](../assets/fix.svg) Las opciones sin existencias ahora se muestran en el widget PDP.

#### Limitaciones conocidas

Estas funciones aún no son compatibles:

- El tamaño máximo de la carga útil de atributos dinámicos es 9 MB.
- Precio del producto del grupo. Este valor se puede calcular con precios de productos simples.
- En una matriz de imágenes, solo la primera imagen contiene funciones.

Utilice API Mesh y la API principal de GraphQL para lo siguiente:

- Precio Mínimo Anunciado
- [Precios de nivel](mesh.md)

### Octubre de 2023

**Fecha de la versión**: 12 de octubre de 2023
<!-- v1.13 -->

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

El servicio de catálogo ![New](../assets/new.svg) admite el indicador `inStock` para las variantes de producto.
![Nuevo](../assets/new.svg): los campos `urlKey` y `externalId` se han agregado al esquema de GraphQL.
Ahora se admiten ![nuevos](../assets/new.svg) productos descargables y tarjetas regalo.

### Septiembre de 2023

**Fecha de la versión**: 19 de septiembre de 2023
<!-- v1.12 -->

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

El servicio de catálogo ![New](../assets/new.svg) ahora usa [indización de precios SaaS](../price-index/price-indexing.md).
![Corrección](../assets/fix.svg) Esta versión contiene correcciones de errores y mejoras en el servicio.

### Julio de 2023

**Fecha de la versión**: 18 de julio de 2023
<!-- v1.11 -->

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

El servicio de catálogo ![New](../assets/new.svg) admite ahora la consulta de GraphQL [`recommendations`](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/) para Product Recommendations.

### Junio de 2023

**Fecha de la versión**: 27 de junio de 2023
<!-- v1.10 -->

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg): la API del servicio de catálogo ahora admite `related products`.

### Abril de 2023

**Fecha de publicación**: 12 de abril de 2023
<!-- v1.7 -->

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

El servicio de catálogo ![New](../assets/new.svg) ahora limpia las variantes de producto eliminadas.
![Corrección](../assets/fix.svg): mejoras de rendimiento y escalabilidad de la infraestructura.

### Marzo de 2023

**Fecha de la versión**: 28 de marzo de 2023
<!-- v1.6 -->

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg) agregó muestras a la consulta [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/).
![Nuevo](../assets/new.svg) agregó la capacidad para obtener `entityId` usando [API Mesh](mesh.md).

**Fecha de la versión**: 6 de marzo de 2023
<!-- v1.5 -->

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg) agregó la funcionalidad de GraphQL [`categories`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/).
![Corrección](../assets/fix.svg): rendimiento y escalabilidad de API mejorados.

### Febrero de 2023

**Fecha de lanzamiento**: 7 de febrero de 2023
<!-- v1.4 -->

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.x y posteriores

![Nuevo](../assets/new.svg) paquete de servicio de catálogo publicado para simplificar los pasos de instalación.
![Corrección](../assets/fix.svg) de escalabilidad y mejoras de rendimiento de API.

### Enero de 2023

**Fecha de la versión**: 17 de enero de 2023
<!-- v1.3 -->

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.x y posteriores

![Nuevo](../assets/new.svg) ha simplificado y mejorado la experiencia de incorporación.
![Nuevos](../assets/new.svg) nuevos extremos de zona protegida del cliente disponibles para pruebas previas a la producción.
![Se ha agregado soporte](../assets/new.svg) para productos virtuales.
![Corrección](../assets/fix.svg) de escalabilidad de API y mejoras de rendimiento.

### Noviembre de 2022

**Fecha de la versión**: 18 de noviembre de 2022
<!-- v1.1 -->

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.x y posteriores

El servicio de catálogo ![New](../assets/new.svg) ahora es compatible con la [malla de API](https://developer.adobe.com/graphql-mesh-gateway/) de Adobe.
![Corrección](../assets/fix.svg): se mejoró la escalabilidad de la API y el rendimiento general.

### Octubre de 2022

**Fecha de la versión**: 4 de octubre de 2022
<!-- v1.0 -->

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.x y posteriores

![Nuevo](../assets/new.svg) soporte para productos agrupados y agrupados.
![Nuevo](../assets/new.svg) agregó invalidaciones de visibilidad B2B. Ahora se pueden buscar productos y se pueden agregar al carro de compras para grupos de clientes específicos.
El servicio ![Fix](../assets/fix.svg) es ahora más estable y ha mejorado el rendimiento.

### Septiembre de 2022

**Fecha de la versión**: 12 de septiembre de 2022
<!-- v0.3 -->

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.x y posteriores

![Nuevas](../assets/new.svg) imágenes de variante: las imágenes de producto devueltas se basan en las opciones seleccionadas.
![Nuevos](../assets/new.svg) roles de precio: solo los miembros de grupos de clientes específicos pueden ver los precios de los productos.
![Corrección](../assets/fix.svg): se ha mejorado la estabilidad y el rendimiento del servicio.
![Se reciben nuevas](../assets/new.svg) actualizaciones cuando los productos se eliminan del catálogo.

### Agosto de 2022

**Fecha de lanzamiento**: 9 de agosto de 2022
<!-- Beta -->

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.x y posteriores

![Nuevo](../assets/new.svg) Las consultas `products` y `refineProduct` devuelven los siguientes datos:

- Atributos de producto predefinidos (del sistema).
- Atributos de producto dinámicos y filtrarlos por función (página de visualización de producto/página de lista de productos).
- Opciones de producto.
- Imágenes de productos y filtrarlas por función (PDP/PLP).
- Un precio específico para productos simples y rangos de precios para productos configurables.
- Precios de grupo de clientes e intervalos de precios. Devuelven un precio predeterminado alternativo para los compradores sin grupo de clientes.
- Tipos de productos que utilizan precios específicos del cliente B2B.

+++

## Metapackage del servicio de catálogo

Actualizaciones al metapaquete PHP del servicio de catálogo (`magento/catalog-service`).

- Para los clientes de Adobe Commerce as a Cloud Service, la versión más reciente está instalada en su entorno.

- Para Adobe Commerce en la nube o de forma local, Adobe recomienda utilizar Composer para actualizar el metapaquete del servicio de catálogo en los entornos de nube en la última versión.

### Versión 3.4.0

**Fecha de la versión**: 8 de junio de 2026

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg) **Soporte para la supervisión del estado de sincronización de fuentes de datos**—Se han actualizado las dependencias del metapaquete del servicio de catálogo para incluir la extensión de estado del exportador de datos (`magento/module-data-exporter-status`). Esto habilita la [supervisión del estado de sincronización de fuentes de datos](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) desde el administrador de Commerce sin requerir ningún paso adicional de instalación o configuración

![Nuevo](../assets/new.svg) Se han actualizado las dependencias para mantener la compatibilidad entre el servicio de catálogo y la pila de Commerce.

### Versión 3.3.0

**Fecha de la versión**: 14 de octubre de 2025

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Nueva](../assets/new.svg) **actualización de servicios de datos**—`magento/data-services` dependencia actualizada a ^8.0.0. Compruebe el uso de la API de servicios de datos personalizados y del entorno para la compatibilidad con 8.x antes de actualizar.

![Nuevo](../assets/new.svg) Se actualizaron la versión y los metadatos de la versión 3.3.0.

### Versión 3.2.0

**Fecha de publicación**: 12 de abril de 2024

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Nueva](../assets/new.svg) versión y metadatos actualizados para 3.2.0. No hay otros cambios de dependencia.

### Versión 3.1.0

**Fecha de la versión**: 26 de enero de 2024

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg) agregó nuevas dependencias de paquete:

- **Exportador de datos de permisos de categoría** (`magento/module-category-permission-data-exporter`) para exportar datos de permisos de categoría usados por el servicio de catálogo.
- **Administrador de sincronización de catálogos** `magento/module-catalog-sync-admin` para la interfaz de usuario de administración y la configuración relacionada con la sincronización de catálogos.

![Nuevo](../assets/new.svg) Se actualizaron la versión y los metadatos de la versión 3.1.0.

## Instalador del servicio de catálogo

El instalador se entrega con la extensión del Servicio de catálogo y gestiona las comprobaciones de instalación y entorno para que el Servicio de catálogo coincida con la pila de Commerce.

- Para los clientes de **Adobe Commerce as a Cloud Service**, la versión más reciente del instalador está instalada en su entorno.

- Para **Adobe Commerce en la infraestructura en la nube** o **local**, mantenga el instalador alineado con el [metapaquete del servicio de catálogo](#catalog-service-metapackage).

Siempre que use Composer para actualizar `magento/catalog-service`, el paquete del instalador se actualizará automáticamente a la última versión. También puede usar Composer para actualizar `magento/catalog-service-installer` por separado cuando estas notas de la versión describan un cambio que necesite, por ejemplo, compatibilidad con una nueva versión de PHP. De este modo, las herramientas de instalación seguirán siendo compatibles con la versión del servicio de catálogo que ejecute.

### Versión v1.0.6

**Fecha de la versión**: 25 de marzo de 2026

![Nuevo](../assets/new.svg) **PHP 8.5**—Garantiza la compatibilidad cuando el Servicio de catálogo funcione en PHP 8.5.

## Documentación relacionada

- Para los proyectos implementados en **Adobe Commerce en la nube, local o Adobe Commerce as a Cloud Service, consulte la siguiente documentación:

   - [Guía del servicio de catálogo](overview.md)
   - [Referencia de API de GraphQL del servicio de catálogo](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/)
   - [Guía de administración de Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-admin/)
   - [Guía de Adobe Commerce as a Cloud Service](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/)
   - [Guía de Adobe Commerce en la nube](https://experienceleague.adobe.com/en/docs/commerce-cloud/)

- Para proyectos que usan **Adobe Commerce Optimizer** o **Conector de Adobe Commerce Optimizer**, consulte la siguiente documentación:

   - [Guía para desarrolladores de Merchandising Services](https://developer.adobe.com/commerce/services/optimizer/)
   - [Referencia de API de GraphQL de comercialización](https://developer.adobe.com/commerce/services/reference/graphql/)
   - [Guía de Adobe Commerce Optimizer](../optimizer/overview.md)
