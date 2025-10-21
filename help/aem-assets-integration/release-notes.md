---
title: Notas de la versión de AEM Assets Integration
description: Revise las notas de la versión para obtener información acerca de todas las versiones de integración de AEM Assets.
feature: CMS, Media, Release Notes
exl-id: 0d639565-812f-481a-afd6-6e6fa54ed70e
source-git-commit: 141f2291d1ead324a159053145e92ee7d4237a7d
workflow-type: tm+mt
source-wordcount: '467'
ht-degree: 0%

---

# Notas de la versión de AEM Assets Integration

Estas notas de la versión describen la versión inicial de la integración de AEM Assets e incluyen:

![Nuevas](../assets/new.svg) nuevas características
![Se ha corregido un problema](../assets/fix.svg) Correcciones y mejoras
![Problema conocido](../assets/bug.svg) Problemas conocidos

Para ver los cambios y correcciones de características publicados fuera de la versión normal de la funcionalidad, consulte las secciones _Actualizaciones de servicios alojados_.

Obtenga más información acerca de las próximas versiones, la compatibilidad del producto y las versiones de Adobe Commerce que admiten la extensión de integración de AEM Assets. Consulte los temas [Programación de versiones](https://experienceleague.adobe.com/es/docs/commerce-operations/release/planning/schedule) y [Disponibilidad del producto](https://experienceleague.adobe.com/es/docs/commerce-operations/release/product-availability) de Adobe Commerce.

## Actualizaciones de servicios alojados

Estas notas de la versión describen los cambios y correcciones de características que se produjeron y que se lanzaron fuera de las versiones de funciones normales para el servicio alojado.

+++Actualizaciones de servicios alojados

_11 de septiembre de 2025_

![Nuevo problema](../assets/new.svg) actualizó los extremos [coincidencia automática personalizada](https://experienceleague.adobe.com/es/docs/commerce/aem-assets-integration/synchronize/custom-match){target=_blank} con un nuevo atributo `asset_matches`.

_11 de febrero de 2025_

![Nuevo problema](../assets/new.svg) Ahora, los comerciantes pueden sincronizar imágenes para productos y categorías.

+++

## Versión 1.2.4

_17 de octubre de 2025_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} con Adobe Commerce versión 2.4.5 y versiones posteriores.

![Se ha corregido un problema](../assets/fix.svg)<!-- Issue ACAP-1155 --> que mejoraba la estabilidad general de los atributos personalizados. Los atributos personalizados ahora se actualizan correctamente al utilizar API asincrónicas.

## Versión 1.2.3

_2 de octubre de 2025_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} con Adobe Commerce versión 2.4.5 y versiones posteriores.

![Se ha corregido un problema](../assets/fix.svg)<!-- Issue ACAP-1135 --> que provocaba que se actualizaran los atributos del producto. Los atributos del producto ahora se actualizan según lo esperado y, cuando falla la actualización, se devuelve un error correspondiente en lugar de una respuesta 200.

## Versión 1.2.2

_18 de septiembre de 2025_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} con Adobe Commerce versión 2.4.5 y versiones posteriores.

![Se corrigió un problema](../assets/fix.svg)<!-- Issue ACAP-1110 -->: se mejoró la estabilidad general de la imagen en las páginas de minicarrito, carrito y cierre de compra. Las imágenes de estas páginas ahora se cargan correctamente.

## Versión 1.2.0

_7 de agosto de 2025_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} con Adobe Commerce versión 2.4.5 y versiones posteriores.

![Nuevo problema](../assets/new.svg)<!-- Issue ACAP-1018 --> Ahora, los comerciantes pueden elegir el origen de los recursos de medios e imágenes seleccionando un [Propietario de visualización](https://experienceleague.adobe.com/es/docs/commerce/aem-assets-integration/get-started/setup-synchronization){target=_blank} al configurar la integración de Assets desde el Administrador.

![Nuevo problema](../assets/new.svg)<!-- Issue ACAP-1078 --> actualizó los extremos [coincidencia automática personalizada](https://experienceleague.adobe.com/es/docs/commerce/aem-assets-integration/synchronize/custom-match){target=_blank} con un nuevo atributo `asset_matches`. Este cambio le permite implementar su propia lógica de coincidencia para devolver todos los recursos asociados con un `productSku` específico.

## Versión 1.1.2

_11 de junio de 2025_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} con Adobe Commerce versión 2.4.5 y versiones posteriores.

![Nuevo problema](../assets/new.svg)<!-- Issue ACAP-1041 --> agregó compatibilidad con Adobe Commerce 2.4.8 y PHP 8.4.

## Versión 1.1.0

_23 de abril de 2025_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} con Adobe Commerce versión 2.4.5 y versiones posteriores.

![Nuevo problema](../assets/new.svg)<!-- Issue ACAP-955 --> Ahora se puede usar una [URL de dominio personalizado](https://experienceleague.adobe.com/es/docs/commerce/aem-assets-integration/get-started/setup-synchronization#optional-configure-the-custom-domain-url) en lugar de la URL de envío de AEM. Si un comerciante establece un **nombre de dominio personalizado** en su panel de AEM, es necesario agregar esta **URL de dominio personalizado** en Commerce.

![Se corrigió un problema](../assets/fix.svg)<!-- Issue ACAP-987 --> Se mejoraron los registros generales de los procesos de sincronización de AEM Assets.

## Versión 1.0.22

_12 de marzo de 2025_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} con Adobe Commerce versión 2.4.5 y versiones posteriores.

![Nuevo problema](../assets/new.svg)<!-- Issue ACAP-xx --> Ahora, el selector de Assets requiere el [ID de cliente IMS del selector de Assets](https://experienceleague.adobe.com/es/docs/commerce/aem-assets-integration/get-started/setup-synchronization) para habilitar la asignación de imágenes de AEM Assets con categorías de productos y contenido generado por Page Builder.

## Versión 1.0.20

_11 de febrero de 2025_

[!BADGE Compatible]{type=Informative tooltip="Admitido"} con Adobe Commerce versión 2.4.5 y versiones posteriores.

![Nuevo](../assets/new.svg)<!-- Issue ACAP-xx --> lanzamiento de disponibilidad general.
