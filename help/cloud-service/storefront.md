---
title: Configurar tu tienda
description: Aprenda a ejecutar la herramienta de andamiaje para configurar su tienda  [!DNL Adobe Commerce as a Cloud Service] Storefront.
feature: Storefront
role: Developer
level: Beginner
exl-id: 02928dc4-1777-483e-b0ee-b04fc813864d
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
source-git-commit: 0cd9749574460374a8fe875f1eff54f2a4a8d614
workflow-type: tm+mt
source-wordcount: '250'
ht-degree: 0%

---

# Configurar tu tienda

Para configurar su [!DNL Adobe Commerce Storefront] con tecnología de [!DNL Edge Delivery Services] para [!DNL Adobe Commerce as a Cloud Service] (SaaS), complete los siguientes pasos.

Para obtener un tutorial más personalizable y detallado, consulte la [documentación de tienda](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/?lang=es).

1. Abra la [herramienta de creación de sitios](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator).

1. Seleccione **[!UICONTROL Create New Site (Code & Content)]**.

1. Escriba **[!UICONTROL Github Organization/Username]** donde desee crear el repositorio de código de tienda.

1. Escriba un **[!UICONTROL Site Name]**.

1. En el campo **[!UICONTROL Commerce GraphQL Endpoint (optional)]**, introduzca su extremo de GraphQL [!DNL Adobe Commerce as a Cloud Service] (SaaS), al cual puede acceder en el Administrador de Commerce Cloud después de [crear su instancia](./getting-started.md#create-an-instance).

   Alternativamente, si está usando [[!DNL API Mesh]](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic), ingrese su extremo de GraphQL [!DNL API Mesh] en el campo **[!UICONTROL Commerce GraphQL Endpoint (optional)]**. Consulte [crear una malla](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic/create-mesh) para obtener más información.

1. Haga clic en **[!UICONTROL Create Site]**. Siga las instrucciones en pantalla para autorizar el acceso al repositorio de GitHub.

Una vez completado el proceso, puede personalizar la tienda mediante los siguientes métodos:

* Personalice su código: `https://github.com/<username or org>/<repo name>`
* Edite el contenido: `https://da.live/#/<username or org>/<repo name>`
* Administrar su configuración: `https://da.live/sheet#/<username or org>/<repo name>/configs-stage`
* Vista previa de tu tienda: `https://main--<repo name>--<username or org>.aem.page/`

## Pasos siguientes

Consulte los siguientes artículos para obtener más información:

* [Actualizando contenido de tienda](./use-cases.md#update-storefront-content): administra y muestra contenido y datos en la tienda.
* [Experimentación contextual](./use-cases.md#contextual-experimentation): crea y administra experimentos en tu tienda.
* [Generar variaciones](./use-cases.md#generate-variations): utilice IA generativa para automatizar la generación de contenido de alta calidad.
* [Documentación de Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=es): obtenga información detallada sobre cómo actualizar el contenido del sitio e integrarlo con componentes de front-end y datos de back-end de Commerce.
* [Servicio de configuración](https://www.aem.live/docs/config-service-setup): obtenga información sobre cómo migrar la configuración de la tienda de `config.json` para que use el servicio de configuración, que admite casos de uso avanzados como reposta la configuración y las superposiciones.
