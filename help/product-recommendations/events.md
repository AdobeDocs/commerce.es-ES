---
title: Recopilar datos
description: Descubra cómo los eventos recopilan datos para  [!DNL Product Recommendations].
feature: Services, Recommendations, Eventing
exl-id: 0d5317e3-c049-4fcd-a8e4-228668d89386
TQID: https://experienceleague.adobe.com/efHRMj3u3w-xvUgMnEYDpX0D-BDCUyjhhrkMaa3n-xg
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c4147b6e-073b-4d3c-9ab1-d60f2f4434ef
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: eb30f47f-d87a-400f-8f78-63ce7979ff56
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 88a0b1a238090dec85e0f79082d264b720999fee
workflow-type: tm+mt
source-wordcount: 937
ht-degree: 0%

---

# Recopilar datos

Al instalar y configurar [[!DNL Product Recommendations]](install-configure.md), el módulo implementa la recopilación de datos de comportamiento en la tienda. Este mecanismo recopila datos de comportamiento anónimos de los compradores y alimenta a [!DNL Product Recommendations]. Por ejemplo, el evento `view` se usa para calcular el tipo de recomendación `Viewed this, viewed that`, y el evento `place-order` se usa para calcular el tipo de recomendación `Bought this, bought that`.

Para obtener más información acerca de los datos de comportamiento que recopilan los eventos de [!DNL Product Recommendations], consulte la [documentación para desarrolladores](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#product-recommendations).

>[!NOTE]
>
>La recopilación de datos a los efectos de [!DNL Product Recommendations] no incluye información de identificación personal (PII). Todos los identificadores de usuario, como los ID de cookie y las direcciones IP, se anonimizan estrictamente. Más información [más](https://www.adobe.com/privacy/experience-cloud.html).

## Clientes sanitarios

Si es cliente de atención médica y ha instalado la extensión [Data Services HIPAA](../data-connection/hipaa-readiness.md#installation), que se incluye con la extensión [Data Connection](../data-connection/overview.md), [!DNL Product Recommendations] deja de recopilar datos de evento de tienda porque se generan en el lado del cliente.

Para reanudar la recopilación y el envío de datos de evento de tienda, vuelva a habilitar la recopilación de eventos para [!DNL Product Recommendations]. Para obtener más información, consulte [Configuración general](https://experienceleague.adobe.com/es/docs/commerce-admin/config/general/general#data-services).

## Tipos de datos y eventos

Existen dos tipos de datos utilizados en Product Recommendations:

- **Comportamiento**: datos de la participación de un comprador en el sitio, como vistas de productos, elementos agregados al carro de compras y compras.
- **Catálogo**: metadatos de producto, como nombre, precio, disponibilidad, etc.

Al instalar el módulo `magento/product-recommendations`, Adobe AI agrega los datos de comportamiento y catálogo, creando Product Recommendations para cada tipo de recomendación. A continuación, el servicio Recomendaciones de productos implementa esas recomendaciones en la tienda en forma de widget que contiene el producto recomendado _items_.

Algunos tipos de recomendación utilizan los datos de comportamiento de los compradores para entrenar modelos de aprendizaje automático y generar recomendaciones personalizadas. Otros solo dependen de los datos del catálogo. Para empezar a usar Recommendations de productos rápidamente, elija entre los siguientes tipos de recomendación solo de catálogo:

- `More like this`
- `Visual similarity`

### Inicio en frío

¿Cuándo puede empezar a utilizar tipos de recomendación que utilicen datos de comportamiento? Depende de ti. Esta situación se conoce como el problema de _inicio en frío_.

El problema de _inicio en frío_ es el tiempo necesario para que un modelo de aprendizaje automático se entrene antes de que pueda producir recomendaciones efectivas. Para las recomendaciones de productos, Adobe AI debe recopilar datos suficientes para entrenar a sus modelos antes de implementar unidades de recomendación. Por lo general, más datos mejoran la precisión y utilidad de las recomendaciones. Como la recopilación de datos se produce en el sitio activo, inicie este proceso antes de tiempo instalando y configurando el módulo `magento/product-recommendations`.

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

Mientras el sitio activo recopila datos y los modelos de aprendizaje automático se entrenan, complete las tareas de prueba y configuración restantes. Una vez que los modelos tengan datos suficientes para generar recomendaciones útiles, implemente las unidades de recomendación en su tienda.

Si su sitio no recibe tráfico suficiente (vistas, compras o tendencias) para la mayoría de las SKU de productos, es posible que el proceso de aprendizaje no se complete, lo que provoca que los indicadores de preparación en el administrador aparezcan atascados. Los indicadores de preparación ayudan a los comerciantes a elegir el mejor tipo de recomendación para su tienda, pero son solo una guía y es posible que nunca lleguen al 100%. Más información sobre los indicadores de disponibilidad. [Más información](create.md#readiness-indicators) sobre los indicadores de preparación.

### Recomendaciones de copia de seguridad {#backuprecs}

Cuando los datos de entrada insuficientes impiden que una unidad de recomendación devuelva todos los artículos solicitados, Adobe Commerce los rellena con recomendaciones de copia de seguridad. Por ejemplo, después de implementar el tipo de recomendación `Recommended for you` en la página de inicio, es posible que un comprador primerizo no haya generado suficientes datos de comportamiento para recomendaciones personalizadas. En este caso, Adobe Commerce muestra los artículos según el tipo de recomendación `Most viewed `.

Si la recopilación de datos de entrada no es suficiente, los siguientes tipos de recomendación vuelven a `Most viewed`:

- `Recommended for you`
- `Viewed this, viewed that`
- `Viewed this, bought that`
- `Bought this, bought that`
- `Trending`
- `Conversion (view to purchase)`
- `Conversion (view to cart)`

#### Advertencias

- Los bloqueadores de anuncios y la configuración de privacidad pueden impedir que se recopilen eventos y provocar que las [métricas](workspace.md#column-descriptions) de participación e ingresos no se comuniquen correctamente. Además, algunos eventos no se envían debido a que los compradores abandonan la página o a problemas de red.
- [Implementaciones sin encabezado](headless.md) deben implementar eventos para activar el panel Recomendaciones de productos.
- Para los productos configurables, las recomendaciones de productos utilizan la imagen del producto principal. Si el producto principal no tiene imagen, ese producto no aparece en la unidad de recomendación.

>[!NOTE]
>
>Si el [Modo de restricción de cookies](https://experienceleague.adobe.com/es/docs/commerce-admin/start/compliance/privacy/compliance-cookie-law) está habilitado, Adobe Commerce no recopilará datos de comportamiento hasta que el comprador acepte el uso de cookies. Si el modo de restricción de cookies está deshabilitado, Adobe Commerce recopila datos de comportamiento de forma predeterminada.
