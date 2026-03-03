---
title: '[!DNL Adobe Commerce as a Cloud Service] notas de la versión'
description: Obtenga información acerca de las últimas características y mejoras de  [!DNL Adobe Commerce as a Cloud Service].
feature-set: Commerce
feature: App Builder, GraphQL, Integration, Saas
role: Admin, Developer, User, Leader
level: Beginner
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
exl-id: cf06dec6-8d6b-413e-9977-df88373c188e
source-git-commit: f0f667254bb8b33905543afe83f17428bc3dbdc2
workflow-type: tm+mt
source-wordcount: '1735'
ht-degree: 0%

---

# Notas de la versión

Las siguientes notas de la versión contienen actualizaciones de [!DNL Adobe Commerce as a Cloud Service].

>[!NOTE]
>
>Si utiliza Adobe Commerce local o Adobe Commerce en infraestructura en la nube, consulte las [notas de la versión de Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-operations/release/notes/overview).

## Marzo de 2026 {#latest}

[!BADGE espacio aislado]{type=Caution tooltip="Actualmente, los elementos enumerados solo están disponibles en entornos de espacio aislado. Adobe hace que las nuevas versiones estén disponibles primero en entornos limitados para proporcionar tiempo a las pruebas de los próximos cambios antes de que el lanzamiento esté disponible en los entornos de producción."}

Los elementos siguientes están disponibles actualmente en entornos limitados de [!DNL Adobe Commerce as a Cloud Service] y se lanzarán a los entornos de producción el 9 de marzo de 2026.

>[!BEGINSHADEBOX]

### Tutoriales y herramientas de codificación de App Builder AI

Ahora puede usar la [herramienta para desarrolladores de programación de IA](./migration/coding-tools.md) para crear nuevas aplicaciones de [!DNL App Builder] y convertir las extensiones de PHP de [!DNL Adobe Commerce] existentes en aplicaciones de [!DNL App Builder]. Los siguientes tutoriales están disponibles para demostrar cómo utilizar las herramientas:

* [Requisitos previos del tutorial](./tutorials/tutorial-prerequisites.md)
* [Tutorial de extensión de clasificaciones](./tutorials/ratings-extension.md)
* [Tutorial de extensión de métodos de envío](./tutorials/shipping-method-extension.md)

### Acceso a la administración de aplicaciones de App Builder mediante el administrador

[!DNL Commerce Admin] ahora incluye un elemento de menú que se vincula a [Administración de aplicaciones](https://developer.adobe.com/commerce/extensibility/app-management/){target="_blank"}, un shell unificado para administrar [!DNL App Builder] aplicaciones asociadas con la instancia de Commerce. Esta adición se basa en la última actualización de SDK de la IU de administración. <!-- CEXT-5755 -->

### Solicitar cambio de límite de creación de entidad

El límite del número de sitios web, tiendas y vistas de tiendas estaba limitado anteriormente a 50. Ahora puede enviar una [solicitud de soporte](https://experienceleague.adobe.com/home?support-tab=home#support) para modificar estos límites, si es necesario. <!-- ACCS-398 -->

### Personalizar mensajes de autenticación de tienda con códigos de error estructurados

La mutación de GraphQL [`generateCustomerToken` &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/generate-token/){target="_blank"} ahora devuelve códigos de error escritos junto con mensajes de error, lo que permite que las tiendas muestren mensajes específicos de la interfaz de usuario por motivo de error. Los códigos de error disponibles incluyen: `CUSTOMER_MISSING_EMAIL`, `CUSTOMER_MISSING_PASSWORD`, `CUSTOMER_SIGN_IN_INCORRECT_OR_LOCKED`, `CUSTOMER_ACCOUNT_NOT_CONFIRMED` y `CUSTOMER_GENERIC_ERROR`. <!-- ACCS-301 -->

### Enviar recordatorios automáticos por correo electrónico sobre la inactividad del carro de compras y la lista de deseos

El módulo [Recordatorio de correo electrónico](https://experienceleague.adobe.com/en/docs/commerce-admin/marketing/communications/email-reminders/email-reminder-rules) (`Magento_Reminder`) ahora está activo en [!DNL Adobe Commerce as a Cloud Service], lo que permite a los comerciantes crear reglas de recordatorio automatizadas que almacenan en déclencheur los correos electrónicos enviados a los clientes en función de la inactividad del carro de compras y la lista de deseos. <!-- CCSAAS-4597 -->

### Suscribirse al webhook de eventos de eliminación de categorías

El webhook `observer.catalog_category_delete_before` ya está disponible en [!DNL Adobe Commerce as a Cloud Service]. Utilícela para ejecutar la lógica antes de eliminar una categoría. <!-- CEXT-5862 -->

### Rastrear pedidos de invitados realizados con un correo electrónico registrado

Una nueva configuración opcional de nivel de tienda (desactivada de forma predeterminada) permite a los comerciantes realizar un seguimiento de los pedidos de los clientes realizados mediante una dirección de correo electrónico que coincida con una cuenta de cliente registrada. Cuando se habilita, los pedidos de pago y envío de invitados realizados con un correo electrónico registrado siguen siendo accesibles, y también aparecen en el historial de pedidos del cliente.

Para habilitar esta característica, vaya a **Tiendas** > Configuración > **Configuración** > Ventas > **Ventas** > **Cierre de compra para invitados** y establezca la opción **Permitir el acceso a pedidos de invitados para correos electrónicos registrados** en `Yes`.
<!-- ACCS-289 -->

### Mejoras y correcciones de errores

En esta versión se incluyen las siguientes mejoras, optimizaciones y correcciones de errores seleccionadas:

* Se ha corregido un problema en el cual algunos administradores de organización podían acceder incorrectamente a instancias de inquilino sin tener derecho de por inquilino. <!-- ACCS-335 -->

* Se ha corregido un problema que podía cerrar la sesión de un usuario de [!DNL Commerce Admin] al realizar cambios en un catálogo compartido. <!-- ACCS-318 -->

* Se ha corregido un problema que causaba que algunos campos de webhooks se mostraran incorrectamente en la interfaz de usuario de [!DNL Commerce Admin]. <!-- CEXT-5874 -->

### Interno (POR ELIMINAR)

Se incluyen las siguientes mejoras de infraestructura:

* Se ha actualizado el núcleo de [!DNL Adobe Commerce] de 2.4.8-p3 a 2.4.8-p4. <!-- CCSAAS-4588 -->

* Se ha corregido la gestión de la sesión de cierre de compra de invitado para que la cotización del carro de compras se asocie y mantenga correctamente a lo largo del flujo de cierre de compra de invitado. <!-- ACCS-261 -->

* Se ha ampliado el registro de errores de GraphQL para capturar todos los seguimientos de pila de excepciones y mejorar la capacidad de depuración. <!-- ACCS-305 -->

* Se ha transferido el grupo de pruebas GraphQL de Company Resolver al entorno de prueba CCSaaS. <!-- CCSAAS-2122 -->

* Se han corregido errores de escenarios de administración en compilaciones de CI de devbox de PAT. <!-- ACCS-351 -->

* Se ha agregado un escenario de creación de producto a las compilaciones de tendencias PAT. <!-- CCSAAS-4498 -->

* Paquete transferido del grupo de pruebas GraphQL RequisitionList al entorno de prueba CCSaaS. <!-- CCSAAS-2113 -->

* Se ha paralizado la ejecución de pruebas funcionales de la API de GraphQL en CI para reducir el tiempo de comentarios. <!-- CCSAAS-4607 -->

* Documentación LÉAME actualizada. <!-- ACCS-404 -->

* Reglas de IA del cursor expandidas para el contexto del repositorio de CCSaaS. <!-- PR #1295 -->

* Se han eliminado los archivos de migración antiguos. <!-- PR #1296 -->

* Se deshabilitó el procesamiento de plantillas durante la generación de datos de rendimiento. <!-- PR #1297 -->

* Se agregaron reglas de cursor y documentación de CLI de Magento. <!-- PR #1300 -->

* Se agregó el script de ayuda de base de datos local para desarrollo. <!-- PR #1305 -->

* Se introdujeron las reglas de codificación de seguridad Cursor. <!-- PR #1306 -->

* Se ha optimizado el análisis estático de CI para que se ejecute solo en los archivos modificados. <!-- PR #1309 -->

{{accs-release}}

>[!ENDSHADEBOX]

## Febrero de 2026: #2 de la versión

[!BADGE Producción]{type=Neutral tooltip="Los elementos enumerados están disponibles actualmente en entornos de producción."}

Los elementos siguientes se lanzaron a los entornos de producción de [!DNL Adobe Commerce as a Cloud Service] el 24 de febrero de 2026.

>[!BEGINSHADEBOX]

### Envío de campos de contexto con eventos de comercio

[!DNL Adobe Commerce as a Cloud Service] ahora admite [campos de contexto](https://developer.adobe.com/commerce/extensibility/events/context-fields/) en las cargas de eventos, lo que le permite incluir datos que no forman parte del evento de forma predeterminada. <!-- CEXT-5713 -->

### Suscribirse a eventos de guardado de elementos de presupuesto usando un nuevo webhook

El webhook `observer.sales_quote_item_save_before` ya está disponible en [!DNL Adobe Commerce as a Cloud Service]. Utilícela para ejecutar la lógica antes de guardar un elemento de oferta. <!-- ACCS-346 -->

### Mejoras y correcciones de errores

En esta versión se incluyen las siguientes mejoras, optimizaciones y correcciones de errores seleccionadas:

* Se ha corregido un error que podría provocar problemas de visualización en la lista de productos [!DNL Commerce Admin]. La lista de productos ahora limita el número de catálogos compartidos mostrados para mejorar el rendimiento. <!-- CCSAAS-1242 -->

* Se ha corregido un error de GraphQL que podía impedir la adición de tarjetas de regalo personalizables al carro de compras. <!-- ACCS-313 -->

{{accs-release}}

>[!ENDSHADEBOX]

## Febrero de 2026: #1 de la versión

[!BADGE Producción]{type=Neutral tooltip="Los elementos enumerados están disponibles actualmente en entornos de producción."}

Los elementos siguientes se lanzaron a los entornos de producción de [!DNL Adobe Commerce as a Cloud Service] el 10 de febrero de 2026.

>[!BEGINSHADEBOX]

### Personalización de los métodos de envío y visualización de informes de administración

Se realizaron las siguientes mejoras en [!DNL Commerce Admin]:

* Se mejoró la carga del gancho web de envío [fuera de proceso](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/shipping-use-cases/#payload) para incluir los atributos personalizados de la dirección de envío. Este cambio permite a los comerciantes implementar métodos de envío personalizados. <!-- ACCS-235 -->

* Se ha agregado acceso a los informes de administración, incluidos los informes de [Clientes](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/customer-reports), [Marketing](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/marketing-reports), [Productos](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/product-reports) y [Ventas](https://experienceleague.adobe.com/en/docs/commerce-admin/start/reporting/sales-reports). <!-- CCSAAS-3085 -->

>[!NOTE]
>
>Los informes que no están disponibles en [!DNL Adobe Commerce as a Cloud Service] están etiquetados como solo PaaS ([!BADGE Solo PaaS]{type=Informative url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."}).

### Capturar importes de facturas personalizadas mediante la API de REST

La API de facturas ahora admite [importes de captura personalizados](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/invoices#custom-capture-amounts) mediante atributos de extensión. <!-- ACCS-186, ACCS-197, ACCS-143 -->

>[!NOTE]
>
>Debido a restricciones legales, la cantidad de captura personalizada solo está disponible en la región de América del Norte (NA) y otras regiones donde se permite la captura excesiva de pago.

### Mejoras y correcciones de errores

En esta versión se incluyen las siguientes mejoras, optimizaciones y correcciones de errores seleccionadas:

* Se ha corregido el filtro Cuadrícula de cupones para mostrar todos los cupones personalizados creados mediante la API o mediante la importación. <!-- CCSAAS-4509 -->

* Se ha corregido un problema en [!DNL Storefront Compatibility B2B Package] en el cual la mutación `setNegotiableQuoteShippingAddress` no guardaba las direcciones introducidas manualmente en la libreta de direcciones del cliente, incluso cuando `save_in_address_book` se había establecido en `true`. <!-- LYNX-1031 -->

<!-- The above change will also be covered by the B2B changelog published on February 13, 2026. -->

* Se ha resuelto un problema en el cual las imágenes de producto no se mostraban correctamente en [!DNL Edge Delivery Services] debido a valores `no_selection` dañados en atributos personalizados relacionados con funciones de recurso. <!-- ACAP-1206 -->

* Se ha resuelto un problema que impedía que las cuentas de usuario federadas con valores de nombre o apellido nulos accedieran al administrador de Commerce. <!-- ACCS-200 -->

* Se ha simplificado la configuración del Selector de recursos al proporcionar automáticamente ID de cliente IMS específicos de la región. Los comerciantes ya no necesitan enviar vales de soporte para configurar el Selector de recursos para asignar imágenes de categoría de producto con los recursos. El sistema ahora utiliza automáticamente los ID de cliente de IMS específicos basados en la región de Commerce. <!-- ACCS-175 -->

* Varias mejoras de rendimiento y optimización. <!-- CCSAAS-4485, CCSAAS-4497, ACCS-196 -->

{{accs-release}}

>[!ENDSHADEBOX]

## Enero de 2026

[!BADGE Producción]{type=Neutral tooltip="Los elementos enumerados están disponibles actualmente en entornos de producción."}

Los elementos siguientes se lanzaron a los entornos de producción de [!DNL Adobe Commerce as a Cloud Service] el 20 de enero de 2026.

>[!BEGINSHADEBOX]

### Complementos de B2B

Se han realizado los siguientes cambios en los componentes desplegables B2B:

* [!DNL Commerce Storefront on Edge Delivery Services] ahora incluye [componentes integrados B2B](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/). Ya están disponibles los siguientes complementos B2B:

   * **[Administración de la empresa](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/company-management/)**: habilita la administración de perfiles de empresa y permisos basados en roles para tiendas Adobe Commerce.
   * **[Conmutador de empresa](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/company-switcher/)**: proporciona un componente de interfaz de usuario para que los usuarios cambien entre varias empresas con las que están asociados.
   * **[Pedidos de compra](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/purchase-order/)**: administra los flujos de trabajo de los pedidos de compra, las reglas de aprobación y el historial de pedidos de compra de las transacciones B2B.
   * **[Administración de ofertas](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/quote-management/)**: habilita ofertas negociables para clientes B2B con flujos de trabajo de solicitud de ofertas, negociación y aprobación.
   * **[Listas de solicitudes](https://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/requisition-list/)**: proporciona herramientas para crear y administrar listas de solicitudes para compras repetidas y pedidos masivos.

* Se ha lanzado el paquete de compatibilidad de B2B Storefront. Este paquete mejora el esquema de GraphQL B2B [!DNL Adobe Commerce] para ayudar a mejorar el desarrollo en los sistemas B2B.

<!-- 
* [!DNL Commerce Storefront on Edge Delivery Services] now includes [B2B drop-in components](http://experienceleague.adobe.com/developer/commerce/storefront/dropins-b2b/). For a complete list of available B2B drop-in blocks, refer to the [storefront documentation](http://experienceleague.adobe.com/developer/commerce/storefront/merchants/b2b-commerce-blocks/).

* Released the [B2B Storefront Compatibility Package](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility-b2b/). This package enhances the [!DNL Adobe Commerce] B2B GraphQL schema to help improve development on B2B systems. -->

### Vínculos a rastreadores de envío externos en los que puede hacer clic

Transforme los números de seguimiento de envío incluidos en los correos electrónicos de comprador de texto sin formato en vínculos en los que se puede hacer clic al [habilitar las direcciones URL de seguimiento personalizadas](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/delivery/shipping-settings#shipment-tracking-urls). Esta característica es compatible con USPS, UPS, FedEx y DHL. <!-- See PR #716 in commerce-admin -->

### Compatibilidad con Google reCAPTCHA Enterprise

Las tiendas de [!DNL Adobe Commerce as a Cloud Service] ahora admiten [reCAPTCHA Enterprise](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/security/captcha/security-google-recaptcha-enterprise). Esta función ofrece protección avanzada para bots mediante el uso del análisis de riesgo adaptable y el aprendizaje automático para distinguir con precisión a los usuarios humanos de los bots automatizados. Refuerza la seguridad del sitio, evita actividades fraudulentas y reduce el spam y el abuso para mantener una experiencia de compra fiable. <!-- CCSAAS-4242 -->

### Acceso de administrador específico de instancia

Ahora puede [asignar acceso de usuarios](./user-management.md#add-users) a instancias individuales de [!DNL Adobe Commerce as a Cloud Service] en Admin Console. <!-- CCSAAS-4337 --><!-- See PR #332 -->

### Observabilidad

Si usa [!DNL App Builder], puede obtener una visibilidad más profunda de su instancia de [!DNL Adobe Commerce as a Cloud Service] con la [observabilidad de OpenTelemetry](https://developer.adobe.com/commerce/extensibility/observability/), ahora disponible automáticamente. OpenTelemetry proporciona métricas, registros y seguimientos para ayudarle a supervisar el rendimiento, solucionar problemas más rápido y optimizar su tienda. Esta capacidad permite obtener información proactiva sobre el estado del sistema y mejora la fiabilidad para sus clientes.

>[!NOTE]
>
>La observabilidad de OpenTelemetry requiere el uso de [!DNL App Builder] u otras ofertas de extensibilidad fuera de proceso (OOPE).

### Precio de nivel para reglas de precios de catálogo

Ahora puede combinar descuentos de precios por niveles con descuentos de reglas de catálogo mediante [reglas de precios de catálogo](https://experienceleague.adobe.com/en/docs/commerce-admin/catalog/products/pricing/product-price-tier#enable-tier-pricing-for-catalog-price-rules). Esta mejora le permite crear estrategias de precios más dinámicas y competitivas, recompensando las compras masivas y aplicando descuentos promocionales al mismo tiempo. El resultado es una mayor flexibilidad para atraer clientes, aumentar el valor del pedido y dirigir las conversiones.<!-- See PR #708 in commerce-admin -->

### Mejoras y correcciones de errores

En esta versión de se incluyen las siguientes mejoras, optimizaciones y correcciones de errores seleccionadas:

* Se ha resuelto un error que se podía producir al cargar un archivo en S3. <!-- CCSAAS-4189 -->

* Se ha resuelto un error `User is not entitled to access this instance` que se podía producir al iniciar sesión en el administrador de Commerce o al acceder a la API de REST. <!-- CCSAAS-4324 -->

* Se ha corregido un error que se producía al obtener una vista previa o poner en cola una newsletter desde la cuadrícula Plantilla de newsletter. <!-- CCSAAS-4398 -->

* Se ha corregido un error `404` que se producía al hacer clic en el botón [!UICONTROL **Recargar datos**] en el panel de administración. <!-- CCSAAS-4468 -->

* Se ha resuelto un problema en el cual los atributos personalizados de producto no se podían actualizar a través de la API de REST cuando [!DNL AEM Assets integration] estaba habilitado y el producto tenía imágenes. <!-- ACAP-1178 -->

* Varias mejoras de rendimiento y optimización.<!-- CCSAAS-4255 --><!-- CCSAAS-4233 --><!-- CCSAAS-4220 --><!-- CCSAAS-4252 --><!-- CCSAAS-4330 --><!-- CCSAAS-3669 --><!-- CCSAAS-4462 -->

{{accs-release}}

>[!ENDSHADEBOX]

## Noviembre de 2025

>[!BEGINSHADEBOX]

### Mejoras

* [Administración de usuarios](./user-management.md) - Se ha cambiado el rol de **Administrador de productos** en Admin Console para actualizar automáticamente el acceso de los usuarios al Administrador de Commerce. <!-- CCSAAS-3012 -->

* Se ha agregado la capacidad de cargar y recuperar archivos adjuntos de presupuestos negociables, así como archivos e imágenes asociados con clientes y direcciones de clientes en Amazon S3, usando direcciones URL con firma previa en [GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/uploads) y [REST](https://developer.adobe.com/commerce/webapi/rest/modules/s3-uploads). Con REST, también puede cargar imágenes de categoría. <!-- CCSAAS-3250 -->

* Se agregaron los extremos `POST /V1/customers` y `PUT /V1/customers/{customerId}` a la [API de REST](https://developer.adobe.com/commerce/webapi/rest/reference/) para crear y actualizar clientes. Estos extremos requieren la autorización de IMS. <!-- CCSAAS-3112 -->

* Se ha agregado la mutación [`exchangeOtpForCustomerToken` &#x200B;](https://developer.adobe.com/commerce/webapi/graphql/schema/customer/mutations/exchange-otp-customer-token/), que requiere una dirección de correo electrónico y una contraseña de un solo uso (OTP) para el comprador, y a cambio recibe un token de cliente. Esta mutación se utiliza generalmente en situaciones en las que un cliente necesita autenticarse mediante un OTP enviado a su correo electrónico o teléfono.

* Si una dirección definida en la pantalla de configuración [!UICONTROL **Almacenar direcciones de correo electrónico**] en el administrador contiene un valor que termina con `example.com`, Commerce no envía correos electrónicos a esta dirección. En su lugar, el sistema registra que no se ha enviado el correo electrónico.  <!-- CCSAAS-3533 -->

#### Atributos de pedido personalizados

* Los usuarios administradores ahora pueden ver y editar [atributos de pedidos personalizados](https://experienceleague.adobe.com/en/docs/commerce-admin/stores-sales/order-management/orders/order-processing#custom-order-attributes) directamente desde las pantallas Vista de pedidos, Editar y Crear del panel de administración. Esta mejora mejora mejora la administración de los datos de pedidos personalizados creados mediante GraphQL. <!-- CEXT-5044 -->

>[!ENDSHADEBOX]
