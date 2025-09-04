---
title: Añadir atributos de producto de forma dinámica
description: Obtenga información sobre cómo añadir atributos de producto personalizados a fuentes de exportación de datos de forma dinámica durante el proceso de sincronización de datos.
role: Admin, Developer
exl-id: d5ed7497-4be1-440a-a567-81b64fdc54fc
source-git-commit: 37d5699315e34f1504602090fae5201ee51cf470
workflow-type: tm+mt
source-wordcount: '281'
ht-degree: 0%

---

# Añadir atributos de producto de forma dinámica durante la sincronización de datos

Puede ampliar los atributos de producto sin registrarlos en Adobe Commerce creando un complemento para añadir los atributos durante el proceso de sincronización de datos.

>[!NOTE]
>
>La mejor manera de ampliar los atributos del producto es [agregarlos a Adobe Commerce](extensibility-and-customizations.md#add-product-attributes-to-adobe-commerce), donde puede configurarlos y administrarlos desde el administrador de Commerce. Añádalos dinámicamente únicamente si los necesita únicamente para los servicios de tienda de Commerce y no desea registrarlos en Adobe Commerce. También tiene la opción de administrar atributos personalizados mediante [API Mesh con el servicio de catálogo](../catalog-service/mesh.md) para extender el esquema GraphQL del servicio de catálogo.

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

   ```
   bin/magento saas:resync --feed=products
   ```

## Declarar metadatos de atributos de producto personalizados

Si crea dinámicamente un atributo de producto personalizado y desea utilizarlo para su visualización, búsqueda o filtrado en los servicios de tienda, agregue los metadatos del atributo de producto para configurar el comportamiento de la tienda.

1. Actualice el [archivo de configuración de inyección de dependencia](https://developer.adobe.com/commerce/php/development/build/dependency-injection-file/) (`di.xml`) para definir el complemento para los metadatos de atributos del producto.

   ```xml
   <type name="\Magento\CatalogDataExporter\Model\Provider\ProductMetadata">
     <plugin name="product_customer_attributes_metadata" type="Vendor\CatalogDataExporter\Model\Plugin\AddAttributeMetadata"/>
   </type>
   ```

1. Cree el complemento al siguiente proveedor `\Magento\CatalogDataExporter\Model\Provider\ProductMetadata`.

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

   ```
   bin/magento saas:resync --feed=productattributes
   ```

