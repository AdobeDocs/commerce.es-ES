---
title: Administre su aplicación
description: Asocie, configure y desasocie aplicaciones de App Builder con su instancia de Commerce.
feature: App Builder, Extensibility, Integration
source-git-commit: ab635fecb7b82294bd4a4fd045ed71931e9d265d
workflow-type: tm+mt
source-wordcount: '420'
ht-degree: 0%

---


# Administre su aplicación

Un administrador de aplicaciones asocia una aplicación de App Builder con su instancia de Commerce. Los formularios de configuración se representan de forma dinámica en función del esquema de la aplicación, por lo que no se requiere el desarrollo de la IU de administración personalizada. El administrador de aplicaciones configura las opciones a través de formularios que Commerce genera automáticamente.

![Administración de aplicaciones](assets/app-management-ui.png){width="500" zoomable="yes"}

## Requisitos previos

Antes de asociar una aplicación, asegúrese de que dispone de lo siguiente:

| Requisito | Descripción |
|-------------|-------------|
| **Acceso de administrador** | Administrador de Commerce con permisos para [!DNL App Management] |
| **Aplicación implementada** | Aplicación de App Builder implementada en su organización y lista para conectarse |
| **Acceso a la organización** | Acceso a la organización de Adobe donde se implementa la aplicación |

## Tutorial

Vea este vídeo para aprender a asociar una aplicación a una instancia de Commerce y configurar opciones.

>[!VIDEO](https://video.tv.adobe.com/v/3478958?captions=spa)

## Asociar una aplicación

El proceso de asociación importa sitios web, tiendas y vistas de tiendas desde Commerce y crea el vínculo entre la aplicación y la instancia de Commerce.

Para vincular la aplicación de App Builder a una instancia de Commerce:

1. Vaya a **[!UICONTROL Apps]** > **[!UICONTROL App Management]**.

1. Haga clic en **[!UICONTROL Associate App]**.

   ![Asociar aplicación](assets/associate-app.png){width="500" zoomable="yes"}

1. Seleccione un(a) **[!UICONTROL Project]** de la lista.

1. Seleccione **[!UICONTROL Workspace]**.

1. Haga clic en **[!UICONTROL Associate]**.

   ![Detalles de la aplicación](assets/app-details.png){width="500" zoomable="yes"}

>[!WARNING]
>
>Si la sincronización del ámbito falla, la asociación se completa. Puede sincronizar los ámbitos manualmente más adelante desde la vista **[!UICONTROL Manage Scopes]** en la configuración de la aplicación asociada.

## Configurar opciones

Después de asociar una aplicación en la vista [!DNL App Management], configure su configuración mediante el formulario:

1. Haga clic en **[!UICONTROL Configure]** en la aplicación asociada.

1. El formulario muestra la configuración de la aplicación.

1. Modifique los valores según sea necesario.

1. Haga clic en **[!UICONTROL Save]**.

### Configuración específica del ámbito

Utilice una configuración específica del ámbito cuando diferentes sitios web, tiendas o vistas de tiendas necesiten una configuración única. Por ejemplo, habilite una función solo para una región o vista de tienda específica, o use diferentes configuraciones por marca. La configuración de un ámbito inferior anula la de los ámbitos superiores.

Para anular los valores globales en un nivel de ámbito específico:

1. Haga clic en **[!UICONTROL Change Scope]**.

1. Seleccione un ámbito de la lista.

1. Modifique los valores de este ámbito.

1. Haga clic en **[!UICONTROL Save]**.

## Administrar ámbitos

Acceda a **[!UICONTROL Manage Scopes]** desde la pantalla de detalles de la aplicación para administrar la jerarquía de ámbito de la aplicación.

![Administrar ámbitos](assets/manage-scopes.png){width="500" zoomable="yes"}

| Acción | Descripción |
|--------|-------------|
| **[!UICONTROL Add root scope]** | Agregue un ámbito que se aplique únicamente a la aplicación. |
| **[!UICONTROL Sync Commerce scopes]** | Actualice la lista de sitios web, tiendas y vistas de tiendas desde Commerce después de agregarlos o cambiarlos. |
| **[!UICONTROL Import scopes]** | Importar ámbitos de forma masiva desde un archivo. |

## Desasociar una aplicación

Cancele la asociación de una aplicación cuando ya no la necesite conectada a su instancia de Commerce. Por ejemplo, es posible que tenga que retirar una integración, cambiar a un espacio de trabajo diferente o limpiar las configuraciones de prueba.

>[!WARNING]
>
> Al desasociar, se eliminan todos los valores de configuración de esta instancia. Esta acción no puede deshacerse.

Para eliminar una aplicación de una instancia de Commerce:

1. Vaya a **[!UICONTROL Apps]** > **[!UICONTROL App Management]**.

1. Haga clic en **[!UICONTROL Unassociate]** en la aplicación.

1. Confirme la acción.

## Documentación relacionada

* [Solución de problemas [!DNL App Management]](troubleshooting.md): resuelva problemas comunes con la asociación y configuración de la aplicación.
