---
title: Recopilar datos
description: Descubra cómo los eventos recopilan datos para  [!DNL Product Recommendations].
feature: Services, Recommendations, Eventing
exl-id: 0d5317e3-c049-4fcd-a8e4-228668d89386
source-git-commit: 458f34c45406db871ec61ff408aa624f163b6ee0
workflow-type: tm+mt
source-wordcount: '980'
ht-degree: 0%

---

# Recopilar datos

Al instalar y configurar [[!DNL Product Recommendations]](install-configure.md), el módulo implementa la recopilación de datos de comportamiento en la tienda. Este mecanismo recopila datos de comportamiento anónimos de los compradores y alimenta a [!DNL Product Recommendations]. Por ejemplo, el evento `view` se usa para calcular el tipo de recomendación `Viewed this, viewed that`, y el evento `place-order` se usa para calcular el tipo de recomendación `Bought this, bought that`.

Consulte la [documentación para desarrolladores](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#product-recommendations) para obtener más información sobre los datos de comportamiento que recopilan los eventos de [!DNL Product Recommendations].

>[!NOTE]
>
>La recopilación de datos a los efectos de [!DNL Product Recommendations] no incluye información de identificación personal (PII). Todos los identificadores de usuario, como los ID de cookie y las direcciones IP, se anonimizan estrictamente. Más información [más](https://www.adobe.com/privacy/experience-cloud.html).

## Clientes sanitarios

Si es cliente de atención médica e instaló la extensión HIPAA de [Data Services](../data-connection/hipaa-readiness.md#installation), que forma parte de la extensión [Data Connection](../data-connection/overview.md), ya no se capturarán los datos de evento de tienda que usa [!DNL Product Recommendations]. Esto se debe a que los datos de evento de tienda se generan en el lado del cliente. Para seguir capturando y enviando datos de evento de tienda, vuelva a habilitar la recopilación de eventos para [!DNL Product Recommendations]. Consulte [configuración general](https://experienceleague.adobe.com/es/docs/commerce-admin/config/general/general#data-services) para obtener más información.

## Tipos de datos y eventos

Existen dos tipos de datos utilizados en Product Recommendations:

- **Comportamiento**: datos de la participación de un comprador en el sitio, como vistas de productos, elementos agregados al carro de compras y compras.
- **Catálogo**: metadatos de producto, como nombre, precio, disponibilidad, etc.

Al instalar el módulo `magento/product-recommendations`, Adobe AI agrega los datos de comportamiento y catálogo, creando Product Recommendations para cada tipo de recomendación. A continuación, el servicio Recomendaciones de productos implementa esas recomendaciones en la tienda en forma de widget que contiene el producto recomendado _items_.

Algunos tipos de recomendación utilizan datos de comportamiento de los compradores para entrenar modelos de aprendizaje automático y crear recomendaciones personalizadas. Otros tipos de recomendación solo utilizan datos de catálogo y no utilizan datos de comportamiento. Si desea empezar a utilizar Product Recommendations rápidamente en su sitio, puede utilizar los siguientes tipos de recomendaciones solo de catálogo:

- `More like this`
- `Visual similarity`

### Inicio en frío

¿Cuándo puede empezar a utilizar tipos de recomendación que utilicen datos de comportamiento? Depende de ti. Este problema se conoce como _Inicio en frío_.

El problema de _arranque en frío_ se refiere al tiempo que tarda un modelo en entrenar y en ser efectivo. Para las recomendaciones de productos, esto significa esperar a que la IA de Adobe recopile datos suficientes para entrenar sus modelos de aprendizaje automático antes de implementar unidades de recomendación en el sitio. Cuantos más datos tengan los modelos, más precisas y útiles serán las recomendaciones. Dado que la recopilación de datos se produce en un sitio activo, es mejor iniciar este proceso antes de tiempo instalando y configurando el módulo `magento/production-recommendations`.

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

#### Advertencias

- Los bloqueadores de anuncios y la configuración de privacidad pueden impedir que se recopilen eventos y provocar que las [métricas](workspace.md#column-descriptions) de participación e ingresos no se comuniquen correctamente. Además, es posible que algunos eventos no se envíen debido a que los compradores abandonan la página o a problemas de red.
- [Implementaciones sin encabezado](headless.md) deben implementar eventos para activar el panel Recomendaciones de productos.
- Para los productos configurables, las recomendaciones de productos utilizan la imagen del producto principal en la unidad de recomendación. Si el producto configurable no tiene una imagen especificada, la unidad de recomendación estará vacía para ese producto específico.

>[!NOTE]
>
>Si el [Modo de restricción de cookies](https://experienceleague.adobe.com/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law.html?lang=es) está habilitado, Adobe Commerce no recopilará datos de comportamiento hasta que el comprador acepte el uso de cookies. Si el modo de restricción de cookies está deshabilitado, Adobe Commerce recopila datos de comportamiento de forma predeterminada.
