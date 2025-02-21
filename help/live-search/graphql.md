---
title: GraphQL
description: El espacio de trabajo  [!DNL Live Search] GraphQL le permite generar consultas con sus datos activos.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '39'
ht-degree: 0%

---

# GraphQL

El área de trabajo *GraphQL* permite a los administradores crear y probar consultas de GraphQL con sus propios datos.

Este área de trabajo admite las consultas [`productSearch`](https://developer.adobe.com/commerce/services/graphql/live-search/product-search/) y [`attributeMetadata`](https://developer.adobe.com/commerce/services/graphql/live-search/attribute-metadata/).

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

