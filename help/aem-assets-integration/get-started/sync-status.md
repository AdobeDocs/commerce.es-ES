---
title: Ver estado de sincronización de AEM Assets
description: Revise los recursos sincronizados en una lista centrada en los recursos en el Administrador de Commerce.
feature: CMS, Media, Integration
source-git-commit: 446739ffad0da97e2e923e6e02be3f8f6b3eb2b3
workflow-type: tm+mt
source-wordcount: '330'
ht-degree: 0%

---


# Ver estado de sincronización de AEM Assets

La vista **[!UICONTROL Sync Status]** proporciona una lista de recursos sincronizados a través de la integración de AEM Assets centrada en recursos. Utilícelo para buscar, revisar y solucionar problemas de recursos mediante sus propios atributos en lugar de navegar producto por producto en el catálogo.

![Vista del estado de sincronización de AEM Assets](../assets/aem-assets-sync-status-view.png){width="700" zoomable="yes"}

>[!NOTE]
>
> [!UICONTROL Sync Status] no está disponible para [!DNL Adobe Commerce Optimizer].

## Abrir estado de sincronización

En la barra lateral _Admin_, vaya a **[!UICONTROL System]** > **[!UICONTROL AEM Assets]** > **[!UICONTROL Sync Status]**.

![Estado de sincronización de AEM Assets en el menú Sistema](../assets/aem-assets-configuration-admin-menu.png){width="600" zoomable="yes"}

## Estado de sincronización de integración

En la parte superior de la página, el banner **Estado de sincronización de AEM** resume el estado de la canalización y cuántos eventos están esperando a procesarse. Seleccione **[!UICONTROL Refresh]** para actualizar el banner de mantenimiento de sincronización.

## Lista de recursos

La cuadrícula enumera los recursos procesados por la canalización de sincronización de AEM Assets y su estado de sincronización actual. Cada fila representa un recurso y su estado de sincronización en Commerce. No representa un registro de producto.

| Columna | Descripción |
|--------|-------------|
| **ID de recurso** | Identificador de recurso de AEM (por ejemplo, `urn:aaid:aem:…`). |
| **Estado** | Resultado del último intento de sincronización del recurso. Los valores posibles son **Success**, **Failed** o **Waiting**. |
| **Procesando** | Fecha y hora en que se inició el procesamiento del recurso. |
| **Enviado** | Fecha y hora de envío del evento de sincronización. |
| **Error** | Mensaje de error cuando **Status** indica un error; vacío cuando la sincronización se realizó correctamente. |

### Filtrar recursos

1. Seleccione **[!UICONTROL Filters]** para expandir el panel de filtros.

1. Escriba un **ID de recurso** o elija un valor de **Estado**.

1. Seleccione **[!UICONTROL Apply Filters]** para actualizar la cuadrícula o **[!UICONTROL Cancel]** para cerrar el panel sin aplicar los cambios.

Los filtros se aplican a los datos de nivel de recurso, lo que permite aislar las sincronizaciones fallidas o rastrear un recurso específico sin abrir productos individuales.

## Sincronizaciones fallidas

Cuando **Status** muestre un error, revisa la columna **Error** en la cuadrícula para ver el mensaje devuelto por la canalización de sincronización.

Revise el mensaje de error completo y los detalles del último intento de sincronización para diagnosticar el error.

[!BADGE Solo PaaS]{type=Informative tooltip="Solo se aplica a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe)."} Para obtener información adicional sobre la solución de problemas, consulte [Coincidencia automática predeterminada](../synchronize/default-match.md). Los archivos de registro de integración están disponibles en `/var/log/aem-assets-integration.log` y `/var/log/aem-assets-integration-errors.log` en su instancia de Commerce.
