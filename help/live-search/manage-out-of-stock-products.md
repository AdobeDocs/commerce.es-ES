---
title: Administrar productos sin existencias en  [!DNL Live Search]
description: Obtenga información sobre cómo administrar productos sin existencias en  [!DNL Live Search] for Adobe Commerce. Configure la visualización del inventario, el filtro inStock y el filtrado de la API de GraphQL.
feature: Services, Search
role: Admin, Developer
level: Intermediate
source-git-commit: bc8f35434c9f01f1a920745fe42617df2003ca60
workflow-type: tm+mt
source-wordcount: '447'
ht-degree: 0%

---

# Administración de productos sin existencias

Puede controlar cómo se muestran los productos sin existencias en los resultados de búsqueda y categoría de [!DNL Live Search] mediante la configuración del inventario, los filtros de tiempo de consulta y los indicadores de características de backend opcionales. Estas opciones tienen límites importantes, que se explican en este tema.

## Filtros de estado de stock

El atributo de Adobe Commerce Stock `quantity_and_stock_status` no se admite como faceta y no aparece en el cuadro de diálogo **[!UICONTROL Add Facet]**. Sin embargo, [!DNL Live Search] expone un campo `inStock` que puede usar como filtro en el momento de la consulta.

## Ocultar productos sin existencias

Utilice uno de los siguientes métodos para ocultar los productos sin existencias.

### Configuración de Commerce

1.Desde *Admin*, vaya a **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**>**[!UICONTROL Catalog]**>**[!UICONTROL Inventory]**.

1.Establezca **[!UICONTROL Display Out of Stock Products]** en **[!UICONTROL No]**.

1. Haga clic en **[!UICONTROL Save Config]**.

Cuando **[!UICONTROL Display Out of Stock Products]** se establece en `No`, [!DNL Live Search] agrega `inStock = 'no` a las consultas de tienda a través del widget PLP, por lo que no se devuelven productos sin existencias.

### Filtro de API

Cuando llame directamente a la API [!DNL Live Search] (GraphQL o REST), filtre los productos sin existencias de forma explícita, por ejemplo:

```graphql
query productSearchInStockOnly {
  productSearch(
    phrase: ""
    filter: [
      { attribute: "inStock", eq: "true" }
    ]
  ) {
    total_count
    items {
      productView {
        sku
        name
        inStock
      }
    }
  }
}
```

Utilice este método cuando no enrute la solicitud a través de [Live Search PLP Widget](plp-styling.md).

### Mostrar las existencias agotadas después de obtener los resultados

Para mantener los productos sin existencias en el conjunto de resultados, pero siempre después de los productos en existencias, al ordenarlos por relevancia, Adobe puede habilitar un indicador de funciones interno para su entorno.

- Esta marca de característica no se expone en la interfaz de usuario del administrador de [!DNL Live Search].
- Para solicitarlo, [comuníquese con la atención al cliente de Adobe](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide){target="_blank"} y haga referencia a la función para mover los productos sin existencias al final de los resultados de búsqueda.

>[!NOTE]
>
>Una vez habilitado el indicador, cualquier producto que quede sin existencias en el conjunto de resultados se moverá al final al ordenar por *Relevancia*. Otros criterios de ordenación (por ejemplo, *Precio* o *Nombre del producto*) no se ven afectados.

### Buscar reglas de comercialización y existencias

Las reglas de comercialización de búsqueda se basan en consultas y se dirigen a productos individuales, no a grupos enteros por estado de stock o valor de faceta:

- Las condiciones de regla dependen únicamente de la frase de búsqueda del comprador (`Query is`, `Query contains`, `Query starts with`, `Query ends with`).
- Los eventos de regla (Boost, Bury, Pin, Hide) se aplican a un SKU por evento.

Debido a estas restricciones:

- No puede crear una regla que entierre u oculte todos los productos sin existencias solo en función del estado de las existencias.
- Puede ocultar o enterrar manualmente SKU específicas que añada como eventos en una regla (sujeto a límites de 50 reglas y 25 eventos por regla).

Para ocultar o quitar la prioridad a los productos sin existencias en el catálogo, use la configuración de inventario y el filtro `inStock` (y el indicador de característica opcional) que se describen en este tema en lugar de las reglas de comercialización de búsqueda.

>[!MORELIKETHIS]
>
> - [Buscar reglas de comercialización](rules.md)
> - [Configurar las opciones globales de Inventory management](https://experienceleague.adobe.com/en/docs/commerce-admin/inventory/configuration/configuration)
