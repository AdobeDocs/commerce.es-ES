---
title: Administración de usuarios
description: Obtenga información sobre cómo administrar usuarios en  [!DNL Adobe Commerce Optimizer].
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
source-git-commit: 1427db02c65fd45777f69eac3d10417d6e6177a1
workflow-type: tm+mt
source-wordcount: '508'
ht-degree: 0%

---

# Administración de usuarios

>[!NOTE]
>
>Esta documentación de administración de usuarios está destinada a los participantes con acceso anticipado e instrucciones de incorporación para administrar y aprovisionar a los usuarios de [!DNL Adobe Commerce Optimizer] dentro de su organización de Adobe. Si no tiene estas instrucciones, póngase en contacto con el representante de la cuenta para obtener ayuda con la administración de usuarios. Durante el programa de acceso anticipado, el aprovisionamiento de usuarios para [!DNL Adobe Commerce Optimizer] se administra asignando usuarios a la solución de producto **[!UICONTROL Adobe Commerce as a Cloud Service - backend]**.

Para habilitar el acceso a [!DNL Adobe Commerce Optimizer], agregue usuarios de [Adobe Admin Console](https://adminconsole.adobe.com){target="_blank"} y asegúrese de que tengan acceso al producto de Commerce.

Puede asignar usuarios a cualquiera de las siguientes funciones:

* **Usuario**: los usuarios tienen acceso a la interfaz de usuario de [!DNL Adobe Commerce Optimizer] para ver y administrar vistas de catálogo y reglas de comercialización, así como para realizar un seguimiento de las métricas de rendimiento.

* [**Desarrollador**](https://helpx.adobe.com/enterprise/using/manage-developers.html#Adddevelopers){target="_blank"} Los desarrolladores tienen permisos de usuario y acceso a Adobe Developer Console. Esto significa que pueden crear proyectos y configurar credenciales para utilizar herramientas para desarrolladores como las API y SDK de [!DNL Adobe Commerce Optimizer], así como herramientas de extensibilidad de Adobe como App Builder y API Mesh.

* **Administrador** - Existen tres tipos diferentes de roles de administrador:
   * [Administradores del sistema](https://helpx.adobe.com/enterprise/using/admin-roles.html){target="_blank"}: el administrador del sistema tiene acceso a todos los productos y perfiles de producto de la organización a través de Adobe Admin Console.
   * [Administradores de productos](#add-a-product-admin): los administradores de productos pueden [administrar usuarios, roles y permisos para el producto](#add-users-and-admins) en [!DNL Adobe Admin Console].
   * [Administradores de perfil de producto](#add-users-developers-and-product-profile-admins): los administradores de perfil de producto pueden administrar usuarios para el producto en [!DNL Adobe Admin Console].

## Añadir un administrador de productos

1. Vaya a [Admin Console](https://adminconsole.adobe.com) e inicie sesión con su Adobe ID.

1. Seleccione su organización.

1. En la ficha [!UICONTROL **Productos**], en [!UICONTROL **Productos y servicios**], seleccione el producto [!UICONTROL **Adobe Commerce as a Cloud Service - servidor**].

   ![seleccionar producto](../cloud-service/assets/backend.png){width="600" zoomable="yes"}

1. Seleccione la ficha [!UICONTROL **Administradores**].

1. Haga clic en [!UICONTROL **Agregar administrador**].

1. Escriba el nombre de usuario o la dirección de correo electrónico de los usuarios que quiere agregar como administradores y haga clic en [!UICONTROL **Guardar**].

## Adición de usuarios, desarrolladores y administradores de perfil de producto

>[!BEGINSHADEBOX &quot;Requisitos previos&quot;]
>
Se requiere el siguiente aprovisionamiento para la administración de usuarios:

* Organización de IMS aprovisionada para [!DNL Adobe Commerce Optimizer]
* Una cuenta de Adobe Experience Cloud en la misma organización de IMS con la función de administrador de sistemas o productos

>[!ENDSHADEBOX]

Siga estas instrucciones para agregar usuarios y desarrolladores a [!DNL Commerce Cloud Manager], donde administra las instancias de Commerce.

1. Vaya a https://adminconsole.adobe.com e inicie sesión con su Adobe ID.

1. Seleccione su organización.

1. En la ficha [!UICONTROL **Productos**], en [!UICONTROL **Productos y servicios**], seleccione el producto [!UICONTROL **Adobe Commerce as a Cloud Service - servidor**].

   ![seleccionar producto](../cloud-service/assets/backend.png){width="600" zoomable="yes"}

1. Haga clic en el perfil de producto [!UICONTROL **Predeterminado - Cloud Manager**].

1. Seleccione la ficha [!UICONTROL **Usuarios**], [!UICONTROL **Desarrolladores**] o [!UICONTROL **Administradores**] y haga clic en [!UICONTROL **Agregar usuarios**] o [!UICONTROL **Agregar desarrolladores**] o [!UICONTROL **Agregar administradores**].

   Los administradores agregados desde esta pantalla se asignan al grupo [administradores de perfil de producto](#understanding-roles).

   ![selección de ficha](../cloud-service/assets/tab-select.png){width=600 zoomable="yes"}

1. Escriba el nombre de usuario o la dirección de correo electrónico de los usuarios que quiere agregar como administradores y haga clic en [!UICONTROL **Guardar**].

## Administración de usuarios en masa

Puede agregar varios usuarios de forma más eficaz mediante uno de los métodos siguientes:

* Use la función **Agregar usuarios mediante CSV** en Adobe Admin Console para realizar una [carga CSV en lotes](https://helpx.adobe.com/enterprise/using/bulk-upload-users.html){target="_blank"}.
* Agregue varios usuarios a una función creando un [grupo de usuarios](https://helpx.adobe.com/enterprise/using/user-groups.html){target="_blank"}. A continuación, agregue el producto [!UICONTROL **Adobe Commerce as a Cloud Service - servidor**] al grupo de usuarios.

