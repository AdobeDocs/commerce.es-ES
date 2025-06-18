---
title: Coincidencia automática personalizada
description: Descubra cómo la coincidencia automática personalizada es especialmente útil para los comerciantes con una lógica de coincidencia compleja o para aquellos que dependen de un sistema de terceros que no puede rellenar metadatos de imágenes de producto en los AEM Assets.
feature: CMS, Media, Integration
source-git-commit: 3ecc429003490235211a812af064d1b10d053e38
workflow-type: tm+mt
source-wordcount: '251'
ht-degree: 0%

---


# Coincidencia automática personalizada

Si la estrategia de coincidencia automática predeterminada (**coincidencia automática OOTB**) no está alineada con los requisitos comerciales específicos, seleccione la opción de coincidencia personalizada. Esta opción admite el uso de [Adobe Developer App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder) para desarrollar una aplicación de emparejamiento personalizada que administre lógicas de emparejamiento complejas, o recursos procedentes de un sistema de terceros que no puedan rellenar metadatos de imágenes de producto en AEM Assets.

## Configurar la coincidencia automática personalizada

1. En el Administrador de Commerce, vaya a **[!UICONTROL Store]** > Configuración > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

1. Seleccione **[!UICONTROL Custom Matcher]** como regla coincidente.

1. Al seleccionar esta regla coincidente, el administrador muestra campos adicionales para configurar los **extremos** y los **parámetros de autenticación** necesarios para la lógica de coincidencia personalizada.

## Extremos de API de emparejador personalizados

Cuando crea una aplicación de emparejador personalizada usando [App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder){target=_blank}, la aplicación debe exponer los siguientes extremos:

* **Extremo de recurso de App Builder a dirección URL del producto**
* Extremo de **App Builder product to asset URL**

### Extremo de recurso de App Builder a URL del producto

Este punto de conexión recupera la lista de SKU asociadas a un recurso determinado:

#### Ejemplo de uso

```bash
const { Core } = require('@adobe/aio-sdk')
 
async function main (params) {
    // return the products that map to the assetId
    return {
        statusCode: 200,
        body: {
          asset_id: "urn:aaid:aem:1aa1d4a0-18b8-40a7-a228-e0ab588deee1",
          product_matches: [
            {
              product_sku: "SKU1",
              asset_roles: ["thumbnail"],
              asset_position: [1]
            }
          ]
        }
   }
}
 
exports.main = main
```

**Solicitud**

```bash
GET https://your-app-builder-url/api/v1/web/app-builder-external-rule/asset-to-product
```

| Parámetro | Tipo de datos | Descripción |
| --- | --- | --- |
| `assetId` | Cadena | Representa el ID de recurso actualizado |

**Respuesta**

```bash
{
  "asset_id": "{ASSET_ID}",
  "product_matches": [
    {
      "product_sku": "{PRODUCT_SKU_1}",
      "asset_roles": ["thumbnail","image"]
    },
    {
      "product_sku": "{PRODUCT_SKU_2}",
      "asset_roles": ["thumbnail"]
    }
  ]
}
```

### Extremo de URL de producto a recurso de App Builder

Este extremo recupera la lista de recursos asociados a un SKU determinado:

#### Ejemplo de uso

```bash
const { Core } = require('@adobe/aio-sdk')
 
async function main (params) {
    // return asset matches for a product
    return {
        statusCode: 200,
        body: {
          product_sku: params.productSku, //SKU-1
          asset_matches: [
            {
              asset_id: "urn:aaid:aem:1aa1d4a0-18b8-40a7-a228-e0ab588deee1",
              asset_roles: ["thumbnail","image"]
            }
          ]
        }
      }
}
 
exports.main = main
```

**Solicitud**

```bash
GET https://your-app-builder-url/api/v1/web/app-builder-external-rule/product-to-asset
```

| Parámetro | Tipo de datos | Descripción |
| --- | --- | --- |
| `productSKU` | Cadena | Representa el SKU del producto actualizado |

**Respuesta**

```bash
{
  "product_sku": "{PRODUCT_SKU}",
  "asset_matches": [
    {
      "asset_id": "{ASSET_ID_1}",
      "asset_roles": ["thumbnail","image"]
    },
    {
      "asset_id": "{ASSET_ID_2}",
      "asset_roles": ["thumbnail"]
    }
  ]
}
```

>[!TIP]
>
> En la clave `asset_roles`, use los [roles de recurso de Commerce](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/digital-assets/product-image#image-roles) admitidos, como `thumbnail`, `image`, `small_image` y `swatch_image`.
