---
source-git-commit: 18c4528fade63545415135808d2d40ac2b95e86d
workflow-type: tm+mt
source-wordcount: '920'
ht-degree: 0%
---
Las facetas son un método de filtrado de alto rendimiento que utiliza varias dimensiones de valores de atributo como criterios de búsqueda.

![Resultados de búsqueda filtrados](/help/assets/ccdm-shared/facets/storefront-search-results-run.png)

Dentro de una faceta, los compradores pueden seleccionar varias opciones, como &quot;Básico&quot; y &quot;Cómodo&quot; en &quot;Estilo&quot;, y los resultados de la búsqueda se actualizan para mostrar solo esos estilos. Del mismo modo, si un comprador selecciona &quot;Básico&quot; en &quot;Estilo&quot; e &quot;Interior&quot; en &quot;Clima&quot;, los resultados de la búsqueda muestran esas selecciones.

Cualquier faceta definida puede utilizarse como parámetro de URL y los resultados se filtran según los valores del parámetro, por ejemplo: `http://yourstore.com?brand=acme&color=red`.

## Agregación de facetas

La agregación de facetas se realiza de la siguiente manera: si la tienda tiene tres facetas (categorías, color y precio) y el comprador filtra las tres (color = azul, el precio está entre 10,00 y 50,00 $, `categories` = `promotions`)

- Agregación `categories`: agrega `categories` y, a continuación, aplica los filtros `color` y `price`, pero no el filtro `categories`.
- Agregación `color`: agrega `color` y, a continuación, aplica los filtros `price` y `categories`, pero no el filtro `color`.
- Agregación `price`: agrega `price` y, a continuación, aplica los filtros `color` y `categories`, pero no el filtro `price`.

## Valores de atributo predeterminados

El sistema habilita los siguientes atributos de producto de forma predeterminada.

| Propiedad | Descripción | Atributo |
|---|---|---|
| Ordenable | Se utiliza para ordenar en la lista de productos | `price` |
| Buscable | Uso en la búsqueda | `price` <br />`sku`<br />`name` |

Obtenga más información acerca de los atributos del producto y sus propiedades:

- Para implementaciones conectadas a un servidor de Adobe Commerce, consulte [Descripción general de los atributos del producto](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/product-attributes)
- Para implementaciones que utilizan un servidor Commerce de terceros, consulte la [API de metadatos de ingesta de datos](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/#metadata).

## Búsqueda por capas y expansión de tipos de búsqueda

La búsqueda por capas, o búsqueda dentro de una búsqueda, es un sistema de filtrado basado en atributos que amplía la funcionalidad de búsqueda tradicional para incluir parámetros de búsqueda adicionales. Estos parámetros de búsqueda adicionales permiten una detección de productos más precisa y flexible.

Con la búsqueda por capas puede:

- Permitir que los compradores busquen en los resultados de búsqueda.
- Restrinja aún más los resultados utilizando la indexación de búsqueda `startsWith` y `contains` en la segunda capa de la búsqueda por capas.

Las funcionalidades de búsqueda avanzada se implementan a través del parámetro `filter` en la consulta [`productSearch`](https://developer.adobe.com/commerce/services/reference/graphql/#productsearch) utilizando operadores específicos:

- **Búsqueda por niveles**—Buscar en otro contexto de búsqueda—Con esta capacidad, puede realizar hasta dos niveles de búsqueda para sus consultas de búsqueda. Por ejemplo:

  - **Búsqueda de nivel 1**: busque &quot;motor&quot; en `product_attribute_1`.
  - **Búsqueda de nivel 2**: busque &quot;número de pieza 123&quot; en `product_attribute_2`. En este ejemplo se busca &quot;número de pieza 123&quot; dentro de los resultados para &quot;motor&quot;.

  La búsqueda por capas está disponible tanto para la indexación de búsqueda `startsWith` como para la indexación de búsqueda `contains` en la segunda capa de la búsqueda por capas, como se describe a continuación:

- **startsWith la indexación de búsqueda**—Search using `startsWith` indexation. Esta capacidad permite:

  - Buscando productos en los que el valor del atributo comience con una cadena especificada.
  - Configuración de una búsqueda &quot;termina con&quot; para que los compradores puedan buscar productos en los que el valor del atributo termine con una cadena en particular.
    - Para habilitar una búsqueda &quot;termina con&quot;, introduzca el atributo de producto al revés y utilice una cadena invertida para la llamada de API. Por ejemplo, si desea buscar un nombre de producto que termine con &quot;pantalones&quot;, debe enviarlo como &quot;stnap&quot;.

- **contiene indización de búsqueda**: la búsqueda de un atributo mediante contiene indización. Esta nueva capacidad permite:

  - Búsqueda de una consulta dentro de una cadena más grande. Por ejemplo, si un comprador busca el número de producto PE-123 en la cadena HAPE-123.

    - Nota: este tipo de búsqueda es diferente de la búsqueda de frases [existente](https://developer.adobe.com/commerce/services/reference/graphql/#productsearch), que realiza una búsqueda de autocompletar. Por ejemplo, si el valor de atributo del producto es &quot;pantalones de exterior&quot;, una búsqueda de frase devuelve una respuesta para &quot;sin bandeja&quot;, pero no devuelve una respuesta para &quot;u hormigas&quot;. Sin embargo, una búsqueda contiene sí devuelve una respuesta para &quot;o hormigas&quot;.

Estas nuevas condiciones mejoran el mecanismo de filtrado de consultas de búsqueda para restringir los resultados de búsqueda. Estas nuevas condiciones no afectan a la consulta de búsqueda principal.

### Implementación

1. [Establecer atributos como para búsqueda](https://developer.adobe.com/commerce/services/reference/rest/#tag/Metadata).

1. Especifique la capacidad de búsqueda para ese atributo, como **Contiene** (predeterminado) o **Comienza con**. Para habilitar **Contiene** y **Comienza con**, especifique un máximo de seis atributos para cada uno. Además, para la indexación **Contiene**, la longitud de la cadena está limitada a 50 caracteres o menos.

1. Consulte la [documentación para desarrolladores](https://developer.adobe.com/commerce/services/reference/graphql/#productsearch) para ver ejemplos de cómo actualizar las llamadas a la API de GraphQL de Adobe Merchandising Services con las nuevas funciones de búsqueda `contains` y `startsWith`.

   Puede implementar estas nuevas condiciones en la página de resultados de búsqueda. Por ejemplo, puede agregar una nueva sección en la página donde el comprador pueda restringir aún más los resultados de búsqueda. Puede permitir que los compradores seleccionen atributos de producto específicos, como Fabricante, Número de pieza y Descripción. Desde allí, buscan dentro de esos atributos utilizando las condiciones `contains` o `startsWith`.

### Cuándo utilizar la búsqueda por capas en lugar de las facetas

La búsqueda por capas y las facetas sirven para diferentes propósitos en la detección de productos y la elección entre ellos depende de su caso de uso específico:

**Usar búsqueda por capas para:**

- Buscar en los resultados de búsqueda utilizando varios criterios
- Trabaje con números de pieza, SKU o especificaciones técnicas cuando los usuarios conozcan información parcial
- Permitir que los compradores reduzcan los resultados paso a paso con criterios anidados
- Reduzca la cantidad de llamadas de API combinando varios criterios de búsqueda en una sola consulta
- Implementar patrones de búsqueda específicos de la empresa que vayan más allá de la navegación con facetas estándar

**Usar facetas para:**

- Proporcionar filtrado típico de categoría, precio, marca y atributo
- Ofrezca opciones de filtro intuitivas que los usuarios puedan comprender y seleccionar fácilmente
- Mostrar las opciones disponibles según los resultados de búsqueda actuales
- Mostrar recuentos e intervalos de filtros que ayuden a los usuarios a comprender las opciones disponibles
- Trabaje con características comunes de producto, como color, tamaño y material

**Práctica recomendada:** Utilice la búsqueda por niveles para búsquedas técnicas y complejas en las que los usuarios tengan criterios específicos y utilice facetas para el filtrado estándar de comercio electrónico en las que los usuarios deseen explorar y refinar las opciones visualmente.
