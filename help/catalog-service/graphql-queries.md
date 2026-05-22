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
source-git-commit: d842311424e76b83a131ada7a2db6e3fb868acd8
workflow-type: tm+mt
source-wordcount: 269
ht-degree: 0%

---

# Recuperación de datos de catálogo con GraphQL {#graphql-queries}

Use consultas de GraphQL para recuperar datos de productos, precios y otros catálogos del espacio de datos [!DNL Catalog Service] y procesar experiencias de tienda [!DNL Adobe Commerce] más rápido que las consultas de productos nativas.

{{aco-merchandising-services}}

[!DNL Catalog Service] proporciona las siguientes consultas:

| Consulta | Descripción | Uso | Límites |
| --- | --- | --- | --- |
| `categories` | Devuelve datos de categoría. Si se especifica el objeto de entrada `subtree`, la consulta devuelve detalles sobre las subcategorías. | Útil para procesar páginas de categoría y navegación de tiendas. [Ver ejemplo.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/){target="_blank"} | — |
| `products` | Devuelve detalles acerca de los SKU especificados como entrada. | Se utiliza principalmente para procesar contenido en páginas de detalles y comparaciones de productos. [Ver ejemplo.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/){target="_blank"} | 100 SKU por solicitud |
| `productSearch` | Devuelve una lista de productos que coinciden con los criterios de búsqueda. | Útil para procesar resultados de búsqueda y páginas de lista de productos basadas en la entrada de búsqueda. [Ver ejemplo.](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/){target="_blank"} | 100 SKU por solicitud |
| `refineProduct` | Reduce los resultados de la consulta `products` de un producto complejo para devolver información específica acerca de una variante de producto. | Útil para procesar páginas de detalles de productos actualizadas cuando los compradores seleccionan una opción de producto. [Ver ejemplo.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/){target="_blank"} | 100 SKU por solicitud |
| `variants` | Devuelve detalles sobre todas las variaciones de un producto. | Útil para mostrar imágenes de variante en páginas de detalles o listas de productos sin enviar varias solicitudes de API. [Ver ejemplo.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/product-variants/){target="_blank"} | 100 SKU por solicitud |

{style="table-layout:auto"}

Consulte [Storefront Services GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/){target="_blank"} para obtener más información sobre el uso de estas consultas.
