---
title: Notas de la versión [!DNL Product Recommendations]
description: La información de la versión más reciente de  [!DNL Product Recommendations]  de Adobe Commerce.
feature: Services, Recommendations, Release Notes
exl-id: 37404605-5b62-4c71-90d1-4f09e6105c4b
source-git-commit: 30cbe1ed54dd8a1149afe9f5f77b1b6f543b277e
workflow-type: tm+mt
source-wordcount: '1878'
ht-degree: 0%

---

# Notas de la versión [!DNL Product Recommendations]

Las notas de la versión contienen actualizaciones de los siguientes [!DNL Product Recommendations] módulos:

* [!DNL Product Recommendations] metapaquete: `magento/product-recommendations`
* Compatibilidad con Page Builder en el módulo [!DNL Product Recommendations] (opcional): `magento/module-page-builder-product-recommendations`
* Compatibilidad de tipo de recomendación de similitud visual para el módulo [!DNL Product Recommendations] (opcional): `magento/module-visual-product-recommendations`

Se proporciona soporte para la última versión. Las notas de la versión de las versiones anteriores se proporcionan como referencia.
Las notas de la versión incluyen:

![Nuevas](../assets/new.svg) nuevas características
![Corrección](../assets/fix.svg) Correcciones y mejoras
![Error](../assets/bug.svg) Problemas conocidos

Consulte la documentación para desarrolladores para [obtener más información sobre la compatibilidad del producto](https://experienceleague.adobe.com/en/docs/commerce-operations/release/product-availability).

## Actualizaciones de servicios alojados

Estas notas describen actualizaciones o problemas conocidos que se publicaron o descubrieron fuera de una versión o mejoras en el servicio alojado.

_19 de noviembre de 2025_

![Nuevo](../assets/new.svg): ahora puede crear hasta 50 unidades de recomendación activas para cada tipo de página. Anteriormente, el límite era de cinco.

_1 de octubre de 2025_

![Nuevo](../assets/new.svg) agregó una nueva clave de almacenamiento de datos denominada `ds-logged-in` para los datos de inicio de sesión del cliente.

_31 de enero de 2025_

![Nuevo](../assets/new.svg): hay una nueva directiva de retención de datos para los datos de catálogo no consultados en su entorno de prueba. [Más información](overview.md#catalog-data-retention-policy).

_28 de junio de 2024_

![Error](../assets/bug.svg) Los productos agregados al carro de compras desde una unidad [!DNL Product Recommendations] en la página del carro de compras no se eliminan de la lista de productos recomendados cuando la página del carro de compras se vuelve a cargar.
![Error](../assets/bug.svg) Los productos eliminados del carro de compras continúan en la matriz `cartSkus` hasta que se vuelva a cargar la página del carro de compras.

_18 de julio de 2023_

![Nuevo](../assets/new.svg) [!DNL Product Recommendations] tiene ahora una consulta de GraphQL [`recommendations`](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/).

_25 de abril de 2023_

![Nuevos](../assets/new.svg) clientes de [!DNL Product Recommendations] ahora pueden aprovechar la [indexación de precios SaaS](../price-index/price-indexing.md).

## Versión principal actual

### 6.5.0 magento/product-recommendations

_3 de noviembre de 2025_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Corrección](../assets/fix.svg) mejoró la forma en que las unidades de recomendación de productos interactúan en entornos diferentes.

### Versiones anteriores

### 6.4.0 magento/product-recommendations

_17 de septiembre de 2025_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Corrección](../assets/fix.svg) resolvió un problema intermitente en el que las unidades de recomendación de productos desaparecían debido a un error de JavaScript cuando los datos de almacenamiento local no estaban disponibles. Esta corrección garantiza que PREX ya no genera errores si falta `ds-view-history-time-decay` en el almacenamiento local.
![Nuevo](../assets/new.svg) se han actualizado las direcciones URL de la red de distribución de contenido (CDN) para `recommendations-sdk` al dominio `adobe.io`.

### 6.3.0 de magento/product-recommendations

_5 de septiembre de 2025_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg) agregó compatibilidad para mostrar métricas para [unidades de recomendación de PageBuilder](page-builder.md) creadas en vistas de tienda no predeterminadas dentro del área de trabajo de [Product Recommendations](workspace.md).
![Las nuevas](../assets/new.svg) recomendaciones de productos ahora respetan completamente el [modo de restricción de cookies](setting-cookie.md) al impedir la recopilación y el almacenamiento de datos en cookies o el almacenamiento local cuando las restricciones están habilitadas.

### 6.2.1 de magento/product-recommendations

_14 de julio de 2025_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Corrección](../assets/fix.svg) realizó mejoras en el panel [previsualizar recomendaciones](./create.md#preview-recommendations).

### 6.2.0 de magento/product-recommendations

_4 de abril de 2025_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg) Se han actualizado las direcciones URL de CDN para `recommendations-admin-ui` en el dominio `adobe.io`.

### 6.1.0 de magento/product-recommendations

_11 de marzo de 2025_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg) agregó compatibilidad con PHP 8.4.

### 6.0.3 de magento/product-recommendations

_6 de noviembre de 2024_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Corregir](../assets/fix.svg) Se corrigió un problema en el cual el filtro de [categoría](filters.md#category) incluía categorías que no pertenecían a la vista de tienda actual.
![Corregir](../assets/fix.svg) Se corrigió un problema de dependencia en el metapaquete `magento/product-recommendations`.

### 6.0.2 de magento/product-recommendations

_9 de mayo de 2024_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Corrección](../assets/fix.svg) Se ha corregido un problema que causaba que, al hacer clic en el botón **[!DNL Add to Cart]** de un producto simple dentro de una unidad de Recomendaciones de productos, se redirigiera al comprador a la página principal en lugar de permanecer en la página actual.
![Error](../assets/bug.svg) Hay un error de validación causado por el elemento `referenceBlock` en el archivo XML `ProductRecommendations Layout`.

### 6.0.1 de magento/product-recommendations

_19 de marzo de 2024_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg) agregó compatibilidad con PHP 8.3.

### 6.0.0 de magento/product-recommendations

_22 de febrero de 2024_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg) El [!DNL Catalog Sync Dashboard] es ahora el [[!DNL Data Management Dashboard]](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard). Este panel modificado proporciona información sobre las secuencias de datos de [!DNL Product Recommendations], [!DNL Live Search] y [!DNL Catalog Service].
![Corregir](../assets/fix.svg) Se corrigió un problema que causaba errores de desprotección para [!DNL Product Recommendations].

+++5.0.0 y anteriores

### 5.0.1 de magento/product-recommendations

_15 de septiembre de 2023_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg) Se agregaron nuevos módulos para admitir el [Indizador de precios Saas](../price-index/price-indexing.md).
![Nuevo](../assets/new.svg) Se agregaron nuevos módulos de exportación de datos para admitir la exportación de más tipos de productos, incluidos productos agrupados y tarjetas regalo.
![Corrección](../assets/fix.svg) El tamaño de tabla de las fuentes Products y Price se ha reducido considerablemente. Las tablas `catalog_data_exporter_products` y `catalog_data_exporter_product_prices` deberían ver una reducción de tamaño sustancial.

#### Limitaciones conocidas

* El valor `websiteCode` se devuelve incorrectamente si contiene un guion bajo (_).

### 5.0.0 de magento/product-recommendations

_20 de marzo de 2023_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg) se ha actualizado [!DNL Product Recommendations] para admitir Adobe Commerce 2.4.6.
![Nuevo](../assets/new.svg) Esta es una versión principal. [Editar](install-configure.md#update) el archivo raíz `composer.json` de su proyecto.
![Nuevo](../assets/new.svg) [!DNL Product Recommendations] ahora admite las capacidades completas de [Inventory management](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/introduction) en Commerce (anteriormente conocido como Multi-Source Inventory o MSI). Para habilitar la compatibilidad total, debe [actualizar](install-configure.md#update) el módulo de dependencia `commerce-data-export` a la versión 102.2.0+.

### 4.0.1 de magento/product-recommendations

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Corrección](../assets/fix.svg) Anteriormente, [!DNL Product Recommendations] mostraba un error cuando la moneda de visualización se cambiaba a una moneda no predeterminada. El cambio de moneda ahora funciona correctamente.

### 4.0.0 de magento/product-recommendations

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.4 y posteriores

![Nuevo](../assets/new.svg) agregó [indicadores de preparación](create.md) para ayudarle a visualizar el progreso de entrenamiento de cada tipo de recomendación.
![Nuevo](../assets/new.svg) Esta es una versión principal. [Editar](install-configure.md#update) el archivo raíz `composer.json` de su proyecto. Esta versión también requiere que proporcione dos claves API al instalar y configurar [!DNL Product Recommendations]: [una clave de producción y una clave de zona protegida](../landing/saas.md).

#### Limitaciones conocidas

* El valor `websiteCode` se devuelve incorrectamente si contiene un guion bajo (_).

### 3.3.7 de magento/product-recommendations

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.x y posteriores

![Nuevo](../assets/new.svg) agregó compatibilidad con PHP 8.1
![Nuevo](../assets/new.svg) se ha mejorado el cambio de tamaño de las imágenes para que el tamaño se gestione de forma más coherente en la plantilla de visualización de referencia

### 3.3.6 de magento/product-recommendations

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.x y posteriores

![Nuevo](../assets/new.svg) optimizó el metapaquete [!DNL Product Recommendations] enumerando explícitamente las dependencias

### 3.3.5 de magento/product-recommendations

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.x y posteriores

![Nuevo](../assets/new.svg) agregó [compatibilidad con B2B](onboarding.md#b2bsupport) en [!DNL Product Recommendations]
![Nuevo](../assets/new.svg) agregó nuevas fuentes a [sincronizar datos del catálogo](https://experienceleague.adobe.com/en/docs/commerce/user-guides/data-services/catalog-sync) con los servicios de Commerce a través de la línea de comandos

### 3.3.3 de magento/product-recommendations

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.x y posteriores

![Nuevo](../assets/new.svg) agregó [tipos de recomendación](type.md) nuevos: Conversión (ver al carro de compras), Conversión (ver para comprar) y Vistos recientemente. Estos nuevos tipos de recomendación están disponibles en el módulo 3.2.2 y versiones posteriores de `magento/product-recommendations`.
![Corregir](../assets/fix.svg) Se corrigió un problema en el cual Firewall de aplicaciones web de Fastly (WAF) bloqueaba incorrectamente una cookie
![Corrección](../assets/fix.svg) Se ha corregido un problema por el que los productos asignados a la vista de tienda no predeterminada no se mostraban en el panel _Vista previa de productos de Recommendations_ al crear una recomendación para esa vista de tienda específica
![Corregir](../assets/fix.svg) Se ha corregido un problema por el cual algunos nombres de unidades de recomendación en Page Builder impedían que se mostrara la unidad de recomendación en la tienda

### 3.3.2 de magento/product-recommendations

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.x y posteriores

![Corrección](../assets/fix.svg) Se ha corregido la dependencia que faltaba para la compatibilidad con B2B

### 3.3.1 de magento/product-recommendations

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.x y posteriores

![Nuevo](../assets/new.svg) agregó compatibilidad con los precios de grupos de clientes B2B. Cuando establece un [filtro de precios](filters.md) en una unidad de recomendación, los clientes de B2B que iniciaron sesión ven el conjunto de precios del grupo de clientes para los productos mostrados.

### 3.3.0 de magento/product-recommendations

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.x y posteriores

![Nuevo](../assets/new.svg) Se agregó compatibilidad con la capa de datos del cliente de Adobe para estandarizar la recopilación de datos de comportamiento en las características y servicios de Adobe Commerce. Consulte [readme](https://github.com/adobe/commerce-events/blob/main/packages/storefront-events-collector/README.md) para obtener más información.

### 3.2.6 de magento/product-recommendations

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.x y posteriores

![Corregir](../assets/fix.svg) se corrigió un error modal de JavaScript
![Corregir](../assets/fix.svg) Se corrigió un problema en el cual Firewall de aplicaciones web de Fastly (WAF) bloqueaba incorrectamente una cookie

### 3.2.5 de magento/product-recommendations

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.x y posteriores

![Nuevo](../assets/new.svg) cambió el nombre de los servicios de Magento a [Servicios de Commerce](https://experienceleague.adobe.com/en/docs/commerce/user-guides/integration-services/saas) y mejoró el uso en el administrador

### 3.2.4 de magento/product-recommendations

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.x y posteriores

![Corrección](../assets/fix.svg) Se corrigió el error &quot;No se pueden recuperar los datos de opciones de productos configurables&quot; al indexar atributos de productos

### 3.2.3 de magento/product-recommendations

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.x y posteriores

![Corrección](../assets/fix.svg) Se corrigió el error &quot;No se pueden recuperar los datos de las opciones de productos configurables&quot; durante la sincronización del catálogo
![Corrección](../assets/fix.svg) Se ha corregido un problema por el cual el código de tienda no se configuraba correctamente al habilitar la configuración &quot;Agregar código de tienda a URL&quot;
![Corrección](../assets/fix.svg) Se ha mejorado la detección de los cambios de configuración del Panel de administración para garantizar que estos cambios se reflejen en los datos de sincronización de catálogos

### 3.2.2 de magento/product-recommendations

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.x y posteriores

![Nuevo](../assets/new.svg) agregó la capacidad de [previsualizar resultados de recomendaciones](create.md) en el momento de la creación. Esto puede requerir que actualice el módulo a la versión más reciente.
![Nuevo](../assets/new.svg) agregó la capacidad para [supervisar y administrar](https://experienceleague.adobe.com/en/docs/commerce/user-guides/data-services/catalog-sync) el proceso de sincronización del catálogo desde el administrador.
![Nuevo](../assets/new.svg) agregó [filtros](filters.md) para controlar qué productos se muestran en las recomendaciones.
![Nuevo](../assets/new.svg) agregó el tipo de recomendación [Similitud visual](type.md#visualsim).

### 1.2.1 de magento/module-page-builder-product-recommendations para Page Builder

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.x y posteriores

![Nuevo](../assets/new.svg) agregó compatibilidad con la versión 3.2.0+ del módulo `magento/product-recommendations`

### 3.1.0 de magento/product-recommendations

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.x y posteriores

![Nuevo](../assets/new.svg) agregó la capacidad para [resincronizar](https://experienceleague.adobe.com/en/docs/commerce/user-guides/data-services/catalog-sync) su catálogo a los servicios SaaS a través de la línea de comandos.
![Nuevo](../assets/new.svg) agregó compatibilidad con los prefijos de tabla de base de datos
![Corrección](../assets/fix.svg) eliminó la compatibilidad con PHP 7.1

### 3.0.8 de magento/product-recommendations

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.x y posteriores

![Corrección](../assets/fix.svg) Se ha corregido un problema por el cual se enviaban eventos para la recopilación de datos antes de configurar el módulo, lo que provocaba un tráfico no válido

### 3.0.6 de magento/product-recommendations

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.x y posteriores

![Nuevo](../assets/new.svg) **(Beta)** Incluye compatibilidad con el nuevo tipo de recomendación [Similitud visual](type.md#visualsim).

### 1.0.0 de magento/module-visual-product-recommendations

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.x y posteriores

![Nuevo](../assets/new.svg) **(Beta)** [Similar visual](type.md#visualsim). Con el tipo de recomendación _Similitud visual_, puede implementar una unidad de recomendación en la página de detalles del producto que muestre productos visualmente similares al producto que se está viendo.

### 3.0.5 de magento/product-recommendations

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.x y posteriores

![Corrección](../assets/fix.svg) Se ha corregido el error &quot;No se pueden recuperar los datos de las opciones del producto&quot; que se podía producir durante la exportación del catálogo.
![Corrección](../assets/fix.svg) El símbolo de moneda de la columna _Ingresos_ del panel _[!DNL Product Recommendations]_ahora refleja correctamente la moneda base configurada.

### 3.0.4 de magento/product-recommendations

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.x y posteriores

![Corrección](../assets/fix.svg) se agregó compatibilidad con Adobe Commerce 2.4.0

### 3.0.3 de magento/product-recommendations

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.x y posteriores

![Corrección](../assets/fix.svg): se ha mejorado la implementación de símbolos en la plantilla de tienda

### 1.0.4 de magento/module-page-builder-product-recommendations para Page Builder

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.x y posteriores

![Nuevo](../assets/new.svg) nombre de recomendación de producto agregado al editar el tipo de contenido de Page Builder

### 3.0.2 magento/product-recommendations

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.x y posteriores

![Nuevo](../assets/new.svg) agregó una columna de estado en la cuadrícula al seleccionar Unidades de recomendación en Page Builder
![Corregir](../assets/fix.svg) Se ha corregido un problema con los protocolos http/https incorrectos en las direcciones URL de productos e imágenes

### 3.0.1 de magento/product-recommendations

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.x y posteriores

Esta es una versión principal. [Editar](install-configure.md#update) el archivo root composer.json de su proyecto.

![Nuevo](../assets/new.svg) Recuperar [!DNL Product Recommendations] de espacios de datos SaaS alternativos. Esto le permite usar [!DNL Product Recommendations] calculado en el entorno del producto en otros entornos que no sean de producción. [Cambiar espacios de datos SaaS](settings.md) describe más esta característica.

![Corregir](../assets/fix.svg) Se corrigió un problema por el cual el cierre de compra se inhibía para los compradores que usaban uBlock Origin
![Corregir](../assets/fix.svg) se ha corregido un problema que enviaba eventos de complemento al carro de compras superfluos

### 1.0.3 de magento/module-page-builder-product-recommendations para Page Builder

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.x y posteriores

![Nueva](../assets/new.svg) compatibilidad con Page Builder. Con la integración de Page Builder, puede colocar unidades de Recommendations de forma precisa y granular en cualquier ubicación arbitraria del contenido creado por Page Builder. También puede aplicar estilo a los encabezados y a las unidades de recomendación. Vaya a [Page Builder](https://experienceleague.adobe.com/en/docs/commerce-admin/page-builder/add-content/recommendations) para obtener más información.

### 2.0.0 de magento/product-recommendations

[!BADGE Compatible]{type=Informative tooltip="Admitido"} versiones de Adobe Commerce 2.4.x y posteriores

![Nuevo](../assets/new.svg) lanzamiento de disponibilidad general.

+++

## Documentación

Para obtener más información acerca del desarrollo de [!DNL Product Recommendations] y [!DNL Product Recommendations]:

* [Guía del usuario](overview.md)
* [Documentación para desarrolladores](https://experienceleague.adobe.com/en/docs/commerce/product-recommendations/developer/development-overview)
