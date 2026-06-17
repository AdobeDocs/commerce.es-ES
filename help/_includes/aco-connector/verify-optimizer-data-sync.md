---
source-git-commit: 3d05a7307e58ea2758ac4b6f2b70d24b8ea7a5ac
workflow-type: tm+mt
source-wordcount: '144'
ht-degree: 0%

---
# Verificar sincronización de datos del Optimizador

Confirme que los datos exportados correctamente desde el administrador de Commerce y que los datos se entregaron correctamente a [!DNL Commerce Optimizer]. Comience con la exportación en el administrador de Commerce y confirme la entrega en [!DNL Commerce Optimizer].

1. **Comprobar el estado de sincronización en el administrador de Commerce:**

   Vaya a **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Feed Sync Status]**.

   ![Página de estado de sincronización de fuente de datos con informes de estado de elemento de fuente](/help/aco-connector/assets/data-feed-sync-status.png){width="700" zoomable="yes"}

   Cuando se está ejecutando la sincronización, los datos de la fuente muestran los registros enviados correctamente. Seleccione una fuente para ver los detalles o solucionar problemas de sincronización.

1. **Confirmar datos entregados a [!DNL Commerce Optimizer]:**

   En el menú [!DNL Commerce Optimizer], seleccione **[!UICONTROL Data Sync]**.

   ![Página de sincronización de datos en Adobe Commerce Optimizer que muestra datos de catálogo sincronizados](/help/aco-connector/assets/data-sync.png){width="700" zoomable="yes"}

   Compruebe que aparecen los productos, precios y atributos esperados.

Cuando la sincronización funciona según lo esperado:

- **[!UICONTROL Data Feed Sync Status]** muestra los registros enviados correctamente para las fuentes de conectores, sin errores de nivel de elemento sin resolver.
- **[!UICONTROL Data Sync]** en [!DNL Commerce Optimizer] enumera los orígenes de catálogo, los productos, los precios y los atributos esperados.

>[!TIP]
>
>Si tiene algún problema con la sincronización de datos, consulte la guía [Solución de problemas](/help/aco-connector/troubleshooting.md).
