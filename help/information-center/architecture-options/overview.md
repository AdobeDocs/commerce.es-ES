---
title: Descripción general de arquitectura de Commerce
description: Obtenga información acerca del modelo de producto de Adobe Commerce y dónde encontrar opciones de arquitectura detalladas, tienda e instrucciones de API.
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T10:11:03.706Z'
TQID: 'https://experienceleague.adobe.com/V9Zp0eS8b45xYEay4EK91tPVnKhRdkWGDj4Vv7hB79U'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
feature_v2:
  - id: 4273989f-0bf2-5361-a17a-6909488d18ab
    internal-label: Catalog Service
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: da3860b0-d637-47df-bef0-273751180266
    internal-label: Digital asset management
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%
---

# Descripción general de arquitectura de Commerce

Las arquitecturas de Adobe Commerce generalmente combinan tres capas: un servidor de comercio ([!DNL Adobe Commerce] o [!DNL Adobe Commerce Optimizer]), una tienda y un conjunto de servicios e integraciones conectados. Esta sección le guía por el modelo del producto y le dirige a las comparaciones detalladas, los diagramas y las referencias de la API que se mantienen en cada página dedicada.

## Primeros pasos

| Sección | Úselo para lo siguiente |
| ------- | --------- |
| [Plataformas y servicios](../portfolio/platform-and-services.md) | Comprenda qué es cada producto de Commerce: Adobe Commerce, Commerce Foundation, Adobe Commerce Optimizer y Adobe Commerce as a Cloud Service. |
| [Elegir una opción de Commerce](../portfolio/choose-commerce-option.md) | Compare las opciones de Commerce en función de la propiedad de la transacción, el modelo de implementación y las necesidades de comercialización. |
| [Opciones de arquitectura](../architecture-options/implementation-architectures.md) | Compare en detalle las cuatro arquitecturas compatibles, incluidos diagramas de sistemas y vínculos de referencia. |
| [Tiendas](../storefronts/overview.md) | Comprenda las opciones de la tienda y cómo se conectan a cada arquitectura. |
| [API](../apis/commerce-apis.md) | Compare las familias de API utilizadas en Commerce Foundation, Storefront Services y Commerce Optimizer. |
| Integración de [AEM Assets para Commerce](../aem-assets/aem-assets-integration.md) | Añada la administración centralizada de recursos digitales a cualquier arquitectura de Commerce o Optimizer. |
| [Migración y adopción](../migration-adoption/overview.md) | Planifique un cambio entre arquitecturas o una adopción gradual de Adobe Commerce Optimizer. |

## Referencia rápida de terminología

| Término preferido | Significado | Evite utilizar como etiqueta de arquitectura actual |
| --- | --- | --- |
| **Commerce Foundation** | Funcionalidades comerciales y transaccionales básicas | Nivel básico de Commerce y PHP |
| **Servicios de tienda** | API orientadas a tiendas para el servicio de catálogo, Live Search y recomendaciones de productos | Una etiqueta limitada a una sola plataforma de Commerce |
| **Servicios de comercialización de Commerce Optimizer** | API de Optimizer para la detección de catálogos y experiencias de comercialización | API de Commerce Foundation |
| **Tienda Commerce con tecnología de Edge Delivery Services** | Implementación de tienda orientada al cliente | Una familia de API |

## Directrices relacionadas

- [Arquitecturas de implementación](implementation-architectures.md)
- [Arquitecturas de referencia](reference-architectures.md)
- [Crear una nueva tienda](../implementation-guides/build-new-storefront.md)
