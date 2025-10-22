---
title: Administrar recursos
description: Utilice la integración de AEM Assets para Commerce para administrar los recursos de medios de su tienda.
feature: CMS, Media
exl-id: 40ca36e0-d617-4814-852d-bc60ff53b2b3
source-git-commit: 5dd290a4e10bdbd1f6c96b67ab6c9ba1598705dc
workflow-type: tm+mt
source-wordcount: '866'
ht-degree: 0%

---

# Administrar recursos de medios de Commerce

<!--In ACAP-844, this topic was linked to from the Commerce Admin products images and videos when the Assets integration is enabled. If the URL to the topic changes, be sure to add a redirect.-->

Puede administrar los siguientes tipos de medios una vez habilitada la integración de AEM Assets para Commerce:

* Imágenes de productos
* Imágenes de contenido
* Vídeos del producto
* Imágenes de categoría

## Imágenes de productos

Cuando la integración está habilitada, la administración de imágenes está centralizada dentro del sistema de administración de activos digitales (DAM). A continuación, Adobe Commerce funciona como un canal de participación clave, lo que garantiza que solo se utilicen imágenes aprobadas y de alta calidad en las tiendas. Esta configuración mejora la coherencia de la marca, minimiza el esfuerzo manual y optimiza las actualizaciones de contenido, lo que elimina la necesidad de que los comerciantes carguen o administren manualmente las imágenes en Adobe Commerce.

### Ver imágenes de productos en Adobe Commerce

Las imágenes de producto se obtienen automáticamente de los AEM Assets en función de las reglas de coincidencia preconfiguradas:

1. En la barra lateral _Admin_, vaya a **[!UICONTROL Catalog]** > **[!UICONTROL Products]**.

1. Seleccione un producto.

1. Abra la sección **Imágenes y vídeos**.

   ![Imagen del producto](assets/product-image.png){width="600" zoomable="yes"}

   >[!NOTE]
   >
   > Un mensaje indica que la integración está habilitada, lo que la convierte en una sección **de solo lectura**, ya que la administración de imágenes está centralizada en DAM.

### Administración de imágenes de productos en AEM Assets

Para administrar imágenes relacionadas con el producto, todos los cambios deben hacerse directamente en **AEM Assets**. Este proceso está completamente automatizado, lo que garantiza que todos los cambios se sincronicen con Adobe Commerce sin necesidad de intervención manual.

### SLA de sincronización

Compruebe [Sincronización SLA](get-started/setup-synchronization.md#synchronization-sla)para obtener más información sobre este tema.

## Imágenes de contenido

Adobe Commerce proporciona Page Builder como **sistema de administración de contenido (CMS)** para los comerciantes que no usan el conjunto de herramientas de Adobe Experience Manager (AEM). Para mejorar la creación de contenido, nuestra integración aprovecha [AEM Asset Selector](synchronize/asset-selector-integration.md), lo que permite a los especialistas en marketing acceder e incrustar imágenes directamente desde **DAM** sin problemas. Esto garantiza que en la creación de contenido solo se utilicen imágenes aprobadas y de alta calidad, eliminando la necesidad de almacenamiento redundante en Adobe Commerce.

### Uso del Selector de recursos de AEM en Page Builder

[!BADGE Solo PaaS]{type=Informative tooltip="Solo se aplica a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe)."} Para usar el **Selector de recursos de AEM** para incrustar imágenes:

1. Vaya a cualquier sección de **Adobe Commerce Admin** que admita `content enrichment` con **Page Builder**.

1. Abra [Page Builder](https://developer.adobe.com/commerce/frontend-core/page-builder/){target=_blank}.

   Habrá disponible un nuevo tipo de medio llamado **AEM Asset**.

1. Arrastre y suelte el tipo de medios de AEM Asset en un bloque de contenido.

1. Cuando se le solicite, proporcione las credenciales para acceder a DAM.

1. Seleccione una imagen del DAM e insértela directamente en el contenido.

La asociación con la imagen seleccionada se almacenará en Adobe Commerce como una dirección URL directa que señala a **Dynamic Media**, lo que garantiza que:

* No es necesario almacenar los archivos de imagen en Adobe Commerce.

* Los especialistas en marketing trabajan exclusivamente con recursos aprobados de DAM.

* El contenido sigue siendo coherente y está actualizado en todos los puntos de contacto del cliente.

>[!TIP]
>
> [DA.live (Creación de documentos)](https://experienceleague.adobe.com/developer/commerce/storefront/merchants/storefront-builder/?lang=es#dalive-document-authoring){target=_blank} también proporciona un selector de recursos para enriquecer datos.

## Vídeos del producto

Adobe Commerce sirve como canal de participación clave para los recursos digitales. Una vez habilitada la integración de AEM Assets, la administración de vídeo se centraliza en **DAM**, lo que garantiza la coherencia, el cumplimiento y la entrega optimizada en las tiendas de comercio.

### Administrar vídeos de productos

1. En la barra lateral _Admin_, vaya a **[!UICONTROL Catalog]** > **[!UICONTROL Products]**.

1. Seleccione un producto.

1. Abra la sección **Imágenes y vídeos**.

   ![Imagen del producto](assets/product-image.png){width="600" zoomable="yes"}

   >[!NOTE]
   >
   > Un mensaje indica que la integración está habilitada, por lo que esta sección es **de solo lectura**, ya que los vídeos se controlan en los AEM Assets.

### Asociar vídeos en AEM Assets

1. En AEM Assets, vaya al vídeo que desee asociar con un producto.

1. Vincule el vídeo a uno o varios productos en Adobe Commerce.

1. La integración sincroniza automáticamente la asociación y muestra el reproductor de vídeo de Dynamic Media directamente en la tienda. Esto elimina la necesidad de que los comerciantes administren las configuraciones de reproducción de vídeo.

### Solo compatibilidad con vídeo API-First

Actualmente, la integración admite vídeos mediante API, lo que permite a los socios recuperar vídeos mediante programación.

>[!WARNING]
>
> De forma predeterminada, los vídeos aún no están integrados en las soluciones de tienda de Adobe Commerce existentes.

Esta integración garantiza que los comerciantes puedan administrar fácilmente los vídeos de los productos de una manera escalable y optimizada, aprovechando los AEM Assets y Dynamic Media para una entrega sin problemas.

### SLA de sincronización

Compruebe [Sincronización SLA](get-started/setup-synchronization.md#synchronization-sla)para obtener más información sobre este tema.

## Imágenes de categoría

Adobe Commerce permite a los comerciantes asociar imágenes con categorías de productos, lo que ayuda a crear una tienda atractiva visualmente. La integración de AEM Assets aprovecha el Selector de recursos de AEM, lo que permite a los especialistas en mercadotecnia seleccionar recursos sin problemas directamente desde el **sistema de administración de recursos digitales (DAM)**. Esto garantiza que solo se utilicen imágenes aprobadas y elimina la necesidad de almacenarlas en Adobe Commerce, lo que mantiene la coherencia y la eficacia en todos los canales de participación.

### Uso del Selector de recursos de AEM para imágenes de categoría

Después de configurar el [Selector de recursos de AEM](synchronize/asset-selector-integration.md), puede utilizarlo para agregar recursos al contenido de las categorías del catálogo.

1. En la barra lateral _Admin_, vaya a **[!UICONTROL Catalog]** > **[!UICONTROL Categories]**.

1. Seleccione la categoría que desee actualizar.

1. Expanda ![Selector de expansión](../assets/icon-display-expand.png) en la sección **[!UICONTROL Content]**.

1. En la sección **[!UICONTROL Content]**, busque el *campo de imagen* asociado a la categoría.

   ![Contenido de categoría](assets/category-asset.png){width="600" zoomable="yes"}

1. Haga clic en **[!UICONTROL Select from Assets]** para cambiar la imagen de la categoría.

   ![Contenido de categoría](assets/asset-view.png){width="600" zoomable="yes"}

1. Elija una imagen del Selector de recursos de AEM.

   ![Contenido de categoría](assets/select-image.png){width="600" zoomable="yes"}

1. Haga clic en **[!UICONTROL Save]** y continúe.

   Para obtener más información sobre cómo crear una categoría, consulte [Completar el contenido de la categoría](https://experienceleague.adobe.com/es/docs/commerce-admin/catalog/categories/create/category-create#step-3-complete-the-category-content) en la **Guía de administración del catálogo de Commerce**.

## Actualizar un recurso

Después de actualizar y aprobar un recurso en AEM Assets, las actualizaciones se envían automáticamente a Adobe Commerce mediante la función de coincidencia automatizada. Este proceso se activa tras la aprobación del recurso. Para asegurarse de que se incluyen todos los cambios finales y las actualizaciones de metadatos, asegúrese de volver a procesar el recurso antes de aprobarlo.

Para obtener más información, consulte la siguiente documentación de AEM Assets.

* [Reprocesando recursos digitales](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/assets/manage/reprocessing)

* [Aprobar un recurso](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/assets/dynamicmedia/dynamic-media-open-apis/approve-assets)
