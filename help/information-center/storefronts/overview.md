---
title: Tiendas
description: Obtenga información acerca de las opciones de tienda de Adobe Commerce, incluida la tienda de Commerce con tecnología de Edge Delivery Services y las implementaciones personalizadas sin encabezado.
role: Developer, Leader
feature: Storefront, Integration
recommendations: noCatalog
autotag-review: '2026-10-20T01:12:22.967Z'
TQID: 'https://experienceleague.adobe.com/1mQm2s3UGzr7S4j9RMZAaRoUVtzu93N1IFbOypR8vkA'
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
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
subfeature_v2:
  - id: e396cff5-f586-484c-89f0-7f1da3308f92
    internal-label: GraphQL
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '349'
ht-degree: 0%
---

# Tiendas

La tienda es independiente del back-end de Commerce y de las capas de API. Según la arquitectura seleccionada, una tienda puede recuperar datos de las API de Commerce Foundation, las API de Storefront Services, las API de [!DNL Adobe Commerce Optimizer] Merchandising Services o los sistemas conectados mediante API Mesh, App Builder u otros mecanismos de integración. Consulte [Opciones de arquitectura](../architecture-options/overview.md) para ver cómo se vincula cada tienda con un servidor de Commerce.

## Tienda Commerce con tecnología de Edge Delivery Services

La Tienda Commerce con tecnología de [!DNL Edge Delivery Services] es una opción de tienda orientada al cliente creada en la plantilla de Adobe Commerce, que usa componentes desplegables y bloques de contenido. Es compatible con cualquiera de las [descripciones generales de arquitectura](../architecture-options/overview.md), la conexión a Commerce Foundation, Storefront Services o [!DNL Adobe Commerce Optimizer] Merchandising Services, según el servidor. Ver la [descripción general de Adobe Commerce Storefront](https://experienceleague.adobe.com/en/tools/commerce-storefront/).

## Servicios de tienda

[!DNL Storefront Services] son servicios orientados a tiendas que se usan con [!DNL Adobe Commerce]. Las API de servicio proporcionan un acceso optimizado a funcionalidades como:

- [!DNL Catalog Service]
- [!DNL Live Search]
- [!DNL Product Recommendations]

Tanto [!DNL Adobe Commerce] en la nube o de forma local (cuando está configurado) como [!DNL Adobe Commerce as a Cloud Service] usan los servicios de tienda. No son exclusivos de [!DNL Adobe Commerce as a Cloud Service] y no deben usarse como etiqueta distintiva entre las dos opciones de plataforma de [!DNL Adobe Commerce]. Consulte el [esquema de GraphQL de Storefront Services](https://developer.adobe.com/commerce/webapi/graphql/schema/storefront-services/).

## Tiendas personalizadas sin encabezado

Las opciones de tienda más allá de Commerce Storefront con tecnología de [!DNL Edge Delivery Services] incluyen [!DNL Luma], [!DNL PWA Studio] o una tienda sin encabezado personalizada, según la compatibilidad de la plataforma y los requisitos de implementación. Una tienda personalizada sin encabezado se conecta a las mismas familias de API que cualquier otra opción de tienda (Commerce Foundation, Storefront Services o Commerce Optimizer Merchandising Services) según la [opción de arquitectura seleccionada](../architecture-options/overview.md).

## Integración del carro y el cierre de compra

El lugar donde se gestionan las transacciones de carro de compras y cierre de compra depende del back-end de Commerce, no de la tecnología de tienda:

- Cuando [!DNL Adobe Commerce] Commerce Foundation es el servidor, la tienda usa las API de Commerce Foundation para las operaciones de carro de compras, cierre de compra, cliente y pedido, además de las integraciones de pago, impuestos, envío y cumplimiento configuradas.
- Cuando una plataforma de comercio de terceros es el servidor (como con [!DNL Adobe Commerce Optimizer]), la tienda se conecta al carro de compras, el cierre de compra, el cliente, el pedido, los pagos, los impuestos, el envío y los servicios de cumplimiento de esa plataforma a través de API Mesh, App Builder o una integración directa.

## Directrices relacionadas

- [Descripción general de arquitectura](../architecture-options/overview.md)
- [API](../apis/commerce-apis.md)
