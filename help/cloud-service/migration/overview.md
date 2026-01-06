---
title: Migrar a  [!DNL Adobe Commerce as a Cloud Service]
description: Obtenga información sobre cómo migrar a  [!DNL Adobe Commerce as a Cloud Service].
feature: Cloud
exl-id: 9065c92a-f6b2-4464-8ec0-5c549bf78104
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
role: Developer
level: Intermediate
source-git-commit: 3fe22d47b6fd6cf1077cbd4644ffad08f55826ca
workflow-type: tm+mt
source-wordcount: '3020'
ht-degree: 0%

---

# Migrar a [!DNL Adobe Commerce as a Cloud Service]

[!DNL Adobe Commerce as a Cloud Service] proporciona una guía completa para los desarrolladores que realizan la transición de una implementación de Adobe Commerce PaaS existente a la nueva oferta de Adobe Commerce as a Cloud Service (SaaS). Adobe Commerce as a Cloud Service representa un cambio significativo a un modelo SaaS completamente administrado y sin versiones, que ofrece rendimiento mejorado, escalabilidad, operaciones simplificadas e integración más estrecha con el [!DNL Adobe Experience Cloud] más amplio.

>[!NOTE]
>
>Para obtener más información sobre las herramientas de migración, consulte [Herramienta de migración de datos en lotes](./bulk-data.md).

## Explicación del cambio: comparación de PaaS y SaaS

**Diferencias clave**

* [!BADGE Solo PaaS]{type=Informative url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."} **PaaS (actual)**: El comerciante administra el código de la aplicación, las actualizaciones, los parches y la configuración de la infraestructura dentro del entorno alojado de Adobe. [Modelo de responsabilidad compartida](https://experienceleague.adobe.com/es/docs/commerce-operations/security-and-compliance/shared-responsibility) para servicios (MySQL, Elasticsearch y otros).
* [!BADGE Solo SaaS]{type=Positive url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."} **SaaS (Nuevo - [!DNL Adobe Commerce as a Cloud Service])**: Adobe administra completamente la aplicación, la infraestructura y las actualizaciones principales. Los comerciantes se centran en la personalización a través de puntos de extensibilidad (API, App Builder, SDK de IU). Código de la aplicación principal bloqueado.

**Implicaciones arquitectónicas**

* **Plataforma sin versiones**: las actualizaciones continuas significan que no habrá más actualizaciones de versiones principales para el núcleo.
* **Microservicios y API-First**: mayor dependencia de las API para la extensibilidad y la integración.
* **Sin encabezado de forma predeterminada (opcional)**: Compatibilidad sólida con escaparates disociados (por ejemplo, Commerce Storefront con tecnología Edge Delivery Services).
* **Edge Delivery Services**: Impacto en el rendimiento y la implementación del front-end.

**Nuevas herramientas y conceptos**

* [Adobe Developer App Builder](https://developer.adobe.com/app-builder/) y [API Mesh para Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway)
* [Commerce Optimizer](../../optimizer/overview.md)
* [Edge Delivery Services](https://experienceleague.adobe.com/developer/commerce/storefront/?lang=es)
* Aprovisionamiento de autoservicio con [Commerce Cloud Manager](../getting-started.md#create-an-instance)

## Rutas de migración

[!DNL Adobe Commerce as a Cloud Service] admite varias rutas de migración, según la cronología, la tienda y las personalizaciones.

Como alternativa a una migración completa, [!DNL Adobe Commerce as a Cloud Service] admite una migración por fases mediante Commerce Optimizer o un método incremental.

* **Migración incremental**: este enfoque implica migrar los datos, las personalizaciones y las integraciones por fases. Este enfoque es ideal para grandes comerciantes con muchas personalizaciones que deseen realizar una transición gradual de sus personalizaciones y datos complejos a [!DNL Adobe Commerce as a Cloud Service] a su propio ritmo.

![migración incremental](../assets/incremental.png){width="600" zoomable="yes"}

* **Commerce Optimizer**: este enfoque le permite migrar de forma iterativa, utilizando Commerce Optimizer como una fase de transición para mover personalizaciones y datos complejos a [!DNL Adobe Commerce as a Cloud Service] a su propio ritmo. Commerce Optimizer proporciona acceso a los servicios de comercialización con vistas y directivas de catálogo, Commerce Storefront con tecnología Edge Delivery y [!DNL Product Visuals powered by AEM Assets].

![migración iterativa](../assets/optimizer.png){width="600" zoomable="yes"}

* **Migración completa**: este enfoque implica migrar todos los datos, las personalizaciones y las integraciones a la vez. Este enfoque es ideal para comerciantes más pequeños con pocas personalizaciones que deseen realizar una transición rápida a [!DNL Adobe Commerce as a Cloud Service].

La siguiente tabla proporciona información general del proceso de migración para diferentes tiendas y configuraciones:

|                    | Tienda de LUMA | PWA Storefront | Tienda Commerce con tecnología de Edge Delivery | Headless |
|--------------------|----------------------------------------|----------------------------------------|------------------------------------------------------|----------------------------------------|
| Migración de datos | Requerido | Requerido | Requerido | Requerido |
| Tienda | Migrar a Commerce Storefront con tecnología de Edge Delivery | Migrar a Commerce Storefront con tecnología Edge Delivery o mantener | Sin impacto | Sin impacto |
| API Mesh | Crear nueva malla | Crear nueva malla o volver a configurar la existente | Crear nueva malla o volver a configurar la existente | Crear nueva malla o volver a configurar la existente |
| Integraciones | Aproveche el kit de inicio de integración | Aproveche el kit de inicio de integración | Aproveche el kit de inicio de integración | Aproveche el kit de inicio de integración |
| Personalizaciones | Paso a App Builder y API Mesh | Paso a App Builder y API Mesh | Paso a App Builder y API Mesh | Paso a App Builder y API Mesh |
| Administración de Assets | Migración necesaria si se utiliza OOTB | Migración necesaria si se utiliza OOTB | Migración necesaria si se utiliza OOTB | Migración necesaria si se utiliza OOTB |
| Extensiones | Migrar a App Builder | Migrar a App Builder | Migrar a App Builder | Migrar a App Builder |

Como se indica en la tabla, las mitigaciones para cada migración consistirán en:

* **Migración de datos**: Se está utilizando la [herramienta de migración](./bulk-data.md) proporcionada para migrar datos de su instancia existente a [!DNL Adobe Commerce as a Cloud Service].
* **Storefront**: las tiendas Commerce existentes que cuentan con tecnología de Edge Delivery y las tiendas sin encabezado no requieren mitigación, pero las tiendas Luma requieren migrar a Commerce Storefront que cuenta con tecnología Edge Delivery. Las tiendas de PWA Studio se pueden migrar a Commerce Storefront con tecnología de Edge Delivery o se pueden mantener en su estado actual. Adobe proporcionará aceleradores para ayudar con la migración de tiendas.
* **[Mesh de API](https://developer.adobe.com/graphql-mesh-gateway)**: cree una nueva malla o modifique la existente. Adobe proporcionará mallas preconfiguradas para ayudarle con este proceso.
* **Integraciones**: todas las integraciones deben aprovechar [integration starter kit](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/) o [[!DNL Adobe Commerce as a Cloud Service] REST API](https://developer.adobe.com/commerce/webapi/reference/rest/saas/).
* **Personalizaciones**: todas las personalizaciones deben moverse a App Builder y a la malla de API.
* **Administración de Assets**: la administración de todos los recursos requiere migración. Si ya está usando [!DNL AEM Assets], no es necesario migrar.
* **Extensiones**: todas las extensiones en proceso deben volver a crearse como extensiones fuera de proceso. A finales de 2025, Adobe proporcionará acceso a nuestras extensiones más populares para minimizar los tiempos de compilación.

## Fases de migración

Las fases siguientes describen los pasos y consideraciones necesarios para migrar a [!DNL Adobe Commerce as a Cloud Service].

### Planificación y evaluación previas a la migración

Esta fase es crítica para minimizar los riesgos, establecer una ruta de migración clara e identificar los problemas antes de que surjan.

**Detección y auditoría del entorno actual**

**Análisis de la base de código:**

* Identifique todos los módulos, temáticas y invalidaciones personalizados.
* Analice las modificaciones del código principal y determine cuáles necesitarán refactorización como parte de la migración.
* Evalúe las extensiones de terceros y determine la compatibilidad con [!DNL Adobe Commerce as a Cloud Service]. ¿Existen alternativas compatibles con SaaS o necesita crear integraciones de API personalizadas o aplicaciones de App Builder?
* Identifique el código o la funcionalidad obsoletos que no se migrarán.

**Auditoría de datos:**

* Evalúe el tamaño y la complejidad de la base de datos.
* Identificar datos o tablas no utilizados para su limpieza.
* Revise los procesos de importación y exportación de datos existentes.

**Revisión de integraciones:**

* Enumere todos los sistemas externos integrados con Adobe Commerce (ERP, CRM, PIM, puertas de enlace de pago, proveedores de envío, OMS y cualquier otro sistema).
* Evalúe los métodos de integración (API, scripts personalizados y otros métodos).
* Evalúe la compatibilidad con el método API-First de [!DNL Adobe Commerce as a Cloud Service] y con App Builder.

**Análisis de rendimiento:**

* Documente las puntuaciones actuales de Lighthouse, los tiempos de carga de las páginas y los indicadores clave de rendimiento (KPI), que proporcionan una línea de base para medir las mejoras posteriores a la migración.

**Revisión de la configuración de seguridad:**

* Evalúe las reglas de WAF personalizadas, las listas de permitidos IP y cualquier otra configuración de seguridad.

**Definir ámbito y estrategia de migración:**

* **Migración por fases o de todo a la vez:** Evalúe los pros y los contras de cada enfoque.
* **Identifique los procesos empresariales principales:** Priorice las funcionalidades que deben migrarse primero, como:
   * Reglas de precios complejas
   * Reglas de negocio personalizadas aplicadas antes de que se realice o procese oficialmente un pedido
   * Cálculos de impuestos complejos
   * Validaciones de direcciones
   * Lógica personalizada activada después de realizar un pedido
* **Tienda sin encabezado o monolítica:** punto de decisión para el desarrollo de nuevas tiendas o para la adaptación de las existentes.
* **Estrategia de integración:** Determine cómo se volverán a configurar las integraciones existentes (API Mesh, App Builder, API directa).
* **Estrategia de migración de datos:** Determine si desea migrar utilizando datos históricos completos, datos parciales o ningún dato migrado.

**Preparación y entrenamiento del equipo:**

* Familiarícese con [!DNL Adobe Commerce as a Cloud Service] conceptos, flujos de trabajo de desarrollo y nuevas herramientas.
* Asista a formación práctica con Adobe App Builder, Edge Delivery Services y [!DNL Adobe Commerce as a Cloud Service] canalizaciones de implementación.

**Configuración y aprovisionamiento del entorno:**

* Aprovisionar su zona protegida [!DNL Adobe Commerce as a Cloud Service] y entornos de desarrollo con Commerce Cloud Manager.

### Fases de migración incrementales

**Refactorización y externalización estratégicas**

Esta fase consiste en el núcleo de la migración, centrándose en adaptar la base de código al paradigma nativo de la nube [!DNL Adobe Commerce as a Cloud Service]. Esto implica adoptar estratégicamente nuevos servicios de Adobe y mover la lógica personalizada fuera de la plataforma principal de Commerce.

#### &#x200B;1. Migrar personalizaciones y extensiones &quot;en proceso&quot; a App Builder

Esta es una fase crucial para lograr un &quot;núcleo bloqueado&quot; y afianzar el futuro de su solución, algo fundamental para la filosofía arquitectónica de [!DNL Adobe Commerce as a Cloud Service].

* **Externalización de la lógica compleja a App Builder**: Analice los módulos personalizados existentes y las extensiones de terceros en la base de código de PaaS. Para lógicas empresariales complejas, integraciones a medida o microservicios que no requieran manipulación directa en proceso del modelo de datos principal de Commerce, refactorícelos y vuelva a plataformas como aplicaciones sin servidor dentro de Adobe Developer App Builder.
* **Aprovechar la malla de API**: En escenarios que requieran datos de varios sistemas backend (por ejemplo, su back-end Commerce PaaS, ERP, CRM y microservicios personalizados de App Builder), implemente una capa de malla de API en App Builder. Esto consolida las API dispares en un único punto de conexión de GraphQL de rendimiento consumido por la nueva tienda u otros servicios, lo que simplifica la captura de datos complejos.
* **Arquitectura impulsada por eventos**: Use Adobe I/O Events para almacenar en déclencheur las acciones de App Builder en función de los eventos que se produzcan en su instancia de PaaS (por ejemplo, actualizaciones de productos, registros de clientes, cambios de estado de pedidos) u otros sistemas conectados. Esto promueve la comunicación asíncrona, reduce el acoplamiento estrecho y mejora la resiliencia del sistema.

**Beneficio**: Este paso reduce significativamente la deuda técnica asociada con las personalizaciones profundamente incrustadas, acelera considerablemente la transición de la instancia de Commerce a [!DNL Adobe Commerce as a Cloud Service], mejora la escalabilidad y la implementación independiente de la lógica personalizada, y promueve ciclos de desarrollo más rápidos para las extensiones.

#### &#x200B;2. Adopte servicios de comercialización de Adobe Commerce basados en SaaS e integre datos de catálogo

Este es un punto de integración inicial crítico con dos opciones con respecto a la administración de datos del catálogo:

>[!BEGINTABS]

>[!TAB Opción 1 - Servicio SaaS de catálogo existente]

**Aproveche el servicio SaaS de catálogo existente integrado con el servidor PaaS**

Esta opción sirve como paso de transición, basado en una integración existente en la que el backend de PaaS rellena una instancia existente del servicio SaaS de Adobe Commerce con datos del [servicio de catálogo](../../catalog-service/guide-overview.md), [búsqueda activa](../../live-search/overview.md) y [recomendaciones de producto](../../product-recommendations/overview.md).

* **Sincronización de datos de catálogo**: Asegúrese de que la instancia de Adobe Commerce PaaS siga sincronizando los datos de producto y catálogo con el servicio SaaS de catálogo de Adobe Commerce existente. Esto generalmente se basa en conectores o módulos establecidos dentro de la instancia de PaaS. El servicio SaaS de catálogo sigue siendo la fuente autorizada para las funciones de búsqueda y comercialización, y deriva sus datos del backend de PaaS.
* **Mesh de API para optimización**: Aunque la tienda sin encabezado (en Edge Delivery Services) y otros servicios podrían consumir directamente datos del servicio SaaS de catálogo, Adobe recomienda encarecidamente usar Mesh de API (en App Builder). La malla de API puede unificar las API del servicio SaaS de catálogo con otras API necesarias del backend de PaaS (por ejemplo, comprobaciones de inventario en tiempo real de la base de datos transaccional o atributos de producto personalizados no replicados completamente en el servicio SaaS de catálogo) en un único extremo de GraphQL con rendimiento. Esto también permite el almacenamiento en caché, la autenticación y la transformación de respuestas centralizadas.
* **Integrar Live Search y Product Recommendations**: configure los servicios SaaS de Live Search y Product Recommendations para [introducir datos de catálogo](https://experienceleague.adobe.com/es/docs/commerce/live-search/install#configure-the-data) directamente desde el servicio SaaS de catálogo de Adobe Commerce existente, que a su vez se rellena mediante el servidor PaaS.

**Beneficio**: Esto proporciona una ruta más rápida a una tienda sin encabezado y a funciones avanzadas de comercialización de SaaS al aprovechar un servicio SaaS de catálogo existente y operativo y su canalización de integración con su servidor PaaS. Sin embargo, conserva la dependencia del backend de PaaS para la fuente de datos del catálogo principal y no proporciona las capacidades de agregación de varias fuentes inherentes al nuevo modelo de datos de catálogo componible. Esta opción es un trampolín válido hacia una arquitectura componible más completa.

>[!TAB Opción 2 - Modelo de datos de catálogo maquetable]

**Adoptar el nuevo Modelo de datos de catálogo compuesto (CCDM)**

Este es el enfoque estratégico, preparado para el futuro, para aprovechar Adobe Commerce Optimizer. CCDM proporciona un servicio de catálogo flexible, escalable y unificado diseñado para la agregación de datos de varias fuentes y la comercialización dinámica.

* **Ingesta y unificación de datos**
   * Comience por ingerir datos de producto y catálogo de la instancia de Adobe Commerce PaaS existente (y/u otros sistemas PIM/ERP) en el nuevo Modelo de datos de catálogo componible (CCDM).
   * Asigne atributos de producto existentes al esquema flexible del CCDM. Priorice los datos críticos del producto para la ingesta inicial.
   * Establezca canalizaciones de datos sólidas para una sincronización continua. Esto puede implicar:
      * **Impulsado por eventos** (a través de App Builder): Utilice Adobe I/O Events desde su instancia de PaaS para almacenar en déclencheur aplicaciones de Adobe App Builder personalizadas o disponibles públicamente. Estas aplicaciones transforman e insertan cambios en los datos (crean, actualizan y eliminan) en el CCDM a través de sus API.
      * **Ingesta por lotes**: Para cargas iniciales grandes o actualizaciones masivas periódicas, utilice transferencias de archivos seguras (por ejemplo, CSV o JSON) a un área de ensayo, procesadas por los servicios de ingesta de Adobe Experience Platform (AEP) en CCDM.
      * **Integración directa de API** (con orquestación de App Builder): para escenarios más complejos, App Builder puede actuar como una capa de orquestación, haciendo llamadas directas de API al servidor PaaS, transformando los datos y enviándolos a CCDM.
* **Vista de catálogo y definición de directiva**: configure vistas de catálogo (agrupaciones lógicas para la presentación de catálogo único, como vistas de tienda, regiones y segmentos B2B/B2C) y defina directivas (conjuntos de reglas para la presentación, el filtrado y la comercialización de productos) dentro de CCDM. Esto permite un control dinámico sobre la variedad de productos y la lógica de visualización por vista de catálogo.
* **Integrar Live Search y Product Recommendations**: Una vez que los datos del catálogo estén presentes en CCDM, integre Live Search y los servicios de Adobe basados en SaaS. Estos aprovechan la IA de Adobe Sensei y los modelos de aprendizaje automático para ofrecer una relevancia de búsqueda superior y recomendaciones personalizadas, consumiendo datos directamente del CCDM.

**Beneficio**: Al abstraer la administración y la detección de catálogos en los servicios CCDM y SaaS asociados, se logra un rendimiento mejorado, se obtienen capacidades de comercialización impulsadas por IA, se descargan significativamente las operaciones de lectura de su back-end heredado y se habilita una sólida experiencia de &quot;despegue&quot; de la parte superior de funnel.

>[!ENDTABS]

#### &#x200B;3. Crea tu tienda en Edge Delivery Services

Con las canalizaciones de datos de comercialización establecidas y las personalizaciones externalizadas, el enfoque cambia a la creación de su front-end de alto rendimiento.

* **Configuración inicial**: configure el proyecto con la plantilla de Adobe Commerce Storefront para Edge Delivery Services. Esto proporciona un front-end sin encabezado fundacional creado en tecnologías web modernas.
* **Conéctese a los servicios de catálogo y a la malla de API**: Su tienda de Commerce consumirá datos principalmente a través de las API de GraphQL:
   * **Opción 1**: desde el servicio existente de SaaS de catálogo (a través de API Mesh) para obtener información de productos y reglas de comercialización.
   * **Opción 2**: de CCDM para obtener información de productos y reglas de comercialización.
   * Desde API Mesh para cualquier dato orquestado desde su backend heredado (instancia PaaS) o servicios personalizados de App Builder (por ejemplo, se muestran el inventario en tiempo real, los atributos de producto personalizados y los puntos de lealtad).
* **Migración de contenido (servicios de AEM)**: Migre el contenido estático existente (por ejemplo, páginas &quot;Acerca de nosotros&quot;, publicaciones de blog y banners de marketing) a los servicios de AEM, que alimentan la Tienda Commerce. Aproveche las funcionalidades de creación de contenido de AEM y asegúrese de que los recursos estén optimizados para Edge Delivery Services.
* **Desarrollar componentes principales de la interfaz de usuario**: Cree componentes críticos de la interfaz de usuario para páginas de detalles de productos (PDP), páginas de listas de productos (PLP) y páginas de contenido general usando componentes desplegables de Edge Delivery Services y componentes React/Vue personalizados. Priorizar los flujos de comercio principales.
* **Integración con el carro de compras/cierre de compra existente**: inicialmente, la tienda de Edge Delivery Services organizará un envío a las PaaS de Adobe Commerce existentes (u otra plataforma de terceros) para la administración y el cierre de compra del carro de compras. Esto suele implicar:
   * **Redirección**: redireccionando al usuario al carro de compras nativo de la plataforma heredada y a las direcciones URL de cierre de compra, pasando los identificadores de sesión y carro de compras necesarios.
   * **Interacción directa con la API** (con la orquestación de App Builder): al crear componentes personalizados de la interfaz de usuario del carro de compras y del cierre de compra en Edge Delivery Services que interactúan directamente con las API del carro de compras y del cierre de compra de PaaS. Esto a menudo implica a App Builder como servidor para front-end (BFF) para orquestar llamadas a varios servicios back-end (por ejemplo, carro de compras PaaS, puertas de enlace de pago y calculadoras de envío).

**Beneficio**: ofrece una experiencia de tienda increíblemente rápida, optimizada para SEO y altamente flexible. Esta fase contribuye directamente a una experiencia del cliente superior y sienta las bases para la futura innovación de front-end.

#### &#x200B;4. Migración de datos (proceso por fases)

La migración de datos es un proceso crítico y multifacético que se ejecuta simultáneamente con la refactorización y el desarrollo de tiendas, lo que garantiza la coherencia y la integridad de los datos.

* **Limpie y optimice los datos existentes**: antes de cualquier migración a gran escala, realice una limpieza, deduplicación y validación de datos completa en su base de datos PaaS existente. Este paso proactivo es crucial para minimizar la transferencia de problemas de datos heredados y garantizar la calidad de los datos en el nuevo entorno.

**Migraciones de datos en lotes**

La migración masiva de datos implica tomar un volcado de datos completo de la instancia de Adobe Commerce PaaS, transformar todo ese conjunto de datos e importarlo a Adobe Commerce as a Cloud Service de una sola vez. Este método se utiliza generalmente para la población inicial de datos.

* **Disponibilidad de herramientas**: Las [herramientas de migración de datos en lote](./bulk-data.md) dedicadas al uso de los clientes para las migraciones de datos en lote de Commerce estarán disponibles por solicitud a mediados de julio de 2025. Si los clientes necesitan asistencia con la migración masiva de datos con antelación, Adobe puede facilitar la transferencia de datos en su nombre mediante solicitud.

* **Proceso**:
   * **Exportación de datos completa**: extraiga un conjunto de datos completo de su instancia de Adobe Commerce PaaS (por ejemplo, productos, categorías, cuentas de cliente, datos de pedidos históricos, bloques estáticos y contenido de página).
   * **Transformación de datos**: aplique las transformaciones necesarias para alinear los datos extraídos con los requisitos de esquema de los nuevos componentes de Adobe Commerce as a Cloud Service, incluido el Modelo de datos de catálogo componible (CCDM) si se adopta, y cualquier otro servicio o base de datos de Adobe relevante. Esto puede implicar secuencias de comandos personalizadas o herramientas especializadas de asignación de datos.
   * **Importación inicial**: importe el conjunto de datos completo transformado en los componentes respectivos de Adobe Commerce as a Cloud Service. Para los datos de producto y categoría, se rellena el servicio de catálogo seleccionado (CCDM o SaaS de catálogo existentes). Para los datos de clientes y pedidos, esto rellena el backend transaccional o los servicios asociados.
   * **Validación**: valide rigurosamente los datos importados para garantizar integridad, precisión y coherencia en todos los sistemas nuevos.

**Migraciones de datos iterativas**

Las migraciones de datos iterativas se centran en la sincronización de cambios incrementales y deltas de la instancia de PaaS de origen a los nuevos componentes de Cloud Service, lo que garantiza la actualización de los datos hasta y después del cambio.

* **Disponibilidad de herramientas**: Las herramientas diseñadas específicamente para migraciones de datos iterativas estarán disponibles en el segundo semestre de 2025.

* **Proceso**:
   * **Identificación Delta**: establezca mecanismos para identificar cambios (creaciones, actualizaciones y eliminaciones) en conjuntos de datos críticos en su entorno PaaS desde la última sincronización. Esto puede implicar la captura de datos de cambios (CDC), comparaciones de marcas de tiempo o déclencheur basados en eventos.
   * **Sincronización continua**: Implemente mecanismos sólidos para una sincronización de datos continua e incremental desde su entorno PaaS a los nuevos componentes de Cloud Service (por ejemplo, CCDM y back-end transaccional). Esto es crucial para mantener la actualización de los datos y minimizar el tiempo de inactividad durante la migración.
   * **Aprovechamiento de eventos**: Utilice Adobe I/O Events siempre que sea posible para almacenar en déclencheur las acciones de App Builder para obtener actualizaciones en tiempo real o casi en tiempo real desde su instancia de PaaS a los nuevos servicios. Por ejemplo, una actualización de producto en PaaS podría almacenar en déclencheur un evento que actualice la entrada correspondiente en CCDM.
   * **Actualizaciones controladas por API**: Para los datos que no están impulsados por eventos, utilice llamadas de API programadas (a través de App Builder u otras plataformas de integración) para extraer cambios de PaaS e insertarlos en los nuevos sistemas.
   * **Control y supervisión de errores**: Implemente funciones sólidas de control, registro y supervisión de errores para todas las canalizaciones de datos iterativas a fin de garantizar que se mantenga la integridad de los datos durante todo el proceso.

### Operaciones posteriores a la migración y en curso

**Cambio de DNS y lanzamiento:**

* Planifique cuidadosamente la migración de DNS con un tiempo de inactividad mínimo.
* Monitorice el estado y el rendimiento del sitio inmediatamente después del lanzamiento.

**Operaciones posteriores al inicio:**

**Retirada del entorno de PaaS:**

* Archive o elimine de forma segura las instancias y los datos de PaaS antiguos después del periodo de validación.

**Flujo de trabajo de desarrollo en curso:**

* Acepte la naturaleza sin versiones de [!DNL Adobe Commerce as a Cloud Service], que tiene implementaciones pequeñas continuas en lugar de actualizaciones grandes.
* Utilice Cloud Manager para administrar entornos e implementaciones.
* Aproveche App Builder para ampliar la funcionalidad sin afectar al núcleo.

**Supervisión, rendimiento y seguridad:**

* Supervise continuamente el rendimiento del sitio, los errores y los registros de seguridad.
* Utilice las funciones de seguridad integradas de Adobe y siga las prácticas recomendadas.

**Formación y documentación:**

* Capacite a nuevos desarrolladores y usuarios empresariales en la plataforma y los flujos de trabajo de [!DNL Adobe Commerce as a Cloud Service].
* Mantenga actualizada la documentación interna para integraciones y procesos personalizados.
