---
title: Añadir atributos de producto de forma dinámica
description: Obtenga información sobre cómo añadir atributos de producto personalizados a fuentes de exportación de datos de forma dinámica durante el proceso de sincronización de datos.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
exl-id: d5ed7497-4be1-440a-a567-81b64fdc54fc
TQID: https://experienceleague.adobe.com/SZWtLSvxb-w-968f4wqWrPTBn1c9IEuthvhIv86Pvss
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047id: b974b164-8a4e-43b8-a9e2-8e67ec131677id: cdf0c6dd-1717-4e20-9530-a24eee57088bid: de2e2e68-c5d7-4efe-be7b-27528698f06b
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
topic_v2: id: a004cc84-67b9-4a33-a3a7-8ec7273ef4dc
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 267
ht-degree: 0%

---

# Añadir atributos de producto de forma dinámica

Puede ampliar los atributos de producto sin registrarlos en [!DNL Adobe Commerce] creando un complemento para agregar los atributos durante el proceso de sincronización de datos.

>[!NOTE]
>
>La mejor manera de ampliar los atributos del producto es [agregarlos a [!DNL Adobe Commerce]](extensibility-and-customizations.md#add-product-attributes-to-adobe-commerce) where you can configure and manage them from the Commerce Admin. Only add them dynamically if you need them solely for Commerce storefront services and do not want to register them in [!DNL Adobe Commerce]. You also have the option to manage custom attributes using [[!DNL API Mesh] con [!DNL Catalog Service]](../catalog-service/mesh.md) para extender el esquema [!DNL Catalog Service] [!DNL GraphQL].

## Añadir atributos del producto

Cree un complemento que agregue `customer_attribute` a la clase `Magento\CatalogDataExporter\Model\Provider\Product\Attributes`.

1. Actualice el [archivo de configuración de inyección de dependencia](https://developer.adobe.com/commerce/php/development/build/dependency-injection-file/) (`di.xml`) para definir el complemento.

   ```xml
   <type name="Magento\CatalogDataExporter\Model\Provider\Product\Attributes">
     <plugin name="product_customer_attributes" type="Vendor\CatalogDataExporter\Model\Plugin\AddAttribute"/>
   </type>
   ```

1. Cree el complemento.

   ```php
    <?php
    declare(strict_types=1);
   
    namespace Vendor\CatalogDataExporter\Model\Plugin;
   
    use Magento\CatalogDataExporter\Model\Provider\Product\Attributes;
   
    class AddAttribute {
   
         /**
          * @param Attributes $subject
          * @param array $result
          * @param $arguments
          * @return array
          * @throws \Zend_Db_Statement_Exception
          */
          public function afterGet(Attributes $subject, array $result, $arguments): array
          {
              $additionalAttributes = [];
              $attributeCode = 'customer_attribute';
              foreach ($result as $product) {
                  if (!isset($product['productId']) || !isset($product['storeViewCode'])) {
                      continue;
                  }
                  // HINT: if needed, do filtration by "storeViewCode" and or "productId"
   
                  $productId = $product['productId'];
                  $storeViewCode = $product['storeViewCode'];
   
                  $newKey = \implode('-', [$product['storeViewCode'], $product['productId'], $attributeCode]);
                  if (isset($additionalAttributes[$newKey])) {
                      continue;
                  }
                  $additionalAttributes[$newKey] = [
                      'productId' => $productId,
                      'storeViewCode' => $storeViewCode,
                      'attributes' => [
                          'attributeCode' => $attributeCode,
                          // provide single or multiple values for the attribute
                          'value' => [
                              rand(1, 42)
                          ]
                      ]
                  ];
   
              }
   
              return array_merge($result, $additionalAttributes);
          }
    }
   ```

   Después de agregar el complemento, los cambios se sincronizan con los servicios de tienda conectados durante la siguiente sincronización programada. Para enviar las actualizaciones inmediatamente, utilice el siguiente comando CLI para iniciar el proceso de sincronización manualmente.

   ```shell
   bin/magento saas:resync --feed=products
   ```

## Declarar metadatos de atributos de producto personalizados

Si crea dinámicamente un atributo de producto personalizado y desea utilizarlo para su visualización, búsqueda o filtrado en los servicios de tienda, agregue los metadatos del atributo de producto para configurar el comportamiento de la tienda.

1. Actualice el [archivo de configuración de inyección de dependencia](https://developer.adobe.com/commerce/php/development/build/dependency-injection-file/) (`di.xml`) para definir el complemento para los metadatos de atributos del producto.

   ```xml
   <type name="Magento\CatalogDataExporter\Model\Provider\ProductMetadata">
     <plugin name="product_customer_attributes_metadata" type="Vendor\CatalogDataExporter\Model\Plugin\AddAttributeMetadata"/>
   </type>
   ```

1. Cree el complemento para el siguiente proveedor `Magento\CatalogDataExporter\Model\Provider\ProductMetadata`.

   Compruebe `ProductAttributeMetadata` en `vendor/magento/module-catalog-data-exporter/etc/et_schema.xml` los campos obligatorios.

   ```php
    <?php
    declare(strict_types=1);
   
    namespace Vendor\CatalogDataExporter\Model\Plugin;
   
    use Magento\CatalogDataExporter\Model\Provider\ProductMetadata;
   
    class AddAttributeMetadata {
   
         /**
          * @param ProductMetadata $subject
          * @param array $result
          * @param $arguments
          * @return array
          * @throws \Zend_Db_Statement_Exception
          */
         public function afterGet(ProductMetadata $subject, array $result, $arguments): array
         {
              $result[] = [
                'id' => '123',
                // provide storeCode, websiteCode and storeViewCode applicable for your AC instance
                'storeCode' => 'default',
                'websiteCode' => 'base',
                'storeViewCode' => 'default',
                // specify the customer attribute code - should be the same as used in the products attributes plugin
                'attributeCode' => 'customer_attribute',
                // only product attributes are supported
                'attributeType' => 'catalog_product',
                // specify the data type
                'dataType' => 'int',
                'multi' => false,
                'label' => 'Customer Attribute',
                'frontendInput' => 'select',
                'required' => false,
                'unique' => false,
                'global' => true,
                'visible' => true,
                'searchable' => true,
                'filterable' => true,
                // This value must be set to true to export it to the storefront services
                'visibleInCompareList' => true,
                'visibleInListing' => true,
                'sortable' => true,
                'visibleInSearch' => true,
                'filterableInSearch' => true,
                'searchWeight' => 1.0,
                'usedForRules' => true,
                'boolean' => false,
                'systemAttribute' => false,
                'numeric' => false,
                // specify the list of attribute options
                'attributeOptions' => [
                    'option1',
                    'option2',
                    'option3'
                ]
             ];
   
              return $result;
         }
      }
   ```

   Después de agregar el complemento, los cambios se sincronizan con los servicios de tienda conectados durante la siguiente sincronización programada. Para enviar las actualizaciones inmediatamente, utilice el siguiente comando CLI para iniciar el proceso de sincronización manualmente.

   ```shell
   bin/magento saas:resync --feed=productAttributes
   ```

>[!MORELIKETHIS]
>
> * [Ampliar y personalizar fuentes de exportación de datos SaaS](extensibility-and-customizations.md)
> * [Sincronizar fuentes usando la CLI de Commerce](data-export-cli-commands.md)
> * [Funcionamiento de la sincronización](sync-overview.md): obtenga información sobre los modos de sincronización y la resincronización programada frente a la manual.
> * [Revisar registros y solucionar problemas](troubleshooting/logging.md)
