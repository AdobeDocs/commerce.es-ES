---
title: Rendimiento
description: El área de trabajo  [!DNL Live Search] Rendimiento proporciona una perspectiva de los términos de búsqueda que utilizan los compradores.
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '487'
ht-degree: 0%

---

# Rendimiento

El área de trabajo *Rendimiento* proporciona información sobre los términos de búsqueda que usan los compradores. La información se puede utilizar para identificar tendencias, aumentar los clics y mejorar la tasa de conversión. El espacio de trabajo Rendimiento proporciona una instantánea de las métricas de búsqueda para un intervalo de fechas específico e incluye los siguientes informes:

* Búsquedas únicas
* Cero resultados
* Resultados frecuentes

![Rendimiento](assets/performance-unique-searches.png)

También puede consultar el [Tablero de administración de datos](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-dashboard.html?lang=es) para obtener más datos sobre la sincronización de datos.

>[!NOTE]
>
>El espacio de trabajo de rendimiento se actualiza cada 12 horas.

## Ver un informe

1. Para escribir **Intervalo de fechas**, haga clic en el calendario (![Calendario](assets/btn-calendar.png)) y realice una de las siguientes acciones:

   * Para especificar una sola fecha, haga doble clic en la fecha del calendario.
   * Para especificar un intervalo de fechas, haga clic en la primera y en la última fecha del calendario.

>[!NOTE]
>
>El intervalo de fechas no puede superar un año.

## Descripciones de campos

| Datos de instantánea | Descripción |
|--- |--- |
| Búsquedas únicas | Número total de búsquedas únicas para el intervalo de fechas especificado. Varias búsquedas realizadas por el mismo comprador, incluso si se refieren a la misma consulta, se consideran únicas si se envían con más de una hora de diferencia. |
| Tasa de pulsaciones | El porcentaje de búsquedas que finalizan cuando el comprador hace clic en un producto. Por ejemplo, la tasa de clics es del 50 % si el comprador busca &quot;pantalones&quot; y &quot;camisa&quot; y luego hace clic en un resultado de la búsqueda &quot;camisa&quot;. |
| Tasa de conversión | El porcentaje de productos que compra el comprador en comparación con el número de productos en los que hace clic para el intervalo de fechas especificado. Por ejemplo, la tasa de conversión de la interacción es del 100 % si el comprador ve seis productos en la ventana emergente, hace clic en uno y realiza una compra. <br /><br />La tasa de conversión no se ve afectada por el número de vistas de un producto determinado. Por ejemplo, la tasa de conversión sigue siendo la misma si el comprador utiliza la búsqueda, pero no hace clic en ningún producto. |
| Tasa de resultados cero | Porcentaje de búsquedas únicas que no devuelven resultados para el intervalo de fechas especificado. Por ejemplo, la tasa de resultados cero es del 66,67 % si el comprador busca &quot;fjjajfjfjf&quot; dos veces (sin resultados) y &quot;pantalones&quot; una vez (con resultados). |
| El Promedio de posición del clic | La posición relativa de la tasa promedio de pulsaciones basada en búsquedas únicas para el intervalo de fechas especificado. |

| Informes | Descripción |
|--- |--- |
| Búsquedas únicas | Enumera las consultas de búsqueda únicas utilizadas durante el intervalo de fechas especificado. Los datos del informe se calculan del mismo modo que los datos de instantáneas de búsqueda única. Si un comprador escribe la misma consulta de búsqueda dos veces, pero con una diferencia de más de una hora, la búsqueda se considera dos búsquedas únicas. Límite de informes: 500 términos principales |
| Cero resultados | Enumera las consultas de búsqueda que no devuelven resultados y la cantidad de veces utilizadas durante el intervalo de fechas especificado. Límite de informes: 500 términos principales |
| Resultados frecuentes | Enumera los nombres de los productos que recibieron la mayor cantidad de vistas durante el intervalo de fechas especificado. Los resultados populares se calculan únicamente en función de las impresiones y no se ven afectados por el número de clics o ingresos generados. Límite de informes: 500 términos principales |
