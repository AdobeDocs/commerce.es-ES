---
title: Observabilidad de  [!DNL Adobe Commerce as a Cloud Service]
description: Obtenga información acerca de las herramientas de observabilidad y las capacidades de telemetría disponibles para  [!DNL Adobe Commerce as a Cloud Service], incluidas las métricas, el registro y el seguimiento.
feature: Cloud, Integration
role: Admin, Developer
level: Intermediate
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
autotag-review: '2026-06-09T15:41:54.613Z'
TQID: 'https://experienceleague.adobe.com/jTPNVSy6cP8v-pV-3pyqgJX-PAzFFhOUf9SjQIMeBns'
product_v2:
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: c2be0313-b3ae-45e0-b454-d20bf54b23f2
  - id: d3cdead0-685a-4489-9250-4bb709942f66
source-git-commit: 15a99ce130efaf3a35968cfc01747fe1b6ab93c9
workflow-type: tm+mt
source-wordcount: 607
ht-degree: 0%

---

# Observabilidad

La observabilidad es un aspecto crítico del funcionamiento de [!DNL Adobe Commerce as a Cloud Service]. Incluye la recopilación, el procesamiento y la visualización de datos de telemetría, incluidas las métricas, el registro y el seguimiento, para que pueda supervisar el estado de las aplicaciones, diagnosticar problemas de rendimiento y optimizar la fiabilidad de su plataforma de comercio y sus integraciones.

## [!DNL Adobe Commerce as a Cloud Service]

### Resumen de observabilidad

La observabilidad le ofrece visibilidad sobre el estado y el rendimiento de su tienda de Adobe Commerce y de todas las aplicaciones de App Builder conectadas. Al recopilar datos de telemetría en todo el ecosistema comercial, puede:

* **Rastree métricas** como tiempos de respuesta de API, tasas de solicitud y error y utilización de recursos para monitorear el rendimiento en tiempo real y detectar tendencias.
* **Centralice los registros** de su aplicación, infraestructura, CDN e integraciones en una sola vista para una solución de problemas más rápida.
* **Solicitudes de seguimiento** de extremo a extremo a medida que fluyen desde el front-end a través de Commerce y aplicaciones conectadas, lo que le ayuda a identificar cuellos de botella y errores antes de que afecten a los clientes.

En conjunto, estas funciones le ayudan a identificar y resolver problemas rápidamente, optimizar el rendimiento y garantizar una experiencia fiable para sus clientes. La [descripción general de la observabilidad](https://developer.adobe.com/commerce/extensibility/observability/) explica cómo [!DNL Adobe Commerce as a Cloud Service] usa OpenTelemetry para unificar esta colección de telemetría en las aplicaciones de eventos, webhooks y App Builder.

![Arquitectura de observabilidad](./assets/observability.png){width="600" zoomable="yes"}

Adobe Commerce admite las siguientes herramientas de observabilidad a través de OpenTelemetry:

* Elasticsearch
* Grafana
* Jaeger
* New Relic
* Prometeo
* Splunk
* Cremallera

### Configurar suscripciones

[Configure suscripciones de observabilidad](https://developer.adobe.com/commerce/extensibility/observability/configuration/) en [!UICONTROL Admin] o a través de la API de REST para enrutar registros, métricas o seguimientos a cualquier extremo compatible con OpenTelemetry. Cada suscripción se dirige a componentes específicos (enlaces web, eventos o [!UICONTROL Admin UI SDK]).

### API de REST de observabilidad

La [API de REST de observabilidad](https://developer.adobe.com/commerce/extensibility/observability/api/) proporciona extremos que crean, recuperan, actualizan y eliminan suscripciones de observabilidad mediante programación. Utilice estos extremos para automatizar la configuración en todas las instancias.

## Adobe Developer App Builder

### instrumentación de App Builder

[Implemente la observabilidad en [!DNL App Builder]](https://developer.adobe.com/commerce/extensibility/observability/app-builder/) para propagar el contexto de seguimiento de Commerce en sus [!DNL App Builder] acciones, de modo que los registros y los seguimientos de ambos sistemas se correlacionen en su plataforma de observabilidad. Abarca la instrumentación para integraciones basadas en ganchos web y en eventos.

[!DNL App Builder] también proporciona herramientas integradas para [administrar registros de aplicaciones](https://developer.adobe.com/app-builder/docs/guides/app_builder_guides/application_logging/logging), incluido el acceso a CLI y Developer Console, y el reenvío de registros a soluciones externas como Splunk, Azure y New Relic.

### Biblioteca de telemetría

La biblioteca [`@adobe/aio-lib-telemetry`](https://github.com/adobe/aio-lib-telemetry/blob/main/docs/usage.md) es lo que utilizan las acciones de App Builder para emitir registros y seguimientos compatibles con OpenTelemetry. Abarca la instalación, configuración y configuración del exportador.

### Desarrollo y pruebas locales

[Pruebe la configuración de observabilidad localmente](https://developer.adobe.com/commerce/extensibility/observability/local-development/) antes de implementar. Use [!DNL Grafana] para la visualización y el reenvío de túnel (por ejemplo, [!DNL Ngrok]) para recibir telemetría de una instancia remota de Commerce en su equipo de desarrollo.

## [!DNL API Mesh]

### Registro de malla de API

El [registro de malla de API](https://developer.adobe.com/graphql-mesh-gateway/mesh/advanced/logging/) le permite supervisar y depurar las solicitudes que fluyen por su malla mediante identificadores de rayo. Exporte los registros de forma masiva o reenvíelos a plataformas como [!DNL New Relic] para un análisis centralizado.

## Tienda

### CDN y monitorización de usuarios reales

[Supervisión de usuarios reales proxy (RUM)](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/content-delivery-network/#proxy-rum-through-the-origin-to-avoid-a-tls-handshake) recopilación de datos a través de su origen de CDN para eliminar un protocolo de enlace TLS adicional y mejorar la medición de rendimiento front-end.

## Vídeos de observabilidad

Los siguientes vídeos proporcionan información general de alto nivel sobre las ofertas de observabilidad en [!DNL Adobe Commerce as a Cloud Service]:

* [Vídeos de observabilidad de App Builder](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/observability/overview){target="_blank"}
* [Vídeos de API Mesh](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/extensibility/api-mesh/getting-started-api-mesh){target="_blank"}
