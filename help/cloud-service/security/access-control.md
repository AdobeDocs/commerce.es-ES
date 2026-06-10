---
title: Administración de acceso e identidad
description: Obtenga información acerca de las funciones de administración de identidades y acceso de Adobe Commerce as a Cloud Service.
role: Admin, Developer, Leader
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
TQID: 'https://experienceleague.adobe.com/lbI3nsLtafel6GtquXnkZmXD2Z3b-rRGPOyr8EqzrjE'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b5f00040-57a0-4a6d-a39e-383b1936c2c9id: ba9e5be9-7de1-4f71-a5d2-baead0e425eeid: c32adafa-ed01-4b31-997e-2413013911b0id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
topic_v2: id: c1579802-ddd4-4214-8a91-97b2066abe11id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adebid: d095671a-1355-40aa-8b5f-06c33c68080bid: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: ef32511703a96b5f4db32d54229e9a7cbe961f12
workflow-type: tm+mt
source-wordcount: 419
ht-degree: 0%

---


# Administración de acceso e identidad

[!DNL Adobe Commerce as a Cloud Service] aprovecha la infraestructura de identidad empresarial de Adobe para garantizar un control de acceso seguro, escalable y centralizado en todos los entornos. La administración de identidad y acceso (IAM) en [!DNL Adobe Commerce as a Cloud Service] está diseñada para simplificar el aprovisionamiento de usuarios, aplicar el acceso con menos privilegios y admitir el cumplimiento de los estándares de seguridad globales.

- **[!DNL Adobe Identity Management Services (IMS)]**: [!DNL Adobe Commerce as a Cloud Service] utiliza [Adobe Identity Management Services (IMS)](https://experienceleague.adobe.com/en/docs/commerce-admin/start/admin/ims/adobe-ims-integration-overview) para autenticar a los usuarios y administrar los derechos. Esto incluye compatibilidad con proveedores de identidad federados y [control de acceso basado en roles](../user-management.md).

- **Gobernanza de Admin Console**: Los administradores administran el acceso a la tienda y al servidor a través de [!DNL Adobe Admin Console]. Los permisos se pueden asignar a características y funciones específicas, lo que garantiza un acceso con menos privilegios.

## Servicios de Adobe Identity Management (IMS)

[!DNL Adobe Commerce as a Cloud Service] usa [!DNL Adobe Identity Management Services (IMS)] para autenticar usuarios y administrar derechos en toda la plataforma. IMS proporciona:

- **Compatibilidad con identidad federada**: integre con proveedores de identidad empresariales, como Azure AD y Okta, mediante SAML o OIDC.
- **Inicio de sesión único (SSO)**: acceso sin problemas a [!DNL Adobe Commerce] y otros [!DNL Adobe Experience Cloud] productos.
- **Autenticación de varios factores (MFA)**: Se aplica en el nivel de organización para mejorar la seguridad.
- **Redundancia global**: los datos de identidad se almacenan en una infraestructura de nube de carga equilibrada de varias regiones.

## Control de acceso de Admin Console

[!DNL Adobe Admin Console] es el concentrador central para administrar el acceso de los usuarios a [!DNL Adobe Commerce as a Cloud Service]:

- **Control de acceso basado en roles (RBAC)**: asigne permisos granulares a los usuarios según sus roles, como Desarrollador, Administrador y Analista.
- **Perfiles de producto**: defina ámbitos de acceso para diferentes entornos, como ensayo y producción.
- **Administración delegada**: los administradores del sistema y de productos pueden administrar el acceso de los usuarios sin la participación de TI.

Consulte [administración de usuarios](https://experienceleague.adobe.com/en/docs/commerce/cloud-service/user-management) para obtener más información.

## Autenticación de API y seguridad de integración

La autenticación de la API REST de [!DNL Adobe Commerce as a Cloud Service] se administra mediante [!DNL Adobe Identity Management Services (IMS)] de Adobe con protocolos OAuth 2 estandarizados. Este sistema de autenticación admite flujos de trabajo interactivos basados en usuarios e integraciones automatizadas servidor a servidor, lo que garantiza un acceso seguro y adecuado para diferentes casos de uso.

>[!NOTE]
>
>Los métodos de administración y generación de tokens de integración de las versiones de PaaS de [!DNL Adobe Commerce] no son compatibles con los entornos SaaS. En su lugar, debe obtener un token de administrador de IMS mediante la autenticación OAuth.

- **Compatibilidad con OAuth 2.0**: autenticación segura basada en tokens para integraciones y servicios de terceros.
- **Acceso a API con ámbito**: Limite el acceso a API a recursos y operaciones específicos.
- **Registro de auditoría**: haga un seguimiento de los eventos de autenticación y los cambios de acceso para comprobar el cumplimiento y solucionar problemas.

Consulte [Autenticación REST](https://developer.adobe.com/commerce/webapi/rest/authentication/) para obtener más información.
