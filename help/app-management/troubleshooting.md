---
title: Solución de problemas [!DNL App Management]
description: Resuelva los problemas comunes con la asociación y configuración de la aplicación.
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
source-git-commit: 76e77db86adecdbd3be76040970c0d0899c34cdc
workflow-type: tm+mt
source-wordcount: '217'
ht-degree: 0%
---
# Solución de problemas [!DNL App Management]

Utilice las siguientes soluciones para resolver los problemas comunes con la asociación y configuración de la aplicación.

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

Para obtener más información sobre la solución de problemas técnicos, consulte [Extensibilidad de Commerce [!DNL App Management]](https://developer.adobe.com/commerce/extensibility/app-management/){target="_blank"}.
