---
title: Notas de la versión [!DNL Catalog Adapter]
description: La información de la versión más reciente de  [!DNL Catalog Adapter]  para Adobe Commerce.
feature: Services, Release Notes
recommendations: noCatalog
roles: Admin, Developer
exl-id: d4dd0288-8853-43fe-9103-1aead8d3b56e
source-git-commit: 47419e7e19611dc4a045c195f259e2126ab77372
workflow-type: tm+mt
source-wordcount: '197'
ht-degree: 0%

---

# Notas de la versión de la extensión [!DNL Catalog Adapter]

Estas notas de la versión describen las versiones más recientes de la extensión [!DNL Catalog Adapter]. Se proporciona soporte para la versión publicada principal actual. Las notas de la versión de las versiones anteriores se proporcionan como referencia.

Las actualizaciones incluyen:

![Nuevas](../assets/new.svg) nuevas características
![Corrección](../assets/fix.svg) Correcciones y mejoras
![Error](../assets/bug.svg) Problemas conocidos


>[!NOTE]
>
>La [extensión del adaptador de catálogo](catalog-adapter.md) deshabilita la indización de precios de Adobe Commerce. Si lo ha instalado, puede comprobar la versión instalada en su sistema con Composer. En algunos casos, es posible que desee actualizar la extensión del adaptador de catálogo en el sistema para recoger correcciones o nuevas funciones sin actualizar la versión del servicio de Commerce.

## Versión principal actual

## Versión 1.0.10

![Corrección](../assets/fix.svg) Se ha corregido un problema en el cual las consultas de precios para productos de paquete importados o recién creados podían provocar errores internos del servidor porque el sistema intentó usar un SKU concatenado para la búsqueda en lugar del SKU válido y correcto. Las consultas de precios para los productos agrupados ahora utilizan el SKU apropiado y se resuelven correctamente.<!--MDEE-1040-->

## Versión 1.0.9

![Corrección](../assets/fix.svg) Se agregó compatibilidad con PHP 8.4. <!--MDEE-941-->

## Versión 1.0.8

![Corrección](../assets/fix.svg) Se ha corregido un problema que provocaba un error en el registro de excepciones al agregar variantes de productos configurables con SKU numéricas a la lista de deseos. <!--MDEE-876-->
