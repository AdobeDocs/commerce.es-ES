---
title: Visualización y administración de registros
description: Descubra dónde encontrar y administrar los registros de la integración de AEM Assets para Commerce.
feature: CMS, Media, Integration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."
exl-id: 9c6c8694-6ded-4cc8-a3ab-d1dfb50e3583
TQID: https://experienceleague.adobe.com/im5QUgqayCNj9lZfZ-7UvxiUW9NmgHyhVbyBdjjPxAA
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 154
ht-degree: 0%

---

# Visualización y administración de registros

La integración de AEM Assets proporciona los siguientes archivos de registro en la instancia de Commerce:

- `/var/log/aem-assets-integration.log`
- `/var/log/aem-assets-integration-errors.log`

Pida al administrador del sistema que compruebe el horario de rotación de archivos de registro para evitar que crezcan demasiado. En algunos entornos, los registros giran automáticamente; en otros, debe configurar la rotación de registros manualmente.  Para obtener más información, consulte los temas siguientes:

- Para las instalaciones locales de Adobe Commerce, pídale al administrador del sistema que configure [rotación del registro](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/configuration.html?lang=es#server-settings).
- Para Adobe Commerce sobre proyectos de infraestructura en la nube, consulte [Ver y administrar registros](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/test/log-locations.html?lang=es).
