---
title: Commerce Services Connector
description: Learn how to integrate your Adobe Commerce or Magento Open Source instance to services using production and sandbox API keys.
feature: Services, Saas
role: Admin, User
exl-id: 1aa6ba8b-be39-496e-b83d-a4a7db9f5dd8
badgePaas: label="PaaS only" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Applies to Adobe Commerce on Cloud projects (Adobe-managed PaaS infrastructure) and on-premises projects only."
source-git-commit: be1c739f3821a5f1e846b3026088e3a3ff45a60f
workflow-type: tm+mt
source-wordcount: '1420'
ht-degree: 0%

---

# [!DNL Commerce Services Connector]

Some Adobe Commerce and Magento Open Source features are powered by [!DNL Commerce Services] and deployed as SaaS (software as a service). To use these services, you must connect your [!DNL Commerce] instance using production and sandbox API keys, and specify the data space in the [configuration](#saas-configuration). You only need to configure the connection one time for each instance.

## Available services {#availableservices}

The following lists the [!DNL Commerce] features you can access through the [!DNL Commerce Services Connector]:

| Service | Disponibilidad |
| ---|--- |
| [[!DNL Product Recommendations]](/help/product-recommendations/overview.md) con tecnología de Adobe Sensei | Adobe Commerce |
| [[!DNL Live Search]](/help/live-search/overview.md) con tecnología de Adobe Sensei | Adobe Commerce |
| [[!DNL Payment Services]](/help/payment-services/overview.md) | ADOBE COMMERCE y MAGENTO OPEN SOURCE |
| [[!DNL Site-Wide Analysis Tool]](https://experienceleague.adobe.com/en/docs/commerce-operations/tools/site-wide-analysis-tool/intro) | Adobe Commerce |
| [[!DNL Catalog Service]](/help/catalog-service/overview.md) | Adobe Commerce |
| [[!DNL Data Connection]](/help/data-connection/overview.md) | Adobe Commerce |

## Arquitectura

En un nivel superior, [!DNL Commerce Services Connector] se compone de los siguientes elementos principales:

![Arquitectura del conector de servicios de Commerce](assets/saas-config-sync-workflow.png)

En las secciones siguientes se analiza cada uno de estos elementos con más detalle.

## Credenciales {#apikey}

Las claves API de producción y de zona protegida se generan a partir de la cuenta [!DNL Commerce] del [propietario de la licencia](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/start/onboarding). La cuenta de Commerce está identificada por un ID único de [!DNL Commerce] (MageID). El propietario de la licencia de la organización del comerciante puede generar claves de API para servicios como Product Recommendations o Live Search, siempre y cuando la cuenta esté al día.

Las claves se pueden compartir según sea necesario con el integrador de sistemas o el equipo de desarrollo que gestiona los proyectos y entornos en nombre del titular de la licencia. Los desarrolladores a los que el propietario de la licencia ha concedido [!DNL Shared Access] no pueden generar las claves en su nombre aunque la organización del comerciante esté presente en el menú desplegable [!DNL Switch Accounts] de su cuenta.

Además, los integradores de soluciones también tienen derecho a utilizar [!DNL Commerce Services]. Si usted es un integrador de soluciones, el firmante del contrato del socio [!DNL Commerce] debe generar las claves de API.

>[!NOTE]
>Los identificadores de clave *Production* y *Sandbox* no hacen referencia a su entorno. Utilice el mismo conjunto de claves API para para cada uno de los entornos, por ejemplo, los entornos local, de desarrollo, de ensayo o de producción.
>
>El propietario de la licencia suele ser el contacto principal de la cuenta de Adobe Commerce y no siempre es el mismo que el propietario del proyecto de Adobe Commerce en el proyecto de infraestructura en la nube.

### Generar las claves API de producción y de zona protegida {#genapikey}

1. Inicie sesión en su cuenta de [!DNL Commerce] en [https://account.magento.com](https://account.magento.com/customer/account/login){:target="_blank"}.

1. En la ficha **Magento**, seleccione **Portal de API** en la barra lateral.

1. En el menú _Entorno_, seleccione **Producción** o **Espacio aislado**.

   >[!NOTE]
   >
   >*Production* and *Sandbox* refer to the data space environments where data is stored in Adobe SaaS backend systems. No se refiere a entornos comerciales en los que vaya a utilizar las claves.

1. Enter a name in the _API Keys_ section, and click **Add New** to open the dialog to download the new key.

   ![Descargar clave privada](assets/download-api-private-key.png)

   >[!WARNING]
   >
   > Este cuadro de diálogo proporciona la única oportunidad que tiene para copiar o descargar las claves.

1. Haz clic en **Descargar** y luego en **Cancelar**.

1. Repita los pasos anteriores para cada entorno (producción y zona protegida).

   La sección **Claves de API** ahora muestra sus claves de API (públicas). Necesita las cuatro claves (tanto la de producción como la de zona protegida, Pública+Privada) al [seleccionar o crear un proyecto SaaS](#createsaasenv) en cualquiera de los entornos o instalaciones asociados con la licencia.

## Configuración de SaaS {#saasenv}

Las instancias de [!DNL Commerce] deben configurarse con un proyecto SaaS y un espacio de datos SaaS para que [!DNL Commerce Services] pueda enviar datos a la ubicación correcta. Un proyecto SaaS agrupa todos los espacios de datos SaaS. Los espacios de datos SaaS se utilizan para recopilar y almacenar datos que permiten que [!DNL Commerce Services] funcione. Algunos de estos datos pueden exportarse desde la instancia [!DNL Commerce] y otros pueden recopilarse a partir del comportamiento del comprador en la tienda. Estos datos se conservan para proteger el almacenamiento en la nube.

Para [!DNL Product Recommendations], el espacio de datos de SaaS contiene datos de catálogo y de comportamiento. Puede apuntar una instancia de [!DNL Commerce] a un espacio de datos SaaS [seleccionándola](https://experienceleague.adobe.com/en/docs/commerce-admin/config/services/saas) en la configuración de [!DNL Commerce].

>[!WARNING]
>
> Use su **espacio de datos SaaS de producción** solo en su instalación de producción [!DNL Commerce] para evitar conflictos de datos. De lo contrario, se corre el riesgo de contaminar los datos del sitio de producción con datos de prueba, lo que provoca retrasos en la implementación. Por ejemplo, los datos del producto de producción se podrían sobrescribir por error a partir de los datos de ensayo, como las direcciones URL de ensayo.
> Si esto sucede, [envíe una solicitud de soporte técnico](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/overview) para solicitar la limpieza de datos.

### Aprovisionamiento de espacio de datos SaaS

All Adobe Commerce merchants can access one production data space and two testing data spaces per SaaS project.

Puede utilizar los espacios de datos de prueba en cualquier entorno que no sea de producción, siempre que no utilice el mismo espacio de datos en varios entornos al mismo tiempo. Para utilizar el espacio de datos de prueba en un entorno diferente, realice una limpieza de datos antes de seleccionar y configurar el espacio de datos en ese entorno.

Para los proyectos de Adobe Commerce Cloud Pro con varios entornos de ensayo, puede solicitar espacios de datos de prueba adicionales para cada entorno de ensayo [enviando una solicitud de asistencia](https://experienceleague.adobe.com/home?support-tab=home#support). Sin embargo, si solo tiene un entorno de ensayo y necesita espacios de datos de prueba adicionales, tiene las siguientes opciones:
- Póngase en contacto con el equipo de éxito del cliente o con el administrador de éxito del cliente designado para solicitar un entorno de ensayo adicional.
- [Envíe una solicitud de soporte técnico](https://experienceleague.adobe.com/home?support-tab=home#support) para solicitar el espacio de datos de prueba adicional e indicar la justificación comercial del espacio de datos adicional. Esta solicitud está sujeta a aprobación.

Magento Open Source customers using Adobe Payment Services may also request an additional data space. Contact the Payments team for prior approval of the additional data spaces before submitting a [Support request](https://experienceleague.adobe.com/home?support-tab=home#support) to request the testing data space.

Customers who own multiple Cloud projects or on-premises (live/production) installations can also request additional production and testing data spaces for each project or instance by [submitting a Support request](https://experienceleague.adobe.com/home?support-tab=home#support).

### Select or create a SaaS project {#createsaasenv}

To select or create a SaaS project, request the [!DNL Commerce] API key from the [!DNL Commerce] license owner for your store:

>[!NOTE]
>
> If you do not see the **[!UICONTROL Commerce Services Connector]** section in the [!DNL Commerce] configuration, you must install the [!DNL Commerce] modules for your desired [[!DNL Commerce] service](#availableservices).

1. On the _Admin_ sidebar, go to **System** > Services > **Commerce Services Connector**.

   If you do not see the **[!UICONTROL Commerce Services Connector]** section in the [!DNL Commerce] configuration, install the [!DNL Commerce] modules for your desired [[!DNL Commerce] service](#availableservices). Also, make sure that the `magento/module-services-id` package is installed.

1. In the _[!UICONTROL Sandbox API Keys]_and_[!UICONTROL Production API Keys]_ sections, paste your key values.

   - Private keys must include `----BEGIN PRIVATE KEY---` at the beginning of the key and `----END PRIVATE KEY----` at the end of the key.
   - If you do not have a copy of the actual keys, ask the Account Owner for them, then plug the values into the configuration.

   >[!WARNING]
   >
   > Si agrega valores de clave consultando una copia de seguridad o instantánea de base de datos y pegando los valores en la configuración, se aplica una capa adicional de cifrado y las claves no funcionan.

1. Haga clic en **Guardar**.

Cualquier proyecto SaaS asociado con sus claves aparecerá en el campo **Proyecto** de la sección **Identificador SaaS**.

1. Si no existen proyectos SaaS, haga clic en **Crear proyecto**. A continuación, en el campo **Proyecto**, escriba un nombre para su proyecto SaaS.

>[!NOTE]
>
>Para evitar confusiones, no use un servicio Commerce específico como nombre para el proyecto, por ejemplo *Live Search*, *Product Recommendations* o *Conexión de datos*.  A menos que la licencia se haya aprovisionado para varios proyectos SaaS, puede utilizar el mismo proyecto SaaS para varios servicios.

1. Seleccione el **espacio de datos** que se usará para la configuración actual de su almacén de [!DNL Commerce].

>[!NOTE]
>
>Si tiene instancias independientes para integrar con los servicios de Commerce, [envíe un vale de soporte técnico](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#submit-ticket) para solicitar un nuevo proyecto de SaaS para cada instancia adicional. Una vez que el equipo de asistencia haya creado el proyecto de SaaS, configure la integración de servicios de Commerce para la instancia de con la misma clave de API y seleccione el nuevo proyecto de SaaS para el espacio de datos.

>[!WARNING]
>
> Si genera claves nuevas en la sección del portal de API de Mi cuenta, actualice inmediatamente las claves de API en la configuración de la administración. Si genera claves nuevas y no las actualiza en el Administrador, las extensiones SaaS dejarán de funcionar y perderá datos valiosos.

Para cambiar los nombres de tu proyecto SaaS o espacio de datos, haz clic en **Cambiar nombre** junto a uno de ellos. Cambiar el nombre no afecta al servicio porque el nombre es sólo una etiqueta para ayudarle a identificar y diferenciar entre proyectos y espacios de datos.

## Organización de IMS (opcional) {#organizationid}

Para conectar la instancia de Adobe Commerce a Adobe Experience Platform, inicie sesión en la cuenta de Adobe con el Adobe ID. Después de iniciar sesión, la organización de IMS asociada a su cuenta de Adobe se muestra en esta sección.

## Exportación de datos SaaS

Cuando la instancia de [!DNL Commerce] se conecta correctamente a [!DNL Commerce Services], el proceso de exportación de datos de SaaS exporta los datos de Commerce del servidor [!DNL Commerce] a [!DNL Commerce SaaS Services] para que se puedan sincronizar con los servicios de Commerce conectados. En el Administrador, puede comprobar el estado de sincronización mediante el [panel de administración de datos](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard). Para obtener más información, consulte la [Guía de exportación de datos SaaS](../data-export/overview.md).
