---
title: Probar en el entorno de ensayo
description: Aprenda a usar  [!DNL Product Recommendations] de su entorno de producción en su entorno de ensayo con fines de prueba.
feature: Services, Recommendations, Staging
exl-id: 5b6d7615-6021-4419-98ea-006c8a299fe4
TQID: https://experienceleague.adobe.com/7e7e3T-vgkN-Pbqx6TwrBAWTEozhzS0h--tguOGe0yI
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
topic_v2: id: c4147b6e-073b-4d3c-9ab1-d60f2f4434efid: d3cdead0-685a-4489-9250-4bb709942f66id: eb30f47f-d87a-400f-8f78-63ce7979ff56
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 436
ht-degree: 0%

---

# Probar en el entorno de ensayo

Antes de implementar recomendaciones en el entorno de producción, pruebe el servicio en un entorno que no sea de producción para asegurarse de que todo funciona según lo esperado.

[!DNL Product Recommendations] devuelven productos basados en [datos de comportamiento del comprador](events.md) recopilados de su tienda. Sin embargo, en un entorno que no es de producción, es probable que no tenga datos de comportamiento de los compradores. El único tipo de recomendación que puede probar sin datos de comportamiento es `More like this`. Este tipo de recomendación no requiere datos de entrada, ya que utiliza una coincidencia de similitud de contenido directo.

Los siguientes tipos de recomendación requieren datos de comportamiento:

- Más visitados
- Vio esto, vio aquello.
- Compré esto, compré aquello.

¿Cómo puede probar las recomendaciones en un entorno que no es de producción utilizando datos de comportamiento? Hay un par de opciones.

## Obtener recomendaciones del entorno de producción (recomendado)

Adobe Commerce le permite recuperar recomendaciones de su entorno de producción y previsualizarlas en el entorno que no sea de producción [cambiando](settings.md) el espacio de datos SaaS.

Para recuperar recomendaciones del entorno de producción, debe asegurarse de que:

- La recopilación de datos de la tienda está [configurada y habilitada](install-configure.md) en el entorno de producción.
- El catálogo en el entorno que no es de producción es básicamente el mismo que el del entorno de producción. El uso de catálogos similares garantiza que los productos devueltos en las unidades de recomendación imiten estrechamente los del entorno de producción.

## Generar datos de comportamiento en un entorno que no sea de producción

1. Implemente el módulo `magento/product-recommendations` en un entorno que no sea de producción en el que los datos del catálogo sean similares a los del catálogo de producción.

1. Use uno de los ID de espacio de datos que no sean de producción para [configuration](../landing/saas.md#saas-configuration) en el administrador.

1. Genere los datos usted mismo haciendo clic en su tienda para imitar el comportamiento de los compradores reales (o cree un script de automatización). Con las pruebas, se generan eventos de comportamiento en el entorno que no es de producción. Estos eventos se utilizan para producir las afinidades de productos que alimentan las recomendaciones. Para las pruebas, [!DNL Commerce] sugiere que interactúe con los siguientes tipos de recomendaciones:

   - Más visitados: requiere datos de entrada mínimos. Los usuarios deben ver los productos.
   - Visto esto, visto aquello: requiere que varios usuarios vean varios productos.
   - Compró esto, compró aquello. Requiere que varios usuarios compren varios productos.

### Advertencias

- Los datos de catálogo y comportamiento del espacio de datos [SaaS](../landing/saas.md#saas-configuration), que no es de producción, identifican un entorno aislado en el que las recomendaciones de productos resultantes se basan totalmente en los datos de comportamiento generados en la tienda asociada.

- Como no tiene grandes cantidades de datos de comportamiento, los datos de entrada para calcular asociaciones de productos son escasos. Sin embargo, esos datos se siguen enviando a Sensei para calcular los modelos de aprendizaje automático y proporcionar recomendaciones basadas en los datos generados dentro de este entorno.
