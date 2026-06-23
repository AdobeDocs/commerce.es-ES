---
title: Administrar  [!DNL Adobe Commerce Optimizer Connector] sincronización
description: Aprenda a verificar la sincronización de datos del catálogo y a resincronizar manualmente las fuentes de conectores entre  [!DNL Adobe Commerce] y [!DNL Adobe Commerce Optimizer].
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
subfeature_v2:
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 0bfd368c50707692c7a0adda6e70e3776bd9692a
workflow-type: tm+mt
source-wordcount: 349
ht-degree: 0%

---

# Administrar sincronización a [!DNL Commerce Optimizer]

Después de configurar [!DNL Adobe Commerce Optimizer Connector], la mayoría de las actualizaciones del catálogo se sincronizan automáticamente mediante trabajos cron programados. Para obtener más información sobre cómo funciona la sincronización automatizada, consulte [Canalización de sincronización de conectores](connector-sync-pipeline.md). Utilice las herramientas de este tema para comprobar que los datos llegan a [!DNL Adobe Commerce Optimizer] y para volver a sincronizar manualmente las fuentes cuando sea necesario.

## Compruebe que la sincronización de datos funciona {#verify-that-the-data-sync-is-working}

{{$include /help/_includes/aco-connector/verify-optimizer-data-sync.md}}

## Resincronizar datos manualmente {#manually-resync-data}

Cuando la sincronización parcial y los reintentos automáticos no resuelven los problemas de sincronización, puede volver a sincronizar manualmente los datos del catálogo. La opción que elija dependerá del origen del problema y de la cantidad de control que necesite.

| Tarea | Opción | Notas |
| --- | --- | --- |
| Verificar el estado de sincronización y volver a sincronizar desde el sistema ascendente cuando falten productos | **Sincronización ascendente del sistema** | En [!DNL Commerce Optimizer], seleccione **[!UICONTROL Data Sync]** y compruebe que se muestran los orígenes de catálogo, los productos, los precios y los atributos esperados. Cuando faltan productos, vuelva a sincronizar desde la instancia de [!DNL Adobe Commerce] ascendente mediante la página **[!UICONTROL Data Feed Sync Status]** o la CLI de Commerce (consulte las filas siguientes). |
| Resincronizar los elementos de fuente de conector problemáticos o con errores seleccionados | **[!UICONTROL Data Feed Sync Status]página en el administrador de Commerce** | Monitorice el estado de exportación y vuelva a sincronizar los elementos de fuente seleccionados del conector desde el administrador de Commerce. Ver [Verificar que la sincronización de datos funcione](#verify-that-the-data-sync-is-working). |
| Sincronización de fuentes de conector de destino con control operativo | **CLI de Commerce** | Ejecute `saas:resync` desde la instancia de Adobe Commerce para las fuentes de conectores. Ver [Fuentes de sincronización mediante la CLI de Commerce](../data-export/data-export-cli-commands.md) y [Fuentes compatibles](reference/connector-reference.md#supported-feeds). |

>[!MORELIKETHIS]
>
> - [Canalización de sincronización de conectores](connector-sync-pipeline.md): aprenda cómo funcionan la sincronización automatizada, las programaciones cron y la administración de errores
> - [Estimar el volumen de datos y el tiempo de sincronización](reference/estimate-data-volume-sync-time.md) — Calcular la duración de sincronización esperada
> - [Solución de problemas](troubleshooting.md): Diagnostique problemas de exportación de credenciales, sincronización y ámbito
> - [Módulos de conector y extremos de fuente](reference/connector-reference.md): revise módulos, extremos de API y fuentes admitidas
> - [Página de estado de sincronización de fuentes de datos en el administrador de Commerce](https://experienceleague.adobe.com/es/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status){target="_blank"}: Más información acerca de los campos y las funciones disponibles para supervisar el estado de las fuentes
> - [Panel de sincronización de datos en [!DNL Commerce Optimizer]](https://experienceleague.adobe.com/en/docs/commerce-optimizer/data-sync/data-sync){target="_blank"}: Documentación de referencia para campos y acciones disponibles para supervisar la sincronización de datos del catálogo
