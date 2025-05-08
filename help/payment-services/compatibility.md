---
title: Compatibilidad para  [!DNL Payment Services]
description: Aprende si [!DNL Payment Services] está disponible en tu país y si es compatible con tu versión de Adobe Commerce.
role: User
level: Intermediate
feature: Payments, Checkout, Paas, Saas
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---


# Compatibilidad para [!DNL Payment Services]

[!DNL Payment Services] está disponible para Adobe Commerce y Magento Open Source. [!DNL Payment Services] ahora es compatible con las versiones 2.4.x de Adobe Commerce.

## Requisitos previos

Para usar [!DNL Payment Services], primero tendrá que conectar su instancia de Commerce. **Solo configuró esta conexión una vez**.

1. Si no está seguro de si la instancia está conectada, vaya a **Sistema** > Servicios > **Conector de servicios de Commerce** y vea los valores de las claves API públicas y privadas en las secciones Claves de espacio aislado y Claves de producción, y los campos Proyecto y Espacio de datos en la sección Identificador de SaaS. Si esos valores están presentes, la instancia está conectada.

1. Si todavía necesita conectar su instancia, consulte las instrucciones en la página [Conector de servicios de Commerce](../landing/saas.md).

   >[!TIP]
   >
   > Vea nuestro tutorial de [Adobe Commerce Services Connector](https://experienceleague.adobe.com/es/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-commerce-services-connector) para obtener más información.

1. Si ya ha conectado su instancia, vaya a la página [incorporación](onboard.md) para ver los pasos siguientes.

>[!IMPORTANT]
>
> Todos los comerciantes con derecho a [!DNL Payment Services] pueden usar **un espacio de datos de producción** y **dos espacios de datos de prueba**.

## Experiencia [!DNL Payment Services] estándar frente a avanzada

[!DNL Payment Services] proporciona las opciones de pago y los flujos de incorporación de **Estándar** (Pago exprés) y **Avanzado** (totalmente compatible), según el país en el que opere.

>[!NOTE]
>
> [!DNL Payment Services] proporciona [funciones de Pago y envío exprés](../payment-services/payments-options.md) (subconjunto de opciones de pagos) para otros [países disponibles durante la incorporación](../payment-services/production.md#complete-merchant-onboarding).

### ¿Qué opción de [!DNL Payment Services] es adecuada para usted?

>[!VIDEO](https://video.tv.adobe.com/v/3447811)

Consulte [Connect](connect.md) para obtener más información sobre cómo configurar la extensión de [!DNL Payment Services].

>[!BEGINTABS]

>[!TAB Estándar (Pago y envío exprés)]

![cheque](assets/icon-check.png) Pago y envío mediante PayPal

![cheque](assets/icon-check.png) botón de débito o tarjeta de crédito de PayPal

![comprobar](assets/icon-check.png) configuraciones de cierre de compra personalizadas

![comprobar](assets/icon-check.png) precio estándar

![comprobar](assets/icon-check.png) **Disponible en XX países**

[![más información](assets/learn-more-button.svg)](onboard.md)

>[!TAB Avanzado (Totalmente Compatible)]

![cheque](assets/icon-check.png) tarjeta de débito

![cheque](assets/icon-check.png) crédito de PayPal

![comprobar](assets/icon-check.png) campos de tarjeta de crédito

![comprobar](assets/icon-check.png) botón Apple Pay

![comprobar](assets/icon-check.png) botón Google Pay

![comprobar](assets/icon-check.png) botones de pago de PayPal

![comprobar](assets/icon-check.png) botón Venmo

![cheque](assets/icon-check.png) botón de débito o tarjeta de crédito de PayPal

![cheque](assets/icon-check.png) botón Pagar más tarde

![comprobar](assets/icon-check.png) configuraciones de cierre de compra personalizadas

![comprobar](assets/icon-check.png) precios personalizados

![comprobar](assets/icon-check.png) (capacidades de precios L2/L3 - solo EE. UU.)

![comprobar](assets/icon-check.png) **Solo disponible en Estados Unidos (EE.UU.), Canadá (CA) y Australia (AUS). Francia (FR), Reino Unido (UK)**

[![más información](assets/learn-more-button.svg)](onboard.md)

>[!ENDTABS]

Consulte las páginas [Política del ciclo vital](https://experienceleague.adobe.com/docs/commerce-operations/release/planning/lifecycle-policy.html?lang=es) y [[!DNL Payment Services] Notas de la versión](release-notes.md) para obtener más información específica de la versión y la versión.

Para obtener las instrucciones completas e iniciar el proceso de incorporación, consulta [Introducción a [!DNL Payment Services]](onboard.md).

### Tarjetas de crédito y divisas aceptadas

[!DNL Payment Services] acepta las monedas de los países [en los que está disponible](#availability). Consulte [Configuración de moneda](https://experienceleague.adobe.com/docs/commerce-admin/stores-sales/site-store/currency/currency-configuration.html?lang=es) para obtener más información sobre la configuración de tasas de moneda.

Para obtener más información sobre las divisas y los métodos de pago disponibles con los productos y servicios de PayPal, consulte las siguientes páginas:

* [Documentación sobre monedas admitidas](https://developer.paypal.com/docs/reports/reference/paypal-supported-currencies/).

* [Documentación sobre métodos de pago](https://developer.paypal.com/docs/checkout/payment-methods/).
