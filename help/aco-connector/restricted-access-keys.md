---
title: Administración de claves de acceso restringido para catálogos compartidos B2B
description: Obtenga información sobre cómo administrar las claves de acceso restringido que utiliza el conector de Adobe Commerce Optimizer para proteger las proyecciones de catálogos compartidos B2B.
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
    internal-label: Admin tools and workspace
subfeature_v2:
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
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
    internal-label: Data management
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
    internal-label: Data integration
source-git-commit: a3ade1a31d3c2905b601f71bda118de89c43cf59
workflow-type: tm+mt
source-wordcount: '1105'
ht-degree: 0%
---

# Administración de claves de acceso restringido para catálogos compartidos B2B

[!BADGE Private Beta]{type=Caution tooltip="Requiere la extensión B2B del conector de Adobe Commerce Optimizer, que actualmente se encuentra en versión beta privada."}

Si utiliza [!DNL Adobe Commerce] catálogos compartidos B2B con [!DNL Adobe Commerce Optimizer Connector B2B extension], la extensión genera y asigna automáticamente la primera clave de acceso restringido cuando se crea una vista de catálogo. Utilice la página [!UICONTROL Restricted Access Keys] del administrador de Commerce para ver esa clave y crear, asignar o eliminar claves adicionales.

![Claves de acceso restringido para vistas de catálogo compartido B2B](assets/restricted-access-keys.png){width="800" zoomable="yes"}

>[!NOTE]
>
>Para administrar las claves que cree manualmente en casos de uso que no sean B2B, como los portales de socios, consulte [Claves de acceso restringido](/help/optimizer/setup/restricted-access-keys.md#create-a-restricted-access-key).

## Acceso a la página {#access-the-page}

Desde Commerce Admin, vaya a **[!UICONTROL System]** > **[!UICONTROL Data Transfer]** > **[!UICONTROL Restricted Access Keys]**.

Puede asignar una clave a la vista de catálogo desde la cuadrícula Catálogo compartido o desde la cuadrícula Compañía. Consulte [Asignar claves a una vista de catálogo compartido B2B](#assign-keys-to-a-shared-catalog-view).

>[!NOTE]
>
>Para obtener una referencia a los campos de esta página, [Administración de claves de acceso restringido](https://experienceleague.adobe.com/es/docs/commerce-admin/systems/data-transfer/data-sync/catalog-view-sync/restricted-access-keys){target="_blank"} en la *Guía de administración de Commerce*.—>

## Cuando necesite algo más que la clave automática {#when-you-need-more-than-the-automatic-key}

La clave automática generada por [!DNL Adobe Commerce Optimizer Connector B2B extension] abarca la mayoría de los catálogos compartidos B2B sin que usted tenga que hacer nada. Administre las claves usted mismo en estos casos:

- **Rotación de una clave**: cree una clave nueva, asígnela a la vista de catálogo junto con la existente, confirme que funciona y, a continuación, elimine la clave antigua. La rotación automática aún no está disponible.
- **Una clave no se puede vincular**: si [Estado de sincronización de vista de catálogo](catalog-view-sync-status.md) muestra un desplazamiento relacionado con la clave, intente guardar de nuevo la asignación de vista de catálogo para volver a intentar el vínculo con error. Si la clave sigue fallando, ejecute [!UICONTROL Reconcile & Repair] para recuperar la clave o el estado antes de crear un reemplazo. Cree una clave de reemplazo solo si la clave ha caducado o si el error es irrecuperable de forma persistente.
- **Buscar una clave pública**: en la página Claves de acceso restringido, seleccione **[!UICONTROL View Public Key]** para ver y copiar la clave pública de una clave.

Una vista de catálogo puede tener hasta tres claves asignadas a la vez. Durante la rotación de claves, [!DNL Adobe Commerce Optimizer] acepta tokens firmados por cualquier clave asignada que no haya caducado; no hay ningún paso manual para establecer una clave &quot;activa&quot;.

## Creación de una clave

En la página [!UICONTROL Restricted Access Keys], cree una clave seleccionando **[!UICONTROL Create Key]**.

Commerce genera un nuevo par de claves y contiene la clave privada. La tabla Claves de acceso restringido se actualiza con una nueva entrada de clave que muestra el ID de clave único. Utilice este(a) [!UICONTROL Key ID] cuando asigne la clave a una vista de catálogo.

La clave pública no se registra con [!DNL Adobe Commerce Optimizer] hasta que asigne la clave a una vista de catálogo. Después del registro, la entrada de la tabla Clave de acceso restringido se actualiza para mostrar la asignación del catálogo y la fecha de caducidad.

## Asignar claves a una vista de catálogo proyectada desde un catálogo compartido B2B {#assign-keys-to-a-shared-catalog-view}

Asigne o anule la asignación de claves desde la vista de catálogo desde la cuenta de la compañía o la página del catálogo compartido, no desde la cuadrícula principal de [!UICONTROL Restricted Access Keys].

Una vista de catálogo debe tener al menos una clave y puede tener como máximo tres.

- Si intenta asignar una cuarta clave, recibirá un mensaje de error cuando intente guardar el valor: `A Catalog View can have at most 3 access keys.`
- Si una vista de catálogo sólo tiene una clave, ésta no se puede eliminar ni anular.

Para actualizar la configuración de la clave de vista de catálogo, puede acceder a ella desde la página de cuenta de la empresa o desde la página de catálogo compartido.

>[!BEGINTABS]

>[!TAB Administrar claves desde una cuenta de compañía]

1. En el Administrador de Commerce, abra la página de la compañía (**[!UICONTROL Customers]** > **[!UICONTROL Companies]**).

1. En la columna [!UICONTROL Action] de la compañía, seleccione [!UICONTROL Edit].

1. Para ver la lista de vistas de catálogo proyectadas desde el catálogo compartido asignado a la compañía, expanda la sección _[!UICONTROL Catalog Views]_.

La pestaña enumera las vistas de catálogo proyectadas desde el catálogo compartido, incluidas sus claves asignadas.

1. En la columna [!UICONTROL Actions] para que la vista de catálogo se actualice, seleccione **[!UICONTROL Edit Restricted Access Keys]**.

   ![Editar la lista desplegable de claves de acceso restringido que muestra las claves asignadas a una vista de catálogo](assets/restricted-access-key-selector.png){width="500" zoomable="yes"}

1. Para asignar una clave, seleccione la lista desplegable **[!UICONTROL Access Keys]**. A continuación, seleccione una clave sin asignar por parte de [!UICONTROL key ID], por ejemplo `#42`. A continuación, haga clic en [!UICONTROL Done] para asignarlo a la vista de catálogo.

   Las claves ya asignadas a una vista de catálogo diferente se etiquetan como corresponda.

1. Para quitar un token de acceso, quítelo del campo [!UICONTROL Access Tokens] seleccionando el control `x` en la etiqueta de clave.

1. Para guardar y aplicar las actualizaciones de configuración, seleccione **[!UICONTROL Save]**.

>[!TAB Administrar claves de un catálogo compartido]

1. En el Administrador de Commerce, abra la página del catálogo compartido (**[!UICONTROL Catalog]** > **[!UICONTROL Shared catalogs]**).

1. En la columna [!UICONTROL Action] del recurso compartido, elija **[!UICONTROL General Settings]** en el menú [!UICONTROL Select].

1. Para ver la lista de vistas de catálogo proyectadas desde el catálogo compartido, seleccione **[!UICONTROL Catalog Views]** del menú [!UICONTROL Shared Catalog Information].

La página [!UICONTROL Catalog Views] muestra el identificador de vista de catálogo, la vista de tienda asociada y la clave de acceso para cada vista de catálogo.

1. En la columna [!UICONTROL Actions] para que la vista de catálogo se actualice, seleccione **[!UICONTROL Edit Restricted Access Keys]**.

   ![Editar la lista desplegable de claves de acceso restringido que muestra las claves asignadas a una vista de catálogo](assets/restricted-access-key-selector.png){width="500" zoomable="yes"}

1. Para asignar una clave, seleccione la lista desplegable **[!UICONTROL Access Keys]**. A continuación, seleccione una clave sin asignar por el título de clave predeterminado, por ejemplo `#42`. A continuación, haga clic en [!UICONTROL Done] para asignarlo a la vista de catálogo.

   Las claves ya asignadas a una vista de catálogo diferente se etiquetan como corresponda.

1. Para quitar un token de acceso, quítelo del campo [!UICONTROL Access Tokens] seleccionando el control `x` en la etiqueta de clave.

1. Para guardar y aplicar las actualizaciones de configuración, seleccione **[!UICONTROL Save]**.

>[!ENDTABS]

## Administrar la caducidad y renovación de claves

Puede configurar la duración predeterminada de las claves para las claves de acceso restringido. El valor determina la fecha de caducidad establecida cuando la extensión [!DNL Adobe Commerce Optimizer Connector B2B] genera la clave inicial o cuando se crea una nueva clave manualmente.

La fecha de caducidad se muestra en la columna [!UICONTROL Expires At] de la página [!UICONTROL Restricted Access Keys].

Para cambiar la duración, vaya a **[!UICONTROL Stores]** > [!UICONTROL Settings] > **[!UICONTROL Configuration]** > **[!UICONTROL Services]** > **[!UICONTROL ACO Restricted Access Keys]**. En la página [!UICONTROL Provisioning], actualice el campo **[!UICONTROL Default Key Expiry (days)]**. La duración predeterminada de la clave del sistema se establece inicialmente para un período prolongado (~100 años). Asegúrese de actualizarlo a un valor que coincida con sus directivas de seguridad.

### Renovación de clave

Cuando una clave está dentro de los 10 días de caducidad, la página [!UICONTROL Restricted Access Keys] muestra un icono de advertencia junto a su entrada. Si no renueva la clave antes de que caduque, no podrá acceder a la vista del catálogo hasta que asigne una clave nueva.

Puede crear y asignar una clave nueva en cualquier momento y eliminar la anterior después de confirmar que la clave nueva funciona.

## Limitaciones conocidas

La rotación automática de claves aún no está disponible.

>[!MORELIKETHIS]
>
> - [Administrar claves de acceso restringido](https://experienceleague.adobe.com/es/docs/commerce-admin/systems/data-transfer/data-sync/catalog-view-sync/restricted-access-keys){target="_blank"} — Referencia de campo completo para esta página, en la *Guía de administración de Commerce* —>
> - [Supervisar sincronización de vista de catálogo](catalog-view-sync-status.md) — Supervisar las vistas de catálogo que estas claves protegen
> - [Vistas de catálogo privado](/help/optimizer/setup/private-catalog-view.md) — Descubra qué es una vista de catálogo privado administrada por conectores
> - [Claves de acceso restringido](/help/optimizer/setup/restricted-access-keys.md): aprenda cómo funciona el flujo de claves manual basado en ACO Studio para casos de uso que no son B2B
