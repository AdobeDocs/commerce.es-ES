---
title: Creación de eventos personalizados
description: Aprenda a crear eventos personalizados para conectar los datos de Adobe Commerce a otros productos DX de Adobe.
role: Admin, Developer
feature: Personalization, Integration, Eventing
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '260'
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

Las anulaciones de atributos para eventos estándar solo se admiten en Experience Platform. Los datos personalizados no se reenvían a los paneles de Commerce ni a los rastreadores de métricas.

Para cualquier evento con `customContext`, el recolector anula los campos combinados establecidos en los contextos relevantes con campos en `customContext`. El caso de uso de las invalidaciones es cuando un desarrollador desea reutilizar y ampliar contextos establecidos por otras partes de la página en eventos ya admitidos.

>[!NOTE]
>
>Al anular los eventos personalizados, el reenvío de eventos a Experience Platform debe desactivarse para ese tipo de evento a fin de evitar el recuento doble.

Ejemplos:

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

>[!NOTE]
>
> Anular los eventos con atributos personalizados puede afectar a los informes predeterminados de Adobe Analytics.
