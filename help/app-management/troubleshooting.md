---
title: Solución de problemas [!DNL App Management]
description: Resuelva los problemas comunes con la asociación, instalación, configuración y actualizaciones de la aplicación.
feature: App Builder, Extensibility, Integration
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 72863f3c-9d27-5dda-afe1-d9f934b1fba0
    internal-label: Extensibility
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: cc250cf1-34eb-4863-80d0-d170d45ea067
    internal-label: Developer tools
subfeature_v2:
  - id: a743e5dc-8f37-4b5d-a848-03c32ca30598
    internal-label: App Builder
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
source-git-commit: a00b9e1654a572e1773b5b7e321683332882d86f
workflow-type: tm+mt
source-wordcount: '648'
ht-degree: 0%
---
# Solución de problemas [!DNL App Management]

Utilice las siguientes soluciones para resolver los problemas comunes con la asociación, instalación, configuración y actualizaciones de la aplicación.

## Antes de ponerse en contacto con el proveedor de aplicaciones

Siga los pasos de su problema a continuación. Si necesita ayuda del desarrollador o del proveedor de la aplicación, recopile la siguiente información:

* Nombre de la aplicación y versión instalada, si están disponibles en **[!UICONTROL Manage]** > **[!UICONTROL Details]** en la tarjeta de la aplicación.
* Instancia de Commerce y organización de Adobe afectadas.
* Operación que ha fallado, como instalación o actualización, y el paso que ha fallado.
* Se muestra un mensaje de error y una captura de pantalla del error, si está disponible.
* Hora aproximada del error, incluida la zona horaria.
* Cualquier reintento y sus resultados.

## La aplicación no se muestra

Si la aplicación no aparece en la lista después de la implementación, compruebe los siguientes pasos:

1. Compruebe que la aplicación esté implementada y disponible en su organización.

1. Confirme que ha iniciado sesión en la organización correcta de Adobe en Developer Console.

1. Asegúrese de que la aplicación esté lista para conectarse (el desarrollador de la aplicación o su socio pueden confirmarla).

Si la aplicación sigue sin aparecer, póngase en contacto con el desarrollador de aplicaciones o consulte la [Extensibilidad de Commerce [!DNL App Management]](https://developer.adobe.com/commerce/extensibility/app-management/){target="_blank"} para obtener información técnica.

## Error de sincronización de ámbito

Si la sincronización del ámbito falla al asociar una aplicación, intente lo siguiente:

1. Compruebe que la instancia de Commerce esté accesible y en línea.

1. Compruebe que las credenciales de la API son válidas y que tienen los permisos correctos.

1. Intente sincronizar manualmente desde **[!UICONTROL Manage Scopes]** en la configuración de la aplicación.

## Configuración no guardada

Si los cambios de configuración no se guardan, intente lo siguiente:

1. Compruebe que todos los campos obligatorios estén rellenados y sean válidos.

1. Asegúrese de que tiene los permisos correctos para modificar la configuración de la aplicación.

1. Actualice la página y vuelva a guardar los cambios.

Si el problema persiste, compruebe si la consola del explorador tiene errores o póngase en contacto con el desarrollador de la aplicación.

## La instalación falla

Mantenga la página de instalación abierta sin actualizar hasta que finalice la instalación. Si la cierra o la actualiza, es posible que la instalación no se complete correctamente.

Si la instalación informa de un error:

1. Tenga en cuenta el elemento fallido y cualquier mensaje de error mostrado.

1. Compruebe que ha completado las instrucciones de preinstalación de la aplicación.

1. Pida al desarrollador de aplicaciones que inspeccione el paso con error y corrija la causa antes de intentar la instalación de nuevo.

Una instalación fallida puede dejar algunos cambios aplicados. Cuando se vuelve a intentar la instalación, se omiten los pasos personalizados registrados como correctos; los pasos fallidos o interrumpidos pueden volver a ejecutarse. Pida al desarrollador que compruebe los recursos creados por la ejecución parcial.

## Error de actualización

Una actualización fallida puede dejar algunas operaciones aplicadas. No desasocie ni vuelva a instalar la aplicación como un paso de recuperación rutinario, ya que la desasociación elimina la configuración y puede ejecutar scripts de limpieza destructivos.

1. Identifique el paso fallido y registre cualquier mensaje de error mostrado.

1. Pida al desarrollador de aplicaciones que inspeccione los registros, compruebe los cambios ya realizados en Commerce o en recursos externos y corrija la causa.

1. En [!DNL App Management], seleccione **[!UICONTROL Retry Upgrade]**. Esta acción está disponible tanto para los modos de actualización manual como automática.

Cada reintento crea un nuevo plan a partir del estado actual. Los pasos de instalación personalizados registrados como correctos se omiten; los pasos erróneos o interrumpidos se pueden ejecutar de nuevo. En modo automático, volver a implementar la aplicación también déclencheur otro intento de actualización.

Si los intentos repetidos fallan, pida al desarrollador de la aplicación que conserve los ID de ejecución o intento y cualquier ID de activación de ejecución para la resolución de problemas. Para ver los comandos de estado, el historial de intentos y los registros de tiempo de ejecución, consulte [Reintentar una actualización fallida](https://developer.adobe.com/commerce/extensibility/app-management/upgrade-app/#retry-a-failed-upgrade){target="_blank"} en la documentación para desarrolladores.

## Los recursos permanecen después de una actualización

Al eliminar un paso de instalación personalizada de la configuración de una aplicación, no se ejecuta su script de desinstalación ni se eliminan los recursos que ha creado. El plan de actualización advierte de que no se ejecuta ningún script para el paso eliminado y este no aparece en la pantalla de progreso ni en los detalles de la aplicación después de la actualización.

Pida al desarrollador de aplicaciones que confirme si los recursos siguen siendo necesarios y que realice una migración para limpieza cuando sea necesario. Consulte [Actualizar una aplicación](manage-app.md#upgrade-an-app) para el flujo de trabajo del administrador.

Para obtener más información sobre la solución de problemas técnicos, consulte [Extensibilidad de Commerce [!DNL App Management]](https://developer.adobe.com/commerce/extensibility/app-management/){target="_blank"}.
