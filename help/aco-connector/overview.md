---
title: '[!DNL Adobe Commerce Optimizer Connector]'
description: Obtenga información acerca de [!DNL Adobe Commerce Optimizer Connector] para la sincronización de catálogos, la búsqueda y la entrega de tiendas entre [!DNL Adobe Commerce] y [!DNL Adobe Commerce Optimizer].
feature: Integration, Storefront, Configuration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."
autotag-review: '2026-06-09T19:00:00.000Z'
TQID: 'https://experienceleague.adobe.com/-C-XP5YYxwyGrkvVR6CDd-FpDybqnlaKMmFPKOKUbFA'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
subfeature_v2:
  - id: ae62cf09-5996-4921-bda8-fbe67b62e470
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
  - id: dad884f1-e840-49a1-970e-2f965bdbc410
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2:
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 1075
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

[!DNL Adobe Commerce Optimizer Connector] funciona con los ámbitos de Commerce existentes (sitios web y vistas de tiendas) y la segmentación de clientes para rellenar el modelo de catálogo [!DNL Adobe Commerce Optimizer]:

![Asignación de datos de Commerce a Adobe Commerce Optimizer](./assets/storeview-to-catalogview-mapping.png){width="750" zoomable="yes"}

- **Vista de tienda → Orígenes de catálogo**: cada vista de tienda se convierte en un Source de catálogo independiente en [!DNL Adobe Commerce Optimizer]. Esa fuente incluye atributos de productos localizados y datos específicos de vistas de tienda
- **Libros de precios → del sitio web** — Cada sitio web de [!DNL Adobe Commerce] se asigna a uno o más Libros de precios en [!DNL Adobe Commerce Optimizer]. Exportación de precios de sitio web y precios de grupo de clientes como libros de precios y entradas de precios
- **Variantes de precios → grupo de clientes** — Los precios de grupo de clientes [!DNL Adobe Commerce] aparecen como entradas adicionales en los libros de precios correspondientes

Después de que [!DNL Adobe Commerce Optimizer] ingrese los datos, puede configurar lo siguiente:

- **Vistas de catálogo y directivas** en el estudio [!DNL Adobe Commerce Optimizer] (para generar región, marca o subconjuntos específicos del cliente)
- **Descubrimiento de productos** (búsqueda, facetas, reglas de comercialización)
- **[!DNL Product Recommendations]**

Al habilitar el conector, la instancia [!DNL Adobe Commerce] permanece como el sistema de registro para los datos de catálogo y precio. Cuando actualiza datos en [!DNL Adobe Commerce], el conector sincroniza esas actualizaciones con la instancia [!DNL Adobe Commerce Optimizer].

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
- **Comandos de resincronización** para fuentes de destino

Para obtener información sobre el comportamiento de sincronización automatizada, las programaciones de cron y la administración de errores, consulte [Canalización de sincronización de conectores](/help/aco-connector/connector-sync-pipeline.md). Antes de sincronizar todo el catálogo o de realizar una actualización grande, usa [Estimar el volumen de datos y el tiempo de sincronización](/help/aco-connector/reference/estimate-data-volume-sync-time.md) para planificar el tiempo y evitar que el sitio se interrumpa.

Las siguientes fuentes están disponibles para [!DNL Adobe Commerce Optimizer Connector]:

- `products` - datos de productos
- `productAttributes`: metadatos de atributos de producto
- `priceBooks` - libros de precios
- `prices` - precios de productos
- `categories` - datos de categorías

Para obtener más información, consulte los temas siguientes:

- Compruebe la sincronización de datos del catálogo y vuelva a sincronizar manualmente las fuentes del conector: [Administrar la sincronización](/help/aco-connector/data-sync-manage.md)
- Para operaciones de resincronización de CLI de [!DNL Adobe Commerce], consulte [Sincronizar fuentes mediante la CLI de Commerce](/help/data-export/data-export-cli-commands.md)
- [[!DNL Adobe Commerce Optimizer Connector] módulos y extremos de fuentes](/help/aco-connector/reference/connector-reference.md)
- [Asignación de campos para fuentes de conector](/help/aco-connector/reference/field-mapping.md)

### Configuración de tiendas y comercialización {#merchandising-storefronts}

Una vez que los datos de [!DNL Adobe Commerce] estén disponibles en [!DNL Adobe Commerce Optimizer], usa [[!DNL Adobe Commerce Optimizer] Studio](/help/optimizer/overview.md#quick-tour) para conectar las experiencias de comercialización y tienda a tu catálogo sincronizado. Los pasos siguientes habituales incluyen:

- **Vistas de catálogo y políticas**: defina subconjuntos y reglas de acceso específicas de la región, marca o cliente desde el menú [!UICONTROL Store setup]
- **Descubrimiento de productos y recomendaciones**: configure la búsqueda, las facetas, las reglas de comercialización, los sinónimos y las unidades de recomendación en el menú [!UICONTROL Merchandising]. El comportamiento de búsqueda y recomendación se administra en [!DNL Adobe Commerce Optimizer]; la configuración de [!DNL Live Search] y [!DNL Product Recommendations] en el administrador de [!DNL Adobe Commerce] ya no se aplica a estos flujos
- **Conexiones de tienda**: coloque tiendas Commerce en [!DNL Edge Delivery Services] o compilaciones de terceros sin encabezado en los extremos de inquilino, vista de catálogo y API de comercialización correctos [!DNL Adobe Commerce Optimizer]. Para integraciones sin encabezado personalizadas, consulte [Integración de tienda sin encabezado](/help/aco-connector/headless-storefront.md). Para ver un ejemplo de integración de terceros, consulte [Conector de Salesforce Commerce para [!DNL Adobe Commerce Optimizer]](/help/optimizer/developer/salesforce-connector.md)
- **Cierre de compra**: mantenga las cuentas de carro de compras, cierre de compra, administración de pedidos y clientes en [!DNL Adobe Commerce] o en una plataforma de terceros conectada. Usar [!DNL App Builder] y [!DNL API Mesh] para el traspaso del carro de compras cuando sea necesario

Para obtener instrucciones de configuración detalladas, consulte [Introducción](/help/aco-connector/get-started.md) y las [[!DNL Adobe Commerce Optimizer] herramientas de comercialización](/help/optimizer/overview.md#quick-tour).

## Escenarios admitidos {#supported-scenarios}

El conector está diseñado para comerciantes B2C con [!DNL Adobe Commerce] en implementaciones locales y en la nube que deseen adoptar [!DNL Adobe Commerce Optimizer] sin volver a crear su servidor.

**Casos de uso comunes:**

- **Migración de tienda a Edge Delivery**
Mantener el servidor [!DNL Adobe Commerce] existente, mover el PLP/Search/PDP a [!DNL Edge Delivery Services] tiendas con tecnología [!DNL Adobe Commerce Optimizer]

- **Escalar el rendimiento del catálogo y la búsqueda**
Descargue la indexación de catálogos y busque en los servicios SaaS de [!DNL Adobe Commerce Optimizer] mientras mantiene la propiedad del producto y el precio en [!DNL Adobe Commerce]

- **Adopción incremental de SaaS**
Utilice el conector como un trampolín hacia [!DNL Adobe Commerce as a Cloud Service] + [!DNL Adobe Commerce Optimizer], con un catálogo [!DNL Adobe Commerce] maquetable compatible

## Responsabilidades y requisitos previos de implementación {#responsibilities-prerequisites}

[!DNL Adobe Commerce] es la fuente fiable para productos, precios y grupos de clientes. Realice cambios en [!DNL Adobe Commerce] y el conector los sincronizará con [!DNL Adobe Commerce Optimizer].

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
> - [Administrar sincronización](/help/aco-connector/data-sync-manage.md): compruebe la sincronización de datos del catálogo y vuelva a sincronizar las fuentes manualmente.
> - [Asignación de campos para fuentes de conector](/help/aco-connector/reference/field-mapping.md): revise la asignación de datos de nivel de campo para todas las fuentes.
> - [Situaciones de solución de problemas](/help/aco-connector/troubleshooting/troubleshooting-scenarios.md): resuelva la configuración incorrecta o los resultados de sincronización inesperados.
> - [Notas de la versión](/help/aco-connector/release-notes.md): revise las actualizaciones del conector y los problemas conocidos.
