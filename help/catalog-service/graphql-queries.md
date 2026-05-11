---
title: '[!DNL Retrieve catalog data with GraphQL]'
description: Utilice consultas de GraphQL para recuperar los datos del catálogo y potenciar las experiencias de Commerce.
role: Admin, Developer
feature: Services, API Mesh, Catalog Service
exl-id: 49bbdb3b-bbe9-4777-8ea7-3bd25ae53889
TQID: https://experienceleague.adobe.com/ahutwotbB6Dxg7Tc3WMFd7S-WBMALvOYIUTmB5JKmyM
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 268
ht-degree: 0%

---

# Recuperación de datos de catálogo con GraphQL {#graphql-queries}

Utilice las consultas de GraphQL para recuperar datos de producto, precio y de otro tipo del espacio de datos SaaS del catálogo de Adobe Commerce y utilícelos para procesar experiencias de Commerce más rápidamente que las consultas nativas de GraphQL de Adobe Commerce.

{{aco-merchandising-services}}

El servicio de catálogo ofrece las siguientes consultas:

| Consulta | Descripción | Uso |
|-------|-------------|-------|
| `categories` | Devuelve datos de categoría. Si se especifica el objeto de entrada del subárbol, la consulta devuelve detalles sobre las subcategorías. | Útil para procesar páginas de categoría y navegación de tiendas. [Ver ejemplo.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) |
| `products` | Devuelve detalles acerca de los SKU especificados como entrada. | Se utiliza principalmente para procesar contenido en páginas de detalles y comparaciones de productos. [Ver ejemplo.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) |
| `productSearch` | Devuelve una lista de productos que coinciden con los criterios de búsqueda. | Útil para procesar resultados de búsqueda y páginas de lista de productos basadas en la entrada de búsqueda. [Ver ejemplo.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/) |
| `refineProduct` | Restringe los resultados de una consulta de productos que se ejecuta con un producto complejo para devolver información específica acerca de una variante de producto. | Útil para procesar páginas de detalles de productos actualizadas cuando los compradores seleccionan una opción de producto. [Ver ejemplo.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/) |
| `variants` | Devuelve detalles sobre todas las variaciones de un producto. | Útil para mostrar imágenes de variante en páginas de detalles o listas de productos sin enviar varias solicitudes de API. [Ver ejemplo.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/product-variants/) |

Consulte [Storefront Services GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/) para obtener más información sobre el uso de estas consultas.
