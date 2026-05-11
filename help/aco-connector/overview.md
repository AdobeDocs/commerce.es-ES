---
title: Conector de Adobe Commerce Optimizer
description: Obtenga información sobre cómo conectar los datos de su proyecto de nube o local de Commerce a Adobe Commerce Optimizer
feature: Personalization, Integration, Configuration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."
TQID: https://experienceleague.adobe.com/-C-XP5YYxwyGrkvVR6CDd-FpDybqnlaKMmFPKOKUbFA
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
  - id: f42e0a1a-0d79-488d-a83f-f2c30672b137
subfeature_v2:
  - id: ae62cf09-5996-4921-bda8-fbe67b62e470
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
topic_v2:
  - id: aa2f3246-cb95-4b30-8899-fdf7d73550cc
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
  - id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 1233
ht-degree: 0%

---

# Conector de Adobe Commerce Optimizer

Adobe Commerce Optimizer Connector es una integración nativa de origen entre Adobe Commerce (en la nube o de forma local) y Adobe Commerce Optimizer. Sincroniza los datos de catálogo y precios de sus tiendas Adobe Commerce con Commerce Optimizer para que pueda:

- Activar **descubrimiento y recomendaciones de productos impulsados por IA**
- Ejecutar **tiendas sin encabezado de alto rendimiento** (incluidas las tiendas Commerce con tecnología Edge Delivery)
- Analizar **antes y después de** KPI y el estado de sincronización de datos en un solo lugar

Commerce sigue siendo el sistema de registro para productos, precios y estructura de catálogo. Commerce Optimizer se convierte en su nivel de experiencia y comercialización, y sirve resultados rápidos y relevantes para cualquier tienda o canal conectado.

## Ventajas principales {#key-benefits}

| Beneficio | Lo que significa para usted |
| --- | --- |
| **No hay ningún conector personalizado para compilar** | Utilice una integración de origen admitida en lugar de escribir y mantener fuentes y scripts personalizados. |
| **Obtención de valor en menos tiempo con Commerce Optimizer** | Active la Búsqueda por IA, las recomendaciones y las tiendas sin encabezado sobre su implementación de Adobe Commerce existente. |
| **Alineado con ámbitos de Commerce** | Asigna automáticamente sitios web, vistas de tiendas y grupos de clientes en construcciones de catálogo de Commerce Optimizer (fuentes de catálogo y libros de precios). |
| **Visibilidad operativa** | Monitorice el estado de la fuente, los tiempos de última sincronización y el estado por SKU desde una vista de estado de sincronización de fuente de datos dedicada. |
| **Ruta preparada para el futuro hacia SaaS** | Proporciona una ruta de modernización de bajo riesgo de PaaS a Adobe Commerce as a Cloud Service + Optimizer, sin una nueva plataforma. |

## Arquitectura del conector {#connector-architecture}

El diagrama siguiente ilustra la arquitectura de extremo a extremo para el conector, desde Adobe Commerce a través de Commerce Optimizer y hacia fuera hasta los sistemas de tiendas y cajas.

![Diagrama de arquitectura de extremo a extremo del conector Commerce Optimizer Commerce](./assets/aco-connector-end2end-architecture.png){width="700" zoomable="yes"}

En esta arquitectura:

- Adobe Commerce (en la nube o de forma local) es el sistema de producción de registros y piensos
- El conector exporta fuentes de catálogo, precio y categoría
- Commerce Optimizer ingiere y normaliza los datos de fuentes en fuentes de catálogo, libros de precios y vistas de catálogo
- Las tiendas (tienda de Commerce en Edge Delivery o compilaciones personalizadas sin encabezado) llaman a las API de GraphQL de Commerce Optimizer para obtener información y recomendaciones, y llaman a Commerce u otra plataforma de terceros conectada para realizar operaciones de carrito y cierre de compra

## Cómo funciona el conector con Adobe Commerce {#how-it-works}

- Commerce Optimizer ingiere y normaliza los datos de fuente en fuentes de catálogo, libros de precios y vistas de catálogo.

- Las tiendas (tienda de Commerce en Edge Delivery o compilaciones personalizadas sin encabezado) llaman a las API de GraphQL de Commerce Optimizer para obtener información y recomendaciones, y llaman a Commerce u otra plataforma de terceros conectada para realizar operaciones de carrito y cierre de compra.

## Cómo funciona el conector con Adobe Commerce

El conector de Adobe Commerce Optimizer funciona mediante los ámbitos de Commerce existentes (sitios web y vistas de tiendas) y la segmentación de clientes para rellenar el modelo de catálogo de Commerce Optimizer:

![Asignación de datos de Commerce a Adobe Commerce Optimizer](/help/aco-connector/assets/storeview-to-catalogview-mapping.png){width="750" zoomable="yes"}

- **Vistas de tienda → Fuentes de catálogo**: cada vista de tienda se convierte en una Source de catálogo independiente en Commerce Optimizer. Esa fuente incluye atributos de productos localizados y datos específicos de vistas de tienda
- **Sitios web → Libros de precios**: cada sitio web de Commerce se asigna a uno o más Libros de precios en Commerce Optimizer. Exportación de precios de sitio web y precios de grupo de clientes como libros de precios y entradas de precios
- **Grupos de clientes → Variantes de precios** — Los precios de grupos de clientes de Commerce aparecen como entradas adicionales en los libros de precios correspondientes

Una vez que Commerce Optimizer haya introducido los datos, puede configurar lo siguiente:

- **Vistas de catálogo y directivas** en Commerce Optimizer (para generar región, marca o subconjuntos específicos del cliente)
- **Descubrimiento de productos** (búsqueda, facetas, reglas de comercialización)
- **Recomendaciones de productos**

Al habilitar el conector, la instancia de Adobe Commerce sigue siendo el sistema de registro para los datos de catálogo y precio. Al actualizar datos en Commerce, el conector sincroniza esas actualizaciones con la instancia [!DNL Adobe Commerce Optimizer].

>[!NOTE]
>
>Para obtener más información sobre la configuración de Commerce Optimizer, consulte [[!DNL Adobe Commerce Optimizer] Herramientas de comercialización](../optimizer/overview.md#quick-tour).

## Flujos de trabajo habituales {#typical-workflows}

Estos flujos de trabajo describen cómo los equipos configuran y utilizan el conector de Adobe Commerce Optimizer. Para obtener más información sobre cómo configurar la integración y habilitar estos flujos de trabajo, consulte [Introducción](get-started.md).

### Configuración y configuración iniciales {#initial-setup}

1. **Instale el paquete del conector en Adobe Commerce** mediante Composer:

   `composer require adobe-commerce/commerce-data-export-aco-adapter`

1. **Configure los detalles de autenticación y entorno** en el administrador de Commerce o a través de CLI:

   ```terminal
   bin/magento aco:config:init \
     --org_id=<your-org> \
     --tenant_id=<your-tenant> \
     --client_id=<your-client-id> \
     --client_secret=<your-secret> \
     --region=na1 \
     --type=production
   ```

1. **Asignar ámbitos de Commerce a Commerce Optimizer:**

   - Confirmar qué sitios web y vistas de la tienda deben estar dentro del ámbito
   - Asegúrese de que los grupos de clientes y las reglas de precios se modelan según lo esperado

1. **Verificar conectividad:**

   - Ejecute una sincronización de prueba y confirme que las fuentes de catálogo, los libros de precios y los productos iniciales aparecen en Commerce Optimizer
   - Utilice la página Estado de sincronización de fuentes de datos en Commerce y los paneles de sincronización de datos en Commerce Optimizer para la validación

### Sincronización de datos en curso {#ongoing-sync}

Después de la configuración inicial, el conector admite:

- **Sincronización de catálogo completo** para la migración inicial o cambios estructurales grandes
- **Delta sincroniza** para actualizaciones continuas cuando los productos o precios cambian
- **Comandos de resincronización** para fuentes de destino (incluidas categorías desde la versión 1.0.12):

   - `bin/magento saas:resync --feed=products`
   - `bin/magento saas:resync --feed=prices`
   - `bin/magento saas:resync --feed=categories`

### Configuración de tiendas y comercialización {#merchandising-storefronts}

Una vez que los datos de Commerce estén disponibles en Commerce Optimizer, utilice Commerce Optimizer Studio para conectar las experiencias de comercialización y tienda al catálogo sincronizado.

**Para configurar la comercialización y las tiendas:**

1. **Crear vistas de catálogo y directivas** en Commerce Optimizer Studio:

   - Filtre el catálogo por marca, región, segmento de cliente o canal
   - Aplicar reglas de acceso a datos por tienda o socio

1. **Configurar Descubrimiento de productos y Recommendations** en la interfaz de usuario de Optimizer:

   - Crear reglas de comercialización, facetas, sinónimos y unidades de recomendación.
   - El conector descarga toda la configuración de búsqueda y recomendación en Commerce Optimizer (las reglas de Live Search y Product Recommendations del administrador de Commerce ya no se aplican a estos flujos)

1. **Conectar tiendas** a Commerce Optimizer:

   - En el caso de las tiendas Commerce con tecnología Edge Delivery Services, configure la tienda para que utilice el inquilino del Optimizer y la vista de catálogo correctos, y para que invoque los extremos de búsqueda y recomendación mediante la API de comercialización
   - Para tiendas de terceros, utilice las API públicas o SDK de Optimizer para llamadas de búsqueda y recomendación

   >[!NOTE]
   >
   >Para ver un ejemplo de integración de terceros, consulte [Conector de Salesforce Commerce para Commerce Optimizer](../optimizer/developer/salesforce-connector.md).

1. **Mantener cierre de compra** en la plataforma existente:

   - Mantenga las cuentas de carro de compras, cierre de compra, administración de pedidos y clientes en Adobe Commerce o en una plataforma de terceros
   - Utilice App Builder y API Mesh para el traspaso del carro de compras al integrarse con sistemas de cierre de compra externos

## Escenarios admitidos {#supported-scenarios}

El conector está diseñado para comerciantes B2C con Adobe Commerce en implementaciones en la nube y locales que deseen adoptar Commerce Optimizer sin reconstruir su back-end.

**Casos de uso comunes:**

- **Modernizar solo la tienda**
Mantenga su backend de Commerce existente, mueva el PLP/Search/PDP a las tiendas de Edge Delivery con tecnología de Commerce Optimizer

- **Escalar el rendimiento del catálogo y la búsqueda**
Descargue la indexación de catálogos pesados y busque en los servicios SaaS de Commerce Optimizer mientras mantiene la propiedad de productos y precios en Commerce

- **Adopción incremental de SaaS**
Utilice el conector como un paso hacia Adobe Commerce as a Cloud Service + Optimizer, con un catálogo de Commerce componible y compatible

## Responsabilidades y requisitos previos de implementación {#responsibilities-prerequisites}

Commerce es la fuente fiable de productos, precios y grupos de clientes. Realice cambios en Commerce; el conector los sincroniza con Commerce Optimizer.

**Commerce Optimizer es responsable de:**

- Modelado de catálogos (fuentes de catálogo, libros de precios, vistas de catálogo, directivas)
- Descubrimiento de productos y recomendaciones
- Informes de métricas de tienda, paneles de sincronización de datos y métricas de éxito

**El conector no:**

- Modificar el carro de compras, el cierre de compra o los flujos de pedidos de Commerce
- Aprovisionar automáticamente proyectos de tienda (las herramientas de Commerce Storefront y Edge Delivery se encargan de ello)

**Antes de comenzar:**

- Compruebe que Commerce cumple los requisitos mínimos de versión y conector de servicios. Consulte [Introducción](get-started.md#prerequisites) para obtener más información.
- Asegúrese de que tiene acceso a la organización de IMS, una instancia de [!DNL Adobe Commerce Optimizer] y las credenciales y los detalles de región necesarios.

## Documentación relacionada {#related-documentation}

- Configure la integración y habilite los flujos de trabajo clave: [Introducción al conector de Adobe Commerce Optimizer](get-started.md)
- Obtenga información acerca de los conceptos y la arquitectura de Commerce Optimizer: [¿Qué es Adobe Commerce Optimizer?](../optimizer/overview.md)
