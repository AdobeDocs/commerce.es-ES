---
title: Configurar tu tienda
description: Aprenda a conectar su tienda de Edge Delivery Services con la integración de AEM Assets.
feature: CMS, Media, Integration
source-git-commit: d426c7878f7a66fe1047673be7c5bf65ae1949a7
workflow-type: tm+mt
source-wordcount: '127'
ht-degree: 0%

---


# Configurar tu tienda

La integración de AEM Assets muestra imágenes de productos administradas en AEM Assets en lugar de utilizar imágenes alojadas en Adobe Commerce. La integración permite funcionalidades mejoradas de administración de imágenes, incluida la optimización avanzada, el recorte y la entrega a través de la red de entrega de contenido (CDN) de Adobe.

Para habilitar la integración en tiendas de Commerce con tecnología de Edge Delivery Services, actualice el archivo de configuración de la tienda (`config.json`) para agregar el parámetro `"commerce-assets-enabled": true`.

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

Para obtener más información sobre cómo usar AEM Assets con Commerce Storefront con tecnología Edge Delivery Services, complete la configuración de tienda que se describe en el tema [Integración de AEM Assets](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/aem-assets-configuration/?lang=es) de la *documentación de Adobe Commerce Storefront*.
