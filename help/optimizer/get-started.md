---
title: Introducción
description: Obtenga información sobre cómo empezar a usar  [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
exl-id: de57d93d-e156-45c1-86aa-de29a8c34bd2
source-git-commit: b0ce0a399e89baaeabe87c53d069df866378f8c8
workflow-type: tm+mt
source-wordcount: '867'
ht-degree: 0%

---

# Primeros pasos

Esta guía lo acompaña en la configuración de [!DNL Adobe Commerce Optimizer] de principio a fin. Aunque esta guía cubre todas las funciones, consulte la [documentación para desarrolladores](https://developer.adobe.com/commerce/services/optimizer/) para obtener contenido detallado específico para desarrolladores.

## Requisitos previos

Antes de empezar, asegúrese de que dispone de lo siguiente:

- **Cuenta de Adobe Experience Cloud** con [!DNL Adobe Commerce Optimizer] derechos
- **Acceso de administrador de organización** para crear instancias y administrar usuarios
- **Cuenta de GitHub** (para cargar datos de muestra y desarrollar tiendas)
- **Comprensión básica** de los conceptos de comercio electrónico

## Guía de inicio rápido

Siga estos pasos esenciales para ejecutar el entorno [!DNL Adobe Commerce Optimizer]:

### Paso 1. Creación de una instancia

1. Inicie sesión en [Adobe Experience Cloud](https://experience.adobe.com/).
1. Vaya a **Commerce** > **Commerce Cloud Manager**.
1. Haga clic en **Agregar instancia** > **Commerce Optimizer**.

   ![Crear instancia](./assets/create-aco-instance.png){width="60%" zoomable="yes"}

1. Configure las opciones de instancia:
   - **Nombre**: Nombre descriptivo (por ejemplo, &quot;Mi espacio aislado de la compañía&quot;)
   - **Descripción**: Breve descripción del propósito
   - **Región**: selecciona tu región preferida
   - **Tipo de entorno**: Comience con un entorno de **espacio aislado** para realizar pruebas

1. Haga clic en **Agregar instancia**.

   Cloud Manager se actualiza para incluir la nueva instancia. Para obtener más información sobre cómo obtener acceso y administrarla, consulte [Administrar una instancia](#manage-an-instance).

>[!NOTE]
>
>Las instancias de zona protegida se limitan a la región de América del Norte. No se puede cambiar la región después de crearla.

### Paso 2. Configurar su entorno

Después de crear la instancia:

1. [Administre su instancia](#manage-an-instance) desde Commerce Cloud Manager.
1. Configure el acceso de los usuarios con la [guía de administración de usuarios](./user-management.md).

### Paso 3. Añadir datos de ejemplo (opcional)

Para pruebas y aprendizaje, siga las instrucciones [Cargar datos de muestra](#add-sample-data).

## Flujos de trabajo basados en roles

La configuración y administración de [!DNL Adobe Commerce Optimizer] dependen de tres funciones clave. Cada función tiene tareas y responsabilidades específicas:

![Flujo de trabajo de alto nivel](./assets/high-level-workflow.png){zoomable="yes"}

### Tareas del administrador

Los administradores administran instancias, usuarios y configuración organizativa.

| Tarea | Descripción | Vínculo |
|---|---|---|
| **Administrar usuarios** | Añadir usuarios, desarrolladores y administradores | [Administración de usuarios](./user-management.md) |
| **Crear instancias** | Configuración de entornos de zona protegida y producción | [Crear instancia](#create-an-instance) |
| **Configurar acceso** | Configuración de vistas de catálogo y políticas | [Vistas de catálogo](./setup/catalog-view.md) |

### Tareas del desarrollador

Los desarrolladores gestionan la implementación técnica y la integración de datos, incluidas las tareas de arquitectura de la plataforma.

| Tarea | Descripción | Vínculo |
|---|---|---|
| **Acceder a Developer Console** | Crear proyectos y generar credenciales | [Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started) |
| **Ingesta de datos de catálogo** | Importar datos de productos de sistemas existentes | [API de ingesta de datos](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/) |
| **Configurar tienda** | Configurar la tienda de Edge Delivery Services | [Configuración de tienda](./storefront.md) |

### Tareas del comerciante

Los comerciantes optimizan y personalizan la experiencia de compra a través de la detección de productos y recomendaciones. También usan datos y análisis de compradores para tomar decisiones estratégicas acerca de la ubicación de productos, precios y promociones en la tienda.

| Tarea | Descripción | Vínculo |
|---|---|---|
| **Descubrimiento de productos** | Configuración de la búsqueda y el filtrado | [Información general de comercialización](./merchandising/overview.md) |
| **Recomendaciones** | Configurar recomendaciones de productos con tecnología de IA | [Recomendaciones de productos](./merchandising/recommendations/overview.md) |
| **Seguimiento del rendimiento** | Monitorización de métricas de éxito | [Métricas de éxito](./manage-results/success-metrics.md) |

## Administración de una instancia

1. Inicie sesión en [Adobe Experience Cloud](https://experience.adobe.com/).

1. Abra Commerce Cloud Manager:
   - En **Acceso rápido**, haga clic en **Commerce**.
   - Ver las instancias disponibles.

1. Acceda a su instancia:

   Haga clic en el nombre de instancia para abrir la aplicación [!DNL Adobe Commerce Optimizer]. En la aplicación, puede cambiar entre diferentes instancias de [!DNL Adobe Commerce Optimizer] mediante la lista desplegable situada en la parte superior de la página:

   ![Cambio de instancia](./assets/context-switcher.png){zoomable="yes"}

   Todas las instancias mostradas pertenecen a la misma organización. Puede cambiar entre instancias para ver los datos y la configuración de cada una, como entre entornos de zona protegida y entornos de producción.

1. Obtener detalles de la instancia:
   - Haga clic en el icono de información junto al nombre de la instancia.
   - Observe el extremo de GraphQL, el extremo del servicio de catálogo para la ingesta de datos y el ID de instancia (también conocido como `tenant ID`).

   ![Detalles de instancia](./assets/aco-instance-details.png){width="60%" zoomable="yes"}

   Los detalles del punto de conexión y el ID de instancia (ID de inquilino) son necesarios para integrarse con aplicaciones de front-end y sistemas back-end. La URL para acceder a la aplicación [!DNL Adobe Commerce Optimizer] también se proporciona aquí.

   No todos los usuarios de Adobe Commerce Optimizer tienen acceso a Cloud Manager y a los detalles de la instancia. El acceso depende de la función y los permisos asignados a la cuenta de usuario. Si no tiene acceso, póngase en contacto con el administrador de la organización para obtener los detalles de la instancia.

1. Editar nombre y descripción de instancia:
   - Haga clic en el icono **Editar** junto al nombre de una instancia.
   - Actualice el nombre y la descripción según sea necesario.
   - Haga clic en **Guardar**.

   También puede utilizar las opciones de búsqueda y filtro para buscar instancias específicas rápidamente.

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
- **Recursos De Tienda**: [Documentación De Tienda Commerce](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=es)
- **Soporte**: [Recursos de soporte de Adobe Commerce](https://experienceleague.adobe.com/es/docs/commerce-knowledge-base/kb/overview)
