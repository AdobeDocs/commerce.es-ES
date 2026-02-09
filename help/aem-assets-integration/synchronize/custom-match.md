---
title: Coincidencia automática personalizada
description: Descubra cómo la coincidencia automática personalizada es especialmente útil para los comerciantes con una lógica de coincidencia compleja o para aquellos que dependen de un sistema de terceros que no puede rellenar metadatos en los AEM Assets.
feature: CMS, Media, Integration
exl-id: e7d5fec0-7ec3-45d1-8be3-1beede86c87d
source-git-commit: dfc4aaf1f780eb4a57aa4b624325fa24e571017d
workflow-type: tm+mt
source-wordcount: '432'
ht-degree: 0%

---

# Coincidencia automática personalizada

Si la estrategia de coincidencia automática predeterminada (**coincidencia automática OOTB**) no está alineada con los requisitos comerciales específicos, seleccione la opción de coincidencia personalizada. Esta opción admite el uso de [Adobe Developer App Builder](https://experienceleague.adobe.com/es/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder) para desarrollar una aplicación de emparejamiento personalizada que administre lógicas de emparejamiento complejas o recursos procedentes de un sistema de terceros que no puedan rellenar metadatos en los AEM Assets.

## Configurar la coincidencia automática personalizada

1. En el Administrador de Commerce, vaya a **[!UICONTROL Store]** > Configuración > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

1. Seleccione **[!UICONTROL Custom Matcher]** como regla coincidente.

1. Al seleccionar esta regla coincidente, el administrador muestra campos adicionales para configurar los **extremos** y los **parámetros de autenticación** necesarios para la lógica de coincidencia personalizada.

### workspace.json

El campo **[!UICONTROL Adobe I/O Workspace Configuration]** proporciona una forma sencilla de configurar su emparejador personalizado mediante la importación del archivo de configuración de App Builder `workspace.json`.

Puede descargar el archivo de `workspace.json` desde [Adobe Developer Console](https://developer.adobe.com/console). El archivo contiene todas las credenciales y los detalles de configuración de App Builder Workspace.

+++Ejemplo `workspace.json`

```json
{
  "project": {
    "id": "project_id",
    "name": "project_name",
    "title": "title_name",
    "org": {
      "id": "id",
      "name": "Organization_name",
      "ims_org_id": "ims_id"
    },
    "workspace": {
      "id": "workspace_id",
      "name": "workspace_name_id",
      "title": "workspace_title_id",
      "action_url": "https://action_url.net",
      "app_url": "https://app_url.net",
      "details": {
        "credentials": [
          {
            "id": "credential_id",
            "name": "credential_name_id",
            "integration_type": "oauth_server_to_server",
            "oauth_server_to_server": {
              "client_id": "client_id",
              "client_secrets": ["secret"],
              "technical_account_email": "xx@technical_account_email.com",
              "technical_account_id": "technical_account_id",
              "scopes": [
                "AdobeID",
                "openid",
                "read_organizations",
                "additional_info.projectedProductContext",
                "additional_info.roles",
                "adobeio_api",
                "read_client_secret",
                "manage_client_secrets"
              ]
            }
          }
        ],
        "services": [
          {
            "code": "AdobeIOManagementAPISDK",
            "name": "I/O Management API"
          }
        ],
        "runtime": {
          "namespaces": [
            {
              "name": "namespace_name",
              "auth": "example_auth"
            }
          ]
        },
        "events": {
          "registrations": []
        },
        "mesh": {}
      }
    }
  }
}
```

+++

1. Arrastre y suelte el archivo `workspace.json` de su proyecto de App Builder en el campo **[!UICONTROL Adobe I/O Workspace Configuration]**. También puede hacer clic en para examinar y seleccionar el archivo.

![Configuración de Workspace](../assets/workspace-configuration.png){width="600" zoomable="yes"}

1. El sistema automáticamente:

   * Valida la estructura JSON.
   * Extrae y rellena credenciales de OAuth
   * Obtiene las acciones de tiempo de ejecución disponibles para el espacio de trabajo
   * Rellena las opciones desplegables de los campos **[!UICONTROL Product to Asset URL]** y **[!UICONTROL Asset to Product URL]**

1. Seleccione las acciones de tiempo de ejecución adecuadas en los menús desplegables para cada flujo.

1. Haga clic en **[!UICONTROL Save Config]**.

## Extremos de API de emparejador personalizados

Cuando crea una aplicación de emparejador personalizada usando [App Builder](https://experienceleague.adobe.com/es/docs/commerce-learn/tutorials/adobe-developer-app-builder/introduction-to-app-builder){target=_blank}, la aplicación debe exponer los siguientes extremos:

* **Extremo de recurso de App Builder a dirección URL del producto**
* Extremo de **App Builder product to asset URL**

### Extremo de recurso de App Builder a URL del producto

Este punto de conexión recupera la lista de SKU asociadas a un recurso determinado:

#### Ejemplo de uso

```bash
const { Core } = require('@adobe/aio-sdk')

async function main(params) {

    // Build your own matching logic here to return the products that map to the assetId
    // var productMatches = [];
    // params.assetId
    // params.eventData.assetMetadata['commerce:isCommerce']
    // params.eventData.assetMetadata['commerce:skus'][i]
    // params.eventData.assetMetadata['commerce:roles']
    // params.eventData.assetMetadata['commerce:positions'][i]
    // ...
    // End of your matching logic

    return {
        statusCode: 500,
        body: {
            asset_id: params.assetId,
            product_matches: [
                {
                    product_sku: "<YOUR-SKU-HERE>",
                    asset_roles: ["thumbnail", "image", "swatch_image", "small_image"],
                    asset_position: 1
                }
            ]
        }
    };
}

exports.main = main;
```

**Solicitud**

```bash
POST https://your-app-builder-url/api/v1/web/app-builder-external-rule/asset-to-product
```

| Parámetro | Tipo de datos | Descripción |
| --- | --- | --- |
| `assetId` | Cadena | Representa el ID de recurso actualizado. |
| `eventData` | Cadena | Devuelve la carga útil de datos asociada al ID de recurso. |

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

async function main(params) {
    // return asset matches for a product
    // Build your own matching logic here to return the assets that map to the productSku
    // var assetMatches = [];
    // params.productSku
    // ...
    // End of your matching logic

    return {
        statusCode: 500,
        body: {
            product_sku: params.productSku,
            asset_matches: [
                {
                    asset_id: "<YOUR-ASSET-ID-HERE>", // urn:aaid:aem:1aa1d5i2-17h8-40a7-a228-e3ur588deee1
                    asset_roles: ["thumbnail", "image", "swatch_image", "small_image"],
                    asset_format: "image", // can be "image" or "video"
                    asset_position: 1
                }
            ]
        }
    };
}

exports.main = main;
```

**Solicitud**

```bash
POST https://your-app-builder-url/api/v1/web/app-builder-external-rule/product-to-asset
```

| Parámetro | Tipo de datos | Descripción |
| --- | --- | --- |
| `productSKU` | Cadena | Representa el SKU del producto actualizado. |
| `eventData` | Cadena | Devuelve la carga útil de datos asociada al SKU del producto. |

**Respuesta**

```bash
{
  "product_sku": "{PRODUCT_SKU}",
  "asset_matches": [
    {
      "asset_id": "{ASSET_ID_1}",
      "asset_roles": ["thumbnail","image"],
      "asset_position": 1,
      "asset_format": image
    },
    {
      "asset_id": "{ASSET_ID_2}",
      "asset_roles": ["thumbnail"]
      "asset_position": 2,
      "asset_format": image     
    }
  ]
}
```

| Parámetro | Tipo de datos | Descripción |
| --- | --- | --- |
| `productSKU` | Cadena | Representa el SKU del producto actualizado. |
| `asset_matches` | Cadena | Devuelve todos los recursos asociados con un SKU de producto específico. |

El parámetro `asset_matches` contiene los atributos siguientes:

| Atributo | Tipo de datos | Descripción |
| --- | --- | --- |
| `asset_id` | Cadena | Representa el ID de recurso actualizado. |
| `asset_roles` | Cadena | Devuelve todas las funciones de recurso disponibles. Utiliza [funciones de recurso de Commerce](https://experienceleague.adobe.com/es/docs/commerce-admin/catalog/products/digital-assets/product-image#image-roles) compatibles como `thumbnail`, `image`, `small_image` y `swatch_image`. |
| `asset_format` | Cadena | Proporciona los formatos disponibles para el recurso. Los valores posibles son `image` y `video`. |
| `asset_position` | Cadena | Muestra la posición del recurso. |
