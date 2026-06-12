---
title: Notas de la versión [!DNL Adobe Commerce Optimizer Connector]
description: Obtenga información acerca de  [!DNL Adobe Commerce Optimizer Connector] notas de la versión, incluidas las nuevas características, las correcciones de errores y los problemas conocidos de la sincronización y exportación del catálogo.
feature: Release Notes
TQID: 'https://experienceleague.adobe.com/6NeLAfThvIWIyV4Y6OWtL8V9mC7lPy7UH-Zli8E-WEk'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
subfeature_v2:
  - id: dad884f1-e840-49a1-970e-2f965bdbc410
  - id: a40ebd6b-b542-4432-a730-1803ef74518d
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: af45543a52d1c88149574dc22cdef37af01404c8
workflow-type: tm+mt
source-wordcount: 353
ht-degree: 0%

---

# Notas de la versión de Adobe Commerce Optimizer Connector

Estas notas de la versión describen todas las versiones para [!DNL Adobe Commerce Optimizer Connector] e incluyen:

![Nuevas](../assets/new.svg) nuevas características
![Se corrigió el problema](../assets/fix.svg) Correcciones y mejoras
![Problema conocido](../assets/bug.svg) Problemas conocidos

## Versiones de 2026

### Versión 1.0.14

_11 de junio de 2026_

![Corrección](../assets/fix.svg) **Compatibilidad con PHP 8.5** - [!DNL Adobe Commerce Optimizer Connector] ahora es compatible con PHP 8.5, por lo que puede actualizar su entorno [!DNL Adobe Commerce] sin interrumpir la funcionalidad del conector o la sincronización del catálogo. <!--MDEE-1388-->

![Corrección](../assets/fix.svg) **Los libros de precios se actualizan después de cambiar de divisa** - Los precios actualizados se reflejan automáticamente en Adobe Commerce Optimizer después de cambiar de divisa. <!--MDEE-1384-->

![Corrección](../assets/fix.svg) **La navegación respeta las categorías principales deshabilitadas u ocultas**: los productos de las jerarquías de categorías deshabilitadas u ocultas ya no aparecen inesperadamente en las experiencias de navegación.<!--MDEE-1385-->

![Corregir](../assets/fix.svg) **URL de categoría coherentes después de las actualizaciones de ensayo**: los vínculos de categoría y la navegación siguen siendo precisos después de aplicar las actualizaciones de ensayo. <!--MDEE-1395-->

### Versión 1.0.13

_6 de mayo de 2026_

![Corrección](../assets/fix.svg) **Se mejoraron las instrucciones de configuración de [!DNL Adobe Commerce Optimizer Connector]** - Se ha actualizado la página de configuración de [!DNL Adobe Commerce Optimizer] en el administrador de Commerce para vincular a la guía de integración de _[!DNL Adobe Commerce Optimizer Connector]_.
<!--COMOPT-1922-->

![Corrección](../assets/fix.svg) **[!DNL Adobe Commerce Optimizer Connector]mejora de metadatos**: [!DNL Adobe Commerce Optimizer Connector] ahora incluye su versión instalada en el encabezado de metadatos. Esta mejora permite a los equipos identificar rápidamente qué versión del conector se está usando durante la solución de problemas o las contrataciones de soporte técnico.<!--MDEE-1323-->

### Versión 1.0.12

_2 de abril de 2026_

![Nuevo](../assets/new.svg) **Se ha agregado compatibilidad con la fuente Categorías en el comando `saas:resync`**. Ahora puede actualizar y ver fácilmente los datos de categoría más recientes mediante el comando CLI `saas:resync`:

```terminal
bin/magento saas:resync --feed=categories
```

### Versión 1.0.11

_10 de marzo de 2026_

![Se ha corregido un problema](../assets/fix.svg) que bloqueaba el acceso a la página de configuración de [!DNL Commerce Services Connector] desde los menús de administración de Commerce **[!UICONTROL System]** y **[!UICONTROL Configuration]** cuando [!DNL Adobe Commerce Optimizer Connector] estaba instalado en una instancia de [!DNL Adobe Commerce].  Ahora puede acceder a la página de configuración de [!DNL Commerce Services Connector] cuando ambas extensiones estén instaladas. <!--MDEE-1322-->


### Versión 1.0.10

_9 de marzo de 2026_

![Corrección](../assets/fix.svg) Si accede a la página **[!UICONTROL Data Feed Sync Status]** antes de completar la configuración del conector, ahora se le redirigirá automáticamente a la página de configuración del conector. Este flujo guiado garantiza que la instalación del conector se complete y ayuda a evitar errores causados por la falta de opciones de configuración que podrían dar como resultado elementos de estado incompletos o con errores.<!--MDEE-1296-->

### Versión v1.0.9

_1 de marzo de 2026_

Versión de disponibilidad general de [!DNL Adobe Commerce Optimizer Connector].

>[!NOTE]
>
>Si ha participado en el programa Beta para [!DNL Adobe Commerce Optimizer Connector] y tiene instalada una versión anterior de la extensión, actualice a la versión de disponibilidad general para recibir las actualizaciones más recientes.
