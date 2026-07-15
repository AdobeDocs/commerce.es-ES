---
title: Configurar tu tienda
description: Aprenda a conectar su tienda de Edge Delivery Services con la integración de AEM Assets.
feature: CMS, Media, Integration
TQID: https://experienceleague.adobe.com/gl0Y2UNs3sYkXE9QYwLtAltyX1dxE699y23ey-y0KUU
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
subfeature_v2:
  - id: ae62cf09-5996-4921-bda8-fbe67b62e470
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2:
  - id: cdd65e7e-8839-44a2-bc21-0e03623b5dd1
source-git-commit: 7f901cec90291e264376e3f93e6ebaaccf7c15f0
workflow-type: tm+mt
source-wordcount: 610
ht-degree: 0%

---

# Configurar tu tienda

## Habilitar la visualización de la imagen del producto desde los AEM Assets {#enable-product-images}

La integración de AEM Assets muestra imágenes de productos de AEM Assets en lugar de Adobe Commerce, lo que permite una optimización avanzada, un recorte y una entrega de CDN.

Para habilitar la integración en tiendas de Commerce con tecnología de Edge Delivery Services, agregue el parámetro `"commerce-assets-enabled": true` al archivo de configuración de la tienda (`config.json`).

```json
{
  "public": {
    "default": {
      "commerce-assets-enabled": true
    }
  }
}
```

Los complementos de Commerce detectan automáticamente la configuración de `commerce-assets-enabled` y ajustan la administración de imágenes en consecuencia.

Para obtener más información sobre el uso de AEM Assets con Commerce Storefront con tecnología de Edge Delivery Services, consulte el tema [Integración de AEM Assets](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/) en la documentación de *Adobe Commerce Storefront*.

>[!TIP]
>
>Para que los autores puedan examinar e insertar AEM Assets en páginas de contenido estático, consulte [Conectar AEM Assets a Da.live para la creación de contenido estático](#connect-aem-assets-authoring).

## Conectar AEM Assets a Da.live para la creación de contenido estático {#connect-aem-assets-authoring}

>[!NOTE]
>
>Esta configuración es independiente de la extensión de integración de AEM Assets. Proporcionado por [Da.live](https://da.live){target="_blank"}, permite a los autores examinar e insertar AEM Assets en páginas de contenido estático (por ejemplo, páginas de aterrizaje o bloques de contenido) a través del panel [!UICONTROL Library] y [!UICONTROL Content Advisor]. Las imágenes de producto sincronizadas mediante la integración de AEM Assets se configuran por separado con la configuración de `commerce-assets-enabled`.

Siga estos pasos para conectar los AEM Assets a una tienda de Document Authoring (Da.live) para que los autores puedan examinar e insertar AEM Assets de **[!UICONTROL Content Advisor]** mientras editan contenido estático.

>[!NOTE]
>
>Para obtener instrucciones de configuración detalladas, consulte [AEM Assets de instalación](https://docs.da.live/administrators/guides/setup-aem-assets){target=_blank} en la documentación de Da.live y [AEM Assets de integración al crear contenido para Edge Delivery Services](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/integrate-aem-assets-edge-delivery-services/integrate-aem-assets-edge-delivery-services){target=_blank} en la documentación de AEM Assets.

### Paso 1: Abrir la configuración de su sitio en Da.live

1. Desde [Da.live](https://da.live){target=_blank}, localiza y abre tu tienda.

1. En la ruta de exploración, seleccione el icono **[!UICONTROL Settings]** junto al nombre del sitio para abrir la hoja de cálculo de configuración del sitio.

### Paso 2: copie la URL de su repositorio de AEM

1. En una pestaña nueva, ve a [experience.adobe.com](https://experience.adobe.com){target=_blank} y ve a **[!UICONTROL Experience Manager]**.

1. Abra Adobe Experience Manager Assets: Desplácese hasta la sección **[!UICONTROL My Authoring]** y, a continuación, seleccione **[!UICONTROL Assets]** junto a su entorno **[!UICONTROL Production]**.

1. Desde la barra de direcciones del explorador, copie el segmento que comienza con `author` hasta `.com`, inclusive; por ejemplo, `author-p107634-e1009805.adobeaemcloud.com`.

### Paso 3: Añadir el ID de repositorio a la configuración

1. Para configurar su sitio, vuelva a Da.live y seleccione **[!UICONTROL data]** en la configuración del sitio.

1. Complete la hoja de cálculo de la siguiente manera:

   | Celda | Valor |
   |---|---|
   | A1 | `key` |
   | B1 | `value` |
   | A2 | `aem.repositoryId` |
   | B2 | La URL que copió en el paso 2 |

1. Seleccione **[!UICONTROL Save]** y, a continuación, seleccione la flecha hacia atrás junto al nombre del sitio para volver a la raíz del sitio.

   >[!NOTE]
   >
   > El host con prefijo `author-` explora los recursos desde el nivel de creación. Para enviar recursos a través de Dynamic Media, use un host con el prefijo `delivery-`. Para ver todas las opciones de `aem.repositoryId`, consulte [AEM Assets de instalación](https://docs.da.live/administrators/guides/setup-aem-assets){target=_blank}.

### Paso 4: Conectar AEM Assets a través de la biblioteca

1. En la raíz del sitio, seleccione la carpeta **[!UICONTROL index]** para abrirla.

1. En el editor, abra el panel **[!UICONTROL Library]** y seleccione **[!UICONTROL AEM Assets]**.

   La ventana emergente **[!UICONTROL Content Advisor]** se abre y muestra los archivos y las carpetas de los AEM Assets.

La tienda está conectada a los AEM Assets. Puede examinar e insertar recursos directamente desde **[!UICONTROL Content Advisor]**.

## Documentación relacionada

* [Integración de AEM Assets](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/){target=_blank} en la documentación de *Adobe Commerce Storefront*: configuración de tienda y comportamiento de administración de imágenes.

* [Integrar AEM Assets al crear contenido para Edge Delivery Services](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/integrate-aem-assets-edge-delivery-services/integrate-aem-assets-edge-delivery-services){target=_blank} en la documentación de *AEM Assets*.

* [AEM Assets de instalación](https://docs.da.live/administrators/guides/setup-aem-assets){target=_blank} y [trabajando con medios](https://docs.da.live/authors/guides/adding-media){target=_blank} en la documentación de Da.live.
