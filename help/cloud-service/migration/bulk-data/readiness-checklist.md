---
title: Lista de comprobación de preparación del cliente
description: Obtenga información sobre cómo prepararse para una migración de datos masiva a Adobe Commerce as a Cloud Service con una lista de comprobación de preparación que incluya la participación, la máquina, el origen y el destinatario.
feature: Cloud
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
role: Developer
level: Intermediate
autotag-review: '2026-07-22T19:19:18.443Z'
TQID: 'https://experienceleague.adobe.com/728hkK-dzIPzyuBhuNyOqEE9FxlVGdVc9R2wIRcXobk'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
  - id: c32adafa-ed01-4b31-997e-2413013911b0
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
  - id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75
  - id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
subfeature_v2:
  - id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2:
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 670b6214b28be93a16130552a226a8cadb487324
workflow-type: tm+mt
source-wordcount: 1171
ht-degree: 0%

---

# Lista de comprobación de preparación del cliente

{{bulk-data-early-access}}

Utilice esta lista de comprobación para prepararse para la migración de datos de una instancia de [!DNL Adobe Commerce on Cloud] o local a [!DNL Adobe Commerce as a Cloud Service] mediante la herramienta de migración de datos en masa.

La herramienta de migración se distribuye como parte del proceso de participación de ingeniería implementada de Commerce (CDE). El acceso a la herramienta está garantizado por un acuerdo de CDE firmado y no está disponible públicamente.

Esta lista de comprobación cubre lo que necesita disponer antes de compartir la herramienta ([Fase 1](#stage-1-before-tool-access)) y lo que necesita para comenzar la configuración y ejecución una vez que tenga la herramienta ([Fase 2](#stage-2-before-running-the-migration)). Revise esta lista de comprobación con su equipo de Adobe antes de tiempo, ya que algunos elementos requieren la coordinación de Adobe.

## Fase 1: antes del acceso a la herramienta

Complete o confirme lo siguiente antes de proporcionar la herramienta de migración y la documentación.

- **Participación de CDE**: debe haber un acuerdo de ingeniería implementada de Commerce firmado. El acceso a las herramientas se concede en la fase de firma del acuerdo del ciclo vital de CDE. Coordine con su equipo de Adobe.
- **Cuestionario de ámbito completado**: se completa un cuestionario de ámbito durante la detección de CDE para validar que la migración es factible con las capacidades actuales de la herramienta y para evaluar la huella y la complejidad de los datos. Asegúrese de que su equipo de Adobe lo haya completado antes de continuar.
- **No se han confirmado datos de HIPAA**: la instancia de origen no debe contener datos regulados por HIPAA. Confirme esto antes de continuar.
- **Direcciones IP proporcionadas**: proporcione a su equipo de Adobe la lista de direcciones IP estáticas desde las que se ejecutará la herramienta de migración. Esto es necesario para configurar el acceso a la red en el lado de Adobe.
- **Instancia de destino aprovisionada** — La instancia de destino [!DNL Adobe Commerce as a Cloud Service] debe aprovisionarse antes de que comience la migración. Póngase en contacto con el equipo de Adobe para confirmar que la instancia está lista.

## Fase 2: antes de ejecutar la migración

Una vez que tenga acceso a la herramienta, prepare los siguientes elementos antes de comenzar la configuración y ejecución.

### Equipo de migración

La herramienta de migración se ejecuta en una máquina que controla, como un cuadro de salto dedicado. Este equipo debe cumplir los siguientes requisitos.

- **[!DNL Docker]y [!DNL Docker Compose] instalaron** — La herramienta está basada en [!DNL Docker]. Tanto `docker` como `docker compose` (o el elemento heredado `docker-compose`) deben estar instalados y en funcionamiento en el equipo de migración.
- **[!DNL Docker]permisos de ejecución** — Se debe permitir al usuario que ejecuta la migración ejecutar [!DNL Docker] comandos. El [!DNL Linux], el usuario debe estar en el grupo `docker`. En [!DNL macOS] y [!DNL Windows], [!DNL Docker Desktop] debe estar en ejecución y ser accesible.
- **Directorio de trabajo grabable**: el usuario de migración debe poder escribir completamente en el directorio donde se extrae la herramienta de migración. La herramienta escribe registros, caché, dependencias [!DNL Composer] y archivos generados durante la ejecución.
- **Espacio en disco suficiente**: garantice espacio en disco suficiente para los datos extraídos, las imágenes de [!DNL Docker] y la salida de registro. Los requisitos de espacio varían según el tamaño de la base de datos de origen.
- **Orígenes locales: conectividad directa de la base de datos desde la máquina de migración**: para las instancias de origen locales, la máquina de migración debe tener acceso directo de red a la base de datos de origen. La herramienta no establece automáticamente la conectividad de la base de datos local. Antes de ejecutar cualquier comando de migración, confirme que el host, el puerto y las credenciales están accesibles desde el equipo de migración.
- **CLI de nube instalada y clave SSH registrada**: para [!DNL Adobe Commerce on Cloud] instancias de origen, [CLI de nube](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/dev-tools/cloud-cli/cloud-cli-overview) debe estar instalado en el equipo de migración. Su clave pública SSH también debe estar registrada en su cuenta. Consulte la [Guía de conexiones seguras](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/secure-connections) para obtener instrucciones.

### Instancia de Source

- **Se puede acceder a las API de la tienda Source** — Las API de REST y GraphQL de la tienda de origen deben ser accesibles desde el equipo de migración. Asegúrese de que ninguna restricción de red o autenticación HTTP Basic bloquee el tráfico de API a la dirección URL de origen.
- **Credenciales de OAuth de Source**: la herramienta de migración utiliza OAuth para autenticarse en el almacén de origen. Cree o confirme una integración en el origen [!UICONTROL **Admin**] ([!UICONTROL **System**] > [!UICONTROL **Extensions**] > [!UICONTROL Integrations]) y prepare la clave de consumidor, el secreto de consumidor, el token de acceso y el secreto del token de acceso.
- **Fuentes de PaaS: token de API de Magento Cloud**. Genere un token de API [!DNL Cloud] a partir de la [configuración de la cuenta en la nube](https://accounts.magento.cloud) en [!UICONTROL **Configuración de la cuenta**] > [!UICONTROL **Tokens de API**]. Solo es necesario cuando el origen es una instancia de [!DNL Adobe Commerce on Cloud].
- **Credenciales de base de datos de Source** — (Solo local) Tenga preparados los detalles de conexión de base de datos de origen [!DNL MySQL] para la configuración: nombre `host`, `port`, `user`, `password` y `database`.
- **Capacidad de pausar cron**: debe poder detener cron en la instancia de origen durante la extracción de datos para evitar escrituras simultáneas.
- **Capacidad para pausar integraciones y trabajos en segundo plano**: cualquier integración de terceros (ERP, OMS, PIM), trabajos programados o procesos en segundo plano que escriban en la base de datos de origen debe estar en pausa para la ventana de extracción.
- **Capacidad para habilitar y deshabilitar el modo de mantenimiento** — (Solo migración por fases) Si ejecuta una migración por fases con una ventana de mantenimiento, debe poder habilitar y deshabilitar el modo de mantenimiento en la instancia de origen.

### Instancia de destino

- **ID de inquilino e ID de organización confirmados**: obtenga sus `TARGET_TENANT_ID` y `TARGET_ORG_ID` de su equipo de Adobe antes de configurarlos.
- **Credenciales de servidor a servidor OAuth de IMS**: necesarias para que la herramienta de migración se autentique con el destino. Generado mediante [Adobe Developer Console](https://developer.adobe.com/console/). Necesita acceso de [!UICONTROL Developer] o [!UICONTROL Admin] a su organización de Adobe, ya que el acceso básico de usuario no es suficiente para crear credenciales. Coordine con su equipo de Adobe el perfil de producto correcto que desea seleccionar y prepare el ID de cliente (`ADOBE_IMS_CLIENT_ID`) y el secreto de cliente (`ADOBE_IMS_CLIENT_SECRET`).
- **Dirección URL del extremo CDMS** proporcionada por su equipo de Adobe. No intente deducir este valor. Necesita el punto final de preproducción para migraciones de zona protegida y de prueba y el punto final de producción para migraciones de migración total activas.
- **Configuración principal alineada entre el origen y el destino**: la herramienta no migra los datos de configuración principal, como la configuración del almacén y del sistema. Configúrela manualmente en el destino para que coincida con el origen antes de la migración.
- **Almacenes B2B: características B2B configuradas de forma coherente** — Si el origen es un almacén habilitado para B2B, asegúrese de que la configuración de B2B [!UICONTROL Admin] relevante esté configurada de forma coherente en el origen y el destino antes de la migración. Consulte la [guía de migración](migration-guide.md) para conocer la configuración específica requerida.

### Planificación de migración

- **Enfoque de migración decidido** — Determine qué enfoque se ajusta a su caso de uso antes de comenzar.
  - Migración monofásica: no se requiere modo de mantenimiento. Se adapta a ejecuciones en seco, entornos de desarrollo o de zona protegida, o a cualquier migración en la que el origen pueda permanecer activo durante la extracción.
  - Migración multifase: se requiere el modo de mantenimiento. Se requiere una migración multifase para las migraciones de producción en las que la fuente debe bloquearse durante la extracción para garantizar la coherencia de los datos.
- **Ventana de mantenimiento planificada** — Se aplica solo a las migraciones multifase. Planifique y comunique la ventana de mantenimiento con antelación. La instancia de origen no está disponible para los usuarios finales durante las fases de extracción y carga.
- **Código de vista de tienda confirmado** — Identifique el código de vista de tienda (`STORE_CODE`) en la instancia de origen. Su valor predeterminado es `default`, pero debe coincidir con el código real de [!UICONTROL Admin] > [!UICONTROL Stores] > [!UICONTROL All Stores]. Un código de almacén incorrecto puede afectar a las operaciones de datos durante la migración.

Después de confirmar todos los elementos, está listo para comprobar el acceso al servicio con la [guía de acceso al servicio de migración](cdms-access.md) y, a continuación, comenzar los pasos de configuración y ejecución en la [guía de migración](migration-guide.md).
