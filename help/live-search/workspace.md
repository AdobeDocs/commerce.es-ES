---
title: Configuración de Live Search
description: El área de trabajo  [!DNL Live Search] se usa para configurar, administrar y supervisar el rendimiento de la búsqueda.
exl-id: 07c32b26-3fa4-4fae-afba-8a10866857c3
source-git-commit: a22a57f52503811a3a3e9294174a6626c5630b79
workflow-type: tm+mt
source-wordcount: '1990'
ht-degree: 0%

---

# Configuración de Live Search

En el área de trabajo es donde se configura, administra y supervisa el rendimiento de [!DNL Live Search]. El menú de la parte superior proporciona acceso a las herramientas de cada área funcional. Las funciones disponibles reflejan la selección actual del menú.

![Workspace](assets/workspace.png)

## Recopilación de datos

Para asegurarse de que cada área funcional del espacio de trabajo contiene los datos correctos, debe configurar la recopilación de datos en función de la implementación de tienda seleccionada:

1. Luma: la recopilación de datos está disponible de forma predeterminada.
1. Sin encabezado: la recopilación de datos debe configurarse manualmente, según la implementación de la tienda.

Si utiliza una tienda sin encabezado, consulte la siguiente documentación para obtener más información sobre los eventos necesarios que debe agregar:

- [Eventos requeridos](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#live-search) para el panel de Live Search.
- [Recopilador de eventos de tienda](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/) que debe agregarse como requisito previo.
- [Ejemplos](https://github.com/adobe/commerce-events/tree/main/examples) de la estructura de eventos.

### Clientes sanitarios

Si es cliente de atención médica e instaló la extensión HIPAA de [Data Services](../data-connection/hipaa-readiness.md#installation), que forma parte de la extensión [Data Connection](../data-connection/overview.md), ya no se capturarán los datos de evento de tienda que usa [!DNL Live Search]. Esto se debe a que los datos de evento de tienda se generan en el lado del cliente. Para seguir capturando y enviando datos de evento de tienda, vuelva a habilitar la recopilación de eventos para [!DNL Live Search]. Consulte [configuración general](https://experienceleague.adobe.com/en/docs/commerce-admin/config/general/general#data-services) para obtener más información.

## Establecer el ámbito

Inicialmente, el [ámbito](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html#scope-settings) de toda la configuración de [!DNL Live Search] se ha establecido en `Default Store View`. Si su instalación de [!DNL Commerce] incluye varias vistas de tienda, establezca **Ámbito** en la [vista de tienda](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html) donde se aplique la configuración de faceta.

## Opciones de menú

| Opción | Descripción |
|--- |--- |
| [Rendimiento](performance.md) | El panel proporciona insight en el rendimiento de búsqueda de productos. |
| [Faceteo](facets.md) | Filtro de alto rendimiento que utiliza varias dimensiones de valores de atributo para restringir los criterios de búsqueda. |
| [Sinónimos](synonyms.md) | Amplíe el alcance de la búsqueda para incluir las palabras que los compradores podrían utilizar para encontrar productos que difieran de los del catálogo. |
| [Buscar comercialización](rules.md) | Dé forma a la experiencia de búsqueda con reglas lógicas que almacenan en déclencheur las acciones programadas. Impulse, entierre, fije u oculte productos para calibrar los resultados de búsqueda y lograr así sus objetivos empresariales. |
| [Comercialización de categorías](category-merch.md) | Aplicar reglas y comercialización inteligente en el nivel de categoría. |
| [GraphQL](graphql.md) | Los desarrolladores que han iniciado sesión en el administrador de su tienda pueden componer y probar consultas con datos de catálogo reales. Para obtener más información, ve a [Información general de GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/) en la documentación para desarrolladores de [!DNL Live Search]. |
| [Configuración](settings.md) | Determine cómo se agrupan los valores de faceta de precio por intervalo de precio en la tienda y establezca el idioma de indexación. |

## Definir atributos como en los que se puede buscar

Para generar resultados de alto nivel de segmentación, revise el conjunto de atributos de producto [en los que se puede buscar](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/product-attributes.html) (`searchable=true`). Para garantizar la relevancia, haga que los atributos solo se puedan buscar si contienen contenido que tenga un significado claro y conciso. Evite utilizar atributos que contengan texto menos preciso y largo, como `description`, que aunque la búsqueda está habilitada de forma predeterminada, puede reducir la precisión de los resultados de búsqueda. Por ejemplo, si una persona busca &quot;pantalones cortos&quot; y hay camisas con una descripción que incluye el término &quot;mangas cortas&quot;, entonces las camisas se incluirán en los resultados de búsqueda.

Para permitir que se puedan buscar los atributos, complete los siguientes pasos:

1. En el Administrador, vaya a **Tiendas** > *Atributo* > **Producto**.
1. Seleccione el atributo en el que desea que se puedan realizar búsquedas, como `color`.
1. Seleccione **Propiedades de tienda** y establezca **Usar en búsqueda** en `yes`.

[!DNL Live Search] también respeta el [peso](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search-results.html#weighted-search) de un atributo de producto, tal como se establece en Adobe Commerce. Los atributos con un peso mayor aparecerán más arriba en los resultados de búsqueda.

Siempre se pueden buscar los atributos siguientes:

- `sku`
- `name`
- `categories`

### Búsqueda por capas y expansión de tipos de búsqueda

La búsqueda por capas, o búsqueda dentro de una búsqueda, es un potente sistema de filtrado basado en atributos que amplía la funcionalidad de búsqueda tradicional para incluir parámetros de búsqueda adicionales. Estos parámetros de búsqueda adicionales permiten una detección de productos más precisa y flexible.

>[!NOTE]
>
>La búsqueda por capas está disponible en Live Search 4.6.0.

Con la búsqueda por capas puede:

- Permitir que los compradores busquen en los resultados de búsqueda.
- Use la indexación de búsqueda `startsWith` y `contains` en la segunda capa de la búsqueda por capas para restringir aún más los resultados.

Las funcionalidades de búsqueda avanzada se implementan a través del parámetro `filter` en la consulta [`productSearch`](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/) utilizando operadores específicos:

- **Búsqueda por niveles** - Buscar en otro contexto de búsqueda - Con esta capacidad, puede realizar hasta dos niveles de búsqueda para sus consultas de búsqueda. Por ejemplo:

   - **Búsqueda de nivel 1** - Busque &quot;motor&quot; en `product_attribute_1`.
   - **Búsqueda de nivel 2** - Busque &quot;número de pieza 123&quot; en `product_attribute_2`. En este ejemplo se busca &quot;número de pieza 123&quot; dentro de los resultados para &quot;motor&quot;.

  La búsqueda por capas está disponible tanto para la indexación de búsqueda `startsWith` como para la indexación de búsqueda `contains` en la segunda capa de la búsqueda por capas, como se describe a continuación:

- **comienza con la indexación de búsqueda** - La búsqueda usa la indexación `startsWith`. Esta nueva capacidad permite:

   - Buscando productos en los que el valor del atributo comience con una cadena especificada.
   - Configuración de una búsqueda &quot;termina con&quot; para que los compradores puedan buscar productos en los que el valor del atributo termine con una cadena en particular. Para habilitar una búsqueda &quot;termina con&quot;, el atributo del producto debe ingerirse a la inversa y la llamada de API también debe ser una cadena invertida. Por ejemplo, si desea buscar un nombre de producto que termine con &quot;pantalones&quot;, debe enviarlo como &quot;stnap&quot;.

- **contiene indización de búsqueda** - La búsqueda de un atributo mediante contiene indización. Esta nueva capacidad permite:

   - Búsqueda de una consulta dentro de una cadena más grande. Por ejemplo, si un comprador busca el número de producto PE-123 en la cadena HAPE-123.

      - Nota: este tipo de búsqueda es diferente de la búsqueda de frases [existente](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#phrase), que realiza una búsqueda de autocompletar. Por ejemplo, si el valor de atributo del producto es &quot;pantalones de exterior&quot;, una búsqueda de frase devuelve una respuesta para &quot;sin bandeja&quot;, pero no devuelve una respuesta para &quot;u hormigas&quot;. Sin embargo, una búsqueda contiene sí devuelve una respuesta para &quot;o hormigas&quot;.

Estas nuevas condiciones mejoran el mecanismo de filtrado de consultas de búsqueda para restringir los resultados de búsqueda. Estas nuevas condiciones no afectan a la consulta de búsqueda principal.

#### Implementación

1. En el Administrador, [establezca un atributo de producto](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/product-attributes-add#step-5-describe-the-storefront-properties) en el que se puedan realizar búsquedas.

   Consulte la lista de [atributos](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/product-attributes/attributes-input-types) en los que se pueden realizar búsquedas.

1. Especifique la capacidad de búsqueda para ese atributo, como **Contiene** (predeterminado) o **Comienza con**. Puede especificar un máximo de seis atributos que se habilitarán para **Contiene** y seis atributos que se habilitarán para **Comienza con**. Además, para la indexación **Contiene**, la longitud de la cadena está limitada a 50 caracteres o menos.

   ![Especificar la capacidad de búsqueda](./assets/search-filters-admin.png)

1. Consulte la [documentación para desarrolladores](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#filtering-using-search-capability) para ver ejemplos de cómo actualizar las llamadas a la API [!DNL Live Search] con las nuevas funciones de búsqueda `contains` y `startsWith`.

   Puede implementar estas nuevas condiciones en la página de resultados de búsqueda. Por ejemplo, puede agregar una nueva sección en la página donde el comprador pueda restringir aún más los resultados de búsqueda. Puede permitir que los compradores seleccionen atributos de producto específicos, como Fabricante, Número de pieza y Descripción. Desde allí, buscan dentro de esos atributos utilizando las condiciones `contains` o `startsWith`.

### Cuándo utilizar la búsqueda por capas en lugar de las facetas

La búsqueda por capas y las facetas sirven para diferentes propósitos en la detección de productos y la elección entre ellos depende de su caso de uso específico:

**Usar búsqueda por niveles cuando:**

- Debe buscar en los resultados de búsqueda utilizando varios criterios.
- Trabajar con números de pieza, SKU o especificaciones técnicas cuando los usuarios conocen información parcial.
- Los compradores deben reducir los resultados paso a paso con criterios anidados.
- Desea reducir el número de llamadas a la API combinando varios criterios de búsqueda en una sola consulta.
- Debe implementar patrones de búsqueda específicos de la empresa que vayan más allá de la navegación con facetas estándar.

**Usar facetas cuando:**

- Proporcionar filtrado típico de categoría, precio, marca y atributo
- Ofrecer opciones de filtro intuitivas que los usuarios pueden comprender y seleccionar fácilmente
- Mostrando opciones disponibles según los resultados de búsqueda actuales
- Visualización de recuentos e intervalos de filtros que ayudan a los usuarios a comprender las opciones disponibles
- Trabajo con características comunes del producto, como el color, el tamaño, el material, etc.

**Práctica recomendada:** Utilice la búsqueda por niveles para búsquedas técnicas y complejas en las que los usuarios tengan criterios específicos y utilice facetas para el filtrado estándar de comercio electrónico en las que los usuarios deseen explorar y reducir las opciones visualmente.

## Facetas y sinónimos

Las facetas y los sinónimos son otra manera de mejorar la experiencia de búsqueda de sus compradores.

[Las facetas](facets.md) son atributos de producto definidos en [!DNL Live Search] para poder filtrarlos. Puede establecer cualquier atributo que se pueda filtrar como faceta en [!DNL Live Search], pero existen [límites](boundaries-limits.md) para la cantidad de facetas que puede buscar al mismo tiempo.

>[!NOTE]
>
>Un atributo de producto sólo se puede filtrar si la configuración del atributo de producto tiene las propiedades requeridas: *Usar en la búsqueda = Sí*, *Usar en la navegación por capas de resultados de búsqueda=sí* y *Usar en la navegación por capas=Filtrable (con resultados)*. Si faltan estas propiedades o no se han configurado correctamente, el atributo no estará visible en la configuración de faceta. Para obtener instrucciones de configuración, consulte [Agregar una faceta](facets-add.md#add-a-facet).

[Sinónimos](synonyms.md) son términos que puede definir para ayudar a guiar a los usuarios hacia el producto correcto. Los usuarios que buscan pantalones pueden escribir &quot;pantalones&quot; o &quot;pantalones&quot;. Puede establecer sinónimos para que estos términos de búsqueda lleven a los usuarios a los resultados de &quot;pantalones&quot;.

## Ajustes de configuración de Commerce

En la siguiente sección se describen las opciones de configuración de Commerce admitidas y no admitidas para [!DNL Live Search].

### Valores de configuración admitidos

>[!IMPORTANT]
>
>Se recomienda encarecidamente utilizar las utilidades de lista de productos, habilitadas de forma predeterminada en Live Search 4.0.0. Los widgets están destinados a reemplazar por completo la implementación del adaptador en futuras versiones. Consulte [habilitar widgets de lista de productos](install.md#enable-product-listing-widgets) para obtener más información.

| Ajuste de configuración de Commerce | Descripción | Compatible con Popover | Admitido por el adaptador |
|---|---|---|---|
| Tiendas > Configuración > Catálogo > Buscar en el catálogo > Permitir todos los productos por página | Si se establece en `Yes`, incluye la opción `ALL` en el control &quot;Mostrar por página&quot;. | Sí. Máx. 500 productos | Sí. Máx. 500 productos |
| Tiendas > Configuración > Catálogo > Buscar en el catálogo > Longitud mínima de la consulta | Número mínimo de caracteres permitidos en una búsqueda en el catálogo. | Sí | Sí |
| Tiendas > Configuración > Catálogo > Buscar en el catálogo > Productos por página en la cuadrícula Valores permitidos | Determina el número de productos mostrados en la vista de cuadrícula. | Sí | Sí |
| Tiendas > Configuración > Catálogo > Buscar en el catálogo > Productos por página en el valor predeterminado de la cuadrícula | Determina el número de productos mostrados por página de forma predeterminada en la vista de cuadrícula. | Sí. Máx. 500 productos | Sí. Máx. 500 productos |
| Tiendas > Configuración > Catálogo > Inventario > Mostrar productos sin existencias | Muestra los productos sin existencias. | Sí | Sí |
| Tiendas > Configuración > Moneda > Moneda de visualización predeterminada | La divisa principal utilizada para mostrar los precios. | Sí | Sí |
| Tiendas > Configuración > General > Configuración de Divisa > Opciones de Divisa > Divisa Base | La divisa principal utilizada para todas las transacciones de pago en línea. | Sí | Sí |

Los precios de la página Widget de Lista de Productos y de la ventana emergente se convierten a la moneda para mostrar predeterminada mediante las tasas de cambio configuradas.

### Valores de configuración no admitidos

| Ajuste de configuración de Commerce | Descripción | Notas |
|---|---|---|
| Tiendas > Configuración > Catálogo > Tienda > Modo de lista | Determina el formato de la lista de resultados de búsqueda. | Se representa correctamente, pero los eventos no se envían para algunas interacciones de página |
| Tiendas > Configuración > Catálogo > Buscar en el catálogo > Longitud máxima de la consulta | Número máximo de caracteres permitidos en una búsqueda en el catálogo. | No implementado; los servicios de búsqueda aceptan hasta 255 caracteres |
| Configuración > Ventas > Impuestos > Configuración De Visualización De Precios > Mostrar Precios De Productos En El Catálogo | Determina si los precios de productos publicados en el catálogo incluyen o excluyen impuestos, o muestran dos versiones del precio; una con y otra sin impuestos |  |
| Tiendas > Configuración > Catálogo > Tienda > Lista de productos Ordenar por | Determina el criterio de ordenación de la lista de resultados de búsqueda. | No se aplica al [!DNL Live Search] [widget de página de lista de productos](plp-styling.md) |

## Valores de atributo predeterminados

Los atributos de producto siguientes tienen [propiedades de tienda](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/product-attributes.html) que usa [!DNL Live Search] y que están habilitadas de manera predeterminada.

| Propiedad | Propiedad Storefront | Atributo |
|---|---|---|
| Ordenable | Se utiliza para ordenar en la lista de productos | `price` |
| Buscable | Uso en la búsqueda | `price` <br />`sku`<br />`name` |
| FilterableInSearch | Uso en la navegación por capas: filtrable (con resultados) | `price`<br />`visibility`<br />`category_name` |

## Propiedades de atributo predeterminadas que no son del sistema

En la tabla siguiente se muestran las propiedades de búsqueda y filtrado predeterminadas de los atributos que no son del sistema, incluidos los que son específicos de los datos de ejemplo de Luma. Al establecer la propiedad del atributo *Use in Search* en `Yes`, se permite la búsqueda en el atributo tanto en [!DNL Live Search] como en Adobe Commerce nativo.

| Código de atributo | Buscable | Uso en la navegación por capas |
|--- |--- |--- |
| actividad | Sí | Filtrable (con resultados) |
| attributes_brand | Sí | No |
| marca | Sí | No |
| clima | Sí | Filtrable (con resultados) |
| collar | Sí | Filtrable (con resultados) |
| color | Sí | Filtrable (con resultados) |
| coste | Sí | No |
| eco_collection | Sí | Filtrable (con resultados) |
| género | Sí | Filtrable (con resultados) |
| fabricante | Sí | Filtrable (con resultados) |
| material | Sí | Filtrable (con resultados) |
| propósito | Sí | Filtrable (con resultados) |
| strap_bags | Sí | Filtrable (con resultados) |
| style_general | Sí | Filtrable (con resultados) |

## Propiedades predeterminadas de atributos del sistema

En la tabla siguiente se muestran la búsqueda predeterminada y las propiedades filtrables de los atributos del sistema.

| Código de atributo | Buscable | Uso en la navegación por capas |
|--- |--- |--- |
| allow_open_amount | Sí | Filtrable (con resultados) |
| description | Sí | No |
| name | Sí | No |
| precio | Sí | Filtrable (con resultados) |
| short_description | Sí | No |
| sku | Sí | No |
| status | Sí | No |
| tax_class_id | Sí | No |
| url_key | Sí | No |
| peso | Sí | No |
