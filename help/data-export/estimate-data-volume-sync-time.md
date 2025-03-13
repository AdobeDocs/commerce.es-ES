---
title: Estimar el volumen de datos y el tiempo de transmisión
description: Aprenda a calcular el volumen de datos y el tiempo de transmisión necesarios para que la herramienta  [!DNL data export]  sincronice los datos de fuente entre Adobe Commerce y los servicios conectados.
role: Admin, Developer
exl-id: 787d05d6-fc2f-4f23-8ea7-ef54330e1f37
source-git-commit: 86f7473e994348d81c0a8f71548bb7a8d3923a21
workflow-type: tm+mt
source-wordcount: '559'
ht-degree: 0%

---

# Calcular el volumen de datos y el tiempo de transmisión para la sincronización de datos

Adobe recomienda estimar el volumen de datos y el tiempo de sincronización antes de iniciar cualquier sincronización de fuente de datos para garantizar una programación sin problemas y evitar interrupciones en las operaciones del sitio. Esta estimación es importante a la hora de planificar sincronizaciones iniciales o actualizaciones de catálogos a gran escala, como cambios masivos de precios.

De forma predeterminada, la herramienta de exportación de datos procesa los datos en modo de subproceso único con un tamaño de lote predeterminado. Con la configuración predeterminada, no hay paralelización del proceso de envío de fuentes. Además, este componente acepta solicitudes por segundo (RPS) que se traducen en lo siguiente:

- Hasta 10 000 productos por minuto donde un producto es un SKU con atributos de una tienda específica
- Hasta 50.000 precios por minuto

Los siguientes factores afectan al tiempo de transmisión de datos durante la sincronización.

- El recuento de subprocesos se establece en 1 (de forma predeterminada)
- El tamaño del lote está establecido en _100_ para todas las fuentes, excepto para la fuente `prices`, donde está establecido en _500_.
- La tasa de aceptación de fuentes es de 2 solicitudes por segundo.
- Todos los productos se asignan a todos los sitios web existentes
- Para los escenarios de cálculo de precios, todos los productos tienen precios especiales y agrupados asignados


## Calcular transmisión de datos por fuente

Utilice los valores y las fórmulas de la tabla siguiente para calcular el volumen de datos y el tiempo de sincronización de cada fuente de datos.

>[!NOTE]
>
>Estos cálculos se basan en una tasa de transmisión de 2 solicitudes por segundo. La velocidad se basa en el tiempo necesario para la recopilación y el envío de datos. La velocidad de transmisión real varía según el tamaño de carga útil de la solicitud y la carga actual en el servidor de aplicaciones de Commerce.

| Fuente | Ejemplo de datos | Fórmula para calcular registros | Recuento de solicitudes previstas | Tiempo de resincronización previsto |
| --- | --- | --- | --- | --- |
| Productos | Productos (P): 10000, Vistas de la tienda (SV): 4 | P * SV = 40000 | 40000 / Tamaño del lote (100) = 400 solicitudes | (400 solicitudes * 0,5 segundos por solicitud) / 60 = 3,3 minutos |
| Categorías | Categorías (C): 500, Vistas de la tienda (SV): 4 | C * SV = 2000 | 2000 / Tamaño de lote (100) = 20 solicitudes | (20 solicitudes * 0,5 segundos por solicitud) / 60 = 0,1 minutos (4 segundos) |
| Precios | Productos (P): 10000, Grupos de clientes (CG): 6 (por ejemplo, precio único en catálogo compartido), Sitios web (WS): 2 | P \* WS * CG = 120000 | 120000 / Tamaño del lote (500) = 240 solicitudes | (240 solicitudes * 0,5 segundos por solicitud) / 60 = 2 minutos |
| Anulaciones de productos | Productos con permisos o en catálogo compartido (P): 10000, Grupos de clientes afectados (CG): 5, Sitios web asignados WS: 2 | P \* WS * CG = 100000 | 100000 / Tamaño del lote (100) = 1000 solicitudes | (1000 solicitudes * 0,5 segundos por solicitud) / 60 = 8,3 minutos |
| Variantes del producto | Variantes (productos secundarios) asignadas a productos configurables (PV): 100000 | PV = 100000 | 100000 / Tamaño del lote (100) = 1000 solicitudes | (1000 solicitudes * 0,5 segundos por solicitud) / 60 = 8,3 minutos |
| Permisos de categoría | Recuento de todos los permisos de categoría + 4 registros de reserva (CP): 10000 | CP = 10000 | 10000 / Tamaño del lote (100) = 100 solicitudes | (100 solicitudes * 0,5 segundos por solicitud) / 60 = 0,8 minutos (50 segundos) |
| Estado de stock de inventario | Productos (P): 10000, Existencias Productos asignados a (S): 5 (suponiendo que cada producto se asigna a cada stock) | P * S = 50000 | 50000 / Tamaño del lote (100) = 500 solicitudes | (500 solicitudes * 0,5 segundos por solicitud) / 60 = 4,2 minutos |
| Pedidos de venta | Todos los registros de pedidos (facturas, envíos, etc.) (PC): 10000 | SO = 10000 | 10000 / Tamaño del lote (100) = 100 solicitudes | (100 solicitudes * 0,5 segundos por solicitud) / 60 = 0,8 minutos (50 segundos) |
