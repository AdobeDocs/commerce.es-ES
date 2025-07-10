---
title: Extensión de adaptador de catálogo
description: Uso del adaptador de catálogo para representar los precios de los servicios de Commerce
seo-title: Catalog Adapter Extension
seo-description: Using Catalog Adapter to render prices from Commerce Services
exl-id: e42101fa-9c30-482c-a649-44dc35376abb
source-git-commit: 74f6cb64724194651c4eeb538c0c69142b01ac5d
workflow-type: tm+mt
source-wordcount: '715'
ht-degree: 0%

---

# Adaptador de catálogo

La extensión `[!DNL Catalog Adapter]` deshabilita el indizador de precios de producto predeterminado incluido en la aplicación Commerce y, en su lugar, utiliza los precios proporcionados por el [servicio de catálogo](../catalog-service/overview.md).

El adaptador está diseñado para funcionar con la [exportación de datos SaaS](../data-export/overview.md) y el servicio Adobe Commerce. La exportación de datos de SaaS es responsable de enviar los precios y [!DNL Catalog Adapter] recupera todos los precios del servicio de Adobe Commerce.

Al habilitar [!DNL Catalog Adapter], las operaciones y la indexación de precios se ven afectadas de las siguientes maneras:

- El indexador de precios incluido en la aplicación Adobe Commerce está desactivado.
- Los precios se administran usando la exportación de datos SaaS y el [indexador de precios SaaS](price-indexing.md).
- Cuando un cliente abre un producto, una categoría u otra página que muestra los precios de los productos, los precios se recuperan del servicio de Adobe Commerce.
- Los precios se envían al servicio Adobe Commerce sincronizando los datos de [exportación de datos SaaS](../data-export/overview.md).
- El cierre de compra vuelve a calcular los precios dinámicamente.

Puede volver a activar la indexación de precios en la aplicación Commerce si elimina o desactiva la extensión del adaptador de catálogo.

## Requisitos

- Adobe Commerce 2.4.4+
- El entorno de Adobe Commerce debe tener habilitado y configurado uno de los siguientes servicios de Commerce:

   - [Live Search](../live-search/install.md)
   - [Recomendaciones de productos](../product-recommendations/install-configure.md)
   - [Servicio de catálogo](../catalog-service/installation.md)

## Instalación

La extensión del adaptador de catálogo es un metapaquete de Composer que instala los siguientes módulos:

- **Desactivador del indexador de precios**: este módulo deshabilita el índice de precios en la aplicación Commerce para que los precios se entreguen mediante la indexación de precios SaaS. El indexador de precios de producto de la aplicación Commerce no se puede activar cuando se instala la extensión de indexación de precios SaaS.
- **Proveedor de precios**: este módulo proporciona precios para productos del servicio Adobe Commerce. Forma la consulta de búsqueda y obtiene los precios de los productos en el front-end.
- **Adaptador de búsqueda del servicio de catálogo**- Este módulo transfiere precios de la aplicación Adobe Commerce a un servicio Adobe Commerce en respuesta a una solicitud de búsqueda de producto.

## Pasos de instalación

>[!BEGINTABS]

>[!TAB Infraestructura en la nube]

Utilice este método para instalar [!DNL Catalog Adapter] para una instancia de Commerce Cloud.

1. En la estación de trabajo local, cambie al directorio del proyecto para su proyecto de Adobe Commerce en la nube.

   >[!NOTE]
   >
   >Para obtener información sobre cómo administrar los entornos de proyecto de Commerce localmente, consulte [Administración de ramas con la CLI](https://experienceleague.adobe.com/es/docs/commerce-cloud-service/user-guide/develop/cli-branches) en la _Guía del usuario de Adobe Commerce on Cloud Infrastructure_.

1. Consulte la rama de entorno para actualizar con la CLI de Adobe Commerce Cloud.

   ```shell
   magento-cloud environment:checkout <environment-id>
   ```

1. Añada el módulo Adaptador de catálogo.

   ```bash
   composer require magento/catalog-adapter --no-update
   ```

1. Actualizar dependencias del paquete.

   ```bash
   composer update "magento/catalog-adapter"
   ```

1. Confirme y envíe los cambios de código para los archivos `composer.json` y `composer.lock`.

1. Agregue, confirme e inserte los cambios de código para los archivos `composer.json` y `composer.lock` en el entorno de nube.

   ```shell
   git add -A
   git commit -m "Add catalog adapter module"
   git push origin <branch-name>
   ```

   Si se insertan las actualizaciones en el entorno de la nube, se inicia el [proceso de implementación de la nube de Commerce](https://experienceleague.adobe.com/es/docs/commerce-cloud-service/user-guide/develop/deploy/process) para aplicar los cambios. Compruebe el estado de implementación desde el [registro de implementación](https://experienceleague.adobe.com/es/docs/commerce-cloud-service/user-guide/develop/test/log-locations#deploy-log).

>[!TAB Local]

Utilice este método para instalar [!DNL Catalog Adapter] para una instancia local.

1. Añada el adaptador de catálogo al proyecto mediante Composer:

   ```bash
   composer require magento/catalog-adapter --no-update
   ```

1. Actualice las dependencias e instale la extensión:

   ```bash
   composer update  "magento/catalog-adapter"
   ```

1. Actualizar Adobe Commerce:

   ```bash
   bin/magento setup:upgrade
   ```

1. Borre la caché:

   ```bash
   bin/magento cache:clean
   ```

   >[!TIP]
   >
   >En algunos casos, especialmente al implementar en producción, puede que desee evitar borrar el código compilado, ya que puede tardar algún tiempo. Asegúrese de realizar una copia de seguridad del sistema antes de realizar cualquier cambio.

>[!ENDTABS]


## Volver a habilitar el indexador de precios de productos de Adobe Commerce

Si tiene aplicaciones de terceros que dependen del indexador de precios de producto predeterminado de Adobe Commerce, puede volver a activarlo con los siguientes comandos:

```bash
# re-enable Product Price indexer
bin/magento module:disable Magento_PriceIndexerDisabler
# re-index Product Price indexer
bin/magento index:reindex catalog_product_price
```

## Deshabilitar indizador de precios de productos para escenario de tienda sin encabezado

Si tiene una instancia de Commerce sin encabezado, es posible que tenga que deshabilitar el indexador de precios de productos de Adobe Commerce para reducir la carga en la instancia de Adobe Commerce. Puede completar esta tarea instalando el módulo `magento/module-price-indexer-disabler`:

```bash
composer require magento/module-price-indexer-disabler
```

## Escenarios de uso

Los siguientes son algunos escenarios comunes de `[!DNL Catalog Adapter]`.

### Sin dependencias en el indexador de precios de productos Adobe Commerce

- Es un comerciante de Luma o Adobe Commerce Core GraphQL que tiene instalado un servicio requerido (Live Search, Product Recommendations, Servicio de catálogo)
- No hay integraciones con extensiones de terceros que dependan del indexador de precios de productos de Adobe Commerce

1. Instale [!DNL Catalog Adapter].

### Con dependencias del indexador de precios de productos Adobe Commerce

- Es un comerciante de Luma o Adobe Commerce Core GraphQL que tiene instalado un servicio compatible (Live Search, Product Recommendations, Servicio de catálogo)
- Utilice una extensión de terceros que dependa del indexador de precios de productos de Adobe Commerce

1. Instale [!DNL Catalog Adapter].
1. Vuelva a habilitar el indizador de precios de producto predeterminado de Adobe Commerce.

### Instancias de Commerce sin encabezado

- Un comerciante con una instancia de Commerce sin encabezado con los servicios necesarios instalados (Live Search, Product Recommendations, Servicio de catálogo)
- No se depende del indexador de precios de producto predeterminado de Adobe Commerce

1. Instale el módulo `magento/module-price-indexer-disabler` desde el paquete [!DNL Catalog Adapter].
