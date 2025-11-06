---
title: Límites y límites
description: Conozca los límites y limitaciones de [!DNL Live Search] para asegurarse de que cumple con las necesidades de su empresa.
role: Admin, Developer
exl-id: 28b8d98f-0784-4c4d-b382-81c01838e0de
source-git-commit: 935bc5867db5fb7664068f0e2b01158d87a5d824
workflow-type: tm+mt
source-wordcount: '1188'
ht-degree: 0%

---

# Límites y límites

Cuando se trata de buscar sitios, Adobe Commerce le da opciones. Revise los límites y limitaciones siguientes para asegurarse de que [!DNL Live Search] y [!DNL Catalog Service] satisfacen las necesidades de su empresa. Si necesita funcionalidades de búsqueda avanzadas como búsqueda de contenido, traer su propio algoritmo (BYOA) o comercialización basada en atributos, considere una solución de búsqueda de terceros.

## General

- El módulo [Búsqueda avanzada](https://experienceleague.adobe.com/es/docs/commerce-admin/catalog/catalog/search/search) se deshabilita al instalar [!DNL Live Search] y se quita el vínculo Búsqueda avanzada del pie de página de la tienda.
- El campo [&#x200B; y el widget de página de lista de productos no admiten &#x200B;](https://experienceleague.adobe.com/es/docs/commerce-admin/catalog/products/pricing/product-price-tier)precios de nivel[!DNL Live Search].
- Los precios de los productos incluyen el impuesto sobre el valor agregado (IVA), pero [!DNL Live Search] no puede mostrar el IVA como un valor separado.
- No se admite la búsqueda de contenido (páginas y bloques de CMS).
- El número máximo de resultados que se pueden paginar es 10 000. Para garantizar que los compradores no tengan que utilizar la paginación profunda cuando una categoría o resultado de búsqueda incluya un gran número de productos, proporcione formas significativas de filtrar los productos.
- Hay un límite estricto de 1 MB por atributo, incluida la descripción y los atributos personalizados.
- El adaptador de búsqueda no admite atributos de producto creados con un modelo de origen personalizado y utilizados como facetas. Para admitir esta funcionalidad, debe usar el [Widget de la página de lista de productos](plp-styling.md).
- El adaptador de búsqueda quedará obsoleto a partir de Live Search 4.0.0.
- No se admiten los tipos de producto personalizados.
- No se admiten los atributos personalizados creados mediante programación con `"is_user_defined": false`.
- Puede filtrar los resultados usando las condiciones &quot;comienza con&quot; o &quot;contiene&quot; con algunas limitaciones como se describe en [documentación para desarrolladores](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/#limitations).
- Solo puede realizar el seguimiento de las métricas de rendimiento durante el último año.
- Si una consulta de búsqueda contiene varias palabras, el espacio en blanco entre las palabras hace que se traten como términos de búsqueda independientes. Use [sinónimos](./synonyms.md) si quiere dar cuenta de consultas de búsqueda de varias palabras.
- [!DNL Live Search] no admite [redirecciones de términos de búsqueda](https://experienceleague.adobe.com/es/docs/commerce-admin/catalog/catalog/search/search-terms) de forma nativa. Implemente redirecciones mediante Fastly u otra configuración personalizada.

## Indexación

- [!DNL Live Search] [índices](indexing.md) hasta un total de 450 atributos de producto por vista de tienda. Se distribuyen de la siguiente manera:
   - 50 atributos que se pueden ordenar
   - 200 atributos filtrables
   - 200 atributos en los que se puede buscar
- [!DNL Live Search] solo indexa productos de la base de datos de Adobe Commerce.
- Las páginas de CMS no están indexadas.
- Los atributos SKU, nombre y categoría se pueden buscar de forma predeterminada y no se pueden excluir de la búsqueda. Asegúrese de anular la asignación de los productos de las categorías si no están pensados para estar en esas categorías.

## Facetas

- Desde el conjunto de atributos filtrables definidos, puede configurar hasta 100 atributos como facetas.
- Dentro de una faceta, se puede devolver un máximo de 100 contenedores. Si necesita devolver más de 100 contenedores, [cree un vale de soporte técnico](https://experienceleague.adobe.com/es/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide) para que Adobe pueda analizar el impacto en el rendimiento y determinar si es factible aumentar este límite para su entorno.
- Las facetas dinámicas pueden causar problemas de rendimiento en índices grandes e índices con una alta ordinalidad. Si ha creado facetas dinámicas y observa algún deterioro del rendimiento o si la página no se carga con errores de tiempo de espera, intente cambiar las facetas a ancladas para determinar si esto resuelve el problema de rendimiento.
- El estado de las existencias (`quantity_and_stock_status`) no se admite como faceta. Puede usar `inStock: 'true'` para filtrar productos sin existencias. Esto se admite de forma predeterminada en el módulo `LiveSearchAdapter` cuando &quot;Mostrar productos sin existencias&quot; está establecido en &quot;Verdadero&quot; en el administrador [!DNL Commerce].
- Los atributos de tipo de fecha no se admiten como faceta.
- Los cambios realizados en los metadatos del atributo después de añadir dicho atributo como faceta no se reflejarán en la faceta.
- Puede tener hasta 50 atributos que se pueden ordenar y 200 atributos que se pueden buscar.

## Consulta

- [!DNL Live Search] usa un único [extremo de GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/) para que las consultas admitan características como facetas dinámicas y búsqueda mientras escribe. Aunque es similar a la [API de GraphQL](https://developer.adobe.com/commerce/webapi/graphql/), existen algunas diferencias y algunos campos pueden no ser totalmente compatibles.
- El número máximo de resultados que se pueden devolver en una consulta de búsqueda es 10 000.
- El número máximo de resultados por página es de 500.
- No es posible filtrar los resultados mediante un atributo de tipo de fecha.

## Buscar en comercialización

- El número máximo de [reglas](rules.md) de comercialización de búsqueda por vista de tienda es 50.
- El número máximo de condiciones por regla es 10.
- El número máximo de eventos por regla es 25.
- Las reglas y los productos clasificados manualmente se aplican a los resultados de búsqueda cuando se selecciona el orden predeterminado, &quot;Ordenar por: Más relevante&quot;. Si un comprador cambia el criterio de ordenación a algo como ordenar por nombre o precio, las reglas y las clasificaciones manuales ya no están en vigor.
- Para evitar resultados impredecibles en respuestas paginadas, el número de productos anclados no debe superar el tamaño de página solicitado.

## Sinónimos

- [!DNL Live Search] puede administrar hasta 200 [sinónimos](synonyms.md) por vista de tienda.

## Comercialización por categorías

- Puede crear una regla por categoría para cada vista de tienda.
- El número máximo de condiciones por regla es 10.
- El número máximo de eventos por regla es 25.
- Las reglas se aplican cuando se abre una categoría específica en la tienda y existe una regla para esa categoría. Para las reglas de comercialización por categorías, el criterio de ordenación predeterminado es &quot;Ordenar por: Posición&quot;. Si un comprador cambia el orden, todos los productos ocultos, anclados y enterrados ya no se ordenarán.

## Permisos B2B y de categoría

- Los productos no se muestran si no se añaden a un catálogo compartido predeterminado.
- Para restringir grupos de clientes que usen [permisos de categoría](https://experienceleague.adobe.com/es/docs/commerce-admin/catalog/categories/category-permissions):
   - Los productos deben asignarse a la categoría raíz. (**Nota:** Puede eliminar esta limitación actualizando la extensión de exportación de datos SaaS a la versión 103.4.0+. Ver [Administrar la extensión de exportación de datos](../data-export/manage-extension.md).
   - El grupo de clientes &quot;Sin sesión iniciada&quot; debe tener permisos de navegación &quot;Permitir&quot;.
   - Para restringir productos al grupo de clientes &quot;No se inició sesión&quot;, vaya a cada categoría y establezca permisos para cada [grupo de clientes](https://experienceleague.adobe.com/es/docs/commerce-admin/b2b/shared-catalogs/catalog-shared-manage).
- En este momento no se admite la compatibilidad predeterminada con B2B con el widget PLP en PWA Studio. Sin embargo, puede [usar la API](install.md#pwa-support) para implementar esta funcionalidad.
- Las facetas de categoría de [!DNL Live Search] pueden mostrar categorías que no se pueden mostrar a un [grupo de clientes](https://experienceleague.adobe.com/es/docs/commerce-admin/b2b/shared-catalogs/catalog-shared-manage) específico.
- [!DNL Live Search] admite hasta 1000 grupos de clientes.

## [!DNL Storefront popover]

- [[!DNL popover]](storefront-popover.md) solo está disponible para tiendas que usen el tema *Luma* o un tema personalizado basado en *Luma*. Las rutas de exploración de la página de resultados de búsqueda no tendrán el estilo *Luma*.
- [!DNL popover] no admite el tema *En blanco*.
- [!DNL popover] no es compatible con el formulario de pedido rápido.
- No se admiten listas de deseos ni comparaciones de productos.
- El símbolo de moneda para el sol peruano (PEN) no es compatible.

## Resolución de problemas

Para obtener ayuda con la solución de problemas comunes de [!DNL Live Search], vea los siguientes artículos de la base de conocimiento:

- [[!DNL Live Search] catálogo no sincronizado](https://experienceleague.adobe.com/es/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-catalog-data-sync): proporciona soluciones para los casos en los que los datos del catálogo de productos no se sincronizan correctamente entre la tienda Adobe Commerce y el servicio Live Search. Este artículo explica cómo comprobar el estado de sincronización, identificar errores de sincronización y resolver problemas de sincronización de datos.
- [[!DNL Live Search] La clasificación del tablero y los resultados de búsqueda es incorrecta](https://experienceleague.adobe.com/es/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-dashboard-ranking-incorrect): soluciona problemas en los que los resultados de búsqueda o las métricas de rendimiento mostrados en el tablero de Live Search no se muestran según lo esperado. Este artículo explica cómo solucionar discrepancias de clasificación e incoherencias en los datos del panel.
- [[!DNL Live Search] las facetas no están ordenadas alfabéticamente](https://experienceleague.adobe.com/es/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/live-search-facets-not-sorted). Resuelve el problema de que los valores de faceta aparezcan en un orden inesperado en lugar de hacerlo alfabéticamente. Este artículo proporciona los pasos para configurar y corregir el comportamiento de ordenación de facetas en la tienda.

Si necesita ayuda adicional, comuníquese con [soporte técnico](https://experienceleague.adobe.com/es/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide).
