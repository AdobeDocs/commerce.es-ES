---
title: '[!DNL Adobe Commerce Optimizer Connector] módulos y extremos de fuente'
description: Obtenga información sobre  [!DNL Adobe Commerce Optimizer Connector] módulos, puntos finales de API de fuentes de catálogo, límites de lotes y rutas de configuración core_config_data para [!DNL Adobe Commerce].
feature: Integration, Configuration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."
autotag-review: '2026-06-09T15:48:19.494Z'
TQID: 'https://experienceleague.adobe.com/UM6Y-xoQpUDzWpaMe1GRPp4XoAtHBLBsHw388kumN8g'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: e7dae43f-215c-4cdf-90d3-c5a461a6e669
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 19de20caafd45e3a00896d0d4b29b7e96dfe94e1
workflow-type: tm+mt
source-wordcount: 301
ht-degree: 1%

---

# Módulos de conector y extremos de fuente para el conector de Adobe Commerce Optimizer

Esta referencia enumera los paquetes de módulos [!DNL Adobe Commerce Optimizer Connector], los extremos de API de fuentes compatibles y las rutas de acceso de claves de configuración almacenados en `core_config_data`. Para saber cómo funcionan juntos estos componentes durante la sincronización, consulte [Canalización de sincronización de conectores](../connector-sync-pipeline.md).

## Módulos

El conector incluye varios módulos de Magento que recopilan datos de catálogo, asignan datos de fuente al formato admitido por la API [!DNL Commerce Optimizer] y administran el envío y el control de ámbito. La siguiente tabla resume cada módulo y su función.

| Módulo | Rol |
| ------ | ---- |
| `DataExporterAdapter` | Asigna [!DNL Adobe Commerce] fuentes al formato requerido por la API [!DNL Adobe Commerce Optimizer]. Anula la configuración del esquema y el grupo de fuentes. |
| `SaasExportAdapter` | Enruta las fuentes [!DNL Commerce Optimizer] a la API de ingesta y bloquea el envío de las fuentes no admitidas. |
| `CommerceAcoExporter` | Administra las credenciales de [!DNL Commerce Optimizer] y proporciona comandos de configuración de CLI |
| `CommerceAdapter` | [!DNL Commerce Optimizer] capa de compatibilidad de API (GraphQL, paquete, complemento al carro, interfaz de usuario de configuración) |
| `PriceBookDataExporter` | Fuente de libro de precios indexada por sitio web y grupo de clientes |
| `SaasPriceBook` | Infraestructura SaaS para la presentación de la cartera de precios |
| `CommerceOptimizerScopeMapper` | Habilitación de la sincronización por sitio web y vista de tienda |

## Fuentes compatibles

El conector envía varios tipos de fuentes a [!DNL Commerce Optimizer] [[!DNL Catalog Data Ingestion API]](https://developer.adobe.com/commerce/services/optimizer/data-ingestion/){target="_blank"}. En la tabla siguiente se muestra cada fuente con su extremo, límite de lotes, nombre de indizador y tabla de fuentes en [!DNL Adobe Commerce].

| Fuente | Extremo de API [!DNL Commerce Optimizer] | Límite de lotes | Nombre de índice de AC | Tabla de fuentes |
| ---- | ----------------------------------- | ----------- | ------------- | ---------- |
| `products` | `POST /v1/catalog/products` | 100 | `catalog_data_exporter_products` | `cde_products_feed` |
| `categories` | `POST /v1/catalog/categories` | 100 | `catalog_data_exporter_categories` | `cde_categories_feed` |
| `productAttributes` | `POST /v1/catalog/products/metadata` | 100 | `catalog_data_exporter_product_attributes` | `cde_product_attributes_feed` |
| `prices` | `POST /v1/catalog/products/prices` | 500 | `catalog_data_exporter_product_prices` | `cde_product_prices_feed` |
| `priceBooks` | `POST /v1/catalog/price-books` | 500 | `data_exporter_price_books` | `cde_price_books_feed` |

Las fuentes `products`, `productAttributes`, `categories` y `prices` reutilizan los datos recopilados por los indizadores [!DNL SaaS Data Export]. El conector genera la fuente `priceBooks` a partir de la configuración del sitio web y del grupo de clientes y no depende de un indizador [!DNL SaaS Data Export].

Para obtener detalles de asignación de nivel de campo para cada fuente, consulte [Asignación de campo para [!DNL Commerce Optimizer Connector] fuentes](field-mapping.md).
Para calcular cuánto tiempo tardará una sincronización en función del tamaño del catálogo, consulte [Estimar el volumen de datos y el tiempo de sincronización](estimate-data-volume-sync-time.md).

## Rutas de configuración

Las credenciales de [!DNL Commerce Optimizer Connector] y las direcciones URL del servicio se almacenan en `core_config_data` bajo el prefijo de ruta de acceso de `aco_exporter/general/`. Ejecute `bin/magento aco:config:show` para revisar los valores actuales. El comando no muestra el secreto de cliente.

```text
aco_exporter/general/org_id
aco_exporter/general/tenant_id
aco_exporter/general/client_id
aco_exporter/general/client_secret       (encrypted)
aco_exporter/general/type
aco_exporter/general/ingestion_url
aco_exporter/general/optimizer_studio_url
```
