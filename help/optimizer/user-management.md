---
title: Usuario y Identity Management
description: Obtenga información sobre cómo crear y administrar usuarios, y asignar funciones de usuario para  [!DNL Adobe Commerce Optimizer].
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
exl-id: 9ab2118d-b7e3-4e2e-adac-8f3950fe1824
source-git-commit: b88406169191cb9d4f0d2b5ef113703f5afcd589
workflow-type: tm+mt
source-wordcount: '704'
ht-degree: 0%

---

# Administración de usuarios

Para habilitar el acceso a [!DNL Adobe Commerce Optimizer], agregue usuarios de [Adobe Admin Console](https://adminconsole.adobe.com){target="_blank"} y asegúrese de que tengan acceso al producto de Commerce.

Puede asignar usuarios a cualquiera de las siguientes funciones:

- **Usuario**: los usuarios tienen acceso a la interfaz de usuario de [!DNL Adobe Commerce Optimizer] para ver y administrar vistas de catálogo y reglas de comercialización, así como para realizar un seguimiento de las métricas de rendimiento.

- [**Desarrollador**](https://helpx.adobe.com/es/enterprise/using/manage-developers.html#Adddevelopers){target="_blank"}— Los desarrolladores tienen permisos de usuario y acceso a Adobe Developer Console. Esto significa que pueden crear proyectos y configurar credenciales para utilizar herramientas para desarrolladores como las API y SDK de [!DNL Adobe Commerce Optimizer], así como herramientas de extensibilidad de Adobe como App Builder y API Mesh.

- **Administrador** - Existen tres tipos diferentes de roles de administrador:
   - [Administradores del sistema](https://helpx.adobe.com/es/enterprise/using/admin-roles.html){target="_blank"}: el administrador del sistema tiene acceso a todos los productos y perfiles de producto de la organización a través de Adobe Admin Console.
   - [Administradores de productos](#add-a-product-admin): los administradores de productos pueden [administrar usuarios, roles y permisos para el producto](#add-users-and-admins) en [!DNL Adobe Admin Console].
   - [Administradores de perfil de producto](#add-users-developers-and-product-profile-admins): los administradores de perfil de producto pueden administrar usuarios para el producto en [!DNL Adobe Admin Console].

## Añadir un administrador de productos

>[!BEGINTABS]

>[!NOTE]
>
>Asigne a los administradores de productos la [función de usuario](#add-users) antes de agregarlos como administradores de productos. La función Usuario es necesaria para los permisos básicos de Commerce.

>[!TAB GA (aprovisionado después del 13 de octubre de 2025)]

1. Vaya a <https://adminconsole.adobe.com> e inicie sesión con su Adobe ID.

1. Seleccione su organización.

1. Seleccione la ficha [!UICONTROL **Usuarios**].

1. Seleccione la ficha [!UICONTROL **Administradores**].

1. Haga clic en [!UICONTROL **Agregar administrador**].

1. Escriba el nombre de usuario o la dirección de correo electrónico de los usuarios que desea agregar como administradores y haga clic en [!UICONTROL **Siguiente**].

1. Seleccione el rol [!UICONTROL **Administrador del perfil de producto**].

1. Haga clic en **+** para agregar productos.

1. Seleccione la instancia de Commerce Optimizer existente a la que desee agregar al administrador. Las instancias de Commerce Optimizer utilizan el siguiente formato: `Adobe Commerce - <instance-name> - ACO - <environment-type> - <tenant-id>`.

1. Seleccione el perfil de producto.

1. Haga clic en [!UICONTROL **Aplicar**].

1. Haga clic en [!UICONTROL **Guardar**].

>[!TAB Acceso anticipado (aprovisionado antes del 13 de octubre de 2025)]

1. Vaya a <https://adminconsole.adobe.com> e inicie sesión con su Adobe ID.

1. Seleccione su organización.

1. En la ficha [!UICONTROL **Productos**], en [!UICONTROL **Productos y servicios**], seleccione el producto [!UICONTROL **Adobe Commerce - Commerce Cloud Manager**].

   ![seleccionar producto](/help/cloud-service/assets/backend.png){width="600" zoomable="yes"}

1. Seleccione la ficha [!UICONTROL **Administradores**].

1. Haga clic en [!UICONTROL **Agregar administrador**].

1. Escriba el nombre de usuario o la dirección de correo electrónico de los usuarios que quiere agregar como administradores y haga clic en [!UICONTROL **Guardar**].

>[!ENDTABS]

## Adición de usuarios

Las siguientes instrucciones proporcionan información sobre cómo agregar usuarios a [!DNL Commerce Cloud Manager] y Commerce Optimizer. La interfaz [!DNL Commerce Cloud Manager] le permite crear y administrar las instancias de Commerce Optimizer. Este proceso es necesario para todos los usuarios, incluidos desarrolladores y administradores.

>[!NOTE]
>
>Solo los administradores de productos y de sistemas pueden agregar usuarios y desarrolladores al producto de Adobe Commerce Optimizer.

>[!BEGINTABS]

>[!TAB GA (aprovisionado después del 13 de octubre de 2025)]

1. Vaya a <https://adminconsole.adobe.com> e inicie sesión con su Adobe ID.

1. Seleccione su organización.

1. Seleccione la ficha [!UICONTROL **Productos**].

1. Seleccione el producto [!UICONTROL **Adobe Commerce**].

1. Seleccione el producto Commerce Cloud Manager si desea agregar el usuario a la interfaz de Cloud Manager, donde puede crear y administrar instancias de Commerce Optimizer, o bien seleccione la instancia de Commerce Optimizer existente a la que desea agregar el usuario. Las instancias de Commerce Optimizer utilizan el siguiente formato: `Adobe Commerce - <instance-name> - ACO - <environment-type> - <tenant-id>`.

1. Seleccione la ficha [!UICONTROL **Usuarios**] y haga clic en [!UICONTROL **Agregar usuarios**].

1. Escriba el nombre de usuario o la dirección de correo electrónico de los usuarios que desea agregar y haga clic en [!UICONTROL **Guardar**].

1. Seleccione el perfil de producto deseado.

1. Haga clic en [!UICONTROL **Aplicar**].

1. Haga clic en [!UICONTROL **Guardar**].

>[!TAB Acceso anticipado (aprovisionado antes del 13 de octubre de 2025)]

1. Vaya a <https://adminconsole.adobe.com> e inicie sesión con su Adobe ID.

1. Seleccione su organización.

1. En la ficha [!UICONTROL **Productos**], en [!UICONTROL **Productos y servicios**], seleccione el producto [!UICONTROL **Adobe Commerce - Commerce Cloud Manager**].

   ![seleccionar producto](/help/cloud-service//assets/backend.png){width="600" zoomable="yes"}

1. Haga clic en el perfil de producto [!UICONTROL **Predeterminado - Cloud Manager**].

1. Seleccione la ficha [!UICONTROL **Usuarios**] y haga clic en [!UICONTROL **Agregar usuarios**].

   ![selección de ficha](/help/cloud-service/assets/tab-select.png){width=600 zoomable="yes"}

1. Escriba el nombre de usuario o la dirección de correo electrónico de los usuarios que desea agregar y haga clic en [!UICONTROL **Guardar**].

>[!ENDTABS]

### Adición de desarrolladores y administradores de perfil de producto

Para agregar desarrolladores y administradores de perfiles de producto, repita el proceso [agregar usuarios](#add-users), pero seleccione la ficha [!UICONTROL **Desarrolladores**] o [!UICONTROL **Administradores**] en lugar de la ficha [!UICONTROL **Usuarios**].

>[!NOTE]
>
>Asigne a los desarrolladores la función Usuario antes de agregarlos como desarrolladores. La función Usuario es necesaria para los permisos básicos de Commerce.

![selección de ficha](/help//cloud-service/assets/tab-select.png){width=600 zoomable="yes"}

## Administración de usuarios en masa

Puede agregar varios usuarios de forma más eficaz mediante uno de los métodos siguientes:

- Use la función **Agregar usuarios mediante CSV** en Adobe Admin Console para realizar una [carga CSV en lotes](https://helpx.adobe.com/es/enterprise/using/bulk-upload-users.html){target="_blank"}.
- Agregue varios usuarios a una función creando un [grupo de usuarios](https://helpx.adobe.com/es/enterprise/using/user-groups.html){target="_blank"}. A continuación, agregue el producto [!UICONTROL **Adobe Commerce - Commerce Cloud Manager**] al grupo de usuarios.

## Administración de identidades y configuración de inicio de sesión único

{{ims-identity-and-sso-config}}
