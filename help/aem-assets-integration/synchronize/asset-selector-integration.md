---
title: Selección manual de recursos
description: Descubra cómo el Selector de recursos de AEM, integrado en el Administrador de Commerce, ayuda a los especialistas en marketing y a los comerciantes a añadir fácilmente imágenes de los AEM Assets a Adobe Commerce, lo que optimiza la administración de recursos.
feature: CMS, Media, Integration
exl-id: 3c1f906f-3ec3-4eac-a47e-b21792767359
TQID: 'https://experienceleague.adobe.com/3fYabUvRiY8KTxQX1YiTBbLxABpQqfZLu0a6IBDsM3E'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b5f00040-57a0-4a6d-a39e-383b1936c2c9
    internal-label: Compliance
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: ddbd0f6e-b569-5a04-8a70-55058777c373
    internal-label: CMS
  - id: 4ca54350-01cb-5b22-8966-5f2873dc6d90
    internal-label: Media
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
topic_v2:
  - id: da3860b0-d637-47df-bef0-273751180266
    internal-label: Digital asset management
source-git-commit: 76e77db86adecdbd3be76040970c0d0899c34cdc
workflow-type: tm+mt
source-wordcount: '397'
ht-degree: 0%
---
# Selección manual de recursos

El **Selector de recursos de AEM** permite a los especialistas en mercadotecnia y mercadotecnia agregar fácilmente imágenes de los AEM Assets a Adobe Commerce, lo que optimiza el proceso de administración de recursos. Este método garantiza la coherencia y el cumplimiento de la marca limitando la selección de recursos a los revisados y aprobados en [!DNL DAM (Digital Asset Management system)].

El **Selector de recursos de AEM** está disponible cuando el ID de cliente IMS para el proyecto de AEM Assets se ha configurado en el administrador de Commerce y los usuarios tienen los [permisos y la autenticación IMS](../get-started/permissions.md) necesarios. Consulte [Configuración del Selector de recursos de AEM](#configure-the-aem-asset-selector-in-adobe-commerce).

Una vez configurada la integración de **AEM Asset Selector**, los especialistas en marketing y los comerciantes podrán:

* Administre las imágenes de categoría sin esfuerzo, para que se ajusten a las directrices de marca y campaña.
* [!BADGE Solo PaaS]{type=Informative tooltip="Solo se aplica a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe)."}: asigne recursos directamente en Page Builder para contenido visualmente enriquecido.
* [!BADGE Solo SaaS]{type=Positive url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."} Asigna Assets directamente en Commerce Storefront con tecnología Edge Delivery Services para contenido visualmente enriquecido.

>[!NOTE]
>
> El Selector de recursos de AEM es un componente front-end de recursos de AEM para integrar AEM Assets con aplicaciones de creación. Para obtener más información sobre este componente, consulte el [Selector de recursos de Micro-Frontend](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/assets/content-advisor/integrate-adobe-non-adobe-applications){target=_blank} en la *Guía del usuario de AEM as a Cloud Service*.

## Ventajas principales

La incrustación del Selector de recursos de AEM en el Panel de administración de Adobe Commerce ofrece varias ventajas clave:

* **Coherencia de la marca**: muestra solo los recursos aprobados, lo que minimiza el riesgo de que haya imágenes obsoletas o no compatibles en la tienda.

* **Eficiencia**: permite a los especialistas en marketing y a los comerciantes asignar recursos rápidamente sin cambiar entre distintas plataformas.

* **Collaboration optimizado**: facilita el trabajo en equipo al permitir la selección directa de imágenes desde DAM, lo que elimina las descargas y cargas manuales.

* **Calidad de contenido mejorada**: garantiza el uso de imágenes optimizadas de alta resolución en páginas de productos, categorías y Page Builder.

![Selector de recursos](../assets/asset-selector.png){width="600" zoomable="yes"}

## Configuración del Selector de recursos de AEM en Adobe Commerce

1. En el Administrador de Commerce, vaya a **[!UICONTROL Store]** > Configuración > **[!UICONTROL ADOBE SERVICES]** > **[!UICONTROL AEM Assets Integration]**.

1. Rellene el campo **[!UICONTROL IMS Client ID]**. Para obtener los permisos necesarios y cómo obtener este ID, consulte [Permisos de usuario e IMS](../get-started/permissions.md).

1. **Guarde** la configuración.

## Pasos siguientes

* [Administrar imágenes de categoría con el selector de recursos](../manage-assets.md#category-images)
* [Administración de imágenes en el contenido de Page Builder](../manage-assets.md#using-aem-asset-selector-in-page-builder)
