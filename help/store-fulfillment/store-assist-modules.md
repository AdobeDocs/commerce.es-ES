---
title: Flujos de trabajo de asistencia de tienda
description: Obtenga información acerca de los módulos Acopio, Escenario, Entrega y Pedidos disponibles en la aplicación Asistencia en tienda. Estos módulos habilitan el flujo de trabajo de entrega de tiendas de extremo a extremo para pedidos BOPIS. Store Associates utiliza estos módulos para gestionar y entregar pedidos de recogida de tiendas a los clientes.
role: Leader, Admin, User
level: Intermediate
feature: Shipping/Delivery, Tools and External Services, Customer Service
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '806'
ht-degree: 0%

---

# Flujos de trabajo de asistencia de tienda

La aplicación Store Assist proporciona a Store Associates cuatro módulos para administrar el proceso de cumplimiento en la tienda para comprar en línea y recoger pedidos en la tienda:

- **[Seleccionar](#pick-module)**: Obtenga visibilidad completa de todos los artículos pedidos y las herramientas para asegurarse de que se seleccionan los artículos y las cantidades adecuados. Los asociados de la tienda pueden elegir uno o varios pedidos simultáneamente para lograr una mayor eficiencia.

- **[Fase](#stage-module)**: especifica la ubicación en la que se realizan los pedidos mientras los clientes están de viaje en la tienda para que los Asociados de tienda puedan encontrar y entregar los pedidos más rápidamente.

- **[Entrega](#hand-off-module)**: recibe notificaciones en tiempo real después de que los clientes lleguen a la tienda para minimizar el tiempo de espera y entregar los pedidos sin problemas.

- **[Pedidos](#orders-module)**: vea una lista de todos los pedidos realizados en una tienda para que todos sepan la cantidad de pedidos y el estado de cada uno.

>[!NOTE]
>
>Antes de que los asociados de tienda puedan usar la aplicación Store Assist, un administrador debe completar el [proceso de configuración de la aplicación](app-setup.md).

## Elegir módulo

El módulo Pick ayuda a los asociados del almacén a encontrar y escanear los artículos pedidos por el cliente y empaquetarlos para su recogida. Puede ver cuántos pedidos han vencido y empezar a recogerlos de inmediato. También puede elegir otros pedidos para elegir primero. Los pedidos se ordenan por tiempo de vencimiento de entrega con pedidos vencidos primero. Los asociados de la tienda pueden seleccionar los pedidos que desean seleccionar en cualquier pedido que requieran sus operaciones.

Sus asociados también pueden elegir elegir un pedido a la vez o varios pedidos al mismo tiempo.

Al realizar la selección, los asociados de la tienda ven una lista de todos los artículos que se van a seleccionar para cada pedido, sus cantidades, el precio y la descripción del producto del catálogo. Se muestra una barra de progreso para ayudarles a navegar dentro de la Asistencia de tienda mientras recogen pedidos.

Una vez que sus asociados empiezan a seleccionar y seleccionan los artículos que van a seleccionar, se les presenta toda la información relevante del artículo, como: tamaño, color, cantidad, precio, descripción, ajuste y SKU/UPC. Los asociados tienen dos acciones disponibles al acopio de pedidos:

- Indica que el artículo no se puede encontrar y déclencheur un reembolso.
- Escanee el código de barras del elemento. El propósito de la exploración es verificar que seleccionaron el elemento correcto. En caso de que la cámara no pueda leer el código de barras, los socios de la tienda deben introducir manualmente el SKU del artículo que han elegido.

Si los asociados no pueden encontrar un elemento, pueden omitirlo y volver a él más tarde.  El reembolso mencionado anteriormente se emite solo una vez que completan la fase de recogida del pedido.

## Módulo de ensayo

El módulo Fase muestra dónde se coloca el pedido embolsado hasta que llega el cliente para recogerlo. La configuración de esta ubicación es un paso clave para evitar la pérdida de pedidos cuando los socios de la tienda finalizan su turno antes de que llegue el cliente o si tiene muchos pedidos. En cualquier caso, está diseñado para ayudarle a encontrar rápidamente el pedido correcto con toda la información relevante sobre él.

Puede utilizar una barra de texto de forma libre para indicar dónde se coloca el pedido: debajo del mostrador, en la sala de atrás o en la ubicación B3, todo en función de sus operaciones.

También puede actualizar fácilmente la ubicación de ensayo en la aplicación, si sus asociados necesitan colocarla en otro lugar.

## Módulo de mano libre

El módulo [!UICONTROL Hand Off] muestra qué clientes se han registrado para recoger sus pedidos y dónde se almacenan en zona intermedia sus pedidos y los esperan. Los clientes pueden recoger los pedidos en la tienda o en el aparcamiento exterior / acera. La información sobre su ubicación exacta se presenta en este módulo una vez que se han registrado.

Una vez que seleccione un pedido que esté listo para el traspaso de clientes. Todos pueden ver la información del pedido, incluidos los artículos que no se encontraron, la ubicación de espera del cliente, el tiempo de espera, el lugar en el que se realiza el pedido y el número de teléfono del cliente si está disponible.

Es posible que el cliente haya elegido a una persona alternativa para recoger el pedido. En este caso, verá el nombre y la información de contacto de la persona que se supone que debe elegir el pedido.

Al entregar el pedido al cliente, el asociado de tienda debe aceptar el pedido o rechazar determinados artículos. Una vez que el cliente está satisfecho, debe firmar para el pedido en el dispositivo de su socio, si una firma de su compañía requiere una firma.

Si los clientes llegan sin registrarse, sus asociados pueden registrarlos manualmente.

## Módulo Pedidos

El módulo Pedidos muestra todos los pedidos existentes y su estado. Cuando un cliente llama para comprobar su pedido, los Asociados de la Tienda pueden encontrar la información rápidamente buscando el número o buscando en el módulo Pedidos.

Store Associates también puede cancelar pedidos desde la página Pedidos de la aplicación Store Assist.
