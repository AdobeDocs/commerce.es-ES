---
title: Configuración del conector para B2B Commerce
description: Obtenga información sobre cómo instalar el conector B2B, seleccionar ámbitos de Commerce, sincronizar datos de catálogo compartidos, comprobar vistas de catálogo y supervisar el estado de la proyección.
feature: Integration, Configuration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."
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
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
subfeature_v2:
  - id: e126554b-28f9-4290-b58c-10b888b88174
    internal-label: IMS integration
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
    internal-label: Data Transfer
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
    internal-label: Personalization
last-update: 2026-09-11
source-git-commit: a3ade1a31d3c2905b601f71bda118de89c43cf59
workflow-type: tm+mt
source-wordcount: '843'
ht-degree: 0%
---

# Configuración del conector para B2B Commerce

Los comerciantes que usen [!DNL Adobe Commerce] catálogos compartidos B2B pueden usar [!DNL Adobe Commerce Optimizer Connector for B2B] para sincronizar datos y configuración de catálogo compartido personalizado con [!DNL Adobe Commerce Optimizer].

{{aco-integration-environment-alignment}}

## Requisitos para utilizar la integración {#requirements-to-use-the-integration}

* Adobe Commerce 2.4.8+ con [Commerce B2B versión 1.5.3+](https://experienceleague.adobe.com/en/docs/commerce-admin/b2b/install) instalado y habilitado.

* Licencia de [!DNL Commerce Optimizer] con instancia de zona protegida aprovisionada.

* [Claves de autenticación](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys) para descargar el metapaquete del conector mediante Composer.

* Acceso de administrador a [[!DNL Commerce Optimizer] instancia de zona protegida](../optimizer/get-started.md).

El usuario [!DNL Adobe Commerce] que configuró la integración debe tener:

* Acceso de administrador al administrador de Commerce.

* [Acceso desde la línea de comandos al [!DNL Adobe Commerce] servidor de aplicaciones](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/project/user-access).

* Acceso de desarrollador a la [organización de IMS] (¿https://experienceleague.adobe.com/en/docs/core-services/interface/administration/organizations?) donde se aprovisiona el proyecto [!DNL Commerce Optimizer].

### Requisitos de aplicación

* Commerce cron e indexadores funcionan normalmente.
* Se han identificado los sitios web y las vistas de tienda necesarios para la exportación.
* Catálogos compartidos, asignaciones de la empresa, variedad y precios B2B configurados o listos para configurar en Adobe Commerce.

>[!BEGINSHADEBOX]

## Eliminar extensiones en conflicto {#remove-conflicting-extensions}

{{$include /help/_includes/aco-connector/remove-conflicting-extensions.md}}

>[!ENDSHADEBOX]

## Pasos de configuración {#configuration-steps}

Para habilitar [!DNL Adobe Commerce Optimizer Connector for B2B] y comenzar a sincronizar la configuración del catálogo compartido personalizado de [!DNL Adobe Commerce] a su instancia de [!DNL Commerce Optimizer], siga estos pasos.

1. **[Instale el [!DNL Adobe Commerce Optimizer Connector for B2B] paquete](#install-the-adobe-commerce-optimizer-connector-for-B2B-package)** mediante Compositor para conectar su instancia de [!DNL Adobe Commerce] a [!DNL Commerce Optimizer].

1. **[Personalizar la configuración de exportación de los ámbitos de Commerce](#data-export-and-scope-mapping)** desde el administrador.

1. **[Habilitar la [!DNL Commerce Optimizer] integración](#enable-the-adobe-commerce-optimizer-integration)**.

1. **[Compruebe que la sincronización de datos funciona](#verify-that-the-data-sync-is-working)**.

## Instalar el paquete [!DNL Adobe Commerce Optimizer Connector for B2B] {#install-the-adobe-commerce-optimizer-connector-for-B2B-package}

[!DNL Adobe Commerce Optimizer Connector for B2B] se entrega como un metapaquete de Compositor disponible para todos los comerciantes de Commerce con una licencia activa para [!DNL Commerce Optimizer].

### Pasos de instalación

1. Agregar el módulo `adobe-commerce/commerce-data-export-aco-adapter-b2b` mediante Composer:

   ```shell
   composer require adobe-commerce/commerce-data-export-aco-adapter-b2b
   ```

1. Implementar los cambios en el entorno de ensayo [!DNL Adobe Commerce].

   Una vez finalizada la implementación, la opción [!DNL Commerce Optimizer] está disponible en el menú Administrador de Commerce. Seleccione **[!UICONTROL Commerce Optimizer]** para abrir su instancia de [!DNL Commerce Optimizer] directamente desde el administrador de Commerce.

{{install-extension-links}}

### Exportación de datos y asignación de ámbito

Seleccione los sitios web y las vistas de la tienda que desea sincronizar y, a continuación, compruebe las fuentes iniciales. Para B2B, el conector utiliza los ámbitos habilitados cuando proyecta datos de catálogo compartidos a [!DNL Commerce Optimizer].

* **Vista de tienda** → origen de catálogo con contenido de producto localizado
* **El sitio web y el grupo de clientes** → el precio del sitio web y el grupo de clientes
* **El catálogo compartido** → una vista de catálogo privado protegido y una directiva aplicada

El catálogo compartido define el surtido de productos y cada vista de tienda habilitada proporciona el origen de catálogo localizado. El sitio web y el grupo de clientes determinan el libro de precios aplicable. El conector proyecta cada catálogo compartido personalizado para cada vista de tienda habilitada, por lo que no necesita un ajuste de ámbito independiente para la proyección B2B.

Un catálogo compartido personalizado puede generar varias vistas de catálogo privado protegido, una para cada vista de tienda habilitada. El catálogo compartido público predeterminado no se proyecta como una vista de catálogo privado B2B. Para obtener información detallada sobre la asignación de objetos y el flujo de autorización de tiempo de ejecución, consulte [proyección del catálogo compartido B2B](b2b-shared-catalog-projection.md).

>[!IMPORTANT]
>
>Cambiar la configuración de exportación déclencheur una reindexación completa, que puede tardar un tiempo considerable según el tamaño del catálogo. Configure los ámbitos de Commerce antes de habilitar la integración e iniciar la sincronización de datos inicial.

### Para cambiar la configuración de exportación del ámbito

1. En el Administrador de Commerce, vaya a **[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL All Stores]**.

1. Seleccione el sitio web o la vista de tienda que desee configurar.

1. En la configuración del exportador **[!DNL Commerce Optimizer]**, utilice la casilla de verificación para habilitar o deshabilitar la sincronización de datos según sea necesario.

   ![Actualizar configuración de sincronización de datos](./assets/aco-connector-b2b-storeview-list.png){width="500" zoomable="yes"}

1. Guarde los cambios.

### Habilitar y deshabilitar el comportamiento

| Acción | Resultado |
| -------- | -------- |
| Deshabilitar una vista de tienda | **Al deshabilitar la sincronización, se eliminan los datos del catálogo de la tienda B2B.** El origen del catálogo permanece en [!DNL Adobe Commerce Optimizer], pero todos los datos sincronizados se eliminan en la siguiente ejecución de cron. |
| Deshabilitar y volver a habilitar una vista de tienda | El mismo origen de catálogo se vuelve a rellenar con una resincronización de datos completa. |

### Monitorización de cambios en el catálogo compartido B2B

El conector observa los cambios en los catálogos compartidos y las asignaciones de la empresa. Cuando se elimina un catálogo compartido en el administrador de Commerce, el conector elimina el acceso a su vista de catálogo privado después de un período de gracia configurable.

>[!NOTE]
>
>El período de gracia de eliminación es de siete días de forma predeterminada. Puede cambiarla actualizando la configuración de sincronización de la vista de catálogo. Ver [configuración del estado de sincronización de vista de catálogo](catalog-view-sync-status.md#configure-aco-catalog-view-sync-settings).

## Habilitar la integración [!DNL Commerce Optimizer] {#enable-the-adobe-commerce-optimizer-integration}

Habilite la integración e inicie la sincronización de datos ejecutando el comando CLI `aco:config:init`. Este comando completa los siguientes pasos:

1. Obtiene un token de acceso de IMS utilizando las credenciales proporcionadas como argumentos de línea de comandos.
1. Llama al servicio Commerce Cloud Manager (CCM) en `https://ccm.api.commerce.adobe.com/api/v1/tenants/{tenantId}/owner/{orgId}` para validar el inquilino y extraer la URL de ingesta y la URL de estudio [!DNL Commerce Optimizer].
1. Guarda toda la configuración (secreto de cliente cifrado) en `core_config_data`.
1. Programa la sincronización completa inicial invalidando todos los indizadores de fuentes [!DNL Commerce Optimizer].

{{aco-data-sync-processing-note}}

## Obtener los detalles de conexión necesarios

{{$include /help/_includes/aco-connector/connection-details.md}}

### Obtener detalles de instancia de [!DNL Commerce Optimizer]

{{$include /help/_includes/aco-connector/configure-connection.md}}

## Compruebe que la sincronización de datos funciona {#verify-that-the-data-sync-is-working}

{{$include /help/_includes/aco-connector/verify-optimizer-data-sync.md}}

## Pasos siguientes

1. **Supervisar la proyección de la vista del catálogo B2B**

Después de la sincronización inicial de la fuente, use [Estado de sincronización de vista de catálogo](catalog-view-sync-status.md) para comprobar las vistas de catálogo privado proyectadas, las directivas, las referencias de libro de precios y la configuración de clave de acceso restringido. Para el modelo de proyección y el flujo de autorización de tiempo de ejecución, consulte [proyección del catálogo compartido B2B](b2b-shared-catalog-projection.md).

1. **Configurar una tienda Commerce en[!DNL Edge Delivery Services]**

   Para conectar tu tienda a la instancia [!DNL Commerce Optimizer] y comenzar a ofrecer experiencias de comercio personalizadas, sigue la [documentación de configuración de tienda](https://experienceleague.adobe.com/en/tools/commerce-storefront/setup/){target="_blank"}.
