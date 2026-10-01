---
title: Conector de Adobe Commerce Optimizer
description: Obtenga información acerca de [!DNL Adobe Commerce Optimizer Connector] para la sincronización de catálogos, la búsqueda y la entrega de tiendas entre [!DNL Adobe Commerce] y [!DNL Adobe Commerce Optimizer].
feature: Integration, Storefront, Configuration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."
autotag-review: '2026-06-09T19:00:00.000Z'
nudge: true
TQID: 'https://experienceleague.adobe.com/v769V06jl-9YfovpL3HOB-FxovIMZyHxOlHXHvkQmbc'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
    internal-label: Commerce ecosystem
  - id: 00451af3-7b97-5414-9992-3a6c269e413f
    internal-label: Paas
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 76cfaac4-e563-56dd-8938-708bf8b84956
    internal-label: Attributes
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: adedf70c-c1e1-5734-acdc-c5c43b114964
    internal-label: Release Notes
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: e9004f3c-09ae-5d24-acd2-fa0987fdb66e
    internal-label: Companies
  - id: f37757d8-3174-5335-b977-1161792f965d
    internal-label: Personalization
subfeature_v2:
  - id: ae62cf09-5996-4921-bda8-fbe67b62e470
    internal-label: Storefront configuration
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
    internal-label: Cloud architecture
  - id: dad884f1-e840-49a1-970e-2f965bdbc410
    internal-label: Extensions
  - id: 3c398179-d35a-51ba-b317-6c5b95feef5e
    internal-label: Logs
  - id: a1d22079-48b9-5e69-9ee6-eb236068ef34
    internal-label: Search
  - id: e396cff5-f586-484c-89f0-7f1da3308f92
    internal-label: GraphQL
  - id: f56d26ed-050b-4fb7-b29b-8e6e994e80a2
    internal-label: B2B
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
    internal-label: Administration
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
    internal-label: Troubleshooting
source-git-commit: a3ade1a31d3c2905b601f71bda118de89c43cf59
workflow-type: tm+mt
source-wordcount: '1204'
ht-degree: 0%
---
# [!DNL Adobe Commerce Optimizer Connector]

[!DNL Adobe Commerce Optimizer Connector] es una integración de origen nativa entre [!DNL Adobe Commerce] (en la nube o local) y [!DNL Adobe Commerce Optimizer]. Sincroniza los datos de catálogo y de precios de sus tiendas [!DNL Adobe Commerce] en [!DNL Adobe Commerce Optimizer] para que pueda:

- Activar **descubrimiento y recomendaciones de productos impulsados por IA**
- Ejecutar **tiendas sin encabezado de alto rendimiento** (incluidas las tiendas Commerce con tecnología [!DNL Edge Delivery Services])
- Analizar **antes y después de** KPI y el estado de sincronización de datos en un solo lugar

[!DNL Adobe Commerce] sigue siendo el sistema de registro para productos, precios y estructura de catálogo. [!DNL Adobe Commerce Optimizer] se convierte en su nivel de experiencia y comercialización, y ofrece resultados rápidos y relevantes a cualquier tienda o canal conectado.

## Ventajas principales {#key-benefits}

| Beneficio | Lo que significa para usted |
| --- | --- |
| **No hay ningún conector personalizado para compilar** | Utilice una integración de origen admitida en lugar de escribir y mantener fuentes y scripts personalizados. |
| **Obtención de valor en menos tiempo con[!DNL Adobe Commerce Optimizer]** | Activa la Búsqueda por IA, las recomendaciones y las tiendas sin encabezado sobre tu implementación de [!DNL Adobe Commerce] existente. |
| **Alineado con ámbitos de Commerce** | Asigna automáticamente sitios web, vistas de tiendas y grupos de clientes en [!DNL Adobe Commerce Optimizer] construcciones de catálogo (fuentes de catálogo y libros de precios). |
| **Visibilidad operativa** | Monitorice el estado de las fuentes, los tiempos de última sincronización y el estado por SKU desde una vista [!UICONTROL Data Feed Sync Status] dedicada. |
| **Ruta preparada para el futuro hacia SaaS** | Proporciona una ruta de migración por fases desde Commerce en la nube o local a [!DNL Adobe Commerce as a Cloud Service] + [!DNL Adobe Commerce Optimizer], sin necesidad de volver a configurar la plataforma. |

## Arquitectura del conector {#connector-architecture}

El diagrama siguiente ilustra la arquitectura de extremo a extremo para el conector, desde [!DNL Adobe Commerce] hasta [!DNL Adobe Commerce Optimizer], y desde los escaparates hasta los sistemas de cierre de compra.

![Diagrama de arquitectura de extremo a extremo del conector Adobe Commerce Optimizer](./assets/aco-connector-end2end-architecture.png){width="700" zoomable="yes"}

En esta arquitectura:

- [!DNL Adobe Commerce] (en la nube o de forma local) es el sistema de producción de registros y fuentes
- El conector exporta fuentes de catálogo, precio y categoría
- [!DNL Adobe Commerce Optimizer] ingiere y normaliza los datos de fuente en orígenes de catálogo, libros de precios y vistas de catálogo
- Las tiendas (tienda de Commerce en [!DNL Edge Delivery Services] o compilaciones personalizadas sin encabezado) llaman a las API de GraphQL [!DNL Adobe Commerce Optimizer] para el descubrimiento y las recomendaciones y llaman a [!DNL Adobe Commerce] u otra plataforma de terceros conectada para operaciones de carrito y cierre de compra

Compilado en [[!DNL SaaS Data Export]](/help/data-export/overview.md), el conector asigna las fuentes recopiladas al formato [!DNL Catalog Data Ingestion API] y administra la autenticación y el envío. Consulte [Canalización de sincronización de conectores](/help/aco-connector/connector-sync-pipeline.md) para obtener información sobre el comportamiento de sincronización, el control de ámbito y la administración de errores.

## Cómo funciona el conector con [!DNL Adobe Commerce] {#how-the-connector-works-with-adobe-commerce}

[!DNL Adobe Commerce Optimizer Connector] admite la sincronización del catálogo B2C. Sincroniza las fuentes de catálogo y de precios de una instancia de [!DNL Adobe Commerce] y asigna las vistas de tienda, los sitios web y los grupos de clientes a los orígenes de catálogo y los libros de precios de [!DNL Adobe Commerce Optimizer]. No sincroniza el catálogo compartido B2B ni la configuración de asignación de la empresa. Después de la sincronización, configure las vistas de catálogo y las directivas en [!DNL Adobe Commerce Optimizer] Studio.

![Asignando datos de [!DNL Adobe Commerce] a [!DNL Adobe Commerce Optimizer]](./assets/storeview-to-catalogview-mapping.png){width="750" zoomable="yes"}

### Asignación de catálogo base

El conector asigna los datos del catálogo [!DNL Adobe Commerce] al modelo de catálogo [!DNL Adobe Commerce Optimizer]:

- **Vista de tienda → Orígenes de catálogo**: cada vista de tienda se convierte en un origen de catálogo independiente en [!DNL Adobe Commerce Optimizer]. Esa fuente incluye atributos de producto localizados y cualquier dato específico de la vista de tienda.
- **Libros de precios de → del sitio web** — Cada sitio web de [!DNL Adobe Commerce] se asigna a uno o más libros de precios en [!DNL Adobe Commerce Optimizer]. Exportación de precios de sitios web y grupos de precios de clientes como libros de precios y entradas de precios.
- **Entradas del libro de precios del → de grupo de clientes** — Los precios del grupo de clientes [!DNL Adobe Commerce] aparecen como entradas adicionales en los libros de precios relevantes.

Una vez que el conector sincronice los datos del catálogo, configure el modelo de comercialización en [!DNL Adobe Commerce Optimizer] Studio. Por ejemplo, configure:

- **Vistas de catálogo y directivas** para subconjuntos específicos de región, marca o cliente
- **Descubrimiento de productos** para reglas de comercialización, facetas y búsqueda
- **[!DNL Product Recommendations]**

### Comportamiento del conector B2B {#b2b-shared-catalog-projection-specification}

[!DNL Adobe Commerce Optimizer Connector for B2B] amplía el conector base con una proyección unidireccional del catálogo compartido B2B y la configuración de asignación de la empresa en experiencias de catálogo protegidas. [!DNL Adobe Commerce] sigue siendo la fuente fiable de los datos de catálogo y precios; el conector B2B se basa en el catálogo base y en la sincronización de precios y administra las proyecciones generadas por el conector.

Para la asignación de proyección, el flujo de autorización de tiempo de ejecución y el límite de protección, consulte [proyección del catálogo compartido B2B](b2b-shared-catalog-projection.md). Para obtener instrucciones de configuración, consulte [Introducción al conector B2B](/help/aco-connector/get-started-b2b-shared-catalogs.md).

>[!NOTE]
>
>Para obtener más información sobre la configuración de [!DNL Adobe Commerce Optimizer], consulte [[!DNL Adobe Commerce Optimizer] Herramientas de comercialización](/help/optimizer/overview.md#quick-tour).

## Flujos de trabajo habituales {#typical-workflows}

Estos flujos de trabajo describen cómo los equipos configuran y usan [!DNL Adobe Commerce Optimizer Connector]. Para obtener más información sobre cómo configurar la integración y habilitar estos flujos de trabajo, consulte [Introducción](/help/aco-connector/get-started.md).

### Configuración y configuración iniciales {#initial-setup}

Consulte [Pasos de configuración](/help/aco-connector/get-started.md#configuration-steps) en la guía de _Introducción_.

### Sincronización de datos en curso {#ongoing-sync}

Después de la configuración inicial, el conector admite:

- **Sincronización de catálogo completo** para la migración inicial o cambios estructurales grandes
- **Delta sincroniza** para actualizaciones continuas cuando los productos o precios cambian
- **Comandos de resincronización** para sincronizar fuentes de destino

Para obtener información sobre el comportamiento de sincronización automatizada, las programaciones de cron y la administración de errores, consulte [Canalización de sincronización de conectores](/help/aco-connector/connector-sync-pipeline.md). Antes de sincronizar todo el catálogo o de realizar una actualización grande, usa [Estimar el volumen de datos y el tiempo de sincronización](/help/aco-connector/reference/estimate-data-volume-sync-time.md) para planificar el tiempo y evitar que el sitio se interrumpa.

Las siguientes fuentes están disponibles para [!DNL Adobe Commerce Optimizer Connector]:

- `products` - datos de productos
- `productAttributes`: metadatos de atributos de producto
- `priceBooks` - libros de precios
- `prices` - precios de productos
- `categories` - datos de categorías

Para obtener más información, consulte los temas siguientes:

- Compruebe la sincronización de datos del catálogo y vuelva a sincronizar manualmente las fuentes del conector: [Administrar la sincronización](/help/aco-connector/data-sync-status.md)
- Para operaciones de resincronización de CLI de [!DNL Adobe Commerce], consulte [Sincronizar fuentes mediante la CLI de Commerce](/help/data-export/data-export-cli-commands.md)
- [[!DNL Adobe Commerce Optimizer Connector] módulos y extremos de fuentes](/help/aco-connector/reference/connector-reference.md)
- [Asignación de campos para fuentes de conector](/help/aco-connector/reference/field-mapping.md)

### Configuración de tiendas y comercialización {#merchandising-storefronts}

Una vez que los datos de [!DNL Adobe Commerce] estén disponibles en [!DNL Adobe Commerce Optimizer], usa [[!DNL Adobe Commerce Optimizer] Studio](/help/optimizer/overview.md#quick-tour) para conectar las experiencias de comercialización y tienda a tu catálogo sincronizado. Los pasos siguientes habituales incluyen:

- **Vistas de catálogo y políticas**: para el conector base, defina subconjuntos y reglas de acceso específicos de la región, marca o cliente desde el menú [!UICONTROL Store setup]. Para restringir quién puede consultar una vista de catálogo, consulte [Vistas de catálogo privadas](/help/optimizer/setup/private-catalog-view.md)
- **Descubrimiento de productos y recomendaciones**: configure la búsqueda, las facetas, las reglas de comercialización, los sinónimos y las unidades de recomendación en el menú [!UICONTROL Merchandising]. El comportamiento de búsqueda y recomendación se administra en [!DNL Adobe Commerce Optimizer]; la configuración de [!DNL Live Search] y [!DNL Product Recommendations] en el administrador de [!DNL Adobe Commerce] ya no se aplica a estos flujos
- **Conexiones de tienda**: coloque tiendas Commerce en [!DNL Edge Delivery Services] o compilaciones de terceros sin encabezado en los extremos de inquilino, vista de catálogo y API de comercialización correctos [!DNL Adobe Commerce Optimizer]. Para integraciones sin encabezado personalizadas, consulte [Integración de tienda sin encabezado](/help/aco-connector/headless-storefront.md). Para ver un ejemplo de integración de terceros, consulte [Conector de Salesforce Commerce para [!DNL Adobe Commerce Optimizer]](/help/optimizer/developer/salesforce-connector.md)
- **Cierre de compra**: mantenga las cuentas de carro de compras, cierre de compra, administración de pedidos y clientes en [!DNL Adobe Commerce] o en una plataforma de terceros conectada. Usar [!DNL App Builder] y [!DNL API Mesh] para el traspaso del carro de compras cuando sea necesario

Para obtener instrucciones de configuración detalladas, consulte [Introducción](/help/aco-connector/get-started.md) y las [[!DNL Adobe Commerce Optimizer] herramientas de comercialización](/help/optimizer/overview.md#quick-tour).

## Escenarios admitidos {#supported-scenarios}

La base [!DNL Adobe Commerce Optimizer Connector] admite comerciantes B2C con [!DNL Adobe Commerce] en implementaciones locales y en la nube que deseen adoptar [!DNL Adobe Commerce Optimizer] sin volver a crear su servidor.

El(la) [!DNL Adobe Commerce Optimizer Connector for B2B] independiente amplía el conector base para sincronizar la configuración del catálogo compartido y proyectar automáticamente catálogos compartidos personalizados como vistas de catálogo privado. Para obtener más información, consulte [proyección del catálogo B2B](b2b-shared-catalog-projection.md).

**Casos de uso comunes:**

- **Migración de tienda a Edge Delivery**
Mantener el servidor [!DNL Adobe Commerce] existente, mover el PLP/Search/PDP a [!DNL Edge Delivery Services] tiendas con tecnología [!DNL Adobe Commerce Optimizer].

- **Escalar el rendimiento del catálogo y la búsqueda**
Descargue la indexación de catálogos pesados y busque en los servicios de [!DNL Adobe Commerce Optimizer] SaaS (Software as a Service) mientras mantiene la propiedad del producto y el precio en [!DNL Adobe Commerce].

## Responsabilidades y requisitos previos de implementación {#responsibilities-prerequisites}

[!DNL Adobe Commerce] es el sistema de registro para productos, precios y grupos de clientes. Realice cambios en [!DNL Adobe Commerce] y el conector los sincronizará con [!DNL Adobe Commerce Optimizer].

**[!DNL Adobe Commerce Optimizer]es responsable de:**

- Modelado de catálogos (fuentes de catálogo, libros de precios, vistas de catálogo, directivas)
- Descubrimiento de productos y recomendaciones
- Informes de métricas de tienda, paneles de sincronización de datos y métricas de éxito

**El conector no:**

- Modificar [!DNL Adobe Commerce] flujos de pedido, cierre de compra o carro de compras
- Aprovisionar automáticamente proyectos de tienda (Commerce Storefront / [!DNL Edge Delivery Services] se encarga de ello)

**Antes de comenzar:**

- Compruebe que [!DNL Adobe Commerce] cumple los requisitos de versión mínima y [!DNL Adobe Commerce Optimizer Connector]. Consulte [Introducción](/help/aco-connector/get-started.md#requirements-to-use-the-integration) para obtener más información.
- Asegúrese de que tiene acceso a la organización de IMS, una instancia de [!DNL Adobe Commerce Optimizer] y las credenciales y los detalles de región necesarios.

>[!MORELIKETHIS]
>
> - [Introducción a [!DNL Adobe Commerce Optimizer Connector]](/help/aco-connector/get-started.md): configure la integración y habilite los flujos de trabajo clave.
> - [Canalización de sincronización del conector](/help/aco-connector/connector-sync-pipeline.md): comprenda el mecanismo de sincronización, la inicialización y la administración de errores.
> - [Administrar sincronización](/help/aco-connector/data-sync-status.md): compruebe la sincronización de datos del catálogo y vuelva a sincronizar las fuentes manualmente.
> - [Asignación de campos para fuentes de conector](/help/aco-connector/reference/field-mapping.md): revise la asignación de datos de nivel de campo para todas las fuentes.
> - [Situaciones de solución de problemas](/help/aco-connector/troubleshooting/troubleshooting-scenarios.md): resuelva la configuración incorrecta o los resultados de sincronización inesperados.
> - [Notas de la versión](/help/aco-connector/release-notes.md): revise las actualizaciones del conector y los problemas conocidos.
