---
title: Módulos de exportación de datos SaaS
description: Obtenga información acerca de los paquetes de módulos de Magento incluidos en  [!DNL SaaS Data Export]  y sus funciones en la recopilación, transformación y envío de datos a los servicios SaaS de Adobe.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Developer
feature: Services
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 111
ht-degree: 0%

---


# Módulos de exportación de datos SaaS

[!DNL SaaS Data Export] consta de dos grupos de módulos: primero para la recopilación y la indexación de datos y segundo para el transporte y el envío HTTP.

Estos módulos administran la detección de cambios de entidad, la indexación de fuentes, la extracción de datos y la definición de esquemas.
La siguiente tabla proporciona solo módulos de nivel de marco; la lista completa de módulos disponibles depende de los paquetes instalados.

| Módulo | Finalidad | Clases clave |
| --- | --- |--- |
| `DataExporter` | Marco principal: indexador, tabla de fuentes, hash, reintento, bloqueo | `FeedIndexer`, `FeedIndexMetadata`, `FeedMetadataPool`, `FeedLockManager` |
| `QueryXml` | DSL de consulta basado en XML para la recopilación de datos | `QueryFactory`, `QueryProcessor`, `SelectBuilder` |
| `SaaSCommon` | Transporte HTTP compartido, reintento, CLI (`saas:resync`), orquestación de resincronización | `ExportFeed`, `SubmitFeed`, `ResyncManager`, `ResyncManagerPool`, `ProgressBarManager` |

Para saber cómo funcionan juntos estos módulos durante la sincronización, consulte [Canalización de exportación de datos SaaS](../sync-overview.md).

>[!MORELIKETHIS]
>
>- [Funcionamiento de la sincronización](../sync-overview.md)
>- [Esquema de tabla de fuentes](feed-table-reference.md)
>- [Administrar la extensión de exportación de datos SaaS](../manage-extension.md)
