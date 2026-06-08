---
title: Introducción
description: Obtenga información sobre cómo empezar a usar  [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a Adobe Commerce as a Cloud Service y  [!DNL Adobe Commerce Optimizer] proyectos (infraestructura SaaS administrada por Adobe)."
exl-id: de57d93d-e156-45c1-86aa-de29a8c34bd2
TQID: https://experienceleague.adobe.com/1dcKMjOut1GtiOevvGJECsaU7URFmYg-mQ-m9wi7n4Y
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
subfeature_v2: id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87cid: c1579802-ddd4-4214-8a91-97b2066abe11id: dba482e5-29a8-4127-afa2-c4b913512ef8id: df401a2a-327d-468c-a5e4-b7b7ccd071a0id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 48b94b1b5f38560d5a7be6c5f5431007685202fa
workflow-type: tm+mt
source-wordcount: 1349
ht-degree: 0%

---

# Primeros pasos

Esta guía lo acompaña en la configuración de [!DNL Adobe Commerce Optimizer] de principio a fin. Aunque esta guía cubre todas las funciones, consulte la [documentación para desarrolladores](https://developer.adobe.com/commerce/services/optimizer/) para obtener contenido detallado específico para desarrolladores.

## Tipos de instancias y aislamiento de entornos

Adobe Commerce Optimizer usa instancias independientes para entornos diferentes, como **sandbox** y **production**. Cada instancia tiene su propio ID de instancia y sus propios datos aislados, incluidas las vistas de catálogo, las directivas, la configuración de búsqueda y las recomendaciones de productos.

Al integrarse con Adobe Commerce as a Cloud Service, plataformas de comercio de terceros o tiendas Edge Delivery Services, siempre coinciden con los entornos:

- Conecte **instancias de sandbox Optimizer** a entornos de comercio y tienda que no sean de producción.
- Conecte **instancias de production Optimizer** a los entornos de comercio de producción y tienda.

La combinación de entornos de zona protegida con entornos de producción causa datos de catálogo incoherentes, un comportamiento inesperado de búsqueda y comercialización y métricas poco fiables. Utilice el tipo de instancia y el ID de instancia en Commerce Cloud Manager como fuente fiable al configurar integraciones.

## Requisitos previos

Antes de empezar, asegúrese de que dispone de lo siguiente:

- **Cuenta de Adobe Experience Cloud** con [!DNL Adobe Commerce Optimizer] derechos
- **Acceso de administrador de organización** para crear instancias y administrar usuarios
- **Cuenta de GitHub** para cargar datos de muestra y desarrollar tienda
- **Comprensión básica** de los conceptos de comercio electrónico

## Guía de inicio rápido

Siga estos pasos esenciales para ejecutar el entorno [!DNL Adobe Commerce Optimizer]:

### Paso 1. Crear una instancia

1. Inicie sesión en [Adobe Experience Cloud](https://experience.adobe.com/).
1. Vaya a **Commerce** > **Commerce Cloud Manager**.
1. Haga clic en **Agregar instancia** > **Commerce Optimizer**.

   ![Pantalla Añadir instancia de Adobe Commerce Cloud Manager para crear un entorno de Commerce Optimizer](./assets/create-aco-instance.png){width="60%" zoomable="yes"}

1. Configure las opciones de instancia:
   - **Nombre de instancia**: Nombre descriptivo (por ejemplo, &quot;Mi espacio aislado de la compañía&quot;)
   - **Descripción**: Breve descripción del propósito
   - **Tipo de entorno**: Comience con un entorno de **espacio aislado** para realizar pruebas
   - **Región**: selecciona tu región preferida

1. Haga clic en **Agregar instancia**.

   Cloud Manager se actualiza para incluir la nueva instancia. Para obtener más información sobre cómo obtener acceso y administrarla, consulte [Administrar una instancia](#manage-instances).

>[!NOTE]
>
>Solo puede crear entornos de zona protegida en la región de América del Norte. Una vez creada una instancia, no se puede cambiar la región.

### Paso 2. Configurar su entorno

Después de crear la instancia:

1. [Administre su instancia](#manage-instances) desde Commerce Cloud Manager.
1. Configure el acceso de los usuarios mediante la [Guía de administración de usuarios](./user-management.md).

### Paso 3. Añadir datos de ejemplo (opcional)

Para pruebas y aprendizaje, siga las instrucciones [Cargar datos de muestra](#add-sample-data).

## Flujos de trabajo basados en roles

La configuración y administración de [!DNL Adobe Commerce Optimizer] dependen de tres funciones clave. Cada función tiene tareas y responsabilidades específicas:

![Flujo de trabajo basado en roles para la configuración de [!DNL Adobe Commerce Optimizer] que muestra tareas de administrador, desarrollador y usuario](./assets/high-level-workflow.png){zoomable="yes"}

### Tareas del administrador

Los administradores administran instancias, usuarios y configuración organizativa.

| Tarea | Descripción | Vínculo |
|---|---|---|
| **Administrar usuarios** | Añadir usuarios, desarrolladores y administradores | [Administración de usuarios](./user-management.md) |
| **Crear instancias** | Configuración de entornos de zona protegida y producción | [Crear instancia](#step-1-create-an-instance) |
| **Administrar instancias** | Compruebe el estado, actualice el nombre y la descripción de la instancia y obtenga las URL clave para el acceso a la aplicación y la API | [Administrar instancias](#manage-instances) |
| **Configurar acceso** | Configuración de vistas de catálogo y políticas | [Vistas de catálogo](./setup/catalog-view.md) |

### Tareas del desarrollador

Los desarrolladores gestionan la implementación técnica y la integración de datos, incluidas las tareas de arquitectura de la plataforma.

| Tarea | Descripción | Vínculo |
|---|---|---|
| **Acceder a Developer Console** | Crear proyectos y generar credenciales | [Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started) |
| **Ingesta de datos de catálogo** | Importar datos de productos de sistemas existentes | Para ingerir datos directamente en Adobe Commerce Optimizer, consulte la [API de ingesta de datos](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/){target="_blank"}.<br><br>Para ingerir datos de Commerce en entornos locales o en la nube u otros sistemas de terceros, consulte el tema [Integraciones](./integrations/integrations-overview.md){target="_blank"}. |
| **Configurar la tienda** | Configurar la tienda de Edge Delivery Services | [Configuración de tienda](./storefront.md) |

### Tareas del comerciante

Los comerciantes optimizan y personalizan la experiencia de compra a través de la detección de productos y recomendaciones. También usan datos y análisis de compradores para tomar decisiones estratégicas acerca de la ubicación de productos, precios y promociones en la tienda.

| Tarea | Descripción | Vínculo |
|---|---|---|
| **Descubrimiento de productos** | Configuración de la búsqueda y el filtrado | [Información general de comercialización](./merchandising/overview.md) |
| **Configuración de búsqueda** | Administrar la búsqueda semántica (habilitada de forma predeterminada) y el ajuste opcional | [Configuración — Búsqueda avanzada](./settings.md#advanced-search) y [Búsqueda semántica](./setup/semantic-search.md) |
| **Recomendaciones** | Configurar recomendaciones de productos con tecnología de IA | [Recomendaciones de productos](./merchandising/recommendations/overview.md) |
| **Seguimiento del rendimiento** | Monitorización de métricas de éxito | [Métricas de éxito](./manage-results/success-metrics.md) |

## Administrar instancias

Administre instancias desde Commerce Cloud Manager.

>[!NOTE]
>
>No todos los usuarios de [!DNL Adobe Commerce Optimizer] tienen acceso a Cloud Manager. El acceso depende de la función y los permisos asignados a la cuenta de usuario.

1. Inicie sesión en [Adobe Experience Cloud](https://experience.adobe.com/).

1. Abra Commerce Cloud Manager:

   - En **Acceso rápido**, haga clic en **Commerce**.
   - Ver las instancias disponibles.

### Buscar y filtrar instancias

Después de iniciar sesión, el panel muestra todas las instancias de productos de Commerce disponibles en la organización.
La columna Product indica para qué aplicación de Commerce se aprovisiona la instancia.

![Panel que muestra las opciones de búsqueda y filtro de las instancias de producto de Adobe Commerce Cloud](./assets/search-filter-instances.png){zoomable="yes"}

Utilice las herramientas Filtro y Búsqueda para buscar rápidamente instancias específicas por fecha de creación, región, creador, tipo de producto, entorno o estado.

### Acceder a la interfaz de administración de [!DNL Adobe Commerce Optimizer Studio]

Una vez abierta la aplicación, cambie fácilmente entre entornos como zona protegida y producción para ver los datos y la configuración de cada uno sin volver al Administrador de Commerce Cloud.

1. En el Administrador de Commerce Cloud, haga clic en el nombre de la instancia para abrir [!DNL Adobe Commerce Optimizer Studio].

1. Cambiar entre [!DNL Adobe Commerce Optimizer] instancias sin salir de la aplicación.

   - Haga clic en la lista desplegable de instancias para ver todas las instancias de Optimizer disponibles en la organización.

     ![Menú desplegable del conmutador de instancias para seleccionar [!DNL Adobe Commerce Optimizer] entornos](./assets/context-switcher.png){zoomable="yes"}

- Seleccione la instancia que desea ver.

>[!NOTE]
>
>Para volver al Administrador de Commerce Cloud para ver los detalles de las instancias o administrarlas, haga clic en el icono ![para abrir las aplicaciones de Experience Cloud](./assets/apps-icon.png) (aplicaciones) en la esquina superior izquierda de la navegación superior de Commerce Optimizer.

### Obtener detalles de la instancia

Vea los detalles de la instancia haciendo clic en el icono de información junto al nombre de la instancia.

![[!DNL Adobe Commerce Optimizer] panel de detalles de instancia que muestra los extremos y el identificador de instancia ](./assets/aco-instance-details.png){width="60%" zoomable="yes"}

Tenga en cuenta la siguiente información clave:

- **Extremo de GraphQL** Extremo de GraphQL que usa tu tienda para consultar los datos de catálogo y comercialización de esta instancia mediante la [API del servicio de comercialización](https://developer.adobe.com/commerce/services/optimizer/merchandising-services/){target=&quot;_blank}
- **Punto final de catálogo** Punto final de API de REST que usa para introducir productos y precios en Adobe Commerce Optimizer desde su sistema de comercio o PIM. Ver la [API de ingesta de datos](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/)
- **URL de Commerce Optimizer** Abre la interfaz de usuario de administración de [Adobe Commerce Optimizer Studio](overview.md) para configurar y administrar las vistas de catálogo, las directivas y la comercialización.
- **ID de instancia**: Identificador único (ID de inquilino) de esta instancia de Adobe Commerce Optimizer que usan las tiendas, las API y las herramientas para conectarse al entorno correcto.

Si es desarrollador, necesita estos detalles para configurar su entorno de desarrollo y conectarse a las API de [!DNL Adobe Commerce Optimizer].

>[!NOTE]
>
>Para acceder a los detalles de la instancia, debe tener los permisos necesarios en la organización IMS de Adobe. Si no ve los detalles de la instancia o no puede acceder a la aplicación, póngase en contacto con el administrador de la organización.

### Editar nombre y descripción de instancia

Actualice el nombre y la descripción de la instancia según sea necesario.

1. Haga clic en el icono **Editar** junto al nombre de una instancia.
1. Actualice **Instance name** y **Description** según sea necesario.
1. Haga clic en **Guardar**.

## Añadir datos de ejemplo

Adobe proporciona un repositorio de GitHub con datos de ejemplo y herramientas que le ayudarán a aprender y probar las características de [!DNL Adobe Commerce Optimizer].
Los datos de ejemplo se basan en el [escenario comercial de Carvelo](./use-case/admin-use-case.md) e incluyen:

- Catálogo de productos con piezas de automóvil
- Varios libros de precios y escenarios de precios
- Vistas del catálogo y políticas para diferentes distribuidores
- Completar ejemplos de flujo de trabajo de extremo a extremo

**Cargar los datos de ejemplo:**

1. Acceda al repositorio de GitHub [Ingesta de datos de catálogo de muestra](https://github.com/adobe-commerce/aco-sample-catalog-data-ingestion).

1. Siga las instrucciones de configuración del archivo LÉAME del repositorio para completar las siguientes tareas:

   - Configurar su entorno
   - Completar el proceso de ingesta de datos
   - Creación de vistas de catálogo y políticas con los datos de ejemplo
   - Compruebe la ingesta de datos comprobando los datos del servicio de catálogo en la página [Sincronización de datos](./setup/data-sync.md)

## Pasos siguientes

Después de completar la configuración:

1. Configura tu tienda:
   - Configurar [tienda de Edge Delivery Services](./storefront.md)
   - Conexión a los datos del catálogo

1. Explore el caso de uso de Carvelo:
   - Siga el [flujo de trabajo de extremo a extremo](./use-case/admin-use-case.md)
   - Práctica con escenarios reales

1. Configurar la comercialización:
   - Configurar [descubrimiento de productos](./merchandising/overview.md)
   - Crear [recomendaciones](./merchandising/recommendations/overview.md)

1. Monitorización del rendimiento:
   - Rastrear [métricas de éxito](./manage-results/success-metrics.md)
   - Analizar [rendimiento de búsqueda](./manage-results/search-performance.md)

## Resolución de problemas

### Problemas comunes

| Problema | Solución |
|---|---|
| **No se puede crear una instancia** | Compruebe que tiene [!DNL Adobe Commerce Optimizer] derechos y permisos de administración. |
| **La instancia no aparece** | Compruebe la organización IMS de Adobe y actualice la página. |
| **No se puede obtener acceso a la instancia** | Asegúrese de que se le añade como usuario en Admin Console. |
| **No se cargan los datos de muestra** | Compruebe las credenciales de la instancia y los extremos de la API. |

### Obtener ayuda

- **Recursos para desarrolladores**: [Documentación para desarrolladores](https://developer.adobe.com/commerce/services/optimizer/)
- **Recursos de tienda**: [documentación de tienda Commerce](https://experienceleague.adobe.com/developer/commerce/storefront/)
- **Tutoriales**: [Tutoriales de Commerce Optimizer](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-commerce-optimizer/overview)
- **Soporte**: [Recursos de soporte de Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/overview)
