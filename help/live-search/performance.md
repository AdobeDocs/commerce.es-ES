---
title: Rendimiento
description: El área de trabajo  [!DNL Live Search] Rendimiento proporciona insight a los términos de búsqueda que utilizan los compradores.
exl-id: 07a63df8-b981-4913-841a-7e81ec634281
source-git-commit: 5978a400d985e3099962af8bcefdd6f29f687d67
workflow-type: tm+mt
source-wordcount: '675'
ht-degree: 0%

---

# Rendimiento

El área de trabajo *Rendimiento* proporciona insight a los términos de búsqueda que usan los compradores. La información se puede utilizar para identificar tendencias, aumentar los clics y mejorar la tasa de conversión. El espacio de trabajo Rendimiento proporciona una instantánea de las métricas de búsqueda para un intervalo de fechas específico e incluye los siguientes informes:

* Búsquedas únicas
* Cero resultados
* Resultados frecuentes

![Rendimiento](assets/performance-unique-searches.png)

También puede consultar el [Tablero de administración de datos](https://experienceleague.adobe.com/docs/commerce-admin/systems/data-transfer/data-sync/data-dashboard.html?lang=es) para obtener más datos sobre la sincronización de datos.

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

| Datos de instantánea | Descripción | Ejemplo de cálculo |
|--- |--- |--- |
| Búsquedas únicas | Número total de búsquedas únicas para el intervalo de fechas especificado. Varias búsquedas realizadas por el mismo comprador, incluso si se refieren a la misma consulta, se consideran únicas si se envían con más de una hora de diferencia. | **Ejemplo:**<br /> Búsquedas:<br />- &quot;pantalones&quot; a las 10:00 AM<br />- &quot;pantalones&quot; a las 10:30 AM (dentro de 1 hora no → únicos)<br />- &quot;pantalones&quot; a las 12:00 PM (después de 1 hora → únicos)<br />- &quot;camisa&quot; a las 1:00 PM <br /><br />**Búsquedas únicas totales = 3** |
| Tasa de clics | El porcentaje de búsquedas que finalizan cuando el comprador hace clic en un producto. Por ejemplo, la tasa de clics es del 50 % si el comprador busca &quot;pantalones&quot; y &quot;camisa&quot; y luego hace clic en un resultado de la búsqueda &quot;camisa&quot;. | **Fórmula:**<br /> Tasa de pulsaciones = Búsquedas con ≥1 clic ÷ Total de búsquedas únicas <br /><br />**Ejemplo:**<br /> Total de búsquedas únicas = 4<br />Búsquedas con al menos un clic = 2<br /><br />CTR = 2 ÷ 4 = **50%** |
| Tasa de conversión | El porcentaje de productos que compra el comprador en comparación con el número de productos en los que hace clic para el intervalo de fechas especificado. Por ejemplo, la tasa de conversión de la interacción es del 100 % si el comprador ve seis productos en la ventana emergente, hace clic en uno y realiza una compra. <br /><br />La tasa de conversión no se ve afectada por el número de vistas de un producto determinado. Por ejemplo, la tasa de conversión sigue siendo la misma si el comprador utiliza la búsqueda, pero no hace clic en ningún producto. | **Fórmula:**<br /> Tasa de conversión = Productos totales comprados ÷ Productos totales en los que se hizo clic <br /><br />**Ejemplo 1:**<br /> Productos en los que se hizo clic = 5<br />Productos comprados = 2<br /><br />CVR = 2 ÷ 5 = **40%**<br /><br />**Ejemplo 2 (agregación de 5 horas):**<br /> Clics por hora: 4, 5, 6, 10, 2<br />Compras por hora: 1, 3, 0, 4, 1<br /><br />Clics totales = 4 + 5 + 6 + 10 + 2 = 27<br /> Compras totales 3 + 0 + 4 + 1 = 9<br /><br />CVR = 9 ÷ 27 = **33,33 %** |
| Tasa de resultados cero | Porcentaje de búsquedas únicas que no devuelven resultados para el intervalo de fechas especificado. Por ejemplo, la tasa de resultados cero es del 66,67 % si el comprador busca &quot;fjjajfjfjf&quot; dos veces (sin resultados) y &quot;pantalones&quot; una vez (con resultados). | **Fórmula:**<br /> Tasa de resultados cero = Búsquedas únicas con resultados cero ÷ Total de búsquedas únicas <br /><br />**Ejemplo:**<br /> Total de búsquedas únicas = 3<br />Búsquedas con resultados cero = 2<br /><br />Tasa de resultados cero = 2 ÷ 3 = **66,67%** |
| El Promedio de posición del clic | La posición relativa de la tasa promedio de pulsaciones basada en búsquedas únicas para el intervalo de fechas especificado. | **Fórmula:**<br /> Posición de clic promedio = Suma de posiciones de clic ÷ Clics totales <br /><br />**Ejemplo:**<br /> Clics en posiciones: 1, 3, 2<br /><br />Posición de clic promedio = (1 + 3 + 2) ÷ 3 = **2** |

| Informes | Descripción |
|--- |--- |
| Búsquedas únicas | Enumera las consultas de búsqueda únicas utilizadas durante el intervalo de fechas especificado. Los datos del informe se calculan del mismo modo que los datos de instantáneas de búsqueda única. Si un comprador escribe la misma consulta de búsqueda dos veces, pero con una diferencia de más de una hora, la búsqueda se considera dos búsquedas únicas. <br />**Límite de informes:** 500 términos principales al generar el archivo CSV. |
| Cero resultados | Enumera las consultas de búsqueda que no devuelven resultados y la cantidad de veces utilizadas durante el intervalo de fechas especificado. <br />**Límite de informes:** 500 términos principales al generar el archivo CSV. |
| Resultados frecuentes | Enumera los nombres de los productos que recibieron la mayor cantidad de vistas durante el intervalo de fechas especificado. Los resultados populares se calculan únicamente en función de las impresiones y no se ven afectados por el número de clics o ingresos generados. <br />**Límite de informes:** 500 términos principales al generar el archivo CSV. |
