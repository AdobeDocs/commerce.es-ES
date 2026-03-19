---
title: Commerce Services Connector
description: Obtenga información sobre cómo integrar su instancia de Adobe Commerce o Magento Open Source en servicios mediante claves de API de producción y de zona protegida.
feature: Services, Saas
role: Admin, User
exl-id: 1aa6ba8b-be39-496e-b83d-a4a7db9f5dd8
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."
source-git-commit: 6e107238b8eae31f35f43524aee5690c0fe0e03d
workflow-type: tm+mt
source-wordcount: '1564'
ht-degree: 0%

---

# [!DNL Commerce Services Connector]

Algunas características de Adobe Commerce y Magento Open Source utilizan [!DNL Commerce Services] y se implementan como SaaS (software como servicio). Para utilizar estos servicios, debe conectar su instancia de [!DNL Commerce] mediante las claves de API de producción y de zona protegida, y especificar el espacio de datos en la [configuración](#saas-configuration). Solo es necesario configurar la conexión una vez para cada instancia.

Solamente el propietario de la licencia [!DNL Commerce] puede generar estas claves API. Si no es el propietario de la licencia, solicite las claves a la persona o al equipo propietario de la licencia de Commerce para su tienda.

## Servicios disponibles {#availableservices}

A continuación se enumeran las características de [!DNL Commerce] a las que puede tener acceso a través de [!DNL Commerce Services Connector]:

| Servicio | Disponibilidad |
| --- | --- |
| [[!DNL Product Recommendations]](/help/product-recommendations/overview.md) con tecnología de Adobe AI | Adobe Commerce |
| [[!DNL Live Search]](/help/live-search/overview.md) con tecnología de Adobe AI | Adobe Commerce |
| [[!DNL Payment Services]](/help/payment-services/guide-overview.md) | ADOBE COMMERCE y MAGENTO OPEN SOURCE |
| [[!DNL Catalog Service]](/help/catalog-service/overview.md) | Adobe Commerce |
| [[!DNL Data Connection]](/help/data-connection/overview.md) | Adobe Commerce |

## Arquitectura

En un nivel superior, [!DNL Commerce Services Connector] se compone de los siguientes elementos principales:

![Arquitectura del conector de servicios de Commerce](assets/saas-config-sync-workflow.png)

En las secciones siguientes se analiza cada uno de estos elementos con más detalle.

## Credenciales {#apikey}

Las claves API de producción y de zona protegida se generan a partir de la cuenta [!DNL Commerce] del [propietario de la licencia](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/start/onboarding). La cuenta de Commerce está identificada por un ID único de [!DNL Commerce] (MageID). El propietario de la licencia de la organización del comerciante puede generar claves de API para servicios como Product Recommendations o Live Search, siempre y cuando la cuenta esté al día.

Las claves se pueden compartir según sea necesario con el integrador de sistemas o el equipo de desarrollo que gestiona los proyectos y entornos en nombre del titular de la licencia. Los desarrolladores a los que el propietario de la licencia ha concedido [!DNL Shared Access] no pueden generar las claves en nombre del propietario de la licencia aunque la organización del comerciante esté presente en el menú desplegable [!DNL Switch Accounts] de su cuenta.

Además, los integradores de soluciones tienen derecho a utilizar [!DNL Commerce Services]. Si usted es un integrador de soluciones, el firmante del contrato del socio [!DNL Commerce] debe generar las claves de API.

Los identificadores clave *Production* y *Sandbox* hacen referencia a entornos de espacio de datos SaaS donde [!DNL Commerce Services] almacenan datos (no en los entornos de Adobe Commerce). Puede utilizar el mismo conjunto de claves API en los entornos local, de desarrollo, de ensayo y de producción de Adobe Commerce; lo que importa es que pegue el par de claves correcto para el espacio de datos que configure.

El propietario de la licencia suele ser el contacto principal de la cuenta de Adobe Commerce y no siempre es el mismo que el propietario del proyecto de Adobe Commerce en el proyecto de infraestructura en la nube.

### Generar las claves API de producción y de zona protegida {#genapikey}

1. Inicie sesión en su cuenta de [!DNL Commerce] en [https://account.magento.com](https://account.magento.com/customer/account/login){:target="_blank"}.

1. En la ficha **Magento**, seleccione **Portal de API** en la barra lateral.

1. En el menú _Entorno_, seleccione **Producción** o **Espacio aislado**.

1. Escriba un nombre en la sección _Claves de API_ y haga clic en **Agregar nueva** para abrir el cuadro de diálogo y descargar la clave nueva.

   ![Descargar clave privada](assets/download-api-private-key.png)

   >[!WARNING]
   >
   > Puede copiar o descargar la clave privada solo una vez. Guárdelo en un lugar seguro.

1. Haga clic en **Descargar** para guardar la clave privada y cierre el cuadro de diálogo.

1. Repita los pasos anteriores para cada entorno (producción y zona protegida).

   La sección **Claves de API** ahora muestra sus claves de API (públicas). Necesita las cuatro claves (tanto la de producción como la de zona protegida, Pública+Privada) al [seleccionar o crear un proyecto SaaS](#createsaasenv) en cualquiera de los entornos o instalaciones asociados con la licencia.

## Configuración de SaaS {#saasenv}

Las instancias de [!DNL Commerce] deben configurarse con un proyecto SaaS y un espacio de datos SaaS para que [!DNL Commerce Services] pueda enviar datos a la ubicación correcta. Un proyecto SaaS agrupa todos los espacios de datos SaaS. Los espacios de datos SaaS se utilizan para recopilar y almacenar datos que permiten que [!DNL Commerce Services] funcione. Algunos de estos datos pueden exportarse desde la instancia [!DNL Commerce] y otros pueden recopilarse a partir del comportamiento del comprador en la tienda. Estos datos se conservan para proteger el almacenamiento en la nube.

Para [!DNL Product Recommendations] y [!DNL Live Search], el espacio de datos de SaaS contiene datos de catálogo y de comportamiento. Puede apuntar una instancia de [!DNL Commerce] a un espacio de datos SaaS [seleccionándola](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas) en la configuración de [!DNL Commerce].

>[!WARNING]
>
> Use su **espacio de datos SaaS de producción** solo con su instalación de producción [!DNL Commerce]. Su uso en entornos que no son de producción puede combinar datos de prueba y activos (por ejemplo, direcciones URL de ensayo o datos de catálogo de prueba). Si esto sucede, [envíe una solicitud de soporte técnico](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/overview) para solicitar la limpieza de datos.

Si no encuentra los campos de configuración de Live Search en el Administrador, compruebe que ha introducido el par de claves de API correcto para el espacio de datos seleccionado (los espacios de datos de producción utilizan claves de producción; los espacios de datos de prueba utilizan claves de zona protegida). Si configura claves incorrectas, los servicios SaaS como Live Search no están disponibles en ese entorno de Adobe Commerce.

### Eliminación de una clave API {#delapikey}

>[!WARNING]
>
>La eliminación de una clave que aún está en uso interrumpe inmediatamente los servicios conectados.

Antes de eliminar una clave API, genere y almacene de forma segura una clave de reemplazo. Actualice todas las integraciones para utilizar la nueva clave y confirme que los servicios dependientes funcionan según lo esperado.

Si no ve **[!DNL Live Search]** campos de configuración en el panel de administración, confirme que ha introducido la clave de API de SaaS correcta para ese entorno. Utilice la clave SaaS de producción para el espacio de datos de producción y la clave de ensayo para el espacio de datos de ensayo. Si se configura una clave incorrecta, los servicios SaaS (incluido **[!DNL Live Search]**) no estarán disponibles en su entorno de Adobe Commerce.

En la clave de API que desea quitar, haga clic en **[!UICONTROL Delete]**. Cuando se le solicite, confirme la operación para quitar la clave de forma permanente.

### Aprovisionamiento de espacio de datos SaaS

Todos los comerciantes de Adobe Commerce pueden acceder a un espacio de datos de producción y a dos espacios de datos de prueba por proyecto de SaaS.

Puede utilizar los espacios de datos de prueba en entornos que no sean de producción, pero evite utilizar el mismo espacio de datos en varios entornos al mismo tiempo. Si desea mover un espacio de datos de prueba a un entorno diferente, realice una limpieza de datos antes de seleccionarlo y configurarlo en el entorno nuevo.

Para los proyectos de Adobe Commerce Cloud Pro con varios entornos de ensayo, puede solicitar espacios de datos de prueba adicionales para cada entorno de ensayo [enviando una solicitud de asistencia](https://experienceleague.adobe.com/home?support-tab=home#support). Sin embargo, si solo tiene un entorno de ensayo y necesita espacios de datos de prueba adicionales, tiene las siguientes opciones:

- Póngase en contacto con el equipo de éxito del cliente o con el administrador de éxito del cliente designado para solicitar un entorno de ensayo adicional.

- [Envíe una solicitud de soporte técnico](https://experienceleague.adobe.com/home?support-tab=home#support) para solicitar el espacio de datos de prueba adicional e indicar la justificación comercial del espacio de datos adicional. Esta solicitud está sujeta a aprobación.

Los clientes de Magento Open Source que utilicen Adobe Payment Services también pueden solicitar un espacio de datos adicional. Póngase en contacto con el equipo de pagos para obtener la aprobación previa de los espacios de datos adicionales antes de enviar una [solicitud de soporte](https://experienceleague.adobe.com/home?support-tab=home#support) para solicitar el espacio de datos de prueba.

Los clientes que sean propietarios de varios proyectos en la nube o instalaciones locales (activas/de producción) también pueden solicitar espacios de datos de producción y prueba adicionales para cada proyecto o instancia enviando [una solicitud de soporte](https://experienceleague.adobe.com/home?support-tab=home#support).

### Seleccionar o crear un proyecto SaaS {#createsaasenv}

Para seleccionar o crear un proyecto SaaS, solicite las claves de API [!DNL Commerce] al propietario de la licencia [!DNL Commerce] de su tienda:

1. En la barra lateral _Admin_, vaya a **Sistema** > Servicios > **Conector de servicios de Commerce**.

   Si no ve la sección **[!UICONTROL Commerce Services Connector]**, instale los módulos [!DNL Commerce] para el [[!DNL Commerce] servicio](#availableservices) deseado y asegúrese de que el paquete `magento/module-services-id` esté instalado.

1. En las secciones _[!UICONTROL Sandbox API Keys]_y_[!UICONTROL Production API Keys]_, pegue los valores de clave.

   - Las claves privadas deben incluir `-----BEGIN PRIVATE KEY-----` al principio de la clave y `-----END PRIVATE KEY-----` al final de la clave.
   - Si no dispone de una copia de las claves reales, solicítelas al propietario de la licencia y, a continuación, introduzca los valores en la configuración.

   No pegue los valores clave copiados de una copia de seguridad o instantánea de la base de datos. Cuando se guarda la configuración, se aplica una capa adicional de cifrado y las claves no funcionan.

1. Haga clic en **Guardar**.

   Cualquier proyecto SaaS asociado con sus claves aparecerá en el campo **Proyecto** de la sección **Identificador SaaS**.

1. Si no existen proyectos SaaS, haga clic en **Crear proyecto**. A continuación, en el campo **Proyecto**, escriba un nombre para su proyecto SaaS.

   Para evitar confusiones, no use un servicio Commerce específico como nombre para el proyecto (por ejemplo, *Live Search*, *Product Recommendations* o *Conexión de datos*). A menos que la licencia se haya aprovisionado para varios proyectos SaaS, puede utilizar el mismo proyecto SaaS para varios servicios.

1. Seleccione el **espacio de datos** que se usará para la configuración actual de su almacén de [!DNL Commerce].

   Si tiene instancias independientes para integrar con los servicios de Commerce, [envíe un vale de soporte técnico](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) para solicitar un nuevo proyecto de SaaS para cada instancia adicional. Una vez que la compatibilidad haya creado el proyecto SaaS, configure Commerce Services Connector para la instancia **con las mismas claves de API** y seleccione el nuevo proyecto SaaS y el espacio de datos.

>[!WARNING]
>
> Si genera claves nuevas en el portal de API, actualice inmediatamente las claves de API en la configuración de administración. Si el administrador sigue utilizando claves antiguas, las extensiones SaaS dejan de funcionar y se interrumpe la recopilación de datos.

Para cambiar los nombres de tu proyecto SaaS o espacio de datos, haz clic en **Cambiar nombre** junto a uno de ellos. Cambiar el nombre no afecta al servicio porque el nombre es sólo una etiqueta para ayudarle a identificar y diferenciar entre proyectos y espacios de datos.

## Organización de IMS (opcional) {#organizationid}

Para conectar la instancia de Adobe Commerce a Adobe Experience Platform, inicie sesión en la cuenta de Adobe con el Adobe ID. Después de iniciar sesión, la organización de IMS asociada a su cuenta de Adobe se muestra en esta sección.

## Exportación de datos SaaS

Cuando la instancia de [!DNL Commerce] se conecta correctamente a [!DNL Commerce Services], el proceso de exportación de datos de SaaS exporta los datos de Commerce del servidor [!DNL Commerce] a [!DNL Commerce SaaS Services] para que se puedan sincronizar con los servicios de Commerce conectados. En el Administrador, puede comprobar el estado de sincronización mediante el [panel de administración de datos](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard). Para obtener más información, consulte la [Guía de exportación de datos SaaS](../data-export/overview.md).
