---
title: Límites y límites
description: Conozca los límites y limitaciones de [!DNL Product Recommendations] para asegurarse de que cumple con las necesidades de su empresa.
role: Admin, Developer
source-git-commit: 66830c9d950a27269aca1bda0dcc7d0d86f05647
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 0%

---

# Límites y límites

Revise los límites y limitaciones siguientes para asegurarse de que [!DNL Product Recommendations] cumple con las necesidades de su empresa. Comprender estas restricciones le ayuda a planificar la implementación, configurar filtros y evitar problemas comunes.

## General

- **Tipos de productos** - Los tipos de productos admitidos son _simples_, _configurables_, _virtuales_, _descargables_ y _tarjetas regalo_. No se admiten los tipos de producto _Paquete_, _agrupado_ y personalizado. Si el catálogo contiene un gran número de tipos de productos no compatibles, recibirá una baja [puntuación de preparación](create.md#readiness-indicators). Ver [Filtrar por tipo de producto](filters.md#type).
- **SKU con espacios**: las SKU que contienen espacios pueden reducir la relevancia de las recomendaciones y se deben evitar cuando sea posible.
- **Página del carro de compras**: las recomendaciones de productos no se admiten en la página del carro de compras cuando la tienda está configurada para [mostrar la página del carro de compras inmediatamente después de agregar un producto al carro de compras](https://experienceleague.adobe.com/es/docs/commerce-admin/stores-sales/point-of-purchase/cart/cart-configuration). Ver [Crear recomendaciones](create.md).
- **Productos secundarios**: los productos secundarios de un producto configurable (visibilidad _No visible de forma individual_) no se muestran en una unidad de recomendación. Solo puede aparecer el producto configurable (principal). Ver [Filtrar productos](filters.md#product).
- **Productos deshabilitados o no visibles**: los productos deshabilitados o no visibles individualmente nunca aparecerán en las recomendaciones y no se podrán seleccionar en los filtros de productos.
- **Precios especiales** - [Los precios especiales](https://experienceleague.adobe.com/es/docs/commerce-admin/catalog/products/pricing/product-price-special) con fechas de inicio y finalización no son compatibles con las unidades de recomendación. Un producto con un precio especial puede aparecer en las recomendaciones, pero la unidad no muestra el precio especial, la fecha de inicio ni la fecha de finalización. Los compradores ven el precio normal (u otros datos de precios proporcionados por su catálogo/fuente de precios) hasta que abren la página del producto.

## Unidades de recomendación

- **Unidades activas por tipo de página**: puede crear hasta 50 unidades de recomendación activas para cada tipo de página (inicio, categoría, detalle del producto, carro de compras, confirmación). El tipo de página aparece atenuado en el flujo de creación cuando se alcanza el límite.
- **Productos por unidad**: el número de productos mostrados en una unidad de recomendación puede establecerse de 5 (predeterminado) a un máximo de 20.
- **Estado de borrador**: después de guardar una recomendación como borrador, no puede modificar el tipo de página o el tipo de recomendación de esa unidad. Otros ajustes se pueden editar antes de la activación.

## Filtros y condiciones

- **Condiciones dinámicas**: las condiciones dinámicas (como &quot;productos de la misma categoría que el producto actual&quot; o &quot;intervalo de precios relativo&quot;) están disponibles en todos los tipos de página excepto en la página de inicio. Tampoco están disponibles en páginas donde se colocan recomendaciones con Page Builder. Consulte [Condiciones](filters.md#conditions).

## Entornos de previsualización y sin producción

- **Vista previa vista recientemente** - El tipo de recomendación _Vista recientemente_ no se puede previsualizar en el administrador porque los datos están basados en el historial del explorador y no están disponibles en el contexto del administrador. Ver [recomendaciones de vista previa](create.md#preview).
- **Recomendaciones de otro espacio de datos**: cuando [recupere recomendaciones de un espacio de datos de SaaS diferente](settings.md) (por ejemplo, producción) en una tienda que no sea de producción, podrá ver las recomendaciones, pero no podrá hacer clic en las páginas de producto desde ellas. Esto es por diseño para previsualización y pruebas.
- **GraphQL y espacio de datos alternativo**: al usar Product Recommendations a través de [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/product-recommendations/queries/recommendations/), el parámetro `alternateEnvironmentId` (utilizado para recuperar recomendaciones de otro espacio de datos) no está disponible. Utilice la API de REST o la Configuración de administración para cambiar la fuente de recomendaciones en la fase de no producción.

## API y configuración

- **Claves de API (4.x y posteriores)**: debe proporcionar claves de API públicas y privadas para los entornos de zona protegida y producción. Si no proporciona ambos pares de claves API, no puede acceder a la función Recomendaciones de productos en el Administrador. La recopilación de datos de su tienda y las recomendaciones existentes siguen funcionando. Consulte [Instalar y configurar](install-configure.md).

## Restricciones de cookies

- Cuando el [modo de restricción de cookies](setting-cookie.md) está habilitado y los compradores no han aceptado cookies, es posible que algunos tipos de recomendaciones que dependen de datos de comportamiento no se muestren o que muestren resultados limitados.
- Los tipos de recomendación que no dependen de datos de comportamiento (por ejemplo, _Más visitados_, _Similitud visual_) siguen funcionando cuando las restricciones de cookies están habilitadas.
- Cuando las restricciones de cookies están habilitadas, Recomendaciones de productos no recopila ni almacena datos de comportamiento en cookies ni almacenamiento local hasta que el comprador da su consentimiento.

## Page Builder

- **Métricas y vistas de tienda**: las métricas de las unidades de recomendación de Page Builder solo aparecen en la vista de tienda predeterminada del área de trabajo Recomendaciones de productos. Para ver las métricas de recomendación de Page Builder en una vista de tienda no predeterminada, debe abrir y [editar](edit.md) la unidad de recomendación de Page Builder en esa vista de tienda y guardarla; las métricas aparecerán en esa vista de tienda. Consulte [Integración de Page Builder](page-builder.md).

## B2B

- Product Recommendations respeta [los permisos de categoría](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/categories/category-permissions.html), [los catálogos compartidos](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/shared-catalogs/catalog-shared.html) y los precios específicos de grupos de clientes. Los compradores solo ven recomendaciones de productos a los que pueden acceder según su asignación de segmento y catálogo. Consulte [Incorporación](onboarding.md).

## Datos y preparación

- **Datos de comportamiento**: muchos tipos de recomendación requieren suficientes datos de comportamiento de tienda (vistas, complementos al carro, compras). Las tiendas nuevas o las tiendas de poco tráfico pueden ver resultados limitados o nulos para estos tipos hasta que se recopilen los datos adecuados. Supervise [indicadores de preparación](create.md#readiness-indicators) en el administrador.
- **Ensayo sin datos de producción**: en un entorno que no es de producción sin datos de comportamiento, el único tipo de recomendación que puede probar sin recuperar de producción es _Más como este_, que solo usa similitud basada en catálogo. Consulte [Entorno de ensayo](staging-environment.md).

## Resolución de problemas

Para obtener ayuda con la sincronización del catálogo, recomendaciones que no se muestran u otros problemas comunes, busca en [Commerce Knowledge Base](https://experienceleague.adobe.com/es/docs/commerce-knowledge-base/kb/overview) o ponte en contacto con el [servicio de asistencia](https://experienceleague.adobe.com/es/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide).
