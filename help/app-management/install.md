---
title: Instalar y obtener acceso a  [!DNL App Management]
description: Requisitos previos y requisitos de acceso para usar Adobe Commerce [!DNL App Management].
feature: App Builder, Extensibility, Integration
source-git-commit: 86c0945bbb0a562de1b66d420dec2a05d4d81e5f
workflow-type: tm+mt
source-wordcount: '410'
ht-degree: 0%

---

# Instalar y tener acceso a [!DNL App Management]

[!DNL App Management] está disponible en el administrador de Commerce para instancias de Commerce aptas. La disponibilidad depende del tipo de implementación.

## Disponibilidad

Después de cumplir con los siguientes requisitos, seleccione la ficha correspondiente para su tipo de implementación a continuación, para ver si [!DNL App Management] requiere instalación o ya está disponible en su instancia.

## Requisitos previos

Antes de asociar una aplicación, asegúrese de que dispone de lo siguiente:

| Requisito | Descripción |
|-------------|-------------|
| **Acceso de administrador** | Administrador de Commerce con permisos para [!DNL App Management] |
| **Aplicación implementada** | Aplicación de App Builder implementada en su organización y lista para conectarse |
| **Acceso a la organización** | Acceso a la organización de Adobe donde se implementa la aplicación |

>[!BEGINTABS]

>[!TAB Adobe Commerce as a Cloud Service]

[!DNL App Management] está disponible automáticamente en [!DNL Adobe Commerce as a Cloud Service]. No es necesario realizar ninguna instalación. [Habilítelo en el administrador](#access-app-management) y empiece a asociar aplicaciones.

>[!TAB Adobe Commerce en la nube (PaaS) y local]

* **Adobe Commerce 2.4.8 y posterior**—[!DNL App Management] se incluye automáticamente. No es necesario realizar ninguna instalación.

* **Adobe Commerce 2.4.5 a 2.4.7**—Instale [!DNL Admin UI SDK] (que incluye [!DNL App Management]) usando Composer:

  ```bash
  composer require "magento/commerce-backend-sdk": ">=3.3"
  ```

  A continuación, ejecute:

  ```bash
  composer update
  bin/magento setup:upgrade
  bin/magento indexer:reindex
  bin/magento cache:clean
  ```

Consulte [Instalar o actualizar la IU de administración de Adobe Commerce SDK](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/installation/){target="_blank"} para obtener más información.

>[!ENDTABS]

## Acceder a [!DNL App Management]

1. Inicie sesión en el administrador de Commerce.

1. Vaya a **[!UICONTROL Apps]** > **[!UICONTROL App Management]**.

Se muestra la vista [!DNL App Management]. Aquí puede asociar, configurar y administrar aplicaciones de App Builder.

## Instalación de aplicaciones de App Builder

Si necesita instalar una aplicación de App Builder desde Adobe Exchange (por ejemplo, una aplicación prediseñada de integración o Marketplace), consulte [Instalar aplicaciones de App Builder desde Adobe Exchange](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/install-app-builder-app){target="_blank"} para obtener instrucciones paso a paso.

Después de instalar e implementar una aplicación, usa [!DNL App Management] para [asociarla a tu instancia de Commerce](manage-app.md#associate-an-app) y configurar su configuración.

## Webhooks y aplicaciones de Commerce

Algunas aplicaciones de App Builder usan [webhooks de Adobe Commerce](https://developer.adobe.com/commerce/extensibility/webhooks/) para que Commerce pueda llamar a su aplicación a través de HTTP cuando se produzcan ciertos eventos (por ejemplo, después de guardar un producto). Los extremos de los ganchos web y la lógica de suscripción los define **el desarrollador de aplicaciones** cuando se crea e implementa la aplicación; los administradores de tiendas no configuran los ganchos web por separado en la administración de aplicaciones.

Después de [asociar la aplicación](https://experienceleague.adobe.com/en/docs/commerce/app-management/manage-app/manage-app) con su instancia de Commerce y completar las instrucciones de configuración de la aplicación, el comportamiento del gancho web sigue la implementación de la aplicación.

Si [!DNL App Management] no puede almacenar en déclencheur el extremo de validación de la aplicación (por ejemplo, la dirección URL no está disponible o la respuesta no cumple los requisitos), es posible que vea un error similar al siguiente en el panel [!DNL App Management]:

![Error de validación de webhook](assets/webhook-validation-error.png){width="600" zoomable="yes"}

Trabaje con el **desarrollador de aplicaciones** para corregir la configuración o implementación del webhook de modo que la validación se pueda realizar correctamente.

**Desarrolladores de aplicaciones**. Para implementar suscripciones a ganchos web y respuestas de controladores de App Builder, consulte [Webhooks](https://developer.adobe.com/commerce/extensibility/app-management/installation/webhooks/) en la documentación para desarrolladores de Commerce Extensibility y el paquete [`@adobe/aio-commerce-lib-webhooks`](https://github.com/adobe/aio-commerce-sdk/tree/main/packages/aio-commerce-lib-webhooks) en GitHub.
