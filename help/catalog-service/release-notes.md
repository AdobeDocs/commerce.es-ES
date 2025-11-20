---
title: Notas de la versión [!DNL Catalog Service]
description: La información de la versión más reciente de  [!DNL Catalog Service]  para Adobe Commerce.
feature: Services, Catalog Service, Release Notes
exl-id: 74f2e46a-5592-4857-a6d7-b95b85d8b4cc
source-git-commit: 93adab667d1d8ed40c9d5668db376493bd8ae684
workflow-type: tm+mt
source-wordcount: '1020'
ht-degree: 0%

---

# Notas de la versión [!DNL Catalog Service]

Estas notas de la versión describen las versiones más recientes de [!DNL Catalog Service].
Se proporciona soporte para la versión publicada principal actual. Las notas de la versión de las versiones anteriores se proporcionan como referencia.
Las actualizaciones incluyen:

![Nuevas](../assets/new.svg) nuevas características
![Corrección](../assets/fix.svg) Correcciones y mejoras
![Error](../assets/bug.svg) Problemas conocidos

## Versión principal actual

### Versión V1.26

_22 de octubre de 2024_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg) El esquema de GraphQL ahora incluye el atributo `lastModifiedAt` en la información del producto. Esta marca de tiempo precisa ayuda a los clientes a asegurarse de que los mapas del sitio reflejen con precisión las actualizaciones más recientes de sus productos. También ayuda a los motores de búsqueda como Google a determinar cuándo es necesaria la reindexación, optimizando el proceso de rastreo y evitando problemas relacionados con las últimas fechas de modificación agresivas utilizadas cuando no se dispone de información precisa. <!--DATA-6209-->

## Versiones anteriores

+++ Versiones anteriores

### Versión 1.23

_22 de agosto de 2024_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Corrección](../assets/fix.svg) Ahora puede recuperar información de productos sin datos de anulación de productos (precios). En versiones anteriores, estas consultas devolvían el siguiente error:
`The following sku does not have product override data in the DB: <SKU value>. Make sure data is synced.` <!--DATA-6121-->

### Versión 1.22

_13 de agosto de 2024_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg) se agregó soporte para recuperar todas las variantes por SKU del producto. Consulte la [Referencia de API del servicio de catálogo](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/). <!--DATA-6067-->

### Versión 1.22

_13 de agosto de 2024_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg) se agregó soporte para recuperar todas las variantes por SKU del producto. Consulte la [Referencia de API del servicio de catálogo](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/). <!--DATA-6067-->

### Versión V1.19

_23 de mayo de 2024_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores


![Corrección](../assets/fix.svg) <!--DATA-5033-->El indicador `InStock` para los valores de opción ahora tiene en cuenta el estado `enabled` de ámbito de la variante del producto.

![Corrección](../assets/fix.svg) <!--DATA-5888-->Agregue soporte para precios de productos que requieran números grandes (hasta 16 dígitos) y mayor precisión decimal (hasta 4 decimales). Para aplicar las actualizaciones de la configuración de precios al catálogo existente, vuelva a sincronizar los datos del catálogo desde el [panel de administración de datos](https://experienceleague.adobe.com/es/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard) o mediante la [interfaz de línea de comandos de Adobe Commerce](../landing/catalog-sync.md#command-line-interface).

#### Limitaciones conocidas

Las siguientes funciones aún no son compatibles:

* El tamaño máximo de la carga útil de atributos dinámicos es 9 MB.
* El precio del producto del grupo se puede calcular con precios de productos simples.
* En una matriz de imágenes, solo la primera imagen contiene funciones.

Resuelva las siguientes limitaciones utilizando API Mesh y la API principal de GraphQL:

* Precio Mínimo Anunciado
* Precios de nivel
* Paquete de productos con precios fijos

Para obtener detalles y ejemplos, consulte [Servicio de catálogo y malla de API](mesh.md)

### Versión V1.18

_11 de abril de 2024_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg) agregó compatibilidad con PHP 8.3.

![Nuevas](../assets/new.svg) Las consultas [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/) y [`refineProduct`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/) ahora devuelven datos de opciones personalizables para productos simples y complejos.<!--DATA-5538-->

### Versión V1.17

_22 de febrero de 2024_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg) El [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html?lang=es) ya está disponible. Este panel modificado proporciona información sobre las secuencias de datos de [!DNL Product Recommendations], [!DNL Live Search] y [!DNL Catalog Service]. La compatibilidad con esta característica se introdujo en la versión 3.1.0 del metapaquete `catalog-service`.

### Versión V1.16

_13 de febrero de 2024_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

La API del servicio de catálogo admite ahora ![nuevos](../assets/new.svg) vídeos de producto.
![Corregir](../assets/fix.svg) Las opciones sin existencias ahora se muestran en el widget PDP.

#### Limitaciones conocidas

Estas funciones aún no son compatibles:

* El tamaño máximo de la carga útil de atributos dinámicos es 9 MB.
* Precio del producto del grupo. Este valor se puede calcular con precios de productos simples.
* En una matriz de imágenes, solo la primera imagen contiene funciones.

Las siguientes limitaciones se pueden resolver mediante API Mesh y la API principal de GraphQL:

* Precio Mínimo Anunciado
* [Precios de nivel](mesh.md)

### Versión V1.13

_12 de octubre de 2023_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

El servicio de catálogo ![New](../assets/new.svg) admite el indicador `inStock` para las variantes de producto.
![Nuevo](../assets/new.svg) Los campos `urlKey` y `externalId` se han agregado al esquema de GraphQL.
Ahora se admiten ![nuevos](../assets/new.svg) productos descargables y tarjetas regalo.

### Versión V1.12

_19 de septiembre de 2023_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

El servicio de catálogo ![New](../assets/new.svg) ahora usa [indización de precios SaaS](../price-index/price-indexing.md).
![Corrección](../assets/fix.svg) Esta versión contiene correcciones de errores y mejoras en el servicio.

### Versión V1.11

_18 de julio de 2023_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

El servicio de catálogo ![New](../assets/new.svg) admite ahora la consulta de GraphQL [`recommendations`](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/) para Product Recommendations.

### Versión V1.10

_27 de junio de 2023_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg): la API del servicio de catálogo ahora admite `related products`.

### Versión V1.7

_12 de abril de 2023_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

El servicio de catálogo ![New](../assets/new.svg) ahora limpia las variantes de producto eliminadas.
![Corregir](../assets/fix.svg) mejoras de rendimiento y escalabilidad de la infraestructura.

### Versión V1.6

_28 de marzo de 2023_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg) agregó muestras a la consulta [`products`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/).
![Nuevo](../assets/new.svg) agregó la capacidad para obtener `entityId` mediante [API Mesh](mesh.md).

### Versión V1.5

_6 de marzo de 2023_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg) agregó la funcionalidad de GraphQL [`categories`](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/).
![Corrección](../assets/fix.svg): rendimiento y escalabilidad de API mejorados.

### Versión V1.4

_7 de febrero de 2023_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.x y posteriores

![Nuevo](../assets/new.svg) paquete de servicio de catálogo publicado para simplificar los pasos de instalación.
![Corrección](../assets/fix.svg) de escalabilidad y mejoras de rendimiento de API.

### Versión V1.3

_17 de enero de 2023_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.x y posteriores

![Nuevo](../assets/new.svg) ha simplificado y mejorado la experiencia de incorporación.
![Nuevos](../assets/new.svg) nuevos extremos de zona protegida del cliente disponibles para pruebas previas a la producción.
![Se ha agregado compatibilidad con New](../assets/new.svg) para productos virtuales.
![Corrección](../assets/fix.svg) de escalabilidad y mejoras de rendimiento de API.

### Versión V1.1

_18 de noviembre de 2022_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.x y posteriores

El servicio de catálogo ![New](../assets/new.svg) ahora es compatible con la [malla de API](https://developer.adobe.com/graphql-mesh-gateway/) de Adobe.
![Corrección](../assets/fix.svg): se mejoró la escalabilidad de la API y el rendimiento general.

### Versión 1.0

_4 de octubre de 2022_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.x y posteriores

![Nuevo](../assets/new.svg) ahora admite productos agrupados y agrupados.
![Nuevo](../assets/new.svg) agregó invalidaciones de visibilidad B2B. Ahora se pueden buscar productos y se pueden agregar al carro de compras para grupos de clientes específicos.
El servicio ![Fix](../assets/fix.svg) es ahora más estable y ha mejorado el rendimiento.

### Versión 0.3: Beta+

_12 de septiembre de 2022_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.x y posteriores

![Nuevas](../assets/new.svg) imágenes para compatibilidad con variantes: las imágenes de producto se devuelven según las opciones seleccionadas
![Nuevos](../assets/new.svg) roles para soporte de precios: permitir que solo los miembros de grupos de clientes específicos vean el precio de los productos
![Corrección](../assets/fix.svg): se ha mejorado la estabilidad y el rendimiento del servicio
![Se reciben nuevas](../assets/new.svg) actualizaciones cuando los productos se eliminan del catálogo

### Versión de Beta

_9 de agosto de 2022_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.x y posteriores

![Nuevo](../assets/new.svg) Las consultas `products` y `refineProduct` devuelven los siguientes datos:

* Atributos de producto predefinidos (del sistema).
* Atributos de producto dinámicos y filtrarlos por función (página de visualización de producto/página de lista de productos).
* Opciones de producto.
* Imágenes de productos y filtrarlas por función (PDP/PLP).
* Un precio específico para productos simples y rangos de precios para productos configurables.
* Precios de grupo de clientes e intervalos de precios. Devuelven un precio predeterminado alternativo para los compradores sin grupo de clientes.
* Tipos de productos que utilizan precios específicos del cliente B2B.
