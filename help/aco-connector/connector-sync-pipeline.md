---
title: Canalización de sincronización de catálogos
description: Aprenda cómo funciona la canalización de sincronización  [!DNL Adobe Commerce Optimizer Connector] incluyendo la transformación de fuentes, las programaciones de cron, el control de ámbito y la gestión de errores.
feature: Integration, Configuration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."
autotag-review: '2026-06-09T16:21:52.214Z'
TQID: 'https://experienceleague.adobe.com/EXUQzAd0I6Hnq4twzhaBZZnv0jLjeGBuTx-QgQz-5MA'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2:
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: addc3a3a-2b1c-4fdf-aea4-4b1eb2931ba6
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 662
ht-degree: 1%

---

# Canalización de sincronización de conector

Compilado en [[!DNL SaaS Data Export]](https://experienceleague.adobe.com/en/docs/commerce/saas-data-export/overview), **[!DNL Adobe Commerce Optimizer Connector]** asigna los datos recopilados por los indizadores [!DNL SaaS Data Export] al formato requerido por [!DNL Adobe Commerce Optimizer] [!DNL Catalog Data Ingestion API] y administra la autenticación, el envío por lotes y el control de sincronización basado en el ámbito. Las secciones siguientes describen cómo funciona esa sincronización.

Contexto relacionado:

- Obtenga información acerca del valor comercial, las características clave y la arquitectura de la integración en el tema [[!DNL Commerce Optimizer Connector] descripción general](overview.md).

- Para ver los nombres de paquetes de módulos, extremos de API de fuentes y rutas de claves de configuración, consulte [Referencia del conector](reference/connector-reference.md)

## Funcionamiento de la sincronización

El diagrama siguiente muestra la sincronización de datos de [!DNL Adobe Commerce] a [!DNL Commerce Optimizer] a través de [!DNL Adobe I/O Gateway].

![Diagrama de sincronización de alto nivel del conector Commerce Optimizer](assets/aco-connector-sync-high-level-diagram.png){width="800" zoomable="yes"}

Cuando los datos del catálogo cambian en [!DNL Adobe Commerce], la sincronización pasa por estas fases.

1. **Detección de cambio de entidad** — (cada 1 min) Un trabajo cron (`indexer_reindex_all_invalid`) detecta [!DNL Adobe Commerce] cambios de entidad y déclencheur [!DNL SaaS Data Export], que ensambla elementos de fuente.
1. **Transformación**: [!DNL Commerce Optimizer Connector] recoge las fuentes ensambladas, asigna las entidades y ámbitos de [!DNL Adobe Commerce] a los formatos requeridos por la API de [!DNL Commerce Optimizer] y prepara la carga útil para la transmisión.
1. **Transmisión**: los datos transformados se envían a través de HTTP POST (`/v1/catalog/<feed name>`) a través de [!DNL Adobe I/O Gateway] a [!DNL Commerce Optimizer], lo que valida y mantiene las fuentes entrantes.
1. **Persistir resultados** — Mantener el estado de respuesta de API en [tablas de fuentes](reference/connector-reference.md#supported-feeds).
1. **Reintento de error** (cada 5 minutos): un trabajo cron independiente (`*_resend_failed_items`) detecta los elementos de fuente con errores y los vuelve a enviar a través de la misma canalización.

### Trabajos cron programados

Los siguientes trabajos cron automatizan la canalización en una programación fija.

| Grupo Cron | Trabajo de cron | Finalidad | Programación |
|-------------------------------------|-------------------------------|------------------------------------------------------------------------------|----------------|
| `index` | `indexer_update_all_views` | Escucha actualizaciones de entidad, ensambla elementos de fuente y mantiene el estado de la fuente | Cada 1 minuto |
| `index` | `indexer_reindex_all_invalid` | Realice una resincronización completa de los índices de fuentes marcados como &quot;Reindexación obligatoria&quot; | Cada 1 minuto |
| `resync_failed_feeds_data_exporter` | `*_resend_failed_items` | Comprueba los elementos de fuente con errores y los vuelve a enviar a [!DNL Commerce Optimizer] | Cada 5 minutos |
| `commerce_data_export` | `cleanup_deleted_feed_items` | Limpia los elementos de fuente eliminados sincronizados después del período de retención (7 días) | Todos los días a las 2:00 AM |

La extensión **[!DNL SaaS Data Export]** administra la colección de fuentes y el seguimiento de estado. La capa de conexión asigna entidades y ámbitos al formato requerido por la API [!DNL Commerce Optimizer] y los envía a través de `POST /v1/catalog/<feed name>`.

#### Requisitos

- [Commerce cron debe estar ejecutándose](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues){target="_blank"}.
- Los indexadores de fuente deben utilizar el modo **[!UICONTROL Update by Schedule]**. Consulte [Sincronización parcial](../data-export/sync-overview.md#partial-sync){target="_blank"}.

## Control de sincronización basado en el ámbito

El módulo `CommerceOptimizerScopeMapper` lee la configuración de exportación por sitio web y por vista de tienda y la aplica durante la recopilación y el envío de fuentes.

- **Ámbitos habilitados** exportan datos en la programación delta normal.
- **Los ámbitos deshabilitados** se han excluido de la canalización.
Las entidades sincronizadas anteriormente se eliminarán de [!DNL Commerce Optimizer] en la siguiente ejecución de cron.

Si los problemas de sincronización afectan solamente a un origen de catálogo o libro de precios, vea [Los datos no se sincronizan](troubleshooting.md#data-not-syncing).

Para obtener más información sobre cómo personalizar el ámbito de sincronización, vea [Personalizar la configuración de exportación de los ámbitos de Commerce](get-started.md#customize-the-commerce-scopes-export-configuration).

## Programación y monitorización

| Escenario | Intervalo típico |
| -------- | -------------- |
| Actualizaciones rutinarias del catálogo | 1-2 ciclos de sincronización delta (~1-2 minutos para la indexación, más el envío) |
| Errores transitorios | Se vuelve a intentar cada 5 minutos |
| Sincronización completa para catálogos grandes | De minutos a horas |

Monitorice el estado de cada fuente desde la página [[!UICONTROL Data Feed Sync Status]](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) en el administrador de Commerce. Ver [Verificar que la sincronización de datos funcione](./data-sync-manage.md#verify-that-the-data-sync-is-working).

## Envío de fuentes y gestión de errores

El proceso `FeedSubmitter` administra [!DNL Catalog Data Ingestion API] llamadas.

1. Separa los elementos de actualización de los elementos de eliminación (diferentes extremos de API).
1. Las llamadas actualizan y eliminan puntos finales de forma independiente.
1. Combina los resultados de estado por elemento en una sola respuesta.

### Combinación del código de estado HTTP

Cuando las llamadas de actualización y eliminación devuelven códigos de estado diferentes, `FeedSubmitter` combina los resultados de la siguiente manera.

| Actualiza el resultado | Elimina el resultado | Resultado final |
| --------------- | --------------- | ------------- |
| 200 | 200 o ninguno | 200 con éxito |
| 200 | 400 | 200 con errores de eliminación |
| 400 | 400 | 400 errores combinados |
| otro | otro | REINTENTABLE |

| Tipo de error | Comportamiento |
| ---------- | -------- |
| **400** | Los elementos enumerados en el campo de respuesta `errors` aparecen en el Administrador y requieren atención. Se vuelven a intentar otros elementos del lote. |
| **5xx** | Lo han vuelto a intentar los trabajos cron `*_feed_resend_failed_items` específicos de la fuente en el grupo `resync_failed_feeds_data_exporter`. |

>[!MORELIKETHIS]
>
> - [Descripción general del conector](overview.md): aprenda el contexto empresarial y la asignación de ámbito
> - [Referencia de conector](reference/connector-reference.md): revise módulos, extremos de API y claves de configuración
> - [Personalizar la configuración de exportación de los ámbitos de Commerce](./get-started.md#customize-the-commerce-scopes-export-configuration): configure fuentes por nivel de ámbito, habilite y deshabilite el comportamiento y los pasos de administración
> - [Solución de problemas](troubleshooting.md) — Diagnóstico de errores de sincronización
