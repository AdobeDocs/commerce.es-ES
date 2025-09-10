---
title: Instalar y configurar
description: Obtenga información sobre cómo instalar, actualizar y desinstalar  [!DNL Product Recommendations].
role: Admin, Developer
exl-id: 2e7f6454-d4cb-44bc-982f-354a179e8e59
source-git-commit: 3821893c3df01e2e36ab0142616e52c1c92b4d51
workflow-type: tm+mt
source-wordcount: '567'
ht-degree: 0%

---

# Instalar y configurar

La implementación de [!DNL Product Recommendations] en tu tienda y administrador requiere que instales el módulo y configures [Commerce Services Connector](../landing/saas.md). A medida que se lanzan las actualizaciones, puede actualizar fácilmente la instalación con la versión más reciente.

- [Instalar](#install)
- [Configurar](#configure)
- [Actualizar](#update)
- [Desinstalar](#uninstall)

## Instalar [!DNL Product Recommendations] {#install}

Dado que el módulo [!DNL Product Recommendations] es un metapaquete independiente, las actualizaciones se publican con mayor frecuencia que Adobe Commerce. Para asegurarse de que está al día con las últimas correcciones de errores y características, consulte las [notas de la versión](release-notes.md).

>[!IMPORTANT]
>
>Asegúrese de que cuenta con los [derechos](../landing/saas.md#credentials) correctos para usar las recomendaciones de productos.

Instale el módulo `magento/product-recommendations` con Composer:

```bash
composer require magento/product-recommendations
```

### Añadir compatibilidad con Page Builder {#pbsupport}

[!DNL Product Recommendations] para Page Builder es un módulo opcional y se instala por separado. Para usar [!DNL Product Recommendations] con Page Builder, instale el módulo ejecutando el siguiente comando:

```bash
composer require magento/module-page-builder-product-recommendations
```

Al habilitar [!DNL Product Recommendations] en Page Builder, puede agregar una [unidad de recomendación](https://experienceleague.adobe.com/en/docs/commerce-admin/page-builder/add-content/recommendations) activa y existente a cualquier contenido creado en Page Builder, como páginas, bloques y bloques dinámicos.

Consulte [Uso de [!DNL Product Recommendations] con contenido de Page Builder](page-builder.md) para obtener más instrucciones.

### Agregar tipo de recomendación de similitud visual {#vissimsupport}

El tipo de recomendación _Similitud visual_ le permite implementar una unidad de recomendación en la página de detalles del producto que muestra productos [visualmente similares](type.md#visualsim) al producto que se está viendo. Este tipo de recomendación es más útil cuando las imágenes y los aspectos visuales de los productos son partes importantes de la experiencia de compra. Instale el tipo de recomendación _Visual similarity_ ejecutando el siguiente comando:

```bash
composer require magento/module-visual-product-recommendations
```

## Configurar [!DNL Product Recommendations] {#configure}

1. Después de instalar el módulo `magento/product-recommendations`, configure [Commerce Services Connector](../landing/saas.md) especificando las claves de API y seleccionando un espacio de datos SaaS.

   La configuración de esta conexión permite la sincronización de datos y la comunicación entre la instancia de Commerce, el servicio de catálogo y otros servicios de soporte. La sincronización de datos está controlada por la [extensión de exportación de datos SaaS](../data-export/overview.md).

1. Para garantizar que la exportación del catálogo se pueda ejecutar correctamente, confirme que los trabajos [cron](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs) y los [indexadores](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers) se están ejecutando y que el indexador `Product Feed` está establecido en `Update by Schedule`.

Después de vincular correctamente la aplicación de Commerce a los servicios de Commerce y especificar el [espacio de datos SaaS](../landing/saas.md#saas-configuration), se inicia la sincronización del catálogo. Entonces puedes [verificar](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/verify/) que los datos de comportamiento se están enviando a tu tienda.

## Monitorización y solución de problemas de sincronización de datos

Desde Commerce Admin, puede supervisar el proceso de sincronización mediante [el tablero de administración de datos](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard). Use la [CLI de Commerce](../data-export/data-export-cli-commands.md#troubleshooting) y los registros para administrar y solucionar problemas del proceso.

Entonces puedes [verificar](https://developer.adobe.com/commerce/services/shared-services/storefront-events/collector/verify/) que los datos de comportamiento se están enviando a tu tienda.

## Actualice la instalación de [!DNL Product Recommendations] {#update}

Al igual que todo Adobe Commerce, [!DNL Product Recommendations] usa Composer para la instalación y las actualizaciones. Para actualizar el módulo `magento/product-recommendations`, ejecute lo siguiente:

```bash
composer update magento/product-recommendations --with-dependencies
```

Para actualizar a una versión principal, como de la 5.0 a la 6.0, debe editar el archivo raíz `composer.json` de su proyecto. (Vea las [notas de la versión](release-notes.md) para obtener información sobre la versión más reciente). Por ejemplo, vamos a abrir el archivo principal `composer.json` y buscar el módulo `magento/product-recommendations`:

```json
"require": {
    ...
    "magento/product-recommendations": "^5.0",
    ...
}
```

Vamos a pasar la versión principal de `5.0` a `6.0`:

```json
"require": {
    ...
    "magento/product-recommendations": "^6.0",
    ...
}
```

Guarde el archivo `composer.json` y ejecute:

```bash
composer update magento/product-recommendations --with-dependencies
```

O si ha instalado los módulos `magento/module-visual-product-recommendations` y `magento/module-page-builder-product-recommendations`:

```bash
composer update --with-dependencies magento/product-recommendations magento/module-visual-product-recommendations magento/module-page-builder-product-recommendations
```

>[!NOTE]
>
> En las versiones 3.x.x de Product Recommendations, solo necesitaba una sola clave de API. En las versiones 4.x.x y superiores, debe proporcionar claves de API públicas y privadas para los entornos de zona protegida y producción. Si no proporciona ambos pares de claves API, no puede acceder a la función Recomendaciones de productos en el Administrador. Sin embargo, la recopilación de datos continúa en su tienda y las recomendaciones existentes se siguen mostrando a los compradores.

## Cortafuegos

Para permitir que Product Recommendations pase a través de un firewall, agregue `commerce.adobe.io` a la lista de permitidos.

## Desinstalar [!DNL Product Recommendations] {#uninstall}

Si es necesario, puede [desinstalar](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/tutorials/uninstall-modules) el módulo de recomendaciones de productos.
