---
title: Coincidencia automática predeterminada
description: Descubra cómo la regla de coincidencia automática predeterminada permite una sincronización perfecta entre Adobe Commerce y la integración de AEM Assets, lo que garantiza que los recursos se vinculen automáticamente a las entidades de comercialización correctas.
feature: CMS, Media, Integration
exl-id: 8a18639b-f508-456e-8d22-18e3e0fdd515
source-git-commit: d426c7878f7a66fe1047673be7c5bf65ae1949a7
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---

# Coincidencia automática predeterminada

La integración de AEM Assets para Commerce proporciona un mecanismo de coincidencia automática predeterminado (**[!UICONTROL Match by product SKU]**) basado en la configuración de metadatos de **AEM Assets**. Esta regla habilita la sincronización perfecta entre **Adobe Commerce** y **AEM Assets**, lo que garantiza que los recursos se vinculen automáticamente a las entidades de comercialización correctas.

## Configuración del mecanismo de coincidencia automática

1. En el Administrador de Commerce, vaya a **[!UICONTROL Store]** > Configuración > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

1. Especifique **[!UICONTROL Match by SKU]** como regla coincidente.

   ![regla de coincidencia automatizada predeterminada](../assets/ootb-matching-rule.png){width="600" zoomable="yes"}

1. Introduzca el nombre del campo de metadatos utilizado para la identificación del recurso en los AEM Assets.

   >[!NOTE]
   >
   > Si se siguió el proceso de incorporación estándar, este valor debe establecerse en `commerce:skus`.

## Funcionamiento del mecanismo de coincidencia automática

Cuando la regla de coincidencia **[!UICONTROL Match by product SKU]** está configurada en el administrador de Commerce, los archivos de recursos de Commerce se sincronizan automáticamente de los AEM Assets al proyecto de Commerce en función de los metadatos de recursos configurados para cada archivo. Usted configura los metadatos de la ficha de AEM **Commerce** en el entorno de **autor de AEM Assets**:

1. En AEM Assets, actualice los metadatos de la imagen para agregar la asociación de Adobe Commerce estableciendo el campo `Eligible for Commerce` en `Yes`.

   ![Metadatos de ejemplo](../assets/metadata-commerce-yes.png){width="600" zoomable="yes"}

1. Configure los metadatos ([!UICONTROL SKU], [!UICONTROL position] y [!UICONTROL role]) que vinculan el recurso al SKU del producto asociado.

   >[!NOTE]
   >
   > Si un recurso se utiliza para varios productos, configure los metadatos de cada SKU asociado.

1. En la ficha `Basic`, establezca el valor predeterminado del campo _[!UICONTROL Review Status]_&#x200B;en `approved`.

   ![Metadatos de ejemplo](../assets/metadata-review-status.png){width="600" zoomable="yes"}

Este método garantiza que los recursos digitales se vinculen y muestren correctamente en Adobe Commerce. También permite a los comerciantes y especialistas en marketing administrar las funciones y el posicionamiento de recursos directamente en los AEM Assets, lo que proporciona un mecanismo coherente y centralizado para la selección y el orden de las imágenes en todos los canales de participación.
