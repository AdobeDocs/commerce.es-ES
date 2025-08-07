---
title: Eventos de Back Office
description: Descubra qué datos captura cada evento de back office.
role: Admin, Developer
feature: Personalization, Integration, Eventing
exl-id: 65cf8150-1a14-4d4c-aa0c-1545109e4fe7
source-git-commit: 1750aee715946d3a871e021cbbee687f54d1ff09
workflow-type: tm+mt
source-wordcount: '3618'
ht-degree: 0%

---

# [!DNL Data Connection] eventos de Back Office

A continuación se enumeran los eventos de back office de Commerce disponibles al instalar la extensión [!DNL Data Connection]. Los datos que estos eventos recopilan se envían a Adobe Experience Platform. También puede crear [eventos personalizados](custom-events.md) para recopilar datos adicionales que no se proporcionen de forma predeterminada.

Además de los datos que recopilan los eventos siguientes, también recibirá [otros datos](https://experienceleague.adobe.com/docs/experience-platform/edge/data-collection/automatic-information.html?lang=es) proporcionados por Adobe Experience Platform Web SDK.

Los eventos del back office contienen datos del lado del servidor. Estos datos incluyen [información sobre el estado del pedido](#order-status), por ejemplo, si se hizo, canceló, reembolsó, envió o completó un pedido. Los datos del lado del servidor también incluyen información sobre [eventos de perfil del cliente](#customer-profile-events), como si se creó, actualizó o eliminó una cuenta.

>[!NOTE]
>
>Todos los eventos de back office incluyen el campo [`identityMap`](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/identitymap.html?lang=es), que incluye la dirección de correo electrónico del comprador, cuando está disponible, y el ECID.

## Estado del pedido

Los datos de estado del pedido muestran una vista 360 del pedido del comprador. Esta vista ayuda a los comerciantes a dirigir o analizar mejor todo el estado del pedido al desarrollar campañas de marketing. Por ejemplo, puede identificar tendencias en ciertas categorías de productos que funcionan bien en diferentes épocas del año. Por ejemplo, ropa de invierno que se vende mejor durante los meses más fríos o ciertos colores de producto que los compradores están interesados en los últimos años. Además, los datos de estado de los pedidos pueden ayudarle a calcular el valor de cliente de por vida al comprender la tendencia de un comprador a realizar conversiones en función de pedidos anteriores.

### orderPlayed

| Descripción | Nombre de evento de XDM |
|---|---|
| Se activa cuando un comprador realiza un pedido. | `commerce.backofficeOrderPlaced` |

#### Datos recopilados de orderPlayed

En la tabla siguiente se describen los datos recopilados para este evento.

| Campo | Descripción |
|---|---|
| `commerce.order` | Contiene información sobre el pedido. |
| `commerce.order.purchaseID` | Identificador único asignado por el vendedor a esta compra o contrato. No hay garantía de que el ID sea único. |
| `commerce.order.payments` | La lista de pagos de este pedido. |
| `commerce.order.payments.paymentTransactionID` | Identificador único de esta transacción de pago. |
| `commerce.order.payments.paymentAmount` | El valor del pago. |
| `commerce.order.payments.paymentType` | El método de pago de este pedido. Se han contabilizado los valores personalizados permitidos. |
| `commerce.order.payments.currencyCode` | El código de divisa [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) usado, como `USD` o `EUR`. |
| `commerce.order.taxAmount` | El importe del impuesto pagado por el comprador como parte del pago final. |
| `commerce.order.discountAmount` | Indica el importe de descuento aplicado a todo el pedido. |
| `commerce.order.createdDate` | Fecha y hora en la que se crea un nuevo pedido en el sistema de comercio. Por ejemplo, `2022-10-15T20:20:39+00:00`. |
| `commerce.order.currencyCode` | El código de divisa en formato ISO 4217 usado para el total del pedido. |
| `commerce.shipping` | Detalles de envío de uno o más productos. |
| `commerce.shipping.shippingMethod` | El método de envío elegido por el cliente, como envío estándar, envío rápido, recogida en tienda, etc. |
| `commerce.shipping.shippingAmount` | El importe que el cliente tuvo que pagar por el envío. |
| `commerce.shipping.currencyCode` | El código de divisa en formato ISO 4217 usado para el total de envío. |
| `commerce.commerceScope` | Indica dónde se produjo un evento (vista de tienda, tienda, sitio web, etc.). |
| `commerce.commerceScope.environmentID` | El ID del entorno. ID alfanumérico de 32 dígitos separado por guiones. |
| `commerce.commerceScope.storeCode` | El código de almacén único. Puede tener muchas tiendas por sitio web. |
| `commerce.commerceScope.storeViewCode` | El código de vista de tienda único. Puede tener muchas vistas de la tienda por tienda. |
| `commerce.commerceScope.websiteCode` | El código único del sitio web. Puede tener muchos sitios web en un entorno. |
| `commerce.billing.address` | Dirección postal de facturación. |
| `commerce.billing.address.street1` | Información principal de la dirección postal, número de piso, número de calle y nombre de la calle |
| `commerce.billing.address.street2` | Campo adicional para información de nivel de calle. |
| `commerce.billing.address.city` | El nombre de la ciudad. |
| `commerce.billing.address.state` | El nombre del estado. Este es un campo de forma libre. |
| `commerce.billing.address.postalCode` | El código postal de la ubicación. Los códigos postales no están disponibles en todos los países. En algunos países, solo contiene parte del código postal. |
| `commerce.billing.address.country` | El nombre del territorio administrado por el gobierno. Aparte de `xdm:countryCode`, este es un campo de forma libre que puede tener el nombre del país en cualquier idioma. |
| `personalEmail` | Una dirección de correo electrónico personal. |
| `personalEmail.address` | La dirección técnica, por ejemplo, `name@domain.com`, tal como se define comúnmente en RFC2822 y estándares subsiguientes. |
| `productListItems` | Una matriz de productos en el pedido. |
| `productListItems.id` | El elemento de línea de esta entrada de producto. |
| `productListItems.SKU` | Unidad de stock. El identificador único del producto. |
| `productListItems.name` | El nombre para mostrar o el nombre legible en lenguaje natural del producto. |
| `productListItems.priceTotal` | El precio total de la línea de producto. |
| `productListItems.quantity` | Número de unidades de producto en el carro de compras. |
| `productListItems.discountAmount` | Indica el importe de descuento aplicado. |
| `productListItems.currencyCode` | El código de divisa [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) usado, como `USD` o `EUR`. |
| `productListItems.selectedOptions` | Campo utilizado para un producto configurable. |
| `productListItems.selectedOptions.attribute` | Identifica un atributo del producto configurable, como `size` o `color`. |
| `productListItems.selectedOptions.value` | Identifica el valor del atributo como `small` o `black`. |
| `productListItems.categories` | Contiene información sobre la categoría de un producto. |
| `productListItems.categories.id` | El identificador único de la categoría. |
| `productListItems.categories.name` | Nombre de la categoría. |
| `productListItems.categories.path` | La ruta a la categoría. |
| `productListItems.productImageUrl` | URL de imagen principal del producto. |

### orderInvoiced

| Descripción | Nombre de evento de XDM |
|---|---|
| Se activa cuando un comerciante envía una factura para solicitar el pago. | `commerce.backofficeOrderInvoiced` |

#### Datos recopilados de orderInvoiced

En la tabla siguiente se describen los datos recopilados para este evento.

| Campo | Descripción |
|---|---|
| `commerce.order` | Contiene información sobre el pedido. |
| `commerce.order.purchaseID` | Identificador único asignado por el vendedor a esta compra o contrato. No hay garantía de que el ID sea único. |
| `commerce.order.priceTotal` | El precio total de este pedido después de aplicar todos los descuentos e impuestos. |
| `commerce.order.currencyCode` | El código de divisa en formato ISO 4217 usado para el total del pedido. |
| `commerce.order.purchaseOrderNumber` | Identificador único asignado por el comprador a esta compra o contrato. |
| `commerce.order.payments` | La lista de pagos de este pedido. |
| `commerce.order.payments.currencyCode` | El código de divisa [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) usado, como `USD` o `EUR`. |
| `commerce.order.payments.paymentType` | El método de pago de este pedido. Se han contabilizado los valores personalizados permitidos. |
| `commerce.order.payments.paymentAmount` | El valor del pago. |
| `commerce.shipping` | Detalles de envío de uno o más productos. |
| `commerce.shipping.shippingMethod` | El método de envío elegido por el cliente, como envío estándar, envío rápido, recogida en tienda, etc. |
| `commerce.shipping.shippingAmount` | El importe que el cliente tuvo que pagar por el envío. |
| `commerce.commerceScope` | Indica dónde se produjo un evento (vista de tienda, tienda, sitio web, etc.). |
| `commerce.commerceScope.environmentID` | El ID del entorno. ID alfanumérico de 32 dígitos separado por guiones. |
| `commerce.commerceScope.storeCode` | El código de almacén único. Puede tener muchas tiendas por sitio web. |
| `commerce.commerceScope.storeViewCode` | El código de vista de tienda único. Puede tener muchas vistas de la tienda por tienda. |
| `commerce.commerceScope.websiteCode` | El código único del sitio web. Puede tener muchos sitios web en un entorno. |
| `personalEmail` | Una dirección de correo electrónico personal. |
| `personalEmail.address` | La dirección técnica, por ejemplo, `name@domain.com`, tal como se define comúnmente en RFC2822 y estándares subsiguientes. |
| `productListItems` | Una matriz de productos en el pedido. |
| `productListItems.id` | El elemento de línea de esta entrada de producto. |
| `productListItems.SKU` | Unidad de stock. El identificador único del producto. |
| `productListItems.name` | El nombre para mostrar o el nombre legible en lenguaje natural del producto. |
| `productListItems.priceTotal` | El precio total de la línea de producto. |
| `productListItems.quantity` | Número de unidades de producto en el carro de compras. |
| `productListItems.discountAmount` | Indica el importe de descuento aplicado. |
| `productListItems.categories` | Contiene información sobre la categoría de un producto. |
| `productListItems.categories.id` | El identificador único de la categoría. |
| `productListItems.categories.name` | Nombre de la categoría. |
| `productListItems.categories.path` | La ruta a la categoría. |

### orderItemsShipped

| Descripción | Nombre de evento de XDM |
|---|---|
| Se activa cuando se envía un pedido. | `commerce.backofficeOrderItemsShipped` |

#### Datos recopilados de orderItemsShipped

En la tabla siguiente se describen los datos recopilados para este evento.

| Campo | Descripción |
|---|---|
| `commerce.order` | Contiene información sobre el pedido. |
| `commerce.order.purchaseID` | Identificador único asignado por el vendedor a esta compra o contrato. No hay garantía de que el ID sea único. |
| `commerce.order.payments` | La lista de pagos de este pedido. |
| `commerce.order.payments.paymentTransactionID` | Identificador único de esta transacción de pago. |
| `commerce.order.payments.paymentAmount` | El valor del pago. |
| `commerce.order.payments.paymentType` | El método de pago de este pedido. Se han contabilizado los valores personalizados permitidos. |
| `commerce.order.payments.currencyCode` | El código de divisa [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) usado, como `USD` o `EUR`. |
| `commerce.order.priceTotal` | El precio total de este pedido después de aplicar todos los descuentos e impuestos. |
| `commerce.order.purchaseOrderNumber` | Identificador único asignado por el comprador a esta compra o contrato. |
| `commerce.order.currencyCode` | El código de divisa [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) usado, como `USD` o `EUR`. |
| `commerce.order.lastUpdatedDate` | Hora a la que se actualiza por última vez un registro de pedido determinado en el sistema de comercio. |
| `commerce.shipping` | Detalles de envío de uno o más productos. |
| `commerce.shipping.shippingMethod` | El método de envío elegido por el cliente, como envío estándar, envío rápido, recogida en tienda, etc. |
| `commerce.shipping.shippingAmount` | El importe que el cliente tuvo que pagar por el envío. |
| `commerce.shipping.address` | La dirección física de envío. |
| `commerce.shipping.address.street1` | Información principal de la dirección postal, número de piso, número de calle y nombre de la calle. |
| `commerce.shipping.address.street2` | Segunda línea para información de dirección (opcional) |
| `commerce.shipping.address.city` | El nombre de la ciudad. |
| `commerce.shipping.address.state` | El nombre del estado. Este es un campo de forma libre. |
| `commerce.shipping.address.postalCode` | El código postal de la ubicación. Los códigos postales no están disponibles en todos los países. En algunos países, solo contiene parte del código postal. |
| `commerce.shipping.address.country` | El nombre del territorio administrado por el gobierno. Aparte de `xdm:countryCode`, este es un campo de forma libre que puede tener el nombre del país en cualquier idioma. |
| `commerce.shipping.currencyCode` | El código de divisa [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) usado, como `USD` o `EUR`. |
| `commerce.shipping.trackingNumber` | Número de seguimiento proporcionado por el transportista para un envío de artículo de pedido. |
| `commerce.shipping.trackingURL` | Dirección URL para realizar un seguimiento del estado de envío de un artículo de pedido. |
| `commerce.shipping.shipDate` | La fecha en la que se envían uno o más artículos de un pedido. |
| `commerce.commerceScope` | Indica dónde se produjo un evento (vista de tienda, tienda, sitio web, etc.). |
| `commerce.commerceScope.environmentID` | El ID del entorno. ID alfanumérico de 32 dígitos separado por guiones. |
| `commerce.commerceScope.storeCode` | El código de almacén único. Puede tener muchas tiendas por sitio web. |
| `commerce.commerceScope.storeViewCode` | El código de vista de tienda único. Puede tener muchas vistas de la tienda por tienda. |
| `commerce.commerceScope.websiteCode` | El código único del sitio web. Puede tener muchos sitios web en un entorno. |
| `commerce.billing.address` | Dirección postal de facturación. |
| `commerce.billing.address.street1` | Información principal de la dirección postal, número de piso, número de calle y nombre de la calle |
| `commerce.billing.address.street2` | Campo adicional para información de nivel de calle. |
| `commerce.billing.address.city` | El nombre de la ciudad. |
| `commerce.billing.address.state` | El nombre del estado. Este es un campo de forma libre. |
| `commerce.billing.address.postalCode` | El código postal de la ubicación. Los códigos postales no están disponibles en todos los países. En algunos países, solo contiene parte del código postal. |
| `commerce.billing.address.country` | El nombre del territorio administrado por el gobierno. Aparte de `xdm:countryCode`, este es un campo de forma libre que puede tener el nombre del país en cualquier idioma. |
| `personalEmail` | Una dirección de correo electrónico personal. |
| `personalEmail.address` | La dirección técnica, por ejemplo, `name@domain.com`, tal como se define comúnmente en RFC2822 y estándares subsiguientes. |
| `productListItems` | Una matriz de productos en el pedido. |
| `productListItems.SKU` | Unidad de stock. El identificador único del producto. |
| `productListItems.name` | El nombre para mostrar o el nombre legible en lenguaje natural del producto. |
| `productListItems.priceTotal` | El precio total de la línea de producto. |
| `productListItems.quantity` | Número de unidades de producto en el carro de compras. |
| `productListItems.discountAmount` | Indica el importe de descuento aplicado. |
| `productListItems.currencyCode` | El código de divisa [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) usado, como `USD` o `EUR`. |
| `productListItems.selectedOptions` | Campo utilizado para un producto configurable. |
| `productListItems.selectedOptions.attribute` | Identifica un atributo del producto configurable, como `size` o `color`. |
| `productListItems.selectedOptions.value` | Identifica el valor del atributo como `small` o `black`. |
| `productListItems.categories` | Contiene información sobre la categoría de un producto. |
| `productListItems.categories.id` | El identificador único de la categoría. |
| `productListItems.categories.name` | Nombre de la categoría. |
| `productListItems.categories.path` | La ruta a la categoría. |

### orderCanceled

| Descripción | Nombre de evento de XDM |
|---|---|
| Se activa cuando un comprador cancela un pedido. | `commerce.backofficeOrderCancelled` |

#### Datos recopilados de orderCanceled

En la tabla siguiente se describen los datos recopilados para este evento.

| Campo | Descripción |
|---|---|
| `commerce.order` | Contiene información sobre el pedido. |
| `commerce.order.purchaseID` | Identificador único asignado por el vendedor a esta compra o contrato. No hay garantía de que el ID sea único. |
| `commerce.order.purchaseOrderNumber` | Identificador único asignado por el comprador a esta compra o contrato. |
| `commerce.order.cancelDate` | La fecha y hora en que un comprador cancela un pedido. |
| `commerce.order.lastUpdatedDate` | Hora a la que se actualiza por última vez un registro de pedido determinado en el sistema de comercio. |
| `commerce.commerceScope` | Indica dónde se produjo un evento (vista de tienda, tienda, sitio web, etc.). |
| `commerce.commerceScope.environmentID` | El ID del entorno. ID alfanumérico de 32 dígitos separado por guiones. |
| `commerce.commerceScope.storeCode` | El código de almacén único. Puede tener muchas tiendas por sitio web. |
| `commerce.commerceScope.storeViewCode` | El código de vista de tienda único. Puede tener muchas vistas de la tienda por tienda. |
| `commerce.commerceScope.websiteCode` | El código único del sitio web. Puede tener muchos sitios web en un entorno. |
| `personalEmail` | Una dirección de correo electrónico personal. |
| `personalEmail.address` | La dirección técnica, por ejemplo, `name@domain.com`, tal como se define comúnmente en RFC2822 y estándares subsiguientes. |

### orderLineItemRefund

| Descripción | Nombre de evento de XDM |
|---|---|
| Se activa cuando se reembolsa a un comprador un artículo devuelto. | `commerce.backofficeCreditMemoIssued` |

#### Datos recopilados de orderLineItemRefund

En la tabla siguiente se describen los datos recopilados para este evento.

| Campo | Descripción |
|---|---|
| `commerce.order` | Contiene información sobre el pedido. |
| `commerce.order.purchaseID` | Identificador único asignado por el vendedor a esta compra o contrato. No hay garantía de que el ID sea único. |
| `commerce.order.lastUpdatedDate` | Hora a la que se actualiza por última vez un registro de pedido determinado en el sistema de comercio. |
| `commerce.order.purchaseOrderNumber` | Identificador único asignado por el comprador a esta compra o contrato. |
| `commerce.refunds` | La lista de reembolsos de este pedido. |
| `commerce.refunds.transactionID` | Identificador único de este reembolso. |
| `commerce.refunds.refundAmount` | El valor del reembolso. |
| `commerce.refunds.refundPaymentType` | El método de pago de este pedido. Se han contabilizado los valores personalizados permitidos. |
| `commerce.refunds.currencyCode` | El código de divisa [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) usado, como `USD` o `EUR`. |
| `personalEmail` | Una dirección de correo electrónico personal. |
| `personalEmail.address` | La dirección técnica, por ejemplo, `name@domain.com`, tal como se define comúnmente en RFC2822 y estándares subsiguientes. |
| `productListItems` | Una matriz de productos en el pedido. |
| `productListItems.SKU` | Unidad de stock. El identificador único del producto. |
| `productListItems.name` | El nombre para mostrar o el nombre legible en lenguaje natural del producto. |
| `productListItems.priceTotal` | El precio total de la línea de producto. |
| `productListItems.quantity` | Número de unidades de producto en el carro de compras. |
| `productListItems.discountAmount` | Indica el importe de descuento aplicado. |
| `productListItems.currencyCode` | El código de divisa [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) usado, como `USD` o `EUR`. |
| `productListItems.selectedOptions` | Campo utilizado para un producto configurable. |
| `productListItems.selectedOptions.attribute` | Identifica un atributo del producto configurable, como `size` o `color`. |
| `productListItems.selectedOptions.value` | Identifica el valor del atributo como `small` o `black`. |
| `productListItems.categories` | Contiene información sobre la categoría de un producto. |
| `productListItems.categories.id` | El identificador único de la categoría. |
| `productListItems.categories.name` | Nombre de la categoría. |
| `productListItems.categories.path` | La ruta a la categoría. |

### orderItemsReturnInitiated

| Descripción | Nombre de evento de XDM |
|---|---|
| Se activa cuando un comprador solicita devolver un artículo. | `commerce.backofficeOrderItemsReturnInitiated` |

#### Datos recopilados de orderItemsReturnInitiated

En la tabla siguiente se describen los datos recopilados para este evento.

| Campo | Descripción |
|---|---|
| `commerce.order` | Contiene información sobre el pedido. |
| `commerce.order.purchaseID` | Identificador único asignado por el vendedor a esta compra o contrato. No hay garantía de que el ID sea único. |
| `commerce.order.returns` | La información de la RMA (Autorización de Devolución de Mercancías) para este pedido. |
| `commerce.order.returns.returnID` | El identificador único de esta RMA (autorización de devolución de mercancía). |
| `commerce.order.returns.returnStatus` | El estado de la RMA (autorización de devolución de mercancía), como Pendiente, Cerrado, etc. |
| `commerce.commerceScope` | Indica dónde se produjo un evento (vista de tienda, tienda, sitio web, etc.). |
| `commerce.commerceScope.environmentID` | El ID del entorno. ID alfanumérico de 32 dígitos separado por guiones. |
| `commerce.commerceScope.storeCode` | El código de almacén único. Puede tener muchas tiendas por sitio web. |
| `commerce.commerceScope.storeViewCode` | El código de vista de tienda único. Puede tener muchas vistas de la tienda por tienda. |
| `commerce.commerceScope.websiteCode` | El código único del sitio web. Puede tener muchos sitios web en un entorno. |
| `personalEmail` | Una dirección de correo electrónico personal. |
| `personalEmail.address` | La dirección técnica, por ejemplo, `name@domain.com`, tal como se define comúnmente en RFC2822 y estándares subsiguientes. |
| `productListItems` | Una matriz de productos en el pedido. |
| `productListItems.SKU` | Unidad de stock. El identificador único del producto. |
| `productListItems.name` | El nombre para mostrar o el nombre legible en lenguaje natural del producto. |
| `productListItems.quantity` | Número de unidades de producto en el carro de compras. |
| `productListItems.selectedOptions` | Campo utilizado para un producto configurable. |
| `productListItems.selectedOptions.attribute` | Identifica un atributo del producto configurable, como `size` o `color`. |
| `productListItems.selectedOptions.value` | Identifica el valor del atributo como `small` o `black`. |
| `productListItems.categories` | Contiene información sobre la categoría de un producto. |
| `productListItems.categories.id` | El identificador único de la categoría. |
| `productListItems.categories.name` | Nombre de la categoría. |
| `productListItems.categories.path` | La ruta a la categoría. |
| `productListItems.returnItem` | La información de la RMA (Autorización de Devolución de Mercancías) para este artículo. |
| `productListItems.returnItem.returnStatus` | El estado del elemento devuelto, como Pendiente, Aprobado, etc. |
| `productListItems.returnItem.returnReason` | El motivo por el que se solicita una devolución para este artículo. |
| `productListItems.returnItem.returnItemCondition` | La condición del elemento para el que se solicita la devolución. |
| `productListItems.returnItem.returnResolution` | La resolución solicitada del elemento devuelto, como Reembolso, Intercambio, etc. |
| `productListItems.returnItem.returnQuantityRequested` | El número de este artículo que el comprador solicitó devolver. |
| `productListItems.returnItem.returnQuantityAuthorized` | Número de este artículo que está autorizado a devolver. |
| `productListItems.returnItem.eturnQuantityReceived` | Número de artículos devueltos recibidos. |
| `productListItems.returnItem.returnQuantityApproved` | El número de este artículo con devolución totalmente completa y aprobada. |

### orderItemReturnCompleted

| Descripción | Nombre de evento de XDM |
|---|---|
| Se activa cuando se completa un artículo que un comprador solicitó devolver. | `commerce.backofficeOrderItemsReturnCompleted` |

#### Datos recopilados de orderItemReturnCompleted

En la tabla siguiente se describen los datos recopilados para este evento.

| Campo | Descripción |
|---|---|
| `commerce.order` | Contiene información sobre el pedido. |
| `commerce.order.purchaseID` | Identificador único asignado por el vendedor a esta compra o contrato. No hay garantía de que el ID sea único. |
| `commerce.order.returns` | La información de la RMA (Autorización de Devolución de Mercancías) para este pedido. |
| `commerce.order.returns.returnID` | El identificador único de esta RMA (autorización de devolución de mercancía). |
| `commerce.order.returns.returnStatus` | El estado de la RMA (autorización de devolución de mercancía), como Pendiente, Cerrado, etc. |
| `commerce.commerceScope` | Indica dónde se produjo un evento (vista de tienda, tienda, sitio web, etc.). |
| `commerce.commerceScope.environmentID` | El ID del entorno. ID alfanumérico de 32 dígitos separado por guiones. |
| `commerce.commerceScope.storeCode` | El código de almacén único. Puede tener muchas tiendas por sitio web. |
| `commerce.commerceScope.storeViewCode` | El código de vista de tienda único. Puede tener muchas vistas de la tienda por tienda. |
| `commerce.commerceScope.websiteCode` | El código único del sitio web. Puede tener muchos sitios web en un entorno. |
| `personalEmail` | Una dirección de correo electrónico personal. |
| `personalEmail.address` | La dirección técnica, por ejemplo, `name@domain.com`, tal como se define comúnmente en RFC2822 y estándares subsiguientes. |
| `productListItems` | Una matriz de productos en el pedido. |
| `productListItems.SKU` | Unidad de stock. El identificador único del producto. |
| `productListItems.name` | El nombre para mostrar o el nombre legible en lenguaje natural del producto. |
| `productListItems.selectedOptions` | Campo utilizado para un producto configurable. |
| `productListItems.selectedOptions.attribute` | Identifica un atributo del producto configurable, como `size` o `color`. |
| `productListItems.selectedOptions.value` | Identifica el valor del atributo como `small` o `black`. |
| `productListItems.categories` | Contiene información sobre la categoría de un producto. |
| `productListItems.categories.id` | El identificador único de la categoría. |
| `productListItems.categories.name` | Nombre de la categoría. |
| `productListItems.categories.path` | La ruta a la categoría. |
| `productListItems.returnItem` | La información de la RMA (Autorización de Devolución de Mercancías) para este artículo. |
| `productListItems.returnItem.returnStatus` | El estado del elemento devuelto, como Pendiente, Aprobado, etc. |
| `productListItems.returnItem.returnReason` | El motivo por el que se solicita una devolución para este artículo. |
| `productListItems.returnItem.returnItemCondition` | La condición del elemento para el que se solicita la devolución. |
| `productListItems.returnItem.returnResolution` | La resolución solicitada del elemento devuelto, como Reembolso, Intercambio, etc. |
| `productListItems.returnItem.returnQuantityRequested` | El número de este artículo que el comprador solicitó devolver. |
| `productListItems.returnItem.returnQuantityAuthorized` | Número de este artículo que está autorizado a devolver. |
| `productListItems.returnItem.eturnQuantityReceived` | Número de artículos devueltos recibidos. |
| `productListItems.returnItem.returnQuantityApproved` | El número de este artículo con devolución totalmente completa y aprobada. |

### orderShipmentCompleted

| Descripción | Nombre de evento de XDM |
|---|---|
| Se activa cuando se completa un envío. | `commerce.backofficeOrderShipmentCompleted` |

#### Datos recopilados de orderShipmentCompleted

En la tabla siguiente se describen los datos recopilados para este evento.

| Campo | Descripción |
|---|---|
| `commerce.order` | Contiene información sobre el pedido. |
| `commerce.order.purchaseID` | Identificador único asignado por el vendedor a esta compra o contrato. No hay garantía de que el ID sea único. |
| `commerce.order.payments` | La lista de pagos de este pedido. |
| `commerce.order.payments.paymentTransactionID` | Identificador único de esta transacción de pago. |
| `commerce.order.payments.paymentAmount` | El valor del pago. |
| `commerce.order.payments.paymentType` | El método de pago de este pedido. Se han contabilizado los valores personalizados permitidos. |
| `commerce.order.payments.currencyCode` | El código de divisa [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) usado, como `USD` o `EUR`. |
| `commerce.order.taxAmount` | El importe del impuesto pagado por el comprador como parte del pago final. |
| `commerce.order.createdDate` | Fecha y hora en la que se crea un nuevo pedido en el sistema de comercio. Por ejemplo, `2022-10-15T20:20:39+00:00`. |
| `commerce.shipping` | Detalles de envío de uno o más productos. |
| `commerce.shipping.shippingMethod` | El método de envío elegido por el cliente, como envío estándar, envío rápido, recogida en tienda, etc. |
| `commerce.shipping.shippingAmount` | El importe que el cliente tuvo que pagar por el envío. |
| `commerce.shipping.shipDate` | La fecha en la que se envían uno o más artículos de un pedido. |
| `commerce.shipping.address` | La dirección física de envío. |
| `commerce.shipping.address.street1` | Información principal de la dirección postal, número de piso, número de calle y nombre de la calle. |
| `commerce.shipping.address.street2` | Segunda línea para información de dirección (opcional) |
| `commerce.shipping.address.city` | El nombre de la ciudad. |
| `commerce.shipping.address.state` | El nombre del estado. Este es un campo de forma libre. |
| `commerce.shipping.address.postalCode` | El código postal de la ubicación. Los códigos postales no están disponibles en todos los países. En algunos países, solo contiene parte del código postal. |
| `commerce.shipping.address.country` | El nombre del territorio administrado por el gobierno. Aparte de `xdm:countryCode`, este es un campo de forma libre que puede tener el nombre del país en cualquier idioma. |
| `commerce.billing.address` | Dirección postal de facturación. |
| `commerce.billing.address.street1` | Información principal de la dirección postal, número de piso, número de calle y nombre de la calle |
| `commerce.billing.address.street2` | Campo adicional para información de nivel de calle. |
| `commerce.billing.address.city` | El nombre de la ciudad. |
| `commerce.billing.address.state` | El nombre del estado. Este es un campo de forma libre. |
| `commerce.billing.address.postalCode` | El código postal de la ubicación. Los códigos postales no están disponibles en todos los países. En algunos países, solo contiene parte del código postal. |
| `commerce.billing.address.country` | El nombre del territorio administrado por el gobierno. Aparte de `xdm:countryCode`, este es un campo de forma libre que puede tener el nombre del país en cualquier idioma. |
| `personalEmail` | Una dirección de correo electrónico personal. |
| `personalEmail.address` | La dirección técnica, por ejemplo, `name@domain.com`, tal como se define comúnmente en RFC2822 y estándares subsiguientes. |
| `productListItems` | Una matriz de productos en el pedido. |
| `productListItems.SKU` | Unidad de stock. El identificador único del producto. |
| `productListItems.name` | El nombre para mostrar o el nombre legible en lenguaje natural del producto. |
| `productListItems.priceTotal` | El precio total de la línea de producto. |
| `productListItems.quantity` | Número de unidades de producto en el carro de compras. |
| `productListItems.discountAmount` | Indica el importe de descuento aplicado. |
| `productListItems.currencyCode` | El código de divisa [ISO 4217](https://en.wikipedia.org/wiki/ISO_4217) usado, como `USD` o `EUR`. |
| `productListItems.selectedOptions` | Campo utilizado para un producto configurable. |
| `productListItems.selectedOptions.attribute` | Identifica un atributo del producto configurable, como `size` o `color`. |
| `productListItems.selectedOptions.value` | Identifica el valor del atributo como `small` o `black`. |
| `productListItems.categories` | Contiene información sobre la categoría de un producto. |
| `productListItems.categories.id` | El identificador único de la categoría. |
| `productListItems.categories.name` | Nombre de la categoría. |
| `productListItems.categories.path` | La ruta a la categoría. |

## Eventos de perfil de cliente

Los eventos de perfil capturados del lado del servidor incluyen información de la cuenta, como `accountCreated`, `accountUpdated` y `accountDeleted`. Estos datos se utilizan para rellenar los detalles clave del cliente que se necesitan para definir mejor los segmentos o ejecutar campañas de marketing, como enviar ofertas de descuento de suscripción, confirmaciones de cambio de cuenta, etc. Hay eventos de perfil similares capturados de la [tienda](events.md#customer-profile-events).

>[!NOTE]
>
>Cada evento de perfil de cliente también incluye el campo [`identityMap`](https://experienceleague.adobe.com/docs/experience-platform/xdm/field-groups/profile/identitymap.html?lang=es), que incluye el ID de cliente de Commerce generado por el sistema como identificador principal del perfil y un ID de correo electrónico que se utiliza como identificador secundario. [Obtenga información](custom-identities.md) sobre cómo crear atributos de identidad personalizados para mejorar la identificación del perfil del cliente.

### accountCreated

| Descripción | Nombre de evento de XDM |
|---|---|
| Se activa cuando un comprador intenta crear una cuenta. | `userAccount.backofficeCreateProfile` |

#### Datos recopilados de accountCreated

En la tabla siguiente se describen los datos recopilados para este evento.

| Campo | Descripción |
|---|---|
| `person` | Contiene información sobre el cliente. |
| `person.name` | Contiene información sobre el nombre del cliente. |
| `person.name.firstName` | Contiene el nombre del cliente. |
| `person.name.lastName` | Contiene los apellidos del cliente. |
| `personalEmail` | Una dirección de correo electrónico personal. |
| `personalEmail.address` | La dirección técnica, por ejemplo, `name@domain.com`, tal como se define comúnmente en RFC2822 y estándares subsiguientes. |
| `commerce.commerceScope` | Indica dónde se produjo un evento (vista de tienda, tienda, sitio web, etc.). |
| `commerce.commerceScope.environmentID` | El ID del entorno. ID alfanumérico de 32 dígitos separado por guiones. |
| `commerce.commerceScope.storeCode` | El código de almacén único. Puede tener muchas tiendas por sitio web. |
| `commerce.commerceScope.storeViewCode` | El código de vista de tienda único. Puede tener muchas vistas de la tienda por tienda. |
| `commerce.commerceScope.websiteCode` | El código único del sitio web. Puede tener muchos sitios web en un entorno. |

### accountUpdated

| Descripción | Nombre de evento de XDM |
|---|---|
| Se activa cuando un comprador intenta editar una cuenta. | `userAccount.backofficeUpdateProfile` |

#### Datos recopilados de accountUpdated

En la tabla siguiente se describen los datos recopilados para este evento.

| Campo | Descripción |
|---|---|
| `person` | Contiene información sobre el cliente. |
| `person.name` | Contiene información sobre el nombre del cliente. |
| `person.name.firstName` | Contiene el nombre del cliente. |
| `person.name.lastName` | Contiene los apellidos del cliente. |
| `personalEmail` | Una dirección de correo electrónico personal. |
| `personalEmail.address` | La dirección técnica, por ejemplo, `name@domain.com`, tal como se define comúnmente en RFC2822 y estándares subsiguientes. |
| `commerce.commerceScope` | Indica dónde se produjo un evento (vista de tienda, tienda, sitio web, etc.). |
| `commerce.commerceScope.environmentID` | El ID del entorno. ID alfanumérico de 32 dígitos separado por guiones. |
| `commerce.commerceScope.storeCode` | El código de almacén único. Puede tener muchas tiendas por sitio web. |
| `commerce.commerceScope.storeViewCode` | El código de vista de tienda único. Puede tener muchas vistas de la tienda por tienda. |
| `commerce.commerceScope.websiteCode` | El código único del sitio web. Puede tener muchos sitios web en un entorno. |

### accountDeleted

| Descripción | Nombre de evento de XDM |
|---|---|
| Se activa cuando un comprador intenta eliminar una cuenta. | `userAccount.backofficeDeleteProfile` |

#### Datos recopilados de accountDeleted

En la tabla siguiente se describen los datos recopilados para este evento.

| Campo | Descripción |
|---|---|
| `person` | Contiene información sobre el cliente. |
| `person.name` | Contiene información sobre el nombre del cliente. |
| `person.name.firstName` | Contiene el nombre del cliente. |
| `person.name.lastName` | Contiene los apellidos del cliente. |
| `personalEmail` | Una dirección de correo electrónico personal. |
| `personalEmail.address` | La dirección técnica, por ejemplo, `name@domain.com`, tal como se define comúnmente en RFC2822 y estándares subsiguientes. |
| `commerce.commerceScope` | Indica dónde se produjo un evento (vista de tienda, tienda, sitio web, etc.). |
| `commerce.commerceScope.environmentID` | El ID del entorno. ID alfanumérico de 32 dígitos separado por guiones. |
| `commerce.commerceScope.storeCode` | El código de almacén único. Puede tener muchas tiendas por sitio web. |
| `commerce.commerceScope.storeViewCode` | El código de vista de tienda único. Puede tener muchas vistas de la tienda por tienda. |
| `commerce.commerceScope.websiteCode` | El código único del sitio web. Puede tener muchos sitios web en un entorno. |
