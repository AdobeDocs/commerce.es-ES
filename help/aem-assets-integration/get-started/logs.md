---
title: Visualización y administración de registros
description: Descubra dónde encontrar y administrar los registros de la integración de AEM Assets para Commerce.
feature: CMS, Media, Integration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."
exl-id: 9c6c8694-6ded-4cc8-a3ab-d1dfb50e3583
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: ddbd0f6e-b569-5a04-8a70-55058777c373
    internal-label: CMS
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: 76e77db86adecdbd3be76040970c0d0899c34cdc
workflow-type: tm+mt
source-wordcount: '180'
ht-degree: 0%
---
# Visualización y administración de registros

La integración de AEM Assets proporciona los siguientes archivos de registro en la instancia de Commerce:

- `/var/log/aem-assets-integration.log`
- `/var/log/aem-assets-integration-errors.log`

Para obtener una vista centrada en los recursos de los recursos sincronizados en el administrador, incluidos resúmenes de errores de sincronización, filtros y búsqueda, consulte [Ver el estado de sincronización de los AEM Assets](sync-status.md).

Pida al administrador del sistema que compruebe el horario de rotación de archivos de registro para evitar que crezcan demasiado. En algunos entornos, los registros giran automáticamente; en otros, debe configurar la rotación de registros manualmente.  Para obtener más información, consulte los temas siguientes:

- Para las instalaciones locales de Adobe Commerce, pídale al administrador del sistema que configure [rotación del registro](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/next-steps/configuration#server-settings).
- Para Adobe Commerce sobre proyectos de infraestructura en la nube, consulte [Ver y administrar registros](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/test/log-locations).
