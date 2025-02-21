---
title: Configuración de aplicación
description: Configura la aplicación  [!DNL Store Assist] para administrar los flujos de trabajo y los procesos de adquisición de tiendas de extremo a extremo para comprar en línea y recoger pedidos de tiendas.
level: Intermediate
role: Admin
feature: Shipping/Delivery, Configuration, Tools and External Services
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '619'
ht-degree: 0%

---

# Configuración de aplicación

Store Assist es una aplicación de plataforma de cumplimiento como servicio (FaaS) con tecnología de Walmart Commerce Technologies. La aplicación proporciona capacidades de cumplimiento en la tienda para administrar [!DNL buy online, pick up in store] pedidos (BOPIS). Con la asistencia de tienda, los socios de tienda pueden ver qué artículos pidieron los clientes, recoger los artículos correctos más rápido y configurar pedidos satisfechos para la entrega de recogida en tienda o en la zona de la calle a los clientes.

La aplicación Store Assist recibe toda la información de pedidos y clientes (desde los detalles del pedido hasta las horas de recogida) y pone los datos a disposición de los asociados del almacén en línea, a través de dispositivos móviles. La aplicación incluye módulos de [!UICONTROL Pick], [!UICONTROL Stage], [!UICONTROL Handoff] y [!UICONTROL Orders] para ayudar a las Asociaciones de tienda con actividades de cumplimiento como las siguientes:

- Asignar fechas y horas de entrega de pedidos.
- Reciba notificaciones de clientes cuando lleguen para recoger el pedido.
- Realizar pedidos de entrega a los clientes.
- Rastree el estado de los pedidos de todos los pedidos en sus ubicaciones de tiendas asignadas.

>[!NOTE]
>
>Para obtener más información acerca de la aplicación Store Assist, revisa el tema [Flujos de trabajo de asistencia de almacenamiento](store-assist-modules.md).

## Configuración de la aplicación de asistencia de tienda

La aplicación Store Assist requiere dos tipos de configuración:

- Configuración del sistema de administración de Adobe Commerce para [administrar cuentas de usuario, funciones de usuario, permisos de recursos](user-setup.md) y [las selecciones de modelo y fabricación de automóviles disponibles para los clientes durante el proceso de registro](check-in-experience-setup.md).

- Ajustes de configuración de front-end para personalizar la interfaz de la aplicación Store Assist y otros ajustes, como:

   - **Marca la aplicación de asistencia en tienda**: personaliza la interfaz de usuario de la aplicación con el logotipo y los colores de tu empresa.

   - **Actualice las instrucciones predeterminadas**: personalice las instrucciones de los módulos Asistencia de tienda para la selección, ensayo, transferencia y pedido para guiar a los asociados de tienda en cada paso del flujo de trabajo de cumplimiento de la empresa.

   - **Localización**: seleccione el idioma disponible para la aplicación. Elija el formato de fecha y hora y seleccione las unidades de medida y la moneda predeterminadas.

   - **Tiempo de inactividad**: especifique la cantidad de tiempo que la aplicación debe estar inactiva antes de que cierre la sesión.

   - **Cancelación del almacén**: especifique si los pedidos se pueden cancelar del almacén y qué funciones tienen permisos de cancelación

   - **Ventana de limpieza de pedidos**: especifique cuánto tiempo ha transcurrido el [Plazo estimado de recogida](enable-general.md#delivery-method-title-configuration) durante el cual un pedido recogido permanece en almacenamiento provisional antes de volver a estar disponible, por ejemplo, tres días. El valor predeterminado es de siete días. Si esta configuración está activada, la solicitud se cancela automáticamente cuando caduca este tiempo. Los artículos son repuestos y el comerciante recibe un correo electrónico de cancelación.

   - Personalice todas las instrucciones de la aplicación (picking, ensayo, entrega).

   - **Notificaciones de picking**: especifique si desea enviar una notificación push para iniciar el proceso de picking después de que un cliente realice un pedido.

   - **Notificaciones de registro**: especifique si desea enviar una notificación push durante el proceso de registro para las recogidas de pedidos- después del registro, después de que el tiempo de espera del cliente exceda un período de tiempo especificado. O bien, deshabilite la notificación.

   - **Proceso de entrega**: habilita procesos opcionales cuando el asociado de tienda envía el pedido al cliente; por ejemplo, requiere una firma del cliente o pide al asociado que compruebe el ID del cliente.

   - **Habilitar el rechazo de artículos al entregar**: permite a los clientes devolver o cancelar artículos de pedidos durante el envío de pedidos.

  Trabaje con el equipo de servicios al cliente de Commerce Technologies de Walmart para completar la configuración de front-end de la aplicación Store Assist.

## Descarga e instalación de aplicaciones

Una vez configurada y configurada la aplicación Store Assist, Store Associates puede descargar, instalar e iniciar sesión en la aplicación Store Assist desde sus dispositivos móviles.

- Compruebe que el dispositivo móvil cumple los [requisitos de hardware y software](solution-requirements.md#store-assist-app-requirements) para la solución Store Fulfillment.

- Descargue la aplicación Store Assist desde [Apple App Store](https://apps.apple.com/us/app/store-assist-by-walmart/id1609281539){target="_blank"} o [Google Play store](https://play.google.com/store/apps/details?id=com.walmart.faas.storeassist){target="_blank"}.

- Store Associates necesita la siguiente información para iniciar sesión:

   - **[!UICONTROL Company name]** asociado con la cuenta de asistencia de tienda

   - **Credenciales de cuenta de Store Assist**: credenciales de nombre de usuario y contraseña para su cuenta.

  Un administrador de Adobe Commerce puede crear y administrar cuentas de usuario de [!DNL Store Assist app] para todas las ubicaciones de tiendas que tengan [Recogida en tienda](merchant-store-configuration.md#pickup-location-configuration) habilitada en la configuración de las Tiendas de administración.
