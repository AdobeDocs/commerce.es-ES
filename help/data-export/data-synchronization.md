---
title: Sincronización de datos con exportación de datos SaaS
description: Descubra cómo  [!DNL SaaS Data Export] recopila y sincroniza datos entre instancias de Adobe Commerce y servicios SaaS conectados.
role: Admin, Developer
exl-id: 2ca7c92a-fb52-4055-ae16-11e99b38d161
TQID: https://experienceleague.adobe.com/wM71qxvduDr77EW6Y8mSNfBXlqkloC-PGOOBOl-mZQM
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: d3cdead0-685a-4489-9250-4bb709942f66
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 69f39a6a62e05c86a0e2897d09079543b3d8830e
workflow-type: tm+mt
source-wordcount: 1104
ht-degree: 0%

---

# Sincronización de datos con exportación de datos SaaS

Al instalar un servicio de Commerce que requiere la exportación de datos, como el servicio de catálogo, Live Search o Product Recommendations, se instala una colección de módulos de exportación de datos Saas para administrar la recopilación de datos y el proceso de sincronización.

La exportación de datos de SaaS mueve continuamente los datos de producto de una instancia de Adobe Commerce a la plataforma de servicios de Commerce para mantener los datos actualizados. Por ejemplo, Recomendaciones de productos requiere información actual del catálogo para devolver con precisión las recomendaciones con los nombres, precios y disponibilidad correctos. Para obtener más información sobre la supervisión del proceso de sincronización, vea [Ver y administrar el proceso de sincronización](#view-and-manage-the-synchronization-process).


El diagrama siguiente muestra el flujo de exportación de datos SaaS.

![Flujo de sincronización y recopilación de exportación de datos SaaS para Adobe Commerce](assets/data-export-flow.png){width="900" zoomable="yes"}

Los componentes principales del flujo de exportación de datos de SaaS incluyen:

- Módulos de exportación de datos SaaS que recopilan los datos de las fuentes de Adobe Commerce, ensamblan elementos de fuentes, escuchan actualizaciones y conservan el estado de la fuente.
- Los módulos de exportación SaaS exportan datos, configuran el enrutamiento y publican las fuentes en servicios conectados.
- El servicio Adobe Commerce administra el proceso de ingesta de datos para validar las fuentes entrantes y mantener las actualizaciones de los servicios conectados.

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

### Sincronización parcial

Con la sincronización parcial, la exportación de datos de SaaS envía automáticamente actualizaciones desde la aplicación de Commerce, como cambios de nombre de producto o actualizaciones de precios, a los servicios de comercio conectados.

El proceso de exportación de datos utiliza los siguientes trabajos cron para automatizar la operación de sincronización parcial.

- trabajos del grupo cron &quot;index&quot;:
   - El trabajo `indexer_reindex_all_invalid` reindexa todas las fuentes no válidas. Es un trabajo cron estándar de Adobe Commerce.
   - El trabajo de `saas_data_exporter` es para fuentes de exportación heredadas.
   - El trabajo `sales_data_exporter` es específico de la fuente de exportación de datos de ventas.

Estos trabajos se ejecutan cada minuto.

Se ejecutaron los mismos trabajos cron de sincronización parcial para [!DNL Adobe Commerce Optimizer Connector] fuentes. Para el envío y la administración de errores específicos del conector, consulte [Canalización de sincronización de conectores](../aco-connector/connector-sync-pipeline.md).

Para que funcione la sincronización parcial, la aplicación de Commerce requiere la siguiente configuración:

- [La programación de tareas se habilita mediante trabajos cron](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/configuration.html)

- Todos los indexadores de exportación de datos SaaS están configurados en el modo `Update by Schedule`.

  En la versión de exportación de datos 103.1.0 y posterior de SaaS, el modo `Update by Schedule` está habilitado de forma predeterminada. Puede comprobar la configuración del índice en el servidor mediante el comando CLI de Commerce, `bin/magento indexer:show-mode | grep -i feed`

### Reintentar sincronización de elementos con errores

La sincronización de elementos con errores de reintento utiliza un proceso independiente para reenviar los elementos que no se sincronizaron debido a errores durante el proceso de sincronización; por ejemplo, un error de aplicación, una interrupción de la red o un error del servicio SaaS. La implementación de esta sincronización también se basa en trabajos cron.

- `resync_failed_feeds_data_exporter` trabajos del grupo cron:
   - El trabajo `<feed name>_feed_resend_failed_feeds_items` reenvía elementos que no se pudieron sincronizar, por ejemplo `products_feed_resend_failed_items`.

### Ver y administrar el proceso de sincronización

La mayoría de las actividades de sincronización se procesan automáticamente según la configuración de la aplicación. Sin embargo, la exportación de datos de SaaS también proporciona herramientas para monitorizar y administrar el proceso.

- [!BADGE Solo PaaS]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."} **[Panel de administración de datos](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard)**: los usuarios administradores pueden ver y rastrear los datos sincronizados con los servicios de Commerce y disponibles para los servicios de tienda. Este panel muestra el producto sincronizado con los servicios de Commerce.

  {{aco-data-sync-verification}}

- [!BADGE Solo SaaS]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Se aplica a los proyectos de Adobe Commerce integrados con Adobe Commerce Optimizer (infraestructura SaaS administrada por Adobe)."} **[Página de estado de sincronización de fuentes de sincronización de datos](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/data-sync)**: en el caso de proyectos de Commerce que usen [!DNL Adobe Commerce Optimizer], comprueba la disponibilidad de los datos del catálogo para tu tienda desde la página de estado de sincronización de fuentes de datos en Adobe Commerce Optimizer. Este panel muestra el estado de sincronización de las fuentes de exportación de datos.

>[!NOTE]
>
>El panel de administración de datos solo está disponible si tiene instalado Live Search, Product Recommendations o el servicio de catálogo. El panel Estado de sincronización de fuentes de datos está disponible si tiene estos servicios o el [conector de Adobe Commerce Optimizer](../aco-connector/overview.md) instalado. Para conocer el comportamiento de la canalización del conector del Optimizador, incluidos los errores de control de ámbito y envío, consulte [Canalización de sincronización de conectores](../aco-connector/connector-sync-pipeline.md).

### Verifique la configuración de la aplicación Commerce

La sincronización parcial y la sincronización de elementos con error de reintento solo funcionan si la instancia de Commerce se ha configurado correctamente. Normalmente, la configuración se completa al configurar el servicio de Commerce. Si la exportación de datos no funciona correctamente, compruebe la siguiente configuración.

- [Confirme que los trabajos cron se están ejecutando](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues).

- Compruebe que los indexadores se estén ejecutando desde [Admin](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) o mediante el comando `bin/magento indexer:info` de la CLI de Commerce.

- Compruebe que los indizadores de las siguientes fuentes estén establecidos en `Update by Schedule`: Atributos de catálogo, Producto, Anulaciones de producto y Variante de producto. Puede comprobar los indizadores desde [Administración de índices](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) en el administrador o usando la CLI (`bin/magento indexer:show-mode | grep -i feed`).

### Notificaciones del administrador de eventos para el registro de transferencia de datos

En la versión 103.3.4 y posterior de, la exportación de datos de SaaS distribuye el evento `data_sent_outside` cuando se envían datos desde la instancia de Commerce a los servicios de Adobe Commerce.

```php
$this->eventManager->dispatch(
   "data_sent_outside",
   [
       "timestamp" => time(),
       "type" => $metadata->getFeedName(),
       "data" => $data
   ]
);
```

>[!NOTE]
>
>Para obtener información sobre los eventos y cómo suscribirse a ellos, consulte [Eventos y observadores](https://developer.adobe.com/commerce/php/development/components/events-and-observers) en la documentación para desarrolladores de Adobe Commerce.

