---
title: Configuración de la integración
description: Obtenga información sobre cómo conectar el proyecto de Adobe Commerce y los proyectos de Experience Manager Assets para habilitar la sincronización de recursos entre estos dos sistemas.
feature: CMS, Media
exl-id: 3533d010-926f-4d78-935c-98a9b7040d27
TQID: 'https://experienceleague.adobe.com/MM-neGrH-N8xBcCwLgnsaIrIjhbX6uYL5kS41QdV79I'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: ddbd0f6e-b569-5a04-8a70-55058777c373
    internal-label: CMS
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
subfeature_v2:
  - id: ae62cf09-5996-4921-bda8-fbe67b62e470
    internal-label: Storefront configuration
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: 5e9c42e5c93ac81604aa38bf3e55c5df729650a0
workflow-type: tm+mt
source-wordcount: '1355'
ht-degree: 1%
---
# Configuración de la integración

Configure la integración conectando Commerce a la instancia de AEM Assets y seleccionando la estrategia de coincidencia para la sincronización de recursos.

Después de identificar el proyecto de AEM Assets, seleccione la regla de coincidencia para sincronizar los recursos entre Adobe Commerce y los AEM Assets.

* **[!UICONTROL Match by product SKU]**: regla predeterminada que coincide con el SKU de los metadatos del recurso con el [SKU del producto de Commerce](https://experienceleague.adobe.com/es/docs/commerce-operations/implementation-playbook/glossary#sku) para garantizar que los recursos estén asociados con los productos correctos.

* **[!UICONTROL Custom match]**: regla de coincidencia para escenarios más complejos o requisitos empresariales específicos que requieren una lógica de coincidencia personalizada. La implementación de la coincidencia personalizada requiere el desarrollo de código personalizado en Adobe Developer App Builder para definir cómo se comparan los recursos con los productos. Consulte [Coincidencia automática personalizada](../synchronize/custom-match.md).

Para la configuración inicial, use la regla predeterminada **[!UICONTROL Match by product SKU]**.

## Requisitos

Antes de configurar la integración de AEM Assets, compruebe que ha completado los siguientes pasos:

* [Configuración del proyecto de AEM Assets](configure-aem.md)

* [!BADGE Solo PaaS]{type=Informative tooltip="Solo se aplica a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe)."} [Instale paquetes de Adobe Commerce](configure-commerce.md) para agregar la extensión y generar las credenciales y conexiones necesarias para usar la extensión.

* [Permisos de usuario e IMS](permissions.md): configure los permisos necesarios para el Selector de recursos, la selección del entorno de AEM y la asignación de dominios.

## Configuración de la conexión

![AEM Assets Configuración de integración con valores de dominio y entorno de ejemplo](../assets/aem-assets-view.png){width="900" zoomable="yes"}

1. Desde Commerce Admin, vaya a **[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

>[!INFO]
>
> La integración de AEM Assets solo admite la configuración en el ámbito global (predeterminado). No se admite la configuración en el nivel de sitio web. Cuando intenta configurar la integración en el nivel de sitio web, el sistema ignora la configuración del nivel de sitio web y utiliza los valores de configuración globales en su lugar.

1. [!BADGE Solo PaaS]{type=Informative tooltip="Solo se aplica a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe)."} Escriba **[!UICONTROL Asset Selector IMS Client ID]**.

   Este ID es necesario para habilitar el Selector de recursos. Consulte [Permisos de usuario e IMS](permissions.md) para obtener este ID. Para obtener más información sobre el Selector de recursos, consulte [Selección manual de recursos](../synchronize/asset-selector-integration.md).

1. En **[!UICONTROL AEM Environment]**, seleccione el entorno configurado en [Configurar el proyecto de AEM Assets](configure-aem.md).

   La lista incluye entornos de AEM para los que el usuario tiene un perfil de producto Autor o Entrega. Si falta el entorno esperado, revise [permisos de usuario e IMS](permissions.md).

   Si su configuración muestra campos **[!UICONTROL Program ID]** y **[!UICONTROL Environment ID]** independientes en su lugar, especifique los identificadores para ese entorno. Para la entrada manual, cópielos de AEM Cloud Manager o derivarlos de la dirección URL del autor: `https://author-p<ProgramID>-e<EnvironmentID>.adobeaemcloud.com/`. Escriba solo los identificadores numéricos, sin los prefijos `p` y `e`.

   Para los campos con una casilla de verificación **[!UICONTROL Use system value]**, desactívela antes de anular el valor predeterminado.

1. Marque **[!UICONTROL AEM Domain Mapping]**. Los dominios disponibles se cargan automáticamente en función del entorno de AEM seleccionado. Si su proyecto usa un dominio de entrega de recursos personalizado, siga [Configurar la dirección URL del dominio personalizado](#optional-configure-the-custom-domain-url).

1. [!BADGE Solo PaaS]{type=Informative tooltip="Solo se aplica a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe)."} Seleccione [[!UICONTROL Commerce integration]](configure-commerce.md#add-the-integration-to-the-commerce-environment) para autenticar solicitudes entre Commerce y el servicio de coincidencia de recursos.

1. Establezca **[!UICONTROL Synchronization enabled]** en `Yes` para permitir que Commerce acepte actualizaciones entrantes de los AEM Assets.

   Después de habilitar la integración, hay opciones de configuración adicionales disponibles para especificar criterios coincidentes de recursos.

1. Seleccione una de las reglas de coincidencia de recursos para la sincronización de recursos de la lista desplegable **[!UICONTROL Asset matching rule]**.

   * Seleccione **[!UICONTROL Match by product SKU]** para [coincidencia automática predeterminada](../synchronize/default-match.md).
   * Seleccione **[!UICONTROL Custom match]** para [coincidencia automática personalizada](../synchronize/custom-match.md). Esta opción requiere [Adobe Developer App Builder](https://experienceleague.adobe.com/es/docs/commerce-learn/tutorials/extensibility/adobe-developer-app-builder/introduction-to-app-builder).

1. Para **[!UICONTROL Match by product SKU]**, escriba el nombre de propiedad de metadatos [AEM Assets](../metadata.md) en el campo **[!UICONTROL Match by product SKU attribute name]**. El valor predeterminado es `commerce:skus`.

   Introduzca el nombre de la propiedad, no un valor de SKU del producto. Agregue los SKU de producto reales a los metadatos de **[!UICONTROL Product Data]** de cada recurso en los AEM Assets, tal como se describe en [Coincidencia automática predeterminada](../synchronize/default-match.md).

1. Revise la configuración [Propietario de la visualización](#configure-the-visualization-owner). Durante la migración, conserve la propiedad de **Adobe Commerce** hasta que se complete la sincronización de recursos.

1. Seleccione **[!UICONTROL Save Config]** para aplicar actualizaciones e iniciar la sincronización de recursos.

   La actualización de configuración crea un déclencheur con el proceso de sincronización inicial, lo que permite a Commerce aceptar las actualizaciones entrantes de los AEM Assets. El tiempo necesario para la sincronización depende del volumen de recursos y de las configuraciones específicas. La integración aprovecha los procesos automatizados para minimizar el tiempo necesario para la sincronización.

### Sincronización SLA

Service level agreement (SLA) para la integración garantiza los siguientes niveles de rendimiento de sincronización:

* `< 5 minutes for 99% of updates`

* `< 30 minutes for 99.9% of updates`

Este nivel de servicio garantiza que las páginas de producto siempre muestren las imágenes más actualizadas, manteniendo el contenido de la tienda preciso y visualmente atractivo.

## Sincronizar texto alternativo localizado

El texto alternativo localizado utiliza el proceso de sincronización de recursos existente. No necesita un nuevo tipo de evento ni una configuración de sincronización independiente.

1. Agregue una o más filas de texto alternativo de vista de tienda en la pestaña **[!UICONTROL Commerce]** del recurso de AEM.

1. Asocie el recurso al SKU del producto de Commerce.

1. Apruebe el recurso en AEM Assets.

1. Espere a que se completen el evento de recursos y el proceso de sincronización.

1. Compruebe el valor localizado en el administrador de Commerce y en la respuesta de la tienda.

Para ver los nombres de campo, las reglas de validación y el resultado de Commerce, consulte [Metadatos de Commerce en AEM Assets](../metadata.md).

## Configuración del propietario de la visualización

La configuración **Propietario de la visualización** determina qué sistema proporciona imágenes de producto en la integración:

* Adobe Commerce: Utiliza imágenes alojadas en Commerce.

* AEM Assets: Utiliza imágenes sincronizadas desde AEM.

El administrador muestra las imágenes disponibles para ese propietario, mientras que el resto de las imágenes aparecen atenuadas y mostradas con la etiqueta **hidden**.

Consulte el tema [establecer detalles de la imagen](https://experienceleague.adobe.com/es/docs/commerce-admin/catalog/products/digital-assets/product-image#set-image-details){target=_blank} para obtener detalles sobre el comportamiento de visualización de la imagen.

>[!TIP]
>
> Durante una migración de Commerce a AEM Assets, establezca **Propietario de la visualización** en Commerce para evitar que se rompan los vínculos de imagen. Una vez que todos los productos se hayan sincronizado correctamente con los AEM Assets, cambie al propietario de los AEM Assets para completar la transición. Esto garantiza la disponibilidad continua de las imágenes durante todo el proceso.

1. Vaya a **[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

   ![Propietario de visualización establecido en AEM Assets](../assets/visualization-owner-detail.png){width="700" zoomable="yes"}

1. Seleccione el origen de **Propietario de la visualización** para mostrar las imágenes.

1. Haga clic en **[!UICONTROL Save Config]** para aplicar actualizaciones.

   Antes de cambiar a **AEM Assets**, [compruebe que los recursos estén asociados con los productos esperados](#verify-the-integration). A continuación, [configura tu tienda](configure-storefront.md) para que muestre las imágenes de productos de los AEM Assets.

## Opcional. Configuración de la URL del dominio personalizado

Si el proyecto as a Cloud Service de AEM Assets se ha configurado con un [nombre de dominio personalizado](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/implementing/using-cloud-manager/custom-domain-names/add-custom-domain-name){target=_blank}, debe agregar el nombre de dominio a la configuración de la tienda de Commerce para que la integración de AEM Assets para Commerce pueda utilizarlo.

Obtenga la URL del dominio personalizado de entrega de recursos configurado de su administrador de AEM. Esta configuración reemplaza la dirección URL de envío de AEM; no es la dirección URL de autor de AEM utilizada para identificar el ID de programa y el ID de entorno. Si el proyecto no utiliza un dominio personalizado, deje la asignación de dominio sin cambiar.

>[!NOTE]
>
>La configuración de una URL de dominio personalizado no actualiza las direcciones URL de los recursos sincronizados anteriormente. Estos recursos conservan sus direcciones URL anteriores hasta que se [vuelven a procesar en los AEM Assets](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/assets/manage/reprocessing){target=_blank}. Después de guardar la configuración de dominio personalizado, vuelva a procesar estos recursos para actualizar sus direcciones URL y utilizar el dominio personalizado.

1. Vaya a **[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

1. Confirme el **[!UICONTROL AEM Environment]** seleccionado y, a continuación, seleccione el dominio personalizado configurado de **[!UICONTROL AEM Domain Mapping]**. Los dominios disponibles se cargan automáticamente para el entorno seleccionado.

![Selectores de dominio y entorno de AEM con valores de ejemplo](../assets/aem-assets-environment-domain.png){width="700" zoomable="yes"}

    En el caso de las configuraciones que muestren un campo de texto **[!UICONTROL Asset Custom Domain]**, escriba la dirección URL de dominio personalizado en ese campo.

1. Haga clic en **[!UICONTROL Save Config]** para aplicar actualizaciones.

## Verificar la integración

>[!NOTE]
>
>El estado de sincronización no está disponible para Adobe Commerce Optimizer. Siga el [flujo de trabajo de verificación de Commerce Optimizer](configure-aco.md#match-by-sku-workflow-example) en lugar de las comprobaciones de administrador de Commerce que aparecen a continuación.

1. Elija un producto de Commerce existente y anote su SKU.

1. En AEM Assets, marque un recurso de prueba como **[!UICONTROL Eligible for Commerce]**, asócielo a ese SKU de producto y establezca su rol y posición. Apruebe el recurso. Consulte [Coincidencia automática predeterminada](../synchronize/default-match.md) o use la [regla de coincidencia personalizada](../synchronize/custom-match.md) configurada.

1. Una vez finalizada la sincronización, abra el producto en Commerce Admin y compruebe en su sección **[!UICONTROL Images And Videos]** el recurso, la función y la posición asociados. Consulte [Administrar recursos](../manage-assets.md).

1. Revise [Estado de sincronización](sync-status.md) para el resultado de sincronización del recurso. Si la sincronización falla, revise la columna **[!UICONTROL Error]**.

1. Después de seleccionar **AEM Assets** como Propietario de la visualización y completar la [configuración de la tienda](configure-storefront.md), abre el producto en la tienda y confirma que aparece la imagen esperada.

[!BADGE Solo PaaS]{type=Informative tooltip="Solo se aplica a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe)."} Para obtener más información sobre la solución de problemas de sincronización, revise los [registros de integración](logs.md).

## Siguiente paso

* [Configura tu tienda Commerce](configure-storefront.md) para que muestre las imágenes de productos de los AEM Assets con Edge Delivery Services.

* Configure [reglas coincidentes](../synchronize/default-match.md) entre Adobe Commerce y la integración de AEM Assets.

* [Administrar recursos de Commerce](../manage-assets.md).
