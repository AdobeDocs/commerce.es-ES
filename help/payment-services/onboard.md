---
title: Incorporado [!DNL Payment Services]
description: Conecta tu instancia con la funcionalidad  [!DNL Payment Services] completando algunos pasos de incorporación.
role: User
level: Intermediate
feature: Payments, Checkout, Integration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# Incorporar [!DNL Payment Services]

Para empezar a usar [!DNL Payment Services] para [!DNL Adobe Commerce] y [!DNL Magento Open Source], debe completar algunos pasos de incorporación para conectar su instancia con la funcionalidad de pagos.

## Flujo de incorporación

Este diagrama de flujo muestra el proceso general de incorporación de [!DNL Payment Services].

![Flujo de incorporación](assets/onboarding-diagram.svg){width="600" zoomable="yes"}

>[!NOTE]
>
> Para las versiones de Adobe Commerce 2.4.7 o posteriores, puede omitir el paso de la extensión Marketplace, ya que [!DNL Payment Services] está disponible de forma predeterminada.

Después de completar la incorporación para los pagos en vivo o en la zona protegida, se puede acceder a los informes financieros desde [!DNL Payment Services] en el Administrador.

Si tanto la zona protegida como los pagos activos están incorporados y habilitados, puede cambiar fácilmente entre esos modos desde la página de inicio de [!DNL Payment Services].

## Requisitos previos

Para usar [!DNL Payment Services], debe tener habilitados todos los módulos dependientes y los siguientes disponibles para su instancia:

* Módulo de Conector de servicios
* Módulo de ID de servicios
* Claves de API

Los módulos Conector de servicios e ID de servicios se instalan automáticamente durante la [instalación de [!DNL Payment Services]](install.md).

Cuando finalice la instalación, puede ver una nueva sección en los valores de configuración (**[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**) si expande **[!UICONTROL Services]**—**[!UICONTROL Commerce Services Connector]**.

Para obtener información sobre cómo crear claves API o acceder a ellas, consulte [Credenciales de API](#obtain-api-credentials).

## Pasos de incorporación

1. [Instale la [!DNL Payment Services] extensión](install.md#get-payment-services).
1. [Obtener credenciales de API](connect.md#obtain-api-credentials).
1. [Conecte su instancia](connect.md#configure-commerce-services) a los servicios de Commerce. Esta conexión solo debe completarse una vez por cada instancia de Commerce.
1. [Configura el servicio de zona protegida](sandbox.md#enable-sandbox-testing) (o, alternativamente, continúa con [habilitar pagos activos](sandbox.md#enable-live-payments) si has probado la funcionalidad en otro entorno) con una cuenta de procesamiento de pagos PayPal de prueba.
1. [Establece [!DNL Payment Services] como tu método de pago](production.md#set-payment-services-as-payment-method), en modo de espacio aislado, para comenzar a procesar pagos de prueba.
1. [Solicite el derecho de pagos](production.md#request-payments-entitlement-from-adobe) para habilitar la incorporación activa.
1. [Incorporación completa del comerciante](production.md#complete-merchant-onboarding) para habilitar los pagos activos para los sitios web de Commerce.
1. [Obtén tu [!DNL Payment Services] ID de comerciante](production.md#configure-pricing-tier) y entrégaselo a Ventas para configurar el nivel de precios correcto.
1. [Activar [!DNL Payment Services] en el modo Activo](production.md#enable-live-payments) para comenzar a procesar pagos activos.
1. Pagos de prueba, tanto en entornos de [espacio aislado](sandbox.md#test-in-sandbox-environment) como de [producción](production.md#test-in-production).

>[!NOTE]
>
>Si no configura los servicios de Commerce en el Administrador (paso 3), no podrá configurar la zona protegida ni los pagos activos.

## Resolución de problemas

* [Solucionar problemas [!DNL Payment Services] instalación](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-install.html?lang=en)
* [Cuenta de zona protegida de PayPal no verificada](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-paypal-acct.html)
* [Datos de informe [!DNL Payment Services] aplazados](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-report-info-delayed.html)
* [La tarjeta de crédito de prueba falla con PayPal al procesar pagos en un entorno limitado](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/payments/payservices-cc-sandbox-failure.html?lang=en)
