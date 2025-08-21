---
title: Tipos de recomendación
description: Obtenga información acerca de las recomendaciones que puede implementar en varias páginas del sitio.
exl-id: bbb290b0-b50b-43d9-bf71-1813298d5f39
source-git-commit: 1548b7e11249febc2cd8682581616619f80c052f
workflow-type: tm+mt
source-wordcount: '1719'
ht-degree: 0%

---

# Tipos de recomendación

Adobe Commerce proporciona un gran conjunto de recomendaciones que puede implementar en varias páginas del sitio. Todos los tipos de recomendación están basados en datos. Se basan en datos de comportamiento, datos de atributos de productos y métricas. Para facilitar la referencia, los tipos de recomendación se agrupan de la siguiente manera:

- [Personalizado](#personalized)
- [Venta cruzada y mejora de ventas](#crossup)
- [Popularidad](#popularity)
- [De alto rendimiento](#highperf)

Como práctica recomendada, Adobe recomienda las siguientes directrices al utilizar Recommendations:

- Diversifique los tipos de recomendaciones. Los clientes empiezan a ignorar las recomendaciones si sugieren los mismos productos una y otra vez.

- No implemente las mismas recomendaciones en la página del carro de compras y en la página de confirmación de pedidos. Considere utilizar `Most Added to Cart` para la página del carro de compras y `Bought This, Bought That` para la página de confirmación de pedido.

- Mantenga su sitio ordenado. No implemente más de tres unidades de recomendación en la misma página.

- Si su tienda vende ropa, la recomendación `More like this` puede sugerir productos específicos del sexo que no coincidan con el sexo del producto que se está viendo. Considere utilizar este tipo de recomendación solo para categorías que no sean de ropa.

>[!NOTE]
>
>Para obtener más información sobre los eventos descritos en este artículo, consulte [eventos de tienda](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#product-recommendations) en la documentación para desarrolladores.

## Personalizado {#personalized}

Estos tipos de recomendación recomiendan productos basados en el historial de comportamiento del comprador específico en el sitio. Por ejemplo, si un comprador ya ha buscado una chaqueta o ha comprado una en su sitio web, estas recomendaciones esencialmente recogen lo que dejaron y recomiendan otras chaquetas o productos similares.

| Tipo | Descripción |
|---|---|
| Recomendado para usted | Recomienda productos en función del comportamiento actual y anterior de cada comprador en el sitio. Muestra recomendaciones muy relevantes basadas en el historial de navegación y compra del comprador. Este tipo de recomendación es efectivo en la página de inicio donde la mayoría de los compradores comienzan su recorrido en un sitio. Para los compradores nuevos del sitio que no hayan generado ninguna señal para personalizar su experiencia, Adobe Commerce muestra los productos en función del tipo de recomendación Más visitado. Sin embargo, cuando el comprador comienza a interactuar con los productos en el sitio, los productos recomendados se ajustan en tiempo real a su comportamiento.<br/><br/>**Uso:**<br/>- Página de inicio<br/>- Categoría <br/><br/>**Etiquetas sugeridas:**<br/> - Solo para ti<br/>- Recomendado para ti<br/>- Inspirado en tus tendencias de compras |
| Vistos recientemente | Muestra los productos que el comprador ha visto más recientemente en función del historial del explorador. La unidad de recomendación elimina todos los productos eliminados. La unidad de recomendación no se muestra si no hay historial de explorador o no hay suficiente historial cuando se aplican reglas de filtro. Si los resultados contienen menos productos que los configurados, la unidad de recomendación solo muestra los productos devueltos.<br/><br/>**Uso:**<br/>- Página de inicio<br/>- Categoría<br/>- Detalles del producto<br/>- Carro de compras<br/>- Confirmación <br/><br/>**Etiquetas sugeridas:**<br/>- Vistos recientemente<br/>- Eche otro vistazo |

## Venta cruzada y mejora de ventas {#crossup}

Estos tipos de recomendación están orientados a la prueba social para ayudar a los compradores a encontrar lo que les gustó a otros o están impulsados por productos para ayudarles a encontrar otros productos similares. Los productos recomendados suelen complementar el producto seleccionado.

>[!NOTE]
>
>Los tipos de recomendación &quot;visto esto, visto aquello&quot;, &quot;visto esto, comprado aquello&quot; y &quot;comprado esto, comprado aquello&quot; no usan una métrica de ocurrencia simple, sino un algoritmo de filtrado colaborativo más sofisticado que busca *similitudes interesantes* que no se desvíen hacia productos populares. Los datos utilizados para informar a estos tipos de recomendaciones se basan en el comportamiento agregado del comprador derivado de varias sesiones del sitio. Los datos no se basan en el comportamiento del comprador derivado de una sola incidencia en la sesión en el sitio. Estos tipos de recomendación ayudan a los compradores a encontrar aquellos productos adyacentes que podrían no ser obvios de emparejar con el producto que se está viendo en ese momento.

| Tipo | Descripción |
|---|---|
| Vio esto, vio aquello. | Recomienda productos que los compradores ven con mayor frecuencia y de forma desproporcionada con el producto visualizado actualmente.<br/><br/>**Dónde se usó:**<br/>- Detalles del producto<br/>- Carro<br/>- Confirmación <br/><br/>**Etiquetas sugeridas:**<br/>- Los clientes que vieron este producto también vieron (PDP) |
| Vio esto, compró aquello. | Recomienda productos que los compradores tienden a comprar con desproporción con mayor frecuencia después de ver el producto actual. Este tipo ayuda a guiar a los compradores para que descubran productos que es posible que no hayan notado de otra manera.<br/><br/>**Dónde se usó:**<br/>- Detalles del producto<br/>- Carro<br/>- Confirmación <br/><br/>**Etiquetas sugeridas:**<br/>- Clientes que vieron este producto final comprado<br/>- Clientes que finalmente compraron<br/>- ¿Qué compran otros después de ver este producto? |
| Compré esto, compré aquello. | Recomienda productos que los compradores compran con una frecuencia desproporcionada mayor con el producto visualizado actualmente. Este tipo muestra productos muy relevantes que los compradores pueden añadir a su carro de compras sumando lo que otros compradores han comprado con el producto actual.<br/><br/>**Dónde se usó:**<br/>- Detalles del producto<br/>- Carro<br/>- Confirmación <br/><br/>**Etiquetas sugeridas:**<br/>- Obtenga todo lo que necesita<br/>- No olvide estas<br/>- Compradas frecuentemente juntas |
| Más parecido a esto | Recomienda productos basados en metadatos similares como nombre, descripción, asignación de categorías y atributos. Al evaluar los atributos de los productos que se ven, este tipo recomienda productos similares en la misma categoría. Por ejemplo, si un comprador está explorando alfombras de yoga, se recomiendan otros productos en la categoría de equipamiento. Dado que este tipo de recomendación no distingue entre géneros, no se recomienda para prendas de vestir, moda u otros verticales específicos de género.<br/><br/>**Dónde se usó:**<br/>- Detalles del producto<br/>- Carro<br/>- Confirmación <br/><br/>**Etiquetas sugeridas:**<br/>- Más productos como este<br/>- Similar a este |
| [Similitud visual](#visualsim) | Recomienda productos de aspecto similar al producto que se está viendo. Este tipo de recomendación es más útil si las imágenes y los aspectos visuales de los productos son importantes para la experiencia de compra. |

## Popularidad {#popularity}

Estos tipos de recomendación recomiendan productos que son los más populares o los que han sido tendencia en los últimos siete días.

| Tipo | Descripción |
|---|---|
| Más visitados | Recomienda los productos que más se vieron contando la cantidad de sesiones en las que se produjo una acción de visualización en los últimos siete días.<br/><br/>**Lugar de uso:**<br/>- Página de inicio<br/>- Categoría<br/>- Detalles del producto<br/>- Carro de compras<br/>- Confirmación <br/><br/>**Etiquetas sugeridas:**<br/>- Más populares<br/>- Tendencias<br/>- Más populares ahora<br/>- Recientemente populares<br/>- Productos populares inspirados por este producto (PDP)<br/>- Principales vendedores |
| Más comprados | Recomienda los productos comprados con mayor frecuencia por los compradores en los últimos siete días.<br/><br/>**Lugar de uso:**<br/>- Página de inicio<br/>- Categoría<br/>- Detalles del producto<br/>- Carro de compras<br/>- Confirmación <br/><br/>**Etiquetas sugeridas:**<br/> - Más populares<br/>- Tendencias<br/>- Más populares ahora<br/>- Recientemente populares<br/>- Productos populares inspirados por este producto (PDP)<br/>- Principales vendedores |
| Más añadidos al carro | Recomienda los productos que los compradores añaden con mayor frecuencia a los carros de compras en los últimos siete días. Este tipo de recomendación se puede utilizar en todas las páginas.<br/><br/>**Lugar de uso:**<br/>- Página de inicio<br/>- Categoría<br/>- Detalles del producto<br/>- Carro de compras<br/>- Confirmación <br/><br/>**Etiquetas sugeridas:**<br/> - Más populares<br/>- Tendencias<br/>- Más populares ahora<br/>- Recientemente populares<br/>- Productos populares inspirados por este producto (PDP)<br/>- Principales vendedores |
| Tendencia | Recomienda productos en función del impulso reciente de la popularidad de un producto en todo el sitio.<br/><br/>Adobe Sensei agrega datos de compra y navegación en el sitio para determinar y clasificar qué productos son los más populares entre los compradores. Dado que Trending analiza el impulso reciente del producto, es un tipo de recomendación eficaz para los catálogos que tienen una alta rotación. Si el catálogo es más estático, puede que no sea tan útil a menos que los patrones de compra de la audiencia sean muy variables.<br/><br/>Cuando se usa en la página de inicio, Tendencia recomienda productos que recientemente se han hecho populares en todo el sitio. Las tendencias no muestran productos que son populares de manera consistente, sino más bien aquellos que se han vuelto populares recientemente. Por ejemplo, si tiene una campaña de marketing por correo electrónico que promociona determinados productos, el aumento de popularidad generado por el correo electrónico aumenta la probabilidad de que los productos promocionados se clasifiquen como tendencias.<br/><br/>**Dónde se usó:**<br/>- Página de inicio<br/>- Categoría<br/>- Detalles del producto<br/>- Carro de compras<br/>- Confirmación <br/><br/>**Etiquetas sugeridas:**<br/>- Tendencia<br/>- Tendencia ahora<br/>- Tendencia reciente<br/>- Productos destacados<br/>- Productos relacionados con la tendencia (PDP) |

## Alto rendimiento {#highperf}

Estos tipos de recomendación recomiendan productos de mayor rendimiento según criterios de éxito como las tasas de conversión o de complementos al carro de compras.

| Tipo | Descripción |
|---|---|
| Ver para adquirir la conversión | Recomienda productos con la tasa de conversión de vista a compra más alta. De todas las sesiones de compradores que registraron una vista de producto, ¿cuál es la proporción que finalmente registró una compra por parte del comprador?<br/><br/>**Lugar de uso:**<br/>- Página de inicio<br/>- Categoría<br/>- Detalles del producto<br/>- Carro de compras<br/>- Confirmación <br/><br/>**Etiquetas sugeridas:**<br/> -Principales vendedores<br/>- Productos populares<br/>- Es posible que esté interesado en |
| Ver conversión al carro de compras | Recomienda productos con la mayor tasa de conversión de vista a carro. De todas las sesiones de compradores que registraron una vista de producto, ¿cuál es la proporción que finalmente registró un anuncio al carro de compras del comprador?<br/><br/>**Lugar de uso:**<br/>- Página de inicio<br/>- Categoría<br/>- Detalles del producto<br/>- Carro de compras<br/>- Confirmación <br/><br/>**Etiquetas sugeridas:**<br/> - Principales vendedores<br/>- Productos populares<br/>- Es posible que esté interesado en |
| Más comprados | A menudo denominado &quot;Principales vendedores&quot;, este tipo de recomendación cuenta el número de sesiones en las que se produjo una acción de pedido en los últimos siete días. Este tipo de recomendación se puede utilizar en todas las páginas.<br/><br/>**Lugar de uso:**<br/>- Página de inicio<br/>- Categoría<br/>- Detalles del producto<br/>- Carro de compras<br/>- Confirmación <br/><br/>**Etiquetas sugeridas:**<br/> - Más populares<br/>- Tendencias<br/>- Más populares ahora<br/>- Recientemente populares<br/>- Productos populares inspirados por este producto (PDP)<br/>- Principales vendedores |
| Más añadidos al carro | Recomienda los productos que los compradores añaden con mayor frecuencia a los carros de compras en los últimos siete días. Este tipo de recomendación se puede utilizar en todas las páginas.<br/><br/>**Lugar de uso:**<br/>- Página de inicio<br/>- Categoría<br/>- Detalles del producto<br/>- Carro de compras<br/>- Confirmación <br/><br/>**Etiquetas sugeridas:**<br/> - Más populares<br/>- Tendencias<br/>- Más populares ahora<br/>- Recientemente populares<br/>- Productos populares inspirados por este producto (PDP)<br/>- Principales vendedores |

## Similitud visual {#visualsim}

El tipo de recomendación _Similitud visual_ recomienda productos de aspecto similar al producto que se está viendo. Este tipo de recomendación es más útil cuando las imágenes y los aspectos visuales de los productos son partes importantes de la experiencia de compra.

### Cómo funciona

El tipo de recomendación _Similitud visual_ ofrece recomendaciones para otros productos del catálogo que tengan una similitud visual con las imágenes que se están viendo en ese momento. La similitud visual incluye aspectos como:

- Color
- Forma
- Tamaño
- Textura
- Material
- Estilo

Adobe Sensei utiliza IA para procesar y analizar las imágenes del catálogo y crear atributos utilizados para determinar similitudes visuales.

>[!NOTE]
>
> Si está probando este tipo de recomendación en un entorno que no es de producción, asegúrese de que las URL de la imagen sean accesibles públicamente.

>[!NOTE]
>
> Actualmente, las imágenes de producto deben tener un tamaño de 10 MB o menos.

Debido a que este tipo de recomendación no es aplicable a la mayoría de los catálogos, no está habilitado de forma predeterminada. Debe habilitar explícitamente este tipo de recomendación.

### Habilitar tipo de recomendación de similitud visual

>[!NOTE]
>
> El tipo de recomendación _Similitud visual_ está disponible cuando lo [instala](install-configure.md) como módulo opcional.

1. En la barra lateral de _Admin_, ve a **Marketing** > _Promociones_ > **Recomendaciones de productos** para mostrar el panel de _Recomendaciones de productos_.

1. Haga clic en **Configuración** (icono de engranaje) para mostrar la página _Configuración_.

1. En la sección _Recomendaciones visuales_, seleccione para **Habilitar recomendaciones visuales**.

1. Haga clic en **Guardar cambios** cuando haya terminado.

   La página [Crear nueva recomendación](create.md) ahora muestra **Similitud visual** como un tipo de recomendación seleccionable cuando el tipo de página es **Detalle del producto**.

Después de habilitar las recomendaciones visuales, Adobe Sensei inicia el procesamiento de imágenes. El tiempo que tarda depende del tamaño del catálogo.

### Dónde se utiliza

- Detalles del producto

### Etiquetas de tienda sugeridas

- También le puede gustar
- Encontramos otros productos que te pueden gustar
- Inspirado en este estilo

### Ejemplo

La siguiente imagen muestra la página de detalles del producto _Clamber Watch_:

![Reloj Clamber](assets/visual-sim-pdp.png)

A continuación se muestra la unidad de recomendación _Similitud visual_ para _Clamber Watch_:

![Unidad de similitud visual](assets/visual-sim-unit.png)
