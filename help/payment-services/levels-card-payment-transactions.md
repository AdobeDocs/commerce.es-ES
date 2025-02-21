---
title: Procesamiento de los niveles 2 y 3
description: Niveles de procesamiento de pagos con tarjeta dentro de  [!DNL Payment Services] transacciones.
role: Admin
feature: Payments
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---

# Procesamiento de los niveles 2 y 3

Hay tres niveles de procesamiento de tarjetas disponibles mediante [!DNL Payment Services]:

* El nivel 1 es el más común, requiere menos información y, por lo tanto, en general incurre en tasas de intercambio más altas en comparación con las transacciones procesadas con datos de nivel 2 o nivel 3, que suelen estar relacionadas con tarjetas de crédito corporativas y de compra.

* Con los niveles 2 y 3, los clientes de [!DNL Payment Services] en el precio de Interchange Plus (IC++) que acepten muchas transacciones de tarjetas de compra o corporativas pueden recibir potencialmente una tasa de procesamiento menor al permitir que [!DNL Payment Services] envíe más información sobre una transacción. Si la transacción cumple los requisitos, según los requisitos de la red de tarjetas, el comerciante puede recibir una tasa de procesamiento menor para una transacción en particular.

>[!NOTE]
>
>Los precios de nivel 2 y nivel 3 solo se aplican a las transacciones Visa y MasterCard. American Express sólo ofrece precios de nivel 2. Discover no ofrece precios de nivel 2 ni de nivel 3. Consulta [procesamiento de pagos](https://developer.paypal.com/docs/checkout/advanced/processing/){target=_blank} en la documentación para desarrolladores de PayPal para obtener más información.

Ver [Qué es IC++?](https://www.paypal.com/us/brc/article/what-is-interchange-plus-plus){target=_blank} en la documentación para desarrolladores de PayPal para obtener más información.

Los datos de procesamiento de los niveles 2 y 3 permiten a los comerciantes reducir sus precios de CI++ si proporcionan algunos detalles adicionales sobre la compra que reducen el riesgo del procesador y proporcionan aspectos beneficiosos:

* Los clientes grandes pagarán menos al proporcionar estos datos de procesamiento.

* Es menos probable que los clientes se encuentren con situaciones fraudulentas, ya que los pedidos tienen más información.

Sin embargo, las redes de tarjetas, como Visa y Mastercard, determinan en última instancia si una transacción cumple los requisitos para el procesamiento de nivel 2 o nivel 3:

* Los datos del nivel 2 contienen información adicional, como el importe de impuestos del pedido o el código de cliente o el número de pedido.

* Los datos del Nivel 3 son información más detallada sobre la venta, lo que ayuda a calificar para tasas de intercambio aún más bajas en comparación con el Nivel 2. Los datos del nivel 3 contienen información como una descripción del artículo comprado, la cantidad de unidades compradas, la unidad de medida de los artículos pedidos y otros detalles específicos.

[!DNL Payment Services] recopila estos datos y proporciona un informe detallado de sus transacciones de pago.

## Transacciones de pago con tarjeta de nivel 2 y nivel 3 en [!DNL Payment Services]

Para ser apto para el procesamiento de nivel 2 o nivel 3, los comerciantes deben enviar la información anterior, aunque son las redes de tarjetas las que finalmente determinan para qué nivel se califica una transacción al procesarla.

Consulta las [Preguntas frecuentes sobre el procesamiento de pagos](https://www.paypal.com/us/cshelp/article/ts2278?_ga=1.131773126.875104296.1712843492){target=_blank} en la documentación para desarrolladores de PayPal para obtener más información.

El procesamiento de nivel 2 y nivel 3 está deshabilitado de manera predeterminada para [!DNL Payment Services] comerciantes en el nivel de tienda.

El procesamiento de los niveles 2 y 3 está disponible si ya utiliza los precios de IC++. Para habilitar esta característica, puede hacerlo mediante la [Interfaz de línea de comandos (CLI](configure-cli.md)).

>[!IMPORTANT]
>
>Si tiene alguna pregunta, comuníquese con el administrador de cuentas de [!DNL Payment Services].
