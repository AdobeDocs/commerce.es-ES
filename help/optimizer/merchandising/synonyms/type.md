---
title: Tipos de sinónimos
description: Obtenga información acerca de los distintos tipos de sinónimos en  [!DNL Adobe Commerce Optimizer].
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a Adobe Commerce as a Cloud Service y  [!DNL Adobe Commerce Optimizer] proyectos (infraestructura SaaS administrada por Adobe)."
exl-id: a74e48ea-e069-4ccc-a67f-2f85be251fb5
TQID: https://experienceleague.adobe.com/23kmFWLruZeFMxIjKZJKbs0y9q10DDtbFG8ioLC5U-o
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
topic_v2:
  - id: e0eb8757-182f-49f3-94a4-1587d16f5094
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 393
ht-degree: 0%

---

# Tipos de sinónimos

Los sinónimos unidireccionales y bidireccionales amplían la definición de palabras clave. Algunos son intercambiables con la palabra clave, mientras que otros representan un subconjunto de la palabra clave.

## Bidireccional

Los sinónimos bidireccionales tienen el mismo significado y devuelven los mismos resultados de búsqueda. En el ejemplo siguiente, la primera palabra que aparece en negrita es la palabra clave que se utiliza en el catálogo, seguida de palabras que tienen el mismo significado que la palabra clave original. Puede crear un par simple de sinónimos bidireccionales o una cadena de varios sinónimos bidireccionales para la misma palabra clave.

**chaqueta** ![chaqueta de dos vías](../../assets/two-way.png)
**pantalones** ![Selector bidireccional](../../assets/two-way.png) pantalones ![Selector bidireccional](../../assets/two-way.png)

## Unidireccional

Un sinónimo unidireccional es un subconjunto de una palabra clave, pero con un significado más específico. Por ejemplo, los capris y los shorts son pantalones, pero no todos son capris o shorts. Una búsqueda de pantalones incluye capris y pantalones cortos. Sin embargo, la búsqueda de pantalones cortos no devuelve capris.

**sudadera** ![selector unidireccional](../../assets/one-way.png) con capucha
**pantalones** ![Selector unidireccional](../../assets/one-way.png) capris ![Selector unidireccional](../../assets/one-way.png) pantalones de pantorrilla ![Selector unidireccional](../../assets/one-way.png) empujadores de pedales

## Comportamiento de sinónimo de varias palabras

Para sinónimos de varias palabras, [!DNL Adobe Commerce Optimizer] considera el sinónimo como una frase. Por ejemplo, si crea un sinónimo bidireccional **tabla de comedor** ![selector bidireccional](../../assets/two-way.png) **tabla de cocina** ![selector bidireccional](../../assets/two-way.png) **tabla de comedor**, entonces [!DNL Adobe Commerce Optimizer] busca en todos los campos establecidos para buscar la ocurrencia de **tabla de comedor** o **tabla de cocina** o **tabla de comedor**.

Si no se crea ningún sinónimo y un comprador busca **tabla de cocina**, [!DNL Adobe Commerce Optimizer] busca los términos en cualquier lugar de los campos en los que se puede buscar, incluso en diferentes campos, por ejemplo **tabla** en el campo de nombre y **cocina** en la palabra clave meta.

Después de crear un sinónimo, el comportamiento de búsqueda cambia para buscar la frase exacta **tabla de cocina**. Esto puede reducir el número de resultados, ya que solo se mostrarán los productos con la frase exacta.

Si quieres que los términos se busquen por separado como antes, puedes [crear un ticket de asistencia](https://experienceleague.adobe.com/es/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide). Si hay suficiente demanda, [!DNL Adobe Commerce Optimizer] considerará la posibilidad de agregar esta funcionalidad al producto en una versión futura.
