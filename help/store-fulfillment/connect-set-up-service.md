---
title: Conexión de la solución Store Fulfillment
description: Establezca las conexiones entre Adobe Commerce y la solución Store Fulfillment. Cree y autorice una integración de Adobe Commerce y añada las credenciales de la cuenta Store Fulfillment a la configuración del servicio Adobe Commerce.
role: Admin, Developer
level: Intermediate
feature: Shipping/Delivery, Install, Configuration, User Account, Tools and External Services
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '452'
ht-degree: 0%

---

# Conexión de la solución Store Fulfillment

Conecte los servicios de cumplimiento de almacenamiento con Adobe Commerce agregando las credenciales de autenticación y los datos de conexión necesarios al administrador de Adobe Commerce.

- **[Configurar [!DNL Commerce integration settings]](#create-an-adobe-commerce-integration)**: crea una integración de Adobe Commerce para los servicios Store Fulfillment y genera los tokens de acceso para autenticar las solicitudes entrantes de los servidores Store Fulfillment.

- **[Configurar las credenciales de la cuenta para los servicios de cumplimiento de almacenamiento](#configure-store-fulfillment-account-credentials)**-Agregue sus credenciales para conectar Adobe Commerce a su cuenta de cumplimiento de almacenamiento.

>[!NOTE]
>
>Complete la configuración de la conexión y valide la conexión correctamente antes de comenzar la prueba.

## Creación de una integración de Adobe Commerce

Para integrar Adobe Commerce con los servicios Store Fulfillment, crea una integración de Commerce y genera tokens de acceso que se pueden utilizar para autenticar solicitudes de los servidores Store Fulfillment. También debe actualizar las opciones de Adobe Commerce [!UICONTROL Consumer Settings] para evitar `The consumer isn't authorized to access %resources.` errores de respuesta en las solicitudes de Adobe Commerce a [!DNL Store Fulfillment] servicios.

1. Desde Admin, cree la integración para la adquisición de tiendas.

   - Asigne un nombre a la extensión
   - Introduzca su dirección de correo electrónico
   - Introduzca la contraseña de su cuenta de administrador

1. Configure los permisos de acceso a recursos de API para la integración con lo siguiente:

   - Ventas > BOPIS Actualización de pedidos
   - Sistema > Permisos de aplicación de Store Fulfillment

1. Genere los tokens de acceso para la autenticación guardando y activando la integración.

1. Copie y guarde los tokens de acceso en una ubicación segura y cifrada.

1. Póngase en contacto con el administrador de cuentas para completar la configuración en el lado de Store Fulfillment y autorizar la integración.

1. Habilite la opción de Adobe Commerce [!UICONTROL Consumer Settings] para [!UICONTROL Allow OAuth Access Tokens to be used as standalone Bearer tokens].

   - Desde el administrador, vaya a **[!UICONTROL Stores]** > [!UICONTROL Configuration] > **[!UICONTROL Services]** > **[!UICONTROL OAuth]** > **[!UICONTROL Consumer Settings]**

   - Establezca la opción [!UICONTROL Allow OAuth Access Tokens to be used as standalone Bearer tokens] en **[!UICONTROL Yes]**.

>[!IMPORTANT]
>
> El token de integración es específico del entorno. Si restaura la base de datos para un entorno con los datos de origen de un entorno diferente (por ejemplo, restaurando los datos de producción desde un entorno de ensayo), excluya la tabla `oauth_token` de la exportación de la base de datos para que los detalles del token de integración no se sobrescriban durante la operación de restauración.


## Configurar credenciales de cuenta de Store Fulfillment

Después de completar el formulario de admisión, se crea una cuenta de cumplimiento de Walmart Store para usted. Recibirá las siguientes credenciales cuando estén disponibles:

- [!DNL Merchant ID]
- [!DNL Consumer ID]
- [!DNL Consumer Secret]
- [!DNL API Server URL]
- [!DNL Token Auth Server URL] (normalmente es la misma que la configuración anterior)

Estas credenciales son necesarias para configurar y utilizar Satisfacción de pedidos de la tienda.

>[!NOTE]
>
>El proceso de creación de la cuenta puede tardar un poco en completarse. Mientras espera las credenciales, [revise y configure otras opciones para la solución Store Fulfillment](service-config-settings-overview.md).

### Añadir credenciales para conectarse a Store Fulfillment

1. Configure [credenciales de cuenta](enable-general.md) para los entornos Producción y Zona protegida.

1. Desde el administrador, vaya a **[!UICONTROL Stores > Configuration > Services > Store Fulfillment by Walmart Commerce Technologies]**

1. Escriba las credenciales de cuenta proporcionadas para **[!UICONTROL Production environment]**. Todos los campos son obligatorios.

1. Seleccione **[!UICONTROL Save Config]**.

1. Pruebe la conexión seleccionando **[!UICONTROL Validate Credentials]**.

>[!NOTE]
>
>Si las credenciales no son válidas, compruebe que ha introducido los valores correctos para cada entorno y vuelva a validarlas. Póngase en contacto con el representante de cuentas si sigue teniendo problemas de conexión.
