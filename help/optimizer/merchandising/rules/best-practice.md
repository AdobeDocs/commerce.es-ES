---
title: Prácticas recomendadas de reglas de comercialización
description: Conozca las prácticas recomendadas para implementar reglas de comercialización en las páginas de búsqueda, listados predeterminados y categorías.
role: Admin, Developer
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a Adobe Commerce as a Cloud Service y  [!DNL Adobe Commerce Optimizer] proyectos (infraestructura SaaS administrada por Adobe)."
exl-id: cc8d0879-c253-4ad4-8e7d-e066dff9112d
source-git-commit: 8abc0593c166a2dd861cfb78674918de1d0744de
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---

# Prácticas recomendadas de reglas de comercialización

Para optimizar la conversión y los ingresos, implemente **reglas de búsqueda** efectivas, una regla de **listado predeterminado** sólida y **[reglas de categoría](add.md#category-rules)** (beta). Ajuste las clasificaciones con los datos de ventas, las existencias, las promociones y la [clasificación inteligente](add.md#intelligent-ranking).

Es crucial establecer una **regla predeterminada** bien pensada. Su [regla predeterminada](overview.md#default-rule) determina cómo se ordenan inicialmente los resultados de búsqueda cuando no se aplica ninguna regla de búsqueda más específica, lo que mejora la probabilidad de detección y compra. Revíselo regularmente para que siga el ritmo de las necesidades y campañas del comprador.

## Sugerencias para optimizar las reglas de búsqueda

- Fije o aumente productos con altos volúmenes de ventas o actividad de ventas reciente.
- Priorice los productos con altas calificaciones y críticas positivas.
- Asegúrese de que los artículos en stock tengan una clasificación más alta.
- Priorice ligeramente los productos con márgenes de beneficio más altos sin poner en riesgo la relevancia.
- Resaltar productos que están a la venta o que forman parte de promociones especiales.
- Defina automáticamente reglas de búsqueda durante los periodos de promoción o ventas utilizando el intervalo de fechas durante el periodo de promoción.
- Adapte los resultados de búsqueda según el comportamiento de cada comprador mediante [clasificación inteligente](add.md#intelligent-ranking), como &quot;recomendado para usted&quot;, &quot;más visitados&quot;, etc.
- Utilice siempre el panel &quot;Probar la regla&quot; para obtener una vista previa de cómo la estrategia de clasificación inteligente afecta a los resultados de búsqueda reales de diferentes consultas.

## Sugerencias para reglas de categoría

>[!IMPORTANT]
>
>Las reglas de categoría están en versión beta.

- Use [reglas de categoría](add.md#category-rules) en **páginas de categoría** con mucho tráfico o con mucho margen donde los pedidos revisados importen tanto como la búsqueda; por ejemplo, colecciones de temporada o departamentos destacados.
- Alinee la **clasificación inteligente** (por ejemplo, tendencias, más visitados) con la forma en que los compradores examinan esa categoría; las páginas de categoría no utilizan el texto de consulta de búsqueda como lo hacen las reglas de búsqueda. Consulte [Clasificación inteligente](add.md#intelligent-ranking).
- Aplique **pin**, **boost** y **bury** de forma coherente con su plan de campaña; recuerde que las posiciones manuales normalmente se aplican únicamente cuando el comprador utiliza el **orden predeterminado** para el anuncio. Ver [Clasificación manual](add.md#manual-ranking).
- Obtenga una vista previa en el flujo de reglas **category** en el editor y valide en la tienda después de la publicación, la misma disciplina que usa para el panel &quot;Probar la regla&quot; en la búsqueda.
