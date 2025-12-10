---
title: Crear y administrar sinónimos
description: Aprenda a crear y administrar sinónimos para  [!DNL Adobe Commerce Optimizer].
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
exl-id: d2982a0b-e7df-44e6-b3c9-9b4328635d38
source-git-commit: c6725fc524e9d239ccc0f16701e92ad5d2fc7729
workflow-type: tm+mt
source-wordcount: '597'
ht-degree: 0%

---

# Crear sinónimos

Aumente la participación de los clientes agregando su propia lista revisada de [!DNL Adobe Commerce Optimizer] sinónimos. Puede añadir hasta 200 sinónimos por tienda.

![Workspace de sinónimo](../../assets/synonym-workspace.png)

## Paso 1: Añadir un sinónimo

1. Desde el carril izquierdo, vaya a _Comercialización_ > **Sinónimos**.
1. Haga clic en el botón **[!UICONTROL Add synonyms]**.

## Paso 2: Definir el sinónimo por tipo

Siga las instrucciones del [tipo de sinónimo](type.md) que desea crear.

### Sinónimo bidireccional

1. Acepte la opción predeterminada **Bidireccional**.

   ![Agregar sinónimo bidireccional](../../assets/synonym-add-two-way.png)

1. Escriba el término o frase **Keyword** con el que se debe hacer coincidir.
1. Escriba los términos **Expansion** que desee agregar como sinónimos de la palabra clave. Separe varios términos con una coma.
En este ejemplo, la palabra clave para coincidir es &quot;pantalones&quot; y el conjunto de términos de expansión son &quot;pantalones, pantalones&quot;.

   ![Ejemplo de sinónimo bidireccional](../../assets/synonym-add-two-way-example.png)

1. Una vez finalizado, haga clic en **Guardar**.

   El conjunto de sinónimos aparece en la lista con una flecha bidireccional entre cada término, lo que significa que los términos son intercambiables.

   ![Sinónimo bidireccional](../../assets/synonym-two-way.png)

### Sinónimo unidireccional

1. Haga clic en el tipo de sinónimo **Unidireccional**.

   ![Agregar sinónimo unidireccional](../../assets/synonym-add-one-way.png)

1. Escriba los términos **Palabra clave** y **Expansión**. Separe varios términos con una coma.

   ![Ejemplo de sinónimo unidireccional](../../assets/synonym-add-one-way-example.png)

   En este ejemplo, la palabra clave es &quot;pantalones&quot; y los términos de expansión unidireccional &quot;capris, traficantes de coches&quot; son cada uno un subconjunto de &quot;pantalones&quot;, pero con un significado específico.

1. Una vez finalizado, haga clic en **Guardar**.

   El conjunto de sinónimos aparece en la lista con una flecha unidireccional que señala desde los términos de expansión a la palabra clave para indicar que los términos son subconjuntos de la palabra clave. Un signo más separa cada término de expansión.

   ![Sinónimo unidireccional](../../assets/synonym-one-way.png)

## Paso 3: Publicar cambios

1. Cuando haya completado los sinónimos, haga clic en **Publicar**.
1. Espera hasta dos horas para que tus actualizaciones estén disponibles en la tienda.

## Descripciones de campos

| Campo | Descripción |
|--- |--- |
| [Tipo](type.md) | Determina si los sinónimos tienen el mismo significado que la palabra clave o si son un subconjunto de la palabra clave. Opciones: <br />Dos vías (predeterminado): términos que tienen el mismo significado que la palabra clave y devuelven los mismos resultados de búsqueda<br />Unidireccional: términos que son un subconjunto de la palabra clave. Los sinónimos unidireccionales devuelven una lista más estrecha de productos específicos. |
| Palabra clave | Una palabra que comúnmente se asocia con una selección de productos en su catálogo. |
| Expansión | Términos adicionales que tengan un significado igual o similar al de la palabra clave. |

## Administrar sinónimos

Siga estas instrucciones para administrar los [!DNL Adobe Commerce Optimizer] [sinónimos](overview.md) existentes.

## Buscar sinónimo

Para facilitar la búsqueda de un sinónimo, puede filtrar la lista por tipo y buscar por palabra clave o término de expansión. Estos métodos se pueden utilizar de forma individual o conjunta.

1. Para filtrar la lista, establezca **Type** en uno de los siguientes:

   - Todo
   - Unidireccional
   - Bidireccional

1. Para buscar una palabra clave o un término de expansión, escriba al menos tres caracteres en el cuadro **[!UICONTROL Search]**.

## Editar sinónimo

1. Busque el sinónimo que desea editar y haga clic en las opciones **Más** (...).

1. Haga clic en **Editar**.
La palabra clave es el primer término de la lista y cada término está separado por una coma. La palabra clave y los términos de expansión se pueden actualizar, pero no se puede cambiar el tipo de sinónimo.
1. Haga clic en el elemento que desee editar. A continuación, actualice el texto según sea necesario.

1. Una vez finalizado, haga clic en **Guardar**.

## Eliminar sinónimo

1. Busque el sinónimo que desea eliminar en la lista y haga clic en las opciones **Más** (...).
1. Haga clic en **Eliminar**.
1. Cuando se le solicite, haga clic en **Eliminar sinónimo** para confirmar.

## Publicar cambios

Para completar el proceso, los cambios guardados deben publicarse en la tienda. Las actualizaciones pueden tardar hasta dos horas en estar activas.

1. Haga clic en **Publicar**.
1. Busque el mensaje en la parte superior de la página que confirma que los cambios se han publicado.
