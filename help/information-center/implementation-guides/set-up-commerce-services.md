---
title: Configuración de los servicios de Commerce
description: Obtenga información sobre cómo conectar Adobe Commerce a los servicios de comercialización y Magento Open Source a los servicios de pago mediante Commerce Services Connector.
role: Admin, Developer
feature: Integration, Configuration
recommendations: noCatalog
autotag-review: '2026-10-20T11:14:04.410Z'
TQID: 'https://experienceleague.adobe.com/yyUDw1y5CYHxdLlC3bNo0DKK0byamPAKUjK-wwxVEX4'
product_v2:
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 4273989f-0bf2-5361-a17a-6909488d18ab
    internal-label: Catalog Service
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
subfeature_v2:
  - id: a1d22079-48b9-5e69-9ee6-eb236068ef34
    internal-label: Search
source-git-commit: ca6bb3543583c865c42b8f4d84f01e27a04f9223
workflow-type: tm+mt
source-wordcount: '164'
ht-degree: 0%
---

# Configuración de servicios de Commerce

Adobe Commerce en la infraestructura en la nube y los proyectos locales se conectan a servicios como [!DNL Catalog Service], [!DNL Live Search], [!DNL Product Recommendations] y [!DNL Payment Services] a través de Commerce Services Connector. En [!DNL Adobe Commerce as a Cloud Service], esta conexión se configura automáticamente.

Magento Open Source usa Commerce Services Connector para [!DNL Payment Services]. [!DNL Catalog Service], [!DNL Live Search] y [!DNL Product Recommendations] requieren Adobe Commerce y no están disponibles para Magento Open Source.

>[!NOTE]
>
>Adobe Commerce Optimizer proporciona las funciones de catálogo y comercialización de forma nativa, en lugar de utilizar los servicios independientes [!DNL Live Search], [!DNL Catalog Service] y [!DNL Product Recommendations]. Su sincronización con el catálogo no requiere Commerce Services Connector. Otras integraciones en el backend de Commerce, como [!DNL Payment Services] y [!DNL Data Connection], aún requieren el conector. Consulte [Habilitar Adobe Commerce Optimizer](enable-aco.md) para la configuración de Optimizer.


## Primeros pasos

1. Revise la documentación de [Commerce Services Connector](/help/landing/saas.md) para obtener y configurar las claves de API.

1. Consulte las [Guías de servicios de Adobe Commerce](/help/landing/home.md) para conocer los servicios individuales disponibles a través del conector.

## Directrices relacionadas

- [Configuración de pagos](configure-payments.md)
- [Conectar AEM Assets](connect-aem-assets.md)
- [Integración con Adobe Experience Platform](integrate-aep.md)
