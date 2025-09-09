---
title: Configurar tu tienda
description: Aprenda a ejecutar la herramienta de andamiaje para configurar su tienda  [!DNL Adobe Commerce as a Cloud Service] Storefront.
role: Developer
exl-id: 02928dc4-1777-483e-b0ee-b04fc813864d
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
source-git-commit: 408f28bdc20708022c8eca0fbfea4adb17014bf7
workflow-type: tm+mt
source-wordcount: '282'
ht-degree: 0%

---

# Configurar tu tienda

Para configurar la tienda de Adobe Commerce con tecnología Edge Delivery Services para Adobe Commerce as a Cloud Service (SaaS), siga estos pasos.

Si desea un tutorial más personalizable y detallado, consulte la [documentación de tienda](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/).

1. Abra la [herramienta de creación de sitios](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator).

1. Seleccione **Crear nuevo sitio (código y contenido)**.

1. Escriba **Github Organization/Username** donde desee crear el repositorio de código de tienda.

1. Escriba un **Nombre del sitio**.

1. En el campo **Punto final de Commerce GraphQL (opcional)**, introduzca su punto final de Adobe Commerce as a Cloud Service (SaaS) GraphQL, al que puede acceder en Commerce Cloud Manager después de [crear su instancia](./getting-started.md#create-an-instance).

   Alternativamente, si está usando [API Mesh](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic), ingrese su punto final de API Mesh GraphQL en el campo **Punto final de Commerce GraphQL (opcional)**. Consulte [crear una malla](https://developer.adobe.com/graphql-mesh-gateway/mesh/basic/create-mesh) para obtener más información.

1. Haga clic en **Crear sitio**. Siga las instrucciones que aparecen en pantalla para autorizar el acceso al repositorio de Github.

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
* Para obtener más información sobre cómo actualizar el contenido del sitio e integrar con componentes de front-end y datos de back-end de Commerce, consulte la [documentación de Adobe Commerce Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/).
