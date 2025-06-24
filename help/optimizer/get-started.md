---
title: Introducción
description: Obtenga información sobre cómo empezar a usar  [!DNL Adobe Commerce Optimizer].
role: Admin, Developer
recommendations: noCatalog
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
source-git-commit: f49a86b8793e2d91413acfbc0b922cb94db67362
workflow-type: tm+mt
source-wordcount: '753'
ht-degree: 0%

---

# Primeros pasos

Este artículo explica cómo ponerse al día con [!DNL Adobe Commerce Optimizer]. Aunque esta guía se centra en las funciones de comerciante y administrador, incluye breves tareas de alto nivel que realizaría un desarrollador. Consulte la [documentación para desarrolladores](https://developer-stage.adobe.com/commerce/services/composable-catalog/) para obtener contenido detallado específico para desarrolladores.

## ¿Cuál es su papel?

La configuración correcta de [!DNL Adobe Commerce Optimizer] generalmente implica a los siguientes integrantes del equipo:

- Administrador
- Desarrollador
- Comerciante

Cada miembro del equipo tiene su propio conjunto de funciones y responsabilidades, tal como se describe en la siguiente tabla:

| Función(s) | Tarea |
|---|---|
| Administrador | Utilice Admin Console para crear administradores, grupos de usuarios, usuarios y desarrolladores&#x200B;. |
|  | Crear una nueva instancia de [!DNL Adobe Commerce Optimizer] en Commerce Cloud Manager&#x200B; |
|  | Configure las directivas y las vistas de catálogo. |
| Desarrollador | Utilice Developer Console para crear un proyecto, conceder acceso a la API a los desarrolladores e instalar las aplicaciones y personalizaciones necesarias. |
|  | Conéctese a su sistema de back office (carrito, cierre de compra) mediante API Mesh y App Builder&#x200B;. |
|  | Ingeste los datos del catálogo de sus soluciones de comercio existentes mediante la API de ingesta de datos de servicios de comercialización&#x200B; |
|  | Configurar tu tienda |
| Comerciante | Configure la detección de productos&#x200B;. |
|  | Configurar recomendaciones de productos. |

Cada función desempeña un papel fundamental en la incorporación e inicio correctos de su entorno [!DNL Adobe Commerce Optimizer]. En el diagrama siguiente se muestra un flujo de trabajo de comienzo a fin de alto nivel para cada rol de la organización:

![Flujo de trabajo de alto nivel](./assets/high-level-workflow.png){zoomable="yes"}

### Administrador

Los administradores son responsables de configurar instancias, administrar usuarios, grupos y autorizaciones para su organización.

- **[Acceder a Adobe Admin Console](https://helpx.adobe.com/es/enterprise/admin-guide.html)**: administre los derechos de Adobe en toda la organización. Consulte [administración de usuarios](./user-management.md) para saber cómo usted, el administrador de productos de su organización o el administrador del sistema pueden agregar usuarios al producto [!DNL Adobe Commerce Optimizer].

- **Crear una instancia** - [!DNL Adobe Commerce Optimizer] instancias usan un sistema basado en crédito. Puede crear varias instancias de Zona protegida y Producción, y cada una de ellas requiere un crédito correspondiente. La cantidad de créditos que tienes inicialmente depende de tu suscripción. [Más información](#create-an-instance).

- **Acceder a una instancia**: después de crear una instancia, puede acceder a ella desde [!UICONTROL Commerce Cloud Manager]. [Más información](#access-an-instance).

- **Configurar directivas y vistas de catálogo** - Aprenda a [definir las directivas y vistas de catálogo](./setup/catalog-view.md). El catálogo no solo contiene los datos del producto, sino que también le ayuda a definir la estructura empresarial.

### Desarrollador

Los desarrolladores crean proyectos y credenciales, instalan extensiones, consumen datos de catálogo y realizan tareas generales de arquitectura de la plataforma. Consulte la [documentación para desarrolladores](https://developer-stage.adobe.com/commerce/services/composable-catalog/) para obtener contenido detallado específico para desarrolladores.

- **Acceder a Developer Console**: accede a [Developer Console](https://developer.adobe.com/developer-console/docs/guides/getting-started) para crear un proyecto para [!DNL Adobe Commerce Optimizer], generar tokens de acceso e instalar las aplicaciones y personalizaciones necesarias.

- **Ingesta de datos de catálogo**. Consulte la documentación de la [API de ingesta de datos](https://developer-stage.adobe.com/commerce/services/composable-catalog/data-ingestion/using-the-api/) para obtener información sobre cómo importar datos de catálogo en [!DNL Adobe Commerce Optimizer].

  Los datos del catálogo introducidos se pueden ver en la página [sincronización de datos](./setup/data-sync.md).

- **Configurar la tienda**: antes de configurar la tienda, primero debe crear una instancia, que es una tarea que suele realizar el [administrador](#administrator) de su organización. Una vez creada la instancia, podrás continuar con [la configuración de](./storefront.md) tu tienda Commerce con tecnología Edge Delivery Services.

### Comerciante

El comerciante utiliza los datos y análisis del comprador para tomar decisiones estratégicas acerca de la ubicación, los precios y las promociones de los productos en la tienda, a la vez que optimiza las experiencias de compra mediante la detección de productos y recomendaciones.

- **Configurar la detección y las recomendaciones de productos** - Aprenda a [crear experiencias personalizadas](./merchandising/overview.md) para sus compradores a través de la detección y las recomendaciones de productos.

## Creación de una instancia

1. Inicie sesión en su cuenta de [Adobe Experience Cloud](https://experience.adobe.com/).

1. En [!UICONTROL Quick access], haga clic en [!UICONTROL **Commerce**] para abrir [!UICONTROL Commerce Cloud Manager].

   [!UICONTROL Commerce Cloud Manager] muestra una lista de [!DNL Adobe Commerce] instancias disponibles en su organización de IMS de Adobe, incluidas ambas instancias aprovisionadas para [!DNL Adobe Commerce Optimizer] y [!DNL Adobe Commerce as a Cloud Service].

1. Haga clic en [!UICONTROL **Agregar instancia**] en la esquina superior derecha de la pantalla.

   ![Crear instancia](./assets/create-aco-instance.png){width="100%" align="center" zoomable="yes"}

1. Seleccione [!UICONTROL **Commerce Optimizer**].

1. Escriba un **Nombre** y una **Descripción** para su instancia.

1. Seleccione la región en la que desea alojar la instancia.

   >[!NOTE]
   >
   >Después de crear una instancia, no se puede cambiar la región.

1. Elija uno de los siguientes [!UICONTROL **tipos de entorno**] para su instancia:

   - [!UICONTROL **Espacio aislado**]: ideal para fines de diseño y prueba. Debe comenzar el recorrido de [!DNL Adobe Commerce Optimizer] usando el entorno de espacio aislado.
   - [!UICONTROL **Producción**]: para tiendas en vivo y sitios de cara al cliente.

   >[!NOTE]
   >
   >Actualmente, las instancias de zona protegida están limitadas a la región de América del Norte.

1. Haga clic en [!UICONTROL **Agregar instancia**].

   La nueva instancia ya está disponible en Cloud Manager.

1. Para ver los detalles de la instancia (incluidos los puntos finales de GraphQL y del servicio de catálogo, la URL para acceder a la aplicación de Adobe Commerce Optimizer y el ID de instancia (ID de inquilino)), haga clic en el icono de información junto al nombre de la instancia.

   ![Crear instancia](./assets/aco-instance-details.png){width="100%" align="center" zoomable="yes"}

## Acceso a una instancia

1. Inicie sesión en su cuenta de [Adobe Experience Cloud](https://experience.adobe.com/).

1. En [!UICONTROL Quick access], haga clic en [!UICONTROL **Commerce**] para abrir [!UICONTROL Commerce Cloud Manager].

   [!UICONTROL Commerce Cloud Manager] muestra una lista de instancias disponibles en su organización de Adobe IMS.

1. Para abrir la aplicación [!UICONTROL Commerce Optimizer] asociada a una instancia, haga clic en el nombre de la instancia.


