---
title: Integración de AEM Assets para Commerce
description: Aprenda a integrar Adobe Experience Manager Assets con su instancia de  [!DNL Commerce] para crear y administrar los archivos multimedia de su tienda de Commerce.
feature: CMS, Media, Configuration, Integration
exl-id: f450752a-bef1-419e-ad14-ff8879ab204b
TQID: https://experienceleague.adobe.com/CTDmM7Ox2rQ-55F1BVTg-C8DPBEuEpzFxXGtWpnjXKs
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
subfeature_v2:
  - id: e91a50b1-0b31-436e-9033-00e4776e94cb
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: da3860b0-d637-47df-bef0-273751180266
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 0c2e50338cbf286704239b6d1f628180e85a3bef
workflow-type: tm+mt
source-wordcount: 1081
ht-degree: 1%

---

# Integración de AEM Assets para Commerce

La demanda de contenido personalizado aumenta rápidamente mientras que los presupuestos de marketing están bajo presión. Los minoristas y las marcas tienen dificultades para mantenerse al día con la creciente necesidad de variaciones en las imágenes de los productos, impulsadas por requisitos regionales, estacionales y específicos de segmentos.

Piense en un retailer con 1000 productos. El número de recursos digitales necesarios se amplía significativamente al tener en cuenta diferentes regiones, segmentos de clientes y esfuerzos de personalización. Esta situación puede llevar a un número abrumador de variaciones de activos, llegando a millones.

![descripción general](assets/product-visuals-example.png){width="700" zoomable="yes"}

La integración de AEM Assets aborda este desafío automatizando los flujos de trabajo de administración de recursos. La integración vincula dinámicamente los recursos digitales con los productos y las categorías de Adobe Commerce adecuados en función del SKU u otros atributos clave. Este proceso optimiza las operaciones y mejora la eficacia al permitir lo siguiente:

* **Instalación y configuración sin problemas**: los equipos y desarrolladores de comercialización pueden configurar rápidamente la integración con herramientas y flujos de trabajo de Adobe conocidos.

* **Actualizaciones dinámicas de recursos**: las imágenes de productos y los recursos de marketing reflejan automáticamente los cambios más recientes en los AEM Assets, por lo que las tiendas son precisas y relevantes.

* **Administración optimizada de catálogos**: automatiza la actualización y limpieza de recursos, minimiza el esfuerzo manual y garantiza un catálogo de productos coherente y bien mantenido.

## Requisitos para utilizar la integración

Para aprovechar esta integración con [AEM Assets o elementos visuales del producto](https://experienceleague.adobe.com/es/docs/commerce/cloud-service/overview#product-visuals-powered-by-aem-assets), las empresas deben cumplir con los siguientes requisitos:

>[!BEGINTABS]

>[!TAB Imágenes del producto]

[!BADGE Solo SaaS]{type=Positive url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."} licencias activas para Adobe Commerce, elementos visuales de productos con tecnología de AEM Assets y [AEM Dynamic Media](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/assets/dynamic/administering-dynamic-media) (estas licencias están disponibles de forma predeterminada con [!DNL Adobe Commerce as a Cloud Service] y [!DNL Adobe Commerce Optimizer]).

>[!TAB AEM Assets]

[!BADGE Solo SaaS]{type=Positive url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."} licencias activas para Adobe Commerce, Adobe Experience Manager Assets y [AEM Dynamic Media](https://experienceleague.adobe.com/es/docs/experience-manager-65/content/assets/dynamic/administering-dynamic-media).

[!BADGE Solo PaaS]{type=Informative tooltip="Solo se aplica a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe)."} Adobe Commerce 2.4.5+

* PHP 8.1, 8.2, 8.3 y 8.4

* Composer 2.x

[!BADGE Solo SaaS]{type=Positive url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."} Adobe Experience Manager está aprovisionado con [Adobe Experience Manager Assets as a Cloud Service](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/assets/overview)

>[!ENDTABS]

El usuario de Adobe Commerce que configuró la integración debe tener acceso a la [organización de IMS](https://experienceleague.adobe.com/es/docs/core-services/interface/administration/organizations#concept_EA8AEE5B02CF46ACBDAD6A8508646255) en la que se ha aprovisionado el proyecto de AEM Assets.

>[!BEGINSHADEBOX]

## Ventajas empresariales clave

![cheque](assets/icon-check.png) **Sin costo adicional** - Esta integración se proporciona de forma gratuita para los comerciantes que cumplan con los requisitos de licencia.

![comprobar](assets/icon-check.png) **Solución oficial de Adobe**: desarrollada, mantenida y totalmente compatible con Adobe, que garantiza estabilidad y alineación con futuras mejoras de la plataforma.

![comprobar](assets/icon-check.png) **Modelo de soporte administrado por Adobe**: Adobe gestiona la asistencia y la solución de problemas directamente, lo que proporciona una asistencia fiable y una resolución de problemas optimizada.

![comprobar](assets/icon-check.png) **Funciones de Adobe Storefront Builder**: la solución de administración de activos digitales (DAM) permite el uso de recursos como imágenes, vídeos y otros medios en [Storefront Builder](https://experienceleague.adobe.com/developer/commerce/storefront/merchants/storefront-builder/?lang=es#userlabs-commerce-genai-product-visuals).

>[!ENDSHADEBOX]

## Tutorial

Para aprender a configurar y utilizar la integración de AEM Assets con Adobe Commerce, vea estos vídeos.

>[!BEGINTABS]

>[!TAB Tutorial de Adobe Commerce en la nube o local]

Para conocer cómo Adobe Commerce y los AEM Assets trabajan juntos para optimizar los flujos de trabajo de contenido, vea este vídeo:

>[!VIDEO](https://video.tv.adobe.com/v/3447837)

>[!TAB Tutorial de Adobe Commerce as a Cloud Service]

Aprenda a utilizar Adobe Commerce as a Cloud Service con la integración de AEM Assets.

>[!VIDEO](https://video.tv.adobe.com/v/3478140?quality=12&learn=on)

>[!ENDTABS]

## Pasos siguientes

El proceso de instalación y configuración de la integración de AEM Assets depende de la implementación de Adobe Commerce. En todos los casos, primero se configuran los AEM Assets y luego se conecta Commerce.

Para comprender el espacio de nombres, el esquema de metadatos y la ficha **[!UICONTROL Commerce]** que la integración agrega al entorno de AEM Assets, revise los metadatos de [Commerce en AEM Assets](metadata.md) antes de comenzar.

Seleccione la implementación para seguir los pasos necesarios en orden:

>[!BEGINTABS]

>[!TAB Adobe Commerce as a Cloud Service]

[!BADGE Solo SaaS]{type=Positive tooltip="Solo se aplica a proyectos de Adobe Commerce as a Cloud Service (infraestructura de SaaS administrada por Adobe)."}

1. Para admitir metadatos de Commerce, [configure el proyecto de AEM Assets](get-started/configure-aem.md). En la versión de AEM `2026.5.26309` y posteriores, use la incorporación de autoservicio [2&rbrace;; en versiones anteriores, instale el paquete `assets-commerce` manualmente.](get-started/configure-aem.md#enable-aem-commerce-self-service)

1. [Configure los permisos de usuario de IMS](get-started/permissions.md) para que el Selector de recursos y los campos **[!UICONTROL Program ID]** y **[!UICONTROL Environment ID]** que se rellenan automáticamente estén disponibles.

1. [Configure la integración en el administrador de Commerce](get-started/setup-synchronization.md).

1. Opcional. [Habilitar la visualización de la imagen del producto](get-started/configure-storefront.md#enable-product-images) para que una tienda con tecnología Edge Delivery Services procese imágenes de productos administrados por AEM.

>[!TAB Adobe Commerce en la nube (PaaS)]

[!BADGE Solo PaaS]{type=Informative tooltip="Solo se aplica a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe)."}

1. Para admitir metadatos de Commerce, [configure el proyecto de AEM Assets](get-started/configure-aem.md). En la versión de AEM `2026.5.26309` y posteriores, use la incorporación de autoservicio [2&rbrace;; en versiones anteriores, instale el paquete `assets-commerce` manualmente.](get-started/configure-aem.md#enable-aem-commerce-self-service)

1. [Instale paquetes de Adobe Commerce](get-started/configure-commerce.md) para agregar la extensión y generar las credenciales y conexiones necesarias.

1. [Configure los permisos de usuario de IMS](get-started/permissions.md) para que el Selector de recursos y los campos **[!UICONTROL Program ID]** y **[!UICONTROL Environment ID]** que se rellenan automáticamente estén disponibles.

1. [Configure la integración en el administrador de Commerce](get-started/setup-synchronization.md).

1. Opcional. [Habilitar la visualización de la imagen del producto](get-started/configure-storefront.md#enable-product-images) para que una tienda con tecnología Edge Delivery Services procese imágenes de productos administrados por AEM.

>[!TAB Adobe Commerce Optimizer]

[!BADGE Solo SaaS]{type=Positive tooltip="Solo se aplica a los proyectos de Adobe Commerce Optimizer."}

[!DNL Adobe Commerce Optimizer]: no tiene una interfaz de usuario de configuración de administración. El Soporte de Adobe configura la integración desde su ticket de incorporación, por lo que debe preparar primero a los AEM Assets.

1. Para admitir metadatos de Commerce, [configure el proyecto de AEM Assets](get-started/configure-aem.md). En la versión de AEM `2026.5.26309` y posteriores, use la incorporación de autoservicio [2&rbrace;; en versiones anteriores, instale el paquete `assets-commerce` manualmente.](get-started/configure-aem.md#enable-aem-commerce-self-service)

1. [Envíe el ticket de asistencia para la incorporación](get-started/configure-aco.md#onboarding) con su ID de inquilino, ID de programa de AEM, ID de entorno de AEM, regla de coincidencia, nivel y configuración regional.

1. [Configure la vista de catálogo](get-started/configure-aco.md#onboarding) con la misma configuración regional y capa que registró en el ticket.

1. Opcional. [Habilitar la visualización de la imagen del producto](get-started/configure-storefront.md#enable-product-images) para que una tienda con tecnología Edge Delivery Services procese imágenes de productos administrados por AEM.

   Para obtener instrucciones completas sobre el procedimiento, las limitaciones y la capa, consulte [Configuración de AEM Assets para Commerce Optimizer](get-started/configure-aco.md).

>[!ENDTABS]

## Asistencia

Si necesita información o tiene preguntas que no se tratan en esta guía, póngase en contacto con su representante de ventas de integración de AEM Assets o cree un [ticket de asistencia](https://experienceleague.adobe.com/es/docs/support-resources/adobe-support-tools-guide/adobe-commerce-support/adobe-commerce-help-center-user-guide#support-case) para recibir ayuda adicional.
