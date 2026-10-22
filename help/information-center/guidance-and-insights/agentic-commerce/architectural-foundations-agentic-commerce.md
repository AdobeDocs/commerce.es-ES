---
title: Diseño de una plataforma de Commerce para compradores y agentes de IA
description: Aprenda a crear una plataforma de comercio que sirva a los compradores humanos y a los agentes de IA desde una única fuente de verdad, desde el diseño de catálogos y el MCP hasta la telemetría.
role: Developer, Leader
recommendations: noCatalog
autotag-review: '2026-10-20T20:32:40.424Z'
TQID: 'https://experienceleague.adobe.com/ub4oTxr4IfLGgqqz0S1npY-sn0FZb3mKq-GdjD9eDjI'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: 3dcbfa9e-51f8-569c-a0e4-7f59098f730f
    internal-label: Payments
  - id: 4067ab89-2e97-5de1-8d98-de8318461a8d
    internal-label: Products
  - id: 4239b8a6-e74f-567d-a7a5-b98b9ead0ea4
    internal-label: Observability
  - id: 4820f335-ec9f-5611-8fe3-f5b7e3e56967
    internal-label: Orders
  - id: 8cd50456-5eb0-5364-922a-f14161feb828
    internal-label: Checkout
  - id: b5f00040-57a0-4a6d-a39e-383b1936c2c9
    internal-label: Compliance
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
    internal-label: Security
  - id: c32adafa-ed01-4b31-997e-2413013911b0
    internal-label: Integrations
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
    internal-label: Storefront
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
    internal-label: Architecture
  - id: c4f010fa-1478-4300-a88d-706fbc036a7a
    internal-label: APIs and SDKs
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
topic_v2:
  - id: b4dd41a7-ccf8-4e9d-918e-acaab534a307
    internal-label: Data quality
  - id: bbbea26f-9621-49eb-9ab8-e06fb3bbce8c
    internal-label: Artificial intelligence
  - id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adeb
    internal-label: Governance
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
  - id: e1e0219c-f879-479f-8427-888ed2a6e9c2
    internal-label: Insights
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
    internal-label: Privacy
source-git-commit: f54c816fd23786ec519d5c890bc2664c3dcf8c6f
workflow-type: tm+mt
source-wordcount: '1339'
ht-degree: 0%
---

# Diseño de una plataforma de comercio para compradores y agentes de IA

<table style="table-layout:auto">
<tr style="border: 0;">
   <td valign="middle" style="vertical-align: middle;"><img alt="Retrato de Surya Lamech" src="../../assets/guidance-and-insights/agentic-commerce-author-avatar-slamech.png" width="96"><br><strong>Surya Lamech</strong><br><em>Gerente principal de mercadotecnia del producto</em></td>
</tr>
</table>

![Ilustración heroica de una plataforma de comercio auténtica donde los seres humanos y los agentes de IA interactúan con una única fuente de verdad](../../assets/guidance-and-insights/agentic-commerce-hero.png "Los fundamentos arquitectónicos de una plataforma de comercio auténtica")

*Diseñando una plataforma de comercio donde los humanos y los agentes de IA interactúen con una única fuente de verdad.*

Commerce está experimentando un cambio estructural. Los clientes ya no dependen únicamente de los motores de búsqueda o de la navegación por las tiendas para explorar sus opciones. En su lugar, están recurriendo a interfaces con tecnología LLM, asistentes basados en chat y herramientas de compra auténticas para hacer preguntas, comparar productos entre minoristas y acelerar la toma de decisiones en las primeras etapas.

Estas interfaces son motores potentes para la detección, la educación y la comparación. Ayudan a los clientes a aclarar sus necesidades, evaluar sus compensaciones y reducir las opciones más rápido que la navegación tradicional.

Sin embargo, cuando llega el momento de completar una compra, los clientes siguen prefiriendo abrumadoramente tiendas de confianza y sitios de propiedad de la marca donde la seguridad de pago, la transparencia de cumplimiento y el servicio posterior a la compra se entienden bien. La conversión permanece anclada en entornos en los que ya se ha establecido la confianza.

Es importante destacar que la IA no desaparece en este momento. Cuando los clientes llegan a la tienda de una marca, la IA auténtica puede mejorar la experiencia guiando la selección de productos, personalizando las recomendaciones en tiempo real, respondiendo a las objeciones, agrupando elementos complementarios y optimizando el cierre de compra. En estos entornos de confianza, la IA se convierte en un acelerador de conversiones, lo que mejora las tasas de finalización y aumenta el valor de pedido promedio.

Para competir en este nuevo panorama, las empresas necesitan una base comercial **estructurada, controlada y optimizada tanto para el consumo humano como para el consumo de los agentes**. Adobe Commerce está diseñado para este cambio y los principios siguientes describen lo que se necesita para estar verdaderamente preparado para el agente.

## Arquitectura de comercio diseñada para dos audiencias

![Diagrama que muestra tiendas y aplicaciones para humanos a la izquierda y asistentes de chat y agentes autónomos a la derecha, ambos a partir de un núcleo central de Commerce de productos, precios, inventario, promociones, carrito y pago que se expone a través de API y MCP](../../assets/guidance-and-insights/agentic-commerce-foundational-model.png){width="800" zoomable="yes"}

*Lo que ven los clientes y lo que consumen los agentes se mantienen coherentes, precisos y dentro de la marca.*

La pila de comercio moderno ahora debe servir a dos audiencias igualmente importantes: personas y agentes de IA. Las experiencias con rostro humano, como tiendas y aplicaciones, siguen siendo esenciales para la participación, la expresión de la marca y la lealtad de los clientes. Pero junto a ellos se encuentra una superficie orientada al agente en rápida expansión: puntos finales legibles por máquina que proporcionan a los LLM y agentes autónomos hechos estructurados, contenido controlado y capacidades transaccionales.

Los agentes funcionan mejor cuando trabajan con datos limpios y estructurados que se entregan a través de API predecibles en lugar de intentar interpretar JavaScript o deducir reglas empresariales a partir de capas de presentación. Esto significa que las especificaciones del producto, los precios, la disponibilidad y la lógica promocional deben existir como recursos direccionables expuestos a través de API e interfaces estandarizadas como servidores MCP. Cuando las superficies orientadas al ser humano y al agente se basan en la misma fuente de verdad subyacente, las marcas garantizan que lo que ven los clientes y los agentes que consumen sigan siendo coherentes, precisos y propios de la marca.

Esta arquitectura de doble superficie es la base del comercio auténtico.

## Un catálogo diseñado para el razonamiento automático

![Diagrama que muestra entidades de producto estructuradas (SKU, atributos, variantes, paquetes, precios y disponibilidad) moldeadas por capas de catálogo y políticas, y luego entregadas a través de vistas de catálogo a una tienda de marca, mercado, fuente de socios, aplicación móvil y superficie de IA o agente](../../assets/guidance-and-insights/agentic-commerce-agent-interaction.png){width="800" zoomable="yes"}

*Una fuente fiable regida, formada por canal sin ramificar nunca los datos del producto.*

El catálogo es el núcleo del comercio auténtico. Debe estar estructurada para máquinas, regida por el cumplimiento normativo y ser lo suficientemente flexible como para admitir toda la gama de interacciones humanas y de agentes. El modelo de catálogo de Adobe Commerce creado en torno a vistas de catálogo, directivas, capas y entidades de producto estructuradas está diseñado para este futuro.

Las vistas de catálogo definen dónde y cómo se exponen los datos del producto, ya sea en una tienda, un mercado, una fuente de socios o una superficie de IA. Cada vista puede incluir su propia disponibilidad de productos, precios y reglas de visibilidad de atributos, lo que garantiza que la información correcta llegue al consumidor o agente adecuado. Las capas de catálogo permiten enriquecer los datos de producto para canales específicos sin modificar los datos de producto de origen. Las políticas rigen la idoneidad del cliente, la lógica de inventario, los precios y las restricciones de conformidad. En conjunto, las empresas tienen un control preciso sobre los datos de catálogo a los que un agente puede acceder o sobre los que puede actuar.

## Los MCP como idioma común para los agentes

![Diagrama que muestra asistentes de compras, agentes de soporte y herramientas para desarrolladores que envían solicitudes a través del protocolo de contexto de modelo, que incluye el MCP de Commerce y el MCP para desarrolladores, a funciones de Adobe Commerce como la creación del carro de compras, el cierre de compra, los pagos, el inventario y las promociones y devoluciones](../../assets/guidance-and-insights/agentic-commerce-reference-stack.png){width="800" zoomable="yes"}

*MCP estandariza la manera en que los agentes solicitan acciones por intención natural, y Adobe Commerce las lleva a cabo como acciones determinísticas y gobernadas.*

Para que Agentic Commerce funcione de extremo a extremo, las plataformas de comercio electrónico deben admitir protocolos estandarizados que permitan a los agentes ejecutar acciones de forma segura, como la creación del carro de compras, el inicio del cierre de compra, la orquestación de pagos, la validación del inventario, las promociones y las devoluciones.

Mediante la compatibilidad nativa con el Protocolo de contexto de modelo (MCP), Adobe estructura y expone las capacidades de comercio de una manera que los LLM pueden interpretar de manera coherente. MCP estandariza cómo se presentan los datos de productos, las reglas de negocio y el contexto transaccional a los LLM, lo que garantiza que los agentes puedan razonar sobre ellos de forma fiable mientras las empresas mantienen la gobernanza y el control. Con el MCP de Commerce, las empresas pueden crear experiencias auténticas personalizadas, como asistentes de compras, creación de carros de compras auténticos, agentes de asistencia y mucho más.

El MCP para desarrolladores incorpora funciones de desarrollo impulsadas por IA que permiten a los equipos ampliar rápidamente la funcionalidad de la plataforma e implementar componentes de tienda componibles. Al incorporar fuentes de conocimientos, documentación y prácticas recomendadas de Adobe directamente en el flujo de trabajo de desarrollo, el MCP de desarrollador ayuda a los nuevos desarrolladores a incorporarse más rápido y a ser productivos desde su primer sprint. Genera código que sigue patrones arquitectónicos comprobados, es fácil de mantener y cumple con los estándares de calidad que exige el comercio empresarial. El resultado es un camino acelerado de la idea a la producción, que da a las empresas la velocidad para experimentar, iterar y enviar capacidades de comercio por delante de los competidores.

Adobe también se compromete a admitir protocolos de comercio auténticos, como el Protocolo Commerce agéntico (ACP) y el Protocolo Commerce universal (UCP), lo que permite descubrir productos e interacciones transaccionales seguras y basadas en estándares entre los agentes y su tienda.

Al adoptar protocolos abiertos en lugar de integraciones puntuales, Adobe garantiza que las interacciones comerciales estén gobernadas, sean deterministas y seguras, a la vez que permite un nuevo modelo de participación de agente a comerciante en el que los agentes de confianza pueden realizar transacciones directamente bajo políticas claramente definidas.

## Telemetría y optimización continua

En un ecosistema mediado por IA, la telemetría se convierte en la ventaja estratégica. Las empresas necesitan visibilidad sobre cómo se representa su marca en los LLM, con qué precisión los agentes representan su contenido, cómo se convierte el tráfico referido por el agente y dónde surgen los problemas de gobernanza o cumplimiento. También necesitan telemetría operativa que rastree la ejecución del agente y la detección de anomalías en las interacciones del agente.

Adobe le ofrece visibilidad sobre cómo aparecen sus productos en los LLM, mejora los datos de productos con IA y aumenta la legibilidad de los datos por parte de LLMS. Al añadir un contexto significativo al catálogo, ayuda a los LLM no solo a descubrir sus productos con precisión, sino también a comprender cuáles son, para quién son y por qué importan a los clientes.

Además, las páginas de detalles del producto que se han optimizado para el consumo humano a menudo pueden tener datos invisibles para los agentes. Estos datos se pueden ocultar detrás de modelos, configuradores y páginas vinculadas. Los agentes pueden no comprender completamente las categorías de productos, los paquetes y las variantes. Adobe puede identificar esta información esencial que falta e implementarla como JSON-LD en el perímetro de para que los agentes puedan obtener todos los datos de productos relevantes.

Gracias a esta constante telemetría y optimización, las marcas pueden garantizar la máxima visibilidad y seguir siendo competitivas en todos los LLM.

## Por qué esto importa

El comercio electrónico ya no se limita a las tiendas y los resultados de búsqueda. Los LLM y los agentes autónomos median cada vez más en el descubrimiento, la evaluación y las transacciones. Este cambio cambia la mecánica de la visibilidad, la dinámica del control y los fundamentos de la confianza. Las marcas ganadoras serán las arquitectas de una fundación nativa de IA.

## Directrices relacionadas

* [Vistas de catálogo](/help/optimizer/setup/catalog-view.md)
* [Capas de catálogo](/help/optimizer/setup/catalog-layer.md)
* [Políticas](/help/optimizer/setup/policies.md)
* [Herramientas para desarrolladores de codificación de IA para Adobe Commerce App Builder](/help/cloud-service/migration/coding-tools.md)
* [API de Commerce](../../apis/commerce-apis.md)
* [Lista de reproducción de Commerce Developer Agent](https://experienceleague.adobe.com/es/playlists/commerce-developer-agent): vea vídeos técnicos sobre la configuración y el uso de Commerce Developer Agent.
