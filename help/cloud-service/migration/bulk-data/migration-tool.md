---
title: Herramienta de migración masiva de datos
description: Aprenda a utilizar la herramienta de migración masiva de datos para migrar datos de su instancia de Adobe Commerce en la nube existente a  [!DNL Adobe Commerce as a Cloud Service].
feature: Cloud
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
role: Developer
level: Intermediate
exl-id: 81522de9-df54-4651-b8ed-58956376af86
autotag-review: '2026-07-22T19:18:39.433Z'
TQID: 'https://experienceleague.adobe.com/tkCFabZpBKu-W34wsufHlVIWzCUE8FKm4kK7qZahxBU'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
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
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 4c0eca0039bab7d015144dd9ac3885a0b2be0563
workflow-type: tm+mt
source-wordcount: 924
ht-degree: 0%

---

# Herramienta de migración masiva de datos

>[!IMPORTANT]
>
>La herramienta de migración masiva de datos se encuentra actualmente en Acceso anticipado. El acceso se proporciona exclusivamente a través del proceso de participación de ingeniería implementada de Commerce (CDE).

La herramienta de migración masiva de datos permite a los integradores de sistemas migrar datos de comercio principal de origen de [!DNL Adobe Commerce on Cloud] o instalaciones locales a [!DNL Adobe Commerce as a Cloud Service].

La herramienta de migración masiva de datos es una CLI basada en Docker que los integradores de sistemas ejecutan en su propia máquina de migración. Se conecta a la instancia de origen, extrae los datos principales de comercio de origen, los carga en el servicio de migración de Adobe (servicio de migración de datos de Commerce) y supervisa el progreso hasta la finalización.

Todos los comandos se ejecutan localmente, por lo que se controla cuándo se inicia la migración, cuándo se aplica el modo de mantenimiento y cuándo se ejecuta cada fase.

## Flujo de trabajo migración

La herramienta gestiona las siguientes fases de principio a fin:

- **Extracción de datos**: extrae datos de comercio principal de origen de la instancia de origen ([!DNL Adobe Commerce on Cloud] o local).
- **Carga de datos**: carga datos extraídos en la instancia de destino [!DNL Adobe Commerce as a Cloud Service].
- **Verificación de integridad de datos**: realiza comprobaciones automatizadas posteriores a la migración, incluidas la comparación de las API de REST y GraphQL y la validación del recuento de registros.

>[!NOTE]
>
>Actualmente, la herramienta de migración masiva de datos solo admite la migración de datos de comercio principales de origen. Actualmente no se admite la migración de datos personalizados. Los ajustes de configuración (ajustes de almacenamiento y del sistema) no se migran automáticamente y deben configurarse en la instancia de destino de forma independiente antes de la migración.

## Arquitectura

La herramienta de migración masiva de datos sigue una arquitectura distribuida que permite una migración de datos segura y eficaz. Esta herramienta ayuda a los integradores de sistemas a migrar datos de un [!DNL Adobe Commerce on Cloud or on-premises instance] existente a [!DNL Adobe Commerce as a Cloud Service]. Para obtener más información sobre el proceso de migración, consulte la [descripción general de la migración](../overview.md).

La siguiente imagen detalla la arquitectura y el flujo de datos de extremo a extremo mediante la herramienta de migración masiva de datos.

![Diagrama de arquitectura de la herramienta de migración masiva de datos que muestra el flujo de datos de PaaS a SaaS](../../assets/bulk-data-diagram.png){zoomable="yes"}

### Componentes

| Componente | Rol |
| --------- | ---- |
| **Herramienta de migración masiva de datos** | CLI basada en Docker que el integrador de sistemas ejecuta en el equipo de migración, que organiza la canalización completa leyendo el esquema y los datos del origen, cargando los datos extraídos en el servicio de migración de Adobe e impulsando las transiciones de estado. |
| **Instancia de Source (Commerce en la nube o local)** | El origen de la migración. La herramienta se conecta a través de las API de REST y GraphQL y a través de un túnel SSH ([!DNL Adobe Commerce on Cloud]) o a través de una conexión directa a la base de datos (local) para la extracción de datos. |
| **API del servicio de migración de datos de Commerce (CDMS)** | La API de REST administrada por Adobe registra las migraciones, coordina las transiciones de estado y proporciona puntos finales seguros para cargar los datos extraídos. La herramienta de migración se conecta a esta API mediante la dirección URL del extremo CDMS y las credenciales de IMS en la configuración de `.env`. |
| **Trabajador del servicio de migración de datos de Commerce (CDMS)** | Servicio en segundo plano administrado por Adobe que carga los datos extraídos en la instancia de destino y ejecuta la verificación de integridad posterior a la carga. |
| **[!DNL Adobe Commerce as a Cloud Service]** | La versión basada en SaaS de Adobe Commerce y su objetivo de migración. Recibe los datos cargados y expone los servicios de catálogo, Live Search y reglas de asignación de precios utilizados durante la verificación de la integridad. |

### Flujo de datos

Los datos se mueven por los componentes en la siguiente secuencia:

1. La herramienta de migración masiva de datos lee el esquema y los datos de la base de datos desde la instancia de origen, a través de un túnel SSH para [!DNL Adobe Commerce on Cloud] o una conexión directa a la base de datos para la instalación local.
1. La herramienta registra la migración y carga los datos extraídos mediante la API de CDMS.
1. El trabajador de CDMS carga los datos en el inquilino de destino [!DNL Adobe Commerce as a Cloud Service].
1. [!DNL Adobe Commerce as a Cloud Service] ingiere los datos de catálogo cargados y genera el índice de catálogo.
1. El trabajador del Servicio de migración de datos de Commerce (CDMS) verifica los datos cargados mediante la comparación de suma de comprobación de la base de datos, REST y GraphQL en los siguientes servicios:

   - **Catálogo** (GraphQL): datos de producto y categoría.
   - **Live Search** (REST): la corrección del índice de búsqueda.
   - **Reglas de precios** (REST): datos de precios y reglas.

1. La herramienta sondea el estado de la migración en todo y recupera el informe final de migración una vez finalizado.


## Ciclo de participación

El acceso a la herramienta de migración masiva de datos se proporciona exclusivamente a través de una participación de ingeniería implementada de Commerce (CDE). La herramienta no es de acceso público.

El ciclo de vida típico de la participación es:

1. **Descubrimiento de CDE**: complete la llamada de ámbito inicial, evalúe el tamaño y la complejidad de los datos y complete el cuestionario de ámbito.
1. **Firma del acuerdo**: el acuerdo comercial está en vigor y el ámbito de la migración se ha confirmado. En este momento, se le concede acceso a la herramienta de migración.
1. **Co-innovación y soporte de CDE**: colabore con Adobe para instalar la herramienta en su entorno y ejecutar migraciones de prueba.
1. **Activar**: ejecute la migración total de producción y complete la verificación de integridad de datos.

## Distribución de herramientas

La herramienta se distribuye como parte de la participación del CDE. El representante de Adobe proporciona el paquete de herramientas, que incluye:

- La CLI basada en Docker y la configuración de compilación
- Una plantilla de configuración `.example.env` con documentación para todas las variables de entorno requeridas
- Documentación técnica completa que cubre la arquitectura de la herramienta, la referencia de configuración, los marcos de prueba y transformación personalizados y las guías de solución de problemas

Para obtener instrucciones detalladas de configuración y funcionamiento, consulte la documentación incluida en el paquete de distribución de herramientas.

## Guías de migración

Las siguientes páginas muestran el ciclo de vida completo de la migración, desde la preparación hasta la ejecución. Para una comprensión completa del proceso de migración, revíselos en el siguiente orden:

1. [Lista de comprobación de preparación para clientes](readiness-checklist.md): confirme los requisitos previos de participación, máquina de migración, origen y destino antes de solicitar acceso a la herramienta.
1. [Verificar el acceso al servicio de migración](cdms-access.md): después de obtener acceso a la herramienta, valide la accesibilidad de la red, la autenticación IMS y la autorización del inquilino con la API del servicio de migración de datos (CDMS) de Commerce.
1. [Ejecutar una migración masiva de datos](migration-guide.md): configure la herramienta, prepare la red y las instancias e inicie la migración.

Para obtener la referencia de configuración completa, los marcos de trabajo de prueba y transformación personalizados y las directrices para la resolución de problemas, consulte la documentación incluida en el paquete de distribución de herramientas.
