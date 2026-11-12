---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%
---
Para optimizar la conversión y los ingresos, implemente **reglas de búsqueda** efectivas, una regla de **listado predeterminado** sólida y **[reglas de categoría](https://experienceleague.adobe.com/es/docs/commerce/optimizer/merchandising/rules/add#rule-types)**. Ajuste las clasificaciones con los datos de ventas, las existencias, las promociones y la [clasificación inteligente](https://experienceleague.adobe.com/es/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking).

Es crucial establecer una **regla predeterminada** bien pensada. Su [regla predeterminada](https://experienceleague.adobe.com/es/docs/commerce/optimizer/merchandising/rules/overview#default-rule) determina cómo se ordenan inicialmente los resultados de búsqueda cuando no se aplica ninguna regla de búsqueda más específica, lo que mejora la probabilidad de detección y compra. Revíselo regularmente para que siga el ritmo de las necesidades y campañas del comprador.

## Sugerencias para optimizar las reglas de búsqueda

- Fije o aumente productos con altos volúmenes de ventas o actividad de ventas reciente.
- Priorice los productos con altas calificaciones y críticas positivas.
- Asegúrese de que los artículos en stock tengan una clasificación más alta.
- Priorice ligeramente los productos con márgenes de beneficio más altos sin poner en riesgo la relevancia.
- Resaltar productos que están a la venta o que forman parte de promociones especiales.
- Defina automáticamente reglas de búsqueda durante los periodos de promoción o ventas utilizando el intervalo de fechas durante el periodo de promoción.
- Adapte los resultados de búsqueda según el comportamiento de cada comprador mediante [clasificación inteligente](https://experienceleague.adobe.com/es/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking), como &quot;recomendado para usted&quot;, &quot;más visitados&quot;, etc.
- Cuando se selecciona una estrategia inteligente distinta de **None**, se debe ajustar **[Aumento inteligente de la clasificación](https://experienceleague.adobe.com/es/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking-boost)** por regla y validar en **Probar la regla** antes de publicar.
- Utilice siempre el panel &quot;Probar la regla&quot; para obtener una vista previa de cómo la estrategia de clasificación inteligente afecta a los resultados de búsqueda reales de diferentes consultas.

## Sugerencias para reglas de categoría

- Use [reglas de categoría](https://experienceleague.adobe.com/es/docs/commerce/optimizer/merchandising/rules/add#rule-types) en **páginas de categoría** con mucho tráfico o con mucho margen donde los pedidos revisados importen tanto como la búsqueda; por ejemplo, colecciones de temporada o departamentos destacados.
- Alinee la **clasificación inteligente** (por ejemplo, tendencias, más visitados) con la forma en que los compradores examinan esa categoría; las páginas de categoría no utilizan el texto de consulta de búsqueda como lo hacen las reglas de búsqueda. Consulte [Clasificación inteligente](https://experienceleague.adobe.com/es/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking). Para métodos inteligentes distintos de **None**, use **[Aumento de clasificación inteligente](https://experienceleague.adobe.com/es/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking-boost)** y vista previa de categoría para ajustar la fuerza de comportamiento de esa regla de categoría.
- Aplique **pin**, **boost** y **bury** de forma coherente con su plan de campaña; recuerde que las posiciones manuales normalmente se aplican únicamente cuando el comprador utiliza el **orden predeterminado** para el anuncio. Ver [Clasificación manual](https://experienceleague.adobe.com/es/docs/commerce/optimizer/merchandising/rules/add#manual-ranking).
- Obtenga una vista previa en el flujo de reglas **category** en el editor y valide en la tienda después de la publicación, la misma disciplina que usa para el panel &quot;Probar la regla&quot; en la búsqueda.
