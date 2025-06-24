---
title: Herramienta de migración masiva de datos
description: Aprenda a utilizar la herramienta de migración masiva de datos para migrar datos de su instancia de Adobe Commerce en la nube existente a  [!DNL Adobe Commerce as a Cloud Service].
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
role: Architect
source-git-commit: bc8011189a46ccab986b22020881c808da6ee2cd
workflow-type: tm+mt
source-wordcount: '690'
ht-degree: 0%

---


# Herramienta de migración masiva de datos

La herramienta de migración masiva de datos sigue una arquitectura distribuida que permite una migración de datos segura y eficaz de los entornos PaaS a SaaS. Esta herramienta está diseñada para que los implementadores de soluciones migren datos de una Adobe Commerce en la nube (PaaS) existente a [!DNL Adobe Commerce as a Cloud Service] (SaaS). Para obtener más información sobre el proceso de migración, consulte la [descripción general de la migración](./overview.md).

>[!NOTE]
>
>La herramienta de migración masiva de datos solo admite la migración de datos de comercio principal de origen. Actualmente no se admite la migración de datos personalizados.

La siguiente imagen detalla la arquitectura y los componentes clave para utilizar la herramienta de migración masiva de datos.

![Arquitectura de la herramienta de migración masiva de datos](../assets/bulk-data-diagram.png)

## Flujo de trabajo migración

El flujo de trabajo de migración masiva de datos consta de los siguientes pasos:

1. Configure un nuevo entorno para la migración.
1. Copie los datos del sistema antiguo.
1. Mueva los datos al nuevo sistema.
1. Haga que el catálogo de productos esté disponible en el nuevo sistema.
1. Confirme que los datos se han migrado correctamente.

Las secciones siguientes describen estos pasos en detalle.

## Acceso a la herramienta de migración masiva de datos

La disponibilidad de la herramienta de migración masiva de datos es la siguiente:

- **Mediados de julio de 2025**: para acceder a la herramienta de migración masiva de datos, envíe un ticket de asistencia.
- **Mediados de agosto de 2025**: la herramienta de migración masiva de datos estará disponible para el público y se podrá acceder a ella desde esta página.

## Crear entorno de destino

El implementador de soluciones (SI) crea un entorno de destino para la migración. Este entorno se utiliza para almacenar los datos que se migran de la instancia de origen.

Primero, [cree una nueva instancia de  [!DNL Adobe Commerce as a Cloud Service] (SaaS)](../getting-started.md#create-an-instance).

### Configuración de la herramienta de extracción

La herramienta de extracción se utiliza para extraer datos de la instancia de origen.

1. Descargue la herramienta de extracción desde el vínculo proporcionado por Adobe.
1. Establezca las siguientes variables de entorno en la herramienta de extracción:
   - Detalles de conexión a la base de datos MySQL existente
   - El identificador de inquilino de destino de su instancia [!DNL Adobe Commerce as a Cloud Service]
   - Sus credenciales de IMS, entre ellas:
      - ID de cliente
      - Secreto de cliente
      - Ámbitos de IMS
      - URL de IMS: la URL base. Por ejemplo, `https://ims-na1.adobelogin.com/`.
      - ID de organización IMS

   Para ámbitos de IMS y otros valores, seleccione su tipo de OAuth en la sección **Credenciales** dentro de su proyecto en [Adobe Developer Console](https://developer.adobe.com/console/). Se proporciona más información en el archivo `.example.env` incluido con la herramienta de extracción.

### Extracción de datos

Antes de ejecutar la herramienta de extracción, el implementador de la solución debe establecer un túnel SSH a la base de datos PaaS mediante:

```bash
magento-cloud tunnel:open
```

A continuación, ejecute la herramienta de extracción, que:

1. Conéctese a la base de datos de PaaS, analice su esquema y compárelo con los detalles del esquema del inquilino de SaaS.
1. Generar un plan de extracción y transformación basado en los elementos de esquema comunes entre PaaS y SaaS.
1. Extraiga los datos mediante el Servicio de administración de datos de catálogo (CDMS).

### Carga de datos

Ejecute la herramienta de carga de datos proporcionada por Adobe. Esta herramienta:

1. Conéctese a la base de datos de inquilinos de SaaS con una cuenta de migración.
1. Genere un plan de carga.
1. Ejecute el plan moviendo los datos a la base de datos de inquilinos SaaS por lotes.
1. Procese los medios del catálogo y transfiéralos al entorno de destino.
1. Vacía la caché de Redis de SaaS e invalida los índices de base de datos del inquilino.

### Ingesta de datos del catálogo

Una vez cargados los datos, los datos del catálogo fluyen automáticamente de la base de datos de inquilino de SaaS al servicio de catálogo.

El servicio de catálogo comparte estos datos con Live Search y Recommendations de productos. No se requiere ninguna intervención manual para este proceso. Los datos estarán disponibles en todos los servicios una vez que se complete la ingesta.

### Verificación de integridad de datos

Después de la migración, CDMS realiza las siguientes comprobaciones automáticas de integridad de los datos para garantizar la precisión e integridad de los datos migrados:

**Verificación basada en API**

Durante la verificación, CDMS compara las respuestas de API de REST y GraphQL de consultas ejecutadas anteriormente con los registros correspondientes de la instancia de destino. Cualquier discrepancia es visible en el estado de la migración.

**Verificación a nivel de base de datos**

Durante la verificación, CDMS cuenta el número de registros extraídos y compara ese número con la cantidad de registros cargados.

**Verificación a petición (opcional)**

También puede almacenar en déclencheur manualmente la verificación completa de todos los registros del sistema:

>[!NOTE]
>
>Este proceso consume muchos recursos y solo debe utilizarse en entornos de zonas protegidas.

La verificación completa incluye:

- Verificación completa basada en API mediante todas las respuestas de API de REST y GraphQL extraídas previamente.
- Informe detallado de cualquier incoherencia encontrada
