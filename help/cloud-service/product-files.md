---
title: Añadir archivos a los productos
description: Aprenda a adjuntar archivos como PDF, manuales y hojas de datos a productos mediante atributos de producto de tipo de archivo en  [!DNL Adobe Commerce as a Cloud Service].
feature: Catalog Management, Products, Integration
role: Admin, Developer
level: Intermediate
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
source-git-commit: 848ba518d170c9a0270b2513fdc8efb6813f6845
workflow-type: tm+mt
source-wordcount: '607'
ht-degree: 0%

---

# Añadir archivos a los productos

[!DNL Adobe Commerce as a Cloud Service] admite un &quot;archivo&quot; [tipo de entrada de atributo de producto](https://experienceleague.adobe.com/es/docs/commerce-admin/catalog/product-attributes/attributes-input-types){target="_blank"} que permite a los comerciantes adjuntar archivos, como PDF, manuales, certificados y hojas de datos directamente a los productos. Los archivos se almacenan en el almacenamiento de medios de Amazon S3 y se puede acceder a ellos a través de la tienda mediante GraphQL o a través de integraciones mediante la API de REST.

Existen tres formas de cargar archivos en los atributos del archivo de producto:

* [IU de administración](#upload-through-the-admin) - Cargar archivos manualmente en la página de edición del producto.
* [API de REST](#upload-through-the-rest-api): cargue archivos a través de la API de REST mediante direcciones URL prefirmadas S3.
* [Importación de productos](#upload-through-product-import): importe archivos de forma masiva proporcionando direcciones URL externas en CSV.

## Requisitos previos

Antes de cargar archivos, debe crear un atributo de archivo y asignarlo a un conjunto de atributos.

* [Crear un atributo de archivo](https://experienceleague.adobe.com/es/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create){target="_blank"} - Establecer **[!UICONTROL Catalog Input Type for Store Owner]** en **[!UICONTROL File]**.

* [Asignar el atributo a un conjunto de atributos](https://experienceleague.adobe.com/es/docs/commerce-admin/catalog/product-attributes/create/attribute-sets#create-an-attribute-set){target="_blank"} - Arrastre el nuevo atributo de archivo al grupo deseado.

* Configure los tipos de archivo permitidos y el tamaño en la configuración de [Atributos de archivo de producto](https://experienceleague.adobe.com/es/docs/commerce-admin/config/catalog/product-file-attributes).

## Cargar archivos mediante el administrador

Después de [crear un atributo de archivo](https://experienceleague.adobe.com/es/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create){target="_blank"} y asignarlo a un conjunto de atributos, puede cargar archivos directamente desde la página de edición del producto.

1. En la barra lateral _Admin_, vaya a **[!UICONTROL Catalog]** > **[!UICONTROL Products]**.

1. Abra el producto que desea editar.

1. Busque el campo de atributo de archivo y haga clic en **[!UICONTROL Upload]** para seleccionar un archivo.

![Botón Cargar archivo en el administrador](./assets/upload-file.png){width="600" zoomable="yes"}

1. Haga clic en **[!UICONTROL Save]**.

Para reemplazar un archivo, elimine el archivo existente y cargue uno nuevo. El archivo cargado se almacena en el almacenamiento de medios de Amazon S3.

## Cargar mediante la API de REST

Use el [flujo de URL prefirmado S3](https://developer.adobe.com/commerce/webapi/rest/saas-integrations/s3-uploads/){target="_blank"} para cargar archivos mediante programación a través de la API de REST. Este proceso funciona del mismo modo para los atributos de archivo de producto que para otros tipos de medios, como imágenes de categoría y archivos de atributos del cliente.

El proceso consta de cuatro pasos:

1. Llame a `POST V1/media/initiate-upload` con el nombre de archivo y `media_resource_type` para los atributos del archivo de producto.
1. Use la URL prefirmada devuelta para `PUT` el archivo directamente en Amazon S3.
1. Llame a `POST V1/media/finish-upload` para confirmar la carga.
1. Asigne la clave devuelta al atributo file del producto mediante `PUT /V1/products/{sku}`, pasando la clave como el valor [atributo personalizado](https://developer.adobe.com/commerce/webapi/rest/modules/custom-attributes/).

## Cargar mediante importación de producto

Puede adjuntar archivos a productos de forma masiva mediante la [API de importación](https://developer.adobe.com/commerce/webapi/rest/modules/import/){target="_blank"} o la IU de importación de administración. Los atributos del archivo de producto solo admiten la importación desde direcciones URL externas, que sigue el mismo método que el [Método 2 para la importación de imágenes de producto](https://experienceleague.adobe.com/es/docs/commerce-admin/systems/data-transfer/import/data-import-product-images#method-2-import-images-from-external-server){target="_blank"}. Commerce descarga el archivo desde la dirección URL proporcionada y lo guarda en el almacenamiento de medios S3.

>[!NOTE]
>
>No se admite la importación de archivos desde una ruta de acceso de servidor local (Método 1) en [!DNL Adobe Commerce as a Cloud Service] porque no hay acceso directo al sistema de archivos.

### Proporcione la dirección URL en una columna dedicada

Utilice el código de atributo como encabezado de columna CSV y la dirección URL completa como valor. Por ejemplo, si el código de atributo es `file_upload`, el CSV tendría este aspecto:

```csv
sku,name,file_upload
ADB112,"My Product",https://example.com/files/manual.pdf
```

### Proporcione la dirección URL en `additional_attributes`

Como alternativa, incluya el atributo de archivo en la columna `additional_attributes`:

```csv
sku,name,additional_attributes
ADB112,"My Product",file_upload=https://example.com/files/manual.pdf
```

En ambos casos, la dirección URL debe ser de acceso público, y la extensión y el tamaño del archivo deben cumplir con las [limitaciones configuradas](https://experienceleague.adobe.com/es/docs/commerce-admin/config/catalog/product-file-attributes){target="_blank"}.

## Recuperación de archivos mediante GraphQL

En [!DNL Adobe Commerce as a Cloud Service], el extremo [Catalog Service GraphQL](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/){target="_blank"} proporciona datos de productos. Los atributos de archivo aparecen en el campo `attributes` en `ProductView`, con `value` que contiene la dirección URL pública completa del archivo:

```graphql
{
  products(skus: ["ADB112"]) {
    sku
    name
    attributes(roles: []) {
      name
      label
      value
    }
  }
}
```

La respuesta incluye el atributo del archivo con su URL pública:

```json
{
  "data": {
    "products": [
      {
        "sku": "ADB112",
        "name": "Example product",
        "attributes": [
          {
            "name": "file",
            "label": "FILE",
            "value": "https://<host>/media/catalog/product_file/manual.pdf",
          }
        ]
      }
    ]
  }
}
```

>[!NOTE]
>
>Esta consulta requiere los encabezados `Magento-Website-Code` y `Magento-Store-View-Code`. Para obtener más información, consulte la [consulta de productos del servicio de catálogo](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/queries/products/){target="_blank"}.

## Recuperación de archivos mediante la API de REST

Al recuperar un producto a través de la [API REST](https://developer.adobe.com/commerce/webapi/reference/rest/saas/){target="_blank"} (`GET /V1/products/{sku}`), los atributos de archivo aparecen en la matriz `custom_attributes` con el nombre de archivo como valor:

```json
{
  "custom_attributes": [
    {
      "attribute_code": "file_upload",
      "value": "manual_7aa0b2d63f6d3dbf.pdf"
    }
  ]
}
```
