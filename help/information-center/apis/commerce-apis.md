---
title: API de Commerce
description: Compare familias de API de Adobe Commerce, como Commerce Foundation, servicios de tienda, servicios de comercialización de Commerce Optimizer e ingesta de datos.
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T01:36:11.529Z'
TQID: 'https://experienceleague.adobe.com/JBpnpCy9QITdcYtKnL2btd9grmgIk1prYaCNasgWkok'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: ef0c45ae-6bee-4821-a65e-e1e118e8a01c
    internal-label: Commerce Optimizer
feature_v2:
  - id: 22bad240-8308-569b-a9d5-578f1ff890ca
    internal-label: Customers
  - id: 4273989f-0bf2-5361-a17a-6909488d18ab
    internal-label: Catalog Service
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 72863f3c-9d27-5dda-afe1-d9f934b1fba0
    internal-label: Extensibility
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: c4f010fa-1478-4300-a88d-706fbc036a7a
    internal-label: APIs and SDKs
subfeature_v2:
  - id: e396cff5-f586-484c-89f0-7f1da3308f92
    internal-label: GraphQL
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: da3860b0-d637-47df-bef0-273751180266
    internal-label: Digital asset management
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%
---

# API

| familia de API | Objetivo principal | Utilizado por |
| --- | --- | --- |
| **API de GraphQL de Commerce Foundation** | Funciones comerciales y transaccionales principales, como operaciones de catálogo, carro de compras, cierre de compra, clientes y pedidos | [!DNL Adobe Commerce] en la nube, [!DNL Adobe Commerce] en las instalaciones y [!DNL Adobe Commerce as a Cloud Service] |
| **API de GraphQL de servicios de tienda** | Experiencias de catálogo, búsqueda y recomendación orientadas a tienda mediante [!DNL Catalog Service], [!DNL Live Search] y [!DNL Product Recommendations] | [!DNL Adobe Commerce] en la nube o de forma local con servicios configurados, y [!DNL Adobe Commerce as a Cloud Service] |
| **API de GraphQL de Commerce Optimizer Merchandising Services** | Recupere los resultados de catálogo, vistas de catálogo, contextos de precio, búsqueda, recomendaciones y comercialización gestionados por Optimizer | [!DNL Adobe Commerce] en la nube o de forma local con el conector del optimizador y [!DNL Adobe Commerce Optimizer] de forma independiente |
| **API de REST de ingesta de datos de Commerce Optimizer** | Agregar datos de catálogo y precio a una implementación independiente de [!DNL Adobe Commerce Optimizer] | [!DNL Adobe Commerce Optimizer] independiente conectado a un origen de datos externo |

## API de GraphQL de Commerce Foundation

Funciones principales de comercio, como catálogo, carro de compras, cierre de compra, clientes y pedidos. Utilizado por [!DNL Adobe Commerce] en la nube, [!DNL Adobe Commerce] local y [!DNL Adobe Commerce as a Cloud Service]. Consulte la [API de Commerce GraphQL](https://developer.adobe.com/commerce/webapi/graphql/).

## API de GraphQL de Storefront Services

Experiencias de catálogo, búsqueda y recomendación orientadas a tienda mediante [!DNL Catalog Service], [!DNL Live Search] y [!DNL Product Recommendations]. Utilizado por [!DNL Adobe Commerce] en la nube, local y [!DNL Adobe Commerce as a Cloud Service]. Consulte el [esquema de GraphQL de Storefront Services](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/).

## API de GraphQL de Commerce Optimizer Merchandising Services

Recupere los resultados de catálogo, vistas de catálogo, contextos de precio, búsqueda, recomendaciones y comercialización gestionados por el Optimizador. Utilizado por [!DNL Adobe Commerce] en la nube, local con [!DNL Adobe Commerce Optimizer Connector] y [!DNL Adobe Commerce Optimizer] de forma independiente. Consulte [Servicios de comercialización de Commerce Optimizer](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/).

## API de REST de ingesta de datos de Commerce Optimizer

Agregar datos de catálogo y precio a una implementación independiente de [!DNL Adobe Commerce Optimizer] desde una fuente de datos externa. Consulte [Ingesta de datos de Commerce Optimizer](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/).

## Integraciones de Commerce Optimizer

[!DNL Adobe Commerce Optimizer] se conecta a otros sistemas a través de varias rutas de integración, dependiendo de si está emparejado con [!DNL Adobe Commerce] o con un servidor de terceros.

### Conector de Adobe Commerce Optimizer

Sincroniza los datos de catálogo y precio de [!DNL Adobe Commerce] en la nube o de forma local con [!DNL Adobe Commerce Optimizer], manteniendo [!DNL Adobe Commerce] como el sistema de transacciones mientras Optimizer proporciona detección y comercialización. Consulte [Integraciones de Commerce Optimizer](/help/optimizer/integrations/integrations-overview.md).

### Integraciones de comercio de terceros

Ingesta datos de catálogo y precio de una plataforma de comercio de terceros, PIM, ERP u otra fuente en [!DNL Adobe Commerce Optimizer] independiente a través de la API de REST de ingesta de datos, mientras que la plataforma de terceros sigue siendo el sistema de registro transaccional.

### API Mesh y App Builder

Utilice API Mesh para orquestar las API de Adobe Commerce con API privadas o de terceros. Utilice Adobe Developer App Builder para crear aplicaciones e integraciones personalizadas. Para obtener instrucciones de extensibilidad de Commerce relacionadas, consulte [API Mesh](https://developer.adobe.com/graphql-mesh-gateway/) y [Adobe Commerce extensibility](https://developer.adobe.com/commerce/extensibility/).

Para integraciones impulsadas por eventos específicamente, consulte [Adobe I/O Events para Adobe Commerce](https://experienceleague.adobe.com/es/docs/commerce-learn/tutorials/extensibility/adobe-developer-app-builder/io-events/getting-started-io-events).


### Entrega del carro y cierre de compra

Para [!DNL Adobe Commerce Optimizer] independientes con un servidor externo, la tienda usa las API de GraphQL de Servicios de comercialización para las experiencias de productos y luego transfiere el carro de compras, el cierre de compra, el cliente, el pedido, el pago, los impuestos, el envío y la satisfacción al servidor a través de la malla de API, App Builder o la integración directa.

### AEM Assets

AEM Assets es una integración opcional de administración de recursos digitales transversal que se puede añadir a cualquier arquitectura de Commerce o Optimizer, en lugar de a una ruta de integración propia independiente. Vea la integración de [AEM Assets para Commerce](../aem-assets/aem-assets-integration.md).

## Directrices relacionadas

- [Descripción general de arquitectura](../architecture-options/overview.md)
- [Tiendas](../storefronts/overview.md)
- [Integración de AEM Assets para Commerce](../aem-assets/aem-assets-integration.md)
