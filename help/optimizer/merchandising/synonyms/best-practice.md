---
title: Prácticas recomendadas de sinónimo
description: Conozca las prácticas recomendadas para implementar sinónimos en su tienda.
role: Admin, Developer
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
source-git-commit: 54b300ed89f830c2fe5258ec889302a59decd59f
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# Prácticas recomendadas de sinónimo

A continuación se proporciona una lista de prácticas recomendadas al crear sinónimos.

- [!DNL Adobe Commerce Optimizer] administra los errores ortográficos de forma predeterminada. Puede configurar sinónimos para incluir palabras que los compradores pueden utilizar y que difieren de las palabras especificadas en el catálogo. Usted no quiere perder una venta porque alguien está buscando un &quot;sofá&quot;, mientras que su producto aparece como un &quot;sofá&quot;. Puede capturar una amplia gama de términos de búsqueda introduciendo todas las palabras posibles que los clientes podrían utilizar para encontrar sus productos. Puede [establecer sinónimos de una o dos maneras](add.md#step-2-define-the-synonym-by-type) para mejorar los resultados.

- Asigne nombres de marcas y abreviaturas a sus nombres completos, como &quot;HP&quot; a &quot;Hewlett-Packard&quot; y apodos de productos comunes, como &quot;iPhone&quot; a &quot;Apple iPhone&quot;.

- Incluya jerga y términos específicos del sector que los compradores puedan utilizar indistintamente, como &quot;zapatillas de deporte&quot; y &quot;zapatillas de running&quot;.

- Actualice con regularidad la lista de sinónimos en función de las nuevas tendencias de búsqueda, las adiciones de productos y el comportamiento del comprador.

- Pruebe la eficacia de las asignaciones de sinónimos analizando los resultados de búsqueda y los comentarios del comprador. Refine las asignaciones para mejorar la precisión y la relevancia.

- Evite utilizar palabras de detención, ya que no hacen que los sinónimos sean más significativos, sino que aumentan la cantidad de datos que deben procesarse. [!DNL Adobe Commerce Optimizer] elimina las &quot;palabras de detención&quot; comunes del inglés de los sinónimos, como:

  a, y, son, como, en, ser, pero, por, porque, si, en, en, es, no, no, de, en, o, tal, que, el, su, entonces, allí, estos, ellos, esto, a, era, voluntad, con

- No es necesario definir las formas singular y plural de una palabra como sinónimo. Si en el catálogo existe una mezcla de términos en singular y en plural, Search busca el conjunto de productos correcto. Por ejemplo, si utiliza la palabra &quot;pantalón&quot; en el nombre del producto y un comprador busca &quot;pantalones&quot;, se devuelve el conjunto correcto de productos y la palabra singular &quot;pantalón&quot; se ofrece como sugerencia. El término singular &quot;pantalón&quot; se utiliza a menudo en la industria de la moda y a veces en el comercio minorista, aunque la forma plural &quot;pantalones&quot; se utiliza más comúnmente en algunas áreas. (La palabra &quot;pantalón&quot; se refiere técnicamente a la parte de una prenda que cubre una pierna, por lo que se necesita un &quot;par de pantalones&quot; para cubrir ambas piernas).

- Sea coherente con la forma en que se utiliza la terminología en su catálogo. Tenga en cuenta que puede haber diferencias regionales en el uso y, a veces, diferencias dentro de una industria.
