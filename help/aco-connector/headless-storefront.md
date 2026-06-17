---
title: Integración de tienda sin encabezado [!DNL Adobe Commerce Optimizer Connector]
description: Aprenda a integrar tiendas sin encabezado con la API de  [!DNL Adobe Commerce Optimizer Connector] GraphQL, las ID de los libros de precios y la codificación de los complementos al carro de compras.
feature: Storefront, Integration, GraphQL
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."
autotag-review: '2026-06-09T16:27:30.102Z'
TQID: 'https://experienceleague.adobe.com/Orif1rROglTQ-3ZkRj5LMF90Y-AdpfTnOgPmJXQjYgc'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: c32adafa-ed01-4b31-997e-2413013911b0
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: d378ca77-2da1-4f39-ad92-1917fe974a38
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 237
ht-degree: 0%

---

# Integración de tienda sin encabezado

El módulo `CommerceAdapter` amplía [!DNL Adobe Commerce] para reducir el espacio entre una tienda sin encabezado y [!DNL Adobe Commerce Optimizer]. Proporciona una consulta de GraphQL para resolver el contexto del libro de precios del cliente y aplica la codificación de producto del paquete esperada por la API de GraphQL [!DNL Adobe Commerce Optimizer].

Para obtener instrucciones de configuración de tienda de alto nivel, consulta [Configurar tiendas y comercialización](./overview.md#merchandising-storefronts) en la descripción general de [!DNL Adobe Commerce Optimizer Connector].

## GraphQL: `commerceOptimizer` consulta {#graphql-commerceoptimizer-query}

Las tiendas sin encabezado llaman a la consulta de GraphQL `commerceOptimizer` para recuperar `priceBookId` para la sesión de cliente actual. Pase este valor a la [[!DNL Adobe Commerce Optimizer] API de GraphQL](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/using-the-api){target="_blank"} al obtener los precios.

```graphql
{
  commerceOptimizer {
    priceBookId
  }
}
```

Respuesta de ejemplo:

```json
{
  "data": {
    "commerceOptimizer": {
      "priceBookId": "base::a94a8fe5ccb19ba61c4c0873d391e987982fbbd3"
    }
  }
}
```

Cómo se resuelve `priceBookId`:

| Estado de sesión | `priceBookId` |
|-----------------------|---------------------------------------------------------------------|
| Invitado (sin sesión iniciada) | `websiteCode::sha1(0)`, donde `0` es el identificador del grupo de clientes invitados |
| Cliente conectado | `websiteCode::sha1(customerGroupId)` |

El encabezado de solicitud `Store` determina el ámbito del sitio web y, por lo tanto, el componente `websiteCode`. El componente `sha1(customerGroupId)` coincide con la fórmula de ID de libro de precios utilizada durante la sincronización de datos. Ver [Libros de precios](reference/field-mapping.md#price-books).

## Productos agrupados: formato de complemento al carro de compras {#bundle-products-add-to-cart-format}

Permitir que los compradores agreguen productos agrupados al carro de compras desde una tienda sin encabezado con solo `SKU` y `qty` para cada opción de paquete seleccionada.

Cada valor de opción seleccionado o introducido debe estar codificado en Base64 en el siguiente formato:

```text
base64("bundle_item/" + JSON.stringify({"sku": "<child_sku>", "qty": "<qty>"}))
```

El mismo SKU secundario puede aparecer solo una vez en todas las opciones.

Ejemplo ([!DNL JavaScript]):

```javascript
const encodedOption = btoa(
  'bundle_item/' + JSON.stringify({ sku: 'child-product-sku', qty: '1' })
);
```
