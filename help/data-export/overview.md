---
title: '[!DNL SaaS Data Export Guide]'
description: Obtenga información acerca del uso de la extensión  [!DNL data export] para servicios SaaS de Adobe Commerce que sincroniza datos entre Adobe Commerce y los servicios de Commerce conectados.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: 8a0067ba-90a4-48a6-8276-208d09abe6fc
TQID: https://experienceleague.adobe.com/OHE1GBUEd8hHFPwFlO9fJa3Y0wK2xZ0HOYnwUn0-DSk
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088bid: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2: id: c1256247-af4b-46d8-9dca-0c654ecfa157id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 402
ht-degree: 0%

---

# Guía de [!DNL SaaS Data Export]

[!DNL SaaS data export] sincroniza datos entre una instancia de Adobe Commerce y los servicios de Commerce conectados. Al agregar Live Search, Product Recommendations, el servicio de catálogo o [!DNL Adobe Commerce Optimizer Connector] a una instalación de Adobe Commerce, la extensión [!DNL Data Export] se instala automáticamente.

>[!NOTE]
>
>Si instala [!DNL Adobe Commerce Optimizer Connector], la misma extensión [!DNL Data Export] recopila las fuentes de catálogo y de precios de [!DNL Adobe Commerce]. A continuación, el conector asigna y envía esas fuentes a [!DNL Adobe Commerce Optimizer] mediante el Modelo de datos de catálogo maquetable (CCDM). Consulte [[!DNL Adobe Commerce Optimizer Connector] descripción general](../aco-connector/overview.md) para la configuración y arquitectura, y [Canalización de sincronización de conectores](../aco-connector/connector-sync-pipeline.md) para ver el comportamiento de sincronización después de la exportación.

La exportación de datos SaaS recopila y exporta varios tipos de datos, denominados _fuentes_, que agregan tipos de información específicos. Según los servicios de Commerce que estén instalados, las fuentes de exportación de datos SaaS incluyen:

- **Fuentes de entidades de catálogo** datos de productos agregados. Los datos incluyen productos, atributos de productos, precios de productos, variaciones de productos, categorías, permisos de categorías y permisos de productos.
- La fuente **Ámbitos** agrega datos para grupos de clientes, sitios web, tiendas y vistas de tiendas.
- **Fuente de pedidos de ventas** agrega datos de pedidos, incluidas las entidades relacionadas como facturas, envíos, notas de abono, etc.
- **Fuente de inventario de varios Source** agrega datos sobre los elementos de estado de inventario de stock.

La exportación de datos SaaS se entrega como una extensión PHP que admite sincronización automática y manual:

- **Sincronización automatizada**: después de la sincronización completa inicial al conectar un servicio de Commerce, los trabajos cron mantienen actualizados los servicios conectados mediante la sincronización parcial y el reintento automático de los elementos con errores, sin que se requiera ninguna acción por parte del usuario administrador o del integrador del sistema.

- **Sincronización manual**: ejecute una sincronización completa o vuelva a sincronizar las fuentes seleccionadas desde el administrador de Commerce o desde la [CLI de Commerce](data-export-cli-commands.md).

- **Supervisión**: efectúe el seguimiento del estado, el estado y el envío de la fuente desde la página [!UICONTROL Data Feed Sync Status] y el panel de administración de datos en el administrador de Commerce. Consulte [Administrar sincronización](data-sync-manage.md) para ver los pasos de verificación y resincronización.

Para ver el comportamiento de sincronización, los modos y el diagrama de flujo de exportación, consulte [Funcionamiento de la sincronización](sync-overview.md).

La exportación de datos de SaaS también proporciona herramientas para planificar y solucionar problemas del proceso de sincronización:

- **Programación y rendimiento**: calcule el tiempo de sincronización para programar el procesamiento y evitar la interrupción del sitio, y personalice el procesamiento de exportación para mejorar el rendimiento. Ver [Calcular volumen de datos y tiempo de transmisión](estimate-data-volume-sync-time.md) y [Mejorar rendimiento de exportación de datos](customize-export-processing.md).

- **Seguimiento y solución de problemas**: revise el estado de sincronización y las cargas útiles de fuentes mediante los registros de exportación de datos y saas. Ver [Revisar registros y solucionar problemas](troubleshooting/logging.md).

>[!MORELIKETHIS]
>
> - [Ampliar y personalizar fuentes de exportación de datos SaaS](extensibility-and-customizations.md): agregue o modifique datos de fuentes.
> - [Situaciones de solución de problemas](troubleshooting/troubleshooting-scenarios.md): diagnostique la configuración incorrecta y los resultados de sincronización inesperados.
> - [Notas de la versión](release-notes.md): actualizaciones de la extensión y problemas conocidos.
