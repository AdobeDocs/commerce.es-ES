---
title: Personalizar
description: Aprenda a personalizar las recomendaciones de productos.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '620'
ht-degree: 0%

---

# Personalizar

Al instalar el módulo Recomendaciones de productos, Adobe Commerce crea el directorio `ProductRecommendationsLayout`. Este directorio contiene archivos de plantilla que puede personalizar para cambiar la forma en que aparecen las recomendaciones en la tienda. En concreto, puede modificar o anular la siguiente plantilla:

`<your theme>/Magento_ProductRecommendationsLayout/web/template/recommendations.html`

Para obtener más información sobre la modificación de archivos de plantilla, consulte [Personalización de plantillas](https://developer.adobe.com/commerce/frontend-core/guide/templates/walkthrough/) en la Guía para desarrolladores de Frontend.

Si modifica el archivo `recommendations.html`, debe conservar las siguientes etiquetas en el archivo para asegurarse de que Adobe Commerce pueda recopilar métricas de recomendaciones de su tienda:

| Etiqueta | Uso |
|---|---|
| `<div data-bind="attr : {'data-unit-id' : unitId }"...</div>` | Recopila eventos de vista. |
| `<a data-bind="attr : {'data-sku' : sku, 'data-unit-id'}"...</a>` | Recopila eventos de clic. <br/>**Nota:** Si agrega etiquetas de anclaje, debe incluir estos atributos. |

Además del archivo `recommendations.html`, el directorio `ProductRecommendationsLayout` contiene los siguientes subdirectorios:

| Directorio | Finalidad |
|---|---|
| `layout` | Contiene `*.xml` archivos para cada tipo de página |
| `templates` | Contiene archivos que llaman a los scripts de recuperación y procesamiento |
| `web/js` | Contiene los archivos JavaScript que recuperan y representan recomendaciones para su tienda |
| `web/template` | Contiene la plantilla para el módulo `magento/product-recommendations` |

## Posición de unidad de recomendación

Cuando [crea](create.md) una recomendación, especifica la [ubicación](placement.md) en la que aparece en la página. Se puede colocar una unidad de recomendación en la parte superior o inferior del contenedor de contenido principal. Sin embargo, puede personalizar esta ubicación. Si crea un tipo de contenido de recomendación de Page Builder, utilice las herramientas de Page Builder para colocar la unidad de recomendación en la página. Para el resto de tipos de página, edite los `*.xml` archivos que se generan cuando se crea la recomendación.

1. Cambiar al directorio `layout`:

   ```bash
   cd `<your theme>/Magento_ProductRecommendationsLayout/layout`
   ```

   En la tabla siguiente se enumeran los archivos XML presentes en este directorio:

   | Nombre de archivo | Página |
   |---|---|
   | `catalog_category_view.xml` | Categoría |
   | `catalog_product_view.xml` | Detalles del producto |
   | `checkout_cart_index.xml` | Carrito |
   | `checkout_onepage_success.xml` | Finalizar compra |
   | `cms_index_index.xml` | Inicio |

   >[!NOTE]
   >
   >Los nombres de archivo en el directorio `layout` pueden ser diferentes si el almacén utiliza extensiones de terceros.

1. Modifique el archivo `catalog_product_view.xml` para que la unidad de recomendación aparezca después de la imagen del producto en la página de detalles del producto. Antes de personalizar este archivo XML, consulte el archivo y las secciones que debe modificar:

   ```xml
   <?xml version="1.0"?>
   <page xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:View/Layout/etc/page_configuration.xsd">
       <referenceBlock name="page.wrapper">
           <block class="Magento\Framework\View\Element\Template" before="-" name="product_recommendations_fetcher" template="Magento_ProductRecommendationsStorefront::fetcher.phtml" />
       </referenceBlock>
       <body>
           <referenceBlock name="main.content">
               <block class="Magento\ProductRecommendationsStorefront\Block\Renderer" after="-" name="product_recommendations_product_below_content" template="Magento_ProductRecommendationsStorefront::renderer.phtml">
                   <arguments>
                       <argument name="pagePlacement" xsi:type="string">below-main-content</argument>
                   </arguments>
               </block>
           </referenceBlock>
       </body>
   </page>
   ```

   En el fragmento anterior, el bloque de referencia `main.content` indica que la unidad de recomendación se colocará en algún lugar relativo a ese elemento. Su elemento `block` contiene el atributo `after="-"`, que especifica que la unidad de recomendación se mostrará en la página después del bloque de contenido principal.

1. Vamos a modificar este archivo especificando un bloque de contenido diferente.

   Cambie el bloque de referencia `name` de `main.content` a `product.info.media`.

   ```xml
   <?xml version="1.0"?>
   <page xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:View/Layout/etc/page_configuration.xsd">
       <referenceBlock name="page.wrapper">
           <block class="Magento\Framework\View\Element\Template" before="-" name="product_recommendations_fetcher" template="Magento_ProductRecommendationsStorefront::fetcher.phtml" />
       </referenceBlock>
       <body>
           <referenceBlock name="product.info.media">
               <block class="Magento\ProductRecommendationsStorefront\Block\Renderer" after="-" name="product_recommendations_product_below_content" template="Magento_ProductRecommendationsStorefront::renderer.phtml">
                   <arguments>
                       <argument name="pagePlacement" xsi:type="string">below-main-content</argument>
                   </arguments>
               </block>
           </referenceBlock>
       </body>
   </page>
   ```

   Este cambio hace que la unidad de recomendación aparezca después de la imagen del producto en la página de detalles del producto. Si desea que la unidad de recomendación aparezca antes de `product.info.media`, cambie el atributo `after="-"` a `before="-"`. El argumento `pagePlacement` es un argumento interno que no se debe modificar.

Consulte [descripción general del diseño](https://developer.adobe.com/commerce/frontend-core/guide/layouts/) para obtener más información sobre los tipos de bloques en la página.

## Atributos de producto personalizados

Los desarrolladores suelen necesitar acceso a los valores de atributos de productos personalizados en las unidades de recomendaciones de las tiendas para que puedan añadir tratamientos visuales a los productos basados en esos atributos.

Por ejemplo, si su tienda vende algunos productos orgánicos, es posible que tenga un atributo personalizado en esos productos que los designe como `Organic = Yes`. Es posible que necesite acceso a este valor de atributo en la tienda para que pueda dar a estos productos un tratamiento visual especial cuando aparezcan en Recommendations. Del mismo modo, el acceso a estos valores de atributos de producto personalizados le permite crear insignias de productos o controlar la lógica personalizada en la capa de presentación del sitio.

![Agregar insignia](assets/unit-custom.png)

Para asegurarse de que haya un atributo de producto personalizado disponible cuando procese la unidad de recomendación en la página, establezca la propiedad `Used in Product Listing` en `Yes` en la página [Atributos de producto](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create.html) en el Administrador.

Cuando se establece esta propiedad, la carga útil JSON incluye un objeto `attributes` que contiene una matriz de códigos y valores de atributo. A continuación, puede aplicar un estilo de tienda personalizado basado en estos valores de atributo, como agregar tratamientos visuales especiales o insignias, como se mencionó anteriormente.

>[!NOTE]
>
>Los cambios de atributos del producto pueden tardar hasta una hora en aparecer en la carga útil JSON.
