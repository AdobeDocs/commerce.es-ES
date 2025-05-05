---
title: Tipos de facetas
description: Las facetas [!DNL Live Search] son dinámicas y aparecen en la lista Filtros cuando son relevantes.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '404'
ht-degree: 0%

---

# Tipos de facetas

[!DNL Live Search] usa una variedad de tipos de facetas y aparecen en la lista *Filtros* solo cuando es relevante. La lista de facetas disponibles cambia según los productos devueltos. Las siguientes características afectan su presentación y comportamiento:

* Facetas ancladas: las facetas más utilizadas se pueden anclar al principio de la lista. Las facetas restantes se enumeran en *Tipo de orden* después de las facetas ancladas.
* Facetas dinámicas: atributos de producto que [Adobe Sensei](https://www.adobe.com/sensei.html) encuentra más relevantes para un conjunto de productos y una consulta. El cálculo tiene en cuenta los metadatos de atributos de todo el catálogo y determina, en el momento de la consulta, las facetas más relevantes para la misma.

  >[!NOTE]
  >
  >Si observa que los errores de tiempo de espera aparecen en la respuesta de consulta de GraphQL después de crear facetas dinámicas, cambie todas las facetas a anclado para ver si esto resuelve los problemas de rendimiento.

* Facetas populares: atributos de producto que están presentes con mayor frecuencia en los resultados de búsqueda.
* Facetas de precio - Devolver productos por rango de precios. Puede especificar el número de selecciones y el intervalo de rango de precios en el área de trabajo [*Configuración*](settings.md).

En el momento de la consulta, [!DNL Live Search] genera los resultados de la búsqueda en grupos de facetas dinámicas y populares.

![Facetas - Precio](assets/storefront-search-results-run-price.png)

## Opciones de tienda y sin encabezado

El adaptador de búsqueda procesa las facetas representadas para la tienda [!DNL Commerce], que enruta las solicitudes y procesa los resultados en la tienda. Todas las facetas de tienda de [!DNL Commerce] se ordenan alfabéticamente con opciones de selección única, independientemente del tipo de entrada asignado al atributo correspondiente. Las facetas disponibles en la tienda se procesan según la temática actual y reflejan las personalizaciones realizadas en la presentación de la navegación por capas.

Por el contrario, las implementaciones de [headless](https://developer.adobe.com/commerce/php/architecture/technical-vision/web-api/) son procesadas por la API y admiten opciones adicionales. Las facetas sin encabezado se pueden ordenar alfabéticamente o por recuento, y pueden tener opciones de selección única o múltiple.

### Etiquetas de faceta

Para las tiendas de [!DNL Commerce], la etiqueta de faceta está determinada por las [*propiedades de atributo*](https://experienceleague.adobe.com/docs/commerce-admin/catalog/product-attributes/create/attribute-product-create.html?lang=es). En tiendas con varias vistas, se pueden definir etiquetas adicionales en *Administrar etiquetas*. Para implementaciones sin encabezado, las etiquetas se editan desde el [espacio de trabajo de facetas](faceting-workspace.md).

### Tipo de orden

Todas las facetas representadas para la tienda se ordenan alfabéticamente. Para implementaciones sin encabezado, las facetas se pueden ordenar alfabéticamente o por recuento.

| Tipo de orden | Descripción |
|--- |--- |
| Alfabético | En la lista de la tienda *Filtros*, las facetas se ordenan alfabéticamente. |
| Recuento | (Solo sin encabezado) Para implementaciones sin encabezado, las facetas también se pueden ordenar por el número de valores encontrados por faceta en el conjunto actual de productos devueltos. |
