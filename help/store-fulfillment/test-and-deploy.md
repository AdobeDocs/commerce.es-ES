---
title: Prueba e implementación de cumplimiento de tienda
description: Plan de prueba para verificar la funcionalidad de Store Fulfillment. Las pruebas cubren la API de sincronización de inventario, el flujo de trabajo de cumplimiento completo para pedidos cancelados, la administración de usuarios de la aplicación Store Fulfillment y la experiencia de llegada del cliente.
role: User, Admin
level: Intermediate
feature: Shipping/Delivery, User Account, Roles/Permissions
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '2661'
ht-degree: 0%

---

# Prueba e implementación de la adquisición de tiendas para Adobe Commerce

Una vez completado el proceso de incorporación en el entorno de desarrollo, puede iniciar el proceso para probar e implementar la solución Store Fulfillment en el entorno de producción.

**Requisitos previos**

Antes de probar o sincronizar cualquier información, almacén o pedido, compruebe que ha completado las siguientes tareas:

- Se completó la [configuración general](enable-general.md) para los servicios de cumplimiento de tiendas.

- [Añada y valide las credenciales de la cuenta y los detalles de conexión para su zona protegida y sus entornos de producción](connect-set-up-service.md#configure-store-fulfillment-account-credentials)

- Confirme que la [integración de Adobe Commerce](connect-set-up-service.md#configure-store-fulfillment-account-credentials) para la solución Store Fulfillment está disponible y autorizada.

## Preparar para pruebas

La configuración de la conexión debe completarse antes de poder crear cualquier pedido de prueba o realizar pruebas de integración. Antes de realizar la prueba, también debe comprobar que los datos de almacén estén sincronizados.

1. Sincronizar fuentes de Satisfacción de Pedidos de Almacén.

   - Ir a **[!UICONTROL Stores > Sources]**.

   - Seleccione **[!UICONTROL Synchronize Store Fulfillment Sources]**.

1. En la cuadrícula del almacén, compruebe que los almacenes se han marcado como `Synced` antes de crear pedidos de prueba.

## Ejemplo de plan de pruebas

Los minoristas validan la funcionalidad básica de la solución Store Fulfillment durante las fases de configuración y prueba de una implementación. Este plan de prueba de ejemplo proporciona un punto de partida para las pruebas. Añada escenarios adicionales según sus necesidades.

>[!NOTE]
>
>Después de completar la incorporación inicial de la solución Store Fulfillment o de actualizar una instalación existente, pruebe siempre la aplicación en un entorno que no sea de producción antes de implementarla en producción.

Este plan de pruebas de muestra abarca las siguientes áreas funcionales:

| Área funcional | Función | Rol |
|-------------------------------------|------------------------------------------|----------------------------------|
| Sincronización de inventario y pedido | Sincronización de API de inventario | Administrador de Adobe Commerce |
| De extremo a extremo | Flujos de trabajo de cancelación de pedidos | Cliente, administrador y asociado de tienda |
| Administrador | Permisos de aplicación de Store Fulfillment | Administrador |
| Adobe Commerce Frontend | Tipos de productos | Cliente, administrador |
| Cierre de compra de Frontend</br>Formulario de registro | Experiencia de llegada | Cliente, administrador |
| Aplicación de asistencia de tienda | Pedido</br>Seleccionar</br>Fase</br>y entrega | Asociado de tienda |

### Sincronización de API de inventario

Esta sección del plan de prueba cubre la sincronización de inventario y pedido para verificar que las actualizaciones de los orígenes de recogida y stock estén sincronizadas correctamente entre Adobe Commerce y la solución Store Fulfillment.

**Área funcional**: Sincronización de inventario y pedidos</br>
**Rol:** Administrador</br>
**Tipo de prueba:** Todos positivos

<table>
<thead>
<tr>
<th>Función</th>
<th>Escenario de prueba</th>
<th>Resultados esperados</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>Agregar origen de stock de recogida</strong></td>
<td>Guardar un nuevo origen de stock de recogida.</td>
<td>La sincronización en tiempo real envía los detalles de la fuente al servicio Walmart GIF en un plazo de 5 minutos.</td>
</tr>
<tr>
<td><strong>Actualizar origen de stock de recogida existente</strong></td>
<td>Guardar actualizaciones en un origen de stock de recogida existente.</td>
<td>La operación de sincronización en tiempo real envía los detalles al GIF de Walmart en un plazo de 5 minutos</td>
</tr>
<tr>
<td><strong>Estado de origen de existencias de recogida </br><code>Is Synced</code></strong></td>
<td>Guardar actualizaciones en un origen de stock de recogida existente.</td>
<td>Después de una operación correcta, la columna <code>Is Synced</code> de la página Administrar Source se actualiza de <code>No</code> a <code>Yes</code>.</td>
</tr>
<tr>
<td><strong>Proceso de reserva de stock modificado</strong></td>
<td>Crear y enviar un nuevo pedido de un producto.</td>
<td>La cantidad vendible del producto disminuye en consecuencia.</td>
</tr>
<tr>
<td><strong>Inserción de nuevo pedido, sincronización de API: pedido del cliente</strong></td>
<td>El cliente envía una orden de recogida de la tienda.</td>
<td><ul><li>En la vista Orden de administración, un <strong>usuario administrador de Adobe Commerce</strong> ve que el estado de sincronización de pedidos se ha actualizado a <code>Sent</code></li><li>El registro de detalles del pedido incluye el mensaje <code>Order was sent to BOPIS solution for sync, it's not yet acknowledged yet.</code></li></ul></td>
</tr>
<tr>
<td><strong>Inserción de nuevo pedido, sincronización de API: el administrador envía el pedido</strong></td>
<td>Un Adobe Commerce <strong>Admin</strong> envía una orden de recogida.</td>
<td><ul><li>En la vista Orden de administración, el estado de Sincronización de pedidos se actualiza a <code>Sent</code>.</li><li>El registro de detalles del pedido incluye el mensaje <code>Order was sent to BOPIS solution for sync, it's not yet acknowledged yet.</code></li></ul></td>
</tr>
<tr>
<td><strong>Inserción de Nuevo Pedido, Cola de Excepciones<strong></td>
<td>Identifique varios productos virtuales y descargables del administrador de Adobe Commerce que se puedan cumplir a través de Adobe Commerce sin necesidad de interactuar con el servicio de cumplimiento (FaaS).</td>
<td>Estos productos se eliminan o se marcan adecuadamente en la exportación para evitar un conflicto descendente con las FaaS.</td>
</tr>
</tbody>
</table>

### Flujos de trabajo Cancelación de pedidos

Esta sección del plan de prueba incluye escenarios para probar el flujo de trabajo de extremo a extremo para pedidos cancelados a través de Adobe Commerce.

**Área funcional:** Administrador de Adobe Commerce</br>
**Rol:** de extremo a extremo (administrador, asociado de tienda, cliente)</br>
**Tipo de resultado de prueba:** Positivo para todos los escenarios

<table style="table-layout:fixed">
<tr>
<th>Función</th>
<th>Escenario</th>
<th>Resultados esperados</th>
</tr>
<tr>
<td><strong>Cancelación completa del pedido</strong></td>
<td><ol>
<li>Realice el pedido.</li>
<li>Espere hasta que se sincronice el pedido.</li>
<li>Verificar la creación de facturas (si está autorizado y captura) y la recepción del correo electrónico de factura.</li>
<li>Crear nota de abono con todos los productos pedidos desde la vista Factura.</li>
</ol>
</td>
<td>
<ul>
<li>Historial de pedidos actualizado con <code>We refunded $X online. Transaction ID: transactionID</code> y <code>Received Cancel acknowledgment from the BOPIS solution.</code></li>
<li>El estado del pedido es <code>Closed</code>. (Hemos establecido REVISIÓN DE PAGO ahora.)</li>
<li>Nota de crédito creada en Adobe Commerce. (Espere hasta que el cron funcione).</li>
<li>Si se seleccionan todos los elementos, listo para recibir el correo electrónico <code>DISPLAY COMMENT HISTORY</code> muestra <code>Order is ready for pickup</code> (<code>CUSTOMER NOTIFIED</code> marca es <code>true</code>).</li>
<li>Si no se seleccionan todos los artículos, se muestran el correo electrónico de cancelación y el HISTORIAL DE COMENTARIOS DE VISUALIZACIÓN <code>Order has been canceled - all items were not available</code></li>
<li><code>CUSTOMER NOTIFIED</code> el marcador es <code>true</code>.)</li>
</ul>
</td>
</tr>
<tr><td><strong>Cancelación parcial del pedido<strong></td>
<td>
<ol>
<li>Realice un pedido con al menos dos productos.</li>
<li>Espere hasta que se sincronice el pedido.</li>
<li>Compruebe que la factura se haya creado (si es autorizada y capturada) y que el correo electrónico de la factura se haya recibido.</li>
<li>Espere dos horas para la liquidación de la transacción.</li>
<li>Crear nota de abono con solo parte de los productos pedidos desde la vista Factura.</li>
</td>
<td>
<ul>
<li>Actualización del historial de pedidos: <code>We refunded $X online. Transaction ID: transactionID</code></li>
<li>Actualización del historial de pedidos: <code>Order notified as partly canceled at: Date and Hour</code></li>
<li>Correo electrónico de recepción de reembolso del pedido: <code>$x amount was refunded</code></li>
<li>El estado del pedido es <code>Processing</code>.</li>
<li>Nota de crédito creada en Adobe Commerce (espere hasta que cron funcione).</li>
<li>Si algunos artículos no se seleccionaron, confirme que se muestra el correo electrónico [!UICONTROL Ready for Pickup] con la sección de selección o reembolso nulo. <code>DISPLAY COMMENT HISTORY</code> muestra <code>Order is ready for pickup, but some items not available.</code>.</li>
<li><code>CUSTOMER NOTIFIED</code> el marcador es <code>true</code>.</li>
</ul>
</td>
</tr>
<td><strong>Listo para la recogida</br></br>Cancelación completa</br>(todos los productos se establecen como recogidos con 0 cant.)</strong></td>
<td>
<ol>
<li>Realice el pedido.</li>
<li>Espere hasta que se sincronice el pedido.</li>
<li>Compruebe que la factura se haya creado (si es autorizada y capturada) y que el correo electrónico de la factura se haya recibido.</li>
<li>Vaya a Postman y ejecute la solicitud Listo para la recogida con todos los productos establecidos como <code>picked</code> con <code>0 qty</code>.</li>
</ol>
</td>
<td>
<ul>
<li>Historial de pedidos actualizado: <code>We refunded $X offline</code></li>
<li>El estado del pedido es <code>CLOSED</code>.
<li>Se crea la nota de abono. (Espere hasta que el cron funcione).</li>
<li>Correo electrónico de reembolso recibido: <code>$x amount was refunded</code></li>
<li>Correo electrónico de cancelación de pedido enviado.</li>
</ul>
</td>
</tr>
<tr>
<td><strong>Listo para la recogida - Cancelación parcial</strong></br></br><strong>(Algunos productos se recogen y otros se recogen con <code>0 qty</code>)</strong>
</td>
<td>
<ol>
<li>Realice el pedido.</li>
<li>Espere hasta que se sincronice el pedido.</li>
<li>Compruebe que la factura se haya creado (si es autorizada y capturada) y que el correo electrónico de la factura se haya recibido.</li>
<li>Vaya a Postman y ejecute la solicitud Listo para la recogida con parte del conjunto de productos según la cantidad de 0 y el resto de ellos recogidos.</li>
</ol>
</td>
<td>
<ul>
<li><code>Your order is ready for pickup</code> con [!UICONTROL Ready for Pickup Items] y [!UICONTROL Canceled Items] tablas. </li>
<li>El estado del pedido es LISTO PARA RECOGER. </li>
<li>Historial de pedidos actualizado: <code>We refunded $X offline.</code>
<li>Historial de pedidos actualizado: <code>Order notified as partly canceled at: Date and hour</code>
<li>Correo electrónico de reembolso recibido: <code>$x amount was refunded</code>
<li>Se crea la nota de abono. (Espere hasta que el cron funcione).</li>
</ul>
</td>
</tr>
<tr>
<td><strong>Listo para la recogida - Cancelación parcial</br></br>Algunos productos se recogen y otros se recogen con <code>0 qty</code>)</strong>
</td>
<td><ol>
<li>Realice el pedido.</li>
<li>Espere hasta que se sincronice el pedido.</li>
<li>Compruebe que la factura se haya creado (si es autorizada y capturada) y que el correo electrónico de la factura se haya recibido.</li>
<li>Vaya a Postman y ejecute la solicitud Listo para la recogida con parte del conjunto de productos según la cantidad de 0 y el resto de ellos recogidos.</li>
</ol>
</td>
<td><ul>
<li><code>Your order is ready for pickup</code> con [!UICONTROL Ready for Pickup Items] y [!UICONTROL Canceled Items] tablas. </li>
<li>El estado del pedido es LISTO PARA RECOGER. </li>
<li>Historial de pedidos actualizado: <code>We refunded $X offline.</code>
<li>Historial de pedidos actualizado: <code>Order notified as partly canceled at: Date and hour</code>
<li>Correo electrónico de reembolso recibido: <code>$x amount was refunded</code>
<li>Se crea la nota de abono. (Espere hasta que el cron funcione).</li>
</ul>
</td>
</tr>
<tr>
<td><strong>Dispensados (durante la dispensa) </br></br>Cancelación completa (todos los productos se establecen como rechazados)</strong>
</td>
<td>
<ol>
<li>Realice el pedido.</li>
<li>Espere hasta que se sincronice el pedido.</li>
<li>Compruebe que la factura se haya creado (si es autorizada y capturada) y que el correo electrónico de la factura se haya recibido.</li>
<li>Vaya a Postman y ejecute la solicitud Listo para la recogida con todos los productos configurados como seleccionados.</li>
<li>Abra su buzón y busque el correo electrónico Listo para recoger. A continuación, haga clic en **[!UICONTROL Confirm Arrival]**.</li>
<li>Marque en.</li>
<li>Vaya a Postman y ejecute la solicitud dispensada con todos los productos configurados como rechazados.</li>
</ol>
<td><ul>
<li>Historial de pedidos actualizado: <code>We refunded $X offline.</code></li>
<li>Correo electrónico de reembolso recibido: <code>$x amount was refunded</code></li>
<li>Estado establecido en <code>CLOSED</code>.</li>
<li>Abono creado. (Espere hasta que el cron funcione).</li>
</ul>
</td>
</tr>
<tr>
<td><strong>Dispensados (durante la dispensación)</br></br>Cancelación parcial</br>(Algunos productos se dispensan; algunos se rechazan.)</strong>
</td>
<td>
<ol>
<li>Realice el pedido.</li>
<li>Espere hasta que se sincronice el pedido.</li>
<li>Compruebe que la factura se haya creado (si es autorizada y capturada) y que el correo electrónico de la factura se haya recibido.</li>
<li>Vaya a Postman y ejecute la solicitud Listo para la recogida con todos los productos configurados como seleccionados.</li>
<li>Abra el buzón. Busque el correo electrónico Listo para la recogida y seleccione <code>Confirm Arrival</code>.</li>
<li>Marque en.</li>
<li>Vaya a Postman y ejecute la solicitud dispensada con algunos productos configurados en dispensados y otros configurados en rechazados</li>
</ol>
</td>
<td>
<li>Historial de pedidos actualizado: <code>We refunded $X offline</code></li>
<li><code>Order notified as partly canceled at: Date and Hour</code>
<li>Correo electrónico de reembolso recibido: <code>$x amount was refunded</code>
<li>Estado de pedido establecido en <code>Ready for pickup Dispensed</code>
<li>Abono creado. (Espere hasta que el cron funcione).</li>
</td>
</tr>
<tr>
<td> <strong>Nuevo RMA después del retorno (completo)</strong>
</td>
<td>
<ol>
<li>Realice el pedido.</li>
<li>Espere hasta que se sincronice el pedido.</li>
<li>Si la opción de autorización y captura está configurada, compruebe que la factura se haya creado y que el cliente haya recibido el correo electrónico de factura.</li>
<li>Elija todos los productos con Postman.</li>
<li>Marque en.</li>
<li>Haz un dispendio.</li>
<li>Vaya al pedido y seleccione<strong>[!UICONTROL Create returns]=
<li>Crear la RMA.</li>
</ol>
</td>
<td>
<ul>
<li>La autorización de devolución de material se creó y se muestra debajo de la ficha <strong>[!UICONTROL Returns]</b> en la vista Pedido.</li>
<li>El cliente recibió el correo electrónico de confirmación de RMA.</li>
</ul>
</td>
</tr>
<tr>
<td><strong>Nuevo RMA después del retorno — Parcial</strong>
</td>
<td>
<ol>
<li>Realice el pedido.</li>
<li>Espere hasta que se sincronice el pedido.</li>
<li>Compruebe que la factura se haya creado (si es autorizada y capturada) y que el correo electrónico de la factura se haya recibido.</li>
<li>Elija todos los productos con Postman.</li>
<li>Marque en.</li>
<li>Haz un dispendio.</li>
<li>Vaya al pedido y seleccione  <strong>[!UICONTROL Create returns]</strong></li>
<li>Cree la autorización de devolución de material con parte de los productos solicitados.</li>
</ol>
<td>
<ul>
<li>RMA creada y mostrada debajo de la ficha <strong>[!UICONTROL Returns]</strong> en la vista de pedidos.</li>
<li>El cliente recibió el correo electrónico de confirmación de RMA.</li>
<li>Después de crear la RMA, obtenga la autorización de la RMA: Desde el administrador, vaya a <strong>[!UICONTROL Sales > Returns]</strong>. Seleccione la RMA que ha creado y autorícela.</li>
<li>Compruebe que el cliente ha recibido el correo electrónico de confirmación de autorización de RMA.</li>
<li>Compruebe que el reembolso se haya añadido al historial de transacciones y pedidos.</li>
</ul>
</td>
</tr>
</table>


### Permisos de aplicación de Store Fulfillment

Esta sección del plan de prueba cubre la administración de cuentas para los usuarios de aplicaciones de Store Fulfillment.

- Confirme que un asociado de tienda puede autenticarse con una nueva cuenta de usuario creada desde el administrador de Adobe Commerce.
- Confirme que las actualizaciones de las cuentas existentes se aplican correctamente.

**Área funcional:** Administrador de Adobe Commerce</br>
**Rol:** administrador, asociado de tienda</br>
**Tipo de prueba:** Todas positivas

<table style="table-layout:auto">
<tr>
<th>Función</th>
<th>Escenario</th>
<th>Resultados esperados</th>
</tr>
<tr>
<td><strong>Administración de cuentas de usuario - Crear cuenta</strong></br></br>
</td>
<td>
<ol>
<li><strong>Administrador</strong> — Inicie sesión en el administrador de Adobe Commerce</li>
<li>Vaya a <strong>[!UICONTROL System] &gt; Permisos de aplicación de Store Fulfillment &gt; Todos los usuarios de aplicación Store Fulfillment</strong></li>
<li><strong>Agregar nuevo usuario.</strong></li>
</ol>
<td>
<ul>
<li>Cuenta creada correctamente.</li>
<li>La nueva cuenta de usuario se muestra en el panel [!UICONTROL Store Fulfillment Users].</li>
<li><strong>Asociado de tienda</strong> inicia sesión en la aplicación de asistencia de tienda con la nueva cuenta de usuario.</li>
</ul>
</td>
</tr>
<tr>
<td><strong>Administración de cuentas de usuario - Actualizar cuenta de usuario existente</strong>
</td>
<td>
<ol>
<li>Inicie sesión en Adobe Commerce Admin con una cuenta de usuario de administrador.</li>
<li>Vaya a <strong>[!UICONTROL System] &gt; Permisos de aplicación de Store Fulfillment &gt; Todos los usuarios de aplicación Store Fulfillment</strong>.</li>
<li>En la lista Cuenta de usuario, abra una cuenta de usuario activa existente seleccionando <strong>[!UICONTROL Edit]</strong>.
<li>Deshabilite la cuenta cambiando <strong>[!UICONTROL Is Active]</strong> a <strong>No</strong>.</li>
</ol>
</td>
<td>
<ul>
<li>En el panel <strong>[!UICONTROL Store Fulfillment App Users]</strong>, el estado de la cuenta actualizada cambió a <strong>[!UICONTROL Inactive]</strong>.</li>
<li>El asociado de tienda no puede iniciar sesión en la aplicación de asistencia de tienda con las credenciales de cuenta inactivas.</li>
</ul>
</td>
</tr>
</table>

## Tipos de productos de Adobe Commerce

Los escenarios de prueba para tipos de producto de Adobe Commerce verifican que los clientes ven la información correcta del producto, stock y método de entrega para diferentes tipos de productos:

- [!UICONTROL Configurable]
- [!UICONTROL Grouped]
- [!UICONTROL Virtual]
- [!UICONTROL Bundle products] en la tienda de Adobe Commerce.

**Área funcional:** Adobe Commerce Frontend</br>
**Rol:** Usuario De Aplicación De Asistencia De Tienda (Asociado De Tienda)</br>
**Tipo de prueba:** Todas positivas

<table style="table-layout:auto">
<tr>
<th>Función</th>
<th>Escenario</th>
<th>Comentarios</th>
</tr>
<tr>
<td><strong>Productos configurables</strong>
</td>
<td>
<ul>
<li>Compruebe que el usuario solo puede ver las opciones configurables, qué origen está habilitado, se asignan las existencias y que hay algunos artículos en stock: compruebe los productos secundarios.</li>
<li>Compruebe que, al seleccionar una tienda diferente, las opciones que no están disponibles se muestren tachadas.</li>
<li>Compruebe que si el usuario selecciona un almacén diferente, las opciones configurables no se seleccionan.</li>
<li>Compruebe que si un producto configurable ya está en el carro de compras y un usuario selecciona otra tienda, el producto se muestra sin existencias.</li>
</ul>
</td>
<td></td>
</td>
</tr>
<tr>
<td><strong>Productos agrupados</strong>
</td>
<td>
<ul>
<li>Compruebe que los métodos de envío y el botón [!UICONTROL Add to cart] estén deshabilitados para el cliente cuando todos los productos secundarios tengan
<code>qty</code> se estableció en <code>0</code>.</li>
<li>Compruebe que los métodos de envío estén habilitados para el cliente cuando al menos uno de los productos secundarios tenga <code>qty</code> establecido en <code>0.</code></li>
<li>Compruebe que el método [!UICONTROL Store Pickup Delivery] solo esté visible y activo para los productos que tienen [!UICONTROL Available for Store Pickup] habilitado. (Compruebe el producto secundario).</li>
</ul>
</td>
<td></td>
</tr>
<tr>
<td><strong>Productos virtuales</strong>
</td>
<td>
Compruebe que los productos virtuales no ofrecen el método de entrega [!UICONTROL In-store Pickup].
<td></td>
</td>
</tr>
<tr>
<td><strong>Productos en paquete</strong>
</td>
<td>
<ul>
<li>Compruebe que si al menos un producto secundario tiene [!UICONTROL Available for Store Pickup] deshabilitado, la opción de entrega Recogida en tienda no esté disponible para el cliente.</li>
<li>Compruebe que si al menos un producto secundario tiene [!UICONTROL Available for Home Delivery] deshabilitado, la opción Entrega a domicilio no esté disponible para el cliente.</li>
<li>Compruebe si al menos uno de los productos secundarios de un paquete está agotado, también se muestra el paquete (producto principal)
como [!UICONTROL Out of stock].</li>
</ul>
</td>
<td></td>
</tr>
<tbody>
</table>

## Experiencia de llegada

Esta sección del plan de prueba cubre la experiencia de registro para pedidos de recogida en tienda para las siguientes funciones:

- Contacto de recogida alternativo: compruebe el flujo de trabajo para agregar un(a) [!UICONTROL Alternate Pickup Contact] y seleccionar un(a) [!UICONTROL Preferred Contact] en los pedidos de recogida en tienda.

- Formulario de registro: compruebe el flujo de trabajo para enviar una solicitud de registro para los pedidos de recogida de la tienda.

**Áreas funcionales:** Cierre de carro de compras, Formulario de registro para pedidos de recogida en tienda</br>
**Rol:** Administrador, Cliente, Asociado De Tienda</br>
**Tipo de prueba:** Todas positivas

### Contacto alternativo de recogida


**Área funcional:** Cierre de carro</br>
**Rol:** Cliente</br>
**Tipo de prueba:** Todas positivas

<table style="table-layout:auto">
<tr>
<th>Función</th>
<th>Escenario</th>
<th>Resultados esperados</th>
</tr>
<tr>
<td><strong>Contacto de recogida alternativo </br>
Check-In<strong>
</td>
<td>
Un cliente envía un pedido con la opción de recogida en tienda.</td>
<td>Durante el proceso de cierre de compra, el cliente ve la opción [!UICONTROL Alternate Pickup Contact] en el paso Envío.
</td>
</tr>
<tr>
<td><strong>Contacto preferido de recogida alternativo, registrar</strong>
<td>
Un cliente envía un pedido con la opción de recogida en tienda. Durante el cierre de compra, el cliente agrega un [!UICONTROL Alternate Pickup Contact].</td>
<td>Durante el proceso de cierre de compra, el cliente ve la opción [!UICONTROL Preferred Contact] en el paso de envío.</td>
</td>
</tr>
<tr>
<td><strong>Detalles de contacto de recogida alternativa, proteger</strong>
</td>
<td>
Un cliente envía un pedido con la opción de recogida en tienda. Durante el cierre de compra, el cliente selecciona [!UICONTROL Alternate Pickup Contact] en el paso de envío.
</td>
<td>El cliente ve opciones de entrada para escribir los detalles de contacto: [!UICONTROL First name], [!UICONTROL Last name], [!UICONTROL Phone] y [!UICONTROL Email].</td>
</tr>
<tr>
<td><strong>Recogida alternativa, registrar correo electrónico</strong>
</td>
<td>Un cliente envía un pedido con la opción de recogida en tienda. Durante el cierre de compra, el cliente selecciona [!UICONTROL Alternate Pickup Contact] en el paso de envío, agrega los detalles de contacto y envía el pedido.</td>
<td>Tanto el cliente como el contacto alternativo reciben un mensaje de correo electrónico de registro para el pedido.</td>
</tr>
<td><strong>Recogida alternativa, detalles del pedido</strong></td>
<td>Un cliente envía un pedido con la opción de recogida en tienda. Durante el cierre de compra, el cliente selecciona [!UICONTROL Alternate Pickup Contact] en el paso de envío, agrega los detalles de contacto y envía el pedido.</td>
<td>El administrador ve la información de contacto adicional del pedido guardado.</td>
</tr>
<tr>
<td><strong>Contacto de recogida alternativo, vista de pedido asociado de tienda</strong>
</td>
<td>Un cliente envía un pedido con la opción de recogida en tienda. Durante el cierre de compra, el cliente selecciona [!UICONTROL Alternate Pickup Contact] en el paso de envío, agrega los detalles de contacto y envía el pedido.</td>
<td>El asociado de tienda puede ver la información de contacto adicional en el pedido en FaaS/ChaaS.</td>
</td>
</tr>
</tbody>
</table>

### Formulario de registro de entrada


**Área funcional:** Formulario de registro</br>
**Rol:** Cliente</br>
**Tipo de prueba:** Todas positivas

<table style="table-layout:auto">
<tr>
<th>Función</th>
<th>Escenario</th>
<th>Resultados esperados</th>
</tr>
<tr>
<td><strong>Acción de registro—Enviar solicitud</strong>
</td>
<td>En el formulario de registro, un cliente rellena todos los campos obligatorios y envía la solicitud.</td>
<td>El cliente recibe una respuesta de éxito.</td>
</tr>
<tr>
<td><strong>Acción de registro: ver detalles de la solicitud</strong></td>
<td>Un cliente envía correctamente una solicitud de protección.</td>
<td>El estado del pedido se actualiza en el sistema FaaS y el asociado de tienda puede ver los detalles de la solicitud de registro en FaaS.
</td>
</tr>
<tr>
<td><strong>Acción de registro: enviar la solicitud solo una vez</strong></td>
<td>Después de enviar una solicitud de registro para un pedido, un cliente selecciona el vínculo para registrar por segunda vez.</td>
<td>En el formulario de registro, el cliente no ve una opción para editar o volver a enviar el formulario.</td>
</tr>
<tr>
<td><strong>Acción de registro: confirmar llegada</strong></td>
<td>Una orden de recogida en la tienda se marca como lista para su recogida en la FaaS. El cliente recibe un correo electrónico de Listo para la recogida y selecciona [!UICONTROL Confirm Arrival].</td>
<td>El cliente ve el formulario de registro del pedido.</td>
</tr>
</tbody>
</table>

## Aplicación Store Assist

Esta sección del plan de prueba cubre los escenarios para probar los flujos de trabajo de pedido, picking y entrega en la aplicación Store Assist.

**Área funcional:** Aplicación de asistencia de tienda</br>
**Rol:** asociado de tienda</br>
**Tipo de prueba:** Todas positivas

<table style="table-layout:auto">
<tr>
<th>Función</th>
<th>Escenario</th>
<th>Resultados esperados</th>
</tr>
<tr>
<td>
<strong>Selección de pedido único: ruta feliz, recogida en la acera</strong></td>
<td>Seleccione artículos de una o varias cantidades. Sin recolecciones nulas y recolección en la acera (con ensayo).
</td>
<td>
</td>
</tr>
<tr>
<td><strong>Selección de varios pedidos: ruta feliz, recogida en la acera</strong></td>
<td>Artículos de una o varias cantidades. Sin recolecciones nulas y recolección en la acera (con ensayo)</td>
<td></td>
</tr>
<tr>
<td><strong>Recogida de pedido único: ruta feliz recogida en tienda</strong></td>
<td>Artículos de una o varias cantidades. Sin recogida nula y recogida en tienda (con ensayo)</td>
<td>
</td>
</tr>
<tr>
<td><strong>Selección de pedidos múltiples: ruta feliz, recogida en la tienda</strong></td>
<td>Seleccione artículos de una o varias cantidades. Sin recolecciones nulas y recolección en la acera (con ensayo).</td>
<td></td>
</tr>
<tr>
<td><strong>Selección de pedido único: ruta no feliz, recogida en la tienda</strong></td>
<td>Recoger artículos de una o varias cantidades con recogida parcial y sin recogida y recogida en tienda (con ensayo)</td>
</td>
<td></td>
</tr>
<td><strong>Selección de varios pedidos: no es una recolección feliz en la acera</strong></td>
<td>Recoger artículos de una o varias cantidades con recogida parcial y sin recogida y recogida en tienda (con ensayo)</td>
<td></td>
</tr>
<td><strong>Selección de pedido único: ruta no feliz, recogida en la acera</strong></td>
<td>Escoger artículos de una o varias cantidades con recogida parcial y sin recogida y en la acera (con ensayo)</strong></td>
</td>
<td></td>
</tr>
<tr><td><strong>Pedido realizado - cancelado antes de la selección</strong></td>
<td></td>
<td></td>
</tr>
<tr>
<td><strong>Pedido realizado - cancelado antes del envío</strong></td>
<td></td>
<td></td>
</tr>
<tr>
<td><strong>Pedido realizado: buscar en el módulo de pedido</strong></td>
<td></td>
<td></td>
</tr>
<tr><td><strong>Pedido realizado: búsqueda y registro manual para entrega</strong></td>
<td></td>
<td></td>
</tr>
<tr><td><strong>Pedido realizado: todos los artículos no seleccionados o no disponibles marcados por el selector</strong></td>
<td></td>
<td></td></tr>
<tr><td><strong>Pedido realizado con artículos agrupados - picking y entrega</strong></td>
<td></td>
<td></td></tr>
<tr><td><strong>Pedido realizado - Entregar con rechazo</strong></td>
<td></td>
<td></td></tr>
<tr><td><strong>Pedido realizado: entrega con rechazo de todos los artículos</strong></td>
<td></td>
<td></td></tr>
</tbody>
</table>

## Implementar

Después de comprobar que la solución se ha configurado y probado según sus especificaciones, está listo para implementarla desde el ensayo hasta la producción.

La implementación y las pruebas varían en función de la infraestructura y las capacidades.

>[!TIP]
>
>Para obtener instrucciones de implementación, listas de comprobación y prácticas recomendadas para Adobe Commerce en proyectos de infraestructura en la nube, consulte [Implementar su tienda](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/deploy/staging-production) en la documentación para desarrolladores de Adobe Commerce.
