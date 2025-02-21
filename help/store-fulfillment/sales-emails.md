---
title: Plantillas de correo electrónico de ventas
description: Configure las plantillas de correo electrónico transaccionales para comunicarse con los clientes y los administradores de las tiendas durante el proceso de cumplimiento de los pedidos de recogida en las tiendas.
role: Admin
level: Intermediate
feature: Shipping/Delivery, Communications, Configuration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1233'
ht-degree: 1%

---


# Plantillas de correo electrónico de ventas

Store Fulfillment ofrece un conjunto ampliado de plantillas de correo electrónico transaccionales para admitir flujos de trabajo de pedidos y envíos. Ofrecen una comunicación y mensajería coherentes y automatizadas entre canales, que notifican a los administradores de clientes y tiendas sobre los cambios de estado de los pedidos, las instrucciones para los pedidos de recogida en la tienda y mucho más.

Las plantillas de correo electrónico de Store Fulfillment se configuran con la mensajería y la configuración predeterminadas. Los administradores de comerciantes de Adobe Commerce pueden administrar y modificar las configuraciones y seleccionar las plantillas de correo electrónico para comunicarse con los clientes en diferentes situaciones. Los administradores también pueden configurar y personalizar plantillas.

Configure las plantillas de correo electrónico de ventas desde el administrador: **[!UICONTROL Stores > Configuration > Sales > Sales Emails]**.

## Correos electrónicos: configuración general

<table>
<thead>
<tr>
<th><strong>Campo</strong></th>
<th><strong>Descripción</strong></th>
<th><strong>Ámbito</strong></th>
<th><strong>Requerido</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>Envío asincrónico</strong></td>
<td>Determina si los correos electrónicos de ventas se envían de forma asíncrona. Opciones: <br/>**`Deshabilitar`** - (Predeterminado) Los mensajes de correo electrónico de ventas se envían cuando se activan mediante un evento. Utilice la configuración predeterminada para agilizar la comunicación y el tiempo de respuesta de la recogida en tienda. <br/>**`Enable`**: al habilitar esta opción, se mueven al segundo plano los procesos que administran las notificaciones por correo electrónico de cierre de compra y procesamiento de pedidos para que se envíen a intervalos regulares predeterminados.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
</tbody></table>

## Pedido listo para recoger en tienda

<table>
<thead>
<tr>
<th><strong>Campo</strong></th>
<th><strong>Descripción</strong></th>
<th><strong>Ámbito</strong></th>
<th><strong>Requerido</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>Habilitado</strong></td>
<td>Este correo electrónico se envía al cliente cuando el dependiente de la tienda ha completado la selección de su pedido. Establézcalo en "No" para deshabilitar la notificación por correo electrónico. Si la plantilla de correo electrónico está desactivada, no impide que el asociado de la tienda seleccione un pedido.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
<tr>
<td><strong>Pedido Listo Para La Recogida Remitente De Correo Electrónico</strong></td>
<td>La identidad del remitente utilizada al enviar la notificación por correo electrónico.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
<tr>
<td><strong>Orden Listo Para La Recogida Plantilla De Correo Electrónico</strong></td>
<td>Plantilla de mensaje de correo electrónico utilizada para notificar a los clientes registrados. Con la integración se proporciona una plantilla predeterminada.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
<td><strong>Plantilla de correo electrónico de pedido listo para recoger para invitado</strong></td>
<td>Plantilla de mensaje de correo electrónico utilizada para notificar a los clientes invitados. Con la integración se proporciona una plantilla predeterminada.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
<tr>
<td><strong>Orden listo para la recogida Plantilla de correo electrónico para la recogida alternativa Contacto</strong></td>
<td>La plantilla de mensaje de correo electrónico utilizada para notificar a contactos adicionales nombrados en el pedido. Con la integración se proporciona una plantilla predeterminada.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
<tr>
<td><strong>Enviar Copia Del Pedido Listo Para Su Recogida Por Correo Electrónico A</strong></td>
<td>Una lista delimitada por comas de direcciones de correo electrónico para enviar una copia de cada notificación.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
<tr>
<td><strong>Enviar Pedido Listo Para Recogida Por Correo Electrónico Método De Copia</strong></td>
<td>El método de copia de correo electrónico (copia de carbón) que se va a utilizar.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
</tbody></table>


## El pedido se ha recogido en la tienda

<table>
<thead>
<tr>
<th><strong>Campo</strong></th>
<th><strong>Descripción</strong></th>
<th><strong>Ámbito</strong></th>
<th><strong>Requerido</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>Habilitado</strong></td>
<td>Este correo electrónico se envía al cliente cuando para confirmar que ha recogido su pedido de la tienda. Establézcalo en "No" para deshabilitar la notificación por correo electrónico. Si la plantilla de correo electrónico está desactivada, no impide que el cliente recoja un pedido.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
<tr>
<td><strong>El Pedido Se Ha Recogido En El Remitente De Correo Electrónico</strong></td>
<td>La identidad del remitente utilizada al enviar la notificación por correo electrónico.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
<tr>
<td><strong>Se Ha Recogido La Plantilla De Correo Electrónico Del Pedido</strong></td>
<td>Plantilla de mensaje de correo electrónico utilizada para notificar a los clientes registrados. La integración proporciona una plantilla predeterminada</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
<td><strong>Se ha recogido el pedido como plantilla de correo electrónico para el invitado</strong></td>
<td>Plantilla de mensaje de correo electrónico utilizada para notificar a los clientes invitados. Con la integración se proporciona una plantilla predeterminada.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
<tr>
<td><strong>Enviar Se Ha Recopilado Una Copia Por Correo Electrónico A</strong></td>
<td>Una lista delimitada por comas de direcciones de correo electrónico para enviar una copia de cada notificación.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
<tr>
<td><strong>Enviar Se Ha Recopilado Mediante El Método De Copia De Correo Electrónico</strong></td>
<td>El método de copia de correo electrónico (copia de carbón) que se va a utilizar.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
</tbody></table>

## Pedido aplazado

<table>
<thead>
<tr>
<th><strong>Campo</strong></th>
<th><strong>Descripción</strong></th>
<th><strong>Ámbito</strong></th>
<th><strong>Requerido</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>Habilitado</strong></td>
<td>Este correo electrónico se envía al cliente para notificarle un retraso en el procesamiento o la selección de su pedido en la tienda del comerciante. Establézcalo en "No" para deshabilitar la notificación por correo electrónico. Si la plantilla de correo electrónico está deshabilitada, la función no evita que se retrase una solicitud.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
<tr>
<td><strong>Solicitar remitente de correo electrónico aplazado
</strong></td>
<td>La identidad del remitente utilizada al enviar la notificación por correo electrónico.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
<tr>
<td><strong>Plantilla de correo electrónico con retraso del pedido</strong></td>
<td>Plantilla de mensaje de correo electrónico utilizada para notificar a los clientes registrados. Con la integración se proporciona una plantilla predeterminada.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
<td><strong>Plantilla de correo electrónico de pedido aplazado para invitado</strong></td>
<td>Plantilla de mensaje de correo electrónico utilizada para notificar a los clientes invitados. Con la integración se proporciona una plantilla predeterminada.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
<tr>
<td><strong>Enviar copia de correo electrónico aplazado de pedido a</strong></td>
<td>Una lista delimitada por comas de direcciones de correo electrónico para enviar una copia de cada notificación.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
<tr>
<td><strong>Enviar método de copia aplazada de pedido</strong></td>
<td>El método de copia de correo electrónico (copia de carbón) que se va a utilizar.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
</tbody></table>



## Pedido cancelado

<table>
<thead>
<tr>
<th><strong>Campo</strong></th>
<th><strong>Descripción</strong></th>
<th><strong>Ámbito</strong></th>
<th><strong>Requerido</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>Habilitado</strong></td>
<td>Este correo electrónico se envía al cliente para notificarle que su pedido se ha cancelado en la tienda del comerciante. Se estableció en <code>No</code> para deshabilitar la notificación por correo electrónico. Si la plantilla de correo electrónico está desactivada, esta función no impide que se cancele un pedido.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
<tr>
<td><strong>Remitente de correo electrónico cancelado del pedido
</strong></td>
<td>La identidad del remitente utilizada al enviar la notificación por correo electrónico.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
<tr>
<td><strong>Plantilla de correo electrónico de pedido cancelado</strong></td>
<td>Plantilla de mensaje de correo electrónico utilizada para notificar a los clientes registrados. Con la integración se proporciona una plantilla predeterminada.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
<td><strong>Pedido cancelado para invitado</strong></td>
<td>Plantilla de mensaje de correo electrónico utilizada para notificar a los clientes invitados. Con la integración se proporciona una plantilla predeterminada.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
<tr>
<td><strong>Enviar copia de correo electrónico de pedido cancelado a</strong></td>
<td>Una lista delimitada por comas de direcciones de correo electrónico para enviar una copia de cada notificación.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
<tr>
<td><strong>Enviar método de copia cancelada de pedido</strong></td>
<td>El método de copia de correo electrónico (copia de carbón) que se va a utilizar.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
</tbody></table>


## Pedido Parcialmente Cancelado

<table>
<thead>
<tr>
<th><strong>Campo</strong></th>
<th><strong>Descripción</strong></th>
<th><strong>Ámbito</strong></th>
<th><strong>Requerido</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>Habilitado</strong></td>
<td>Este correo electrónico se envía al cliente para notificarle que parte de su pedido se ha cancelado en la tienda del comerciante. Se estableció en <code>No</code> para deshabilitar la notificación por correo electrónico. Si la plantilla de correo electrónico está desactivada, no impide que se cancele parcialmente una solicitud.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
<tr>
<td><strong>Remitente de correo electrónico parcialmente cancelado del pedido
</strong></td>
<td>La identidad del remitente utilizada al enviar la notificación por correo electrónico.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
<tr>
<td><strong>Plantilla de correo electrónico de pedido parcialmente cancelado</strong></td>
<td>Plantilla de mensaje de correo electrónico utilizada para notificar a los clientes registrados. Con la integración se proporciona una plantilla predeterminada.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
<td><strong>Plantilla de correo electrónico de pedido parcialmente cancelado para contacto de recogida alternativo</strong></td>
<td>La plantilla de mensaje de correo electrónico utilizada para notificar a contactos adicionales nombrados en el pedido. Con la integración se proporciona una plantilla predeterminada.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
<tr>
<td><strong>Pedido Parcialmente Cancelado para Invitado</strong></td>
<td>Plantilla de mensaje de correo electrónico utilizada para notificar a los clientes invitados. Con la integración se proporciona una plantilla predeterminada.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
<tr>
<td><strong>Enviar Copia De Correo Electrónico De Pedido Parcialmente Cancelado A</strong></td>
<td>Una lista delimitada por comas de direcciones de correo electrónico para enviar una copia de cada notificación.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
<tr>
<td><strong>Enviar método de copia de pedido parcialmente cancelado</strong></td>
<td>El método de copia de correo electrónico (copia de carbón) que se va a utilizar.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
</tbody></table>

## Enviar a tienda

<table>
<thead>
<tr>
<th><strong>Campo</strong></th>
<th><strong>Descripción</strong></th>
<th><strong>Ámbito</strong></th>
<th><strong>Requerido</strong></th>
</tr>
</thead>
<tbody><tr>
<td><strong>El pedido tiene un remitente de correo electrónico de productos de envío a tienda</strong></td>
<td>Correo electrónico enviado al personal del comerciante especificado como un informe agregado de todos los pedidos abiertos que no se pueden seleccionar en una tienda de comerciantes hasta que su inventario esté disponible. </br></br> Los comerciantes pueden usar este informe para iniciar y administrar transferencias de inventario de tienda a tienda o reaprovisionamiento. </br></br>Esta notificación solo se aplica cuando las características de [!DNL Ship-to-Store] están habilitadas.
</br></br>Esta etiqueta no afecta al transportista seleccionado ni a las etiquetas de método de envío disponibles.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
<tr>
<td><strong>Enviar a destinatarios de correo electrónico de tienda</strong></td>
<td>Una lista delimitada por comas de direcciones de correo electrónico para enviar una copia de cada notificación.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
<tr>
<td><strong>Plantilla de correo electrónico</strong></td>
<td>Plantilla del mensaje de correo electrónico utilizada para notificar a los destinatarios. Con la integración se proporciona una plantilla predeterminada.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
</tbody></table>

>[!NOTE]
>
>Si permite pedidos no satisfechos, debe proporcionar una dirección de correo electrónico de administrador para recibir notificaciones sobre estos pedidos. Agregue la dirección a las siguientes opciones de configuración: **[!UICONTROL Send Order Delayed Email Copy To]** en la plantilla [Demora del pedido](#order-delayed) y [!UICONTROL Ship To Store Email Recipients] en la plantilla [Enviar a tienda](#ship-to-store).



