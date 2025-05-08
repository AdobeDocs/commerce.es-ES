---
title: Informes
description: Utilice el informe Transacciones para obtener visibilidad sobre las tasas de autorización de transacciones y las tendencias de transacciones.
role: User
level: Intermediate
exl-id: dd1d80f9-5983-4181-91aa-971522eb56fa
source-git-commit: 4482c1f93a424c73497b88c707d0ab93a694c957
workflow-type: tm+mt
source-wordcount: '1270'
ht-degree: 0%

---

# Informes

[!DNL Payment Services] para [!DNL Adobe Commerce] y [!DNL Magento Open Source] le ofrece informes completos para que pueda obtener una visión clara de las transacciones, pedidos y pagos de su tienda.

![Informe de transacciones](assets/transactions-report.png){width="700" zoomable="yes"}

El informe Transacciones proporciona visibilidad sobre las tasas de autorización de transacciones y las tendencias negativas de las transacciones para que pueda monitorizar de forma eficaz el estado de su tienda e identificar y abordar de forma preventiva cualquier problema de transacción.

Ver transacciones individuales para pedidos realizados en la tienda y sus métodos de pago, resultados, códigos de respuesta de pago, etc.

La información proporcionada en el informe Transacciones está destinada únicamente a uso comercial. No comparta esta información con clientes u otros posibles estafadores. La información de transacciones podría utilizarse para omitir las comprobaciones de seguridad o realizar pedidos que resulten en devoluciones de cargos.

Puede descargar el informe Transacciones en formato de archivo .csv para utilizarlo con el software de contabilidad o de gestión de pedidos existente.

>[!NOTE]
>
>No puede ver informes financieros si no ha [incorporado y activado el modo Activo](production.md#enable-live-payments) para [!DNL Payment Services].

## Vista del informe de transacciones

La vista Informe de transacciones está disponible en la vista Transacciones de Servicios de pago. Incluye toda la información disponible sobre las transacciones de tu tienda o tiendas.

En la barra lateral _Admin_, vaya a **[!UICONTROL Sales]** > **[!UICONTROL Payment Services]** > _[!UICONTROL Transactions]_>**[!UICONTROL View Report]**&#x200B;para ver la vista detallada del informe de transacciones tabulares.

![Vista del informe de transacciones](assets/transactions-report-view.png){width="800" zoomable="yes"}

Puede configurar esta vista, según las secciones de este tema, para presentar mejor los datos que desee ver.

Consulte los ID de pedido de Commerce y de transacción de PayPal vinculados, los importes de transacción, la forma de pago por transacción y mucho más, todo ello dentro de este informe.

No todos los métodos de pago proporcionan la misma granularidad de la información. Por ejemplo, las transacciones con tarjeta de crédito proporcionan códigos de respuesta, AVS y CCV, y los últimos cuatro dígitos de la tarjeta en el informe Transacciones; los botones de pago de PayPal no.

Puede [descargar transacciones](#download-transactions) en formato de archivo .csv para usarlas con software de contabilidad o administración de pedidos existente.

>[!WARNING]
>
> El informe de transacciones no incluirá ninguna captura realizada fuera de [!DNL Payment Services].

### Seleccionar fuente de datos

En la vista Informe de transacciones, puede seleccionar el origen de datos (**[!UICONTROL Live]** o **[!UICONTROL Sandbox]**) cuyos resultados desea ver.

![Selección de orígenes de datos](assets/datasource.png){width="300" zoomable="yes"}

Si _[!UICONTROL Live]_&#x200B;es el origen de datos seleccionado, puede ver información de informes de las tiendas que usan [!DNL Payment Services] en el modo de producción. Si&#x200B;_[!UICONTROL Sandbox]_ es el origen de datos seleccionado, puede ver la información del informe del modo de espacio aislado.

Las selecciones de fuentes de datos funcionan de la siguiente manera:

* Si no tiene ningún almacén que use [!DNL Payment Services] en el modo de producción, la selección de origen de datos toma como valor predeterminado _[!UICONTROL Sandbox]_.
* Si tiene tiendas (una o varias) que usan [!DNL Payment Services] en el modo de producción, la selección de origen de datos toma como valor predeterminado _[!UICONTROL Live]_.
* Las exportaciones de informes siempre respetan la selección de fuente de datos.

Para seleccionar el origen de datos de su informe [!UICONTROL Transactions]:

1. En la barra lateral _Admin_, vaya a **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Transactions]_>**[!UICONTROL View Report]**.
1. Haga clic en **[!UICONTROL Data source]** y seleccione **[!UICONTROL Live]** o **[!UICONTROL Sandbox]**.

   Los resultados del informe se regeneran en función del origen de datos seleccionado.

### Personalizar fechas/periodo

Desde la vista Informe de transacciones, puede personalizar el periodo de tiempo de las transacciones que desea ver seleccionando fechas específicas. De forma predeterminada, se muestran en la cuadrícula 30 días de transacciones.

1. En la barra lateral _Admin_, vaya a **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Transactions]_>**[!UICONTROL View Report]**.
1. Haga clic en el filtro de selector de calendario **[!UICONTROL Transaction dates]**.
1. Seleccione el intervalo de fechas aplicable.
1. Ver las transacciones para las fechas especificadas en la cuadrícula.

### Filtrar información del informe

En la vista Informe de transacciones, puede filtrar los resultados de los estados que desea ver seleccionando criterios de filtro.

1. En la barra lateral _Admin_, vaya a **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Transactions]_>**[!UICONTROL View Report]**.
1. Haga clic en el selector **[!UICONTROL Filter]**.
1. Cambie las opciones _[!UICONTROL Transaction Result]_&#x200B;para ver los resultados del informe solamente para las transacciones de pedidos seleccionadas.
1. Cambie las opciones _[!UICONTROL Payment Method]_&#x200B;para ver los resultados del informe para el tipo de pago utilizado para la transacción.
1. Active las opciones _[!UICONTROL Payment Detail]_&#x200B;para ver información adicional sobre el tipo de pago utilizado, cuando esté disponible.
1. Escriba _Importe mínimo de pedido_ o _Importe máximo de pedido_ para ver los resultados del informe dentro de ese intervalo de importe de pedido.
1. Escriba un _[!UICONTROL Order ID]_&#x200B;para buscar una transacción específica.
1. Introduce _[!UICONTROL Card Last Four]_&#x200B;para buscar una tarjeta de crédito o débito específica.
1. Escriba un _[!UICONTROL Customer ID]_&#x200B;para mostrar todas las transacciones de un cliente específico.
1. Escriba _[!UICONTROL Customer Email]_&#x200B;para filtrar las transacciones de ese correo electrónico.
1. Haga clic en **[!UICONTROL Hide filters]** para ocultar el filtro.

### Mostrar y ocultar columnas

El informe Transacciones muestra todas las columnas de información disponibles de forma predeterminada. Sin embargo, puede personalizar qué columnas ve en el informe.

1. En la barra lateral _Admin_, vaya a **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Transactions]_>**[!UICONTROL View Report]**.
1. Haga clic en el icono **[!UICONTROL Column settings]** ![icono de configuración de columna](assets/column-settings.png){width="20" zoomable="yes"}.
1. Para personalizar las columnas que se ven en el informe, marque o desmarque las columnas de la lista.

   El informe Transacciones muestra inmediatamente los cambios realizados en el menú Configuración de columna. Las preferencias de columna se guardan y se mantienen en vigor si se aleja de la vista Informes.

### Actualización de datos del informe

La vista Informe de transacciones muestra una marca de tiempo _[!UICONTROL Last updated]_&#x200B;que indica la última vez que se actualizó la información del informe. De forma predeterminada, los datos del informe de transacciones se actualizan automáticamente cada tres horas.

También puede forzar manualmente una actualización de los datos del informe para ver la información del informe más actualizada.

1. En la barra lateral _Admin_, vaya a **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > _[!UICONTROL Transactions]_>**[!UICONTROL View Report]**.
1. Haga clic en el icono _Actualizar_ (![icono de actualización](assets/refresh-button-med.png){width="20" zoomable="yes"}).

   Los datos del informe de transacciones se actualizan, aparece una confirmación *[!UICONTROL Update complete]* y la información más reciente está presente en la cuadrícula.

### Descargar transacciones

Puede descargar un archivo .csv con todas las transacciones visibles en la cuadrícula de la vista de transacciones, independientemente de si está viendo los 30 días predeterminados de transacciones o un periodo de tiempo personalizado.

1. En la barra lateral _Admin_, vaya a **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]** > **[!UICONTROL Transactions]**.
1. Si desea ver transacciones de un período de tiempo distinto de los últimos 30 días, [personalice el intervalo de tiempo para sus estados](#customize-dates-timeframe).
1. Haga clic en el icono _Descargar_ ![icono de descarga](assets/icon-download.png){width="20" zoomable="yes"}.

Las transacciones se descargan en formato .csv.

### Descripciones de columna

Los informes de transacciones incluyen la siguiente información.

| Columna | Descripción |
| ------------ | -------------------- |
| [!UICONTROL Order ID] | ID de pedido de Commerce (contiene solo valores para transacciones correctas y está vacío para transacciones rechazadas)<br> <br>Para ver [información de pedido](https://experienceleague.adobe.com/es/docs/commerce-admin/stores-sales/order-management/orders/orders){target="_blank"} relacionada, haga clic en el identificador. |
| [!UICONTROL PayPal Transaction ID] | ID de transacción proporcionado por el proveedor de pagos; contiene solo valores para las transacciones correctas y contiene un guión para las transacciones rechazadas. Puedes hacer clic en este identificador para acceder a la página de detalles de la transacción de PayPal. |
| [!UICONTROL Customer ID] | ID de cliente de Commerce de un pedido <br> <br>Vea el tema [información del cliente](https://experienceleague.adobe.com/es/docs/commerce-admin/customers/customer-accounts/account-create){target="_blank"} para obtener más información. |
| [!UICONTROL Transaction Date] | Marca de fecha y hora de transacción |
| [!UICONTROL Payment Method] | Tipo de pago utilizado para la transacción con información sobre la marca y el tipo de tarjeta. Consulte [tipos de tarjeta](https://developer.paypal.com/docs/api/orders/v2/#definition-card_type) para obtener más información; disponible para las versiones 1.6.0 y posteriores de Payment Services |
| [!UICONTROL Payment Detail] | Proporciona información adicional sobre el tipo de pago utilizado para la transacción, cuando está disponible. |
| [!UICONTROL Card Last Four] | Últimos cuatro dígitos de las tarjetas de crédito o débito utilizadas para la transacción |
| [!UICONTROL Result] | El resultado de la transacción—*[!UICONTROL OK]* (transacción correcta), *[!UICONTROL Rejected by Payment Provider]* (rechazado por PayPal), *[!UICONTROL Rejected by Bank]* (rechazado por el banco que emitió la tarjeta) |
| [!UICONTROL Response Code] | Código de error que proporciona un motivo de rechazo del proveedor de pagos o del banco; consulte la lista de posibles códigos de respuesta y descripciones para [`Rejected by Bank` estado](https://developer.paypal.com/docs/api/orders/v2/#definition-processor_response) y [`Rejected by Payment Provider` estado](https://developer.paypal.com/api/rest/reference/orders/v2/errors/). |
| [!UICONTROL AVS Code] | Código de servicio de verificación de direcciones; la información de respuesta del procesador para las solicitudes de pago. Vea [lista de posibles códigos y descripciones](https://developer.paypal.com/docs/api/orders/v2/#definition-processor_response) para obtener más información. |
| [!UICONTROL CVV Code] | Código de valor de verificación de tarjeta para tarjetas de crédito y débito; consulte [lista de códigos y descripciones posibles](https://developer.paypal.com/docs/api/orders/v2/#definition-processor_response) para obtener más información. |
| [!UICONTROL Amount] | Importe del pedido de la transacción |
| [!UICONTROL Currency] | Divisa utilizada para el pedido en la transacción |
| [!UICONTROL Type] | [Acción de pago](../payment-services/production.md#set-payment-services-as-payment-method) para la transacción—`Authorize` o `Authorize and Capture` |

### Códigos de respuesta de error

La columna _Código de respuesta_ muestra un error específico o un código de éxito relacionado con la transacción. Algunos códigos de error comunes que puede ver en pantalla son:

* `PAYMENT_DENIED`: PayPal rechazó la transacción porque se sospechaba que era fraudulenta.
* `INTERNAL_SERVER_ERROR`: PayPal rechazó la transacción y se produjo un error en el servidor de PayPal. Se puede volver a intentar la transacción.
* `INSTRUMENT_DECLINED`: PayPal rechazó el cliente por el método de pago seleccionado. La transacción se puede reintentar con un método de pago diferente.
* `9500`: el banco asociado rechazó la transacción porque se sospechaba que era fraudulenta.
* `5120`: el banco asociado rechazó la transacción porque el cliente no tenía fondos suficientes para el pago.
* `5650`: el banco asociado rechazó la transacción porque el banco requiere autenticación sólida de clientes ([3DS](security.md#3ds)).

Los códigos de respuesta de error detallados para transacciones fallidas están disponibles para transacciones posteriores al 1 de junio de 2023. Los datos de informe parciales aparecerán para las transacciones que se produjeron antes del 1 de junio de 2023.
