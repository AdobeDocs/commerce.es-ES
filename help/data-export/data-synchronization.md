---
title: Sincronización de datos con exportación de datos SaaS
description: Descubra cómo  [!DNL SaaS Data Export] recopila y sincroniza datos entre instancias de Adobe Commerce y servicios SaaS conectados.
role: Admin, Developer
exl-id: 2ca7c92a-fb52-4055-ae16-11e99b38d161
source-git-commit: 291babe5dbdabb7d626ae744335b94e44ba6a6f5
workflow-type: tm+mt
source-wordcount: '881'
ht-degree: 0%

---

# Sincronización de datos con exportación de datos SaaS

Al instalar un servicio de Commerce que requiere la exportación de datos, como el servicio de catálogo, Live Search o Product Recommendations, se instala una colección de módulos de exportación de datos Saas para administrar la recopilación de datos y el proceso de sincronización.

La exportación de datos de SaaS mueve continuamente los datos de producto de una instancia de Adobe Commerce a la plataforma de servicios de Commerce para mantener los datos actualizados. Por ejemplo, Recomendaciones de productos requiere información actual del catálogo para devolver con precisión las recomendaciones con los nombres, precios y disponibilidad correctos. Use el [panel de administración de datos](https://experienceleague.adobe.com/es/docs/commerce/user-guides/data-services/catalog-sync) para observar y administrar el proceso de sincronización o la interfaz de línea de comandos para almacenar en déclencheur una sincronización y reindexar los datos de productos para que los consuman los servicios de Commerce.

El diagrama siguiente muestra el flujo de exportación de datos SaaS.

![Flujo de sincronización y recopilación de exportación de datos SaaS para Adobe Commerce](assets/data-export-flow.png){width="900" zoomable="yes"}

Los componentes principales del flujo de exportación de datos de SaaS incluyen:

- Módulos de exportación de datos SaaS que recopilan los datos de las fuentes de Adobe Commerce, ensamblan elementos de fuentes, escuchan actualizaciones y conservan el estado de la fuente.
- Los módulos de exportación SaaS exportan datos, configuran el enrutamiento y publican las fuentes en servicios conectados.
- El servicio Adobe Commerce administra el proceso de ingesta de datos para validar las fuentes entrantes y mantener las actualizaciones de los servicios conectados.

>[NOTA!]
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

Para que funcione la sincronización parcial, la aplicación de Commerce requiere la siguiente configuración:

- [La programación de tareas está habilitada a través de trabajos cron](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/configuration.html?lang=es)

- Todos los indexadores de exportación de datos SaaS están configurados en el modo `Update by Schedule`.

  En la versión de exportación de datos 103.1.0 y posterior de SaaS, el modo `Update by Schedule` está habilitado de forma predeterminada. Puede comprobar la configuración del índice en el servidor mediante el comando CLI de Commerce, `bin/magento indexer:show-mode | grep -i feed`

### Reintentar sincronización de elementos con errores

La sincronización de elementos con errores de reintento utiliza un proceso independiente para reenviar los elementos que no se sincronizaron debido a errores durante el proceso de sincronización; por ejemplo, un error de aplicación, una interrupción de la red o un error del servicio SaaS. La implementación de esta sincronización también se basa en trabajos cron.

- `resync_failed_feeds_data_exporter` trabajos del grupo cron:
   - El trabajo `<feed name>_feed_resend_failed_feeds_items` reenvía elementos que no se pudieron sincronizar, por ejemplo `products_feed_resend_failed_items`.

### Ver y administrar el proceso de sincronización

La mayoría de las actividades de sincronización se procesan automáticamente según la configuración de la aplicación. Sin embargo, la exportación de datos de SaaS también proporciona herramientas para administrar el proceso.

- Los usuarios administradores pueden ver y hacer un seguimiento del progreso de la sincronización y obtener información sobre los datos desde el [panel de administración de datos](https://experienceleague.adobe.com/es/docs/commerce-admin/systems/data-transfer/data-dashboard).

- Los desarrolladores, integradores de sistemas o administradores con acceso al servidor de aplicaciones de Commerce pueden administrar el proceso de sincronización y las fuentes de datos mediante la herramienta de línea de comandos (CLI) de Adobe Commerce. Consulte [Administrar operaciones de sincronización mediante la CLI de Commerce](data-export-cli-commands.md).

### Verifique la configuración de la aplicación Commerce

La sincronización parcial y la sincronización de elementos con error de reintento solo funcionan si la instancia de Commerce se ha configurado correctamente. Normalmente, la configuración se completa al configurar el servicio de Commerce. Si la exportación de datos no funciona correctamente, compruebe la siguiente configuración.

- [Confirme que los trabajos cron se están ejecutando](https://experienceleague.adobe.com/es/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues).

- Compruebe que los indexadores se estén ejecutando desde [Admin](https://experienceleague.adobe.com/es/docs/commerce-admin/systems/tools/index-management) o mediante el comando `bin/magento indexer:info` de la CLI de Commerce.

- Compruebe que los indizadores de las siguientes fuentes estén establecidos en `Update by Schedule`: Atributos de catálogo, Producto, Anulaciones de producto y Variante de producto. Puede comprobar los indizadores desde [Administración de índices](https://experienceleague.adobe.com/es/docs/commerce-admin/systems/tools/index-management) en el administrador o usando la CLI (`bin/magento indexer:show-mode | grep -i feed`).

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
