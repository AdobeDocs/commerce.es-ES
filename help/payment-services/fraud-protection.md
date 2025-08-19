---
title: Protección contra el fraude significativo
description: Habilite la protección contra fraudes automatizada para  [!DNL Payment Services] con Signifyd.
role: Admin, User
level: Intermediate
feature: Payments, Checkout, Configuration, Security, Paas, Saas
exl-id: 440296bb-a6ff-408b-8195-3027916e4f84
source-git-commit: 870c2497a2d6dcfc4066c07f20169fc9040ae81a
workflow-type: tm+mt
source-wordcount: '372'
ht-degree: 0%

---

# Protección contra fraudes significativa

Puede habilitar la protección contra fraudes automatizada para [!DNL Payment Services] con la [extensión Signifyd](https://commercemarketplace.adobe.com/signifyd-module-connect.html).

Adobe Commerce es compatible con las versiones 5.4.0 y posteriores de Signifyd. [!DNL Payment Services] admite flujos Signify previos y posteriores a la autenticación.

La integración Signifyd/[!DNL Payment Services] proporciona cobertura para tarjetas de crédito, tarjetas de débito, tarjetas abovedadas, pagos a través del administrador y métodos de pago mediante PayPal y Apple Pay. Aunque algunos detalles de las transacciones no se comparten entre los Servicios de pago y Signifyd, Signifyd proporciona una cobertura de riesgo integral para todos los métodos de pago, asegurando la máxima protección.

>[!CAUTION]
>
> [Fastlane](payments-options.md#fastlane-button) no es compatible con Signifyd.

Consulte [Documentación de Signifyd](https://community.signifyd.com/support/s/article/magento-2-extension-install-guide?language=en_US#downloadandinstallingmagento2extension) para obtener más información sobre la instalación y configuración de la extensión.

## Incorporación

Debe comunicarse directamente con Signifyd para incorporar la extensión y usarla con [!DNL Payment Services]; no se necesita la configuración de [!DNL Payment Services]. Puede configurar la extensión Signifyd en el Administrador una vez instalada. Cualquier compatibilidad relacionada con esta extensión será administrada por Signifyd.

Al incorporar Signifyd, debe:

1. Póngase en contacto con Signifyd para configurar una nueva cuenta.
1. De manera predeterminada, Signifyd está [incluido en la lista de permitidos](https://github.com/signifyd/magento2/blob/main/docs/RESTRICT-PAYMENTS.md) para garantizar que Signifyd no dé su déclencheur para otras opciones de pago que no admite actualmente. Si quieres prohibir una forma de pago en particular, debes hacer cambios.
1. Confirme con Signifyd que PayPal no rechazará pedidos, a través de la configuración de protección contra fraude del comerciante en Paypal, que Signifyd pueda aprobar.
1. Habilite la extensión Signifyd para que sea compatible con [!DNL Payment Services]:
   * Cuando se usa [!DNL Payment Services] en el modo _Activo_, Signifyd debe estar en el modo de producción.
   * Cuando se usa [!DNL Payment Services] en el modo _espacio aislado_, Signifyd debe estar en modo de prueba.

## Configuración

Debido a que Signifyd realiza alguna acción sobre sus pedidos, es necesario configurar la extensión para que se comporte de manera adecuada en función de la acción de pago que estableció para [!DNL Payment Services].

Estas opciones de configuración no son compatibles con Payment Services ni con la integración de Signifyd:

* Cuando [!DNL Payment Services] está configurado con la acción de pago `Authorize` _y_ Signifyd está en modo `PostAuth` con la opción _[!UICONTROL Decline Guarantees]_&#x200B;establecida en **Crear nota de crédito**.

  Motivo: [!DNL Payment Services] crea una transacción de autorización que Signify intenta devolver.


* [!DNL Payment Services] está configurado con la acción de pago `Authorize and Capture` _y_ Signifyd está en modo `PostAuth` con la opción _[!UICONTROL Decline Guarantees]_&#x200B;establecida en **Cancelar pedido**.

  Razón: [!DNL Payment Services] crea una transacción de captura que Signifyd intenta anular.


Consulte la documentación de Signifyd para obtener información sobre [configuración de la extensión](https://community.signifyd.com/support/s/article/magento-2-extension-install-guide?language=en_US#configuringmagento2extension).

Consulte Documentación de Signifyd para [obtener más información sobre los flujos de trabajo de pedidos](https://community.signifyd.com/support/s/article/magento-2-extension-install-guide?language=en_US#howmagento2works).
