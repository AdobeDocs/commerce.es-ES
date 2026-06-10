---
title: '[!DNL Adobe Commerce Optimizer Connector]'
description: Obtenga información acerca de la integración de  [!DNL Adobe Commerce Optimizer Connector] entre [!DNL Adobe Commerce] y [!DNL Adobe Commerce Optimizer] para la sincronización de catálogos, la búsqueda y la entrega de tiendas.
feature: Integration, Storefront, Configuration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."
autotag-review: '2026-06-09T19:00:00.000Z'
TQID: 'https://experienceleague.adobe.com/-C-XP5YYxwyGrkvVR6CDd-FpDybqnlaKMmFPKOKUbFA'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75id: c32adafa-ed01-4b31-997e-2413013911b0id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
subfeature_v2: id: ae62cf09-5996-4921-bda8-fbe67b62e470id: f8ddfd3b-6194-46e8-a176-0e918039be56id: dad884f1-e840-49a1-970e-2f965bdbc410
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: eddd9b14-83bd-4ff4-9072-54a4a484abb7id: e0eb8757-182f-49f3-94a4-1587d16f5094id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: 6d4493db5e0714577a8800007cc6d2c552578fa4
workflow-type: tm+mt
source-wordcount: 1037
ht-degree: 0%

---

# Conector de Adobe Commerce Optimizer

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
| **Ruta preparada para el futuro hacia SaaS** | Proporciona una ruta de modernización de bajo riesgo de PaaS hacia [!DNL Adobe Commerce as a Cloud Service] + [!DNL Adobe Commerce Optimizer], sin una nueva plataforma. |

## Arquitectura del conector {#connector-architecture}

El diagrama siguiente ilustra la arquitectura de extremo a extremo para el conector, desde [!DNL Adobe Commerce] hasta [!DNL Adobe Commerce Optimizer], y desde los escaparates hasta los sistemas de cierre de compra.

![Diagrama de arquitectura de extremo a extremo del conector Adobe Commerce Optimizer](./assets/aco-connector-end2end-architecture.png){width="700" zoomable="yes"}

En esta arquitectura:

- [!DNL Adobe Commerce] (en la nube o de forma local) es el sistema de producción de registros y fuentes
- El conector exporta fuentes de catálogo, precio y categoría
- [!DNL Adobe Commerce Optimizer] ingiere y normaliza los datos de fuente en orígenes de catálogo, libros de precios y vistas de catálogo
- Las tiendas (tienda de Commerce en [!DNL Edge Delivery Services] o compilaciones personalizadas sin encabezado) llaman a las API de GraphQL [!DNL Commerce Optimizer] para el descubrimiento y las recomendaciones y llaman a [!DNL Adobe Commerce] u otra plataforma de terceros conectada para operaciones de carrito y cierre de compra

## Cómo funciona el conector con [!DNL Adobe Commerce]

[!DNL Adobe Commerce Optimizer Connector] funciona con los ámbitos de Commerce existentes (sitios web y vistas de tiendas) y la segmentación de clientes para rellenar el modelo de catálogo [!DNL Adobe Commerce Optimizer]:

![Asignación de datos de Commerce a Adobe Commerce Optimizer](./assets/storeview-to-catalogview-mapping.png){width="750" zoomable="yes"}

- **Vistas de tienda → Fuentes de catálogo**: cada vista de tienda se convierte en una Source de catálogo independiente en [!DNL Adobe Commerce Optimizer]. Esa fuente incluye atributos de productos localizados y datos específicos de vistas de tienda
- **Sitios web → Libros de precios** — Cada sitio web de [!DNL Adobe Commerce] se asigna a uno o más Libros de precios en [!DNL Commerce Optimizer]. Exportación de precios de sitio web y precios de grupo de clientes como libros de precios y entradas de precios
- **Grupos de clientes → Variantes de precios** — Los precios de grupos de clientes de [!DNL Adobe Commerce] aparecen como entradas adicionales en los Libros de precios correspondientes

Después de que [!DNL Commerce Optimizer] ingrese los datos, puede configurar lo siguiente:

- **Vistas de catálogo y directivas** en el estudio [!DNL Adobe Commerce Optimizer] (para generar región, marca o subconjuntos específicos del cliente)
- **Descubrimiento de productos** (búsqueda, facetas, reglas de comercialización)
- **[!DNL Product Recommendations]**

Al habilitar el conector, la instancia [!DNL Adobe Commerce] permanece como el sistema de registro para los datos de catálogo y precio. Cuando actualiza datos en [!DNL Adobe Commerce], el conector sincroniza esas actualizaciones con la instancia [!DNL Adobe Commerce Optimizer].

>[!NOTE]
>
>Para obtener más información sobre la configuración de [!DNL Adobe Commerce Optimizer], consulte [[!DNL Adobe Commerce Optimizer] Herramientas de comercialización](../optimizer/overview.md#quick-tour).

## Flujos de trabajo habituales {#typical-workflows}

Estos flujos de trabajo describen cómo los equipos configuran y usan [!DNL Adobe Commerce Optimizer Connector]. Para obtener más información sobre cómo configurar la integración y habilitar estos flujos de trabajo, consulte [Introducción](get-started.md).

### Configuración y configuración iniciales {#initial-setup}

Consulte [Pasos de configuración](./get-started.md#configuration-steps) en la guía de _Introducción_.

### Sincronización de datos en curso {#ongoing-sync}

Después de la configuración inicial, el conector admite:

- **Sincronización de catálogo completo** para la migración inicial o cambios estructurales grandes
- **Delta sincroniza** para actualizaciones continuas cuando los productos o precios cambian
- **Comandos de resincronización** para fuentes de destino

Las siguientes fuentes están disponibles para [!DNL Adobe Commerce Optimizer Connector]:

- `products` - datos de productos
- `productAttributes`: metadatos de atributos de producto
- `priceBooks` - libros de precios
- `prices` - precios de productos
- `categories` - datos de categorías

Para obtener más información, consulte los temas siguientes:

- Para las operaciones de resincronización de CLI de [!DNL Adobe Commerce], consulte el [comando de resincronización de CLI](../data-export/data-export-cli-commands.md#sync-using-cli-commands){target="_blank"}
- [[!DNL Commerce Optimizer Connector] módulos y extremos de fuentes](reference/connector-reference.md)
- [Asignación de campos para fuentes de conector](reference/field-mapping.md)

### Configuración de tiendas y comercialización {#merchandising-storefronts}

Una vez que los datos de [!DNL Adobe Commerce] estén disponibles en [!DNL Adobe Commerce Optimizer], usa [[!DNL Commerce Optimizer] Studio](https://experienceleague.adobe.com/en/docs/commerce/optimizer/overview#quick-tour) para conectar las experiencias de comercialización y tienda a tu catálogo sincronizado.

**Para configurar la comercialización y las tiendas en [!DNL Commerce Optimizer] Studio:**

1. **Crear vistas de catálogo y directivas** desde el menú [!UICONTROL Store setup].

   - Filtre el catálogo por marca, región, segmento de cliente o canal
   - Aplicar reglas de acceso a datos por tienda o socio

1. **Configurar Descubrimiento de productos y Recommendations** desde el menú [!UICONTROL Merchandising].

   - Crear reglas de comercialización, facetas, sinónimos y unidades de recomendación.
   - El conector descarga toda la configuración de búsqueda y recomendación a [!DNL Commerce Optimizer] ([!DNL Live Search] reglas y [!DNL Product Recommendations] en el administrador de Commerce ya no se aplican a estos flujos)

1. **Conectar tiendas** a [!DNL Commerce Optimizer]:

   - Para una tienda Commerce con tecnología [!DNL Edge Delivery Services], configure la tienda para que use el inquilino y la vista de catálogo de Optimizer correctos y para llamar a los extremos de búsqueda y recomendación mediante la API de comercialización
   - Para tiendas de terceros, utilice las API públicas o SDK de Optimizer para llamadas de búsqueda y recomendación

   >[!NOTE]
   >
   >Para ver un ejemplo de integración de terceros, consulte [Conector de Salesforce Commerce para [!DNL Adobe Commerce Optimizer]](../optimizer/developer/salesforce-connector.md).

1. **Mantener cierre de compra** en la plataforma existente:

   - Mantener las cuentas de carro de compras, cierre de compra, administración de pedidos y clientes en [!DNL Adobe Commerce] o una plataforma de terceros
   - Utilice [!DNL App Builder] y [!DNL API Mesh] para el traspaso del carro de compras al integrarse con sistemas de cierre de compra externos

## Escenarios admitidos {#supported-scenarios}

El conector está diseñado para comerciantes B2C con [!DNL Adobe Commerce] en implementaciones locales y en la nube que deseen adoptar [!DNL Adobe Commerce Optimizer] sin volver a crear su servidor.

**Casos de uso comunes:**

- **Modernizar solo la tienda**
Mantener el servidor [!DNL Adobe Commerce] existente, mover el PLP/Search/PDP a [!DNL Edge Delivery Services] tiendas con tecnología [!DNL Adobe Commerce Optimizer]

- **Escalar el rendimiento del catálogo y la búsqueda**
Descargue la indexación de catálogos y busque en los servicios SaaS de [!DNL Adobe Commerce Optimizer] mientras mantiene la propiedad del producto y el precio en [!DNL Adobe Commerce]

- **Adopción incremental de SaaS**
Utilice el conector como un trampolín hacia [!DNL Adobe Commerce as a Cloud Service] + [!DNL Adobe Commerce Optimizer], con un catálogo [!DNL Adobe Commerce] maquetable compatible

## Responsabilidades y requisitos previos de implementación {#responsibilities-prerequisites}

[!DNL Adobe Commerce] es la fuente fiable para productos, precios y grupos de clientes. Realice cambios en [!DNL Adobe Commerce]; el conector los sincroniza con [!DNL Adobe Commerce Optimizer].

**[!DNL Adobe Commerce Optimizer]es responsable de:**

- Modelado de catálogos (fuentes de catálogo, libros de precios, vistas de catálogo, directivas)
- Descubrimiento de productos y recomendaciones
- Informes de métricas de tienda, paneles de sincronización de datos y métricas de éxito

**El conector no:**

- Modificar [!DNL Adobe Commerce] flujos de pedido, cierre de compra o carro de compras
- Aprovisionar automáticamente proyectos de tienda (Commerce Storefront / [!DNL Edge Delivery Services] se encarga de ello)

**Antes de comenzar:**

- Compruebe que [!DNL Adobe Commerce] cumple los requisitos de versión mínima y [!DNL Commerce Optimizer Connector]. Consulte [Introducción](get-started.md#requirements-to-use-the-integration) para obtener más información.
- Asegúrese de que tiene acceso a la organización de IMS, una instancia de [!DNL Adobe Commerce Optimizer] y las credenciales y los detalles de región necesarios.

## Documentación relacionada {#related-documentation}

- Configure la integración y habilite los flujos de trabajo clave: [Empiece con [!DNL Commerce Optimizer Connector]](get-started.md)
- Obtenga información acerca de [!DNL Adobe Commerce Optimizer] conceptos y arquitectura: [Qué es [!DNL Adobe Commerce Optimizer]?](../optimizer/overview.md)
- Comprenda el mecanismo de sincronización, la inicialización y la administración de errores: [Canalización de sincronización del conector](connector-sync-pipeline.md)
- Asignación de datos de nivel de campo para todas las fuentes: [Asignación de campo para fuentes de conector](reference/field-mapping.md)
- Integrar escaparates sin encabezado mediante GraphQL y la codificación de paquetes: [Integración de escaparates sin encabezado](headless-storefront.md)
- Diagnosticar problemas de sincronización y configuración: [Solución de problemas](troubleshooting.md)
