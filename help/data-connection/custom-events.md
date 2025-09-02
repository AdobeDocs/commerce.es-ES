---
title: Creación de eventos personalizados
description: Aprenda a crear eventos personalizados para conectar los datos de Adobe Commerce a otros productos DX de Adobe.
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: db782c0a-8f13-4076-9b17-4c5bf98e9d01
source-git-commit: 81fbcde11da6f5d086c2b94daeffeec60a9fdbcc
workflow-type: tm+mt
source-wordcount: '271'
ht-degree: 1%

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

Las anulaciones de atributos para eventos estándar solo se admiten en Experience Platform. Los datos personalizados no se reenvían a los paneles de Commerce ni a los rastreadores de métricas.

Para cualquier evento con `customContext`, el recolector anula los campos combinados establecidos en los contextos relevantes con campos en `customContext`. El caso de uso de las invalidaciones es cuando un desarrollador desea reutilizar y ampliar contextos establecidos por otras partes de la página en eventos ya admitidos.

### Ejemplos

Vista de producto con invalidaciones publicadas mediante Adobe Commerce Events SDK:

```javascript
mse.publish.productPageView({
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

En Experience Platform Edge:

```javascript
{
  xdm: {
    eventType: 'commerce.productViews',
    identityMap: {
      ECID: [
        {
          id: 'ecid1234',
          primary: true,
        }
      ]
    },
    commerce: {
      productViews: {
        value : 1,
      }
    },
    productListItems: [{
        SKU: "1234",
        name: "leora summer pants",
        productCategories: [{
            categoryID: "cat_15",
            categoryName: "summer pants",
            categoryPath: "pants/mens/summer",
        }],
    }],
  }
}
```

Tiendas basadas en Luma:

En las tiendas basadas en Luma, la publicación de eventos se implementa de forma nativa. Por lo tanto, puede establecer datos personalizados ampliando `customContext`.

Por ejemplo:

```javascript
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
```

Consulte [anulación de evento personalizado](https://github.com/adobe/commerce-events/blob/main/examples/events/custom-event-override.md) para obtener más información sobre la administración de datos personalizados.

>[!NOTE]
>
> Anular los eventos con atributos personalizados puede afectar a los informes predeterminados de Adobe Analytics.
