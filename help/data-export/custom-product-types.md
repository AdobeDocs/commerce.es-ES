---
title: Compatibilidad con tipos de producto personalizados en la exportación de datos del catálogo SaaS
description: Descubra cómo el módulo de habilitación del catálogo Commerce Storefront MCP permite que la exportación de datos SaaS represente tipos de productos de terceros personalizados y no reconocidos como productos simples en datos de catálogo enviados a Live Search y al servicio de catálogo.
role: Admin, Developer
hide: true
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
feature_v2:
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
topic_v2:
  - id: d3cdead0-685a-4489-9250-4bb709942f66
    internal-label: Data collection
source-git-commit: fd87417a494987f33009d386019d870b306dcf73
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%
---
# Compatibilidad con tipos de productos personalizados en la exportación de datos del catálogo SaaS

>[!IMPORTANT]
>
>La compatibilidad con los tipos de productos personalizados se encuentra actualmente en **Acceso anticipado** como parte de [!DNL Commerce Storefront MCP]. Este módulo es compatible con las versiones de Adobe Commerce 2.4.4 y posteriores. Los requisitos de disponibilidad, embalaje e instalación están sujetos a cambios antes de la disponibilidad general. Para solicitar una invitación para este **acceso anticipado**, envíe un mensaje de correo electrónico a [commerceeap@adobe.com](mailto:commerceeap@adobe.com). El equipo de Adobe responderá con los siguientes pasos y los requisitos de idoneidad.

## Información general

[!DNL SaaS Data Export] reconoce los tipos de producto estándar de Adobe Commerce (simple, configurable, paquete, etc.) cuando prepara los datos de catálogo para servicios de Commerce conectados, como [Live Search](../live-search/overview.md) y [Servicio de catálogo](../catalog-service/overview.md). Las extensiones de terceros pueden introducir **tipos de productos personalizados** que [!DNL SaaS Data Export] no reconoce de forma nativa.

El módulo de habilitación del catálogo MCP de Commerce Storefront permite que [!DNL SaaS Data Export] represente estos tipos de productos personalizados no reconocidos como **productos simples** en la carga útil del catálogo saliente, de modo que los compradores que usen [!DNL Commerce Storefront MCP] puedan descubrirlos a través de servicios respaldados por catálogo.

## Ámbito del comportamiento

- El módulo de habilitación del catálogo MCP de Commerce Storefront no cambia el tipo de producto almacenado en Adobe Commerce. La representación de un tipo de producto personalizado como producto simple sólo se aplica a los datos de catálogo enviados a [!DNL Live Search] y [!DNL Catalog Service].
- No se requiere ninguna configuración de administración o de tiempo de ejecución. Los tipos de producto estándar siguen exportándose normalmente.
- El módulo se dirige a tipos de productos personalizados introducidos por extensiones de terceros, no a los tipos de productos estándar de Commerce.

## Instalación del módulo

Para habilitar el módulo de habilitación del catálogo MCP de Commerce Storefront, ejecute lo siguiente desde la línea de comandos:

```bash
composer require magento/module-storefront-mcp-enablement --no-update
composer update magento/module-storefront-mcp-enablement --with-dependencies
bin/magento setup:upgrade
```

## Sincronización de los datos del catálogo

La instalación del módulo no cambia los datos de producto subyacentes en Adobe Commerce, por lo que los elementos de tipo de producto personalizados existentes no se reexportan automáticamente. Para aplicar la nueva representación de producto simple a los datos de catálogo que ya estaban sincronizados antes de instalar el módulo, vuelva a sincronizar manualmente los datos de catálogo. Ver [Sincronizar datos manualmente](data-sync-manage.md#manually-resync-data).
