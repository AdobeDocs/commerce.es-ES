---
title: Integración de AEM Assets para Commerce
description: Aprenda a integrar a los AEM Assets con Adobe Commerce, Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer para administrar las imágenes y los medios de los productos de forma centralizada.
role: Admin, Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T01:34:13.564Z'
TQID: 'https://experienceleague.adobe.com/v15DE37DoqpstrsWqnwd6DYpa5moT-BhQ80zDq2KP6I'
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
  - id: 00451af3-7b97-5414-9992-3a6c269e413f
    internal-label: Paas
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '323'
ht-degree: 4%
---

# Integración de AEM Assets para Commerce

La integración de AEM Assets de permite las funciones de Product Visuals en Adobe Commerce, de modo que puede administrar imágenes de productos, vídeos y otros medios de forma centralizada en los AEM Assets. Es un complemento opcional que funciona con cualquier opción de arquitectura de Commerce, no con una plataforma de Commerce independiente.

## Rutas de integración por arquitectura

Existen dos rutas de integración. La ruta depende de la arquitectura de Commerce.

| Arquitectura de Commerce | Ruta de integración de AEM Assets | Más información |
| --- | --- | --- |
| [!DNL Adobe Commerce] en la nube o de forma local | Integración de [!DNL AEM Assets] para Commerce. Utiliza el paquete de integración de Commerce para sincronizar y administrar imágenes de productos, vídeos y otros medios entre [!DNL Adobe Commerce] y [!DNL AEM Assets]. | Integración de [AEM Assets para Commerce](/help/aem-assets-integration/overview.md) |
| [!DNL Adobe Commerce as a Cloud Service] | [!DNL Product Visuals] con tecnología de [!DNL AEM Assets] | [Configuración de la integración de AEM Assets](/help/aem-assets-integration/overview.md#next-steps) |
| [!DNL Adobe Commerce Optimizer] de forma independiente | [!DNL Product Visuals] con tecnología de [!DNL AEM Assets]. Los datos del precio y el catálogo base llegan a través de la [API de ingesta de datos de Optimizer](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/). | [Imágenes de productos con AEM Assets](/help/optimizer/setup/product-visuals.md) |
| [!DNL Adobe Commerce] con [!DNL Adobe Commerce Optimizer Connector] | [!DNL Product Visuals] con tecnología de [!DNL AEM Assets]. El conector sincroniza los datos de catálogo y precio de [!DNL Adobe Commerce]. | [Integraciones de Commerce Optimizer](/help/optimizer/integrations/integrations-overview.md) |

[!DNL Product Visuals] es la ruta de integración para Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer. Sincroniza las imágenes de producto administradas por AEM con la capa de catálogo de Commerce y las envía a las experiencias de tienda a través de las API de tienda.

## Antes de elegir

- Los requisitos de configuración y licencia difieren entre la ruta de Commerce en la nube o local y la ruta de Commerce as a Cloud Service o Adobe Optimizer [!DNL Product Visuals]. Primero revise los requisitos específicos de la implementación.
- [!DNL AEM Assets] administra recursos digitales. No reemplaza el catálogo, precio, carro de compras, cierre de compra o sistema de pedidos de Commerce.
- Los recursos de producto coinciden con los productos de Commerce mediante SKU u otros metadatos coincidentes documentados.
- Si los equipos de marketing y comercialización necesitan flujos de trabajo centralizados de recursos e imágenes de productos, elija la ruta que coincida con la arquitectura de Commerce.

## Información relacionada

- [Documentación de Adobe Experience Manager Assets](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/assets/overview)
- [Descripción general de arquitectura](../architecture-options/overview.md)
- [API](../apis/commerce-apis.md)
