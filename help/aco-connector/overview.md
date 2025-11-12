---
title: Conector de Adobe Commerce Optimizer para Commerce
description: Obtenga información sobre cómo conectar los datos de su proyecto de nube o local de Commerce a Adobe Commerce Optimizer
feature: Personalization, Integration, Configuration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."
hidefromtoc: true
hide: true
source-git-commit: 36cfafff243a2310a17a2c9ec8a00f10403bc133
workflow-type: tm+mt
source-wordcount: '1552'
ht-degree: 0%

---


# Conector de Adobe Commerce Optimizer para Commerce

Adobe Commerce Connector es el puente de integración que sincroniza los datos de catálogo y precio entre una implementación existente de Adobe Commerce Cloud en la nube o local y el modelo de datos de catálogo maquetable de Adobe Commerce Optimizer. Esto habilita funciones como búsqueda dinámica de IA, Recommendations, tiendas de carga rápida sin encabezado, incluidas las tiendas de Adobe Commerce en Edge Delivery Services y análisis de rendimiento en tiempo real.

>[!NOTE]
>
>Esta documentación describe un producto en desarrollo de acceso anticipado y no refleja todas las funcionalidades pensadas para una disponibilidad general.

## Arquitectura y experiencia

Adobe Commerce Connector funciona asignando la jerarquía de catálogo `website/store/storeview` de Commerce al modelo de datos `channel/policy/source` de Adobe Commerce Optimizer.

En lugar de configurar y administrar los servicios de Commerce (Live Search y Product Recommendations) desde el administrador de Commerce, usa [Adobe Commerce Optimizer Merchandising tools](../optimizer/merchandising/overview.md) para administrar la configuración de reglas de detección de productos (Live Search) y recomendaciones (Product Recommendations).  La instancia de Adobe Commerce se convierte en el origen de los datos de los datos de catálogo y precio. Cuando los datos se actualizan en Commerce, las actualizaciones se sincronizan con la instancia de Adobe Commerce Optimizer.

## Flujos de trabajo

Connector permite varios flujos de trabajo clave:

* **Exportar datos del catálogo Commerce a Adobe Commerce Optimizer**; los datos del libro de precios y precios se exportan al nivel `website`. Los datos de atributos de productos y productos se exportan en el nivel `store view`. De forma predeterminada, la sincronización de datos del catálogo está habilitada para todos los ámbitos de Commerce (sitios web y vistas de tiendas).

  Para habilitar este flujo de trabajo, use Composer para instalar la extensión PHP `adobe-commerce/commerce-data-export-aco-adapter` y luego proporcione las credenciales de IMS para autenticar la conexión entre el proyecto de Commerce.

* **Asigne los datos de Commerce `website/store/storeview` para exportarlos a Adobe Commerce Optimizer**

  Tiene la opción de personalizar la configuración del exportador de Adobe Commerce Optimizer para exportar datos únicamente para ámbitos específicos mediante la actualización de la configuración del exportador desde la cuadrícula Almacenar en administración (**[!UICONTROL Stores]** -> [!UICONTROL Settings] -> **[!UICONTROL All Stores]**).

* **Configuración y administración de reglas de comercialización**

  Cuando el conector está habilitado, las reglas de comercialización para la detección de productos y las recomendaciones se definen y administran desde la interfaz de usuario de Adobe Commerce Optimizer, no desde las páginas de [!UICONTROL Live Search] y [!UICONTROL Product Recommendations] del administrador de Commerce.

* **Implementar tu tienda Commerce en Edge Delivery Services**

  Después de configurar la integración con Adobe Commerce Optimizer, puede configurar e implementar una tienda Commerce en los servicios de Edge Delivery para ofrecer un rendimiento ultrarrápido, escalabilidad, creación de contenido sin problemas, personalización integrada y costes operativos reducidos mediante la arquitectura componible basada en API y los componentes modulares disponibles con Adobe Commerce Optimizer.

## Requisitos para utilizar la integración

* Adobe Commerce 2.4.5+

   * PHP 8.1, 8.2, 8.3 u 8.4
   * Composer 2.x

* Licencia de Adobe Commerce Optimizer con una instancia de zona protegida aprovisionada.

* Acceda a [repo.magento.com](https://repo.magento.com) para descargar el metapaquete del Conector de Commerce usando Composer.

* Acceso de administrador a [instancia de zona protegida de Adobe Commerce Optimizer](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-commerce-optimizer/create-first-instance).

El usuario de Adobe Commerce que configura la integración debe tener:

* Acceso de administrador al administrador de Adobe Commerce.

* [Acceso desde la línea de comandos al servidor de aplicaciones de Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/project/user-access).

* Acceso de desarrollador a la [organización de IMS](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations?) donde se aprovisiona el proyecto de Adobe Commerce Optimizer.

## Primeros pasos

1. **Configurar la integración**

   1. [Instale el paquete del Conector de Commerce](#install-the-commerce-connector-package).

   1. [Obtenga los valores necesarios para configurar la conexión de Commerce Optimizer](#get-required-values-for-configuring-the-commerce-optimizer-connection)

   1. [Habilitar la integración de Adobe Commerce Optimizer](#enable-the-adobe-commerce-optimizer-integration).

   1. [Compruebe que la sincronización de datos funciona](#verify-that-the-data-sync-is-working).

   1. [Personalizar la configuración de exportación de datos](#customize-commerce-data-export-configuration) (opcional).

1. **[Configurar tiendas Adobe Commerce Optimizer](#configure-adobe-commerce-optimizer-stores)**

1. **[Configurar una tienda Commerce en Edge Delivery Services](#set-up-a-commerce-storefront-on-edge-delivery-services)**

## Instalación del paquete de Commerce Connector

El metapaquete del Compositor de conectores de Adobe Commerce está disponible para todos los comerciantes de Commerce con una licencia activa para Adobe Commerce Optimizer.

### Pasos de instalación

1. Agregar el módulo `adobe-commerce/commerce-data-export-aco-adapter` mediante Composer:

```shell
 composer require adobe-commerce/commerce-data-export-aco-adapter
```

1. Implemente los cambios en el entorno de ensayo de Adobe Commerce.

Una vez implementados los cambios, la opción Commerce Optimizer Optimizer está disponible en el menú Administración de Commerce.

>[!NOTE]
>
>Para obtener instrucciones detalladas sobre la instalación de extensiones, consulte las siguientes guías:
>
>[Instalar extensión en Adobe Commerce en la infraestructura de la nube](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure-store/extensions)
>
>[Instalar extensión de Adobe Commerce local](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/extensions)

## Obtenga los valores necesarios para configurar la conexión de Commerce Optimizer

### Obtener credenciales de API

>[!NOTE]
>
>Si ya tiene un proyecto de App Builder Developer en la organización de IMS en la que está implementada su instancia de Commerce Optimizer, puede obtener las credenciales de API y el ID de organización necesarios de las credenciales de servidor a servidor de OAUTH en ese proyecto.

Cree un nuevo proyecto de desarrollador en la consola de Adobe Developer para obtener las credenciales de la API y configurar la integración entre las instancias de Commerce y Commerce Optimizer. Para obtener instrucciones, consulte [Crear un proyecto de App Builder](https://developer.adobe.com/commerce/extensibility/events/project-setup/) en la documentación para desarrolladores.

Después de crear el proyecto, guarde los siguientes valores en la página Credenciales de servidor a servidor OAUTH:

* **ID. de organización** (`org_id`)

* **IMS `client_id` y`client_secret`**

### Obtener detalles de la instancia de Adobe Commerce Optimizer

Guarde los siguientes valores desde los detalles de la instancia de Adobe Commerce Optimizer.

* **ID de instancia: &#x200B;** el identificador único de la instancia de Adobe Commerce Optimizer. También se conoce como ID de inquilino.

  Obtenga el ID de instancia desde la URL para acceder a su instancia de Adobe Commerce Optimizer. Por ejemplo, en la dirección URL `https://na1-sandbox.admin.commerce.adobe.com/1234567890abcdef`, el identificador de instancia es `1234567890abcdef`.

* **Región: &#x200B;** La región en la que está alojada la instancia de la zona protegida de Adobe Commerce Optimizer.

  Obtenga la región desde la URL de Adobe Commerce Optimizer. Por ejemplo, en la dirección URL `https://na1-sandbox.admin.commerce.adobe.com/1234567890abcdef`, la región es `na1`.

## Habilitar la integración de Adobe Commerce Optimizer

>[!IMPORTANT]
>
>El procesamiento de la sincronización de datos se inicia al ejecutar el comando de configuración. De forma predeterminada, la sincronización de datos del catálogo está habilitada para todos los ámbitos de Commerce (sitios web y vistas de tiendas). Según el tamaño del catálogo, el proceso de sincronización de datos puede tardar muchas horas.

Con las credenciales de la API y los detalles de la instancia que recopiló en los pasos anteriores, ahora puede configurar la integración entre las instancias de Commerce y Adobe Commerce Optimizer.

1. En el Administrador de Commerce, seleccione **[!UICONTROL Adobe Commerce Optimizer]** para mostrar la página de configuración con instrucciones.

   ![página de configuración de Adobe Commerce Optimizer](../assets/aco-connector-config-page.png)

1. Desde la línea de comandos, [use SSH](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/secure-connections) para conectarse al entorno de ensayo de Commerce.

1. Ejecute el siguiente comando CLI de Commerce para configurar la integración y reemplace los valores de marcador de posición por los valores de su proyecto de Commerce Optimizer:

```terminal
bin/magento aco:config:init --org_id=<<your_org_id>> --tenant_id=<<your_tenant_id>> --client_id=<<your_client_id>> --client_secret=<<your_client_secret>> --region=<<na1>> --type=sandbox
```

1. Compruebe la conexión volviendo al administrador de Commerce y seleccionando la opción [!UICONTROL Adobe Commerce Optimizer].

   Al hacer clic en la opción, se abre la interfaz de usuario de Adobe Commerce Optimizer en una nueva pestaña.

## Compruebe que la sincronización de datos funciona

Puede comprobar la sincronización de datos desde Commerce Admin y Commerce Optimizer.

* La página **[Estado de sincronización de fuentes de datos](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status.md)** muestra el progreso de la sincronización de datos del catálogo de Commerce a Adobe Commerce Optimizer.

* La página **[[!UICONTROL Data Sync]](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/data-sync)** de Adobe Commerce Optimizer muestra los datos del catálogo transferidos desde la instancia de Commerce.

1. Compruebe que los datos del catálogo fluyen desde Commerce a Commerce Optimizer:

   En Commerce Admin, abra la página [!UICONTROL Data Feed Sync Status] seleccionando [!UICONTROL System] **&#x200B; > [!UICONTROL Data Transfer] > &#x200B;** [!UICONTROL Data Feed Sync Status]**.

   ![Página de estado de sincronización de fuente de datos con informes de estado de elemento de fuente](./assets/data-feed-sync-status.png)

   Si se ha iniciado la sincronización de datos, los datos de la fuente muestran los registros enviados correctamente. También puede ver y solucionar problemas de sincronización consultando los detalles de cada fuente.

1. Compruebe que Adobe Commerce Optimizer está recibiendo los datos del catálogo:

   En el menú Commerce Optimizer, seleccione **[!UICONTROL Data Sync]** para abrir la página Sincronización de datos.

   ![Sincronización de datos](./assets/data-sync.png)

### Resolución de problemas

Si no se ha iniciado la sincronización de datos, asegúrese de que los índices del catálogo sean válidos. Si los índices no son válidos, ejecute el siguiente comando desde la CLI de Commerce para reindexar los datos del catálogo:

```terminal
bin/magento indexer:reindex" catalog indexer re-index CLI command to start PaaS to ACO catalog data synchronization.
```

## Personalizar la configuración de exportación de datos de Commerce

Tiene la opción de personalizar la configuración del exportador de Adobe Commerce Optimizer para exportar datos únicamente para ámbitos específicos mediante la actualización de la configuración del exportador desde la cuadrícula Almacenar en administración (**[!UICONTROL Stores]** -> [!UICONTROL Settings] -> **[!UICONTROL All Stores]**).

* En el nivel `website`, si se deshabilita la configuración del exportador, se detiene la exportación de los datos de los precios y del libro de precios a Adobe Commerce Optimizer.

* En el nivel `storeview`, al deshabilitar la configuración del exportador se detiene la exportación de productos y atributos de productos a Adobe Commerce Optimizer.

Cuando se cambia la configuración, los índices correspondientes se invalidan para almacenar en déclencheur la reexportación de las entidades afectadas.

## Configuración de tiendas Adobe Commerce Optimizer

Configure las tiendas Adobe Commerce Optimizer creando vistas de catálogo y directivas&#x200B; Consulte [Creación de vistas de catálogo](https://experienceleague.adobe.com/en/docs/commerce/optimizer/setup/catalog-view) en la Guía de Adobe Commerce Optimizer.

Tenga en cuenta que los libros de precios se crean automáticamente a partir de los grupos de clientes de Adobe Commerce.

## Configurar una tienda de Commerce en Edge Delivery Services

Esta sección proporciona información general de alto nivel sobre los pasos necesarios para configurar la tienda de Commerce. Encontrará información detallada en el sitio de documentación [Adobe Commerce Storefront] (https://experienceleague.adobe.com/developer/commerce/storefront/).

1. Clonar e implementar plantillas de Adobe Commerce Storefront en EDS mediante la [herramienta de creación de sitios](https://da.live/app/adobe-commerce/storefront-tools/tools/site-creator/site-creator).

1. [Configurar un entorno de desarrollo local](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/#set-up-local-environment).

1. [Instalar el paquete de compatibilidad de GraphQL Storefront](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/storefront-compatibility/install/).&#x200B;

1. [Configurar encabezados CORS para la instancia de Commerce en el entorno de la nube](#configure-cors-headers-for-commerce-instance).

1. [Conecte la tienda a las fuentes de datos de Commerce](#connect-the-storefront-to-commerce-data-sources).

### Configuración de encabezados CORS para instancias de Commerce

Para permitir que las solicitudes de GraphQL provengan de una tienda de Edge Delivery Services (EDS) y se dirijan a Adobe Commerce en la nube o en un entorno local, utilice una de las siguientes opciones para agregar encabezados específicos de Intercambio de recursos de origen cruzado (CORS) a los extremos de GraphQL de Adobe Commerce&#x200B;

1. Agregue encabezados de Intercambio de Recursos de Origen Cruzado (CORS) a los extremos de Adobe Commerce GraphQL&#x200B;

   **Opción 1: Implementar un módulo personalizado de PHP para la base de Adobe Commerce para poder agregar encabezados CORS.&#x200B;**

   **Opción 2: instale un módulo de comunidad de terceros graycore/magento2-cors&#x200B;**. Consulte la [configuración de CORS](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/cors-setup/) en la documentación de *Adobe Commerce Storefront*.

1. Agregue las siguientes variables CORS al archivo de configuración del entorno de Commerce en la instancia de la nube `app.yaml`:

   * `CONFIG__DEFAULT__WEB__GRAPHQL__CORS_ALLOWED_HEADERS: *`
   * `CONFIG__DEFAULT__WEB__GRAPHQL__CORS_ALLOWED_ORIGINS: *`

### Conexión de la tienda a las fuentes de datos de Commerce

En el repositorio de GitHub para el código de plantillas de tienda, actualice el archivo de configuración de tienda `config.json` con los siguientes parámetros:

* `"commerce-core-endpoint": "Commerce cloud instance GraphQL endpoint"`

* `"commerce-endpoint": "Commerce Optimizer instance GraphQL endpoint"`: obtenga este valor de la [página de detalles de la instancia de Commerce Optimizer](https://experienceleague.adobe.com/en/docs/commerce/optimizer/get-started#get-instance-details)&#x200B;

* `"AC-Environment-Id": "Customer organization ID"`: obtenga este valor del [proyecto de nube de Commerce](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/project/overview#project-overview)

* `"AC-View-ID": "Catalog view ID in Commerce Optimizer Admin"`: obtenga este valor del administrador de Adobe Commerce Optimizer.

* `"AC-Price-Book-ID": "base::b6589fc6ab0dc82cf12099d1c2d40ab994e8410c"`: obtenga este valor del administrador de Adobe Commerce Optimizer&#x200B;

* `"AC-Source-Locale": "Catalog source – Store View code from Commerce cloud instance"`

Para obtener más información, consulte [Configuración de tienda](https://experienceleague.adobe.com/developer/commerce/storefront/setup/configuration/commerce-configuration/) en la *documentación de Adobe Commerce Storefront*.


