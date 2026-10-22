---
title: Arquitecturas de referencia
description: Obtenga información sobre los patrones de arquitectura de referencia para implementaciones comunes de Adobe Commerce, como tiendas, servicios y canalizaciones de sincronización de catálogos.
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T11:42:09.021Z'
TQID: 'https://experienceleague.adobe.com/GVbGyRZz8llMWcUykcXXZwWnTaAomHVCTcV3ft49IEc'
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
  - id: 8dc0e58b-adf0-51bb-8db5-bb36e3e656fb
    internal-label: Inventory
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
    internal-label: Commerce ecosystem
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '227'
ht-degree: 0%
---

# Arquitecturas de referencia

La siguiente documentación proporciona patrones de arquitectura de referencia para plataformas y servicios de Adobe Commerce en diferentes modelos de implementación y casos de uso.

- [Arquitectura de Adobe Commerce as a Cloud Service](/help/cloud-service/overview.md#architecture)
- [Arquitectura de referencia empresarial de Adobe Commerce](https://experienceleague.adobe.com/es/docs/commerce-operations/implementation-playbook/architecture/enterprise-blueprint){target="_blank"}
- [arquitectura de tienda de Adobe Commerce](https://experienceleague.adobe.com/en/tools/commerce-storefront/get-started/architecture/){target="_blank"}
- [Adobe Commerce sobre la arquitectura de la infraestructura en la nube](https://experienceleague.adobe.com/es/docs/commerce-on-cloud/user-guide/architecture/cloud-architecture){target="_blank"}

## Tienda con tecnología de Edge Delivery Services

Una tienda basada en la plantilla de Adobe Commerce, que usa componentes desplegables y bloques de contenido, conectada a Adobe Commerce o [!DNL Adobe Commerce Optimizer] como servidor. Ver la [descripción general de Adobe Commerce Storefront](https://experienceleague.adobe.com/en/tools/commerce-storefront/).

- [arquitectura de tienda de Adobe Commerce](https://experienceleague.adobe.com/en/tools/commerce-storefront/get-started/architecture/)

## Canalización de sincronización de catálogo

Flujo de datos para mantener sincronizados los datos de catálogo, precio e inventario entre Adobe Commerce y los servicios de Adobe Commerce (Commerce Optimizer, Live Search, Servicio de catálogo, Recomendaciones de productos y otros [servicios de Commerce](../../landing/home.md) conectados).

- Para Adobe Commerce as a Cloud Service, en la infraestructura de la nube o en implementaciones locales, consulte [Sincronizar datos con la exportación de datos SaaS](/help/data-export/sync-overview.md)

- Para Adobe Commerce en la infraestructura en la nube o de forma local con Adobe Commerce Optimizer Connector, consulte [Canalización de sincronización de conectores](/help/aco-connector/connector-sync-pipeline.md).


## Directrices relacionadas

- [Arquitecturas de implementación](implementation-architectures.md)
