---
title: Rendimiento de búsqueda
description: La página Rendimiento de la búsqueda proporciona a insight los términos de búsqueda que utilizan los compradores.
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
exl-id: 75b43c6f-d876-4379-ad70-5c2a2f29a5ac
source-git-commit: c408f3de4e3b980545a655e2f6040187f00bc571
workflow-type: tm+mt
source-wordcount: '1825'
ht-degree: 0%

---

# Rendimiento de búsqueda

La página *Rendimiento de la búsqueda* proporciona a insight los términos de búsqueda que usan los compradores. La información se puede utilizar para identificar tendencias, aumentar los clics y mejorar la tasa de conversión. La página Rendimiento de la búsqueda proporciona una instantánea de las métricas de búsqueda para un intervalo de fechas específico e incluye los siguientes informes:

- Búsquedas únicas
- Posición de clic promedio
- Tasa de pulsaciones
- Tasa de conversión
- Tasa de resultados cero

![Rendimiento de búsqueda](../assets/search-performance.png){zoomable="yes"}

>[!IMPORTANT]
>
>Si no ve ninguna métrica de rendimiento de búsqueda, asegúrese de que los datos de evento de búsqueda se estén [recopilando](../setup/events/overview.md).

## Elija la **vista de catálogo**

Seleccione la [vista de catálogo](../setup/catalog-view.md) para ver los resultados específicos de rendimiento de la búsqueda.

![Vista de catálogo](../assets/catalog-view.png)

## Ver un informe

Haga clic en el calendario y realice una de las siguientes acciones:

- Para especificar una sola fecha, haga doble clic en la fecha del calendario.
- Para especificar un intervalo de fechas, haga clic en la primera y en la última fecha del calendario.

>[!NOTE]
>
>El intervalo de fechas no puede superar un año.

Haga clic en **[!UICONTROL Export to CSV]** para generar un archivo CSV con el rendimiento de la búsqueda.

## Cómo mejorar el rendimiento de la búsqueda

En la siguiente sección se proporcionan estrategias que puede utilizar para mejorar la funcionalidad de búsqueda del sitio, lo que garantiza una experiencia de comprador perfecta y eficaz que maximiza las tasas de conversión.

Existen varios factores clave que determinan la relevancia y eficacia de los resultados de búsqueda:

- Los datos de productos bien estructurados garantizan que los algoritmos de búsqueda puedan hacer coincidir de forma eficaz los productos con las consultas. Los datos de productos de baja calidad conducen a resultados de búsqueda menos relevantes. Para afectar directamente al éxito de su estrategia de comercialización:
   - Configure los [atributos correctos según la búsqueda](https://developer.adobe.com/commerce/services/reference/rest/#operation/createProductMetadata) con su peso correspondiente.
   - Asegúrese de que los datos de esos atributos sean relevantes.
- Una experiencia de búsqueda bien diseñada crea confianza con los clientes e infunde confianza en que encontrarán lo que necesitan.
- Las reglas de búsqueda son esenciales, ya que pueden aumentar la visibilidad de ciertos productos en función de la popularidad, las nuevas llegadas, los criterios promocionales o cualquier otra estrategia de comercialización para satisfacer los requisitos comerciales.
- La navegación con facetas permite a los compradores refinar su búsqueda y obtener resultados relevantes rápidamente.

### Monitorización de resultados de búsqueda

Para optimizar los resultados de búsqueda con [!DNL Adobe Commerce Optimizer], supervise los indicadores clave de rendimiento (KPI) relevantes, como las consultas únicas, la posición de clics promedio, las tasas de pulsaciones, la tasa de conversión y la tasa de resultados cero, a fin de comprender cómo los compradores interactúan con la funcionalidad de búsqueda. Estos datos le guían para actualizar y perfeccionar regularmente las reglas de búsqueda.

- **Búsquedas únicas**: El recuento de consultas de búsqueda distintas realizadas en el sitio [!DNL Adobe Commerce Optimizer]. Cada búsqueda única se cuenta solo una vez, incluso si la repite varias veces el mismo comprador o distintos compradores. Esta métrica le ayuda a comprender la diversidad de términos de búsqueda utilizados por los clientes y proporciona información sobre los productos o la información que buscan los compradores. El seguimiento de búsquedas únicas le permite:

   - Identificar las tendencias de búsqueda populares y los elementos buscados con frecuencia.
   - Detecte posibles lagunas en el catálogo de productos o en el contenido.
   - Optimice la funcionalidad de búsqueda agregando [sinónimos](../merchandising/synonyms/overview.md), creando o actualizando [reglas de búsqueda](../merchandising/rules/overview.md).

- **Posición de clic promedio**: indica que la posición promedio de los resultados de búsqueda en los que hicieron clic los compradores después de realizar una consulta de búsqueda en el sitio. Esta métrica proporciona perspectivas sobre la relevancia y la eficacia de los resultados de búsqueda.

  Una posición de clic promedio más baja (más cercana a 1) sugiere que los compradores encuentran resultados relevantes rápidamente, lo que indica que la estrategia de búsqueda es eficaz. Ayuda a comprender el comportamiento del comprador y hasta dónde está dispuesto a desplazarse para encontrar el producto deseado. Si la posición del clic promedio es alta, puede indicar que los resultados más relevantes no aparecen en la parte superior, lo que requiere una revisión y optimización de su estrategia de búsqueda.

- **Tasa de clics (CTR)**: mide el porcentaje de compradores que hacen clic en un resultado de búsqueda después de realizar una consulta de búsqueda. Un CTR alto indica que los resultados de búsqueda son relevantes y atractivos para los compradores, ya que están haciendo clic en los resultados que encuentran. La monitorización del CTR puede ayudar a identificar áreas de mejora. Un CTR bajo puede sugerir que los resultados de búsqueda no coinciden con la intención del comprador, lo que provoca la necesidad de refinar las reglas de búsqueda, mejorar los datos del producto o mejorar la presentación de los resultados.

- **Tasa de conversión**: indica la eficacia de la característica de búsqueda para impulsar las ventas y lograr los objetivos empresariales. Refleja la eficacia general de la funcionalidad de búsqueda para satisfacer las necesidades del comprador y facilitar una experiencia de compra sin problemas. Una tasa de conversión alta indica que los resultados de búsqueda son muy relevantes y persuasivos, lo que lleva a los compradores a completar compras. Si la tasa de conversión es baja, puede sugerir problemas con la relevancia de la búsqueda, la disponibilidad del producto o el recorrido general del comprador desde la búsqueda hasta la compra.

- **Tasa de resultados cero**: mide el porcentaje de consultas de búsqueda en el sitio [!DNL Adobe Commerce Optimizer] que no devuelven resultados. Esta métrica es crucial para comprender con qué frecuencia las búsquedas de los compradores no tienen éxito y puede proporcionar perspectivas sobre posibles lagunas en el catálogo de productos o la configuración de búsqueda. Una tasa de resultados cero alta puede frustrar a los compradores, lo que conduce a una mala experiencia de compra y a una posible pérdida de clientes. Puede indicar productos o categorías que faltan en el catálogo que los compradores están buscando, lo que guía las decisiones de inventario y lista de productos.

  Para reducir la tasa de resultados cero, puede:

   - Ofrezca términos de búsqueda alternativos o relacionados, como [sinónimos](../merchandising/synonyms/overview.md), cuando no se encuentren coincidencias exactas.
   - Revise con regularidad las consultas de resultados cero para identificar patrones y realizar los ajustes necesarios en el catálogo de productos y la configuración de búsqueda.

Puede utilizar estos datos de métricas para optimizar la funcionalidad de búsqueda de las siguientes maneras:

- Implemente reglas para clasificar automáticamente los productos más populares en los resultados de búsqueda. Los productos en los que se hace clic con frecuencia o que se compran pueden tener prioridad para aparecer en la parte superior. Seleccione manualmente listas de productos populares para consultas de búsqueda específicas y asegúrese de que estos artículos se muestran de forma destacada.
- Resaltar productos que actualmente son tendencias o que recientemente han visto un pico en popularidad. Esto puede ser especialmente eficaz durante eventos de temporada, festivos o períodos promocionales. Para conseguirlo, utilice la clasificación inteligente que mejor se adapte a su caso de uso y a sus necesidades comerciales al configurar una regla de búsqueda.
- Resalte los filtros o facetas populares, si los compradores filtran con frecuencia por determinadas marcas o intervalos de precios, resalte esas opciones fijando esas facetas y ordenándolas en consecuencia.
- Cuando una búsqueda no genere resultados, use datos de resultados populares para sugerir productos alternativos o categorías relacionadas que tengan una alta participación del comprador.
- Analice los términos de búsqueda populares y los datos del producto para identificar palabras clave importantes. Optimice los atributos en los que se puede buscar productos con estas palabras clave para mejorar la relevancia de la búsqueda.
- Analice con regularidad los datos de resultados para comprender los cambios en las tendencias, las preferencias y el comportamiento de los compradores, identificar los términos de búsqueda principales y detectar problemas. Utilice este bucle de comentarios para refinar y mejorar continuamente sus reglas de búsqueda y ofertas de productos

## Optimización de la funcionalidad de búsqueda

Para optimizar la funcionalidad de búsqueda, usa [sinónimos y ortografía](../merchandising/synonyms/overview.md) para asegurarte de que los compradores encuentren productos aunque usen palabras y [facetas diferentes](../merchandising/facets/overview.md) para permitir que los compradores reduzcan los resultados de búsqueda.

## Mejorar la relevancia de los resultados de búsqueda

Para mejorar la relevancia de los resultados de búsqueda, implemente [reglas de búsqueda](../merchandising/rules/overview.md) efectivas y use metadatos de productos para garantizar que se puedan realizar búsquedas de [atributos precisos y detallados](https://developer.adobe.com/commerce/services/reference/rest/#operation/createProductMetadata).

### Imágenes

Asegúrese de que los productos secundarios de los productos configurables tengan imágenes con las funciones correctas. Si tiene productos principales o secundarios, el resultado de la búsqueda podría no tener imágenes.

>[!NOTE]
>
>Las imágenes de los resultados de búsqueda pueden variar según el término de búsqueda. Si el término de búsqueda determina que un producto secundario es más relevante, se utilizarán imágenes del producto secundario en lugar de imágenes del producto principal.

### Aprovechamiento de metadatos del producto

Asegúrese de que los atributos precisos y detallados del producto [están configurados para permitir búsquedas y de que tienen un peso asignado](https://developer.adobe.com/commerce/services/reference/rest/#operation/createProductMetadata). Tenga en cuenta que los atributos SKU, nombre y categoría se pueden buscar de forma predeterminada y no se pueden excluir de la búsqueda. Para obtener los mejores resultados, no utilice espacios en los SKU.

Para aumentar la relevancia de la búsqueda, asigne una ponderación a cada atributo en el que se pueda buscar. Los atributos con un peso mayor deben aparecer más arriba en los resultados de búsqueda. La ordenación por relevancia se ve afectada por varios criterios, como el peso de la búsqueda. Esto significa que, a veces, los atributos con una ponderación de búsqueda menor pueden seguir teniendo más relevancia que los atributos con una ponderación de búsqueda mayor. Otros criterios pueden incluir el número de coincidencias en cualquier atributo determinado, la posición del término de búsqueda encontrado y la estructura de texto general antes y después de un término de búsqueda.

Asegúrese de que cada producto tenga contenido relevante dentro de cada atributo en el que se puede buscar. No se recomienda establecer un atributo como en el que se pueda buscar si tiene grandes cantidades de contenido, ya que esto puede reducir la relevancia de los resultados de búsqueda.

## Descripciones de campos

| Datos de instantánea | Descripción |
|--- |--- |
| Búsquedas únicas | Número total de búsquedas únicas para el intervalo de fechas especificado. Varias búsquedas realizadas por el mismo comprador, incluso si se refieren a la misma consulta, se consideran únicas si se envían con más de una hora de diferencia. |
| Tasa de pulsaciones | El porcentaje de búsquedas que finalizan cuando el comprador hace clic en un producto. Por ejemplo, la tasa de clics es del 50 % si el comprador busca &quot;pantalones&quot; y &quot;camisa&quot; y luego hace clic en un resultado de la búsqueda &quot;camisa&quot;. |
| Tasa de conversión | El porcentaje de productos que compra el comprador en comparación con el número de productos en los que hace clic para el intervalo de fechas especificado. Por ejemplo, la tasa de conversión de la interacción es del 100 % si el comprador ve seis productos en la ventana emergente, hace clic en uno y realiza una compra. <br /><br />La tasa de conversión no se ve afectada por el número de vistas de un producto determinado. Por ejemplo, la tasa de conversión sigue siendo la misma si el comprador utiliza la búsqueda, pero no hace clic en ningún producto. |
| Tasa de resultados cero | Porcentaje de búsquedas únicas que no devuelven resultados para el intervalo de fechas especificado. Por ejemplo, la tasa de resultados cero es del 66,67 % si el comprador busca &quot;fjjajfjfjf&quot; dos veces (sin resultados) y &quot;pantalones&quot; una vez (con resultados). |
| El Promedio de posición del clic | La posición relativa de la tasa promedio de pulsaciones basada en búsquedas únicas para el intervalo de fechas especificado. |

| Informes | Descripción |
|--- |--- |
| Cero resultados | Enumera las consultas de búsqueda que no devuelven resultados y la cantidad de veces utilizadas durante el intervalo de fechas especificado. Límite de informes: 500 términos principales |
| Resultados frecuentes | Enumera los nombres de los productos que recibieron la mayor cantidad de vistas durante el intervalo de fechas especificado. Los resultados populares se calculan únicamente en función de las impresiones y no se ven afectados por el número de clics o ingresos generados. Límite de informes: 500 términos principales |
| Búsquedas únicas | Enumera las consultas de búsqueda únicas utilizadas durante el intervalo de fechas especificado. Los datos del informe se calculan del mismo modo que los datos de instantáneas de búsqueda única. Si un comprador escribe la misma consulta de búsqueda dos veces, pero con una diferencia de más de una hora, la búsqueda se considera dos búsquedas únicas. Límite de informes: 500 términos principales |

## Propiedades de atributo predeterminadas que no son del sistema

En la tabla siguiente se muestran las propiedades de búsqueda y filtrado predeterminadas de los atributos que no son del sistema. Si establece la propiedad del atributo *Use in Search* en `Yes`, se podrá buscar en el atributo en [!DNL Adobe Commerce Optimizer].

| Código de atributo | Buscable |
|--- |--- |
| actividad | Sí |
| attributes_brand | Sí |
| marca | Sí |
| clima | Sí |
| collar | Sí |
| color | Sí |
| coste | Sí |
| eco_collection |  |
| género | Sí |
| fabricante | Sí |
| material | Sí |
| propósito | Sí |
| strap_bags | Sí |
| style_general | Sí |

## Propiedades predeterminadas de atributos del sistema

En la tabla siguiente se muestran la búsqueda predeterminada y las propiedades filtrables de los atributos del sistema.

| Código de atributo | Buscable |
|--- |--- |
| allow_open_amount | Sí |
| description | Sí |
| name | Sí |
| precio | Sí |
| short_description | Sí |
| sku | Sí |
| status | Sí |
| tax_class_id | Sí |
| url_key | Sí |
| peso | Sí |
