---
title: Añadir sinónimos
description: Agregue  [!DNL Live Search] sinónimos para mejorar la respuesta a las solicitudes de búsqueda.
exl-id: 2dc535ea-35a3-45a8-8171-901005223cc9
source-git-commit: 6dcfd0a54e6a6814b7f5708e0c221452b8af4537
workflow-type: tm+mt
source-wordcount: '385'
ht-degree: 0%

---

# Añadir sinónimos

Aumente la participación de los clientes agregando su propia lista revisada de [!DNL Live Search] sinónimos. [!DNL Live Search] puede administrar hasta 200 sinónimos por vista de tienda.

![[!DNL Live Search] sinónimos](assets/synonym-workspace.png)

## Paso 1: Añadir un sinónimo

1. En el Administrador, vaya a **Marketing** > SEO y búsqueda > **[!DNL Live Search]**.
1. Para varias tiendas, establece **Scope** en la [vista de la tienda](https://experienceleague.adobe.com/docs/commerce-admin/start/setup/websites-stores-views.html#scope-settings) donde se aplica la configuración del sinónimo.
1. Haga clic en la ficha **Sinónimos**.
1. Haga clic en el botón **Agregar sinónimos**.

## Paso 2: Definir el sinónimo por tipo

Siga las instrucciones del [tipo de sinónimo](synonyms-type.md) que desea crear.

### Sinónimo bidireccional

1. Acepte la opción predeterminada **Bidireccional**.

   ![Agregar sinónimo bidireccional](assets/synonym-add-two-way.png)

1. Escriba el término o frase **Keyword** con el que se debe hacer coincidir.
1. Escriba los términos **Expansion** que desee agregar como sinónimos de la palabra clave. Separe varios términos con una coma.
En este ejemplo, la palabra clave para coincidir es &quot;pantalones&quot; y el conjunto de términos de expansión son &quot;pantalones, pantalones&quot;.

   ![Ejemplo de sinónimo bidireccional](assets/synonym-add-two-way-example.png)

1. Una vez finalizado, haga clic en **Guardar**.
El conjunto de sinónimos aparece en la lista con una flecha bidireccional entre cada término, lo que significa que los términos son intercambiables.

   ![Sinónimo bidireccional](assets/synonym-two-way.png)

### Sinónimo unidireccional

1. Haga clic en el tipo de sinónimo **Unidireccional**.

   ![Agregar sinónimo unidireccional](assets/synonym-add-one-way.png)

1. Escriba los términos **Palabra clave** y **Expansión**. Separe varios términos con una coma.

   ![Ejemplo de sinónimo unidireccional](assets/synonym-add-one-way-example.png)

   En este ejemplo, la palabra clave es &quot;pantalones&quot; y los términos de expansión unidireccional &quot;capris, traficantes de coches&quot; son cada uno un subconjunto de &quot;pantalones&quot;, pero con un significado específico.

1. Una vez finalizado, haga clic en **Guardar**.
El conjunto de sinónimos aparece en la lista con una flecha unidireccional que señala desde los términos de expansión a la palabra clave para indicar que los términos son subconjuntos de la palabra clave. Un signo más separa cada término de expansión.

   ![Sinónimo unidireccional](assets/synonym-one-way.png)

## Paso 3: Publicar cambios

1. Una vez completados los sinónimos, haga clic en **Publicar cambios**.
1. Espera hasta dos horas para que tus actualizaciones estén disponibles en la tienda.

## Descripciones de campos

| Campo | Descripción |
|--- |--- |
| [Tipo](synonyms.md) | Determina si los sinónimos tienen el mismo significado que la palabra clave o si son un subconjunto de la palabra clave. Opciones: <br />Dos vías (predeterminado): términos que tienen el mismo significado que la palabra clave y devuelven los mismos resultados de búsqueda<br />Unidireccional: términos que son un subconjunto de la palabra clave. Los sinónimos unidireccionales devuelven una lista más estrecha de productos específicos. |
| Palabra clave | Una palabra que comúnmente se asocia con una selección de productos en su catálogo. |
| Expansión | Términos adicionales que tengan un significado igual o similar al de la palabra clave. |
