---
title: Administración de usuarios
description: Obtenga información sobre cómo administrar usuarios en  [!DNL Adobe Commerce as a Cloud Service].
exl-id: 9bc80fe6-6dfd-4bb3-8dc5-d5efd8a8d90c
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
role: Admin
source-git-commit: 00d31ca7e4e81ecbc34373ce95b1256a7ae012db
workflow-type: tm+mt
source-wordcount: '1225'
ht-degree: 0%

---

# Administración de usuarios

Si desea que los usuarios tengan acceso al administrador en [!DNL Adobe Commerce as a Cloud Service], debe agregarlos como usuarios de su organización y asegurarse de que tengan acceso al producto Cloud Service en [Adobe Admin Console](https://adminconsole.adobe.com){target="_blank"}.

Este proceso requiere una organización de IMS con acceso a [!DNL Adobe Commerce as a Cloud Service]. Solo un administrador del sistema o de producto de la organización puede realizar estos procesos.

>[!TIP]
>
>Para agregar varios usuarios simultáneamente, puede realizar una [carga CSV en lotes](https://helpx.adobe.com/es/enterprise/using/bulk-upload-users.html){target="_blank"}.
> 
> También puede agregar varios usuarios a un rol creando un [grupo de usuarios](https://helpx.adobe.com/es/enterprise/using/user-groups.html){target="_blank"}. A continuación, puede agregar el producto [!UICONTROL **Adobe Commerce - Commerce Cloud Manager**] al grupo de usuarios.

## Explicación de funciones

Los roles siguientes están disponibles para [!DNL Adobe Commerce as a Cloud Service]. Para ver o editar estos roles, en el Administrador de Commerce, vaya a **Sistema** > **Permisos** > **Roles de usuario**.

* **Usuarios**: los usuarios tienen acceso de administrador al administrador de Commerce, pero no pueden administrar el acceso de nivel de producto en Admin Console. Los usuarios también pueden usar créditos para [crear instancias](./getting-started.md#create-an-instance) en [!DNL Commerce Cloud Manager].

  >[!NOTE]
  >
  >Todos los usuarios de Commerce, incluidos los desarrolladores y administradores, también deben tener asignada la función Usuario. Es necesario para los permisos básicos de Commerce.

* [**Desarrolladores**](https://helpx.adobe.com/es/enterprise/using/manage-developers.html#Adddevelopers){target="_blank"} Los desarrolladores tienen permisos de usuario y se agregan a la instancia de Commerce como usuario desarrollador. Esto significa que pueden usar [Admin UI SDK](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/){target="_blank"}, [configurar eventos](https://developer.adobe.com/commerce/extensibility/events/){target="_blank"} y [crear enlaces web](https://developer.adobe.com/commerce/extensibility/webhooks/){target="_blank"}.

* Administradores: existen tres tipos diferentes de administradores:
   * [Administradores del sistema](https://helpx.adobe.com/es/enterprise/using/admin-roles.html){target="_blank"}: el administrador del sistema tiene acceso a todos los productos y perfiles de producto de la organización a través de Admin Console.
   * [Administradores de productos](#add-a-product-admin): los administradores de productos pueden [administrar usuarios, roles y permisos para el producto](#add-users) en [!DNL Adobe Admin Console] y [administrar usuarios en el administrador de Commerce](https://experienceleague.adobe.com/es/docs/commerce-admin/systems/user-accounts/permissions-users-all#create-a-user){target="_blank"}.
   * [Administradores de perfil de producto](#add-developers-and-product-profile-admins): los administradores de perfil de producto no tienen acceso al Administrador de Adobe Commerce, pero pueden administrar usuarios para el producto en [!DNL Adobe Admin Console].

Para obtener información detallada sobre los permisos otorgados a cada función dentro de Adobe Commerce, consulte [permisos de usuario](#user-permissions).

## Añadir un administrador de productos

>[!NOTE]
>
>Asigne a los administradores de productos la [función de usuario](#add-users) antes de agregarlos como administradores de productos. La función Usuario es necesaria para los permisos básicos de Commerce.

1. Vaya a https://adminconsole.adobe.com e inicie sesión con su Adobe ID.

1. Seleccione su organización.

1. En la ficha [!UICONTROL **Productos**], en [!UICONTROL **Productos y servicios**], seleccione el producto [!UICONTROL **Adobe Commerce - Commerce Cloud Manager**].

   ![seleccionar producto](./assets/backend.png){width="600" zoomable="yes"}

1. Seleccione la ficha [!UICONTROL **Administradores**].

1. Haga clic en [!UICONTROL **Agregar administrador**].

1. Escriba el nombre de usuario o la dirección de correo electrónico de los usuarios que quiere agregar como administradores y haga clic en [!UICONTROL **Guardar**].

## Adición de usuarios

Las siguientes instrucciones proporcionan información sobre cómo agregar usuarios a [!DNL Commerce Cloud Manager] y al administrador de Commerce. La interfaz [!DNL Commerce Cloud Manager] le permite crear y administrar sus instancias de Commerce. Este proceso es necesario para todos los usuarios, incluidos desarrolladores y administradores.

>[!NOTE]
>
>Solo los administradores de productos y de sistemas pueden agregar usuarios y desarrolladores al producto Adobe Commerce as a Cloud Service.

1. Vaya a https://adminconsole.adobe.com e inicie sesión con su Adobe ID.

1. Seleccione su organización.

1. En la ficha [!UICONTROL **Productos**], en [!UICONTROL **Productos y servicios**], seleccione el producto [!UICONTROL **Adobe Commerce - Commerce Cloud Manager**].

   ![seleccionar producto](./assets/backend.png){width="600" zoomable="yes"}

1. Haga clic en el perfil de producto [!UICONTROL **Predeterminado - Cloud Manager**].

1. Seleccione la ficha [!UICONTROL **Usuarios**] y haga clic en [!UICONTROL **Agregar usuarios**].

   ![selección de ficha](./assets/tab-select.png){width=600 zoomable="yes"}

1. Escriba el nombre de usuario o la dirección de correo electrónico de los usuarios que quiere agregar como administradores y haga clic en [!UICONTROL **Guardar**].

### Adición de desarrolladores y administradores de perfil de producto

Para agregar desarrolladores y administradores de perfiles de producto, repita el proceso [agregar usuarios](#add-users), pero seleccione la ficha [!UICONTROL **Desarrolladores**] o [!UICONTROL **Administradores**] en lugar de la ficha [!UICONTROL **Usuarios**].

>[!NOTE]
>
>Los administradores de perfil de producto no tienen acceso al administrador de Commerce. Consulte [Explicación de funciones](#understanding-roles) para obtener más información.
>
>Asigne a los desarrolladores la función Usuario antes de agregarlos como desarrolladores. La función Usuario es necesaria para los permisos básicos de Commerce.

![selección de ficha](./assets/tab-select.png){width=600 zoomable="yes"}

## Recursos de roles

En la lista siguiente se describen los recursos a los que los roles predeterminados tienen permiso para acceder dentro del administrador de Adobe Commerce. Para editar los permisos predeterminados de cada función, vaya a **Sistema** > **Permisos** > **Roles de usuario** en el administrador de Commerce.

**Usuarios**

* Catálogo
   * Inventario
      * Productos
         * Leer precio del producto

**Desarrolladores**

* Catálogo
   * Inventario
      * Productos
         * Leer precio del producto
* Sistema
   * Transferencia de datos
      * Importar historial
* Configuración de eventos de Adobe IO
   * Comprobación de configuración
   * Crear proveedor de eventos
   * Actualización de configuración
   * Sincronización de eventos
   * Obtener lista de proveedores de eventos
* Marco de eventos
   * Lista de eventos
   * Probar conexión de evento
   * Suscripción a un evento
   * Cancelar la suscripción a un evento
   * Estado del evento
   * API para obtener suscripciones a eventos
   * Ver IU de administración de suscripciones a eventos
   * IU de administración Crear suscripciones a eventos
   * Solicitar nueva IU de administración de eventos
* Webhooks
   * Firma digital de webhooks
      * Configuración de firma digital de Webhooks
      * Firma digital Generar claves
   * Administración de webhooks
      * Cuadrícula de webhooks
      * Edición de webhooks
      * Probar webhooks
      * Suscripción de API al webhook
      * Cancelar suscripción a API desde webhook
      * Lista de webhooks
      * Solicitar nuevo webhook
      * Registros de webhooks
      * Obtener lista de webhooks

**Administradores**

Los administradores tienen acceso a todos los permisos.

## Agregar un usuario a AEM Assets o a Imágenes de producto

Se requiere la siguiente configuración para [!DNL Adobe Experience Manager Assets] y [!DNL Product Visuals powered by AEM Assets] usuarios.

Si su cuenta tiene acceso a [Adobe Experience Manager as a Cloud Service](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service) y desea permitir que un usuario tenga acceso a las características avanzadas de [AEM Assets](https://experienceleague.adobe.com/es/docs/commerce/aem-assets-integration/overview){target="_blank"} junto con [!DNL Adobe Commerce as a Cloud Service], siga este proceso:

>[!NOTE]
>
>Los usuarios sin los permisos de recursos apropiados no podrán obtener acceso a las características avanzadas de [!DNL AEM Assets], como [generación de imágenes de IA](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/generative-ai/generative-ai-in-aem){target="_blank"}, [variaciones generadas](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/generative-ai/generate-variations-integrated-editor){target="_blank"} y más.

>[!TIP]
>
>Para agregar varios usuarios simultáneamente, puede realizar una [carga CSV en lotes](https://helpx.adobe.com/es/enterprise/using/bulk-upload-users.html){target="_blank"}.
>
>También puede agregar varios usuarios a un rol creando un [grupo de usuarios](https://helpx.adobe.com/es/enterprise/using/user-groups.html){target="_blank"}. A continuación, puede agregar el producto [!UICONTROL **Adobe Experience Manager as a Cloud Service - Cloud Manager**] al grupo de usuarios.

1. Vaya a https://adminconsole.adobe.com e inicie sesión con su Adobe ID.

1. Seleccione su organización.

1. En la ficha [!UICONTROL **Productos**], en [!UICONTROL **Productos y servicios**], seleccione el producto [!UICONTROL **Adobe Experience Manager as a Cloud Service - Cloud Manager**].

   ![seleccionar producto](./assets/backend-aem.png){width="600" zoomable="yes"}

1. Seleccione la ficha [!UICONTROL **Usuarios**].

1. Haga clic en [!UICONTROL **Agregar usuario**].

1. Introduzca el nombre de usuario o la dirección de correo electrónico de los usuarios que desea agregar.

1. Haga clic en [!UICONTROL **Agregar producto**].

1. Seleccione los siguientes perfiles de producto, que son necesarios para integrar AEM Assets con Commerce:

   * Propietario empresarial: necesario para crear y administrar programas.
   * Administrador de implementación: necesario para implementar código de sus repositorios en AEM.

   Si agrega un desarrollador que no necesita acceder a las interfaces de Cloud Manager o Experience Manager, puede asignarle la función de desarrollador.

   >[!NOTE]
   >
   >Para obtener más información sobre cómo estos permisos afectan el acceso a los AEM Assets, consulte [Perfiles de productos de Cloud Manager](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/onboarding/concepts/aem-cs-team-product-profiles#cloud-manager-product-profiles){target="_blank"}.

1. Haga clic en [!UICONTROL **Aplicar**].

1. Haga clic en [!UICONTROL **Guardar**].

Para confirmar que el usuario tiene acceso, haga clic en el nombre del usuario para abrir su página de perfil. En la sección [!UICONTROL **Productos**] debería decir [!UICONTROL **Completados**] bajo el producto [!UICONTROL **Adobe Experience Manager as a Cloud Service - Cloud Manager**]. Puede tardar unos segundos después de agregar el usuario en ver el estado actualizado en su perfil. Actualice la página para ver el estado actualizado.

![acceso al producto](./assets/product-access.png){width="600" zoomable="yes"}

## Acceso a la interfaz de Experience Manager

Después de agregar un usuario a los AEM Assets, pueden obtener acceso a la interfaz [!DNL Experience Manager] si navegan a [https://experience.adobe.com/](https://experience.adobe.com/){target="_blank"}.

1. En la sección [!UICONTROL **Acceso rápido**], haz clic en [!UICONTROL **Experience Manager**] o en [!UICONTROL **Ver todo**] si no ves [!UICONTROL **Experience Manager**]. A continuación, haga clic en [!UICONTROL **Cloud Manager**] o vaya directamente a [https://my.cloudmanager.adobe.com](https://my.cloudmanager.adobe.com){target="_blank"}.

1. En la página [!UICONTROL **Cloud Manager**], haga clic en [!UICONTROL **Agregar programa**] para comenzar.

1. [Crear un nuevo programa](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/onboarding/journey/create-program){target="_blank"}.

1. [Crear un nuevo entorno](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/screens-as-cloud-service/onboarding-screens-cloud/creating-an-environment){target="_blank"}.

1. Después de crear el entorno, vuelve a [Admin Console](https://adminconsole.adobe.com){target="_blank"} y selecciona [!UICONTROL **Adobe Experience Manager as a Cloud Service**].

1. Ahora debería ver perfiles de producto nuevos. Seleccione que contiene `- author -`. Por ejemplo, `<environment-name> - author - <program-id> - <environment-id>`.

1. [Agregar usuarios al perfil del producto](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-manager/content/requirements/users-and-roles){target="_blank"}.

* [Configuración de AEM Assets para admitir metadatos de Commerce](https://experienceleague.adobe.com/es/docs/commerce/aem-assets-integration/get-started/configure-aem)
* [Integrar AEM Assets con Commerce para la sincronización de recursos](https://experienceleague.adobe.com/es/docs/commerce/aem-assets-integration/get-started/setup-synchronization)
