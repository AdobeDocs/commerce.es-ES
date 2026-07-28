---
title: Ejecución de una migración masiva de datos
description: Obtenga información sobre cómo configurar y ejecutar una migración de datos en lotes desde una Adobe Commerce PaaS o una instancia local a Adobe Commerce as a Cloud Service con la CLI.
feature: Cloud
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
role: Developer
level: Intermediate
autotag-review: '2026-07-22T19:19:07.600Z'
TQID: 'https://experienceleague.adobe.com/z9659Vnf2JLxJ4U5p3tEEjurj5Mg3bfKj68Gheq2AXY'
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: bd989d82-1e15-4534-88db-f1f51dd77ffaid: c1256247-af4b-46d8-9dca-0c654ecfa157id: c32adafa-ed01-4b31-997e-2413013911b0id: d1e21356-0064-4f48-9089-16e3f0dbd2a6id: dac87252-6066-4d6e-a9d2-f6d84c323de7id: e8818fe6-9c8b-4bc0-9ef8-377a10b7bc75id: f08fa0de-a550-4acd-b570-f81cf1d03aaf
subfeature_v2: id: f8ddfd3b-6194-46e8-a176-0e918039be56
role_v2: id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: ebde5b41-29c9-4f5e-9ef6-1197e85409e3
source-git-commit: 670b6214b28be93a16130552a226a8cadb487324
workflow-type: tm+mt
source-wordcount: 2802
ht-degree: 0%

---

# Ejecución de una migración masiva de datos

{{bulk-data-early-access}}

Esta guía es una referencia operativa paso a paso para ejecutar una migración de datos desde un PaaS de [!DNL Adobe Commerce] o una instalación local a [!DNL Adobe Commerce as a Cloud Service] mediante la herramienta de migración de datos en masa. Los valores de configuración reales y los detalles específicos del entorno varían según la configuración.

Antes de empezar, confirme que ha completado todos los elementos de la [lista de comprobación de preparación para clientes](readiness-checklist.md) y que ha verificado el acceso a la API con la [guía de acceso al servicio de migración](cdms-access.md).

>[!NOTE]
>
>Como parte del paquete de distribución de herramientas, se proporciona documentación técnica completa que abarca la arquitectura de la herramienta, el diseño interno, el marco de trabajo de transformación de datos y el marco de trabajo de pruebas de integridad.

## Requisitos previos

- **[!DNL Docker]** y **[!DNL Docker Compose]** deben estar instalados en el equipo donde se ejecuta la migración.
- El usuario que ejecuta la migración debe tener permiso para ejecutar `docker` y `docker compose` (o los comandos `docker-compose` heredados). El [!DNL Linux], el usuario debe estar en el grupo `docker`. En [!DNL macOS] y [!DNL Windows], [!DNL Docker Desktop] debe estar en ejecución y ser accesible. La CLI de migración invoca [!DNL Docker] repetidamente y los errores de permisos aquí bloquean la ejecución.
- La configuración principal debe ser coherente entre origen y destino antes de ejecutar la migración. Esta herramienta no migra los datos de configuración principales, como la configuración del sistema y la configuración del almacén. Configúrelo en el destino de forma independiente y alinéelo con el origen antes de la migración.

## Configuración del paquete de herramientas

Configure el entorno para la migración masiva de datos:

>[!VIDEO](https://video.tv.adobe.com/v/3496121)

1. Extraiga el contenido de `ccsaas-migration-tools.tar.gz`.

1. Ejecute todos los comandos de la carpeta `ccsaas-migration-tools` extraída, donde se encuentra `bin/console`.

1. Asegúrese de que la carpeta sea editable para registros, caché, [!DNL Composer] y archivos generados.

   Cambie la propiedad de todos los archivos y subcarpetas de ese directorio al usuario del sistema operativo que ejecuta la migración, de modo que la herramienta pueda leer y escribir de manera coherente. Por ejemplo, en [!DNL Linux]: `chown -R <user>:<group> <project-root>`.

1. Cree los archivos `.env` y `.my.cnf` en la raíz del proyecto copiando los archivos de ejemplo (`.example.env` a `.env` y `.my.cnf.example` a `.my.cnf`) y, a continuación, rellene los valores descritos en las secciones siguientes.

### Archivos de configuración de ejemplo

Los archivos `.example.env` y `.my.cnf.example` de la raíz del repositorio son el punto de partida de la configuración. Copie cada archivo en su nombre de trabajo y rellene los valores necesarios.

| Archivo de ejemplo | Copiar a | Qué cubre |
| --- | --- | --- |
| `.example.env` | `.env` | Lista anotada de todas las variables de entorno admitidas: rendimiento, CDMS, IMS, SaaS de destino, autenticación de direcciones URL de origen, OAuth y valores PaaS opcionales (`MAGENTO_CLOUD_CLI_TOKEN` cuando `id=` se establece en `.my.cnf`). La lista de variables completa está disponible en el archivo `.env`. |
| `.my.cnf.example` | `.my.cnf` | Diseños de referencia `[section]` para [!DNL MySQL] local y PaaS (`id=project:environment`). El nombre de `[section]` debe coincidir con `SOURCE_CONNECTION_NAME` en `.env`. Los campos incluyen `user`, `password`, `host`, `port`, `database` y `id=` para PaaS. |

## Configuración del archivo de entorno

El archivo `.env` en la raíz del proyecto es la configuración de migración y extracción. Controla la canalización de CLI, incluidas las direcciones URL de origen y destino, OAuth, la conexión CDMS remota, la autenticación SaaS e IMS y otros conmutadores.

>[!NOTE]
>
>No incluya barras finales en las direcciones URL. Por ejemplo, use `https://example.com` en lugar de `https://example.com/`.

Edite el archivo `.env` y establezca al menos los siguientes valores correctamente. Para obtener la lista completa de variables admitidas, consulte las anotaciones en línea de `.example.env`.

```shell-session
SOURCE_INSTANCE_URL=https://<source-host>
SOURCE_INSTANCE_GRAPHQL_URL=https://<source-host>/graphql
SOURCE_INSTANCE_REST_URL=https://<source-host>/rest
SOURCE_INSTANCE_CONSUMER_KEY=<consumer_key>
SOURCE_INSTANCE_CONSUMER_SECRET=<consumer_secret>
SOURCE_INSTANCE_ACCESS_TOKEN=<access_token>
SOURCE_INSTANCE_ACCESS_TOKEN_SECRET=<access_token_secret>
```

### Configurar credenciales de OAuth de origen

>[!VIDEO](https://video.tv.adobe.com/v/3496142)

Estos cuatro valores firman solicitudes desde la herramienta de migración a las API del almacén de origen. Para obtenerlas, abra el origen [!UICONTROL Admin] y vaya a [!UICONTROL **Sistema**] > [!UICONTROL **Extensiones**] > [!UICONTROL **Integraciones**]. Cree o abra una integración y copie los valores en `.env`:

```shell-session
SOURCE_INSTANCE_CONSUMER_KEY=<consumer_key>
SOURCE_INSTANCE_CONSUMER_SECRET=<consumer_secret>
SOURCE_INSTANCE_ACCESS_TOKEN=<access_token>
SOURCE_INSTANCE_ACCESS_TOKEN_SECRET=<access_token_secret>
```

### Establezca el token CLI de nube

>[!NOTE]
>
>Esto solo se aplica a [!DNL Adobe Commerce on Cloud] instancias de origen. La herramienta detecta automáticamente el tipo de origen de `.my.cnf`. Si la sección `SOURCE_CONNECTION_NAME` contiene una línea `id=` (por ejemplo, `id=project:production`), el origen es [!DNL Adobe Commerce on Cloud] y se requiere `MAGENTO_CLOUD_CLI_TOKEN`. Para orígenes locales sin `id=`, este token no es necesario y se omite la configuración del túnel.

1. Vaya a `https://accounts.magento.cloud` e inicie sesión.

1. Haga clic en la imagen de perfil y seleccione [!UICONTROL **Configuración de la cuenta**].

1. Vaya a la sección [!UICONTROL **Tokens de API**].

1. Seleccione [!UICONTROL **Crear un token de API**], asígnele un nombre descriptivo y copie el token generado.

1. Establecer el token en `.env`:

   ```text
   MAGENTO_CLOUD_CLI_TOKEN=<your_magento_cloud_api_token>
   ```

>[!NOTE]
>
>Si es la primera vez que utiliza la CLI de nube, también debe agregar su clave pública SSH a la cuenta. Consulte la [Guía de conexiones seguras](https://experienceleague.adobe.com/en/docs/commerce-on-cloud/user-guide/develop/secure-connections) para obtener instrucciones.

### Alinear configuración de administración de Commerce

Antes de la migración, asegúrese de que las siguientes configuraciones sean coherentes entre el origen y el destino.

>[!NOTE]
>
>Para garantizar una migración sin problemas, [!DNL Adobe] recomienda que todas las configuraciones principales en la instancia de destino sean coherentes con el origen.

### Configuración de las credenciales de SaaS e IMS de Target

>[!VIDEO](https://video.tv.adobe.com/v/3496167)

Estas son las configuraciones de IMS y API de [!DNL Adobe Commerce as a Cloud Service] para el destino. Necesita el ID de inquilino, el ID de organización, las credenciales de servidor a servidor de IMS OAuth y el host de IMS correcto para su entorno. Coordine con su equipo de Adobe el acceso a la organización, al inquilino y al perfil. No intente inferir ni estimar valores sensibles.

#### Generar credenciales de IMS

Usar [Adobe Developer Console](https://developer.adobe.com/console/). Necesita acceso de [!UICONTROL Developer] o [!UICONTROL Admin] en la organización de Adobe para crear proyectos. Un inicio de sesión básico de usuario no es suficiente para agregar API.

1. Cree un proyecto o abra uno existente y luego seleccione [!UICONTROL Add API].

1. Elija [!UICONTROL **Adobe Commerce as a Cloud Service**] y continúe.

1. Seleccione [!UICONTROL **Servidor a servidor de OAuth**] como tipo de autenticación y continúe.

1. Seleccione el perfil de producto que su equipo de Adobe espera para este inquilino y, a continuación, seleccione [!UICONTROL **Guardar la API configurada**].

1. En la barra lateral del proyecto, abra [!UICONTROL **OAuth Server-to-Server**] (o [!UICONTROL **Credentials**]) y luego copie el ID de cliente y el secreto de cliente en `.env` como `ADOBE_IMS_CLIENT_ID` y `ADOBE_IMS_CLIENT_SECRET`.

El extremo del token de IMS (`ADOBE_IMS_URL`) debe coincidir con el entorno de la credencial.

| Nivel | Típico `ADOBE_IMS_URL` |
| --- | --- |
| Control de calidad o ensayo | `https://ims-na1-stg1.adobelogin.com` |
| Preproducción o producción | `https://ims-na1.adobelogin.com` |

>[!NOTE]
>
>`na1` en estas direcciones URL representa la región donde se aprovisiona la instancia de destino. Sustitúyala por el identificador de región adecuado si la instancia se aprovisiona en una región diferente.

`ADOBE_IMS_META_SCOPES` debe coincidir con los ámbitos proporcionados en esa credencial. El archivo `.example.env` incluye la cadena de ámbito separada por comas completa como referencia. Cámbielo únicamente si Adobe le indica que lo haga.

#### Asignar credenciales de [!DNL Adobe I/O] al archivo de entorno

En [!DNL Developer Console], los valores de servidor a servidor de OAuth se presentan como un ID de cliente y un secreto de cliente, correspondientes a la siguiente estructura JSON:

```json
{
  "client_id": "xxxxxxxxxxxxxxxxxxxxxxxxxxx",
  "client_secret": "xxxxxxxxxxxxxxxxxxxxxxxxxxx"
}
```

Asignarlos a `.env` (marcadores de posición de ejemplo):

```shell-session
TARGET_ORG_ID=<org_id>@AdobeOrg
ADOBE_IMS_URL=https://ims-na1.adobelogin.com
ADOBE_IMS_CLIENT_ID=xxxxxxxxxxxxxxxxxxxxxxxxxxx
ADOBE_IMS_CLIENT_SECRET=xxxxxxxxxxxxxxxxxxxxxxxxxxx
ADOBE_IMS_META_SCOPES=AdobeID,openid,additional_info.projectedProductContext
```

Los hosts de la API de SaaS difieren entre la preproducción y la producción. `TARGET_INSTANCE_REST_URL` y `TARGET_INSTANCE_GRAPHQL_URL` deben usar el mismo entorno de API de Commerce que la migración, ya sea de preproducción o de producción. No mezcle un nivel con el CDMS o inquilino del otro nivel.

| Entorno | Host típico en `TARGET_INSTANCE_*_URL` |
| --- | --- |
| Preproducción o zona protegida | `https://na1-sandbox.api.commerce.adobe.com/{tenantId}` |
| Producción | `https://na1.api.commerce.adobe.com/{tenantId}` |

>[!NOTE]
>
>`na1` en estas direcciones URL representa la región donde se aprovisiona la instancia de destino. Sustitúyala por el identificador de región adecuado si la instancia se aprovisiona en una región diferente.

```shell-session
TARGET_TENANT_ID=<tenant_id>
TARGET_ORG_ID=<org_id>@AdobeOrg
ADOBE_IMS_URL=https://ims-na1.adobelogin.com
ADOBE_IMS_CLIENT_ID=<client_id>
ADOBE_IMS_CLIENT_SECRET=<client_secret>
ADOBE_IMS_META_SCOPES=AdobeID,openid,additional_info.projectedProductContext
TARGET_INSTANCE_REST_URL=https://na1-sandbox.api.commerce.adobe.com/{tenantId}
TARGET_INSTANCE_GRAPHQL_URL=https://na1-sandbox.api.commerce.adobe.com/{tenantId}/graphql
```

Para los hosts SaaS de producción, reemplace `na1-sandbox` por `na1` en ambas direcciones URL `TARGET_INSTANCE_*`. Utilice el(la) `ADOBE_IMS_URL` coincidente para ese nivel, como se muestra en la tabla anterior.

### Establezca el punto final de CDMS

Dirija la herramienta de migración al host de la API de CDMS que coincida con el entorno al que está migrando. Establezca `CDMS_HOST` (y normalmente `CDMS_PORT=443`) en `.env`. Utilice un host, ya sea de preproducción o de producción, no ambos.

| Entorno | Cuándo usar | `CDMS_HOST` |
| --- | --- | --- |
| Preproducción | Ejecuciones de estilo de zona protegida o de preproducción, CDMS que no son de producción | `https://commerce-data-migration-service-preprod-external.adobe.io` |
| Producción | Migración o migración de producción en directo | `https://commerce-data-migration-service-prod-external.adobe.io` |

Establezca o quite los comentarios del bloque que coincida con la ejecución:

```shell-session
# Pre-production CDMS
CDMS_HOST=https://commerce-data-migration-service-preprod-external.adobe.io
CDMS_PORT=443

# Production CDMS (use for prod cutover only)
# CDMS_HOST=https://na1.api.commerce.adobe.com
# CDMS_PORT=443
```

### Configuración del código de tienda

`STORE_CODE` es el código de vista de tienda que usa la herramienta de migración para las llamadas a la API de REST de instancia de origen, la creación de clientes de prueba sintética y la limpieza de datos. También se envía como encabezado `x-store-code` durante la fase de carga.

`STORE_CODE` toma como valor predeterminado `default` en `.example.env`. Compruebe que coincida con el código de vista de tienda predeterminado de la instancia de origen. Para comprobarlo, en el origen [!UICONTROL Admin] vaya a [!UICONTROL **Tiendas**] > [!UICONTROL **Todas las tiendas**] y observe la columna [!UICONTROL **Código**] para ver la vista de la tienda que se debe usar. Si el código que se muestra allí no es `default`, actualice `STORE_CODE` en `.env` para que coincida.

## Configurar el archivo de conexión a base de datos

>[!VIDEO](https://video.tv.adobe.com/v/3496152)

El archivo `.my.cnf` proporciona la configuración de conexión [!DNL MySQL] para la extracción de la herramienta de migración. Créelo copiando `.my.cnf.example` a `.my.cnf` en la raíz del proyecto. El nombre de sección debe coincidir con `SOURCE_CONNECTION_NAME` en `.env`.

Para una fuente local o autoalojada:

```ini
[<connection-name>]
user=<db_user>
password='<db_password>'
host=<db_host>
port=3306
database=<db_name>
```

>[!NOTE]
>
>El equipo que ejecuta la herramienta de migración debe tener acceso directo a la red a la base de datos de origen. La herramienta no establece ni verifica automáticamente la conectividad local. Antes de ejecutar cualquier comando de migración, confirme que el host, el puerto y las credenciales están accesibles desde el equipo de migración.

Para un origen de [!DNL Adobe Commerce on Cloud]:

```ini
[<connection-name>]
id=<project_id>:<environment>
```

El campo `id=` indica a la herramienta que el origen es PaaS y la configuración del túnel de déclencheur mediante `MAGENTO_CLOUD_CLI_TOKEN`. Los valores `project_id` y `environment` están disponibles en [!DNL Cloud Console] o mediante los comandos `magento-cloud project:list` y `magento-cloud environment:list`.

## Preparar la red y las instancias

La autenticación básica de HTTP delante de la tienda puede bloquear el tráfico de API y herramientas. Asegúrese de que esté desactivado para la URL de origen utilizada por la migración o que las rutas de la herramienta estén permitidas, de modo que las solicitudes REST y GraphQL puedan llegar a la tienda.

### Mantener estabilidad de base de datos de origen durante la extracción

Mientras la herramienta extrae datos de la base de datos de origen, ningún otro proceso debe escribirle. Las escrituras concurrentes pueden generar una instantánea incoherente.

- Detenga cron en el origen y cualquier programador del sistema operativo que ejecute `bin/magento` u otros escritores para la ventana de extracción, o asegúrese de que no se puedan ejecutar durante la extracción.
- Revise otras integraciones, como ERP, OMS, PIM, trabajos personalizados y API de terceros que escriben en la misma base de datos. Pausar o bloquear escrituras para la ventana de extracción de modo que nada mute las tablas mientras se ejecuta la extracción.
- Esto complementa el modo de mantenimiento y el acceso a túneles o bases de datos. Juntos reducen el tráfico de tiendas y API. Cron e integraciones son fuentes independientes de escrituras que se deben controlar explícitamente.

### Target

Si es necesario borrar el catálogo de destino antes de la migración, elimine los productos de [!UICONTROL Admin] en lotes pequeños, por ejemplo, de 200 a la vez, para evitar conflictos de catálogo duplicados y tiempos de espera de eliminación en lotes.

## Cree y ejecute la migración

Trabaje desde el directorio del proyecto extraído con acceso de escritura.

### Mantener la sesión activa a través de SSH

Si se conecta a través de SSH, una red perdida puede acabar con su shell e interrumpir una migración prolongada. El comando GNU `screen` mantiene la sesión activa en el servidor:

```bash
screen -S migration          # new session named "migration"
# run ./bin/console commands here; when you want to disconnect without stopping work:
# press Ctrl+A, release, then press d   # detach
screen -ls                   # list sessions
screen -x migration          # reattach to "migration"
```

También puede usar `tmux` si está disponible en el servidor.

### Crear la imagen de Docker

Genere la imagen [!DNL Docker] utilizada por `bin/console`, que contiene PHP, CLI y dependencias. Ejecute esto antes de la primera ejecución o después de que Dockerfile o la imagen base cambien.

```bash
./bin/console build
```

### Inicio de los servicios de backup

Inicie los servicios de copia de seguridad de [!DNL Docker Compose] para la herramienta, como la base de datos de prueba local y, cuando esté habilitada en `.env`, los servicios locales opcionales. Los servicios exactos dependen de la configuración. Ejecute esto después de una compilación correcta y antes de los comandos shell, migration o phase.

```bash
./bin/console start
```

### Inicialice el contenedor CLI

Inicie el contenedor CLI una vez para que el punto de entrada pueda finalizar la instalación, como una instalación de [!DNL Composer] si es necesario, en el proyecto montado. Ejecute esto una vez antes de la primera ejecución de la migración en un entorno nuevo.

```bash
./bin/console shell
exit
```

### Ejecute la migración

La herramienta admite dos métodos de migración. Elija el que se adapte a su caso de uso.

#### Migración en una sola fase

No se requiere ningún modo de mantenimiento en la instancia de origen. Ejecute la canalización de migración completa con un solo comando:

```bash
./bin/console migration
```

El comando ejecuta todos los pasos de la canalización automáticamente, de extremo a extremo, en el siguiente orden.

1. **Comprobación de configuración**: valida las variables de entorno y la configuración de la herramienta.
1. **Inicialización del entorno**: inicia servicios de [!DNL Docker], abre túneles en la nube (si corresponde) y ejecuta pruebas unitarias.
1. **Pruebas de integración e inicialización de CDMS**: ejecuta pruebas de integración e inicializa la conexión de API de CDMS.
1. **Crear migración**: registra la migración con CDMS y espera el análisis del esquema de destino. El identificador de migración se guardó en `.migration_id`.
1. **Pruebas funcionales y generación de datos de prueba**: ejecuta pruebas funcionales y genera datos de prueba sintéticos en el origen para la comprobación de integridad (si está habilitada).
1. **Extracción de datos**: extrae datos de la instancia de origen.
1. **Cargar en destino**: carga los datos extraídos en la instancia de destino [!DNL Adobe Commerce as a Cloud Service]. Las vistas de ensayo se limpian en el origen y los datos de prueba de origen se eliminan a través de REST en paralelo con la carga.
1. **Verificación de integridad de datos**: déclencheur la verificación de suma de comprobación y ejecuta pruebas de verificación de API locales. Los resultados se registran y los errores no detienen la canalización.
1. **Limpieza de datos de prueba en destino**: quita los datos de prueba sintéticos de la instancia de destino.
1. **Resultados del proceso**: genera un resumen de la migración y, opcionalmente, descarga artefactos del almacenamiento.

Utilice esta opción cuando no se requiera ninguna ventana de mantenimiento, lo que es típico para ejecuciones en seco de extremo a extremo, entornos de desarrollo o de zona protegida, o cualquier migración en la que el origen pueda permanecer activo durante la extracción.

>[!WARNING]
>
>No utilice esta opción cuando sea necesario un origen congelado, por ejemplo, cualquier migración de producción en la que no deban producirse nuevos pedidos o cambios de datos durante la extracción. En su lugar, utilice la migración por fases. No utilice este comando como paso dentro del flujo de trabajo de mantenimiento por fases.

#### Migración multifase con modo de mantenimiento

Se requiere el modo de mantenimiento en la instancia de origen para garantizar la coherencia de los datos durante la extracción. La migración se divide en distintas fases que debe ejecutar en orden.

>[!NOTE]
>
>Hay dos CLI diferentes implicadas. Los comandos `./bin/console` se ejecutan desde la raíz del proyecto de la herramienta de migración. Los comandos `bin/magento maintenance:*` se ejecutan en el servidor de aplicaciones [!DNL Adobe Commerce] de origen, a través de SSH hasta la raíz de instalación o a través de [!UICONTROL Admin]. La herramienta no emite [!DNL Magento] comandos de mantenimiento en su nombre.

| Fase | Quién lo dirige | Estado de Source |
| --- | --- | --- |
| 1. `migration:before-maintenance` | Herramienta | Activo: no habilitar aún el mantenimiento |
| &#x200B;2. Habilitar modo de mantenimiento | Manual | Transición a congelado |
| 3. `migration:during-maintenance` | Herramienta | Congelado: no desactivar el mantenimiento durante esta fase |
| &#x200B;4. Desactivar el modo de mantenimiento | Manual (condicional) | Volver a activar la instancia de origen de transición |
| &#x200B;5. `migration:cleanup` (opcional) | Herramienta | Activo: debe estar fuera de mantenimiento |

**Fase 1: antes del mantenimiento (el origen está activo)**

Ejecute mientras la instancia de origen está activa y acepta tráfico. El acceso de REST y GraphQL al origen debe estar totalmente disponible. No activar el modo de mantenimiento antes de que finalice esta fase.

Vuelva a la raíz del servidor y ejecute:

```bash
./bin/console migration:before-maintenance
```

1. **Comprobación de configuración**: valida las variables de entorno y la configuración de la herramienta.
1. **Inicialización del entorno**: inicia servicios de [!DNL Docker], abre túneles de nube PaaS (si corresponde) y ejecuta pruebas unitarias.
1. **Pruebas de integración e inicialización de CDMS**: ejecuta pruebas de integración e inicializa la conexión de API de CDMS.
1. **Crear migración**: registra la migración con CDMS y espera el análisis del esquema de destino. El identificador de migración se guardó en `.migration_id`.
1. **Pruebas funcionales**: ejecuta pruebas funcionales en el origen activo.
1. **Generación de datos de prueba**: crea clientes de prueba sintética y pedidos en el origen para la verificación de integridad (si está habilitada).

**Fase 2 — Habilitar modo de mantenimiento (manual)**

Habilite el modo de mantenimiento en el origen y ponga en pausa todas las actividades que escriben en la base de datos o que afectan a ella, incluidos los trabajos programados, las integraciones de terceros, el procesamiento de pedidos y la sincronización de recursos de medios.

En el servidor Commerce de origen (raíz de instalación), ejecute:

```bash
bin/magento maintenance:enable
```

**Fase 3: durante el mantenimiento (el origen está congelado)**

Ejecutar con la instancia de origen en modo de mantenimiento. La fuente debe permanecer congelada durante toda esta fase. No desactive el modo de mantenimiento hasta que la **Fase 3** se complete correctamente.

```bash
./bin/console migration:during-maintenance
```

1. **Configuración de túnel de nube**: para [!DNL Adobe Commerce on Cloud] instancias de origen, reabre los túneles de nube y verifica la conectividad de la base de datos. Se omite automáticamente para instancias locales.
1. **Extracción de datos**: extrae datos de la instancia de origen congelada.
1. **Limpieza de la vista de ensayo**: quita las vistas de ensayo del origen mediante una conexión directa a la base de datos (segura en modo de mantenimiento).
1. **Cargar en destino**: carga los datos extraídos en la instancia de destino [!DNL Adobe Commerce as a Cloud Service] y espera a que se completen.
1. **Verificación de integridad de datos**: déclencheur la verificación de suma de comprobación de CDMS y ejecuta pruebas de verificación de API locales. Los resultados se registran y los errores no detienen la canalización.
1. **Limpieza de datos de prueba en destino**: quita los datos de prueba sintéticos de la instancia de destino.
1. **Resultados del proceso**: genera un resumen de la migración y, opcionalmente, descarga artefactos del almacenamiento.

**Fase 4: deshabilitar el modo de mantenimiento (manual, condicional)**

Esta fase desactiva el modo de mantenimiento y vuelve a habilitar el tráfico en la instancia de origen. Este paso es necesario antes de ejecutar la fase de limpieza, ya que la limpieza se comunica con el origen a través de REST y falla con `HTTP 503` si el modo de mantenimiento aún está activo.

En el servidor Commerce de origen, ejecute:

```bash
bin/magento maintenance:disable
```

**Fase 5 — Limpieza (opcional, el origen debe estar activo)**

Elimine los clientes de prueba sintética y los pedidos creados en **Phase 1** de la instancia de origen mediante REST. Esta fase solo se puede ejecutar después de desactivar el modo de mantenimiento.

>[!NOTE]
>
>Omita esta fase si `SKIP_TEST_DATA_CREATION=true` está establecido en `.env`, ya que no se crearon datos de prueba.

Vuelva a la raíz del servidor y ejecute:

```bash
./bin/console migration:cleanup
```

1. **Configuración de conexión de base de datos**: para [!DNL Adobe Commerce on Cloud] instancias de origen, reabre los túneles de nube. Para las instancias locales, establece y verifica la conectividad directa con la base de datos.
1. **Limpieza de REST de Source**: elimina los clientes y pedidos de prueba sintética del origen a través de la API de REST.

## Reanudar o volver a ejecutar una migración

La herramienta de migración realiza un seguimiento del progreso mediante un archivo de `.migration_id` en la raíz del proyecto. Este archivo se crea automáticamente cuando se inicia una nueva migración y registra el identificador de migración actual.

### Reanudar tras un error

Si una ejecución de migración falla o se interrumpe, vuelva a ejecutar el mismo comando para reanudarlo desde el último paso correcto (extracción, carga o verificación) en lugar de reiniciar desde cero. Los pasos ya completados se omiten automáticamente.

>[!IMPORTANT]
>
>Al reanudar la fase `migration:during-maintenance`, el origen debe permanecer en modo de mantenimiento durante todo el proceso. Si el origen se ha eliminado del mantenimiento o los datos se han cambiado entre ejecuciones, la migración reanudada puede producir resultados incoherentes.

### Iniciar una nueva migración

Para descartar una ejecución anterior e iniciar una migración completamente nueva, elimine el archivo `.migration_id` antes de iniciar la siguiente migración:

```bash
rm .migration_id
```

Si `.migration_id` existe y la migración anterior ya se ha completado, la herramienta imprime un mensaje que indica que la migración ya ha finalizado y le recomienda que elimine el archivo.

## Revisar registros y depurar

Todos los registros de migración se escriben en el directorio `logs/` de la raíz del proyecto y se organizan en subdirectorios con marca de tiempo:

```text
logs/
  2026-03-23_14-30-00/     ← one directory per run
    index.log              ← main pipeline log (start here)
    ...
```

- `index.log` es el registro de orquestación de canalización principal. Si un paso falla, muestra qué secuencia de comandos salió con un código distinto de cero y por qué.
- Los registros por paso, como `09b_run_load.log` y `11_verify_data_integrity_local.log`, contienen resultados detallados para cada fase.
