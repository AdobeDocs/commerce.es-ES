---
title: Calcular el volumen de datos y el tiempo de sincronización
description: Aprenda a calcular el volumen de datos y el tiempo de sincronización de las fuentes de  [!DNL Adobe Commerce Optimizer Connector] para planificar las sincronizaciones de catálogos y evitar interrupciones.
autotag-review: '2026-06-17T15:08:59.000Z'
role: Admin, Developer
feature: Integration, Configuration
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
feature_v2:
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: c32adafa-ed01-4b31-997e-2413013911b0
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 182aa9ce819807d1ede85c4fa459714e7dfe0478
workflow-type: tm+mt
source-wordcount: 469
ht-degree: 0%

---


# Calcular el volumen de datos y el tiempo de sincronización

Adobe recomienda estimar el volumen de datos y el tiempo de sincronización antes de iniciar cualquier sincronización de fuente para garantizar una programación sin problemas y evitar interrupciones en las operaciones del sitio. Esto es especialmente importante a la hora de planificar sincronizaciones iniciales o actualizaciones de catálogos a gran escala, como cambios masivos de precios.

De forma predeterminada, el conector procesa las fuentes en modo de un solo subproceso. No hay paralelización en el proceso de envío de fuentes. La API de ingesta acepta hasta 2 solicitudes por segundo. Sin embargo, la asignación base para la tasa de ingesta [!DNL Adobe Commerce Optimizer] limita el rendimiento a lo siguiente:

- Hasta 1000 productos por minuto (un producto es un SKU con atributos en una vista de tienda específica). Consulte [Límites y límites](../../optimizer/boundaries-limits.md) para obtener detalles de asignación base.
- Hasta 50.000 precios por minuto

## Factores que afectan al tiempo de sincronización

Las siguientes estimaciones asumen las siguientes condiciones:

- Recuento de hilos: 1 (predeterminado)
- Tasa de aceptación de fuentes: 2 solicitudes por segundo (0,5 segundos por solicitud)
- Todos los productos se asignan a todos los sitios web existentes

La velocidad de transmisión real varía según el tamaño de la carga útil de la solicitud y la carga actual en el servidor de aplicaciones de Commerce.

## Calcular el tiempo de sincronización por fuente

Utilice la siguiente tabla para calcular el número de registros, solicitudes y tiempo de sincronización para cada fuente del conector. Los valores de tamaño de lote reflejan los límites definidos en la referencia de [fuentes admitidas](connector-reference.md#supported-feeds).

>[!NOTE]
>
>El tiempo de sincronización de productos se basa en el límite base de asignación de 1000 productos por minuto. Para otras fuentes, los cálculos se basan en una tasa de transmisión de 2 solicitudes por segundo. La velocidad real depende del tamaño de la carga útil y de la carga del servidor.
>
>La estimación de precios supone que todos los grupos de clientes tienen precios únicos.

| Fuente | Ejemplo de datos | Fórmula | Solicitudes previstas | Tiempo de sincronización previsto |
| ---- | ------------ | ------- | ------------------ | ------------------- |
| Productos | Productos (P): 10.000, Vistas de la tienda (SV): 4 | P × SV = 40 000 registros | Tamaño de lote de 40 000 ÷ (100) = 400 | 40.000 ÷ 1.000 registros/min = **40 min** |
| Categorías | Categorías (C): 500, Vistas de la tienda (SV): 4 | C × SV = 2000 registros | Tamaño de lote de 2.000 ÷ (100) = 20 | (20 × 0,5 s) ÷ 60 = **~10 s** |
| Atributos del producto | Atributos (A): 200, Vistas de tienda (SV): 4 | A × SV = 800 registros | Tamaño de lote de 800 ÷ (100) = 8 | (8 × 0,5 s) ÷ 60 = **~4 s** |
| Precios | Productos (P): 10 000, Sitios web (WS): 2, Grupos de clientes (CG): 6 | P × WS × CG = 120 000 registros | Tamaño de lote de 120 000 ÷ (500) = 240 | (240 × 0,5 s) ÷ 60 = **2 min** |
| Libros de precios | Sitios web (WS): 2, Grupos de clientes (CG): 6 | WS × CG = 12 registros | Tamaño de lote de 12 ÷ (500) = 1 | (1 × 0,5 s) ÷ 60 = **&lt; 1 s** |

>[!MORELIKETHIS]
>
> - [Módulos de conector y extremos de fuente](connector-reference.md): revise los límites por lotes y las fuentes admitidas
> - [Administrar sincronización](../data-sync-manage.md): supervisar el estado de sincronización y la resincronización manual del déclencheur
> - [Canalización de sincronización de conectores](../connector-sync-pipeline.md): comprenda cómo funcionan las programaciones cron y la sincronización automatizada
