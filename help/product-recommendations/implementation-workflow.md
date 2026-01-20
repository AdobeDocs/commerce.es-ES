---
title: Flujo de trabajo de implementación
description: Conoce los pasos para implementar  [!DNL Product Recommendations] correctamente en tu tienda.
exl-id: 4a784d04-8be6-473f-afb3-264af06c850a
source-git-commit: 458f34c45406db871ec61ff408aa624f163b6ee0
workflow-type: tm+mt
source-wordcount: '534'
ht-degree: 0%

---

# Flujo de trabajo de implementación

[!DNL Product Recommendations] utiliza datos de catálogo y de comportamiento:

- Comportamiento: datos de la participación de un comprador en el sitio, como vistas de productos, artículos añadidos a un carro de compras y compras. Adobe Commerce y Adobe AI no recopilan información de identificación personal.

- Catálogo: metadatos del producto, como nombre, precio y disponibilidad.

Al instalar `magento/product-recommendations module`, Adobe AI agrega los datos de comportamiento y catálogo y crea [!DNL Product Recommendations] para cada tipo de recomendación. A continuación, el servicio [!DNL Product Recommendations] implementa esas recomendaciones en la tienda. Para ayudarle a implementar recomendaciones de productos en su tienda, utilice el siguiente flujo de trabajo:

>[!NOTE]
>
> Si su tienda está implementada con PWA Studio, consulte la [documentación de PWA](https://developer.adobe.com/commerce/pwa-studio/integrations/product-recommendations/). Si usas una tecnología de front-end personalizada como React o Vue JS, aprende a [integrar](headless.md) [!DNL Product Recommendations] en tu tienda sin encabezado.

## Flujo de trabajo

1. **Implementar la recopilación de datos en la producción**

   La implementación de [!DNL Product Recommendations] requiere dos [fuentes de datos](type.md) principales: catálogo y comportamiento. Dado que la producción es el único entorno en el que se capturan y analizan las acciones de los compradores, comience la recopilación de datos sobre la producción lo antes posible. [Descubra](events.md) cómo la IA de Adobe entrena modelos de aprendizaje automático que resultan en recomendaciones de mayor calidad. Como beneficio adicional, cuando empiece a recopilar datos de comportamiento en producción, puede [recuperar recomendaciones](staging-environment.md#fetch-recommendations-from-production-environment-recommended) basadas en estos datos de producción mientras opera en entornos que no son de producción. A continuación, puede probar y experimentar con diferentes recomendaciones que se calculan en función de los datos reales del comprador recopilados en la producción.

   Para implementar la recopilación de datos en producción, debe [instalar y configurar](install-configure.md) el módulo [!DNL Product Recommendations] proporcionando una [clave de API](https://experienceleague.adobe.com/docs/commerce/user-guides/integration-services/saas.html?lang=es).

   >[!TIP]
   >
   > La implementación de la recopilación de datos no cambia el aspecto de la tienda ni la experiencia de los compradores. Solo la creación e implementación de unidades de recomendación altera la experiencia del cliente en su tienda. Asegúrese de realizar pruebas en el entorno que no sea de producción antes de implementarlo en producción. Además, no cree unidades de recomendación hasta que personalice la plantilla. Consulte el paso siguiente.

1. **Personalice la plantilla para que coincida con su estilo**

   La tienda representa su marca, por lo que asegúrese de modificar la plantilla de recomendaciones de productos para que coincida con el tema del sitio.

   >[!TIP]
   >
   > Al personalizar la plantilla, puede especificar la hoja de estilo, sobrescribir dónde aparece una unidad de recomendación en una página, etc.

   Consulte [Personalizar](https://experienceleague.adobe.com/docs/commerce/product-recommendations/developer/customize.html?lang=es) en la documentación para desarrolladores para obtener información sobre cómo completar este paso.

1. **Recomendaciones de prueba en su entorno que no sea de producción**

   Siempre es recomendable probar una nueva tecnología en un entorno que no sea de producción antes de implementarla en producción. Las recomendaciones de prueba en el entorno que no es de producción le permiten jugar con diferentes tipos de unidades de recomendación, posiciones y páginas. Puede extraer recomendaciones basadas en datos de comportamiento ya recopilados en producción mientras realiza pruebas en un entorno que no sea de producción, de modo que los resultados de las recomendaciones se basen en el comportamiento de compra de los clientes reales.

   >[!TIP]
   >
   > Asegúrese de que el catálogo de entornos de no producción sea en gran medida el mismo que el que tiene en producción. El uso de catálogos similares garantiza que los productos devueltos en las unidades de recomendación imiten de cerca los productos en la producción.

   Consulte [Recuperar](staging-environment.md) datos de comportamiento de su entorno de producción para aprender a completar este paso.

1. **Cree e implemente recomendaciones en su tienda de producción**

   Ahora que ha implementado la recopilación de datos de comportamiento en producción, ha modificado la plantilla de recomendaciones de productos y ha probado las recomendaciones utilizando el comportamiento real del comprador, está listo para promocionar todo el código en producción y [crear](create.md) recomendaciones de productos en directo.
