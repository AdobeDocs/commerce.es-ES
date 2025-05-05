---
title: Configuración general
description: Configura la configuración general para habilitar [!DNL Store Fulfillment] para tu tienda. Configure las opciones globales de extensión, la configuración del sistema para el registro, la sincronización de datos y la seguridad. Proporcione datos clave para permitir la integración entre Adobe Commerce y los servicios Store Fulfillment.
role: Admin
level: Intermediate
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '2405'
ht-degree: 0%

---

# Configuración de ventas y servicio de tienda

Habilite la extensión [!DNL Store Fulfillment] desde el administrador de [!DNL Commerce] configurando la configuración de la extensión, la configuración de seguridad para los usuarios de la aplicación Store Assist y las opciones del método de envío.

>[!IMPORTANT]
>
>La configuración del servicio Store Fulfillment solo se aplica después de conectar la instancia de Adobe Commerce y la aplicación [!DNL Store Fulfillment]. Ver [Cumplimiento de tienda Connect](connect-set-up-service.md).

## Administrar configuración de servicios de Store Fulfillment

Administrar la configuración de los servicios de Satisfacción de pedidos de tienda desde el menú [!DNL Commerce Admin Store Configuration].

- Habilite la extensión, configure las opciones globales y especifique las opciones de seguridad de las cuentas y conexiones de los usuarios de la aplicación Store Assist seleccionando **[!UICONTROL Stores > Configuration > Services > Store Fulfillment by Walmart Commerce Technologies]**.

  ![Configuración de servicios de Admin Store para cumplimiento de tienda](assets/store-services-admin-sf-config.png)

- Configure los métodos de entrega seleccionando **[!UICONTROL Store > Configuration > Sales > Delivery Methods > In-Store Pickup]**.

  ![Configuración de ventas de la Tienda de administración para el cumplimiento de tiendas](assets/store-sales-admin-sf-deliver-config.png)

## Configuración básica

<table>
<thead>
<tr>
<td><strong>Campo</strong></td>
<td><strong>Descripción</strong></td>
<td><strong>Ámbito</strong></td>
<td><strong>Requerido</strong></td>
</tr>
</thead>
<tbody>
<tr>
<td><strong>[!UICONTROL Price]</strong></td>
<td>El precio que cobra al cliente por la recogida en la tienda. El valor predeterminado es cero.</td>
<td>Sitio web</td>
<td>No</td>
</tr>
<tr>
<td><strong>[!UICONTROL Search Radius]</strong></td>
<td>El radio, en kilómetros, que se utiliza cuando un comprador busca una ubicación de recogida en la tienda durante el cierre de compra. Los resultados de la búsqueda solo devuelven almacenes ubicados dentro del radio de búsqueda especificado.</td>
<td>Sitio web</td>
<td>No</td>
</tr>
<tr>
<td><strong>[!UICONTROL Displayed error message]</strong></td>
<td>Mensaje que se muestra cuando un cliente selecciona la recogida en tienda de un artículo que no está disponible para la recogida en tienda. Puede personalizar el texto predeterminado si es necesario.
</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
</tbody>
</table>

>[!NOTE]
>
>La configuración [!UICONTROL Search Radius] solo se usa si ha configurado la [ubicación de almacenamiento y la configuración de asignación](store-location-map-provider-setup.md) para Adobe Commerce.

## Activación de la solución Store Fulfillment

Habilite la solución [!DNL Store Fulfillment] para agregar las capacidades de recogida en tienda y en la zona de la acera a las experiencias de compra y cierre de compra en su tienda de Adobe Commerce.

<table>
<thead>
<tr>
<td><strong>Campo</strong></td>
<td><strong>Descripción</strong></td>
<td><strong>Ámbito</strong></td>
<td><strong>Requerido</strong></td>
</tr>
 </thead>
 <tbody>
<tr>
<td><strong>[!UICONTROL Enabled]</strong></td>
<td>Habilite o deshabilite la solución. Cuando esté habilitada, configure y use las capacidades de Satisfacción de pedidos de la tienda y establezca la conexión entre su tienda Adobe Commerce y los servicios de [!DNL Store Fulfillment]. Cuando está desactivada, todas las funciones de Store Fulfillment están desactivadas y no hay comunicación entre los servicios de Adobe Commerce y Store Fulfillment. La información del pedido no se puede procesar ni recibir.</td>
<td>Sitio web</td>
<td>Sí</td>
</tr>
</tbody>
</table>

## Agregar credenciales de cuenta

<table>
<tr>
<td><strong>Campo</strong></td>
<td><strong>Descripción</strong></td>
<td><strong>Ámbito</strong></td>
<td><strong>Requerido</strong></td>
</tr>
<tr>
<td><strong>[!UICONTROL Environment]</strong></td>
<td>Seleccione <i>[!UICONTROL Sandbox]</i> o <i>[!UICONTROL Production]</i><br></br>Al seleccionar [!UICONTROL Sandbox], se habilita la comunicación con los servicios de cumplimiento en un entorno de prueba.<br></br>Al seleccionar [!UICONTROL Production], se habilita la comunicación con los servicios de cumplimiento en un entorno en vivo.<br></br>Se le proporciona un conjunto de credenciales para cada entorno y puede administrar ambos conjuntos en la misma instalación. <br></br>Guarde las credenciales antes de validar la conexión.</td>
<td>Global</td>
<td>Sí</td>
</tr>
<tr>
<td><strong>[!UICONTROL API Server URL]</strong></td>
<td>Dirección URL del punto final de la API de cumplimiento de Walmart Store. El valor debe ser la dirección URL completa que se proporciona durante el proceso de incorporación. Los clientes de Store Fulfillment reciben una zona protegida y una URL de producción. Al añadir los valores, asegúrese de copiar y pegar la dirección URL completa, incluida la barra diagonal "/".</td>
<td>Global</td>
<td>Sí</td>
</tr>
<tr>
<td><strong>[!UICONTROL Token Auth Server URL]</strong></td>
<td>Dirección URL del extremo de autenticación de cumplimiento de Walmart Store. El valor debe ser la dirección URL completa que se proporciona durante el proceso de incorporación. Recibirá una zona protegida y una URL de producción. Al añadir los valores, asegúrese de copiar y pegar la dirección URL completa, incluida la barra diagonal "/".</td>
<td>Global</td>
<td>Sí</td>
</tr>
<tr>
<td><strong>[!UICONTROL Merchant Id]</strong></td>
<td>Su ID único de comerciante (inquilino) proporcionado durante el proceso de incorporación. Este ID se utiliza para enviar pedidos y garantizar que sus tiendas de comercios los reciban.</td>
<td>Global</td>
<td>Sí</td>
</tr>
<tr>
<td><strong>[!UICONTROL Consumer Id]</strong></td>
<td>El ID de integración único proporcionado durante el proceso de incorporación. Este ID se utiliza para autenticar todas las comunicaciones entre Adobe Commerce y los servicios de cumplimiento de la tienda</td>
<td>Global</td>
<td>Sí</td>
</tr>
<tr>
<td><strong>[!UICONTROL Consumer Secret]</strong></td>
<td>La clave de integración única proporcionada durante el proceso de incorporación. Esta clave se utiliza para autenticar todas las comunicaciones entre Adobe Commerce y el servicio de cumplimiento de la tienda.</td>
<td>Global</td>
<td>Sí</td>
</tr>
</table>

Después de configurar [!UICONTROL Account Credentials], seleccione <strong>[!UICONTROL Validate Credentials]</strong> para comprobar y establecer una conexión con el servicio de cumplimiento de almacenamiento por primera vez.

## Configurar el registro

Los registros de los servicios de cumplimiento de almacenamiento están disponibles en el archivo de registro `var/log/walmart-bopis.log`.

Pida al administrador del sistema que configure los entornos para permitir el control de excepciones, de modo que las excepciones relacionadas con la API puedan capturarse a través del cortafuegos o de la caché.

Dado que el archivo de registro de la aplicación puede crecer rápidamente, habilite el registro para la aplicación sólo durante un breve período de tiempo cuando sea necesario, por ejemplo, al solucionar problemas de cumplimiento de almacén para un pedido de [!DNL Commerce]. Esta configuración evita los problemas de tiempo de respuesta en entornos de producción causados por archivos de registro grandes.

>[!TIP]
>
>Para las instalaciones locales de Adobe Commerce, pídale al administrador del sistema que configure la rotación del registro para el archivo `var/log/walmart-bopis.log` a fin de minimizar el tamaño. Para las instalaciones locales de Adobe Commerce, consulte [Rotación del registro](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/next-steps/configuration.html?lang=es#server-settings) en la _Guía de instalación de Adobe Commerce_. Para Adobe Commerce sobre proyectos de infraestructura en la nube, consulte [Ver y administrar registros](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/develop/test/log-locations.html?lang=es).

<table>
<thead>
<tr>
<td><strong>Campo</strong></td>
<td><strong>Descripción</strong></td>
<td><strong>Ámbito</strong></td>
<td><strong>Requerido</strong></td>
</tr>
</thead>
<tbody>
<tr>
<td><strong>[!UICONTROL Debug Mode]</strong></td>
<td>El modo de depuración se utiliza para aumentar la actividad registrada dentro de la integración. Cuando está desactivada, no se registra ninguna información de depuración. Cuando está habilitada, toda la información de depuración se registra <br></br>Todos los datos registrados se pueden encontrar en el archivo: <pre>var/log/walmart-bopis.log</pre>
<td>Global</td>
<td>No</td>
</tr>
</tbody>
</table>

## Administrar sincronización de pedidos

Configure las opciones para administrar la gestión de errores para la sincronización de pedidos, los atributos de catálogo que se utilizarán para el análisis de códigos de barras durante la selección de pedidos y configure los tamaños de lote de pedidos para la cola de satisfacción de pedidos.

Puede ver los detalles sobre las operaciones de sincronización de pedidos desde el panel de control Gestión de colas de satisfacción de pedidos en Admin (
<strong>[!UICONTROL System > Tools > Store Fulfillment Queue]</strong>).

### Administración de errores de sincronización

<table>
<tr>
<td><strong>Campo</strong></td>
<td><strong>Descripción</strong></td>
<td><strong>Ámbito</strong></td>
<td><strong>Requerido</strong></td>
</tr>
<tr>
<td><strong>[!UICONTROL Retry Critical Error]</strong></td>
<td>Especifica los intentos de reintento de una operación de sincronización de registros después de que se produzca un error crítico.<br></br>Se producen errores críticos cada vez que la integración no obtiene una respuesta positiva del servicio de cumplimiento. Estos problemas se producen cuando el servicio está inactivo o cuando hay un error en los datos del pedido que se envían.<br></br>Cuando se alcanza el umbral de reintentos, el elemento permanece en cola pero no se vuelve a procesar. Vea todos los elementos con errores de la administración de <strong>[!UICONTROL System > Tools > Store Fulfillment Queue]</strong> en el administrador. Para solucionar problemas de elementos con errores continuos, póngase en contacto con su administrador de cuentas.</td>
<td>Global</td>
<td>No</td>
</tr>
<tr>
<td><strong>[!UICONTROL Enable Error Notification Email]</strong></td>
<td>Habilitar notificaciones de error para recibir un correo electrónico cuando se llegue a [!UICONTROL Retry Critical Error Threshold] para un pedido. La notificación incluye todos los detalles disponibles sobre el error.</td>
<td>Global</td>
<td>No</td>
</tr>
<tr>
<td><strong>[!UICONTROL Send Error Notification Email To]</strong></td>
<td>Una lista delimitada por comas de direcciones de correo electrónico de los destinatarios para las notificaciones de error.</td>
<td>Global</td>
<td>No</td>
</tr>
<tr>
<td><strong>[!UICONTROL Order Sync Exception Email Template]</strong></td>
<td>Especifica la plantilla de correo electrónico utilizada para notificar a los destinatarios los errores de sincronización de pedidos. Se proporciona una plantilla predeterminada. No admite la personalización.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
</table>

### Sincronización de pedidos

<table>
<thead>
<tr>
<td><strong>Campo</strong></td>
<td><strong>Descripción</strong></td>
<td><strong>Ámbito</strong></td>
<td><strong>Requerido</strong></td>
</tr>
</thead>
<tbody>
<tr>
<td><strong>[!UICONTROL Barcode Source]</strong></td>
<td>Atributo de catálogo que almacena el código que se puede escanear para los artículos correspondientes en las ubicaciones de los comerciantes.<br></br>Si solo tiene una ubicación de comerciante, es probable que use códigos UPC, mientras que su canal de comercio electrónico identifica los productos por SKU. En esta situación, seleccione el atributo de catálogo que contiene el código UPC.<br></br>Esta configuración garantiza que los pedidos enviados a su lista de artículos de tiendas con el identificador correcto para que los asociados de tiendas puedan analizar los artículos con precisión durante el proceso de selección.<br></br>Si no está seguro, consulte con sus asociados de cumplimiento en el departamento de envío y picking para determinar qué atributo se debe enviar. Si el atributo no está incluido actualmente en la base de datos, puede agregarlo al conjunto de atributos del producto Adobe Commerce.</td>
<td>Sitio web</td>
<td>Sí</td>
</tr>
<tr>
<td><strong>[!UICONTROL Barcode Type]</strong></td>
<td>Atributo de catálogo que almacena el origen del código de barras de los artículos correspondientes en las ubicaciones de los comerciantes.<br></br>Esta configuración garantiza que los pedidos enviados a la lista de artículos de las tiendas tengan el identificador correcto para que los asociados de la tienda puedan analizar los artículos con precisión durante el proceso de selección. Las opciones incluyen: SKU, UPC, GTIN, UPCA, EAN13, UPCE0, DISA, UAB, CODABAR, Precio incrustado UPC.<br></br>Si no está seguro, seleccione la opción que se parezca más a los valores contenidos en su atributo [!UICONTROL Barcode Source]. Los socios de la tienda aún pueden hacer coincidir artículos manualmente desde su lista de selección.</td>
<td>Sitio web</td>
<td>Sí</td>
</tr>
<tr>
<td><strong>[!UICONTROL Max Number of Items]</strong></td>
<td>Número máximo de elementos que se van a enviar de la cola de satisfacción de pedidos de tienda al mismo tiempo.<br></br>Los pedidos BOPIS se envían al servicio de cumplimiento por lotes a intervalos regulares. Esta configuración le permite controlar el tamaño del lote.<br></br>El valor predeterminado es 100 elementos. Según el volumen y la capacidad del pedido, puede ajustar el valor máximo hacia arriba o hacia abajo.</td>
<td>Global</td>
<td>No</td>
</tr>
</tbody>
</table>

## Activar opciones de envío de Store Fulfillment

Configure las opciones de envío de Satisfacción de Pedidos que determinan la disponibilidad de las opciones de recogida en tienda y envío a domicilio para sus tiendas Adobe Commerce.

### Enviar a tienda

<table>
<thead>
<tr>
<td><strong>Campo</strong></td>
<td><strong>Descripción</strong></td>
<td><strong>Ámbito</strong></td>
<td><strong>Requerido</strong></td>
</tr>
</thead>
<tbody>
<tr>
<td><strong>[!UICONTROL Enable Ship To Store]</strong></td>
<td>La configuración de envío a tienda se basa en las capacidades de envío a tienda existentes. Si utiliza Inventory management o si puede aceptar y satisfacer pedidos en ubicaciones de comerciantes sin inventario mediante transferencias de inventario de tienda a tienda, establezca esta opción en "Sí".<br></br>Si no admite la opción de envío a tienda o no desea ofrecerla, establézcala en `No`. Cuando está deshabilitado, los artículos del catálogo con inventario cero para una tienda comercial o los artículos que están por debajo de [!DNL Out of Stock Threshold] para esa ubicación no se ofrecen con las opciones de recogida en la tienda.<br></br>Puede ajustar el valor de esta configuración por ubicación de comerciante.</td>
<td>Global</td>
<td>No</td>
</tr>
</tbody>
</table>

### Almacén de origen de envío

<table>
<thead>
<tr>
<td><strong>Campo</strong></td>
<td><strong>Descripción</strong></td>
<td><strong>Ámbito</strong></td>
<td><strong>Requerido</strong></td>
</tr>
</thead>
<tbody>
<tr>
<td><strong>[!UICONTROL Enable Ship From Store]</strong></td>
<td>Activa o desactiva la opción Entrega en el hogar en las tiendas de comercios. Cuando se habilita, las ubicaciones de las tiendas de comerciantes se consideran en conjunto con otras fuentes asignadas en las existencias asociadas a su sitio web.<br></br>En los servicios estándar de Inventory management, la opción [!DNL Ship from Store] es inherente y no se puede deshabilitar. Con la solución Store Fulfillment, puede activarla o desactivarla.<br></br>Puede ajustar esta configuración por ubicación de comerciante y producto.</td>
<td>Global</td>
<td>No</td>
</tr>
</tbody>
</table>


## Administración de cuentas y permisos de uso de aplicaciones de Store Fulfillment

Configure las opciones de seguridad de la cuenta de usuario y la contraseña de la aplicación Store Fulfillment y la autenticación de doble factor.

### Seguridad de aplicación

<table>
<thead>
<tr>
<td><strong>Campo</strong></td>
<td><strong>Descripción</strong></td>
<td><strong>Ámbito</strong></td>
<td><strong>Requerido</strong></td>
</tr>
 </thead>
 <tbody>
<tr>
<td><strong>[!UICONTROL User Session Lifetime]</strong></td>
<td>Período de tiempo, en segundos, durante el que una sesión de usuario asociada a un almacén permanece activa antes del cierre de sesión automático. Los valores válidos van del 60 al 31536000.</td>
<td>Global</td>
<td>No</td>
</tr>
<tr>
<td><strong>[!UICONTROL Maximum Login Failures to Lockout Account]</strong></td>
<td>Especifica el número de intentos de inicio de sesión erróneos permitidos antes de que un asociado de almacén se bloquee en su cuenta.<br></br>Para deshabilitar el bloqueo de cuentas, establezca el valor en 0.</td>
<td>Global</td>
<td>No</td>
</tr>
<tr>
<td><strong>[!UICONTROL Lockout Time (minutes)]</strong></td>
<td>Número de minutos para bloquear una cuenta tras un error de inicio de sesión.</td>
<td>Global</td>
<td>No</td>
</tr>
<tr>
<td><strong>[!UICONTROL Force Password Change]</strong></td>
<td><em>[!UICONTROL Yes]</em>: Requiera que el usuario cambie su contraseña después de configurar la cuenta.<br></br><em>[!UICONTROL No]</em>: recomienda que el usuario cambie la contraseña después de configurar la cuenta.</td>
<td>Global</td>
<td>No</td>
</tr>
<tr>
<td><strong>[!UICONTROL Password Lifetime]</strong></td>
<td>El número de días que una contraseña sigue siendo válida antes de que se cambie la contraseña requerida. Dejar vacío para desactivar esta opción.</td>
<td>Global</td>
<td>No</td>
</tr>
</tbody>
</table>

## Métodos de envío

La Satisfacción de almacenes funciona ampliando las capacidades nativas de Adobe Commerce [!DNL In-Store Delivery]. Después de instalar la extensión, puede configurar los métodos de envío en tienda mediante la siguiente configuración ampliada que se añade al administrador.

- **Recogida en tienda**: opciones de oferta para la entrega en tienda durante el proceso de cierre de compra
Estos ajustes configuran los escenarios de envío más comunes para los pedidos de BOPIS.

- **[!UICONTROL Curbside pick up]**: opciones de oferta para que los clientes estacionen en una ubicación de tienda y un dependiente les entregue su pedido.

Configure estas opciones desde el Administrador seleccionando <strong>[!UICONTROL Stores > Configuration > Sales > Delivery Methods > In-Store Pickup]</strong>.

>[!NOTE]
>
>Para obtener información adicional sobre cómo configurar las opciones de envío en tienda, consulte [Envío en tienda](https://experienceleague.adobe.com/es/docs/commerce-admin/stores-sales/delivery/basic-methods/shipping-in-store-delivery) en la _Guía del usuario de Adobe Commerce_.


### Configuración de métodos de envío

Con el método de entrega en tienda, el cliente puede seleccionar un origen para utilizarlo como ubicación de recogida durante el cierre de compra.

<table>
<thead>
<tr>
<td><strong>Campo</strong></td>
<td><strong>Descripción</strong></td>
<td><strong>Ámbito</strong></td>
<td><strong>Requerido</strong></td>
</tr>
 </thead>
 <tbody>
<tr>
<td><strong>[!UICONTROL Enable In-Store Pickup]</strong></td>
<td>Activa o desactiva la opción de recogida en la tienda disponible durante el cierre de compra para los clientes que elijan la recogida en la tienda. Cuando la selección en tienda está desactivada, la opción no se muestra.<br></br>Esta configuración global se aplica a todas las tiendas. Cuando está activada, puede desactivarla selectivamente en la ubicación de la tienda.</td>
<td>Sitio web</td>
<td>No</td>
</tr>
<tr>
<td><strong>[!UICONTROL Enable Curbside Pickup]</strong></td>
<td>Habilite o deshabilite la opción de recogida en la acera durante el proceso de cierre de compra para los clientes que elijan la recogida en la tienda.<br></br>Esta configuración global se aplica a todas las tiendas. Cuando está activada, puede desactivarla selectivamente en la ubicación de la tienda.</td>
<td>Sitio web</td>
<td>No</td>
</tr>
</tbody>
</table>

### Configuración del título del método de envío

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
<td><strong>Título del envío a domicilio</strong></td>
<td>Especifica el título que se mostrará para la opción Entrega en el hogar en las áreas de producto, carro y cierre de compra. La entrega a domicilio se refiere a las funciones de envío estándar de Adobe Commerce, desde un almacén, por un transportista o directamente a la dirección de envío proporcionada por el cliente. </br></br>Esta etiqueta no afecta a las etiquetas de método de envío del transportista seleccionado.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
<tr>
<td><strong>Descripción del envío a domicilio</strong></td>
<td>Una descripción opcional que se muestra siempre que se muestra el título de la entrega a domicilio a los clientes. La mayoría de las veces, la descripción es un mensaje estático para comunicar las promesas de envío. Algunos ejemplos:</br><code>Same-day shipping on orders by 4</code></br></br><code>Ships within 2 business days</code></td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
<tr>
<td><strong>Título de recogida de tienda</strong></td>
<td>Cuando se presentan a un cliente las opciones de entrega y la recogida en la tienda está disponible, se muestra esta etiqueta. </br></br>Puede personalizar esta etiqueta, que se muestra en las áreas de producto, carro y cierre de compra.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
<td><strong>Descripción de recogida en tienda</strong></td>
<td>Siempre que se muestre el título de la recogida en la tienda, puede incluir una descripción de forma opcional. Este mensaje estático ayuda a mejorar las comunicaciones con los clientes relacionadas con la experiencia de recogida en la tienda. Algunos ejemplos:</br></br><code>Get it today for free!</code></br></br><code>Ready for pickup in an hour!</code></td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
<tr>
<td><strong>Título de recogida en tienda</strong></td>
<td>Cuando la opción de recogida en tienda está activada, este título se muestra a los clientes como la opción de entrega de recogida en tienda. Puede personalizar su etiqueta.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
<tr>
<tr>
<td><strong>Título de recogida en borda</strong></td>
<td>Cuando la opción de recogida en la acera está activada, la opción se muestra a los clientes como un tipo de opción de entrega de recogida en la tienda. Puede personalizar su etiqueta aquí.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
<tr>
<td><strong>Instrucciones de recogida en tienda</strong></td>
<td>Cuando un pedido está listo para ser recogido en sus tiendas minoristas, el cliente es notificado por correo electrónico. Si el cliente seleccionó [!DNL In-Store Pickup] durante el pago, puede personalizar las instrucciones de recogida aquí. </br></br>Estas instrucciones están configuradas globalmente y se aplican a todas las ubicaciones de tiendas minoristas. También puede personalizar las instrucciones en el nivel de ubicación de la tienda.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
<tr>
<td><strong>Instrucciones de recogida en bordillo</strong></td>
<td>Especifica las instrucciones de recogida de pedidos personalizadas que se incluirán en las notificaciones de correo electrónico de los clientes para las solicitudes de recogida en la zona protegida. </br></br>Estas instrucciones están configuradas globalmente y se aplican a todas las ubicaciones de tiendas minoristas. También puede personalizar las instrucciones en el nivel de ubicación de la tienda.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
<tr>
<td><strong>Tiempo de espera de recogida estimado</strong></td>
<td>La cantidad de minutos necesarios antes de recibir un pedido, de cumplimentarlo y de prepararlo para su recogida. Esta información se muestra al cliente al seleccionar una ubicación de tienda minorista para la opción de envío Recogida en tienda. Esta configuración se aplica a todas las tiendas. También puede personalizar el tiempo de espera en el nivel de ubicación de la tienda.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
<tr>
<td><strong>Etiqueta de tiempo de recogida estimado</strong></td>
<td>Muestra el tiempo estimado hasta que un pedido está disponible para la recogida del cliente. Esta información se muestra a los clientes cuando seleccionan una ubicación de tienda minorista para la opción de entrega [!DNL In-Store Pickup]. </br></br>Al personalizar esta etiqueta, puede usar el código <code>%1</code> para insertar su <strong>Plazo estimado de recogida</strong>. Por ejemplo:</br></br><code>Ready for Pickup in %1 minutes.</code></br></br>Esta configuración se aplica a todas las ubicaciones de tiendas. También puede personalizar el tiempo de espera en el nivel de ubicación de la tienda.</td>
<td>Vista de tienda</td>
<td>No</td>
<tr>
<td><strong>Descargo de responsabilidad por tiempo de recogida</strong></td>
<td>El contenido que se muestra en la página de producto en la información del objeto que enumera las horas de almacenamiento, los días festivos, los cierres inesperados, etc</td>
<td>Vista de tienda
</td>
<td>No
</td>
</tr>
</tbody></table>

### Configuración de títulos de disponibilidad de stock

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
<td><strong>En existencia</strong></td>
<td>Cuando un cliente utiliza la ubicación de la tienda, se muestra la disponibilidad de inventario de los artículos actuales para cada ubicación. </br></br>Puede personalizar la etiqueta de estado <em>[!UICONTROL in-stock]</em> aquí.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
<tr>
<td><strong>Agotado</strong></td>
<td>Cuando un cliente utiliza la ubicación de la tienda, se muestra la disponibilidad del inventario de los artículos actuales para cada ubicación.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
<tr>
<td><strong>Parcialmente en stock</strong></td>
<td>Cuando un cliente utiliza la ubicación de la tienda, se muestra la disponibilidad de inventario para cualquier artículo actual en cada ubicación. </br></br>Puede personalizar la etiqueta de estado <em>[!UICONTROL partially in-stock]</em> aquí.</td>
<td>Vista de tienda</td>
<td>No</td>
</tr>
</tbody></table>

