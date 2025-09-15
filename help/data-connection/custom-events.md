---
title: Creación de eventos personalizados
description: Aprenda a crear eventos personalizados para conectar los datos de Adobe Commerce a otros productos DX de Adobe.
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: db782c0a-8f13-4076-9b17-4c5bf98e9d01
source-git-commit: 4e8cf0ad3f8f94d4f59bc8d78a44f4b3e86cbc3e
workflow-type: tm+mt
source-wordcount: '348'
ht-degree: 0%

---

# Creación de eventos personalizados

Puede ampliar la [plataforma de eventos](events.md) creando sus propios eventos de tienda para recopilar datos exclusivos de su sector. Cuando crea y configura un evento personalizado, se envía a [Recopilador de eventos de Adobe Commerce](https://github.com/adobe/commerce-events/tree/main/packages/storefront-events-collector).

## Gestión de eventos personalizados

Los eventos personalizados solo son compatibles con Adobe Experience Platform. Los datos personalizados no se reenvían a los paneles de Adobe Commerce ni a los rastreadores de métricas.

Para cualquier evento `custom`, el recolector:

- Agrega `identityMap` con `ECID` como identidad principal
- Incluye `email` en `identityMap` como identidad secundaria _si_ `personalEmail.address` se establece en el evento
- Envuelve el evento completo dentro de un objeto `xdm` antes de reenviarlo a Edge

Ejemplo:

Evento personalizado publicado mediante Adobe Commerce Events SDK:

```javascript
mse.publish.custom({
    commerce: {
        saveForLaters: {
            value: 1,
        },
    },
});
```

En Experience Platform Edge:

```javascript
{
  xdm: {
    identityMap: {
      ECID: [
        {
          id: 'ecid1234',
          primary: true
        }
      ],
      email: [
        {
          id: "runs@safari.ke",
          primary: false
        }
      ]
    },
    commerce: {
        saveForLaters: {
            value: 1
        }
    }
  }
}
```

>[!NOTE]
>
> El uso de eventos personalizados puede afectar a los informes predeterminados de Adobe Analytics.

## Controlar anulaciones de eventos (atributos personalizados)

Para cualquier evento establecido con un `customContext`, el recolector anula o amplía los campos de la carga útil de evento de los campos del `custom context`. El caso de uso de las invalidaciones es cuando un desarrollador desea reutilizar y ampliar contextos establecidos por otras partes de la página en eventos ya admitidos.

Las anulaciones de eventos solo son aplicables cuando se reenvía a Experience Platform. No se aplican a eventos de análisis de Adobe Commerce y Sensei. El recopilador de eventos de Adobe Commerce [README](https://github.com/adobe/commerce-events/blob/e34bcfc0deca8d5ac1f9310fc1ee4c1becf4ffbb/packages/storefront-events-collector/README.md) proporciona información adicional.

>[!NOTE]
>
>Al aumentar `productListItems` con atributos personalizados en las cargas útiles de evento de Experience Platform, combine los productos con SKU. Este requisito no se aplica a `product-page-view` eventos.

### Uso

```javascript
const mse = window.magentoStorefrontEvents;

mse.publish.productPageView(customCtx);
```

### Ejemplo 1

En este ejemplo se agrega un contexto personalizado al publicar el evento.

```javascript
magentoStorefrontEvents.publish.productPageView({
    productListItems: [
        {
            productCategories: [
                {
                    categoryID: "cat_15",
                    categoryName: "summer pants",
                    categoryPath: "pants/mens/summer",
                },
            ],
        },
    ],
});
```

### Ejemplo 2

En este ejemplo se agrega un contexto personalizado antes de publicar el evento.

```javascript
const mse = window.magentoStorefrontEvents;

mse.context.setCustom({
  productListItems: [
    {
      productCategories: [
        {
          categoryID: "cat_15",
          categoryName: "summer pants",
          categoryPath: "pants/mens/summer",
        },
      ],
    },
  ],
});

mse.publish.productPageView();
```

### Ejemplo 3

Este ejemplo establece el contexto personalizado en el publicador y sobrescribe el contexto personalizado establecido anteriormente en la capa de datos del cliente de Adobe.

En este ejemplo, el evento `pageView` tendrá **Nombre de página personalizado 2** en el campo `web.webPageDetails.name`.

```javascript
const mse = window.magentoStorefrontEvents;

mse.context.setCustom({
  web: {
    webPageDetails: {
      name: 'Custom Page Name 1'
    },
  },
});

mse.publish.pageView({
  web: {
    webPageDetails: {
      name: 'Custom Page Name 2'
    },
  },
});
```

### Ejemplo 4

Este ejemplo agrega contexto personalizado a `productListItems` eventos con varios productos.

```javascript
const mse = window.magentoStorefrontEvents;

mse.context.setCustom({
  productListItems: [
    {
      SKU: "24-WB01", //Match SKU to override correct product in event payload
      productCategory: "Hand Bag", //Custom attribute added to event payload
      name: "Strive Handbag (CustomName)" //Override existing attribute with custom value in event payload
    },
    {
      SKU: "24-MB04",
      productCategory: "Backpack Bag",
      name: "Strive Backpack (CustomName)"
    },
  ],
});

mse.publish.shoppingCartView();
```

Tiendas basadas en Luma:

Los almacenes basados en Luma implementan eventos de publicación de forma nativa, por lo que puede establecer datos personalizados ampliando `customContext`.

Por ejemplo:

```javascript
mse.context.setCustom({
  web: {
    webPageDetails: {
      name: 'Custom Page Name'
    },
  },
});
```

>[!NOTE]
>
> Anular los eventos con atributos personalizados puede afectar a los informes predeterminados de Adobe Analytics.
