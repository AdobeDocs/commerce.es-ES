---
title: Configurar tu tienda
description: Aprenda a ejecutar la herramienta de andamiaje para configurar su tienda  [!DNL Adobe Commerce as a Cloud Service] Storefront.
feature: Storefront
role: Developer
level: Beginner
exl-id: 02928dc4-1777-483e-b0ee-b04fc813864d
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
source-git-commit: 6eda2197fde2e88292e58b2bb4fc4759f24da558
workflow-type: tm+mt
source-wordcount: '235'
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

* Para obtener más información sobre cómo administrar y mostrar contenido y datos en la tienda, consulta [actualizar contenido de la tienda](./use-cases.md#update-storefront-content).
* Para obtener más información sobre las características de experimentación contextual, vea [experimentación contextual](./use-cases.md#contextual-experimentation).
* Para obtener más información sobre el uso de la IA generativa para automatizar la generación de contenido de alta calidad, consulte [Generar variaciones](./use-cases.md#generate-variations).
* Para obtener más información sobre la actualización del contenido del sitio y la integración con los componentes de front-end y los datos del back-end de Commerce, consulte [[!DNL Adobe Commerce Storefront documentation]](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=es).
