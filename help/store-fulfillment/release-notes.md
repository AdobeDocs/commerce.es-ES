---
title: Notas de la versión [!DNL Store Fulfillment by Walmart Commerce Technologies]
description: Revise las notas de la versión para obtener información acerca de todas las  [!DNL Store Fulfillment by Walmart Commerce Technologies] versiones.
role: Admin, User, Leader
feature: Shipping/Delivery, Release Notes
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '488'
ht-degree: 0%

---

# Notas de la versión

Estas notas de la versión describen la versión inicial de [!DNL Store Fulfillment Services by Walmart Commerce Technologies] e incluyen:

![Nuevas](../assets/new.svg) nuevas características
![Se ha corregido un problema](../assets/fix.svg) Correcciones y mejoras
![Problema conocido](../assets/bug.svg) Problemas conocidos

Consulte [Próximas versiones](https://experienceleague.adobe.com/docs/commerce-operations/release/planning/schedule.html?lang=es) para obtener más información sobre las programaciones de versiones y la compatibilidad.

Consulte [Disponibilidad del producto](https://experienceleague.adobe.com/docs/commerce-operations/release/product-availability.html?lang=es) para saber qué versiones de Adobe Commerce admiten esta extensión.

## Versión 1.5.0

*3 de agosto de 2023*

[!BADGE Compatible]{type=Informative tooltip="Admitido"}[Adobe Commerce 2.4.4 a 2.4.6](https://experienceleague.adobe.com/docs/commerce-operations/release/product-availability.html?lang=es), incluidas las revisiones de seguridad 2.4.6-p1, 2.4.5-p3 y 2.4.4-p4

Esta versión incluye las siguientes actualizaciones:

![Nuevo](../assets/fix.svg) Se ha actualizado la extensión para admitir [versiones de parches de seguridad de Adobe Commerce](https://experienceleague.adobe.com/docs/commerce-operations/release/notes/security-patches/overview.html?lang=es) 2.4.6-p1, 2.4.5-p3 y 2.4.4-p4.

![Nuevo](../assets/new.svg)<!-- WMTP-918 --> agregó compatibilidad con la opción de configuración [Envío asincrónico](sales-emails.md) para correos electrónicos de ventas. Los comerciantes que actualicen a la versión 1.5.0 tienen la opción de enviar correos electrónicos inmediatamente (predeterminado) o de forma asíncrona.

![Nuevo](../assets/new.svg)<!-- WMTP-916--> actualizó la [configuración de orígenes](merchant-store-configuration.md) para admitir formatos de número de teléfono internacional.

![Nuevo](../assets/new.svg) Se ha agregado lógica para evitar que los importes de reembolso excedan el importe restante o facturado.

![Nuevo](../assets/new.svg)<!-- WMTP-882 --> reemplazó el objeto `google.map.LatLng` con literales JSON para admitir la compatibilidad con versiones anteriores de [!DNL Google Maps].

![Se ha corregido un problema](../assets/fix.svg)<!-- WMTP- --> Se ha actualizado el script que crea los atributos de producto `[!DNL Available for Store Pickup]` y `[!DNL Available for Home Delivery]` para evitar conflictos de categoría de atributos.

![Se ha corregido un problema](../assets/fix.svg)<!-- WMTP-915 --> que causaba un bucle interminable al cargar y guardar algunas entidades.

![Se ha corregido un problema](../assets/fix.svg)<!-- WMTP-921 --> que impedía que la validación del presupuesto de [!DNL Ship to Store] se activara cuando se agregaba un elemento al carro de compras desde una página de detalles del producto (PDP).

![Se ha corregido un problema](../assets/fix.svg)<!-- WMTP- 932 --> que provocaba que se cerrara la compra y que permitía a los clientes seleccionar el método de entrega a domicilio para los artículos que no cumplen los requisitos para la entrega a domicilio.

![Se corrigió un problema](../assets/fix.svg) Actualizaciones de instalación:

- &#x200B;<!-- WMTP-880--> Se ha corregido un problema que provocaba que se devolviera un código de sitio web incorrecto al instalar la extensión [!DNL Store Fulfillment].

- &#x200B;<!-- WMTP-878--> Se ha corregido un problema con los números enteros de SKU que requería que el tipo de datos se convirtiera en tipo de cadena durante la instalación.

![Se ha corregido un problema](../assets/fix.svg)<!-- WMTP-915--> que provocaba que faltara un código de error de protección.

![Se corrigió un problema](../assets/fix.svg)<!-- WMTP-932 -->. Se corrigió un error relacionado con el rechazo parcial durante las operaciones de dispensación.

![Nuevo](../assets/new.svg)<!-- WMTP-953 --> Se ha actualizado el extremo de la API Cancel para que consuma el parámetro de estado como un objeto opcional.

![Nuevo](../assets/new.svg)<!-- WMTP-960 --> detalles de registro mejorados para el extremo de API de Dispense.

## Versión 1.4.0

*13 de abril de 2023*

[!BADGE Compatible]{type=Informative tooltip="Admitido"}

![Nuevo](../assets/fix.svg) [!DNL Store Fulfillment] es ahora [compatible con [!DNL Adobe Commerce] 2.4.4 a 2.4.6](https://experienceleague.adobe.com/docs/commerce-operations/release/product-availability.html?lang=es).


## Versión 1.3.0

*27 de febrero de 2023*

[!BADGE Compatible]{type=Informative tooltip="Admitido"}

Esta versión incluye la siguiente actualización:

![Nuevo](../assets/fix.svg)<!-- WMTP-795 --> agregó la capacidad de deshabilitar la solución Store Fulfillment para un sitio específico cambiando el ámbito predeterminado de la configuración del sistema de sitio web a global.

## Versión 1.2.0

*27 de septiembre de 2022*

[!BADGE Compatible]{type=Informative tooltip="Admitido"}

Esta versión incluye la siguiente actualización:

![Nuevo](../assets/fix.svg) [!DNL Store Fulfillment] es ahora [compatible con [!DNL Adobe Commerce] 2.4.4 a 2.4.5](https://experienceleague.adobe.com/docs/commerce-operations/release/product-availability.html?lang=es).


## Versión 1.1.0

*15 de julio de 2022*

[!BADGE Compatible]{type=Informative tooltip="Admitido"}

Estabilidad: disponibilidad general

![Nuevo](../assets/fix.svg)<!-- WMTP-731 --> ha simplificado la [configuración de la experiencia de registro](check-in-experience-setup.md) para la aplicación Store Assist al agregar selecciones predeterminadas de modelo y fabricación de automóviles. En la versión anterior, los comerciantes tenían que configurar manualmente la marca del coche y las selecciones del modelo.

## Versión 1.0.0

*4 de marzo de 2022*

[!BADGE Compatible]{type=Informative tooltip="Admitido"}

Estabilidad: disponibilidad general

## Aplicación Store Assist

Para obtener información sobre las nuevas versiones de la aplicación Store Assist, consulte la información de la aplicación en [Apple App Store](https://apps.apple.com/us/app/store-assist-by-walmart/id1609281539){target="_blank"} o en [Google Play store](https://play.google.com/store/apps/details?id=com.walmart.faas.storeassist){target="_blank"}.
