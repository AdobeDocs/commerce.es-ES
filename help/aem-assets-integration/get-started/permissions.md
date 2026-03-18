---
title: Configuración de permisos de usuario de IMS para la integración de AEM Assets
description: Descubra cómo los perfiles de identidad de IMS y Admin Console habilitan el acceso a la entrega de los AEM Assets, el Selector de recursos y los campos de configuración de Commerce rellenados automáticamente.
feature: CMS, Media, Configuration
source-git-commit: 0fd98bf86555c914f7a5b1e177c31c37764dbf84
workflow-type: tm+mt
source-wordcount: '860'
ht-degree: 0%

---

# Permisos de usuario e IMS

**IMS** (Adobe Identity Management System) es la capa de autenticación. Para Adobe Commerce as a Cloud Service, la autenticación IMS está habilitada de forma predeterminada en Admin. Para Adobe Commerce en la nube o local, IMS es opcional;[Al habilitar IMS para Commerce](https://experienceleague.adobe.com/docs/commerce-admin/start/admin/ims/adobe-ims-config.html?lang=es){target=_blank} se proporciona una interfaz de usuario de configuración mejorada (Selector de recursos, listas desplegables rellenadas automáticamente), pero puede configurar la integración sin IMS introduciendo manualmente **ID de programa** e **ID de entorno**.

La integración de AEM Assets también requiere **perfiles de producto de Adobe Admin Console** específicos al usar IMS. Los usuarios que configuran la integración en Commerce Admin necesitan el perfil de producto **Usuarios de DM OpenAPI AEM Assets - entrega** o el perfil de producto **autor** como reserva. Esto se controla mediante perfiles de producto de Admin Console en la organización IMS del usuario y permite:

* **Selector de recursos** permite seleccionar imágenes de AEM Assets al administrar imágenes de categoría o contenido de Page Builder.
* **Campos de configuración rellenados automáticamente** como **ID de programa**, **ID de entorno** y **asignaciones de dominio** desplegables que extraen valores de la sesión IMS del usuario según sus perfiles de producto de Admin Console (envío o autor).

Sin los permisos correctos, el Selector de recursos no está disponible y estos campos aparecen vacíos o requieren una entrada manual.
>[!BEGINSHADEBOX]

**Cómo funcionan juntos IMS y los permisos**

Adobe IMS proporciona la identidad del usuario y el contexto de la organización, mientras que Adobe Admin Console define qué **perfiles de producto**(permisos) tiene. La integración de AEM Assets utiliza los detalles de IMS más el perfil asignado para determinar si puede rellenar automáticamente los campos de configuración y habilitar el selector de recursos.

>[!ENDSHADEBOX]

## Por qué se requieren perfiles de producto

La integración solo puede cargar dominios asignados a un perfil. Por lo tanto, los usuarios pueden tener los siguientes perfiles de producto:

* **Perfil del producto de entrega de AEM**. Necesario para el Selector de recursos y la IU de configuración cuando el usuario tiene perfiles de autor y de envío. La integración utiliza el perfil de producto de entrega de AEM cuando está disponible.

* **Perfil del producto del autor**. Necesario para acceder a la interfaz de usuario de AEM Assets. También sirve como alternativa para el Selector de recursos y la IU de configuración cuando el usuario no tiene el perfil de producto de entrega de AEM en su Admin Console.

Los dominios (incluidos el ID de programa, el ID de entorno y la asignación de dominios) se asignan al perfil de producto de entrega de AEM. La integración carga los dominios del **perfil del producto de envío de AEM** cuando está disponible, o vuelve al **perfil del producto de autor** cuando el perfil del producto de envío de AEM no está en el Admin Console del usuario. Los usuarios necesitan uno de estos perfiles para:

* Rellene los menús desplegables **ID de programa**, **ID de entorno** y **Asignación de dominio** en la configuración de administración de Commerce.
* Utilice el Selector de recursos para examinar y seleccionar recursos de los AEM Assets.

Si ninguno de los perfiles está configurado, los usuarios pueden escribir manualmente **Id. de programa** e **Id. de entorno**, pero el Selector de recursos no estará disponible.

## Conceder permisos por tipo de implementación

>[!BEGINTABS]

>[!TAB Adobe Commerce as a Cloud Service]

[!BADGE Solo SaaS]{type=Positive tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."}

La autenticación IMS está habilitada de forma predeterminada. Agregue el usuario al perfil de producto **Usuarios de OpenAPI de DM AEM Assets - delivery** en el perfil de producto [Adobe Admin Console](https://adminconsole.adobe.com/), o al perfil de producto **author** (por ejemplo, `<environment-name> - author - <program-id> - <environment-id>`) como reserva cuando el usuario no tenga el perfil de producto de AEM delivery en su Admin Console.

>[!NOTE]
>
> Los usuarios también deben añadirse a Commerce y a los AEM Assets. Consulte [Agregar un usuario a AEM Assets o a elementos visuales del producto](https://experienceleague.adobe.com/es/docs/commerce/cloud-service/user-management#add-a-user-to-aem-assets-or-product-visuals){target=_blank} en la guía de _Usuario y Identity Management_ para obtener la configuración completa.

![Perfil de producto de Admin Console para la entrega de AEM Assets](../assets/aem-assets-delivery-product-profile.png){width="600" zoomable="yes"}

>[!TAB Adobe Commerce en la nube o local]

[!BADGE Solo PaaS]{type=Informative tooltip="Solo se aplica a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe)."}

Se requiere el **ID de cliente de IMS** para que PaaS habilite el Selector de recursos. Consulte [Configuración del proyecto de AEM Assets](configure-aem.md#prerequisites) para conocer los requisitos previos, incluido cómo obtener el ID de cliente de IMS al habilitar Dynamic Media con OpenAPI.

Para utilizar el Selector de recursos y los campos de configuración rellenados automáticamente (ID de programa, ID de entorno, asignación de dominio):

1. [Habilite Adobe IMS para Commerce](https://experienceleague.adobe.com/docs/commerce-admin/start/admin/ims/adobe-ims-config.html?lang=es){target=_blank} para que el administrador de Commerce utilice la autenticación IMS y pueda leer los perfiles de producto de Admin Console del usuario.

1. [Abra un ticket de asistencia](https://experienceleague.adobe.com/es/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide#support-cases) para solicitar un ID de cliente IMS personalizado para el Selector de recursos.

1. Desde [Adobe Admin Console](https://adminconsole.adobe.com/), agregue el usuario al perfil de producto **Usuarios de OpenAPI de DM AEM Assets - delivery** o al perfil de producto **author** (por ejemplo, `<environment-name> - author - <program-id> - <environment-id>`) como reserva cuando el usuario no tenga el perfil de producto de entrega de AEM en su Admin Console.

Sin IMS, aún puede configurar la integración introduciendo manualmente el ID de programa y el ID de entorno en el administrador de Commerce.

>[!ENDTABS]

## Documentación relacionada

* [Configuración de permisos de usuario de IMS para la integración de AEM Assets](setup-synchronization.md): conecte Commerce a los AEM Assets y configure las reglas coincidentes.
* [Selección manual de recursos](../synchronize/asset-selector-integration.md): utilice el Selector de recursos para imágenes de categoría y Page Builder.
* [Agregar un usuario a los AEM Assets o a los elementos visuales del producto](https://experienceleague.adobe.com/es/docs/commerce/cloud-service/user-management#add-a-user-to-aem-assets-or-product-visuals){target=_blank}: para ACCS, agregue primero a Commerce y a AEM Cloud Manager (Propietario del negocio, Administrador de implementación). El perfil **Usuarios de DM OpenAPI de AEM Assets - delivery** (o el perfil **author** como reserva) es un requisito adicional para el Selector de recursos y las funciones de rellenado automático.
* [Asignar integrantes del equipo a la capa de entrega de AEM](https://experienceleague.adobe.com/es/docs/experience-manager-cloud-service/content/onboarding/journey/assign-profiles-aem#add-team-members){target=_blank}. Documentación de AEM para el acceso a envíos.
