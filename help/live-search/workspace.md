---
title: Configuración de Live Search
description: El área de trabajo  [!DNL Live Search] se usa para configurar, administrar y supervisar el rendimiento de la búsqueda.
exl-id: 07c32b26-3fa4-4fae-afba-8a10866857c3
source-git-commit: 1548b7e11249febc2cd8682581616619f80c052f
workflow-type: tm+mt
source-wordcount: '1013'
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

   ![Workspace](assets/attribute-searchable.png)

[!DNL Live Search] también respeta el [peso](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search-results.html#weighted-search) de un atributo de producto, tal como se establece en Adobe Commerce. Los atributos con un peso mayor aparecerán más arriba en los resultados de búsqueda.

Siempre se pueden buscar los atributos siguientes:

- `sku`
- `name`
- `categories`

[Las facetas](facets.md) son atributos de producto definidos en [!DNL Live Search] para poder filtrarlos. Puede establecer cualquier atributo que se pueda filtrar como faceta en [!DNL Live Search], pero existen [límites](boundaries-limits.md) para la cantidad de facetas que puede buscar al mismo tiempo.

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

### Términos de búsqueda

[!DNL Live Search] admite [redirecciones de términos de búsqueda](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search-terms.html) en implementaciones en las que Adobe Commerce administra el enrutamiento, como en Luma y otros temas basados en php.
