---
title: Introducción a  [!DNL Adobe Commerce Optimizer Connector]
description: Obtenga información sobre cómo instalar  [!DNL Adobe Commerce Optimizer Connector], configurar la exportación de ámbito, habilitar la autenticación IMS y comprobar la sincronización del catálogo.
feature: Integration, Configuration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."
autotag-review: '2026-06-09T16:55:50.934Z'
TQID: 'https://experienceleague.adobe.com/AcZ6CNyuIdUlfVHXhyQEYuThfLNd4WWqMMY82tjMMCc'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
subfeature_v2:
  - id: e126554b-28f9-4290-b58c-10b888b88174
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 69f39a6a62e05c86a0e2897d09079543b3d8830e
workflow-type: tm+mt
source-wordcount: 1184
ht-degree: 0%

---


# Introducción

Instala y configura [!DNL Adobe Commerce Optimizer Connector] para que sincronice los datos del catálogo [!DNL Adobe Commerce] con [!DNL Adobe Commerce Optimizer] y, a continuación, supervisa el estado de sincronización de datos para asegurarte de que la tienda esté actualizada.

{{aco-integration-environment-alignment}}

## Requisitos para utilizar la integración {#requirements-to-use-the-integration}

* [!DNL Adobe Commerce] 2.4.7+

   * PHP 8.2, 8.3 u 8.4
   * Composer 2.x

* [!DNL Adobe Commerce Optimizer] licencia con una instancia de zona protegida aprovisionada.

* [Claves de autenticación](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys) para descargar el metapaquete de conector mediante Composer.

* Acceso de administrador a [[!DNL Adobe Commerce Optimizer] instancia de zona protegida](../optimizer/get-started.md).

El usuario [!DNL Adobe Commerce] que configuró la integración debe tener:

* Acceso de administrador al administrador de Commerce.

* [Acceso desde la línea de comandos al [!DNL Adobe Commerce] servidor de aplicaciones](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/project/user-access).

* Acceso de desarrollador a la [organización de IMS] (¿https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations?) donde se aprovisiona el proyecto [!DNL Adobe Commerce Optimizer].

>[!BEGINSHADEBOX]

## Requisitos previos

Si tiene instaladas cualquiera de las siguientes extensiones, desinstálelas antes de instalar [!DNL Adobe Commerce Optimizer Connector]:

* [!DNL Adobe Commerce Live Search] (`magento/live-search`)
* [!DNL Adobe Commerce Product Recommendations] (`magento/product-recommendations`)
* [!DNL Adobe Commerce Catalog Service] (`magento/catalog-service`, `magento/catalog-service-installer`)
* Panel de administración de datos (`magento-catalog-sync-admin`)

Los datos asociados con estas extensiones siguen estando disponibles en la base de datos de Commerce. Sin embargo, no se exporta a [!DNL Adobe Commerce Optimizer] cuando el conector está habilitado. Para implementar las funcionalidades de búsqueda y comercialización proporcionadas por estas extensiones después de habilitar el conector, configúrelas desde la [[!DNL Adobe Commerce Optimizer] IU de administración](https://experienceleague.adobe.com/en/docs/commerce/optimizer/overview#quick-tour).

>[!IMPORTANT]
>
>Si estas extensiones no se quitan antes de habilitar el conector, es posible que vea pantallas de configuración rotas, datos duplicados en [!DNL Adobe Commerce Optimizer] porque los mismos datos se exportan desde el conector y las extensiones existentes, y errores 401 o 403 en los registros debido a conflictos en la forma en que las extensiones y el conector se autentican con los servicios conectados.

>[!ENDSHADEBOX]

## Pasos de configuración

Siga estos pasos para habilitar [!DNL Commerce Optimizer Connector] y comenzar a sincronizar datos de [!DNL Adobe Commerce] con su instancia de [!DNL Commerce Optimizer].

1. **[Instale el [!DNL Commerce Optimizer Connector] paquete](#install-the-adobe-commerce-optimizer-connector-package)** mediante Compositor para conectar su instancia de [!DNL Adobe Commerce] a [!DNL Adobe Commerce Optimizer].

1. **[Personalice la configuración de exportación de datos](#customize-the-commerce-scopes-export-configuration)** del administrador.

1. **[Habilitar la [!DNL Adobe Commerce Optimizer] integración](#enable-the-adobe-commerce-optimizer-integration)**.

1. **[Compruebe que la sincronización de datos funciona](#verify-that-the-data-sync-is-working)**.

## Instalar el paquete [!DNL Commerce Optimizer Connector] {#install-the-adobe-commerce-optimizer-connector-package}

[!DNL Commerce Optimizer Connector] se entrega como un metapaquete de Compositor disponible para todos los comerciantes de Commerce con una licencia activa para [!DNL Adobe Commerce Optimizer].

### Pasos de instalación

1. Agregar el módulo `adobe-commerce/commerce-data-export-aco-adapter` mediante Composer:

   ```shell
   composer require adobe-commerce/commerce-data-export-aco-adapter
   ```

1. Implementar los cambios en el entorno de ensayo [!DNL Adobe Commerce].

   Una vez finalizada la implementación, la opción [!DNL Commerce Optimizer] está disponible en el menú Administrador de Commerce. Seleccione **[!UICONTROL Commerce Optimizer]** para abrir su instancia de [!DNL Adobe Commerce Optimizer] directamente desde el administrador de Commerce.

>[!NOTE]
>
>Para obtener instrucciones detalladas sobre la instalación de extensiones, consulte las siguientes guías:
>
>[Instalar extensión en [!DNL Adobe Commerce] en la infraestructura de nube](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/configure-store/extensions)
>
>[Instalar extensión en [!DNL Adobe Commerce] local](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/extensions)

## Personalizar la configuración de exportación de los ámbitos de Commerce {#customize-the-commerce-scopes-export-configuration}

De forma predeterminada, la sincronización de datos del catálogo está habilitada para todos los ámbitos de Commerce (sitios web, grupos de clientes y vistas de tiendas). Puede personalizar la configuración de exportación para sincronizar datos solo para ámbitos específicos según sus necesidades empresariales. Por ejemplo, si tiene varias vistas de tienda que comparten el mismo idioma, puede optar por exportar los datos solo para una de las vistas de tienda y utilizarlos como el [origen de catálogo](../optimizer/setup/catalog-source.md) para varias vistas de catálogo en [!DNL Adobe Commerce Optimizer].

>[!IMPORTANT]
>
>El cambio de la configuración de exportación déclencheur una reindexación completa, que puede tardar un tiempo considerable en función del tamaño del catálogo. Adobe recomienda configurar los ámbitos de Commerce para que se sincronicen con [!DNL Adobe Commerce Optimizer] antes de habilitar la integración e iniciar la sincronización de datos inicial.

En la tabla siguiente se describen los datos que se exportan en cada nivel de ámbito:

| Ámbito | Datos exportados | Notas |
| ----- | ------------- | ----- |
| Sitio web y grupo de clientes | Precios y libros de precios | Cada conjunto de precios se exporta como un [libro de precios](../optimizer/setup/pricebooks.md) utilizando la convención de nomenclatura `<website>::<SHA1 of customer group ID>`. Se incluyen todos los grupos de clientes del sitio web. |
| Vista de tienda | Productos y atributos del producto | Cada vista de tienda crea un [origen de catálogo](../optimizer/setup/catalog-source.md) independiente en [!DNL Adobe Commerce Optimizer]. |

![Almacenar cuadrícula con configuración de sincronización de Commerce Optimizer](./assets/aco-connector-storeviews-list.png){width="600" zoomable="yes"}

**Para cambiar la configuración de un sitio web o vista de una tienda:**

1. En el Administrador de Commerce, vaya a **[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL All Stores]**.

1. Seleccione el sitio web o la vista de tienda que desee configurar.

1. En la configuración del exportador **[!DNL Adobe Commerce Optimizer]**, utilice la casilla de verificación para habilitar o deshabilitar la sincronización de datos según sea necesario.

   ![Actualizar configuración de sincronización de datos](./assets/aco-connector-storeview-export-settings.png){width="500" zoomable="yes"}

1. Guarde los cambios.

### Habilitar y deshabilitar el comportamiento

| Acción | Resultado |
| -------- | -------- |
| Deshabilitar una vista de tienda | El origen del catálogo permanece en [!DNL Adobe Commerce Optimizer], pero se han eliminado todos los datos. |
| Deshabilitar y volver a habilitar una vista de tienda | El mismo origen de catálogo se vuelve a rellenar con una resincronización de datos completa. |

## Habilitar la integración [!DNL Adobe Commerce Optimizer]

Habilite la integración e inicie la sincronización de datos ejecutando el comando CLI `aco:config:init`. Este comando completa los siguientes pasos:

1. Obtiene un token de acceso de IMS utilizando las credenciales proporcionadas como argumentos de línea de comandos.
1. Llama al servicio Commerce Cloud Manager (CCM) en `https://ccm.api.commerce.adobe.com/api/v1/tenants/{tenantId}/owner/{orgId}` para validar el inquilino y extraer la URL de ingesta y la URL de estudio [!DNL Adobe Commerce Optimizer].
1. Guarda toda la configuración (secreto de cliente cifrado) en `core_config_data`.
1. Programa la sincronización completa inicial invalidando todos los indizadores de fuentes [!DNL Commerce Optimizer].

>[!IMPORTANT]
>
>El procesamiento de la sincronización de datos se inicia en segundo plano en cuanto se completa la configuración. Según el tamaño del catálogo, el proceso de sincronización de datos puede tardar entre unos minutos y varias horas.

### Obtener los detalles de conexión necesarios

Desde [Adobe Developer Console](https://developer.adobe.com/console), cree un nuevo proyecto habilitado para el servicio de ingesta [!DNL Adobe Commerce Optimizer] y genere las credenciales de servidor a servidor de OAuth. Para obtener instrucciones detalladas, consulte [Obtener credenciales de IMS](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/authentication/#obtain-ims-credentials) en la *Guía para desarrolladores de comercialización*.

Guarde los siguientes valores desde la página de credenciales:

* **ID. de organización** (`org_id`)
* **ID de cliente** (`client_id`)
* **Secreto de cliente** (`client_secret`)

![Obtener detalles de credenciales de la página del proyecto Adobe Developer Console](./assets/developer-console-project-credentials.png){width="500" zoomable="yes"}

### Obtener detalles de instancia de [!DNL Adobe Commerce Optimizer]

Obtenga el _id. de inquilino_ del campo _[!DNL Instance Id]_&#x200B;en la instancia [!DNL Adobe Commerce Optimizer] [[!DNL Instance details] página](../optimizer/get-started.md#manage-instances), o de la URL utilizada para acceder a la instancia. Por ejemplo, en `https://experience.adobe.com/#/@<your organization>/in:<tenant ID>/commerce-optimizer-studio/home`.

1. En el Administrador de Commerce, seleccione **[!UICONTROL Adobe Commerce Optimizer]** para mostrar la página de configuración con instrucciones.

   ![[!DNL Adobe Commerce Optimizer] página de configuración](./assets/aco-connector-admin-installation.png){width="500" zoomable="yes"}

1. Desde la línea de comandos, [use SSH](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/secure-connections) para conectarse al entorno de ensayo [!DNL Adobe Commerce].

1. Ejecute el siguiente comando CLI [!DNL Adobe Commerce] para configurar la integración y reemplace los valores de marcador de posición por los valores de su proyecto [!DNL Commerce Optimizer]:

   ```terminal
   bin/magento aco:config:init --org_id=your-org --tenant_id=your-tenant --client_id=your-client-id --client_secret=your-secret
   ```

1. Compruebe la conexión volviendo al administrador de Commerce y seleccionando la opción [!UICONTROL Adobe Commerce Optimizer].

   Al seleccionar la opción, se abre la interfaz de usuario de [!DNL Adobe Commerce Optimizer] en una nueva pestaña.

## Compruebe que la sincronización de datos funciona

Puede supervisar y comprobar que la sincronización funciona desde la página [[!UICONTROL Data Feed Sync Status]](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-sync/data-feed-sync-status) disponible en el administrador.

1. **Comprobar el estado de sincronización en el administrador de Commerce:**

   Vaya a **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Data Feed Sync Status]**.

   ![Página de estado de sincronización de fuente de datos con informes de estado de elemento de fuente](./assets/data-feed-sync-status.png){width="500" zoomable="yes"}

   Cuando se está ejecutando la sincronización, los datos de la fuente muestran los registros enviados correctamente. Seleccione una fuente para ver los detalles o solucionar problemas de sincronización.

1. **Confirmar datos que llegaron en [!DNL Commerce Optimizer]:**

   En el menú [!DNL Adobe Commerce Optimizer], seleccione **[!UICONTROL Data Sync]**.

   ![Página de sincronización de datos en Adobe Commerce Optimizer que muestra datos de catálogo sincronizados](./assets/data-sync.png){width="500" zoomable="yes"}

   Compruebe que aparecen los productos, precios y atributos esperados.

>[!TIP]
>
>Si tiene algún problema con la sincronización de datos, consulte la guía [Solución de problemas](troubleshooting.md).

## Pasos siguientes

1. **Configurar [!DNL Adobe Commerce Optimizer] vistas de catálogo y directivas**

   Crear vistas de catálogo y directivas en la interfaz de usuario de [!DNL Adobe Commerce Optimizer]. Tenga en cuenta que los libros de precios se crean automáticamente a partir de [!DNL Adobe Commerce] grupos de clientes. Para obtener instrucciones, consulte la documentación de [Vistas de catálogo](../optimizer/setup/catalog-view.md) y [Directivas](../optimizer/setup/policies.md) en la Guía del usuario de *[!DNL Adobe Commerce Optimizer]*.

1. **Configurar una tienda Commerce en[!DNL Edge Delivery Services]**

   Siga la [documentación de configuración de tienda](https://experienceleague.adobe.com/developer/commerce/storefront/setup/){target="_blank"} para conectar su tienda a la instancia [!DNL Adobe Commerce Optimizer] y comenzar a ofrecer experiencias de comercio personalizadas.

