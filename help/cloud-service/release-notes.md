---
title: '[!DNL Adobe Commerce as a Cloud Service] notas de la versión'
description: Obtenga información acerca de las últimas características y mejoras de  [!DNL Adobe Commerce as a Cloud Service].
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Developer, User, Leader
level: Beginner
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
exl-id: cf06dec6-8d6b-413e-9977-df88373c188e
source-git-commit: 1ce3b6b6b94b1b4e94c0d34c081dec2884d7f0f8
workflow-type: tm+mt
source-wordcount: '310'
ht-degree: 0%

---

# Notas de la versión

Las siguientes notas de la versión contienen actualizaciones de [!DNL Adobe Commerce as a Cloud Service]. Para obtener información de otros productos, consulte [Adobe Commerce Optimizer](../optimizer/release-notes.md) o [Adobe Commerce local y Adobe Commerce en la nube](https://experienceleague.adobe.com/es/docs/commerce-operations/release/notes/overview).

[!DNL Adobe Commerce as a Cloud Service] contiene las versiones más recientes de servicios de comercialización, servicios de pago y versiones de extensibilidad. Utilice los siguientes enlaces para ver las notas de la versión de cada uno:

* Servicios
   * [Servicio de catálogo](../catalog-service/release-notes.md)
   * [Live Search](../live-search/release-notes.md)
   * [Servicios de pago](../payment-services/release-notes.md)
   * [Recomendaciones de productos](../product-recommendations/release-notes.md)
   * [Exportación de datos SaaS](../data-export/release-notes.md)
* Extensibilidad
   * [IU de administración para SDK](https://developer.adobe.com/commerce/extensibility/admin-ui-sdk/release-notes/)
   * [Malla de API](https://developer.adobe.com/graphql-mesh-gateway/mesh/release)
   * [Eventos](https://developer.adobe.com/commerce/extensibility/events/release-notes/)
   * [Webhooks](https://developer.adobe.com/commerce/extensibility/webhooks/release-notes/)

## Noviembre de 2025

>[!BEGINSHADEBOX]

### Mejoras

* [Administración de usuarios](./user-management.md) - Se ha cambiado el rol de **Administrador de productos** en Admin Console para actualizar automáticamente el acceso de los usuarios al Administrador de Commerce. <!-- CCSAAS-3012 -->

* Se ha agregado la capacidad de cargar y recuperar archivos adjuntos de presupuestos negociables, así como archivos e imágenes asociados con clientes y direcciones de clientes en Amazon S3, usando direcciones URL con firma previa en [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/uploads) y [REST](https://developer.adobe.com/commerce/webapi/rest/modules/s3-uploads). Con REST, también puede cargar imágenes de categoría. <!-- CCSAAS-3250 -->

* Se agregaron los extremos `POST /V1/customers` y `PUT /V1/customers/{customerId}` a la [API de REST](https://developer.adobe.com/commerce/webapi/rest/reference/) para crear y actualizar clientes. Estos extremos requieren la autorización del administrador. <!-- CCSAAS-3112 -->

* Se ha agregado la mutación [`exchangeOtpForCustomerToken` &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/exchange-otp-customer-token/), que requiere una dirección de correo electrónico y una contraseña de un solo uso (OTP) para el comprador, y a cambio recibe un token de cliente. Esta mutación se utiliza generalmente en situaciones en las que un cliente necesita autenticarse mediante un OTP enviado a su correo electrónico o teléfono.

* Si una dirección definida en la pantalla de configuración [!UICONTROL **Almacenar direcciones de correo electrónico**] en el administrador contiene un valor que termina con `example.com`, Commerce no envía correos electrónicos a esta dirección. En su lugar, el sistema registra que no se ha enviado el correo electrónico.  <!-- CCSAAS-3533 -->

#### Atributos de pedido personalizados

* Los usuarios administradores ahora pueden ver y editar [atributos de pedidos personalizados](https://experienceleague.adobe.com/es/docs/commerce-admin/stores-sales/order-management/orders/order-processing#custom-order-attributes) directamente desde las pantallas Vista de pedidos, Editar y Crear del panel de administración. Esta mejora mejora mejora la administración de los datos de pedidos personalizados creados mediante GraphQL. <!-- CEXT-5044 -->

>[!ENDSHADEBOX]
