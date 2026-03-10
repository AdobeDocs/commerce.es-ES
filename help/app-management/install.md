---
title: Instalar y obtener acceso a  [!DNL App Management]
description: Requisitos previos y requisitos de acceso para usar Adobe Commerce [!DNL App Management].
feature: App Builder, Extensibility, Integration
source-git-commit: ab635fecb7b82294bd4a4fd045ed71931e9d265d
workflow-type: tm+mt
source-wordcount: '247'
ht-degree: 1%

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
