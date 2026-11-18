---
source-git-commit: e3be9274ca8db80d3559b24a5c8be36f5d61b2ba
workflow-type: tm+mt
source-wordcount: '913'
ht-degree: 0%
---
<!--
SOURCE OF TRUTH: Edit this file in the commerce.en repo:
https://github.com/Adobe-Enterprise-Docs/commerce.en/blob/main/help/_includes/ccdm-shared/merchandising/rules/best-practice.md

This content is shared by the Adobe Commerce Optimizer Guide (commerce.en) and the
Merchandising Services with CCDM Guide (commerce-admin.en). Changes made in commerce.en
are synced automatically to commerce-admin.en, so do not edit the copy in that repo.
This includes related images in help/assets/ccdm-shared/.
-->

# Prácticas recomendadas de reglas de comercialización

Para optimizar la conversión y los ingresos, implemente **reglas de búsqueda** efectivas, una regla de **listado predeterminado** sólida y **[reglas de categoría](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#rule-types)**. Ajuste las clasificaciones con los datos de ventas, las existencias, las promociones y la [clasificación inteligente](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking).

Use [reglas de supresión de búsqueda](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/overview#search-suppression-rules) solo cuando las consultas de comprador coincidentes deban devolver cero productos, no cuando los productos necesiten una clasificación diferente.

Es crucial establecer una **regla predeterminada** bien pensada. Su [regla predeterminada](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/overview#default-rule) determina cómo se ordenan inicialmente los resultados de búsqueda cuando no se aplica ninguna regla de búsqueda más específica, lo que mejora la probabilidad de detección y compra. Revíselo regularmente para que siga el ritmo de las necesidades y campañas del comprador.

## Sugerencias para optimizar las reglas de búsqueda

- Fije o aumente productos con altos volúmenes de ventas o actividad de ventas reciente.
- Priorice los productos con altas calificaciones y críticas positivas.
- Asegúrese de que los artículos en stock tengan una clasificación más alta.
- Priorice ligeramente los productos con márgenes de beneficio más altos sin poner en riesgo la relevancia.
- Resaltar productos que están a la venta o que forman parte de promociones especiales.
- Defina automáticamente reglas de búsqueda durante los periodos de promoción o ventas utilizando el intervalo de fechas durante el periodo de promoción.
- Adapte los resultados de búsqueda según el comportamiento de cada comprador mediante [clasificación inteligente](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking), como &quot;recomendado para usted&quot;, &quot;más visitados&quot;, etc.
- Cuando se selecciona una estrategia inteligente distinta de **None**, se debe ajustar **[Aumento inteligente de la clasificación](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking-boost)** por regla y validar en **Probar la regla** antes de publicar.
- Utilice siempre el panel &quot;Probar la regla&quot; para obtener una vista previa de cómo la estrategia de clasificación inteligente afecta a los resultados de búsqueda reales de diferentes consultas.

## Sugerencias para reglas de categoría

- Use [reglas de categoría](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#rule-types) en **páginas de categoría** con mucho tráfico o con mucho margen donde los pedidos revisados importen tanto como la búsqueda; por ejemplo, colecciones de temporada o departamentos destacados.
- Alinee la **clasificación inteligente** (por ejemplo, tendencias, más visitados) con la forma en que los compradores examinan esa categoría; las páginas de categoría no utilizan el texto de consulta de búsqueda como lo hacen las reglas de búsqueda. Consulte [Clasificación inteligente](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking). Para métodos inteligentes distintos de **None**, use **[Aumento de clasificación inteligente](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#intelligent-ranking-boost)** y vista previa de categoría para ajustar la fuerza de comportamiento de esa regla de categoría.
- Aplique **pin**, **boost** y **bury** de forma coherente con su plan de campaña; recuerde que las posiciones manuales normalmente se aplican únicamente cuando el comprador utiliza el **orden predeterminado** para el anuncio. Ver [Clasificación manual](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#manual-ranking).
- Obtenga una vista previa en el flujo de reglas **category** en el editor y valide en la tienda después de la publicación, la misma disciplina que usa para el panel &quot;Probar la regla&quot; en la búsqueda.

## Prácticas recomendadas y casos de uso para la supresión de búsquedas {#search-suppression-best-practices}

Una regla de supresión de búsqueda bloquea los resultados de las consultas que cumplen sus condiciones, por lo que la tienda muestra una página de resultados de búsqueda sin ningún producto. El editor de reglas no proporciona una previsualización para reglas de supresión. Use la condición más estricta que cumpla la restricción y, a continuación, siga [Crear y administrar reglas de supresión de búsqueda](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add#search-suppression-rules). Cuando la regla se active, compruebe las búsquedas coincidentes y no coincidentes en la tienda. Compruebe la presentación real sin resultados de la tienda.

| Caso de uso | Configuración sugerida | Qué comprobar |
| --- | --- | --- |
| Cumplimiento normativo de la búsqueda | Aplique el ámbito de la regla a la vista de catálogo afectada y coincida con los términos de búsqueda restringidos. | Confirme los términos con su equipo de cumplimiento. La supresión de la búsqueda por sí sola no impide el acceso mediante la navegación por categorías, páginas de comercialización, recomendaciones o direcciones URL directas de productos. |
| Restricciones de marca | Use **La consulta contiene** cuando un nombre de marca restringido deba bloquearse en consultas más largas. | Una vez que la regla se active, compruebe las consultas de tienda no relacionadas que contengan texto similar para evitar la supresión de búsquedas legítimas. |
| Impedir que un término de búsqueda específico devuelva resultados | Use **La consulta es** para una frase exacta que no debería devolver ningún producto. | Compruebe las frases relacionadas por separado. Una condición de coincidencia exacta no bloquea todas las consultas que contengan esa frase. |
| Restricciones en prefijos o sufijos de consulta | Use **La consulta comienza con** o **La consulta termina con** cuando la ubicación del texto restringido es importante. | Una vez que la regla se haya activado, compruebe las consultas de tienda con el texto al principio, al medio y al final para confirmar el ámbito deseado. |
| Restricciones de búsqueda temporal | Establezca una fecha de inicio y de finalización para una restricción de tiempo limitado. | Confirme la programación y el estado habilitado y revise si la regla sigue siendo necesaria después de que finalice la restricción. |

- Asigne a cada regla un nombre descriptivo y registre el motivo de la restricción en su descripción.
- Revise las condiciones de la consulta antes de publicar los cambios. Una vez que la regla se haya activado, compruebe las consultas de tienda que deban bloquearse y las consultas que deban seguir devolviendo productos. Los resultados de las consultas en caché pueden tardar hasta 15 minutos en actualizarse.
- Revise el estado sin resultados de la tienda y asegúrese de que los compradores tengan una forma útil de continuar navegando, como revisar la consulta o navegar a una categoría, donde sea compatible con la tienda.
- No utilice la supresión de consultas como sustituto de las exclusiones de nivel de producto. Para excluir productos en los resultados de búsqueda, las sugerencias de búsqueda y la autocompletar, usa exclusiones manuales o **Eventos de comercialización basados en atributos** con una acción **Ocultar** en la **regla de búsqueda predeterminada**.
- Revise las reglas de supresión activas con regularidad. Deshabilite las reglas que ya no sean necesarias, o edítelas y publíquelas cuando cambien las restricciones.
