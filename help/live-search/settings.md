---
title: Configuración
description: Configure las opciones del servicio  [!DNL Live Search] .
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# Configuración

Use el área de trabajo *Configuración* para configurar los intervalos y rangos de facetas de precios y el idioma predeterminado del índice.

Facetado de precios especifica el número de grupos de intervalos de precios y cómo se distribuyen los valores de precios entre ellos.

La configuración de idioma indica al servicio [!DNL Live Search] qué idioma esperar al escribir el índice.

![Configuración](assets/settings.png)

## Facetado de precios

Puede especificar el número de grupos de intervalos de precios y cómo se distribuyen los valores de precios entre ellos. Cada rango de precios se superpone con el grupo anterior por uno. Por ejemplo, cinco grupos con un intervalo de 20 crean los siguientes intervalos de precios: 0-20, 20-40, 40-60, 60-80 y >80. Si no hay suficientes productos en el catálogo para rellenar todos los intervalos definidos, la visualización de los grupos disponibles se ajusta en consecuencia. Por ejemplo: 0-20, 60-80, >80.

1. En el Administrador, vaya a **Marketing** > *SEO y búsqueda* > **[!DNL Live Search]**.
1. En el área de trabajo **Configuración** en *Faceteo de precios*, haga lo siguiente:
   * Escriba el **número de selecciones** o las agrupaciones de precios que estarán disponibles. Se pueden definir hasta 50 agrupaciones de precios.
   * Escriba el **valor de intervalo** o el rango de precios de cada grupo. El valor máximo es 40 000 000.
1. Haga clic en **Guardar**.

   La configuración actualizada tarda unos 15 minutos en estar disponible en la tienda.

### Descripciones de campos

| Campo | Descripción |
|--- |--- |
| Número de selecciones | Especifica el número de agrupaciones de intervalos de precios que se pueden usar como filtros de búsqueda en la tienda. Valor predeterminado: 8, Valor máximo: 50 |
| Valor de intervalo | Especifica el intervalo de rango de precios para cada grupo. Por ejemplo, cinco selecciones con un valor de intervalo de 20 crean cinco agrupaciones de 0-20, 20-40, 40-60, 60-80 y >80. Valor predeterminado: 5, Valor máximo: 40 000 000 |

## Idioma

La configuración de idioma indica a [!DNL Live Search] qué idioma esperar al leer el catálogo y escribir el índice.

Los idiomas tienen diferentes conjuntos de reglas gramaticales: cómo se separan las palabras, tiempos verbales y formas de palabras, por ejemplo.
La configuración Idioma garantiza que se aplique el conjunto correcto de reglas al mecanismo de indexación.

Establezca la configuración Idioma en el idioma principal del catálogo. Al cambiar el idioma del índice, puede tardar entre 5 y 60 minutos en reflejar el cambio en la tienda, según el tamaño y la complejidad del catálogo.

| Idioma | Código |
|----|----|
| Árabe | ar |
| Armenio | hy |
| Vasco | eu |
| Bengalí | bn |
| brasileño | pt-br |
| Búlgaro | bg |
| Catalán | ca |
| Chino (simplificado) | zh-cn |
| Chino (tradicional) | zh-tw |
| Checo | cs |
| Danés | da |
| Neerlandés | nl |
| Inglés | en |
| Estonio | et |
| Finés | fi |
| francés | fr |
| Gallego | gl |
| Alemán | de |
| Griego | el |
| Hindi | hola |
| Húngaro | hu |
| Indonesio | id |
| Irlandés | ga |
| Italiano | it |
| Japonés (Katakana) | ja |
| Coreano | ko |
| Letón | lv |
| Lituano | lt |
| Noruego | no |
| persa | fa |
| Portugués | pt |
| Rumano | ro |
| Ruso | ru |
| Sorani | ku |
| Español | es |
| Sueco | sv |
| Turco | tr |
| Tailandés | th |
