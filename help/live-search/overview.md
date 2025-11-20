---
title: ¿Qué es  [!DNL Live Search]?
description: '[!DNL Live Search] de Adobe Commerce ofrece una experiencia de búsqueda rápida, relevante e intuitiva.'
recommendations: noCatalog
exl-id: 15399216-6a96-4d0b-bbc1-293190cb9e14
source-git-commit: f96e7d8d2a31d5e0f49bd3ac2da320313908a868
workflow-type: tm+mt
source-wordcount: '925'
ht-degree: 1%

---

# ¿Qué es [!DNL Live Search]?

[!DNL Live Search] es una característica que reemplaza las funciones de búsqueda estándar de Adobe Commerce. Cuando la característica [!DNL Live Search] está habilitada y configurada, el campo de texto de búsqueda predeterminado se reemplaza por el campo de texto [!DNL Live Search]. [!DNL Live Search] también incluye el widget de página de lista de productos (PLP), que proporciona capacidades de filtrado sólidas al examinar los resultados de búsqueda.

Con [!DNL Live Search], puede:

- Cree experiencias de búsqueda significativas para ayudar a los compradores y compradores a encontrar lo que desean con el menor esfuerzo posible.
- Aproveche el faceteo dinámico con tecnología de IA y la reclasificación de los resultados de búsqueda en respuesta a los comportamientos de los compradores durante la sesión.
- Utilice un servicio ligero basado en SaaS que ofrezca actualizaciones sencillas y esté incluido en su licencia, lo que reduce el coste total de propiedad.
- Obtenga información técnica habilitando la API de GraphQL, la flexibilidad sin encabezado, los entornos de zona protegida de API y el SaaS ultrarrápido.

>[!IMPORTANT]
>
>Cuando se trata de buscar sitios, Adobe Commerce le da opciones. Antes de la implementación, revisa la información de [Límites y límites](boundaries-limits.md) para asegurarte de que [!DNL Live Search] se adapte a tus necesidades comerciales.

## Arquitectura

La parte de Adobe Commerce de la arquitectura incluye alojar la búsqueda *Admin*, sincronizar los datos del catálogo y ejecutar el servicio de consultas. Una vez que [!DNL Live Search] se ha instalado y configurado, Adobe Commerce comienza a compartir datos de búsqueda y catálogo con los servicios SaaS. En este momento, los usuarios administradores pueden configurar, personalizar y administrar las [facetas](facets.md), los [sinónimos](synonyms.md) y las [reglas de comercialización](category-merch.md) de búsqueda.

![Flujo de datos de Live Search](assets/ls-cs-data-flow.png)

## Explicación rápida

Con un enfoque en la velocidad, relevancia y facilidad de uso, [!DNL Live Search] cambia las reglas del juego tanto para los compradores como para los comerciantes. Vea el siguiente vídeo y haga un recorrido rápido por [!DNL Live Search] desde la tienda.

>[!VIDEO](https://video.tv.adobe.com/v/3418797?learn=on)

Para ver un vídeo más detallado sobre cómo usar y configurar Live Search, consulte el tema [Demostración completa sobre [!DNL Live Search]](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/getting-started/capabilities/live-search-full-demonstration).

### Buscar mientras escribe

[!DNL Live Search] responde con productos sugeridos y una imagen en miniatura de los principales resultados de búsqueda en una [ventana emergente](storefront-popover.md) mientras los compradores escriben consultas en el cuadro [Buscar](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/catalog/search/search). La página [detalles del producto](https://experienceleague.adobe.com/en/docs/commerce-admin/start/storefront/storefront) se muestra cuando los compradores hacen clic en un producto sugerido o destacado. Un vínculo _Ver todo_ al pie de página de la ventana emergente muestra la página de resultados de la búsqueda.

[!DNL Live Search] devuelve los resultados de &quot;buscar mientras escribe&quot; para una consulta de dos o más caracteres. Para una coincidencia parcial, el número máximo de caracteres por palabra es 20. El número de caracteres de la consulta no se puede configurar. La ventana emergente incluye los campos `name`, `sku` y `category_ids`.

![Tienda de ejemplo: busca mientras escribes](assets/storefront-search-as-you-type.png)

### Ver todos los resultados de búsqueda

Para enumerar todos los productos devueltos por la consulta &quot;buscar mientras escribe&quot;, haga clic en _Ver todo_ en el pie de página de la ventana emergente.

![Ejemplo de tienda - facetas de precio](assets/storefront-view-all-search-results.png)

### Cómo gestiona [!DNL Live Search] los errores tipográficos

Cuando se realiza una búsqueda, [!DNL Live Search] ejecuta una búsqueda no difusa que no tiene en cuenta los errores tipográficos. Si no se encuentran resultados, [!DNL Live Search] realiza una segunda búsqueda difusa, que tiene en cuenta errores menores. La búsqueda parcial se ejecuta con una distancia de edición máxima de 1. Esta distancia de edición utiliza el concepto de [distancia de Levenshtein](https://en.wikipedia.org/wiki/Levenshtein_distance) y permite realizar tres tipos de operaciones:

| Operación | Descripción | Ejemplo |
|---|---|---|
| Inserción | Agregar un carácter. | &quot;cat&quot; -> &quot;cart&quot; |
| Eliminación | Eliminar un carácter. | &quot;carrito&quot; -> &quot;gato&quot; |
| Sustitución | Reemplazar un carácter por otro. | &quot;cart&quot; -> &quot;cast&quot; |

Además de la lógica de búsqueda difusa, también se contabilizan las transposiciones, es decir, cuando se intercambian dos caracteres adyacentes en una palabra, por ejemplo, &quot;el&quot; en lugar de &quot;el&quot;. Tenga en cuenta que estos límites de edición son por palabra y no por la frase en su conjunto.

### Búsqueda filtrada con facetas

La búsqueda filtrada usa varias dimensiones de valores de atributo o [facetas](facets.md) como criterios de búsqueda. La selección de filtros la define el comerciante y cambia según los productos devueltos, con las facetas más utilizadas ancladas en la parte superior de la lista.

Use facetas como parámetros de URL:`http://yourwebsite.com?color=red` y Live Search filtra los resultados en función de estos valores de atributo.

### Sinónimos

[Sinónimos](synonyms.md) amplían el alcance y acentúan el enfoque de las consultas al incluir palabras que los compradores podrían usar y que difieren de las del catálogo. Puede ajustar el diccionario de sinónimos para mantener a los compradores comprometidos y en el camino de compra.

### Reglas de comercialización

Las [reglas](rules.md) de comercialización dan forma a la experiencia de compra con instrucciones if-then que agregan lógica y eventos para la búsqueda. Puede impulsar o enterrar fácilmente productos para una promoción, una temporada u otro período de tiempo.

## Componentes de Live Search

- [!DNL Live Search] [widget de ventana emergente](storefront-popover.md) es el cuadro que se abre debajo del campo de búsqueda que contiene los resultados de la búsqueda.
- [El widget de página de lista de productos](plp-styling.md) (PLP) proporciona una página de lista de productos en la que se pueden buscar con soporte para facetas y sinónimos. El widget se instala y habilita en Live Search 4.0.0+ y reemplaza al adaptador de búsqueda.
- (**Obsoleto**) El adaptador de búsqueda era el precursor del widget PLP y se instaló con Live Search &lt; 4.0.0. Si utiliza una versión de Live Search anterior a la 4.0.0, Commerce recomienda actualizar para recibir las ventajas de las funciones del widget PLP y las mejoras futuras. En adelante, el adaptador de búsqueda solo se actualizará para abordar los problemas de seguridad.

## [!DNL Live Search] espacio de trabajo

El [!DNL Live Search] [espacio de trabajo](workspace.md) es el área del administrador donde se configuran las características de [!DNL Live Search], como sinónimos, facetas y comercialización de categorías.

## Eventos

[!DNL Live Search] usa [events](https://developer.adobe.com/commerce/services/shared-services/storefront-events/#live-search) para calcular los paneles de [comercialización inteligente](category-merch.md) y [rendimiento](performance.md). Los eventos se proporcionan con implementaciones predeterminadas. Los eventos para tiendas sin encabezado deben habilitarse manualmente.

## Política de retención de datos del catálogo

Si no envía una consulta de búsqueda de los datos del catálogo en el entorno de prueba durante 90 días consecutivos, los datos del catálogo se establecen en modo de hibernación y no se devuelve ningún dato para ninguna consulta de búsqueda. Esta directiva no afecta a los datos de catálogo del entorno de producción.

Para reactivar los datos del catálogo en su entorno de prueba, [envíe una solicitud de soporte técnico](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#experience-league-start-page) con el título: &quot;Reactivar [!DNL Live Search]&quot; e incluya los identificadores de entorno. Los datos del catálogo en el entorno de prueba deben restaurarse en un par de horas.
