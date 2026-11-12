---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '803'
ht-degree: 0%
---
Las reglas de comercialización combinan lógica con acciones para dar forma al aspecto de los productos en **resultados de búsqueda**, en **listados de productos predeterminados** a través de la **regla de búsqueda predeterminada** y en **páginas de categoría**. Puedes aumentar, enterrar, fijar u ocultar productos y aplicar **clasificación inteligente** para que los anuncios reflejen tus objetivos comerciales.

Cada **regla de búsqueda** tiene tres componentes principales:

- **Condiciones**: requisitos basados en consultas que requieren una acción cuando la búsqueda del comprador coincide.
- **Eventos**: las acciones que tienen lugar cuando se cumplen las condiciones (clasificación manual y eventos relacionados).
- **Detalles**: el nombre de la regla, el lapso de tiempo y la descripción opcionales.

**Las reglas de categoría** utilizan **selección de categoría** en lugar de las condiciones de consulta de búsqueda; la clasificación inteligente y la clasificación manual funcionan de la misma manera que para la búsqueda, con diferencias indicadas en [Crear y administrar reglas](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add).

Puede combinar varias condiciones y acciones para las reglas de búsqueda y programar cualquier regla para que esté activa durante un periodo. También puede establecer una **regla de búsqueda predeterminada** que se aplique cuando no se aplique una regla de categoría o búsqueda más específica.

## Reglas de categoría {#category-rules}

**Reglas de categoría** controlan el pedido de productos en **páginas de categoría**. Selecciona una o más categorías y, a continuación, aplica una clasificación inteligente (por ejemplo, más visitados, tendencias) y acciones manuales como anclar, aumentar y enterrar. No utilizan condiciones de consulta de búsqueda. Para ver los pasos de configuración, los tipos de reglas y cómo se aplica la clasificación en la categoría en comparación con la búsqueda, consulte [Crear y administrar reglas](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add).

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

Lo siguiente se aplica a **reglas de búsqueda** y a cómo interactúan para una búsqueda determinada. Se aplican **reglas de categoría** por categoría; consulte [Crear y administrar reglas](https://experienceleague.adobe.com/en/docs/commerce/optimizer/merchandising/rules/add) para ver cómo se ajustan a las reglas predeterminadas y de búsqueda.

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
