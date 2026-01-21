---
title: Migrar a [!DNL Adobe Commerce as a Cloud Service]
description: Obtenga información sobre cómo migrar a [!DNL Adobe Commerce as a Cloud Service].
feature: Cloud
exl-id: 9065c92a-f6b2-4464-8ec0-5c549bf78104
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Se aplica a Adobe Systems Commerce como Cloud Service y solo a Adobe Systems proyectos de Commerce Optimizer (infraestructura SaaS administradas por Adobe Systems)."
role: Developer
level: Intermediate
source-git-commit: af56d52f98a83310b858f82f16693f5323c1b962
workflow-type: tm+mt
source-wordcount: '3016'
ht-degree: 0%

---

# Migrar a [!DNL Adobe Commerce as a Cloud Service]

[!DNL Adobe Commerce as a Cloud Service] proporciona una guía completa para los desarrolladores que realizan la transición de una implementación PaaS de Adobe Systems Commerce existente a la nueva oferta de Adobe Systems Commerce as a Cloud Service (SaaS). Adobe Systems Commerce as a Cloud Service representa un cambio significativo hacia un modelo SaaS totalmente administrado y sin versión, que ofrece un rendimiento mejorado, escalabilidad, operaciones simplificadas y una integración más estrecha con el .[!DNL Adobe Experience Cloud]

>[!NOTE]
>
>Para obtener más información sobre las herramientas de migración, consulte la [herramienta](./bulk-data.md) de migración masiva de datos.

## Comprender el cambio: comparar PaaS y SaaS

**Diferencias clave**

* [!BADGE Solo PaaS PaaS (actual):]{type=Informative url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Systems Commerce on Cloud (infraestructura PaaS administrada por Adobe Systems) y proyectos locales."} el comerciante administra el **&#x200B;**&#x200B;código de aplicación, las actualizaciones, la aplicación de parches y la configuración de la infraestructura dentro del entorno alojado de Adobe Systems. [Modelo](https://experienceleague.adobe.com/es/docs/commerce-operations/security-and-compliance/shared-responsibility) de responsabilidad compartida para servicios (MySQL, Elasticsearch y otros).
* [!BADGE Solo]{type=Positive url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Se aplica a Adobe Systems Commerce como Cloud Service y solo a Adobe Systems proyectos de Commerce Optimizer (infraestructura SaaS administradas por Adobe Systems)."} **SaaS SaaS (Nuevo - [!DNL Adobe Commerce as a Cloud Service])**: Adobe Systems administra completamente el aplicación central, la infraestructura y las actualizaciones. Los comerciantes se centran en la personalización a través de puntos de extensibilidad (API, App Builder, SDK de IU). Código de la aplicación principal bloqueado.

**Implicaciones arquitectónicas**

* **Plataforma sin** versiones: Las actualizaciones continuas significan que no hay más actualizaciones de versiones importantes para el núcleo.
* **Microservicios y API primero**: mayor dependencia de las API para la extensibilidad y la integración.
* **Sin periféricos de forma predeterminada (opcional):** compatibilidad sólida para escaparates desacoplados (por ejemplo, Commerce Storefront con tecnología de Edge Delivery Services).
* **Edge Delivery Services**: Impacto en el rendimiento y la implementación del front-end.

**Nuevo herramientas y conceptos**

* [Adobe Developer App Builder](https://developer.adobe.com/app-builder/) y [API Mesh para Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway)
* [Commerce Optimizer](../../optimizer/overview.md)
* [Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=es)
* Aprovisionamiento de autoservicio con [Commerce Cloud Manager](../getting-started.md#create-an-instance)

## Rutas de migración

[!DNL Adobe Commerce as a Cloud Service] Admite varias rutas de migración en función de su cronología, escaparate y personalizaciones.

Como alternativa a una migración completa, [!DNL Adobe Commerce as a Cloud Service] admite una migración por fases mediante Commerce Optimizer o un método incremental.

* **Migración incremental**: este enfoque implica migrar los datos, las personalizaciones y las integraciones por fases. Este enfoque es ideal para grandes comerciantes con muchas personalizaciones que deseen realizar una transición gradual de sus personalizaciones y datos complejos a [!DNL Adobe Commerce as a Cloud Service] a su propio ritmo.

![migración incremental](../assets/incremental.png){width="600" zoomable="yes"}

* **Commerce Optimizer**: este enfoque le permite migrar de forma iterativa, utilizando Commerce Optimizer como una fase de transición para mover personalizaciones y datos complejos a [!DNL Adobe Commerce as a Cloud Service] a su propio ritmo. Commerce Optimizer proporciona acceso a los servicios de comercialización con vistas y directivas de catálogo, Commerce Storefront con tecnología Edge Delivery y [!DNL Product Visuals powered by AEM Assets].

![Migración iterativa](../assets/optimizer.png){width="600" zoomable="yes"}

* **Migración** completa: este enfoque implica migrar todos los datos, personalizaciones e integraciones a la vez. Este enfoque es ideal para comerciantes más pequeños con pocas personalizaciones que desean transición rápidamente a [!DNL Adobe Commerce as a Cloud Service].

La tabla siguiente proporciona una descripción general del proceso de migración para diferentes escaparates y configuraciones:

|                    | Escaparate LUMA | PWA escaparate | Commerce Storefront con tecnología de Edge Delivery | Sin cabeza |
|--------------------|----------------------------------------|----------------------------------------|------------------------------------------------------|----------------------------------------|
| Migración de datos | Obligatorio | Obligatorio | Obligatorio | Obligatorio |
| Escaparate | Migrar a Commerce Storefront con tecnología de Edge Delivery | Migrar a Commerce Storefront con tecnología de Edge Delivery o mantener | Sin impacto | Sin impacto |
| Malla de API | Crear nueva red | Cree una red nueva o reconfigure las existentes. | Cree una red nueva o reconfigure las existentes. | Cree una red nueva o reconfigure las existentes. |
| Integraciones | Aproveche el kit de inicio de integración | Aproveche el kit de inicio de integración | Aproveche el kit de inicio de integración | Aproveche el kit de inicio de integración |
| Personalizaciones | Muévase a aplicación Builder y API Mesh | Muévase a aplicación Builder y API Mesh | Muévase a aplicación Builder y API Mesh | Muévase a aplicación Builder y API Mesh |
| Administración de Assets | Migración necesaria si se usa OOTB | Migración necesaria si se usa OOTB | Migración necesaria si se usa OOTB | Migración necesaria si se usa OOTB |
| Extensiones | Migrar a aplicación Builder | Migrar a aplicación Builder | Migrar a aplicación Builder | Migrar a aplicación Builder |

Como se indica en la tabla, las mitigaciones para cada migración consistirán en:

* **Migración de datos**: Se está utilizando la [herramienta de migración](./bulk-data.md) proporcionada para migrar datos de su instancia existente a [!DNL Adobe Commerce as a Cloud Service].
* **Escaparate**: los escaparates de comercio existentes con tecnología de Edge Delivery y los escaparates sin cabeza no requieren mitigación, pero los escaparates de Luma requieren migrar a Commerce Storefront con tecnología de Edge Delivery. PWA Studio escaparates se pueden migrar a Commerce Storefront con tecnología de entrega perimetral o mantener en su estado actual. Adobe Systems proporcionará aceleradores para ayudar con la migración de escaparates.
* **[API Mesh](https://developer.adobe.com/graphql-mesh-gateway)**: Crear una nueva red o modifique la existente. Adobe Systems proporcionará mallas preconfiguradas para ayudarle en este proceso.
* **Integraciones**: todas las integraciones deben impulsar el kit[&#x200B; de inicio de &#x200B;](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/)integración o la [[!DNL Adobe Commerce as a Cloud Service] API](https://developer.adobe.com/commerce/webapi/reference/rest/saas/) de REST.
* **Personalizaciones**: todas las personalizaciones deben moverse a aplicación Builder y API Mesh.
* **Administración de Assets**: la administración de todos los recursos requiere migración. Si ya está usando [!DNL AEM Assets], no es necesario migrar.
* **Extensiones**: todas las extensiones en proceso deben volver a crearse como extensiones fuera de proceso. A finales de 2025, Adobe proporcionará acceso a nuestras extensiones más populares para minimizar los tiempos de compilación.

## Fases de migración

En las siguientes fases se describen los pasos y consideraciones necesarios para migrar a [!DNL Adobe Commerce as a Cloud Service].

### Planificación y evaluación previas a la migración

Esta fase es crítica para minimizar los riesgos, establecer una ruta de migración clara e identificar los problemas antes de que surjan.

**Descubrimiento y auditoría de entorno actuales**

**El código base análisis:**

* Identifique todos los módulos, temáticas y anulaciones personalizados.
* Analice las modificaciones del código central y determine cuáles serán las que será necesario refactorizar como parte de la migración.
* Evalúe las extensiones de terceros y determine la compatibilidad con [!DNL Adobe Commerce as a Cloud Service]. ¿Existen alternativas compatibles con SaaS o necesita crear integraciones de API personalizadas o aplicaciones de App Builder?
* Identifique el código o la funcionalidad obsoletos que no se migrarán.

**Auditoría de datos:**

* Evalúe el tamaño y la complejidad de la base de datos.
* Identificar datos o tablas no utilizados para su limpieza.
* Revise los procesos de importación/exportación de datos existentes.

**Revisión de integraciones:**

* Enumere todos los sistemas externos integrados con Adobe Systems Commerce (ERP, CRM, GIP, pasarelas de pago, proveedores de envío, OMS y cualquier otro sistema).
* Evaluar los métodos de integración (API, scripts personalizados y otros métodos).
* Evalúe la compatibilidad con [!DNL Adobe Commerce as a Cloud Service]el enfoque API-first de y aplicación Builder.

**Prueba comparativa de desempeño:**

* Documente las puntuaciones actuales de Lighthouse, los tiempos de carga Página y los indicadores clave de rendimiento (KPI), lo que proporciona una línea de base para medir mejoras en la migración de entrada.

**Revisión de la configuración de seguridad:**

* Evalúe las reglas WAF personalizadas, las listas de direcciones IP permitidas y cualquier otra configuración de seguridad.

**Definir ámbito y estrategia de migración:**

* **Migración gradual frente a migración de todo a la vez:** evalúe los pros y los contras de cada enfoque.
* **Identifique los principales procesos empresariales:** priorice las funcionalidades que deben migrarse primero, como:
   * Reglas de precios complejas
   * Reglas empresariales personalizadas aplicadas antes de que un pedido se realice o procese oficialmente
   * Cálculos de impuestos complejos
   * Validaciones de direcciones
   * Lógica personalizada que se activa después de realizar un pedido
* **Escaparate sin cabeza vs. monolítico:** Punto de decisión para el desarrollo de nuevos escaparates o la adaptación de escaparates existentes.
* **Estrategia de integración:** Determine cómo se cambiará la plataforma de las integraciones existentes (API Mesh, aplicación Builder, API directa).
* **Estrategia de migración de datos:** determine si desea migrar utilizando datos datos históricos completos, datos parciales o ningún dato migrado.

**Preparación del equipo y aprendizaje:**

* Familiarícese con [!DNL Adobe Commerce as a Cloud Service] conceptos, flujos de trabajo de desarrollo y nuevas herramientas.
* Asista a aprendizaje prácticos con Adobe Systems aplicación Builder, Edge Delivery Services y [!DNL Adobe Commerce as a Cloud Service] implementación canalizaciones.

**Configuración y aprovisionamiento del entorno:**

* Aprovisione [!DNL Adobe Commerce as a Cloud Service] el entorno de pruebas y los entornos de desarrollo con el Administrador de Commerce Cloud.

### Fases de migración incrementales

**Refactorización y externalización estratégicas**

Esta fase consiste en el núcleo de la migración, centrado en la adaptación de [!DNL Adobe Commerce as a Cloud Service] su base de código al paradigma nube-nativa. Esto implica adoptar estratégicamente nuevos servicios Adobe Systems y sacar la lógica personalizada de la plataforma central de Commerce.

#### &#x200B;1. Migrar personalizaciones y extensiones &quot;en proceso&quot; a aplicación Builder

Esta es una fase crucial para lograr un &quot;núcleo bloqueado&quot; y preparar su solución para el futuro, fundamental para la [!DNL Adobe Commerce as a Cloud Service] filosofía arquitectónica.

* **Externalice lógica compleja a aplicación Builder**: analice los módulos personalizados existentes y las extensiones de terceros dentro de su base de código PaaS. Para lógica empresarial complejos, integraciones a medida o microservicios que no requieren manipulación directa y en proceso del modelo de datos de comercio central, refactorícelos y vuelva a configurarlos como aplicaciones sin servidor dentro de Adobe Systems Developer aplicación Builder.
* **Aproveche la malla** de API: para escenarios que requieren datos de varios sistemas back-end (por ejemplo, su backend PaaS Commerce, ERP, CRM y microservicios personalizados de aplicación Builder), implementar una capa API Mesh dentro de aplicación Builder. Esto consolida API dispares en un único punto final de GraphQL de alto rendimiento consumido por su nueva tienda u otros servicios, simplificando la obtención de datos complejos.
* **Arquitectura** basada en eventos: Utilice eventos de E/S de Adobe Systems para activar acciones de aplicación Builder basadas en eventos que ocurren en su instancia PaaS (por ejemplo, actualizaciones de productos, registros de clientes, cambios de estado de pedidos) u otros sistemas conectados. Esto promueve la comunicación asíncrona, reduce el acoplamiento estrecho y mejora la resiliencia del sistema.

**Beneficio**: Este paso reduce significativamente la deuda técnica asociada con las personalizaciones profundamente incrustadas, acelera considerablemente la transición de la instancia de Commerce a [!DNL Adobe Commerce as a Cloud Service], mejora la escalabilidad y la implementación independiente de la lógica personalizada, y promueve ciclos de desarrollo más rápidos para las extensiones.

#### &#x200B;2. Adopte servicios de comercialización de Adobe Commerce basados en SaaS e integre datos de catálogo

Este es un punto de integración inicial crítico con dos opciones con respecto a la administración de datos del catálogo:

>[!BEGINTABS]

>[!TAB Opción 1 - Servicio SaaS de catálogo existente]

**Aproveche el servicio SaaS de catálogo existente integrado con el back-end PaaS**

Esta opción sirve como paso de transición, basado en una integración existente en la que el backend de PaaS rellena una instancia existente del servicio SaaS de Adobe Commerce con datos del [servicio de catálogo](../../catalog-service/guide-overview.md), [búsqueda activa](../../live-search/overview.md) y [recomendaciones de producto](../../product-recommendations/overview.md).

* **Sincronización de datos de catálogo**: Asegúrese de que la instancia de Adobe Commerce PaaS siga sincronizando los datos de producto y catálogo con el servicio SaaS de catálogo de Adobe Commerce existente. Esto generalmente se basa en conectores o módulos establecidos dentro de la instancia de PaaS. El servicio SaaS de catálogo sigue siendo la fuente autorizada para las funciones de búsqueda y comercialización, y deriva sus datos del backend de PaaS.
* **Mesh de API para optimización**: Aunque la tienda sin encabezado (en Edge Delivery Services) y otros servicios podrían consumir directamente datos del servicio SaaS de catálogo, Adobe recomienda encarecidamente usar Mesh de API (en App Builder). La malla de API puede unificar las API del servicio SaaS de catálogo con otras API necesarias del backend de PaaS (por ejemplo, comprobaciones de inventario en tiempo real de la base de datos transaccional o atributos de producto personalizados no replicados completamente en el servicio SaaS de catálogo) en un único extremo de GraphQL con rendimiento. Esto también permite el almacenamiento en caché, la autenticación y la transformación de respuestas centralizadas.
* **Integre Search en vivo y Recommendations** de productos: configure los servicios SaaS de Search en vivo y Recommendations de productos para [que ingieran datos](https://experienceleague.adobe.com/es/docs/commerce/live-search/install#configure-the-data) de catálogo directamente desde su servicio SaaS de catálogo de Adobe Systems Commerce Catalog existente, que a su vez se rellena con su backend PaaS.

**Beneficio**: Esto proporciona una ruta más rápida hacia una tienda sin cabeza y funciones avanzadas de comercialización SaaS al aprovechar un servicio SaaS de catálogo existente y operativo y su canalización de integración con su backend PaaS. Sin embargo, conserva la dependencia del backend de PaaS para la fuente de datos del catálogo principal y no proporciona las capacidades de agregación de varias fuentes inherentes al nuevo modelo de datos de catálogo componible. Esta opción es un trampolín válido hacia una arquitectura componible más completa.

>[!TAB Opción 2 - Modelo de datos de catálogo maquetable]

**Adoptar el nuevo Modelo de datos de catálogo compuesto (CCDM)**

Este es el enfoque estratégico y de prueba futuro para aprovechar Adobe Systems Commerce Optimizer. CCDM proporciona un servicio de catálogo flexible, escalable y unificado diseñado para la agregación de datos de varias fuentes y la comercialización dinámica.

* **Incorporación y unificación de datos**
   * Comience por incorporar datos de productos y catálogos de su instancia PaaS de comercio de Adobe Systems existente (y/u otros sistemas GIP/ERP) en el nuevo modelo de datos de catálogo componible (CCDM).
   * Asigne los atributos de producto existentes a la esquema flexible del CCDM. Priorice esencial datos de producto para la ingesta inicial.
   * Establezca canalizaciones de datos sólidas para una sincronización continua. Esto puede implicar:
      * **Impulsado por eventos** (a través de App Builder): Utilice Adobe I/O Events desde su instancia de PaaS para almacenar en déclencheur aplicaciones de Adobe App Builder personalizadas o disponibles públicamente. Estas aplicaciones transforman e insertan cambios en los datos (crean, actualizan y eliminan) en el CCDM a través de sus API.
      * **Ingesta por lotes**: Para cargas iniciales grandes o actualizaciones masivas periódicas, utilice transferencias de archivos seguras (por ejemplo, CSV o JSON) a un área de ensayo, procesadas por los servicios de ingesta de Adobe Experience Platform (AEP) en CCDM.
      * **Integración directa de API** (con orquestación de App Builder): para escenarios más complejos, App Builder puede actuar como una capa de orquestación, haciendo llamadas directas de API al servidor PaaS, transformando los datos y enviándolos a CCDM.
* **Definición vista y directiva de** catálogo: Configure vistas de catálogo (agrupaciones lógicas para la presentación única del catálogo, como vistas de tienda, regiones y segmentos B2B/B2C) y defina políticas (conjuntos de regla para presentación, filtrado y comercialización del producto) dentro del CCDM. Esto permite un control dinámico sobre las surtidos de productos y la lógica de visualización por vista de catálogo.
* **Integrar Search en vivo y Recommendations** de productos: una vez que los datos del catálogo estén presentes en CCDM, integre los servicios de Search en vivo y Recommendations de productos basados en SaaS de Adobe Systems. Estos impulsar Adobe Systems la IA y los modelos de aprendizaje automático para obtener una relevancia búsqueda superior y recomendaciones personalizadas, consumiendo datos directamente del CCDM.

**Beneficio**: Al abstraer la administración y el descubrimiento de catálogos en CCDM y los servicios SaaS asociados, logra un rendimiento mejorado, obtiene capacidades de comercialización impulsadas por IA, descarga significativamente las operaciones de lectura de su backend heredado y permite un &quot;peel-off&quot; robusto de la experiencia superior de canal.

>[!ENDTABS]

#### &#x200B;3. Construya su escaparate en Edge Delivery Services

Con comercialización canalizaciones de datos establecidas y las personalizaciones externalizadas, la enfocar cambia a la construcción de su frontend de alto rendimiento.

* **Configuración inicial**: configure el proyecto con el elemento repetitivo de Adobe Systems Commerce Storefront para Edge Delivery Services. Esto proporciona un frontend sin cabeza fundamental construido sobre tecnologías web modernas.
* **Conéctese a los servicios de catálogo y API Mesh**: Su Commerce Storefront consumirá datos principalmente a través de las API de GraphQL:
   * **Opción 1**: Desde el servicio SaaS de catálogo existente (a través de API Mesh) para obtener información del producto y reglas comercialización.
   * **Opción 2**: Desde CCDM para obtener información del producto y reglas comercialización.
   * Desde API Mesh para cualquier dato orquestado de su backend heredado (PaaS instancia) o servicios personalizados de aplicación Builder (por ejemplo, visualización de inventario en tiempo real, atributos de productos personalizados y visualización de puntos de fidelidad).
* **Migración de contenido (AEM Services):** migre sus contenido estáticos existentes (por ejemplo, páginas &quot;Acerca de nosotros&quot;, publicaciones de blog y banners marketing) a AEM Services, que impulsa Commerce Storefront. Aproveche las capacidades creación de contenido de AEM y asegúrese de activos estén optimizadas para los servicios de entrega perimetral.
* **Desarrolle componentes** de IU principales: cree componentes de interfaz de esencial usuario para páginas de detalles del producto (PDP), páginas de listado de productos (PLP) y páginas de contenido generales utilizando componentes sin cita previa de Edge Delivery Services y componentes personalizados de React/Vue. Priorizar los flujos de comercio principales.
* **Integración con carro de compras/pago existentes**: inicialmente, la tienda de Edge Delivery Services organizará una transferencia a su PaaS de comercio de Adobe Systems existente (u otra plataforma terceros) para la administración de carro de compras y el pago. Por lo general, esto implica:
   * **Redirección**: redirigir el usuario a las URL de carro de compras y de pago de nativa de la plataforma heredada, pasando los identificadores de sesión y carro de compras necesarios.
   * **Interacción** directa de API (con orquestación aplicación Builder): creación de componentes personalizados de carro de compras y IU de pago dentro de Edge Delivery Services que interactúan directamente con las API de carro de compras y cierre de compra del backend PaaS. Esto a menudo implica aplicación Builder como backend para frontend (BFF) para orquestar llamadas a múltiples servicios backend (por ejemplo, PaaS carro de compras, pasarelas de pago y calculadoras de envío).

**Beneficio**: Ofrece una experiencia de escaparate ultrarrápida, optimizada para Optimización de los motores de búsqueda y altamente flexible. Esta fase contribuye directamente a una experiencia del cliente superior y sienta las bases para la futura innovación frontend.

#### &#x200B;4. Migración de datos (proceso por fases)

La migración de datos es un proceso esencial y multifacético que se ejecuta simultáneamente con la refactorización y el desarrollo de escaparates, lo que garantiza la coherencia e integridad de los datos.

* **Limpie y optimice los datos** existentes: antes de cualquier migración a gran escala, realice una limpieza de datos integral, una deduplicación y una validación en su base de datos PaaS existente. Este paso proactivo es crucial para minimizar los problemas de transferencia de datos heredados y garantizar la calidad de los datos en el nuevo entorno.

**Migraciones masivas de datos**

La migración masiva de datos implica tomar un volcado de datos completo de su instancia PaaS de Adobe Systems Commerce, transformar toda esa conjunto de datos e importarla a Adobe Systems Commerce como un Cloud Service todo al mismo tiempo. Este método se utiliza normalmente para la población inicial de datos.

* **Disponibilidad de herramientas**: En el primer trimestre de 2026, estará disponible, previa solicitud, [la herramienta de migración de datos en lotes](./bulk-data.md) dedicada para el uso de los clientes en migraciones de datos en lotes de Commerce de origen. Si los clientes necesitan asistencia con la migración masiva de datos con antelación, Adobe puede facilitar la transferencia de datos en su nombre mediante solicitud.

* **Proceso**:
   * **Exportación** total de datos: Extract una conjunto de datos completa desde su instancia PaaS de comercio de Adobe Systems (por ejemplo, productos, categorías, cuentas de clientes, datos históricos de pedidos, bloques estáticos y Página contenido).
   * **transformación** de datos: Aplicar transformaciones necesarias para alinear los datos extraídos con los requisitos de esquema del nuevo Adobe Systems Commerce como Cloud Service componentes, incluido el Modelo de Datos de Catálogo Composable (CCDM) si se adopta, y cualquier otro servicio o base de datos Adobe Systems relevante. Esto podría implicar scripts personalizados o herramientas especializadas de asignación de datos.
   * **Importación** inicial: Importar el conjunto de datos completo transformado en los componentes respectivos de Adobe Systems Commerce como un Cloud Service. Para los datos de productos y categoría, esto rellena el servicio de catálogo elegido (CCDM o SaaS de catálogo existente). Para los datos de clientes y pedidos, esto rellena el back-end transaccional o los servicios asociados.
   * **Validación: valide** rigurosamente los datos importados para garantizar la integridad, exactitud y coherencia en todos los sistemas nuevos.

**Migraciones iterativas de datos**

Las migraciones de datos iterativas enfocar en la sincronización de cambios incrementales y deltas desde el instancia PaaS de origen a los nuevos componentes de Cloud Service, lo que garantiza la frescura de los datos antes y después del corte.

* **Disponibilidad** de herramientas: Las herramientas diseñadas específicamente para migraciones iterativas de datos estarán disponibles en 2026.

* **Proceso**:
   * **Identificación** delta: establezca mecanismos para identificar cambios (creaciones, actualizaciones y eliminaciones) en esencial conjuntos de datos en su entorno PaaS desde el último sincronizar. Esto puede implicar la captura de datos modificados (CDC), comparaciones de marcas de hora o desencadenadores basados en evento.
   * **Sincronización continua**: Implemente mecanismos sólidos para una sincronización de datos continua e incremental desde su entorno PaaS a los nuevos componentes de Cloud Service (por ejemplo, CCDM y back-end transaccional). Esto es crucial para mantener la actualización de los datos y minimizar el tiempo de inactividad durante la migración.
   * **Aprovechamiento de eventos**: Utilice Adobe I/O Events siempre que sea posible para almacenar en déclencheur las acciones de App Builder para obtener actualizaciones en tiempo real o casi en tiempo real desde su instancia de PaaS a los nuevos servicios. Por ejemplo, una actualización de producto en PaaS podría almacenar en déclencheur un evento que actualice la entrada correspondiente en CCDM.
   * **Actualizaciones controladas por API**: Para los datos que no están impulsados por eventos, utilice llamadas de API programadas (a través de App Builder u otras plataformas de integración) para extraer cambios de PaaS e insertarlos en los nuevos sistemas.
   * **Control y supervisión de errores**: Implemente funciones sólidas de control, registro y supervisión de errores para todas las canalizaciones de datos iterativas a fin de garantizar que se mantenga la integridad de los datos durante todo el proceso.

### Post migración y operaciones en curso

**Transferencia de DNS y puesta en marcha:**

* Planifique cuidadosamente el límite de DNS con un tiempo de inactividad mínimo.
* Monitoree el estado y el rendimiento del sitio inmediatamente entrada iniciar.

**Operaciones posteriores al inicio:**

**Retirada del entorno de PaaS:**

* Archive o elimine de forma segura instancias y datos PaaS antiguos después del período validación.

**Desarrollo continuo flujo de trabajo:**

* Adopte la naturaleza sin versión de , que tiene pequeñas implementaciones continuas en lugar de [!DNL Adobe Commerce as a Cloud Service]grandes actualizaciones.
* Utilice Cloud Manager para administrar entornos e implementaciones.
* Aproveche aplicación Builder para ampliar funcionalidad sin afectar al núcleo.

**Supervisión, rendimiento y seguridad:**

* Supervise continuamente el rendimiento del sitio, los errores y los registros de seguridad.
* Utilice las funciones de seguridad integradas de Adobe y siga las prácticas recomendadas.

**Formación y documentación:**

* Capacite a nuevos desarrolladores y usuarios empresariales en la plataforma y los flujos de trabajo de [!DNL Adobe Commerce as a Cloud Service].
* Mantenga actualizada la documentación interna de las integraciones y los procesos personalizados.
