---
title: Elegir una opción de Commerce
description: Compare arquitecturas de Adobe Commerce basadas en la propiedad de la transacción, el modelo de implementación y las necesidades de comercialización.
role: Admin, Developer, Leader, User
feature: Storefront, Integration, Configuration
recommendations: noCatalog
TQID: 'https://experienceleague.adobe.com/5y0IU5nji50eqfFNQHbVDV-R81Mx0I8v5Y0a6nccL-w'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: cdf0c6dd-1717-4e20-9530-a24eee57088b
    internal-label: Commerce on Cloud
  - id: b974b164-8a4e-43b8-a9e2-8e67ec131677
    internal-label: Commerce on Prem
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
feature_v2:
  - id: 22bad240-8308-569b-a9d5-578f1ff890ca
    internal-label: Customers
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 58c984c2-e237-5c50-9718-500e40d1e82c
    internal-label: Merchandising
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
  - id: 6388cf7b-8a81-5248-a1e4-7bb57bbe250f
    internal-label: Install
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: 8d0b446f-5b16-5a10-b272-01143504a11c
    internal-label: System
  - id: bcd8874c-7b93-5596-bdaa-22660e84df14
    internal-label: Deploy
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
    internal-label: Order Management System
  - id: cc04bd17-78d5-5120-8c3d-1b8a57e49280
    internal-label: Integration
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: d3b92bef-63fa-5031-a925-d04d9362d616
    internal-label: Saas
  - id: da76473c-f99b-5ad0-9b14-896aed473f8a
    internal-label: Services
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
    internal-label: Configuration
  - id: dec06508-d41f-555a-87e8-29e8bcdfa95a
    internal-label: Recommendations
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
topic_v2:
  - id: b5ce8718-c3af-4fdb-a1a9-fca32f83a87c
    internal-label: Implementation
source-git-commit: 4c3c267873a68560a885c6376cd1137a7503710a
workflow-type: tm+mt
source-wordcount: '565'
ht-degree: 0%
---

# Elija una opción de Commerce.

Comience por identificar a qué sistema pertenece el carro de compras, el cierre de compra, los pedidos y otras transacciones. A continuación, elija la ruta de comercialización que se ajuste a ese back-end.

## Preguntas para guiar su decisión

Utilice las siguientes preguntas para identificar qué opciones evaluar. Tenga en cuenta el back-end de comercio existente, cuánta responsabilidad de infraestructura desea conservar y si necesita mejorar el descubrimiento y la comercialización de productos. Adobe Commerce Optimizer proporciona funcionalidades de detección y comercialización. No reemplaza el backend que gestiona las transacciones.

1. **¿Desea que Adobe administre la plataforma Commerce como software como servicio (SaaS)?**
   - Sí: Evalúe Adobe Commerce as a Cloud Service.
   - No: Si necesita Adobe Commerce y desea mantener el control sobre su infraestructura en la nube o local, realice la evaluación de Adobe Commerce en la nube o local.
1. **¿Necesita Adobe Commerce para administrar el carro de compras, el cierre de compra, los pedidos y otras transacciones?**
   - Sí: Evalúe Adobe Commerce en la nube o de forma local, o Adobe Commerce as a Cloud Service. Estas opciones utilizan Commerce Foundation como backend transaccional.
   - No: Conserve el back-end transaccional existente o de terceros. Si también necesita funcionalidades de detección y comercialización de Adobe, evalúe Adobe Commerce Optimizer independiente.
1. **¿Desea usar Adobe Commerce Optimizer para mejorar la detección de productos y la comercialización con su backend de comercio de terceros existente?**
   - Sí: Evalúe la Adobe Commerce Optimizer independiente y mantenga el servidor de terceros para las transacciones.
1. **¿Ya utiliza Adobe Commerce en la nube o de forma local y desea una detección y comercialización más sólidas?**
   - Sí: Evalúe el conector de Adobe Commerce Optimizer para sincronizar los datos de catálogo y de precios mientras Adobe Commerce sigue gestionando las transacciones.

Utilice la siguiente tabla comparativa para ajustar sus respuestas a un punto de partida. Para ver diagramas detallados del sistema, consulte [Opciones de arquitectura](../architecture-options/overview.md).

## Comparar opciones de Commerce

| Su requisito | Punto de partida recomendado | Sistema propietario de transacciones | Comercialización y descubrimiento |
| --- | --- | --- | --- |
| Adobe administra la plataforma de Commerce como SaaS. | [Adobe Commerce as a Cloud Service](/help/cloud-service/overview.md) | Adobe Commerce as a Cloud Service Foundation | Utilice los servicios de Commerce proporcionados para Adobe Commerce as a Cloud Service. Para conocer la disponibilidad de la integración de Adobe Commerce Optimizer, consulte la nota debajo de esta tabla. |
| Necesita Adobe Commerce y desea conservar el control sobre su infraestructura en la nube o local. | [Adobe Commerce en la nube o local](https://experienceleague.adobe.com/en/docs/commerce-admin/start/guide-overview) | Adobe Commerce Foundation | Utilice los servicios de Commerce compatibles según sea necesario. |
| En Adobe Commerce en la nube o de forma local, y desea adoptar Adobe Commerce Optimizer para la detección y comercialización. | Adobe Commerce con [conector Adobe Commerce Optimizer](/help/aco-connector/overview.md) | Adobe Commerce sigue siendo el sistema de registro de las transacciones. | El conector sincroniza los datos del catálogo y los precios con Adobe Commerce Optimizer, que proporciona experiencias de descubrimiento y comercialización. |
| Disponer de un servidor de comercio de terceros y querer la detección y comercialización de Adobe Commerce Optimizer sin reemplazar ese servidor. | [Adobe Commerce Optimizer](/help/optimizer/overview.md) independiente | Su servidor de comercio de terceros | Envío de datos de catálogo y precio a Adobe Commerce Optimizer. Integre el carro de compras, el cierre de compra y otras operaciones transaccionales con el back-end a través de API Mesh, App Builder o una integración directa. |

>[!NOTE]
>
>La integración entre Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer está en la hoja de ruta de Commerce. Si necesita ambas plataformas, planifique utilizarlas como opciones de arquitectura independientes por ahora. Póngase en contacto con el administrador de cuentas de Adobe para obtener más información sobre la cronología de la integración.

## Directrices relacionadas

- [Plataformas y servicios](platform-and-services.md)
- [Opciones de arquitectura](../architecture-options/overview.md)
- [Introducción](../get-started/get-started-by-role.md)
