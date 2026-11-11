---
title: Modelo de datos de catálogo componible y servicios de comercialización
description: Descubra cómo el modelo de datos de catálogo maquetable cambia la entrega de catálogos en [!DNL Adobe Commerce as a Cloud Service] y qué necesitan saber los comerciantes y los equipos de tienda.
feature: Catalog Management, Personalization, Saas
role: Leader
level: Beginner
autotag-review: '2026-11-09T05:07:21.124Z'
TQID: 'https://experienceleague.adobe.com/5Aaumfx9-lOBMDOg59rr-MMl-0sgFLSVUzngkdzfyR0'
product_v2:
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 22bad240-8308-569b-a9d5-578f1ff890ca
    internal-label: Customers
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 4273989f-0bf2-5361-a17a-6909488d18ab
    internal-label: Catalog Service
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 76cfaac4-e563-56dd-8938-708bf8b84956
    internal-label: Attributes
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: a8ae7a5a-6cdc-5922-bd0d-6feb44b04984
    internal-label: Upgrade
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: c18ed297-2187-4aec-affb-9d9654eca6fc
    internal-label: Catalog management
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
  - id: e9004f3c-09ae-5d24-acd2-fa0987fdb66e
    internal-label: Companies
  - id: f37757d8-3174-5335-b977-1161792f965d
    internal-label: Personalization
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
    internal-label: Reporting
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
    internal-label: Reporting
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
source-git-commit: c67e36c5a607fa1112a3a34b71c89de1b0162b10
workflow-type: tm+mt
source-wordcount: '899'
ht-degree: 0%
---

# Servicios de comercialización

Adobe Commerce as a Cloud Service ahora es compatible con el modelo de datos de catálogo maquetable (CCDM) a través de Servicios de comercialización. Adobe Commerce Optimizer presentó este modelo de datos y CCDM proporciona a ambos productos una base común para ofrecer funciones de navegación y comercialización en el catálogo de tiendas, mientras que Commerce Foundation sigue administrando productos, precios y transacciones.

En este tema se explican los cambios que se producen con CCDM, las funciones que continúan y el significado del cambio para los comerciantes, socios y desarrolladores de tiendas.

## ¿Qué cambios introduce CCDM?

El modelo de catálogo original utiliza el servicio de catálogo para ofrecer datos de productos a las tiendas, con Live Search y Product Recommendations que proporcionan funciones de búsqueda, comercialización y recomendaciones. En este modelo, Commerce sincroniza usando [exportación de datos SaaS](https://experienceleague.adobe.com/en/docs/commerce/saas-data-export/overview).

Con CCDM, estas funciones funcionan en la misma base de catálogo que alimenta Adobe Commerce Optimizer. [Vistas de catálogo](../optimizer/setup/catalog-view.md) y [políticas](../optimizer/setup/policies.md) definen el contexto de catálogo disponible para una tienda. Las políticas determinan la variedad de productos y las reglas de comercialización pueden aplicarse en todas las vistas de catálogo o adaptarse a una vista específica.

Esto cambia la forma en que se configura, accede y comercializa el catálogo. CCDM se basa en las funciones de búsqueda, recomendaciones y comercialización del catálogo original de Commerce, a la vez que introduce controles en el nivel de vista de catálogo. A continuación se describen funciones adicionales de administración y creación de informes.

Commerce Foundation sigue siendo la fuente canónica de productos y precios. Los datos de productos y precios se sincronizan de una manera con CCDM a través de una integración nativa de Adobe Commerce as a Cloud Service. La configuración del sitio web, la tienda y la vista de tienda permanece en Commerce, junto con los flujos de trabajo de carro de compras, cierre de compra y administración de pedidos existentes.

## Licencias y aprovisionamiento

Los servicios de comercialización están incluidos en el SKU de Adobe Commerce as a Cloud Service existente. No es un segundo producto o suscripción y no requiere una compra, un derecho o un inquilino de Adobe Commerce Optimizer por separado.

## Descripción general de arquitectura

[!DNL Commerce Foundation] sigue siendo el registro principal de productos y precios, y continúa administrando transacciones. La integración nativa sincroniza los datos de productos y precios de una manera de [!DNL Commerce] a CCDM. No instale un conector independiente ni una aplicación [!DNL App Builder] para esta sincronización.

Las tiendas utilizan servicios de comercialización respaldados por CCDM para recuperar datos de catálogo y contexto para navegación, búsqueda, recomendaciones y comercialización. Las solicitudes utilizan el contexto de catálogo para recuperar productos y precios para la audiencia deseada. Sigue administrando la configuración del sitio web, el almacén y la vista de tienda en [!DNL Commerce].

El diagrama siguiente muestra la posición de los servicios de comercialización en la arquitectura de Adobe Commerce as a Cloud Service más amplia.

![Arquitectura de Commerce que muestra el flujo de datos del catálogo a los servicios de comercialización](./assets/data-flow-ccdm.png){zoomable="yes"}

## ¿Qué novedades hay para los comerciantes?

El nuevo modelo permite ampliar el ámbito de las reglas de comercialización existentes a todas las vistas del catálogo o a una vista específica. Esto permite aplicar la comercialización a cada audiencia de la tienda. Aprenda a [ampliar el ámbito de una regla de comercialización a las vistas de catálogo](../optimizer/merchandising/rules/add.md#create-a-rule).

En el Administrador, puede configurar el contexto del catálogo con [!UICONTROL Catalog Views] y [!UICONTROL Policies]. También puede usar [!UICONTROL Success Metrics] para revisar ingresos, conversión, participación, adquisición y tasa de salida hacia otro sitio. Consulte [Métricas de éxito](../optimizer/manage-results/success-metrics.md) para obtener detalles.

## Consideraciones antes de la adopción

Revise cómo el modelo CCDM afecta a los flujos de trabajo de licencias, integraciones de catálogo, tienda y administración antes de adoptar Merchandising Services.

### Administración de catálogos e integraciones

Continuar administrando productos y precios en [!DNL Commerce Foundation]. La integración nativa los sincroniza con el CCDM. No cree un segundo catálogo de productos para Servicios de comercialización.

### Implementación de Storefront

La forma en que la tienda recupera los datos del catálogo depende de la implementación:

- **[!DNL Adobe Commerce Storefront]** complementos: los complementos administran la transición. No se requieren cambios en el código. Consulte la [documentación de configuración de tienda](https://experienceleague.adobe.com/en/tools/commerce-storefront/).
- **Escaparates personalizados u otras tiendas**: actualice los encabezados de solicitud de catálogo como se describe en la [referencia de configuración de encabezado](https://experienceleague.adobe.com/en/tools/commerce-storefront/setup/configuration/commerce-configuration/#headers).

Revise las consultas de catálogo y los encabezados de solicitud del modelo basado en CCDM. No dé por hecho que las consultas o encabezados existentes permanecen sin cambios. Las consultas de GraphQL de comercialización difieren de las consultas utilizadas en el modelo de servicios de catálogo original. Las consultas adicionales admiten CCDM. Use la [referencia de la API de GraphQL de comercialización](https://developer.adobe.com/commerce/services/reference/graphql/) y compruebe el contexto de catálogo requerido con la [referencia de encabezado de tienda](https://experienceleague.adobe.com/en/tools/commerce-storefront/setup/configuration/commerce-configuration/#headers).

### Aplicaciones y extensiones de terceros

Revise las aplicaciones y extensiones de terceros que leen datos de catálogo o consumen eventos de catálogo con su proveedor. La compatibilidad depende de cómo utilice cada aplicación o extensión esas interfaces.

### Experiencia del administrador

Adobe Commerce as a Cloud Service con CCDM usa [[!DNL Adobe Unified Experience]](https://experienceleague.adobe.com/en/docs/commerce-admin/start/admin/admin-unified-experience) (Unified Shell). Adobe lanzó Unified Shell por separado del CCDM. Las instancias existentes en el modelo de servicios de catálogo original conservan el acceso a Classic y Unified Shell.

### Límites

El modelo CCDM no cambia los límites de as a Cloud Service de Adobe Commerce. Compartir una base de catálogo con Optimizer no significa que Commerce herede la capacidad o los límites de Optimizer.

## Disponibilidad y migración

Las organizaciones que empiecen con Adobe Commerce as a Cloud Service después de esta versión reciben Servicios de comercialización de forma predeterminada. Si su organización requiere el modelo de datos del catálogo original, póngase en contacto con el equipo de su cuenta de Adobe para analizar si hay una excepción disponible.

Las organizaciones que tenían Adobe Commerce as a Cloud Service antes de esta versión pueden elegir cualquiera de los modelos de catálogo al [aprovisionar una nueva instancia](./getting-started.md#create-an-instance). De manera predeterminada, el conmutador [!UICONTROL Enable CCDM] está deshabilitado. Una vez habilitado CCDM, no se puede deshabilitar.

Las instancias existentes no cambian automáticamente. Con disponibilidad general (GA), no puede migrar una instancia de catálogo-servicio original existente a Servicios de comercialización.
