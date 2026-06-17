---
title: Sincronización de datos con exportación de datos SaaS
description: Descubra cómo  [!DNL SaaS Data Export] recopila y sincroniza datos entre instancias de Adobe Commerce y servicios de Commerce conectados.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: 2ca7c92a-fb52-4055-ae16-11e99b38d161
TQID: https://experienceleague.adobe.com/wM71qxvduDr77EW6Y8mSNfBXlqkloC-PGOOBOl-mZQM
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088bid: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dcid: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c1579802-ddd4-4214-8a91-97b2066abe11id: d3cdead0-685a-4489-9250-4bb709942f66id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 879
ht-degree: 0%

---

# Sincronización de datos con exportación de datos SaaS

Al instalar un servicio [!DNL Adobe Commerce] que requiere exportación de datos, como Servicio de catálogo, Live Search o Recomendaciones de productos, se instala una colección de módulos de exportación de datos SaaS para administrar la recopilación de datos y el proceso de sincronización.

La exportación de datos de SaaS mueve continuamente los datos de producto de una instancia de Adobe Commerce a la plataforma de servicios de Commerce para mantener los datos actualizados. Por ejemplo, Recomendaciones de productos requiere información actual del catálogo para devolver con precisión las recomendaciones con los nombres, precios y disponibilidad correctos. Para obtener más información sobre la supervisión del proceso de sincronización, vea [Ver y administrar el proceso de sincronización](data-sync-manage.md).

El diagrama siguiente muestra el flujo de exportación de datos SaaS.

![Flujo de sincronización y recopilación de exportación de datos SaaS para Adobe Commerce](assets/data-export-flow.png){width="900" zoomable="yes"}

Cuando los datos del catálogo cambian en [!DNL Adobe Commerce], la sincronización pasa por estas fases.

1. **Detección de cambios de entidad**: el sistema Mview de Magento detecta cambios de fila en las tablas de base de datos suscritas (por ejemplo, `catalog_product_entity`) y escribe entradas en una tabla changelog.
1. **Indexación de fuentes**: el indizador de fuentes lee el registro de cambios, carga los datos de entidad de las tablas de origen y ensambla los elementos de fuente.
1. **Recopilación y transformación de datos**: los proveedores registrados en el esquema de fuentes [`et_schema.xml`](extensibility-and-customizations.md#feed-schema-overview) recopilan datos de campo.
1. **Anulación de duplicación de hash**: se calcula un hash de contenido para cada elemento de fuente. Los elementos cuyo hash no ha cambiado desde la última exportación se omiten, por lo que solo se transmiten los datos modificados.
1. **Envío HTTP**: los elementos de fuente se envían como lotes HTTP POST autenticados al servicio de ingesta de fuentes SaaS de Adobe.
1. **El estado persiste** - El estado de respuesta de la API se vuelve a escribir en la [tabla de fuentes](reference/feed-table-reference.md) para cada elemento.
1. **Reintento de error**: un trabajo cron programado vuelve a intentar automáticamente los elementos que no se pudieron exportar.

>[!NOTE]
>
>Para implementaciones de [!DNL Adobe Commerce Optimizer Connector], [!DNL SaaS Data Export] administra la detección de cambios de entidad y el ensamblado de fuentes. A continuación, el conector asigna fuentes al formato [!DNL Catalog Data Ingestion API] y las envía a [!DNL Adobe Commerce Optimizer]. Consulte [Canalización de sincronización de conectores](../aco-connector/connector-sync-pipeline.md) para el control de ámbito, el envío y la administración de errores.

>[!NOTE]
>
>Para garantizar una programación sin problemas y evitar interrupciones en las operaciones del sitio, Adobe recomienda estimar el volumen de datos y el tiempo de sincronización antes de iniciar cualquier sincronización de fuente de datos. Esta estimación es importante a la hora de planificar sincronizaciones iniciales o actualizaciones de catálogos a gran escala, como cambios masivos de precios. Para obtener más información, consulte [Calcular el volumen de datos y el tiempo de transmisión para la sincronización de datos](estimate-data-volume-sync-time.md)

## Modos de sincronización

La exportación de datos de SaaS tiene dos modos para procesar fuentes de entidades:

- **Modo de exportación inmediato**: en este modo, los datos se recopilan y se envían inmediatamente al servicio de Commerce en una sola iteración. Este modo acelera la entrega de actualizaciones de entidades al servicio Commerce y reduce el tamaño de almacenamiento de las tablas de fuentes.

- **Modo de exportación heredado**: en este modo, los datos se recopilan en un solo proceso. A continuación, un trabajo de cron envía los datos recopilados a los servicios de comercio conectados. En las entradas del registro de exportación de datos, las fuentes que utilizan el modo heredado están etiquetadas como `(legacy)`.

## Tipos de sincronización

La exportación de datos SaaS admite tres tipos de sincronización: sincronización completa, sincronización parcial y reintento de la sincronización de elementos fallidos.

### Sincronización completa

Después de conectar una instancia de Adobe Commerce al servicio de Commerce, realice una sincronización completa para enviar datos de fuente de entidad de Adobe Commerce al servicio conectado.

>[!NOTE]
>
>La sincronización completa se realiza principalmente en la fase de incorporación. Evite el uso regular para evitar la sobrecarga de la base de datos. Después de la sincronización inicial, los cambios en curso se sincronizan automáticamente mediante la sincronización parcial.

### Sincronización parcial {#partial-sync}

Con la sincronización parcial, la exportación de datos de SaaS envía automáticamente actualizaciones desde la aplicación de Commerce, como cambios de nombre de producto o actualizaciones de precios, a los servicios de comercio conectados.
Para que funcione la sincronización parcial, la aplicación de Commerce requiere la siguiente configuración:

- [La programación de tareas se habilita mediante trabajos cron](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/configuration.html)
- Todos los indexadores de exportación de datos SaaS están configurados en el modo `Update by Schedule`.

### Reintentar sincronización de elementos con errores {#retry-failed-items-sync}

La sincronización de elementos con errores de reintento utiliza un proceso independiente para reenviar los elementos que no se sincronizaron debido a errores durante el proceso de sincronización; por ejemplo, un error de aplicación, una interrupción de la red o un error del servicio SaaS. Los trabajos cron de `*_resend_failed_items` en el grupo `resync_failed_feeds_data_exporter` se encargan de esto automáticamente cada 5 minutos.

## Trabajos cron programados

Los siguientes grupos cron automatizan la canalización en una programación fija.

| Grupo Cron | Trabajo cron | Finalidad | Programación |
|---|---|---|---|
| `index` | `indexer_update_all_views` | Procesos Revisar los registros de cambios y las actualizaciones parciales de fuentes de déclencheur | Cada 1 minuto |
| `index` | `indexer_reindex_all_invalid` | Realiza una resincronización completa de los índices de fuentes marcados como &quot;Reindexación obligatoria&quot; | Cada 1 minuto |
| `resync_failed_feeds_data_exporter` | `*_resend_failed_items` | Detecta elementos de fuente con errores y los vuelve a enviar | Cada 5 minutos |
| `commerce_data_export` | `saas_data_exporter` | Envía datos para fuentes en modo heredado (pedidos, ámbitos) | Cada 5 minutos |
| `commerce_data_export` | `cleanup_deleted_feed_items` | Limpia los elementos de fuente eliminados sincronizados después del período de retención (7 días) | Todos los días a las 2:00 AM |

## Envío de fuentes y gestión de errores HTTP {#feed-submission-and-http-error-handling}

Los elementos de fuente se envían como lotes JSON autenticados comprimidos en Gzip a través de un POST HTTP. La siguiente tabla muestra cómo se asignan los códigos de respuesta HTTP al estado de exportación y al comportamiento de reintento.

| Código de estado | ¿Reintentar? | Significado |
|-------------|--------|---------------------------------------------------------------------------------------------------------------------|
| 200 | No | Aceptado correctamente |
| 400 | No | Fallo de validación o datos incorrectos: requiere una investigación manual. Consulte `var/log/saas-export-errors.log` para obtener detalles. |
| 429 | Sí | Se alcanzó el límite de velocidad - reducir `thread_count` en [exportar configuración de procesamiento](customize-export-processing.md) |
| 5xx | Sí | Error del lado de SaaS: reintento automático |
| 2 | Sí | Se ha programado el reintento del elemento |

Además de los errores de nivel HTTP, los errores de nivel de aplicación, como los errores de procesamiento local o las interrupciones de red, también están programados para su reintento automático por parte de los `*_resend_failed_items` trabajos cron.

Monitorice el estado de cada fuente desde la página [[!UICONTROL Data Feed Sync Status]](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) en el administrador de Commerce.

>[!MORELIKETHIS]
>
> - [Administrar sincronización](data-sync-manage.md): compruebe el estado de sincronización y vuelva a sincronizar las fuentes manualmente.
> - [Esquema de tabla de fuentes](reference/feed-table-reference.md): inspeccionar el estado de nivel de elemento y los detalles del error.
> - [Mejorar el rendimiento de la exportación de datos](customize-export-processing.md): ajuste el tamaño del lote y el recuento de subprocesos.
