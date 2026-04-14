---
title: Integraciones de Commerce Optimizer
description: Obtenga información acerca de las integraciones de Adobe Commerce Optimizer para la sincronización de catálogos, la administración de recursos, la optimización de tiendas y la conectividad de Salesforce Commerce Cloud.
solution: Commerce
feature: Integration, Catalog Management
role: Developer, Admin
level: Beginner
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a  [!DNL Adobe Commerce Optimizer] proyectos (infraestructura SaaS administrada por Adobe)."
exl-id: 8f3a2c1b-9d4e-5f6a-bc7d-1e2f3a4b5c6d
source-git-commit: d8cd6f543353e1b11f3aa14b3b97b02155d23809
workflow-type: tm+mt
source-wordcount: '376'
ht-degree: 0%

---


# Integraciones de [!DNL Adobe Commerce Optimizer]

[!DNL Adobe Commerce Optimizer] incluye integraciones que le permiten sincronizar datos de Adobe Commerce en la nube o de forma local, administrar recursos, mejorar experiencias de tienda y conectar sistemas externos. Las secciones siguientes describen cómo funciona cada integración con [!DNL Adobe Commerce Optimizer]. Siga los vínculos para la instalación, configuración y uso diario.

## Conector de Adobe Commerce Optimizer {#aco-connector}

Adobe Commerce Optimizer Connector es el puente que sincroniza los datos de catálogo y de precios entre Adobe Commerce (en la nube o local) y [!DNL Adobe Commerce Optimizer]. Al habilitar el conector, Commerce permanece como el sistema de registro de los datos del producto mientras que [!DNL Adobe Commerce Optimizer] activa la detección de productos, las recomendaciones, las reglas de comercialización, los análisis y las experiencias de tienda sin encabezado.

- [Descripción general del conector Adobe Commerce Optimizer](../../aco-connector/overview.md){target="_blank"}
- [Introducción al conector](../../aco-connector/get-started.md){target="_blank"}

## Imágenes del producto con AEM Assets {#product-visuals}

Product Visuals permite administrar imágenes de productos a través de Adobe Experience Manager (AEM) Assets. Configure los AEM Assets de Commerce Optimizer para habilitar los elementos visuales del producto. Una vez finalizada la configuración, utilice AEM Assets como solución de administración centralizada de recursos digitales para las imágenes de sus productos, con flujos de trabajo automatizados de revisión y administración de recursos que mantengan las imágenes sincronizadas con su catálogo de Commerce Optimizer. La integración hace coincidir los recursos con los productos por SKU. Las actualizaciones fluyen por los servicios de integración de Adobe para que las tiendas reflejen los medios más recientes sin tener que volver a cargarlas manualmente.

- [Imágenes del producto con AEM Assets](../setup/product-visuals.md)
- [Configurar AEM Assets para Commerce Optimizer](../../aem-assets-integration/get-started/configure-aco.md){target="_blank"}

## Adobe Experience Manager Sites Optimizer {#aem-sites-optimizer}

Adobe Experience Manager Sites Optimizer analiza los sitios web de Commerce y mejora el rendimiento al mostrar **[!UICONTROL Opportunities]**, recomendaciones impulsadas por IA que le ayudan a mejorar la detección, la participación y las conversiones.

>[!AVAILABILITY]
>
>Esta funcionalidad requiere la licencia de **Ultima** Adobe Sites Optimizer. Puede solicitar una licencia a través de su asesor técnico del cliente de Adobe. Una vez aprovisionada la cuenta, la característica Oportunidades está disponible en la interfaz de [!DNL Adobe Commerce Optimizer] y puede empezar a utilizar perspectivas controladas por IA para optimizar sus estrategias de tienda y comercialización.

- [Oportunidades](../manage-results/opportunities.md)

## Conector de Commerce Salesforce {#commerce-salesforce-connector}

Commerce Salesforce Connector (integrado en Adobe App Builder) sincroniza los datos de catálogo y precio de Salesforce Commerce Cloud B2C en [!DNL Adobe Commerce Optimizer] para que pueda utilizar las capacidades de tienda y comercialización de Adobe sin tener que volver a crear plataformas en el backend de comercio de Salesforce. Puede programar sincronizaciones, ejecutar actualizaciones bajo demanda y ampliar la integración mediante las API de Commerce de Salesforce.

- [Conector de Salesforce Commerce](../developer/salesforce-connector.md)

>[!MORELIKETHIS]
>
>- [Documentación técnica de Adobe Commerce Optimizer](https://developer.adobe.com/commerce/services/optimizer/){target="_blank"}
>- [Introducción a Adobe Commerce Optimizer](../get-started.md)
