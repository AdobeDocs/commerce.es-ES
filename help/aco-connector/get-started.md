---
title: Introducción al conector de Adobe Commerce Optimizer
description: Obtenga información sobre cómo instalar y configurar el conector, personalizar la configuración de exportación, conectarse a Adobe Commerce Optimizer y monitorizar el estado de sincronización de datos.
feature: Personalization, Integration, Configuration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."
source-git-commit: 79a422b1de81b33c68078af5c082e84d3dfe5bec
workflow-type: tm+mt
source-wordcount: '1093'
ht-degree: 0%

---


# Introducción

Instale y configure Commerce Optimizer Connector para sincronizar los datos del catálogo de Adobe Commerce con [!DNL Adobe Commerce Optimizer] y, a continuación, supervise el estado de sincronización de datos para asegurarse de que la tienda esté actualizada.

## Requisitos para utilizar la integración

* Adobe Commerce 2.4.7+

   * PHP 8.2, 8.3 u 8.4
   * Composer 2.x

* [!DNL Adobe Commerce Optimizer] licencia con una instancia de zona protegida aprovisionada.

* Acceda a [repo.magento.com](https://repo.magento.com) para descargar el metapaquete del Conector de Commerce usando Composer.

* Acceso de administrador a [instancia de zona protegida de Adobe Commerce Optimizer](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-commerce-optimizer/create-first-instance).

El usuario de Adobe Commerce que configura la integración debe tener:

* Acceso de administrador al administrador de Adobe Commerce.

* [Acceso desde la línea de comandos al servidor de aplicaciones de Adobe Commerce](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/project/user-access).

* Acceso de desarrollador a la [organización de IMS](https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations?) donde se aprovisiona el proyecto [!DNL Adobe Commerce Optimizer].

>[!BEGINSHADEBOX]

## Requisitos previos

Si tiene instaladas cualquiera de las siguientes extensiones, desinstálelas antes de instalar el conector de Commerce Optimizer:

* Adobe Commerce Live Search (`magento/live-search`)
* Recomendaciones de productos Adobe Commerce (`magento/product-recommendations`)
* Servicio de catálogo Adobe Commerce (`magento/catalog-service`, `magento/catalog-service-installer`)
* Panel de administración de datos (`magento-catalog-sync-admin`)

Los datos asociados con estas extensiones siguen estando disponibles en la base de datos de Commerce. Sin embargo, no se exporta a [!DNL Adobe Commerce Optimizer] cuando el conector está habilitado. Para implementar las funcionalidades de búsqueda y comercialización proporcionadas por estas extensiones después de habilitar el conector, configúrelas desde la [[!DNL Adobe Commerce Optimizer] IU de administración](https://experienceleague.adobe.com/en/docs/commerce/optimizer/overview#quick-tour).

>[!ENDSHADEBOX]

## Pasos de configuración

1. **Configurar la integración**

   1. **[Instale el paquete Commerce Optimizer Connector](#install-the-commerce-connector-package)** mediante Composer para conectar su instancia de Commerce a [!DNL Adobe Commerce Optimizer].

   1. **[Revise y personalice la configuración de exportación de datos](#customize-commerce-data-export-configuration)** del administrador.

   1. **[Se requieren credenciales de API para establecer la conexión entre Commerce y Commerce Optimizer](#get-required-values-for-configuring-the-commerce-optimizer-connection)**.

   1. **[Habilitar la [!DNL Adobe Commerce Optimizer] integración](#enable-the-adobe-commerce-optimizer-integration)**.

   1. **[Compruebe que la sincronización de datos funciona](#verify-that-the-data-sync-is-working)**.


## Instalación del paquete de Commerce Optimizer Connector

El conector de Adobe Commerce Optimizer se entrega como un metapaquete Composer disponible para todos los comerciantes de Commerce con una licencia activa para [!DNL Adobe Commerce Optimizer].

### Pasos de instalación

1. Agregar el módulo `adobe-commerce/commerce-data-export-aco-adapter` mediante Composer:

   ```shell
   composer require adobe-commerce/commerce-data-export-aco-adapter
   ```

1. Implemente los cambios en el entorno de ensayo de Adobe Commerce.

Una vez finalizada la implementación, la opción Commerce Optimizer está disponible en el menú Administración de Commerce. Haga clic en **[!UICONTROL Commerce Optimizer]** para abrir la instancia de Commerce Optimizer directamente desde el administrador de Commerce.

>[!NOTE]
>
>Para obtener instrucciones detalladas sobre la instalación de extensiones, consulte las siguientes guías:
>
>[Instalar extensión en Adobe Commerce en la infraestructura de la nube](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure-store/extensions)
>
>[Instalar la extensión en Adobe Commerce local](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/extensions)

### Obtener los detalles de conexión necesarios

Desde Adobe Developer Console, cree un proyecto de desarrollador habilitado para el servicio de ingesta [!DNL Adobe Commerce Optimizer] y genere credenciales de servidor a servidor OAuth. Para obtener instrucciones detalladas, consulte [Obtener credenciales de IMS](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/authentication/#obtain-ims-credentials) en la *Guía para desarrolladores de comercialización*.

>[!TIP]
>
>Si ya tiene un proyecto de desarrollador configurado con la API de ingesta de datos en la misma organización de IMS que la instancia de Commerce Optimizer, puede reutilizar las credenciales de servidor a servidor de OAuth existentes.

Guarde los siguientes valores desde la página de credenciales:

* **ID. de organización** (`org_id`)
* **ID de cliente** (`client_id`)
* **Secreto de cliente** (`client_secret`)

### Obtener detalles de instancia de [!DNL Adobe Commerce Optimizer]

Guarde el ID de instancia (también denominado ID de inquilino) de la instancia [!DNL Adobe Commerce Optimizer]. Puede encontrarlo en la dirección URL utilizada para acceder a la instancia. Por ejemplo, en `https://experience.adobe.com/#/@<project-id>/in:TToyu73daQRn66KAYaq8YZ/commerce-optimizer-studio/home`, el identificador de instancia es `TToyu73daQRn66KAYaq8YZ`.

## Personalizar la configuración de exportación de datos de Commerce

De forma predeterminada, la sincronización de datos del catálogo está habilitada para todos los ámbitos de Commerce (sitios web y vistas de tiendas). Puede personalizar la configuración de exportación para sincronizar datos solo para ámbitos específicos según sus necesidades empresariales. Por ejemplo, si tiene varias vistas de tienda, pero solo desea exportar los datos de una de ellas, puede desactivar el exportador de las demás.

>[!IMPORTANT]
>
>El cambio de la configuración de exportación déclencheur una reindexación completa, que puede tardar un tiempo considerable en función del tamaño del catálogo. Planifique estos cambios durante los períodos de poco tráfico para minimizar el impacto en el rendimiento.

### Exportación de datos por ámbito

En la tabla siguiente se describen los datos que se exportan en cada nivel de ámbito:

| Ámbito | Datos exportados | Notas |
| ------- | --------------- | ------- |
| Sitio web | Precios y libros de precios | Cada conjunto de precios se exporta como un [libro de precios](../optimizer/setup/pricebooks.md) utilizando la convención de nomenclatura `website::customergroupcode`. Se incluyen todos los grupos de clientes del sitio web. |
| Vista de tienda | Productos y atributos del producto | Cada vista de tienda crea un origen de catálogo independiente en [!DNL Adobe Commerce Optimizer]. |

### Habilitar y deshabilitar el comportamiento

| Acción | Resultado |
| -------- | -------- |
| Deshabilitar una vista de tienda | El origen del catálogo permanece en [!DNL Adobe Commerce Optimizer], pero se han eliminado todos los datos. |
| Deshabilitar y volver a habilitar una vista de tienda | El mismo origen de catálogo se vuelve a rellenar con una resincronización de datos completa. |

### Actualizar la configuración de exportación

Después de instalar el paquete Connector, la cuadrícula Store en Admin ahora muestra los ajustes de configuración de exportación para Commerce Optimizer.

![Almacenar cuadrícula con configuración de sincronización de Commerce Optimizer](./assets/aco-connector-sync-config.png){width="600" zoomable="yes"}

**Para cambiar la configuración de un sitio web o vista de una tienda:**

1. En el Administrador de Commerce, vaya a **[!UICONTROL Stores]** > [!UICONTROL Settings] > **[!UICONTROL All Stores]**.

1. Seleccione el sitio web o la vista de tienda que desee configurar.

1. En la configuración del exportador **[!DNL Adobe Commerce Optimizer]**, utilice la casilla de verificación para habilitar o deshabilitar la sincronización de datos según sea necesario.

   ![Actualizar configuración de sincronización de datos](./assets/aco-connector-store-website-export-settings.png){width="500" zoomable="yes"}

1. Guarde los cambios.

## Habilitar la integración [!DNL Adobe Commerce Optimizer]

>[!IMPORTANT]
>
>El procesamiento de la sincronización de datos se inicia en cuanto se ejecuta el comando de configuración. De forma predeterminada, la sincronización de datos del catálogo está habilitada para todos los ámbitos de Commerce (sitios web y vistas de tiendas). Según el tamaño del catálogo, el proceso de sincronización de datos puede tardar entre unos minutos y varias horas.

Utilizando las credenciales de la API y los detalles de la instancia que recopiló en los pasos anteriores, ahora puede configurar la integración entre las instancias de Commerce y [!DNL Adobe Commerce Optimizer].

1. En el Administrador de Commerce, seleccione **[!UICONTROL Adobe Commerce Optimizer]** para mostrar la página de configuración con instrucciones.

   ![[!DNL Adobe Commerce Optimizer] página de configuración](/help/aco-connector/assets/aco-connector-admin-installation.png){width="500" zoomable="yes"}

1. Desde la línea de comandos, [use SSH](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/secure-connections) para conectarse al entorno de ensayo de Commerce.

1. Ejecute el siguiente comando CLI de Commerce para configurar la integración y reemplace los valores de marcador de posición por los valores de su proyecto de Commerce Optimizer:

```terminal
bin/magento aco:config:init --org_id=your-org --tenant_id=your-tenant --client_id=your-client-id --client_secret=your-secret
```

1. Compruebe la conexión volviendo al administrador de Commerce y seleccionando la opción [!UICONTROL Adobe Commerce Optimizer].

   Al hacer clic en la opción, se abre la interfaz de usuario de [!DNL Adobe Commerce Optimizer] en una nueva pestaña.

## Compruebe que la sincronización de datos funciona

Después de habilitar la integración, la sincronización de datos se inicia automáticamente. Según el tamaño del catálogo, la sincronización inicial puede tardar entre unos minutos y varias horas.

1. **Comprobar el estado de sincronización en el administrador de Commerce:**

   Vaya a **[!UICONTROL System]** > [!UICONTROL Data Transfer] > **[!UICONTROL Data Feed Sync Status]**.

   ![Página de estado de sincronización de fuente de datos con informes de estado de elemento de fuente](./assets/data-feed-sync-status.png){width="500" zoomable="yes"}

   Cuando se está ejecutando la sincronización, los datos de la fuente muestran los registros enviados correctamente. Seleccione una fuente para ver los detalles o solucionar problemas de sincronización.

1. **Confirmar datos que llegaron a Commerce Optimizer:**

   En el menú [!DNL Adobe Commerce Optimizer], seleccione **[!UICONTROL Data Sync]**.

   ![Sincronización de datos](./assets/data-sync.png){width="500" zoomable="yes"}

   Compruebe que aparecen los productos, precios y atributos esperados.

>[!TIP]
>
>Si tiene algún problema con la sincronización de datos, consulte la sección [Solución de problemas](/help/data-export/troubleshooting-logging.md) en la documentación de *Exportación de datos SaaS*.

## Pasos siguientes

1. **[Configurar [!DNL Adobe Commerce Optimizer] directivas y vistas de catálogo](#configure-adobe-commerce-optimizer-stores)**

   Cree vistas de catálogo y directivas en la guía [!DNL Adobe Commerce Optimizer]. Tenga en cuenta que los libros de precios se crean automáticamente a partir de los grupos de clientes de Adobe Commerce.

1. **[Configurar una tienda Commerce en Edge Delivery Services](#set-up-a-commerce-storefront-on-edge-delivery-services)**

   Siga la [documentación de configuración de tienda](https://experienceleague.adobe.com/developer/commerce/storefront/setup/) para conectar su tienda a la instancia [!DNL Adobe Commerce Optimizer] y comenzar a ofrecer experiencias de comercio personalizadas.


