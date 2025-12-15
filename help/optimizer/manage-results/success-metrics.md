---
title: Métricas de éxito
description: Las métricas de éxito proporcionan a insight las métricas de rendimiento clave para tu tienda  [!DNL Adobe Commerce Optimizer] Store.
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
exl-id: 7202a531-fec3-4698-89b9-6bdbcc37015e
source-git-commit: 4e85d70dc1b099a5b40a807a76ca589aa9a28f07
workflow-type: tm+mt
source-wordcount: '2599'
ht-degree: 0%

---

# Métricas de éxito

Esta página proporciona información general sobre las métricas clave de rendimiento para su tienda [!DNL Adobe Commerce Optimizer]. El objetivo es que usted entienda rápidamente los resultados de implementar [!DNL Adobe Commerce Optimizer], luego lo ayude a usted y a su equipo a identificar oportunidades de crecimiento y a destacar áreas para la optimización.

![Informe de métricas de éxito](../assets/success-metrics.png)

Las métricas del informe se extraen de los datos de evento de la tienda. [Más información](../setup/events/overview.md) acerca de los datos de evento recopilados.

## Explicación de las métricas

El informe de métricas de éxito ofrece perspectivas procesables en cinco áreas de rendimiento clave que afectan directamente a los resultados de su negocio. Cada métrica revela patrones en el comportamiento de los clientes y el rendimiento de las tiendas que le ayudan a descubrir oportunidades y a abordar desafíos. Aproveche estas perspectivas para impulsar decisiones más inteligentes y optimizar su experiencia comercial.

**Aspectos destacados** resume las métricas clave de cada área de rendimiento. Utilice esta sección para identificar rápidamente las principales oportunidades de mejora.

Los indicadores clave de rendimiento son:

- **Ingresos**: la métrica financiera principal que muestra el rendimiento total de ventas.
- **Conversión**: el porcentaje de visitantes que completaron compras.
- **Participación**: la forma en que los usuarios interactúan activamente con el sitio.
- **Adquisición**: La eficacia de los esfuerzos de adquisición de clientes.
- **Tasa de salida hacia otro sitio**: porcentaje de visitantes que se van después de ver una sola página.

### Actualización y precisión de los datos

**Frecuencia de actualización:** Los datos de las métricas de éxito se procesan y actualizan con regularidad a medida que se recopilan y procesan los eventos de tienda.

**Cuándo comprobar las métricas:** Para obtener el análisis de tendencias más preciso, revise las métricas después de haber transcurrido el tiempo suficiente para recopilar datos significativos. Las fluctuaciones diarias son normales; céntrese en las tendencias semanales o mensuales para las decisiones estratégicas.

**Precisión de los datos:** Las métricas se calculan a partir de las interacciones reales de los clientes capturadas mediante eventos de tienda. Asegúrese de que su tienda tenga configurado el [seguimiento de eventos](../setup/events/overview.md) adecuado para generar informes precisos.

## Generación de un informe

1. En el carril izquierdo, seleccione **Métricas de éxito**.
1. En **Configuración de informes**, especifique el **intervalo de fechas**, el **origen del catálogo** en función de la configuración regional y **Moneda**.
1. Haga clic en **[!UICONTROL Apply]**.

   Las **características más destacadas**, **Ingresos**, **Conversión**, **Participación**, **Adquisición** y **Tasa de salida hacia otro sitio** se actualizan según la configuración del informe.

1. Haga clic en **[!UICONTROL Export]** para guardar el informe como un PDF.

## Uso conjunto de métricas de éxito y Sites Optimizer

Las métricas de éxito y Sites Optimizer ([Oportunidades](opportunities.md)) son herramientas complementarias diseñadas para trabajar en conjunto, que le ayudarán a mejorar el rendimiento de su sitio comercial. Comprender la diferencia entre estas funciones le ayuda a tomar mejores decisiones y lograr resultados medibles.

### Diferencias clave

| Aspecto | Métricas de éxito | Sites Optimizer (oportunidades) |
|---|---|---|
| **Propósito** | Mide el rendimiento y los resultados | Identifica problemas y proporciona recomendaciones |
| **Tipo** | Panel analítico | Detección proactiva de problemas |
| **Lo que muestra** | Indicadores clave de rendimiento (ingresos, conversión, participación, adquisición, tasa de devolución) | Recomendaciones con tecnología de IA para problemas que afectan al rendimiento del sitio |
| **Origen de datos** | Datos de evento de tienda | Catálogos de productos, registros de búsqueda y datos de recomendaciones |
| **Usar cuando** | Desea rastrear los resultados a lo largo del tiempo | Desea identificar y corregir problemas específicos |

### Cómo utilizar estas funciones de forma conjunta

El enfoque más eficaz combina ambas herramientas en un ciclo de mejora continua:

1. **Medir con métricas de éxito**: Comience por revisar el panel de métricas de éxito para comprender el rendimiento actual. Identifique qué KPI necesitan mejora (por ejemplo, tasa de conversión baja o tasa de salida hacia otro sitio alta).

1. **Diagnosticar con oportunidades**: vaya a la página Oportunidades para descubrir problemas específicos que pueden estar causando un rendimiento deficiente. Sites Optimizer analiza el catálogo de productos, los registros de búsqueda y los datos de recomendaciones para identificar problemas como la falta de datos de productos, la poca relevancia de la búsqueda o los problemas de navegación.

1. **Implementar recomendaciones**: Siga las recomendaciones impulsadas por IA que se proporcionan en Oportunidades para abordar los problemas detectados. Estos pueden incluir la corrección de problemas de calidad de datos del producto, la mejora de la SEO o la optimización de la búsqueda y el descubrimiento.

1. **Seguimiento de mejoras**: Regrese a las métricas de éxito para monitorizar cómo los cambios afectan los KPI con el paso del tiempo. Utilice el selector de intervalo de fechas para comparar el rendimiento antes y después de implementar las recomendaciones.

1. **Iterar y optimizar**: continúe este ciclo, usando Oportunidades para identificar nuevos problemas y métricas de éxito para medir el impacto de sus optimizaciones.

### Ejemplo de flujo de trabajo

Un comerciante observa que su tasa de conversión disminuye en las Métricas de éxito. A continuación se indica cómo pueden utilizar ambas funciones para solucionarlo:

1. **Identificar el problema**: el panel de métricas de éxito muestra que la tasa de conversión cayó un 15% en el último mes.

1. **Buscar la causa**: La página Oportunidades revela varios problemas:
   - A varios productos les faltan atributos de clave que afectan a la relevancia de búsqueda.
   - Las consultas de búsqueda populares devuelven resultados deficientes.
   - Tiempos de carga de las páginas lentas en las páginas de categoría.

1. **Tomar medidas**: el comerciante da prioridad a corregir primero los problemas de calidad de los datos del producto, ya que Sites Optimizer los clasifica como oportunidades de alto impacto que afectan a las búsquedas y recomendaciones.

1. **Resultados de medidas**: después de actualizar los atributos del producto e implementar los cambios recomendados, el comerciante supervisa semanalmente las métricas de éxito. Durante el mes siguiente, la tasa de conversión aumenta un 12 % y las métricas de participación de búsqueda mejoran significativamente.

1. **Continuar optimizando**: con la mejora de la tasa de conversión, el comerciante cambia el enfoque a la siguiente prioridad que se muestra en Oportunidades: optimizar la velocidad de carga de la página para reducir la tasa de salida hacia otro sitio.

### Cuándo utilizar cada función

**Usar métricas de éxito cuando desee:**

- Rastree el rendimiento empresarial general.
- Mida el impacto de los cambios con el tiempo.
- Identifique qué áreas de su negocio requieren atención.
- Comparta informes de rendimiento con partes interesadas.
- Comprenda las tendencias de comportamiento de los clientes.

**Use Sites Optimizer (Oportunidades) cuando desee:**

- Descubra los problemas específicos que afectan al rendimiento.
- Obtenga recomendaciones procesables para solucionar problemas.
- Comprenda por qué ciertas métricas están declinando.
- Priorice las optimizaciones que desea abordar primero.
- Aproveche la IA para identificar los problemas que podría pasar por alto manualmente.

Juntas, estas características proporcionan una solución completa: las métricas de éxito indican *lo que* está sucediendo, mientras que Sites Optimizer indica *por qué* y *cómo solucionarlo*.

## Pasos siguientes y estrategias de optimización

Utilice sus datos de métricas de éxito para identificar oportunidades de mejora e implementar estrategias de optimización dirigidas. Las siguientes secciones proporcionan directrices específicas y procesables para cada área de métrica.

>[!BEGINTABS]

>[!TAB Optimización de ingresos]

Para los ingresos, su objetivo es aumentar las ventas totales y el valor de pedido promedio.

![Ingresos de métricas de éxito](../assets/revenue.png)

### Explicación de la métrica de ingresos

**Lo que mide:** Ingresos totales generados por su tienda durante el período de tiempo seleccionado.

**Cómo se calcula:** Los ingresos son la suma de todos los pedidos completados (precio base × cantidad) para todos los productos vendidos durante el período de informe. El cálculo usa datos de `place-order` eventos capturados en la tienda.

>[!IMPORTANT]
>
>Los cálculos de ingresos excluyen pedidos cancelados, devoluciones y pedidos en los que no se capturó el evento `place-order`. Es posible que falten eventos debido a la configuración de consentimiento, problemas con el explorador (bloqueadores de anuncios, errores de secuencias de comandos) o errores de procesamiento técnico.

**Fórmula:**

```
Total Revenue = Sum of (Product Base Price × Quantity) for all completed orders
```

**Fuente de datos:** eventos de tienda (específicamente `place-order` eventos)

**Qué se incluye:**

- Todos los pedidos completados durante el intervalo de fechas seleccionado.
- Precios base del producto multiplicados por las cantidades compradas.
- Ingresos de todos los canales de ventas rastreados por Commerce Optimizer.

**Notas importantes:**

- Los ingresos se calculan en función de los precios base capturados en los eventos de tienda.
- El periodo de la creación de informes viene determinado por el intervalo de fechas que seleccione en la configuración del informe.
- Las métricas de ingresos se actualizan a medida que se procesan nuevos eventos de pedidos.

### Estrategias

- **Implementar recomendaciones con tecnología de IA**: Utilice el motor de recomendaciones del optimizador para que aparezcan productos relevantes que generen tasas de conversión más altas. Implementar *Los clientes que vieron esto también vieron* y *Compraron esto, compraron esos* tipos de recomendaciones para aumentar las oportunidades de ventas cruzadas.

- **Crear reglas de comercialización**: Impulse los productos con márgenes elevados en los resultados de búsqueda mediante [reglas de comercialización](../merchandising/rules/overview.md). Anclar los artículos más vendidos a la parte superior de los resultados de búsqueda para consultas de alto tráfico.

- **Optimizar la detección de productos**: use [facetas inteligentes](../merchandising/facets/overview.md) para ayudar a los clientes a encontrar productos de forma más eficiente, lo que aumentará las tasas de conversión y los ingresos.

- **Aproveche las oportunidades de temporada**: Cree reglas de comercialización basadas en el tiempo para promocionar artículos de temporada o promocionales durante los períodos de mayor volumen de compras.

>[!TAB Mejora de la tasa de conversión]

Para mejorar la tasa de conversión, el objetivo es convertir a más visitantes en clientes.

![Tasa de conversión de métricas de éxito](../assets/conversion-rate.png)

### Explicación de la métrica de tasa de conversión

**Lo que mide:** Porcentaje de visitantes que ven productos y luego completan una compra, lo que indica la eficacia con la que su tienda convierte los exploradores en compradores.

**Cómo se calcula:** La tasa de conversión compara el número de visitantes únicos que compraron productos con el número de visitantes únicos que vieron productos.

**Fórmula:**

```
Conversion Rate = (Total Number of Orders ÷ Total Unique Visitors) × 100
```

**Fuente de datos:** eventos de tienda.

**Cómo funciona:**

- Se hace un seguimiento de **vistas de productos** cuando los visitantes ven páginas de productos (usando `product-view` eventos).
- Se hace un seguimiento de **compras** cuando se completan pedidos (con `place-order` eventos).
- El cálculo hace coincidir los usuarios que vieron productos específicos con los que los compraron.

**Notas importantes:**

- Un visitante que ve varios productos pero realiza una compra cuenta como una conversión.
- La métrica rastrea visitantes únicos mediante identificadores basados en el explorador.
- Los eventos de vista de producto siempre incluyen un clic, por lo que las vistas representan un interés genuino del usuario.

### Estrategias

- **Optimizar la relevancia de la búsqueda**: Implemente [sinónimos](../merchandising/synonyms/overview.md) para asegurarse de que los clientes encuentren lo que están buscando, incluso con términos de búsqueda diferentes. Utilice faceteado dinámico para proporcionar opciones de filtrado relevantes.

- **Ubicación de recomendación estratégica**: implemente unidades de recomendación en páginas de alto tráfico, como páginas de detalles de productos y páginas de categorías. Use las recomendaciones *Más visitados* y *Más comprados* para generar confianza y urgencia.

- **Mejore la visibilidad del producto**: utilice reglas de comercialización para asegurarse de que los productos más vendidos y de alta conversión aparezcan de forma destacada en los resultados de búsqueda.

- **Tipos de recomendaciones de pruebas A/B**: experimente con diferentes tipos y ubicaciones de recomendaciones para encontrar lo que mejor funcione para su audiencia.

>[!TAB Mejora de la participación]

Para mejorar la participación, el objetivo es aumentar la interacción con el cliente y el tiempo en el sitio.

![Participación en métricas de éxito](../assets/engagement.png)

### Explicación de la métrica de compromiso

**Lo que mide:** La forma en que los usuarios interactúan activamente con su tienda, y el seguimiento de las acciones significativas desde la exploración inicial hasta el proceso de cierre de compra.

**Cómo se calcula:** La participación hace un seguimiento de todas las interacciones que indican una participación activa en la tienda, incluida la exploración de productos, las actividades del carro de compras y las acciones de cierre de compra.

**Fuente de datos:** eventos de tienda

**Lo que cuenta como compromiso:**

La participación incluye las siguientes categorías y acciones de eventos:

- **Interacciones de productos:** vistas de productos, clics en productos y comparaciones de productos.
- **Actividades del carro de compras:** Agregar elementos al carro, actualizar cantidades y quitar elementos.
- **Acciones de cierre de compra:** Iniciando cierre de compra, completando pasos de cierre de compra.
- **Exploración de categorías:** Visualización de páginas de categorías, filtrado por facetas.
- **Actividades de lista de deseos:** Agregar a lista de deseos y ver elementos de la lista de deseos.

**Detalles de seguimiento de eventos:**

El sistema realiza un seguimiento de la participación cuando los eventos tienen:

- Categoría: `product`, `shopper`, `shopping-cart` o `checkout`.
- Propiedad: `Product`, `Checkout`, `Cart`, `Category` o `Wishlist`.

**Notas importantes:**

- Una participación más alta suele correlacionarse con tasas de conversión más altas.
- Las métricas de participación ayudan a identificar dónde los usuarios son más activos en su recorrido.
- Utilice los datos de participación para optimizar las páginas de alto tráfico y mejorar la experiencia del usuario.

### Estrategias

- **Diversificar tipos de recomendación**: evite mostrar las mismas recomendaciones repetidamente. Usa una combinación de *Recomendado para ti*, *Tendencia* y *Vistos recientemente* para mantener el contenido fresco y atractivo.

- **Implementar búsqueda inteligente**: Use faceteo dinámico impulsado por IA y cambio de clasificación de resultados para adaptar los resultados de búsqueda en tiempo real en función del comportamiento del comprador.

- **Crear experiencias personalizadas**: implementa las unidades &quot;Recomendado para ti&quot; en la página de inicio y en todo el recorrido del cliente para ofrecer sugerencias de productos personalizadas.

- **Optimizar la experiencia de búsqueda**: Use sinónimos para mejorar la relevancia de la búsqueda y garantizar que los clientes encuentren lo que buscan rápidamente.

>[!TAB Aumento de adquisición]

Para adquirir más crecimiento, su objetivo es atraer a más clientes nuevos y mejorar la eficiencia de adquisición.

![Adquisición de métricas de éxito](../assets/acquisition.png)

### Explicación de la métrica de adquisición

**Lo que mide:** El número de visitantes nuevos y únicos que llegan a su tienda, lo que le ayuda a comprender la eficacia de sus esfuerzos de marketing y adquisición de clientes.

**Cómo se calcula:** La adquisición cuenta visitantes únicos según los identificadores de explorador asignados durante su primera visita a su tienda.

**Fuente de datos:** eventos de tienda.

**Cómo funciona:**

- El explorador de cada visitante recibe un identificador único (`domain_userid`) mediante una cookie propia.
- Los nuevos visitantes se identifican cuando su índice de sesión es igual a 1 (primera visita).
- El sistema realiza un seguimiento de estos identificadores para distinguir los nuevos visitantes de los que regresan.

**Notas importantes:**

Este método de seguimiento tiene algunas limitaciones conocidas:

- **Usuarios entre dispositivos:** La misma persona que visita desde diferentes dispositivos (escritorio, móvil, tableta) o exploradores se cuenta como varios visitantes únicos, ya que cada dispositivo y explorador recibe un identificador diferente.
- **Borrado de cookies:** A los usuarios que borran las cookies del explorador se les asigna un nuevo identificador y se cuentan de nuevo como nuevos visitantes.
- **Configuración de privacidad:** Es posible que no se realice un seguimiento de los usuarios con una configuración de privacidad estricta o bloqueadores de cookies.

**Mejor para:**

- Seguimiento de las nuevas tendencias de visitantes a lo largo del tiempo.
- Análisis de la eficacia de campañas de marketing.
- Comprender los patrones de crecimiento del tráfico.

**Sugerencia de interpretación:** Aunque no es perfectamente precisa debido a las limitaciones anteriores, las métricas de adquisición son fiables para identificar tendencias y comparar períodos en los que la mayoría de los usuarios navegan en el mismo dispositivo y no borran las cookies con frecuencia.

### Estrategias

- **Aprovechar los datos de rendimiento de la búsqueda**: Use el informe [rendimiento de la búsqueda](../manage-results/search-performance.md) para identificar los productos de tendencias y los términos de búsqueda más populares. Cree reglas de comercialización para resaltar estos artículos.

- **Optimizar el rendimiento de las recomendaciones**: supervise las métricas de [rendimiento de las recomendaciones](../manage-results/recommendation-performance.md) para identificar qué tipos de recomendaciones generan la mayor cantidad de tráfico y conversiones.

- **Resaltar artículos nuevos y promocionales**: Use reglas de comercialización para impulsar nuevos productos o artículos promocionales en los resultados de búsqueda y así atraer la atención de nuevos visitantes.

- **Rastrear fuentes de tráfico**: Use los datos de evento para comprender qué canales aportan el tráfico más valioso y optimizar los esfuerzos de marketing en consecuencia.

>[!TAB Reducción de tasa de devolución]

Para reducir la tasa de salida hacia otro sitio, el objetivo es mantener el interés de los visitantes y reducir las visitas de una sola página.

![Tasa de devoluciones de métricas de éxito](../assets/bounce-rate.png)

### Explicación de la métrica de tasa de salida hacia otro sitio

**Lo que mide:** Porcentaje de visitantes que abandonan el sitio después de ver una sola página, lo que indica posibles problemas con la experiencia del usuario, la relevancia de la página o la participación en el sitio.

**Cómo se calcula:** La tasa de salida hacia otro sitio compara las sesiones de una sola página con el total de sesiones para determinar qué porcentaje de visitantes se van sin más interacción.

**Fórmula:**

```
Bounce Rate = (Number of Bounced Sessions ÷ Total Sessions) × 100
```

**Fuente de datos:** eventos de tienda.

**Cómo funciona:**

- Se cuenta una **sesión devuelta** cuando un visitante ve solo una página durante toda su visita.
- El sistema realiza un seguimiento de las vistas de página en cada sesión para identificar las visitas de una sola página.
- Las sesiones están determinadas por la actividad del usuario y el tiempo entre interacciones.

**Qué causa las devoluciones:**

- Visitantes que aterrizan en páginas irrelevantes (mala búsqueda/segmentación de anuncios).
- Tiempos de carga de página lentos.
- Experiencia del usuario deficiente o navegación confusa.
- Búsqueda rápida de información sin necesidad de explorarla más.
- Problemas o errores técnicos.

**Notas importantes:**

- Las altas tasas de devolución no siempre son negativas: algunas páginas (como información de contacto o especificaciones específicas del producto) pueden tener naturalmente altas tasas de devolución.
- Compare las tasas de devolución en diferentes tipos de página y fuentes de tráfico para identificar las áreas problemáticas.
- Los incrementos repentinos en la tasa de salida hacia otro sitio suelen indicar problemas técnicos o una mala segmentación de campañas.

**¿Qué es una buena tasa de salida hacia otro sitio?** Esto varía según el sector y el tipo de página, pero en general:

- 40-60%: Promedio para sitios de comercio electrónico.
- Por debajo del 40%: Excelente compromiso.
- Por encima del 70%: puede indicar problemas que requieren investigación.

### Estrategias

- **Mejorar la relevancia de la búsqueda**: Use sinónimos y faceteo inteligente para garantizar que los clientes encuentren productos relevantes rápidamente. Los resultados de búsqueda deficientes son una causa importante de las altas tasas de devolución.

- **Implementar unidades de recomendación**: Implemente unidades de recomendación en páginas de categoría y resultados de búsqueda para proporcionar opciones de producto adicionales y mantener el interés de los visitantes.

- **Optimizar la detección de productos**: use reglas de comercialización para asegurarse de que los productos más relevantes y populares aparezcan primero en los resultados de búsqueda.

- **Cree experiencias atractivas en la página principal**: use los tipos de recomendación &quot;Recomendado para usted&quot; y &quot;Tendencia&quot; en su página principal para atraer de inmediato a los visitantes con contenido relevante.

>[!ENDTABS]

## Solución de problemas y optimización

### Cuando las métricas declinan

**Ingresos en disminución**:

- Compruebe si las unidades de recomendación siguen activas y funcionan bien.
- Revise las reglas de comercialización para asegurarse de que se promocionan los productos con un alto margen.
- Analice el rendimiento de la búsqueda para identificar si los productos populares siguen teniendo una buena clasificación.

**Disminución de la tasa de conversión**:

- Compruebe que se mantiene la relevancia de la búsqueda (compruebe sinónimos y facetas).
- Asegúrese de que las unidades de recomendación se muestran correctamente.
- Revise las reglas de comercialización en busca de conflictos o problemas.

**Altas tasas de devolución**:

- Compruebe la relevancia de los resultados de búsqueda e implemente sinónimos si es necesario.
- Asegúrese de que las unidades de recomendación se cargan correctamente.
- Revise la calidad y disponibilidad de los datos del producto.

**Baja participación**:

- Diversifique los tipos de recomendaciones para evitar la fatiga de los clientes.
- Implementar estrategias de recomendación más personalizadas.
- Optimice la experiencia de búsqueda con mejores facetas y sinónimos.

## Descripciones de campos

### Configuración del informe

| Campo | Descripción |
|---|---|
| Intervalo de fechas | Las opciones incluyen **Últimos 3 meses**, **Últimos 7 días**, **Últimos 30 días**, **Últimos 6 meses**, **Últimos 12 meses** y **Año hasta la fecha**. Utilice intervalos más cortos para obtener perspectivas de optimización inmediatas e intervalos más largos para el análisis de tendencias. |
| País | Basado en el origen de catálogo especificado para su [vista de catálogo](../setup/catalog-view.md). Seleccione el mercado apropiado para un análisis preciso del rendimiento. |
| Moneda | La moneda especificada para la vista de catálogo. Asegúrese de que coincida con su mercado objetivo para obtener informes de ingresos precisos. |
| Exportar | Guarda el informe como un PDF para compartirlo con las partes interesadas o para analizarlo sin conexión. |

## Más parecido a esto

- [Rendimiento de búsqueda](../manage-results/search-performance.md): Analice los términos de búsqueda y optimice la relevancia de la búsqueda.
- [Rendimiento de recomendaciones](../manage-results/recommendation-performance.md): supervise y optimice la eficacia de las recomendaciones.
- [Resumen de recomendaciones](../merchandising/recommendations/overview.md): obtenga información sobre recomendaciones de productos con tecnología de IA.
- [Reglas de comercialización](../merchandising/rules/overview.md): aumente, entierre, fije u oculte productos en los resultados de búsqueda.
- [Facetas](../merchandising/facets/overview.md): mejore la búsqueda con filtrado inteligente.
- [Sinónimos](../merchandising/synonyms/overview.md): mejore la relevancia de búsqueda y la experiencia del cliente.
- [Información general sobre eventos](../setup/events/overview.md): comprenda los datos que alimentan sus métricas.
