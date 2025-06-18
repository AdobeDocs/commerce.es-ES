---
title: Visualización y administración de registros
description: Descubra dónde buscar y administrar registros para imágenes de productos.
feature: CMS, Media, Integration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."
source-git-commit: b6e190e883087a942630f0a27781654cd2c68781
workflow-type: tm+mt
source-wordcount: '115'
ht-degree: 0%

---


# Visualización y administración de registros

Product Visuals proporciona los siguientes archivos de registro en la instancia de Commerce:

- `/var/log/aem-assets-integration.log`
- `/var/log/aem-assets-integration-errors.log`

Pida al administrador del sistema que compruebe el horario de rotación de archivos de registro para evitar que crezcan demasiado. En algunos entornos, los registros giran automáticamente; en otros, debe configurar la rotación de registros manualmente.  Para obtener más información, consulte los temas siguientes:

- Para las instalaciones locales de Adobe Commerce, pídale al administrador del sistema que configure [rotación del registro](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/configuration.html?lang=es#server-settings).
- Para Adobe Commerce sobre proyectos de infraestructura en la nube, consulte [Ver y administrar registros](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/test/log-locations.html?lang=es).
