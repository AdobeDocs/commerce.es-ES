---
title: GraphQL
description: El espacio de trabajo  [!DNL Live Search] GraphQL le permite generar consultas con sus datos activos.
exl-id: d32edf42-1fb0-40f9-89e5-798b39521b77
source-git-commit: ff5c717dbdd638e114bccc3f6dec26f4be269194
workflow-type: tm+mt
source-wordcount: '39'
ht-degree: 0%

---

# GraphQL

El área de trabajo *GraphQL* permite a los administradores crear y probar consultas de GraphQL con sus propios datos.

Este área de trabajo admite las consultas [`productSearch`](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/product-search/) y [`attributeMetadata`](https://developer.adobe.com/commerce/webapi/graphql/schema/live-search/queries/attribute-metadata/).

![espacio de trabajo de GraphQL](assets/graphql.png)

```graphql
query productSearch {
  productSearch(phrase: "a306") {
    total_count
    items {
      product {
        sku
        name
      }
    }
    facets {
      title
    }
  }
}
```

Variables:

```json
{
  "Magento-Environment-Id": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
  "Magento-Website-Code": "base",
  "Magento-Store-Code": "base",
  "Magento-Store-View-Code": "default",
  "X-Api-Key": "search_gql"
}
```
