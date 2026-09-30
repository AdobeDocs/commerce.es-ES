---
title: Buscar actualizaciones de extensión
description: Descubra cómo Adobe Commerce busca y notifica a los administradores sobre las nuevas versiones de la extensión de integración de AEM Assets, incluida la comprobación manual de CLI.
feature: CMS, Media
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
    internal-label: Metadata
source-git-commit: 7950f5d171b35054be42ca60d19bafcf43c53cd6
workflow-type: tm+mt
source-wordcount: '297'
ht-degree: 4%
---
# Buscar actualizaciones de la extensión

Con la versión 1.4.6 y posteriores de la extensión de integración de AEM Assets, Adobe Commerce comprueba automáticamente si hay una versión más reciente de la extensión disponible y se lo comunica a los administradores en el Administrador. Esta comprobación se ejecuta de forma asíncrona como parte del procesamiento programado y no bloquea la representación de la página de administración.

## Funcionamiento de la comprobación de actualizaciones

* La comprobación de actualizaciones compara la versión del paquete `aem-assets-integration` instalado con la versión compatible más alta disponible en [repo.magento.com](https://repo.magento.com/admin/dashboard).
* Los resultados se almacenan en caché. Al cargar una página de administración, se lee el resultado almacenado en caché más reciente en lugar de activar una solicitud de red activa.
* Si `repo.magento.com` no está disponible o los metadatos devueltos no son válidos, Commerce mantiene el último resultado almacenado en caché correcto y no bloquea al administrador.

>[!NOTE]
>
>La comprobación de actualización está diseñada para implementaciones de Adobe Commerce en la nube y locales.

## Ver notificaciones de actualización

Los administradores pueden ver una notificación de actualización disponible en cualquier ubicación:

* **[!UICONTROL Stores]** > [!UICONTROL Settings] > **[!UICONTROL Configuration]** > **[!UICONTROL Adobe Services]** > **[!UICONTROL AEM Assets Integration]**
* El menú desplegable de notificaciones del administrador

Cada notificación muestra:

* La versión instalada
* La versión disponible
* La clasificación de versiones
* Un vínculo a las notas de la versión

Seleccione **[!UICONTROL Remind me later]** para posponer la notificación de esta instancia de Commerce o desactivar por completo las notificaciones de actualización.

## Ejecute una comprobación de actualización manual

Para buscar una actualización disponible inmediatamente, ejecute el siguiente comando desde el directorio raíz de Commerce:

```bash
bin/magento aem:assets:check-update
```

Este comando solo comprueba e informa de una actualización disponible. No modifica los archivos del Compositor ni implementa una actualización. Para instalar una actualización, siga las instrucciones del Compositor en [Instalar paquetes de Adobe Commerce](configure-commerce.md).

## Metadatos de versiones para paquetes de extensiones

La comprobación de actualización lee los metadatos de la versión de la sección `extra` del archivo `composer.json` del paquete instalado:

```json
{
  "extra": {
    "release_notes_url": "https://experienceleague.adobe.com/...",
    "release_type": "feature",
    "compatible_commerce_versions": ">=2.4.7 <2.5.0"
  }
}
```

## Siguiente paso

* [Instalación de paquetes de Adobe Commerce](configure-commerce.md)
