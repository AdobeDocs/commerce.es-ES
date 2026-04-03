---
title: Notas de la versión [!DNL Adobe Commerce Optimizer Connector]
description: La información de la versión más reciente de  [!DNL Adobe Commerce Optimizer Connector]  para Adobe Commerce.
feature: Services, Catalog Service, Release Notes
source-git-commit: 205fca38b379f94027a965b58826ffd922577f61
workflow-type: tm+mt
source-wordcount: '219'
ht-degree: 0%

---

# Notas de la versión de Adobe Commerce Optimizer Connector

Estas notas de la versión describen todas las versiones para [!DNL Adobe Commerce Optimizer Connector] e incluyen:

![Nuevas](../assets/new.svg) nuevas características
![Se ha corregido un problema](../assets/fix.svg) Correcciones y mejoras
![Problema conocido](../assets/bug.svg) Problemas conocidos

## Versiones de 2026

### Versión 1.0.12

_2 de abril de 2026_

![Nuevo](../assets/new.svg) **Se ha agregado compatibilidad con la fuente Categorías en el comando `saas:resync` **-Ahora puede actualizar y ver fácilmente los datos de categoría más recientes mediante el comando CLI `saas:resync`:

```terminal
bin/magento saas:resync --feed=categories
```

_10 de marzo de 2026_

![Se ha corregido un problema](../assets/fix.svg) de compatibilidad que bloqueaba el acceso a la página de configuración del Conector de servicios de Commerce desde los menús Administrador del sistema y Configuración de Commerce cuando el Conector de Adobe Commerce Optimizer está instalado en una instancia de Commerce.  Ahora puede acceder a la página de configuración de Commerce Services Connector cuando ambas extensiones están instaladas. <!--MDEE-1322-->


### Versión 1.0.10

_9 de marzo de 2026_

![Corrección](../assets/fix.svg): Si accede a la página Estado de sincronización de fuentes de datos antes de completar la configuración del conector, ahora se le redirigirá automáticamente a la página de configuración del conector. Este flujo guiado garantiza que la instalación del conector se complete y ayuda a evitar errores causados por la falta de opciones de configuración que podrían dar como resultado elementos de estado incompletos o con errores.<!--MDEE-1296-->

### Versión v1.0.9

_1 de marzo de 2026_

Versión de disponibilidad general de Adobe Commerce Optimizer Connector.

>[!NOTE]
>
>Si ha participado en el programa Beta para el conector de Adobe Commerce Optimizer y tiene instalada una versión anterior de la extensión, actualice a la versión de disponibilidad general para recibir las actualizaciones más recientes.

