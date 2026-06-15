---
title: '[!DNL SaaS Data Export Guide]'
description: Obtenga información acerca del uso de la extensión  [!DNL data export] para servicios SaaS de Adobe Commerce que sincroniza datos entre Adobe Commerce y los servicios de Commerce conectados.
role: Admin, Developer
exl-id: 8a0067ba-90a4-48a6-8276-208d09abe6fc
TQID: https://experienceleague.adobe.com/OHE1GBUEd8hHFPwFlO9fJa3Y0wK2xZ0HOYnwUn0-DSk
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: c1256247-af4b-46d8-9dca-0c654ecfa157id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 69f39a6a62e05c86a0e2897d09079543b3d8830e
workflow-type: tm+mt
source-wordcount: 571
ht-degree: 0%

---

# Guía de [!DNL SaaS Data Export]

[!DNL SaaS data export] sincroniza datos entre una instancia de Adobe Commerce y los servicios de Commerce conectados. Al agregar Live Search, Product Recommendations, el servicio de catálogo o [!DNL Adobe Commerce Optimizer Connector] a una instalación de Adobe Commerce, la extensión [!DNL Data export] se instala automáticamente.

>[!NOTE]
>
>Si instala [!DNL Adobe Commerce Optimizer Connector], la misma extensión [!DNL Data Export] recopila las fuentes de catálogo y de precios de [!DNL Adobe Commerce]. A continuación, el conector asigna y envía esas fuentes a [!DNL Adobe Commerce Optimizer] mediante el Modelo de datos de catálogo maquetable (CCDM). Consulte [[!DNL Adobe Commerce Optimizer Connector] descripción general](../aco-connector/overview.md) para la configuración y arquitectura, y [Canalización de sincronización de conectores](../aco-connector/connector-sync-pipeline.md) para ver el comportamiento de sincronización después de la exportación.

La exportación de datos SaaS recopila y exporta varios tipos de datos, denominados _fuentes_, que agregan tipos de información específicos. Según los servicios de Commerce que estén instalados, las fuentes de exportación de datos SaaS incluyen:

- **Fuentes de entidades de catálogo** datos de productos agregados. Los datos incluyen productos, atributos de productos, precios de productos, variaciones de productos, categorías, permisos de categorías y permisos de productos.
- La fuente **Ámbitos** agrega datos para grupos de clientes, sitios web, tiendas y vistas de tiendas.
- **Fuente de pedidos de ventas** agrega datos de pedidos, incluidas las entidades relacionadas como facturas, envíos, notas de abono, etc.
- **Fuente de inventario de varios Source** agrega datos sobre los elementos de estado de inventario de stock.

La exportación de datos SaaS se entrega como una extensión PHP. Admite varios métodos para iniciar y administrar el proceso de sincronización de datos.

- **Sincronización manual desde el administrador o desde la línea de comandos**

   - El [panel de administración de datos](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard) del administrador de Commerce proporciona una vista gráfica del estado de sincronización que muestra los datos del producto sincronizados correctamente con los servicios de comercio. Puede usar el tablero para realizar una resincronización completa (_sincronización completa_) de todas las fuentes. Sin embargo, Adobe solo recomienda realizar una sincronización completa la primera vez que conecte Adobe Commerce a un servicio de Commerce. Consulte [Proceso de sincronización](data-synchronization.md).

     {{aco-data-sync-verification}}

   - La página [Estado de sincronización de fuentes de datos](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) proporciona información en tiempo real sobre el estado y el rendimiento de las fuentes de exportación de datos que transfieren datos de productos y categorías de Commerce a servicios externos como Product Recommendations, Live Search y Servicio de catálogo, o Adobe Commerce Optimizer.

   - La [herramienta de línea de comandos de Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/config-cli) (CLI) proporciona comandos para sincronizar fuentes específicas e incluye opciones adicionales para personalizar el procesamiento de fuentes.

- **Sincronización automatizada con trabajos cron**

   - [Sincronización parcial de datos](data-synchronization.md#partial-sync): los trabajos Cron almacenan en déclencheur una sincronización parcial de datos cuando un usuario administrador de Commerce actualiza una entidad. El proceso de exportación de datos envía solamente estas actualizaciones a los servicios de Commerce conectados. El proceso de sincronización parcial se basa en el mecanismo MView y no requiere acciones por parte del usuario administrador o del integrador de sistemas.

   - [Reintento automático para errores de sincronización](data-synchronization.md#retry-failed-items-sync): los trabajos Cron déclencheur el reintento automático del proceso de sincronización cuando se producen errores durante el proceso de sincronización de datos.

- **Programación y rendimiento de exportación**

   - Los desarrolladores e integradores de sistemas pueden calcular el tiempo necesario para que la exportación de datos SaaS sincronice los datos entre Adobe Commerce y los servicios conectados. Esta estimación puede ayudar a programar el procesamiento de exportación de datos para evitar interrupciones en el sitio. Ver [Estimar el volumen de datos y el tiempo de transmisión](estimate-data-volume-sync-time.md).

   - En los casos en los que la sincronización debe realizarse más rápidamente, la exportación de datos SaaS proporciona opciones de personalización para mejorar el rendimiento del procesamiento de exportación. Consulte [Mejorar el rendimiento de la exportación de datos](customize-export-processing.md).

- **Rastrear y solucionar problemas de actividades de exportación de datos**: utilice los registros de exportación de datos y saas para revisar el estado de sincronización y las cargas útiles de fuentes durante el proceso de sincronización e indexación. Consulte [Registro y solución de problemas](troubleshooting-logging.md).

