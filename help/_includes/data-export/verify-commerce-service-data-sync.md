---
source-git-commit: e7d9c056ef8d565b4a143b05ff4e06d607fbfa8e
workflow-type: tm+mt
source-wordcount: '139'
ht-degree: 0%

---
# Verificar sincronización de datos del servicio Commerce

Para comprobar que la sincronización de datos funciona, confirme que los datos exportados correctamente desde [!DNL Adobe Commerce] y que se entregaron correctamente al servicio conectado de Commerce. Utilice los paneles de la implementación para comprobar ambos pasos.

Comience con la exportación y confirme la entrega.

1. Compruebe el estado de sincronización en el Administrador de Commerce.

   Vaya a **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Feed Sync Status]**.

   ![Página de estado de sincronización de fuente de datos con informes de estado de elemento de fuente](/help/data-export/assets/data-feed-sync-status.png){width="800" zoomable="yes"}

   Cuando se está ejecutando la sincronización, los datos de la fuente muestran los registros enviados correctamente. Seleccione una fuente para ver los detalles o solucionar problemas de sincronización.

1. Confirme que los datos se han enviado a los servicios conectados de Commerce.

   Desde Commerce Admin, vaya a **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Management Dashboard]**.

   ![Panel de administración de datos que muestra datos de catálogo sincronizados en servicios de Commerce conectados](/help/data-export/assets/data-management-dashboard.png){width="700" zoomable="yes"}

   Compruebe que aparecen los productos, precios y atributos esperados.

>[!TIP]
>
>Si tiene algún problema adicional con la sincronización de datos, consulte [Revisar registros y solucionar problemas](/help/data-export/troubleshooting/logging.md).

