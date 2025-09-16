---
title: '[!DNL SaaS Data Export Guide]'
description: Obtenga información acerca del uso de la extensión  [!DNL data export] para servicios SaaS de Adobe Commerce que sincroniza datos entre Adobe Commerce y los servicios de Commerce conectados.
role: Admin, Developer
exl-id: 8a0067ba-90a4-48a6-8276-208d09abe6fc
source-git-commit: 8e3e71c7de56b367a73ab048fa13ba2cdeb55f41
workflow-type: tm+mt
source-wordcount: '433'
ht-degree: 0%

---

# Guía de [!DNL SaaS Data Export]

[!DNL SaaS data export] sincroniza datos entre una instancia de Adobe Commerce y los servicios de Commerce conectados. Al agregar Live Search, Product Recommendations o el servicio de catálogo a una instalación de Adobe Commerce, la extensión [!DNL Data export] se instala automáticamente.

La exportación de datos SaaS recopila y exporta varios tipos de datos, denominados _fuentes_, que agregan tipos de información específicos. Según los servicios de Commerce que estén instalados, las fuentes de exportación de datos SaaS incluyen:

- **Fuentes de entidades de catálogo** datos de productos agregados. Los datos incluyen productos, atributos de productos, precios de productos, variaciones de productos, categorías, permisos de categorías y permisos de productos.
- La fuente **Ámbitos** agrega datos para grupos de clientes, sitios web, tiendas y vistas de tiendas.
- **Fuente de pedidos de ventas** agrega datos de pedidos, incluidas las entidades relacionadas como facturas, envíos, notas de abono, etc.
- **Fuente de inventario de varios Source** agrega datos sobre los elementos de estado de inventario de stock.

La exportación de datos SaaS se entrega como una extensión PHP. Admite varios métodos para iniciar y administrar el proceso de sincronización de datos.

- **Sincronización manual desde el administrador o desde la línea de comandos**

   - El [panel de administración de datos](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard) del administrador de Commerce proporciona una vista gráfica del estado de sincronización. Puede usar el tablero para realizar una resincronización completa (_sincronización completa_) de todas las fuentes. Sin embargo, Adobe solo recomienda realizar una sincronización completa la primera vez que conecte Adobe Commerce a un servicio de Commerce. Consulte [Proceso de sincronización](data-synchronization.md).

   - La [herramienta de línea de comandos de Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/config-cli) (CLI) proporciona comandos para sincronizar fuentes específicas e incluye opciones adicionales para personalizar el procesamiento de fuentes.

- **Sincronización automatizada con trabajos cron**

   - [Sincronización parcial de datos](data-synchronization.md#partial-synchronization-with-cron-jobs): los trabajos Cron almacenan en déclencheur una sincronización parcial de datos cuando un usuario administrador de Commerce actualiza una entidad. El proceso de exportación de datos envía solamente estas actualizaciones a los servicios de Commerce conectados. El proceso de sincronización parcial se basa en el mecanismo MView y no requiere acciones por parte del usuario administrador o del integrador de sistemas.

   - [Reintento automático para errores de sincronización](data-synchronization.md#failed-items-sync-for-error-recovery): los trabajos Cron déclencheur el reintento automático del proceso de sincronización cuando se producen errores durante el proceso de sincronización de datos.

- **Programación y rendimiento de exportación**

   - Los desarrolladores e integradores de sistemas pueden calcular el tiempo necesario para que la exportación de datos SaaS sincronice los datos entre Adobe Commerce y los servicios conectados. Esta estimación puede ayudar a programar el procesamiento de exportación de datos para evitar interrupciones en el sitio. Ver [Estimar el volumen de datos y el tiempo de transmisión](estimate-data-volume-sync-time.md).

   - En los casos en los que la sincronización debe realizarse más rápidamente, la exportación de datos SaaS proporciona opciones de personalización para mejorar el rendimiento del procesamiento de exportación. Consulte [Mejorar el rendimiento de la exportación de datos](customize-export-processing.md).

- **Rastrear y solucionar problemas de actividades de exportación de datos**: utilice los registros de exportación de datos y saas para revisar el estado de sincronización y las cargas útiles de fuentes durante el proceso de sincronización e indexación. Consulte [Registro y solución de problemas](troubleshooting-logging.md).
