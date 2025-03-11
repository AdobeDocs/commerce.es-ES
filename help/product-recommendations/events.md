---
title: Recopilar datos
description: Descubra cómo los eventos recopilan datos para  [!DNL Product Recommendations].
feature: Services, Recommendations, Eventing
exl-id: 0d5317e3-c049-4fcd-a8e4-228668d89386
source-git-commit: 94d2a9911ab10d164d75779d1f310e5bdf2aea74
workflow-type: tm+mt
source-wordcount: '1360'
ht-degree: 0%

---

# Recopilar datos

Al instalar y configurar características de Adobe Commerce basadas en SaaS como [[!DNL Product Recommendations]](install-configure.md) o [[!DNL Live Search]](../live-search/install.md), los módulos implementan la recopilación de datos de comportamiento en la tienda. Este mecanismo recopila datos de comportamiento anónimos de los compradores y alimenta a [!DNL Product Recommendations]. Por ejemplo, el evento `view` se usa para calcular el tipo de recomendación `Viewed this, viewed that`, y el evento `place-order` se usa para calcular el tipo de recomendación `Bought this, bought that`.

>[!NOTE]
>
>La recopilación de datos a los efectos de [!DNL Product Recommendations] no incluye información de identificación personal (PII). Todos los identificadores de usuario, como los ID de cookie y las direcciones IP, se anonimizan estrictamente. Más información [más](https://www.adobe.com/privacy/experience-cloud.html).

## Clientes sanitarios

Si es cliente de atención médica e instaló la extensión HIPAA de [Data Services](../data-connection/hipaa-readiness.md#installation), que forma parte de la extensión [Data Connection](../data-connection/overview.md), ya no se capturarán los datos de evento de tienda que usa [!DNL Product Recommendations]. Esto se debe a que los datos de evento de tienda se generan en el lado del cliente. Para continuar capturando y enviando datos de evento de tienda, vuelva a habilitar la colección de eventos para [!DNL Product Recommendations]. Consulte [configuración general](https://experienceleague.adobe.com/en/docs/commerce-admin/config/general/general.html#data-services) para obtener más información.

## Tipos de datos y eventos

Existen dos tipos de datos utilizados en Product Recommendations:

- **Comportamiento**: datos de la participación de un comprador en el sitio, como vistas de productos, elementos agregados al carro de compras y compras.
- **Catálogo**: metadatos de producto, como nombre, precio, disponibilidad, etc.

Al instalar el módulo `magento/product-recommendations`, Adobe Sensei agrega los datos de comportamiento y catálogo, creando Product Recommendations para cada tipo de recomendación. A continuación, el servicio Recomendaciones de productos implementa esas recomendaciones en la tienda en forma de widget que contiene el producto recomendado _items_.

Algunos tipos de recomendación utilizan datos de comportamiento de los compradores para entrenar modelos de aprendizaje automático y crear recomendaciones personalizadas. Otros tipos de recomendación solo utilizan datos de catálogo y no utilizan datos de comportamiento. Si desea empezar a utilizar Product Recommendations rápidamente en su sitio, puede utilizar los siguientes tipos de recomendaciones solo de catálogo:

- `More like this`
- `Visual similarity`

### Inicio en frío

¿Cuándo puede empezar a utilizar tipos de recomendación que utilicen datos de comportamiento? Depende de ti. Este problema se conoce como _Inicio en frío_.

El problema de _arranque en frío_ se refiere al tiempo que tarda un modelo en entrenar y en ser efectivo. Para las recomendaciones de productos, esto significa esperar a que Adobe Sensei recopile datos suficientes para entrenar sus modelos de aprendizaje automático antes de implementar unidades de recomendaciones en el sitio. Cuantos más datos tengan los modelos, más precisas y útiles serán las recomendaciones. Dado que la recopilación de datos se produce en un sitio activo, es mejor iniciar este proceso antes de tiempo instalando y configurando el módulo `magento/production-recommendations`.

La siguiente tabla proporciona algunas directrices generales sobre la cantidad de tiempo que se tarda en recopilar suficientes datos para cada tipo de recomendación:

| Tipo de recomendación | Tiempo de formación | Notas |
|---|---|---|
| Basado en popularidad (`Most viewed`, `Most purchased`, `Most added to cart`) | Varía | Depende del volumen de eventos: las vistas son los más comunes y, por lo tanto, aprende más rápido; luego agrega al carro de compras y, por último, compra |
| `Viewed this, viewed that` | Requiere más formación | El volumen de las vistas de productos es decentemente alto |
| `Viewed this, bought that`, `Bought this, bought that` | Requiere la mayor cantidad de formación | Los eventos de compra son los eventos más inusuales en un sitio de comercio, especialmente en comparación con las vistas de productos |
| `Trending` | Se necesitan tres días de datos para establecer una línea de base de popularidad | La tendencia es una medida del impulso reciente en la popularidad de un producto en comparación con su propia línea de base de popularidad. La puntuación de tendencia de un producto se calcula mediante un conjunto en primer plano (popularidad reciente en 24 horas) y un conjunto de fondo (línea de base de popularidad en 72 horas). Si la popularidad de un artículo aumenta significativamente dentro de un periodo de 24 horas en comparación con su popularidad de línea de base, entonces recibe una puntuación de tendencia alta. Cada producto tiene esta puntuación y los artículos con la puntuación más alta en cualquier momento comprenden el conjunto de productos de tendencias principales. |

Otras variables que pueden afectar al tiempo necesario para entrenar:

- Un mayor volumen de tráfico contribuye a un aprendizaje más rápido
- Algunos tipos de recomendación se entrenan más rápido que otros
- Adobe Commerce vuelve a calcular los datos de comportamiento cada cuatro horas. Las recomendaciones se vuelven más precisas cuanto más tiempo se utilizan en el sitio.

Para ayudarle a visualizar el progreso de formación de cada tipo de recomendación, la página [crear recomendación](create.md#readiness-indicators) muestra indicadores de preparación.

Mientras se recopilan los datos en el sitio activo y se imparten los modelos de aprendizaje automático, puede finalizar otras tareas de prueba y configuración necesarias para configurar las recomendaciones. Cuando haya terminado con este trabajo, los modelos tendrán datos suficientes para crear recomendaciones útiles, lo que le permitirá implementarlas en su tienda.

Si el sitio no recibe tráfico suficiente (vistas, compras, tendencias) para la mayoría de los SKU de producto, es posible que no haya suficientes datos para completar el proceso de aprendizaje. Esto puede hacer que el indicador de disponibilidad del administrador parezca atascado. Los indicadores de preparación están pensados para proporcionar a los comerciantes otro punto de datos a la hora de elegir qué tipo de recomendaciones es mejor para su tienda. Los números son una guía y es posible que nunca alcancen el 100%. [Más información](create.md#readiness-indicators) sobre los indicadores de preparación.

### Recomendaciones de copia de seguridad {#backuprecs}

Si los datos de entrada no son suficientes para proporcionar todos los elementos de recomendación solicitados en una unidad, Adobe Commerce proporciona recomendaciones de copia de seguridad para rellenar las unidades de recomendación. Por ejemplo, si implementa el tipo de recomendación `Recommended for you` en su página de inicio, un comprador que visita por primera vez su sitio no ha generado suficientes datos de comportamiento para recomendar con precisión productos personalizados. En este caso, Adobe Commerce muestra artículos basados en el tipo de recomendación `Most viewed` a este comprador.

En caso de que la recopilación de datos de entrada sea insuficiente, los siguientes tipos de recomendación vuelven a `Most viewed`:

- `Recommended for you`
- `Viewed this, viewed that`
- `Viewed this, bought that`
- `Bought this, bought that`
- `Trending`
- `Conversion (view to purchase)`
- `Conversion (view to cart)`

### Eventos

El [Recopilador de eventos de Adobe Commerce Storefront](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/#quick-start) enumera todos los eventos implementados en tu tienda. En esa lista, hay un subconjunto de eventos específicos de [!DNL Product Recommendations]. Estos eventos recopilan datos cuando los compradores interactúan con las unidades de recomendación en la tienda y alimentan las métricas para analizar el rendimiento de las recomendaciones.

| Evento | Descripción |
| --- | --- |
| `impression-render` | Se envía cuando se representa la unidad de recomendación en la página. Si una página tiene dos unidades de recomendación (comprado-comprado, ver-ver), se envían dos eventos `impression-render`. Este evento se utiliza para rastrear la métrica en busca de impresiones. |
| `rec-add-to-cart-click` | El comprador hace clic en el botón **Agregar al carro** de un artículo de la unidad de recomendación. |
| `rec-click` | El comprador hace clic en un producto de la unidad de recomendación. |
| `view` | Se envía cuando la unidad de recomendación alcanza al menos el 50 % de visibilidad, por ejemplo desplazándose hacia abajo en la página. Por ejemplo, si una unidad de recomendación tiene dos líneas, se envía un evento `view` cuando el comprador ve una línea más un píxel de la segunda línea. Si el comprador desplaza la página hacia arriba y hacia abajo varias veces, el evento `view` se envía tantas veces como vuelva a ver toda la unidad de recomendación en la página. |

>[!NOTE]
>
>Las métricas de Recomendación de producto están optimizadas para las tiendas de Luma. Si su tienda está implementada con PWA Studio, consulte la [documentación de PWA](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/). Si usa tecnología de front-end personalizada, como React o Vue JS, aprenda a integrar [Recomendaciones de productos en un entorno sin encabezado](headless.md).

#### Eventos de panel requeridos

Se requieren los siguientes eventos para rellenar el [[!DNL Product Recommendations] panel](workspace.md)

| Columna del panel | Eventos | Campo de combinación |
| ---------------- | --------- | ----------- |
| Impresiones | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render` | `unitId` |
| Vistas | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render`, `recs-unit-view` | `unitId` |
| Clics | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-item-click`, `recs-add-to-cart-click` | `unitId` |
| Ingresos | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-item-click`, `recs-add-to-cart-click`, `place-order` | `unitId`, `sku`, `parentSku` |
| Ingresos LT | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-item-click`, `recs-add-to-cart-click`, `place-order` | `unitId`, `sku`, `parentSku` |
| CTR | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render`, `recs-item-click`, `recs-add-to-cart-click` | `unitId`, `sku`, `parentSku` |
| vCTR | `page-view`, `recs-request-sent`, `recs-response-received`, `recs-unit-render`, `recs-unit-view`, `recs-item-click`, `recs-add-to-cart-click` | `unitId`, `sku`, `parentSku` |

Los siguientes eventos no son específicos de las recomendaciones de productos, pero son necesarios para que Adobe Sensei interprete correctamente los datos del comprador:

- `view`
- `add-to-cart`
- `place-order`

#### Tipo de recomendación

En esta tabla se describen los eventos utilizados por cada tipo de recomendación.

| Tipo de recomendación | Eventos | Página |
| --- | --- | --- |
| Más visitados | `page-view`<br>`product-view` | Página de detalles del producto |
| Más comprados | `page-view`<br>`place-order` | Carro/cierre de compra |
| Más añadidos al carro | `page-view`<br>`add-to-cart` | Página de detalles del producto<br>Página de lista de productos<br>Carro<br>Lista de deseos |
| Vio esto, vio aquello. | `page-view`<br>`product-view` | Página de detalles del producto |
| Vio esto, compró aquello. | Recs. de producto | `page-view`<br>`product-view` | Página de detalles del producto<br>Carro/Cierre de compra |
| Compré esto, compré aquello. | Recs. de producto | `page-view`<br>`product-view` | Página de detalles del producto |
| Tendencia | `page-view`<br>`product-view` | Página de detalles del producto |
| Conversión: Ver para comprar | Recs. de producto | `page-view`<br>`product-view` | Página de detalles del producto |
| Conversión: Ver para comprar | Recs. de producto | `page-view`<br>`place-order` | Carro/cierre de compra |
| Conversión: Ver al carro | Recs. de producto | `page-view`<br>`product-view` | Página de detalles del producto |
| Conversión: Ver al carro | Recs. de producto | `page-view`<br>`add-to-cart` | Página de detalles del producto<br>Página de lista de productos<br>Carro<br>Lista de deseos |

#### Advertencias

- Los bloqueadores de anuncios y la configuración de privacidad pueden impedir que se recopilen eventos y provocar que las [métricas](workspace.md#column-descriptions) de participación e ingresos no se comuniquen correctamente. Además, es posible que algunos eventos no se envíen debido a que los compradores abandonan la página o a problemas de red.
- [Implementaciones sin encabezado](headless.md) deben implementar eventos para activar el panel Recomendaciones de productos.
- Para los productos configurables, las recomendaciones de productos utilizan la imagen del producto principal en la unidad de recomendación. Si el producto configurable no tiene una imagen especificada, la unidad de recomendación estará vacía para ese producto específico.

>[!NOTE]
>
>Si el [Modo de restricción de cookies](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html) está habilitado, Adobe Commerce no recopilará datos de comportamiento hasta que el comprador acepte el uso de cookies. Si el modo de restricción de cookies está deshabilitado, Adobe Commerce recopila datos de comportamiento de forma predeterminada.
