---
source-git-commit: 3478e3f0162b553d03c4ac4f5b3000b8aabd8c66
workflow-type: tm+mt
source-wordcount: '1209'
ht-degree: 0%
---
Las reglas de comercialización combinan lógica con acciones para dar forma al aspecto de los productos en **resultados de búsqueda**, en **listados de productos predeterminados** a través de la **regla de búsqueda predeterminada** y en **páginas de categoría**. Puedes aumentar, enterrar, fijar u ocultar productos y aplicar **clasificación inteligente** para que los anuncios reflejen tus objetivos comerciales. Use **reglas de supresión de búsqueda** para evitar que las consultas de búsqueda coincidentes devuelvan resultados.

Cada **regla de búsqueda** tiene tres componentes principales:

- **Condiciones**: requisitos basados en consultas que requieren una acción cuando la búsqueda del comprador coincide.
- **Eventos**: las acciones que tienen lugar cuando se cumplen las condiciones (clasificación manual y eventos relacionados).
- **Detalles**: el nombre de la regla, el lapso de tiempo y la descripción opcionales.

**Las reglas de categoría** utilizan **selección de categoría** en lugar de las condiciones de consulta de búsqueda; la clasificación inteligente y la clasificación manual funcionan de la misma manera que para la búsqueda, con diferencias indicadas en [Crear y administrar reglas](https://experienceleague.adobe.com/es/docs/commerce/optimizer/merchandising/rules/add).

Puede combinar varias condiciones y acciones para reglas de búsqueda y programar reglas para que estén activas durante un periodo. Las reglas de supresión de búsqueda utilizan condiciones de consulta para bloquear resultados en lugar de clasificar productos. También puede establecer una **regla de búsqueda predeterminada** que se aplique cuando no se aplique una regla de categoría o búsqueda más específica.

## Reglas de supresión de búsqueda {#search-suppression-rules}

Las reglas de supresión de búsqueda son un tipo de regla de comercialización que bloquea los resultados de las consultas de comprador coincidentes. Estas búsquedas no devuelven ningún producto en la tienda. Una vez que la regla se active, verifique la presentación real sin resultados de la tienda.

Utilice la supresión de búsqueda para restricciones de búsqueda reglamentarias, restricciones de marca o términos específicos que no deban devolver resultados. Las condiciones admiten **La consulta es**, **La consulta contiene**, **La consulta comienza con** y **La consulta termina con**. Para ver los pasos de configuración y administración, consulte [Crear y administrar reglas de supresión de búsqueda](https://experienceleague.adobe.com/es/docs/commerce/optimizer/merchandising/rules/add#search-suppression-rules). Para ver ejemplos, consulte [Prácticas recomendadas](https://experienceleague.adobe.com/es/docs/commerce/optimizer/merchandising/rules/best-practice#search-suppression-best-practices).

La supresión de la búsqueda afecta únicamente a la experiencia de búsqueda. No cambia la visibilidad del producto a través de la navegación por categorías, páginas de comercialización, recomendaciones ni direcciones URL directas del producto. No sustituye a los controles de acceso o a la visibilidad del producto en todo el catálogo.

### Interacción con otras capacidades de comercialización

| Capacidad | Interacción con la supresión de búsqueda |
| --- | --- |
| Buscar reglas | Para una consulta que coincide con una regla de supresión de búsqueda activa, la tienda muestra una página de resultados de búsqueda con cero productos. Las acciones de clasificación en una regla de búsqueda no anulan la supresión. Las consultas que no están bloqueadas siguen utilizando reglas de comercialización aplicables. |
| Reglas de categoría | La navegación por categorías y la comercialización de categorías no se ven afectadas por la supresión de búsquedas. Un producto puede permanecer visible en una categoría incluso cuando se bloquea una consulta de búsqueda. |
| Regla de búsqueda predeterminada | La supresión de la búsqueda bloquea las consultas que coinciden, mientras que la regla de búsqueda predeterminada define la clasificación predeterminada y las exclusiones de productos. La clasificación predeterminada no restaura los resultados de una consulta bloqueada. |
| Eventos de comercialización basados en atributos | Estos eventos aplican acciones a productos que cumplen las condiciones de los atributos, tal como se describe en [Clasificación de atributos](https://experienceleague.adobe.com/es/docs/commerce/optimizer/merchandising/rules/add#attribute-ranking). En su lugar, la supresión de la búsqueda bloquea los resultados de una consulta coincidente, independientemente de qué productos coincidirían. |

Los productos excluidos por la **regla de búsqueda predeterminada**, a través de exclusiones manuales o de **Eventos de comercialización basados en atributos** con una acción **Ocultar**, también se excluyen de **sugerencias de búsqueda y autocompletar**. Esto mantiene la coherencia de las exclusiones de productos en toda la experiencia de búsqueda y es independiente del bloqueo de consultas con una regla de supresión de búsqueda.

## Reglas de categoría {#category-rules}

**Reglas de categoría** controlan el pedido de productos en **páginas de categoría**. Selecciona una o más categorías y, a continuación, aplica una clasificación inteligente (por ejemplo, más visitados, tendencias) y acciones manuales como anclar, aumentar y enterrar. No utilizan condiciones de consulta de búsqueda. Para ver los pasos de configuración, los tipos de reglas y cómo se aplica la clasificación en la categoría en comparación con la búsqueda, consulte [Crear y administrar reglas](https://experienceleague.adobe.com/es/docs/commerce/optimizer/merchandising/rules/add).

## Requisitos

Una **regla de búsqueda** simple puede tener una sola condición y un solo evento, mientras que una regla compleja puede tener hasta diez condiciones que almacenen en déclencheur hasta 25 eventos. **Las reglas de categoría** siguen los mismos límites de evento para la clasificación manual; no utilizan condiciones de consulta.

Las reglas pueden tener:

- Hasta diez **condiciones** (solo reglas de búsqueda)
- Hasta 25 **eventos**

El texto de la consulta puede contener:

- Caracteres alfanuméricos (letras y números)
- Caracteres en mayúsculas o minúsculas. Se omiten las mayúsculas.

## Operadores lógicos

Los operadores lógicos `AND` y `OR` unen dos condiciones y devuelven resultados diferentes. Todos los operadores lógicos utilizados en una regla con varias condiciones son los mismos. No es posible usar `AND` y `OR` a la vez en la misma regla.

### Operadores de coincidencia

Los operadores de coincidencia `All` y `Any` determinan el operador lógico que se usa para unir varias condiciones en la regla y se puede usar para cambiar el operador existente.

- `All`: utiliza el operador lógico `AND` para unir varias condiciones. Una regla que usa el operador de coincidencia `All` solo puede tener una condición `Search query is`.
- `Any`: utiliza el operador lógico `OR` para unir varias condiciones.

Al componer una regla compleja, puede resultar útil escribirla con sangría para describir las condiciones, los eventos asociados y los nombres de producto o SKU necesarios para devolver los resultados que desea lograr. A continuación, genere la regla y pruebe el resultado.

## Regla predeterminada

Puede establecer una **regla de búsqueda predeterminada** que se aplique cuando no se proporciona ningún término de búsqueda o cuando no se puede aplicar ninguna otra regla de búsqueda. Si establece la regla predeterminada en Más compradas, las consultas predeterminadas corresponden a ese tipo de clasificación a menos que se las sustituya por un término de búsqueda más específico. No se puede establecer ningún término de búsqueda para la regla predeterminada. **Las reglas de categoría** son independientes: sólo se aplican a las categorías que seleccione y no reemplazan la regla de listado predeterminada.

## Orden de prioridad con varias reglas

En esta sección se explica cómo se aplican las reglas de búsqueda de clasificación a la consulta de un comprador y cómo interactúan entre sí. La clasificación de reglas de búsqueda no anula la supresión de búsqueda: cuando una regla de supresión activa coincide con una consulta, la tienda no devuelve ningún producto para esa búsqueda. Las reglas de categoría se aplican a las categorías seleccionadas. Consulte [Crear y administrar reglas](https://experienceleague.adobe.com/es/docs/commerce/optimizer/merchandising/rules/add) para obtener detalles acerca de la búsqueda, la categoría y las reglas de búsqueda predeterminadas.

Solo se aplica una regla de búsqueda a un término de búsqueda al mismo tiempo.
Si se encuentran varias reglas aplicables a una frase de búsqueda, se aplican todas estas reglas. Si hay un conflicto entre dos reglas (`rule 1` que aumenta sku1 pero `rule 2` oculta el mismo SKU), entonces la regla aplicada más recientemente (`rule 2`) tiene prioridad.

- Las reglas se ordenan por la marca de tiempo &quot;Última modificación&quot;. La regla modificada más recientemente se aplica primero, y las reglas más antiguas después, en orden de marca de tiempo.
- La condición `query is` tiene prioridad sobre otras condiciones. Si una regla más reciente contiene una condición `query contains`, pero una regla más antigua tiene una condición `query is`, se aplica la regla `query is`.

### Solicitudes de tienda

Si una regla activa que contiene una condición `query is` coincide con la frase de búsqueda, se aplica. Si hay varias reglas coincidentes con una condición `query is`, se aplica la regla activa actualizada más recientemente.
De lo contrario, se aplica la regla activa actualizada más recientemente.

### Previsualizar solicitudes

Las solicitudes realizadas en la vista previa funcionan de forma ligeramente diferente. Al obtener una vista previa, se aplican todas las reglas, incluidas las caducadas y programadas.

- Si la regla que se está previsualizando tiene una condición `query is`, se aplica.
- Si la regla que se está previsualizando no tiene una condición `query is` y se encuentra una regla coincidente activa posterior con una condición `query is`, se aplica la regla `query is`.
- Si la regla que se está previsualizando no tiene una condición `query is` y no se encuentra ninguna otra regla con una condición `query is`, se aplica la regla que se está previsualizando.
