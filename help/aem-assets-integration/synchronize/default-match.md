---
title: Coincidencia automática predeterminada
description: Descubra cómo la regla de coincidencia automática predeterminada permite una sincronización perfecta entre Adobe Commerce y la integración de AEM Assets, lo que garantiza que los recursos se vinculen automáticamente a las entidades de comercialización correctas.
feature: CMS, Media, Integration
exl-id: 8a18639b-f508-456e-8d22-18e3e0fdd515
TQID: 'https://experienceleague.adobe.com/z7vpuhsVJnKohiU-bKNrcGnoIQ5WAwcwiccYlvawN0U'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: ddbd0f6e-b569-5a04-8a70-55058777c373
    internal-label: CMS
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
source-git-commit: 5e9c42e5c93ac81604aa38bf3e55c5df729650a0
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%
---
# Coincidencia automática predeterminada

La integración de AEM Assets para Commerce proporciona un mecanismo de coincidencia automática predeterminado (**[!UICONTROL Match by product SKU]**) basado en la configuración de metadatos de **AEM Assets**. Esta regla habilita la sincronización perfecta entre **Adobe Commerce** y **AEM Assets**, lo que garantiza que los recursos se vinculen automáticamente a las entidades de comercialización correctas.

## Configuración del mecanismo de coincidencia automática

1. Desde Commerce Admin, vaya a **[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

1. Especifique **[!UICONTROL Match by product SKU]** como regla coincidente.

   ![Coincidencia por regla de SKU del producto y nombre de propiedad de metadatos](../assets/ootb-matching-rule.png){width="700" zoomable="yes"}

1. En **[!UICONTROL Match by product SKU attribute name]**, escriba el [nombre de propiedad de metadatos](../metadata.md) que almacena SKU de productos en AEM Assets, no un valor de SKU real.

   >[!NOTE]
   >
   > Si se siguió el proceso de incorporación estándar, este valor debe establecerse en `commerce:skus`.

## Funcionamiento del mecanismo de coincidencia automática

Cuando la regla de coincidencia **[!UICONTROL Match by product SKU]** está configurada en el administrador de Commerce, los archivos de recursos de Commerce se sincronizan automáticamente de los AEM Assets al proyecto de Commerce en función de los metadatos de recursos configurados para cada archivo. Usted configura los metadatos de la ficha de AEM **Commerce** en el entorno de **autor de AEM Assets**:

1. Abra la instancia de autor de AEM Assets (la dirección URL se aprovisiona para su proyecto en la misma organización de IMS que Adobe Commerce).

1. En la pantalla de navegación principal, haga clic en **Assets** para acceder a la interfaz de administración de activos digitales (DAM).

1. En AEM Assets, actualice los metadatos de la imagen para agregar la asociación de Adobe Commerce estableciendo el campo `Eligible for Commerce` en `Yes`.

   ![Metadatos de ejemplo](../assets/metadata-commerce-yes.png){width="600" zoomable="yes"}

1. Configure los metadatos ([!UICONTROL SKU], [!UICONTROL position] y [!UICONTROL role]) que vinculan el recurso al SKU del producto asociado.

   Las cuatro funciones estándar son `image`, `small_image`, `thumbnail` y `swatch_image`. Con la versión 1.4.6 y posteriores de la extensión de integración de AEM Assets, también puede introducir una función de imagen personalizada, como `hero` o `custom_role_1`. Consulte [Coincidencia automática personalizada](custom-match.md) para obtener más información.

   >[!NOTE]
   >
   > Si un recurso se utiliza para varios productos, configure los metadatos de cada SKU asociado.

1. En la ficha `Basic`, establezca el valor predeterminado del campo _[!UICONTROL Review Status]_&#x200B;en `approved`.

   ![Metadatos de ejemplo](../assets/metadata-review-status.png){width="600" zoomable="yes"}

Después de aprobar el recurso, [compruebe la asociación del producto, el resultado de la sincronización y la visualización de la tienda](../get-started/setup-synchronization.md#verify-the-integration). Si el recurso no aparece, revise [Estado de sincronización](../get-started/sync-status.md). Para Adobe Commerce Optimizer, usa el [flujo de trabajo de verificación del optimizador](../get-started/configure-aco.md#match-by-sku-workflow-example); el estado de sincronización no está disponible.

[!BADGE Solo PaaS]{type=Informative tooltip="Solo se aplica a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe)."} Para obtener más información sobre la solución de problemas de sincronización, revise los [registros de integración](../get-started/logs.md).
