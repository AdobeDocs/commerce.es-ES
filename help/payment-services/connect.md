---
title: Conectar su instancia
description: Conecte la instancia de Commerce con una clave de API y una clave privada, y especifique el espacio de datos en la configuración.
feature: Payments, Checkout, Configuration, Saas
exl-id: f2b3be02-e9dd-4bca-b9e4-c80a56bf8691
source-git-commit: 16bd0e7ed1e8982e1571e2593115824a2004b7dc
workflow-type: tm+mt
source-wordcount: '636'
ht-degree: 0%

---

# Conectar su instancia

[!DNL Payment Services] cuenta con la tecnología de Commerce Services y se implementa como SaaS (software como servicio). La instancia de Commerce se conecta mediante una clave de API y una clave privada, y se especifica el espacio de datos en la configuración mediante [Commerce Services Connector](https://experienceleague.adobe.com/docs/commerce/user-guides/saas.html). **Solo configuró esta conexión una vez.**

>[!VIDEO](https://video.tv.adobe.com/v/3447835)

>[!INFO]
>
> Vea nuestro vídeo de [[!DNL Adobe Commerce] Services Connector](https://experienceleague.adobe.com/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-commerce-services-connector.html?lang=es) para obtener más información.

* Si ya ha conectado *su instancia*, al obtener y utilizar sus credenciales de la API y configurar los servicios de Commerce, puede continuar con [la configuración de su zona protegida de pruebas](https://experienceleague.adobe.com/docs/commerce/payment-services/get-started/sandbox.html?lang=es).
* Si todavía *necesita conectar su instancia*, vea la información en este tema sobre [obtención de credenciales de API](#obtain-api-credentials) y [configuración de los servicios de Commerce](#configure-commerce-services).
* Si *no está seguro de si la instancia está conectada*, vaya a **Sistema** > Servicios > **Conector de servicios de Commerce** y vea los valores de clave de API pública y privada en las secciones [!UICONTROL Sandbox Keys] y [!UICONTROL Production Keys], y los campos *Proyecto* y *Espacio de datos* en la sección [!UICONTROL SaaS Identifier]. Si esos valores están presentes, la instancia está conectada.

>[!NOTE]
>
>Todos los comerciantes con derecho a servicios de pago pueden utilizar un espacio de datos de producción y dos espacios de datos de prueba.

## Obtener credenciales de API

Para consumir un servicio SaaS de Commerce, debe usar las claves de API de su instancia (clave de API pública de Commerce y clave privada) tanto para la zona protegida como para la producción, que se crean y administran en su [Panel de Mi cuenta](https://account.magento.com/customer/account/login). [El par de claves](https://experienceleague.adobe.com/es/docs/commerce-admin/config/services/saas) se puede crear para una cuenta de Commerce (una para zona protegida y otra para producción), aunque solo se puede usar activamente un par a la vez.

>[!NOTE]
>
>¿Necesita ayuda para acceder a su panel de [!UICONTROL My Account]? Consulte [Crear una cuenta de Commerce](https://experienceleague.adobe.com/es/docs/commerce-admin/start/commerce-account/commerce-account-create).

Una vez creada, siempre encontrará una clave de API pública en el panel de Mi cuenta. Se puede copiar o eliminar según sea necesario. La clave de API privada se vuelve visible al crear una clave de API pública para simulación de pruebas o producción; solo está disponible para copiarla o guardarla en el cuadro de diálogo siguiente y no se puede acceder a ella posteriormente.

Un par de claves API determinado es válido para todos los servicios de Commerce en un entorno, por lo que si ya tiene los servicios de Commerce configurados para su instancia, su par de claves API ya estará presente en el conector de servicios de Commerce.

Si se pierde su clave de API, se debe [generar](https://experienceleague.adobe.com/docs/commerce/payment-services/get-started/connect.html?lang=es#generate-an-api-key-and-private-key) un nuevo par de claves de API y [aplicar](https://experienceleague.adobe.com/docs/commerce/payment-services/get-started/connect.html?lang=es#configure-saas-project) a la configuración del Conector de servicios de Commerce en el administrador. Si se configuran claves incorrectas o no existe ninguna en la configuración, aparecerá un cuadro de diálogo de error de verificación de cuenta en Payment Services que le notificará que la cuenta no se ha verificado.

Ver una [lista de servicios de Commerce disponibles que usan la API](https://experienceleague.adobe.com/es/docs/commerce/user-guides/integration-services/saas#availableservices).

Para obtener información sobre cómo generar una clave de API para entornos de zona protegida o de producción, consulte [Credenciales](https://experienceleague.adobe.com/docs/commerce/user-guides/saas.html#apikey).

>[!IMPORTANT]
>
>Se recomienda no volver a generar un par de claves de API *y* para cambiar el identificador de SaaS o el espacio de datos en una instancia de producción activa. Perderá datos de su instancia si se modifican.

## Configuración de servicios de Commerce

La misma clave de API se puede usar en todas las instancias, pero cada una debe tener su propio [espacio de datos SaaS](https://experienceleague.adobe.com/docs/commerce/user-guides/saas.html#saasenv).

>[!NOTE]
>
>Los comerciantes deben utilizar las mismas claves generadas para el MageID para sus derechos de pago.

Ahora que ha obtenido sus credenciales, puede configurar su proyecto SaaS y el espacio de datos Saas.

1. En la barra lateral _Admin_, vaya a **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]**.
1. Haga clic en **[!UICONTROL Configure Commerce Services]**.

   Esta opción está visible si aún no ha configurado los servicios de Commerce para su cuenta.

   Se le dirigirá al área de configuración en Admin, **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**>**[!UICONTROL Commerce Services Connector]**, para configurar Commerce Services Connector.

1. Para configurar los servicios de Commerce, siga los pasos descritos en [Configuración de SaaS](https://experienceleague.adobe.com/docs/commerce/user-guides/integration-services/saas.html?lang=es#saasenv).

   >[!INFO]
   >
   > Vea nuestro vídeo de [[!DNL Adobe Commerce] Services Connector](https://experienceleague.adobe.com/docs/commerce-learn/tutorials/admin/adobe-commerce-services/configure-adobe-commerce-services-connector.html?lang=es#configuration-faqs) para obtener más información.

## Extremo

[!DNL Payment Services] utiliza [Commerce Services Connector](https://experienceleague.adobe.com/docs/commerce/user-guides/saas.html) para conectarse a Commerce Services e implementarlo como SaaS. Este(a) [!DNL Commerce Services Connector] se comunica a través del extremo en:

* `commerce-beta.adobe.io` para entornos de espacio aislado.
* `commerce.adobe.io for` para entornos en vivo.
