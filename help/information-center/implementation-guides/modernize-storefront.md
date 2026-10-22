---
title: Modernizar una tienda existente
description: Aprenda a planificar una migración incremental de una tienda de Adobe Commerce heredada a una tienda basada en Edge Delivery Services y componentes integrados.
role: Developer, Leader
feature: Storefront
recommendations: noCatalog
autotag-review: '2026-10-20T11:09:14.812Z'
TQID: 'https://experienceleague.adobe.com/1OR7uwncjLw-NpwMMuwKjDjpASdh74sfu6s5rNClqxg'
product_v2:
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 4273989f-0bf2-5361-a17a-6909488d18ab
    internal-label: Catalog Service
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
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '191'
ht-degree: 0%
---

# Modernizar una tienda existente

Puede migrar las tiendas heredadas gradualmente a los componentes desplegables de Edge Delivery Services y Commerce, en lugar de reconstruir todo a la vez.

>[!NOTE]
>
>Esta guía se aplica a Adobe Commerce as a Cloud Service, Adobe Commerce en la infraestructura en la nube o implementaciones locales que utilizan Storefront Services o el conector de Adobe Commerce Optimizer. También se aplica a Adobe Commerce Optimizer independiente con un back-end existente o de terceros. Para confirmar qué opción se aplica a su proyecto, consulte [Opciones de arquitectura de implementación](../architecture-options/implementation-architectures.md).

## Primeros pasos

1. Para entender cómo se compara una tienda creada en Edge Delivery Services con tu implementación actual, revisa la [descripción general de Adobe Commerce Storefront](https://experienceleague.adobe.com/en/tools/commerce-storefront/).

1. Use la [Guía para desarrolladores de Storefront](https://experienceleague.adobe.com/en/tools/commerce-storefront/get-started/) para determinar qué páginas o flujos se migrarán primero.

1. Para Adobe Commerce as a Cloud Service, mantenga las conexiones de servicios de Commerce existentes ([!DNL Catalog Service], [!DNL Live Search], [!DNL Product Recommendations], [!DNL Payment Services]) en su lugar (consulte [Configurar servicios de Commerce](set-up-commerce-services.md)).

## Directrices relacionadas

- [Crear una nueva tienda](build-new-storefront.md)
- [Opciones de arquitectura](../architecture-options/overview.md)
