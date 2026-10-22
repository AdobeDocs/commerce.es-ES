---
title: Opciones de arquitectura de implementación
description: Compare arquitecturas de Adobe Commerce, incluidas Commerce Foundation, Adobe Commerce as a Cloud Service, Optimizer Connector y Optimizer independiente.
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T01:39:51.406Z'
TQID: 'https://experienceleague.adobe.com/tYkxRAfJWOY7C0OEqYxEb4onwvnnL9wEofEG2e6qnKA'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
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
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: 8dc0e58b-adf0-51bb-8db5-bb36e3e656fb
    internal-label: Inventory
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
subfeature_v2:
  - id: e396cff5-f586-484c-89f0-7f1da3308f92
    internal-label: GraphQL
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: 4c3c267873a68560a885c6376cd1137a7503710a
workflow-type: tm+mt
source-wordcount: '863'
ht-degree: 0%
---

# Opciones de arquitectura de implementación

Las arquitecturas de implementación de Adobe Commerce combinan tres capas: un servidor de comercio ([!DNL Adobe Commerce] o [!DNL Adobe Commerce Optimizer]), una tienda y un conjunto de servicios e integraciones conectados. Compare las siguientes opciones para identificar qué sistema posee transacciones de catálogo, precios, carro de compras, cierre de compra, pedidos y clientes en cada arquitectura.

## Resumen de opciones de arquitectura

Compare las opciones por propiedad de transacción y por experiencia de tienda.

### Plataforma y transacciones de Commerce

| Opción | Sistema de registro | Ruta de transacción | Mejor ajuste |
| --- | --- | --- | --- |
| **[!DNL Adobe Commerce as a Cloud Service]con Commerce Foundation** | Commerce Foundation administrado por Adobe | Servicios administrados de Commerce Foundation y Commerce conectados | Clientes que desean un Commerce as a service (SaaS) de software administrado por Adobe con una propiedad de infraestructura reducida |
| **[!DNL Adobe Commerce]en la nube o de forma local con[!DNL Adobe Commerce Optimizer Connector]** | Commerce Foundation existente, para datos y transacciones de Commerce | API de Commerce Foundation y servicios de transacciones conectados existentes | Clientes que deseen agregar las funcionalidades de detección y comercialización de Optimizer a una implementación de [!DNL Adobe Commerce] existente |
| **Cliente [!DNL Adobe Commerce Optimizer] independiente con un servidor de comercio externo** | Plataforma de comercio existente o de terceros. Los datos de catálogo y precio se añaden al Optimizer desde una fuente externa | API Mesh, App Builder o integraciones directas conectan la tienda con el carro de compras, el cierre de compra, el cliente, el pedido, el pago, los impuestos, el envío y los servicios de cumplimiento de terceros | Clientes que desean las funcionalidades de Optimizer mientras conservan una plataforma de comercio transaccional existente o de terceros |
| **[!DNL Adobe Commerce]en la nube o local con Commerce Foundation** | Commerce Foundation | API de Commerce Foundation e integraciones de pago, impuestos, envío, inventario y cumplimiento configuradas | Clientes que necesitan la plataforma completa de [!DNL Adobe Commerce] con control de implementación sobre la infraestructura en la nube o local |

### Experiencia en tienda

Las tiendas se conectan a las API de Commerce Foundation, a los servicios de tienda ([!DNL Catalog Service], [!DNL Live Search] y [!DNL Product Recommendations]) o a los servicios de comercialización de [!DNL Adobe Commerce Optimizer].

| Opción | Experiencia en tienda | Ruta de datos de tienda |
| --- | --- | --- |
| **[!DNL Adobe Commerce as a Cloud Service]con Commerce Foundation** | Tienda Commerce con tecnología Edge Delivery Services u otra experiencia sin encabezado compatible | Servicios de tienda, además de las API de Commerce Foundation para los datos de la plataforma principal |
| **[!DNL Adobe Commerce]en la nube o de forma local con[!DNL Adobe Commerce Optimizer Connector]** | Edge Delivery Services o tienda personalizada sin encabezado con experiencias del Optimizador | API de GraphQL de Commerce Optimizer Merchandising Services para datos de catálogo y comercialización administrados por Optimizer |
| **Cliente [!DNL Adobe Commerce Optimizer] independiente con un servidor de comercio externo** | Tienda Commerce con tecnología Edge Delivery Services o una tienda personalizada sin encabezado | API de GraphQL de Commerce Optimizer Merchandising Services para datos de catálogo y comercialización |
| **[!DNL Adobe Commerce]en la nube o local con Commerce Foundation** | Edge Delivery Services, Luma, PWA o tienda personalizada sin encabezado | API de Commerce Foundation, más servicios de tienda cuando se configuran |

## Adobe Commerce as a Cloud Service

![Diagrama de arquitectura de Adobe Commerce as a Cloud Service con Commerce Foundation administrado y servicios de tienda que alimentan una Commerce Storefront](../assets/architecture/commerce-cloud-service-storefront-services-arch.drawio.png){width="600" zoomable="yes"}

**Límite de clave**: Adobe administra la plataforma Commerce Foundation. La arquitectura usa Storefront Services, incluidos [!DNL Catalog Service], [!DNL Live Search] y [!DNL Product Recommendations], para las experiencias de tienda. [!DNL Product Visuals] con tecnología de AEM Assets es una integración SaaS opcional. Vea la integración de [AEM Assets para Commerce](../aem-assets/aem-assets-integration.md).

**Referencias:**

- [Información general de [!DNL Adobe Commerce as a Cloud Service]](/help/cloud-service/overview.md)
- [Commerce Storefront](https://experienceleague.adobe.com/en/tools/commerce-storefront/)
- [Esquema de GraphQL de Storefront Services](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/)

## Adobe Commerce con Commerce Foundation

![Diagrama de arquitectura de Adobe Commerce en la nube o local con servicios de tienda y API de Commerce Foundation que alimentan una tienda Commerce](../assets/architecture/commerce-paas-storefront-services-arch.drawio.png){width="600" zoomable="yes"}

**Límite de clave**: Commerce Foundation es propietario de la plataforma Commerce y de los flujos de transacciones. [!DNL Catalog Service], [!DNL Live Search] y [!DNL Product Recommendations] proporcionan acceso optimizado de tienda a catálogo, búsqueda y recomendaciones cuando se configuran. La integración de AEM Assets es opcional. Vea la integración de [AEM Assets para Commerce](../aem-assets/aem-assets-integration.md).

**Referencias:**

- [Commerce Storefront](https://experienceleague.adobe.com/en/tools/commerce-storefront/)
- [API de Commerce GraphQL](https://developer.adobe.com/commerce/webapi/graphql/)
- [Esquema de GraphQL de Storefront Services](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/)


## Adobe Commerce con el conector del optimizador

![Diagrama de arquitectura del conector de Adobe Commerce Optimizer que sincroniza los datos de catálogo y precio de Adobe Commerce a Adobe Commerce Optimizer y proporciona una tienda Commerce a través de las API de servicios de comercialización](../assets/architecture/adobe-commerce-optimizer-architecture.drawio.png){width="600" zoomable="yes"}

**Límite de clave**: el conector sincroniza los datos de catálogo y precio de [!DNL Adobe Commerce] a [!DNL Adobe Commerce Optimizer]. [!DNL Adobe Commerce] sigue siendo el sistema de transacciones, mientras que Optimizer proporciona experiencias de detección y comercialización a través de sus API de servicios de comercialización.

**Referencias:**

- [Integraciones de Commerce Optimizer](/help/optimizer/integrations/integrations-overview.md)
- [Servicios de comercialización de Commerce Optimizer](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/)
- [API de Commerce GraphQL](https://developer.adobe.com/commerce/webapi/graphql/)
- [Commerce Storefront](https://experienceleague.adobe.com/en/tools/commerce-storefront/)

## Commerce Optimizer independiente con un servidor de terceros

![Diagrama de arquitectura de sistemas de origen propiedad del cliente que envían datos de catálogo y precio a través de la ingesta de datos a un Adobe Commerce Optimizer independiente, que alimenta una tienda Commerce conectada a un servidor comercial de terceros](../assets/architecture/adobe-commerce-optimizer-standalone-detailed.drawio.png){width="800" zoomable="yes"}

**Límite de clave**: [!DNL Adobe Commerce Optimizer] es propietario independiente de las experiencias de detección de catálogos y comercialización, pero no del backend de Commerce transaccional. Datos de catálogo y precio introducidos mediante la API de REST de ingesta de datos. La tienda de Edge Delivery Services utiliza las API de GraphQL de los servicios de comercialización para las experiencias de los productos y se conecta al servidor de terceros para el carrito y el pago.

**Referencias:**

- [¿Qué es Adobe Commerce Optimizer?](/help/optimizer/overview.md)
- [Ingesta de datos de Commerce Optimizer](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/)
- [Servicios de comercialización de Commerce Optimizer](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/)
- [Commerce Storefront](https://experienceleague.adobe.com/en/tools/commerce-storefront/)

## Referencia rápida de terminología

| Término preferido | Significado | Evite utilizar como etiqueta de arquitectura actual |
| --- | --- | --- |
| **Commerce Foundation** | Funcionalidades comerciales y transaccionales básicas | Core Commerce, nivel básico de PHP |
| **Servicios de tienda** | API orientadas a tiendas para el servicio de catálogo, Live Search y recomendaciones de productos | Una etiqueta limitada a una sola plataforma de Commerce |
| **Servicios de comercialización de Commerce Optimizer** | API de Optimizer para la detección de catálogos y experiencias de comercialización | API de Commerce Foundation |
| **Tienda Commerce con tecnología de Edge Delivery Services** | Implementación de tienda orientada al cliente | Una familia de API |

## Directrices relacionadas

- [Arquitecturas de referencia](reference-architectures.md)
- [Elija una opción de Commerce.](../portfolio/choose-commerce-option.md)
- [Tiendas](../storefronts/overview.md)
- [API](../apis/commerce-apis.md)
