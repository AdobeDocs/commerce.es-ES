---
title: '[!DNL Storefront Popover]'
description: ' [!DNL Live Search storefront popover] devuelve dinámicamente productos sugeridos y miniaturas.'
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '422'
ht-degree: 0%

---

# [!DNL Storefront Popover]

Cuando [!DNL Live Search] está [instalado](install.md), aparece un [!DNL popover] en la tienda cuando los compradores escriben en el cuadro [Buscar](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search.html#quick-search). Con cada carácter escrito, [!DNL popover] se actualiza con productos sugeridos e imágenes en miniatura de los resultados de búsqueda principales.

[!DNL Live Search] devuelve los resultados de una consulta de dos caracteres o más. Para una coincidencia parcial, el número máximo de caracteres por palabra es 20. El número de caracteres de una consulta &quot;buscar mientras escribe&quot; no se puede configurar.

De manera predeterminada, [!DNL Live Search] admite [redirecciones de términos de búsqueda](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search-terms.html).

![[!DNL Live Search popover]](assets/storefront-search-as-you-type.png)

>[!TIP]
>
>Aprenda a establecer atributos de producto según las búsquedas que se pueden realizar en el artículo [Configuración de Live Search](workspace.md).

## [!DNL Popover] tamaño de página

El tamaño de página de [!DNL popover] determina cuántas líneas de productos autocompletados se pueden devolver. Durante la instalación de Live Search, el valor `page_size` cambia al valor actual de la configuración [Búsqueda en el catálogo](https://experienceleague.adobe.com/docs/commerce-admin/config/catalog/catalog.html) - `Autocomplete Limit`.

De forma predeterminada, el valor Búsqueda en el catálogo: Límite de autocompletar está establecido en ocho líneas (o filas). Para cambiar el tamaño de página de [!DNL popover], haga lo siguiente:

1. En la barra lateral de *Administración*, ve a **Tiendas** > Configuración > **Configuración**.
1. En el panel izquierdo, expanda **Catálogo** y elija **Catálogo** de la lista de configuraciones.
1. Expanda la sección *Búsqueda en el catálogo*.
1. Establezca el **Límite de autocompletar** al número de líneas que desea permitir en [!DNL popover].
1. Una vez finalizado, haga clic en **Guardar configuración**.

## Ejemplo de estilo [!DNL Popover]

Puede personalizar el aspecto del widget [!DNL Popover] para que coincida con el estilo y las directrices de personalización de marca de su compañía.

[!DNL storefront popover] siempre muestra el producto `name` y `price`, y la selección de campos no se puede configurar. Sin embargo, los elementos [!DNL popover] se pueden diseñar con clases [CSS](https://developer.adobe.com/commerce/frontend-core/guide/css/). Por ejemplo, las siguientes declaraciones cambian el color de fondo del contenedor y pie de página de [!DNL popover].

```css
.livesearch.popover-container {
    background-color: lavender;
}

.livesearch.view-all-footer {
    background-color: magenta;
}
```

## Visibilidad del contenedor

El componente principal de `.livesearch.popover-container` es `.search-autocomplete`.  La clase `.active` indica la visibilidad del contenedor. La clase `.active` se agrega condicionalmente cuando [!DNL popover] está abierto.

```css
.search-autocomplete.active   /* visible */
.search-autocomplete          /* not visible */
```

Para obtener más información sobre cómo aplicar estilo a los elementos de la tienda, consulte [Hojas de estilo en cascada (CSS)](https://developer.adobe.com/commerce/frontend-core/guide/css/) en la [Guía para desarrolladores de Frontend](https://developer.adobe.com/commerce/frontend-core/guide/).

## Selectores de clase

Puede utilizar los siguientes selectores de clase para aplicar estilo al contenedor y a los elementos de producto en [!DNL popover].

- `.livesearch.popover-container`
- `.livesearch.view-all-footer`
- `.livesearch.products-container`
- `.livesearch.product-result`
- `.livesearch.product-name`
- `.livesearch.product-price`

### Selectores de clase de contenedor

#### .livessearch.popover-container

![[!DNL Popover] contenedor](assets/livesearch-popover-container.png)

#### .livessearch.view-all-footer

![Ver todos los pies de página](assets/livesearch-view-all-footer.png)

### Selectores de clase de producto

#### .livessearch.products-container

![Contenedor de producto](assets/livesearch-product-container.png)

#### .livessearch.product-result

![Resultado del producto](assets/livesearch-product-result.png)

#### .livessearch.product-name

![Nombre del producto](assets/livesearch-product-name.png)

#### .livessearch.product-price

![Precio del producto](assets/livesearch-product-price.png)

#### .livessearch product-link

![Resultado del producto](assets/livesearch-product-link.png)

## Trabajar con una temática modificada {#working-with-modified-theme}

Puede usar [!DNL storefront popover] con un [tema](https://developer.adobe.com/commerce/frontend-core/guide/themes/) personalizado que hereda los archivos necesarios de *Luma*. No se debe modificar el bloque `top.search` en `header-wrapper` del módulo `Magento_Search`.

```html
<referenceContainer name="header-wrapper">
   <block class="Magento\Framework\View\Element\Template" name="top.search" as="topSearch" template="Magento_Search::form.mini.phtml">
      <arguments>
         <argument name="configProvider" xsi:type="object">Magento\Search\ViewModel\ConfigProvider</argument>
      </arguments>
   </block>
</referenceContainer>
```

## Deshabilitando [!DNL popover]

Para deshabilitar [!DNL popover] y restaurar la funcionalidad estándar de [Búsqueda rápida](https://experienceleague.adobe.com/docs/commerce-admin/catalog/catalog/search/search.html#quick-search), escriba el siguiente comando:

```bash
bin/magento module:disable Magento_LiveSearchStorefrontPopover
```

## Implementaciones sin encabezado

Para los que tengan implementaciones sin encabezado, puede instalar [!DNL Live Search popover] con un [paquete npm](https://www.npmjs.com/package/@magento/ds-livesearch-storefront-utils).
