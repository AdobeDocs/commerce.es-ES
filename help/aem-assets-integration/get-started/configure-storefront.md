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
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 137
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
