---
title: '[!DNL Retrieve catalog data with GraphQL]'
description: Utilice consultas de GraphQL para recuperar los datos del catálogo y potenciar las experiencias de Commerce.
role: Admin, Developer
feature: Services, API Mesh, Catalog Service
exl-id: 49bbdb3b-bbe9-4777-8ea7-3bd25ae53889
source-git-commit: ff5c717dbdd638e114bccc3f6dec26f4be269194
workflow-type: tm+mt
source-wordcount: '216'
ht-degree: 0%

---

# Recuperación de datos de catálogo con GraphQL {#graphql-queries}

Utilice las consultas de GraphQL para recuperar datos de producto, precio y de otro tipo del espacio de datos SaaS del catálogo de Adobe Commerce y utilícelos para procesar experiencias de Commerce más rápidamente que las consultas nativas de GraphQL de Adobe Commerce.

El servicio de catálogo ofrece las siguientes consultas:

| Consulta | Descripción | Uso |
|-------|-------------|-------|
| `categories` | Devuelve datos de categoría. Si se especifica el objeto de entrada del subárbol, la consulta devuelve detalles sobre las subcategorías. | Útil para procesar páginas de categoría y navegación de tiendas. [Ver ejemplo.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) |
| `products` | Devuelve detalles acerca de los SKU especificados como entrada. | Se utiliza principalmente para procesar contenido en páginas de detalles y comparaciones de productos. [Ver ejemplo.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/categories/) |
| `productSearch` | Devuelve una lista de productos que coinciden con los criterios de búsqueda. | Útil para procesar resultados de búsqueda y páginas de lista de productos basadas en la entrada de búsqueda. [Ver ejemplo.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/) |
| `refineProduct` | Restringe los resultados de una consulta de productos que se ejecuta con un producto complejo para devolver información específica acerca de una variante de producto. | Útil para procesar páginas de detalles de productos actualizadas cuando los compradores seleccionan una opción de producto. [Ver ejemplo.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/refine-product/) |
| `variants` | Devuelve detalles sobre todas las variaciones de un producto. | Útil para mostrar imágenes de variante en páginas de detalles o listas de productos sin enviar varias solicitudes de API. [Ver ejemplo.](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/product-variants/) |

Consulte la [Guía de API de servicio de catálogo](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/) para obtener más información sobre el uso de estas consultas
