---
title: Herramienta de migración masiva de datos
description: Aprenda a utilizar la herramienta de migración masiva de datos para migrar datos de su instancia [!DNL Adobe Commerce as a Cloud Service] de Adobe Systems Commerce on Cloud existente.
feature: Cloud
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Se aplica a Adobe Systems Commerce como Cloud Service y solo a Adobe Systems proyectos de Commerce Optimizer (infraestructura SaaS administradas por Adobe Systems)."
role: Developer
level: Intermediate
exl-id: 81522de9-df54-4651-b8ed-58956376af86
source-git-commit: e582ce85b58b57922a8cdd63dbe32bd0f08c64f9
workflow-type: tm+mt
source-wordcount: '706'
ht-degree: 0%

---

# Migración masiva de datos herramienta

El herramienta de migración masiva de datos sigue una arquitectura distribuida que permite una migración de datos segura y eficiente de PaaS a entornos SaaS. Este herramienta ayuda a los implementadores de soluciones a migrar datos de una instancia de Adobe Systems Commerce on Cloud (PaaS) existente a [!DNL Adobe Commerce as a Cloud Service] (SaaS). Para obtener más información sobre el proceso de migración, consulte Información general[ sobre migración](./overview.md).

>[!NOTE]
>
>La herramienta de migración masiva de datos solo admite la migración de datos de comercio principales propios. Actualmente no se admite la migración de datos personalizados.

La siguiente imagen detalla la arquitectura y los componentes clave para utilizar el herramienta de migración masiva de datos.

![Diagrama de arquitectura de la herramienta de migración masiva de datos que muestra el flujo de datos de PaaS a SaaS](../assets/bulk-data-diagram.png){zoomable="yes"}

## flujo de trabajo de migración

El flujo de trabajo de migración masiva de datos consta de los siguientes pasos:

1. Configure un nuevo entorno para la migración.
1. Copie sus datos de su sistema anterior.
1. Mueva sus datos al nuevo sistema.
1. Haga que su catálogo de productos esté disponible en el nuevo sistema.
1. Confirme que los datos se han migrado correctamente.

Las siguientes secciones describen estos pasos en detalle.

## Acceda al herramienta de migración masiva de datos

La disponibilidad del herramienta de migración masiva de datos es la siguiente:

- **Q1 2026** (aún no disponible): después de la publicación inicial del herramienta de migración masiva de datos, podrá acceder a él enviando un ticket de soporte.
- **Q1 2026** (aún no disponible) - Después de la publicación del herramienta de migración masiva de datos, será accesible desde este Página.

## Crear destino entorno

El implementador de soluciones (SI) crea un entorno destino para la migración. Este entorno almacena los datos migrados desde el instancia de origen.

Primero, [cree un nuevo [!DNL Adobe Commerce as a Cloud Service]  instancia](../getting-started.md#create-an-instance) (SaaS).

### Configurar extracción herramienta

Utilice el herramienta extracción para extracción datos desde el instancia de origen.

1. Descargue los herramienta de extracción de los vincular que Adobe Systems proporcionó.
1. Configure las siguientes variables de entorno en la herramienta extracción:
   - Detalles de conexión a la base de datos MySQL existente
   - ID de inquilino destino para su [!DNL Adobe Commerce as a Cloud Service] instancia
   - Sus credenciales de IMS, incluyendo:
      - ID del cliente
      - Secreto del cliente
      - Ámbitos IMS
      - IMS URL: la URL base. Por ejemplo, `https://ims-na1.adobelogin.com/`.
      - ID de organización de IMS

   Para ámbitos IMS y otros valores, seleccione su tipo de OAuth en la **sección Credentials (Credenciales** ) del proyecto, en Adobe Systems [Developer Console](https://developer.adobe.com/console/). Se proporciona más información en el `.example.env` archivo incluido con el herramienta de extracción.

### Extract datos

Antes de ejecutar el herramienta extracción, el implementador de la solución debe establecer un túnel SSH a la base de datos PaaS mediante:

```bash
magento-cloud tunnel:open
```

A continuación, ejecute el herramienta extracción, que será:

1. Conéctese a la base de datos PaaS, analice su esquema y compárela con el inquilino SaaS esquema detalles.
1. Genere un plan extracción y transformación basado en los elementos de esquema comunes entre PaaS y SaaS.
1. Extract los datos mediante el servicio de administración de datos de catálogo (CDMS).

### Cargar datos

Ejecute los herramienta de datos de carga proporcionados por Adobe Systems. Esta herramienta:

1. Conéctese a la base de datos de inquilinos SaaS mediante un cuenta de migración.
1. Genere un plan de carga.
1. Ejecute el plan, moviendo datos a la base de datos de inquilinos SaaS en lotes.
1. Procesar el medios del catálogo y transferirlo a la entorno destino.
1. Limpie la caché de Redis SaaS e invalide los índices de la base de datos para el inquilino.

### Consumo de datos de catálogo

Una vez cargados los datos, los datos de catálogo fluyen automáticamente desde la base de datos de inquilinos SaaS al servicio de catálogo.

El servicio de catálogo comparte estos datos con Search activos y Recommendations de productos. No se requiere ninguna intervención manual para este proceso. Los datos están disponibles en todos los servicios una vez finalizada la ingesta.

### Verificación de la integridad de los datos

Después de la migración, CDMS realiza las siguientes comprobaciones automáticas de integridad de datos para garantizar la precisión e integridad de los datos migrados:

**Verificación basada en API**

Durante la verificación, CDMS compara las respuestas de la API REST y GraphQL de consultas ejecutadas previamente con los registros correspondientes del instancia destino. Las discrepancias se pueden ver en el estado de la migración.

**Verificación a nivel de base de datos**

Durante la verificación, CDMS cuenta el número de registros extraídos y compara ese número con la cantidad de registros cargados.

**Verificación bajo demanda (opcional)**

También puede activar manualmente la verificación exhaustiva de todos los registros del sistema:

>[!NOTE]
>
>Este proceso requiere muchos recursos y solo debe usarse en entornos simulados para pruebas.

La verificación completa incluye:

- Todas las aplicaciones verificación basada en API utilizando todas las respuestas de API REST y GraphQL previamente extraídas
- Informe detallado de cualquier inconsistencia encontrada
