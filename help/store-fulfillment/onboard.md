---
title: Información general de incorporación para los servicios de Store Fulfillment
description: '[!DNL Live Search]: flujo de incorporación, requisitos del sistema, límites y limitaciones.'
role: Admin, Leader
level: Intermediate
feature: Shipping/Delivery, Install
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '361'
ht-degree: 0%

---

# Información general de incorporación para la adquisición de tiendas

Comience con [!DNL Store Fulfillment for Adobe Commerce by Walmart Commerce Technologies] configurando, configurando y habilitando los siguientes componentes:

- **Extensión Store Fulfillment**: instale y configure esta extensión de terceros en su instancia de Adobe Commerce. Después de la instalación, puede configurar y administrar la solución Store Fulfillment desde el administrador para admitir escenarios de [!DNL buys online, pickup in store] (BOPIS) en la tienda de Commerce.

  Configuración de ![[!DNL Store Fulfillment Service] en la vista de administración ](assets/store-fulfillment-admin-home.png)

- **Cuenta de satisfacción de pedidos**: durante el proceso de habilitación, un administrador de cuentas crea su cuenta de satisfacción de pedidos y le proporciona la información y las credenciales de la cuenta. Estas credenciales son necesarias para habilitar la conexión entre Adobe Commerce y la solución Store Fulfillment.

- **Aplicación Store Assist**: proporciona a los asociados de la tienda un flujo de trabajo integral de cumplimiento de la tienda para administrar pedidos de BOPIS desde dispositivos móviles. Store Associates puede descargar e instalar [!DNL Store Assist] de Walmart para dispositivos iOS y Android™. El proceso de incorporación de la aplicación es administrado por el Centro de clientes de Commerce Technologies de Walmart como un proceso independiente. Sin embargo, [algunos ajustes de configuración de la aplicación](user-setup.md) se han completado desde el administrador de Adobe Commerce.

  | Aplicación de asistencia de tienda: vista de introducción | Aplicación de asistencia de tienda: vista de módulos |
  |-------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|
  | ![[!DNL Store Assist App Getting Started] vista en dispositivo móvil](assets/store-assist-get-started-small.png) | ![[!DNL Store Assist App Orders view] en el dispositivo móvil](assets/store-assist-orders-small.png) |

## Pasos de aprovisionamiento

- **Regístrese para[!DNL Store Fulfillment for Adobe Commerce by Walmart Commerce Technologies]**: complete el formulario de registro en [business.adobe.com](https://business.adobe.com/resources/store-fulfillment.html) o póngase en contacto con el administrador de cuentas de Adobe Commerce para obtener ayuda.

- **Inicia la solicitud de aprovisionamiento para la satisfacción de pedidos de la tienda**-Completa el formulario de admisión proporcionado por tu administrador de cuentas para proporcionar la información necesaria para comenzar el proceso de aprovisionamiento.

- **Consigue las credenciales de tu cuenta de Store Fulfillment**-Una vez creada la cuenta de Store Fulfillment, recibirás las credenciales necesarias para integrar la solución Store Fulfillment con Adobe Commerce.

- **[Descargue el código fuente para instalar la [!DNL Store Fulfillment] extensión](install.md)**

## Pasos de incorporación

1. [Instale la extensión Store Fulfillment para Adobe Commerce](install.md).

1. Desde el administrador, [habilite la solución](enable-general.md).

1. [Configure la extensión Store Fulfillment desde el administrador de Adobe Commerce](service-config-settings-overview.md).

1. [Conecte el servicio [!DNL Store Fulfillment] usando las credenciales de cumplimiento de la tienda que se le han proporcionado](connect-set-up-service.md).

1. [Crear usuarios y roles para la aplicación de asistencia de tienda](user-setup.md).

1. [Descargue la aplicación  [!DNL Store Assist] de Walmart en el dispositivo que desee. La aplicación está disponible en las tiendas de aplicaciones de Apple (iOS) y Google Play (Android™)](app-setup.md).

Una vez que haya instalado, configurado, completado la incorporación correctamente y tenga acceso a la aplicación [!DNL Store Assist], podrá [empezar a crear pedidos y realizar pruebas](test-and-deploy.md).
