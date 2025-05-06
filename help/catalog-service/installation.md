---
title: Incorporación e instalación
description: Aprenda a instalar [!DNL Catalog Service]
exl-id: 3f8492c3-f76d-49b7-a201-35deace36a1d
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."
source-git-commit: be1c739f3821a5f1e846b3026088e3a3ff45a60f
workflow-type: tm+mt
source-wordcount: '885'
ht-degree: 0%

---

# Incorporación e instalación

Instale el servicio de catálogo para solicitar y recibir datos de producto de una instancia de Commerce mediante la [API de GraphQL del servicio de catálogo](https://developer.adobe.com/commerce/services/graphql/catalog-service/). El servicio de catálogo se entrega como un metapaquete de compositor desde el repositorio repo.magento.com.

>[!NOTE]
>
>Si la instancia de Commerce utiliza Live Search o Product Recommendations, el servicio de catálogo se instala o actualiza automáticamente al incorporar o actualizar esos servicios. Para obtener más información, consulte las instrucciones de instalación de [Live Search](https://experienceleague.adobe.com/en/docs/commerce/live-search/install) y [Product Recommendations](https://experienceleague.adobe.com/en/docs/commerce/product-recommendations/getting-started/install-configure).



## Requisitos del sistema

**Requisitos de software**

- Adobe Commerce 2.4.4+
- PHP 8.1, 8.2, 8.3, 8.4
- Compositor: 2.x

**Plataformas admitidas**

- Adobe Commerce en infraestructura en la nube: 2.4.4+
- Adobe Commerce local: 2.4.4+

## Extremos

[!DNL Catalog Service] tiene dos extremos disponibles para la incorporación:

- Zona protegida (`https://catalog-service-sandbox.adobe.io/graphql`): se usa para pruebas y validación antes de activarse
- Producción (`https://catalog-service.adobe.io/graphql`): se utiliza para tráfico en tiempo real para comerciantes y sitios web de Commerce

Todas las instancias de prueba comercio utilizan el punto final de Sandbox.

Realice todas las pruebas de carga en el extremo del Simulador para pruebas. Antes de comenzar las pruebas de carga, envíe un vale](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) de [soporte para que el equipo Servicios pueda anticipar el tráfico adicional del servidor.

## Instalación y configuración

Para comenzar con [!DNL Catalog Service] para Adobe Commerce, se requieren los siguientes pasos:

- Instalar la extensión del Servicio de catálogo (`magento/catalog-service`)
- Configuración del servicio y la exportación de datos
- Acceso al servicio

### Instalación de la extensión del servicio de catálogo

>[!BEGINSHADEBOX]

**Requisito previo**

- Acceda a [repo.magento.com](https://repo.magento.com) para instalar la extensión. Para obtener las claves de clave y obtener los derechos necesarios, consulte [Obtención de las claves](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys) de autenticación. Para obtener nube instalaciones, consulte la Guía de comercio en infraestructura de [nube](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/authentication-keys)

- Acceso a la línea de comandos del servidor de aplicación de Adobe Systems Commerce.

>[!ENDSHADEBOX]

Instale la última versión de la extensión de servicios de catálogo (`magento/catalog-service`) en una instancia de Adobe Commerce que ejecute Adobe Commerce versión 2.4.4 o posterior. El servicio de catálogo se entrega como un metapaquete de composición desde el repositorio [repo.magento.com](https://repo.magento.com).

>[!BEGINTABS]

>[!TAB Infraestructura en la nube]

Utilice este método para instalar [!DNL Catalog Service] para una instancia de Commerce Cloud.

1. En la estación de trabajo local, cambie al directorio del proyecto para su proyecto de Adobe Commerce en la nube.

   >[!NOTE]
   >
   >Para obtener información sobre cómo administrar los entornos de proyecto de Commerce localmente, consulte [Administración de ramas con la CLI](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/cli-branches) en la _Guía del usuario de Adobe Commerce on Cloud Infrastructure_.

1. Consulte el Rama entorno para actualizar mediante la CLI de Adobe Commerce Cloud.

   ```shell
   magento-cloud environment:checkout <environment-id>
   ```

1. añadir la módulo de servicio de catálogo.

   ```bash
   composer require magento/catalog-service --no-update
   ```

1. Actualizar dependencias del paquete.

   ```bash
   composer update "magento/catalog-service"
   ```

1. Confirme y envíe los cambios de código para los archivos `composer.json` y `composer.lock`.

1. Agregue, confirme e inserte los cambios de código para los archivos `composer.json` y `composer.lock` en el entorno de nube.

   ```shell
   git add -A
   git commit -m "Add catalog service module"
   git push origin <branch-name>
   ```

   Si se insertan las actualizaciones en el entorno de la nube, se inicia el [proceso de implementación de la nube de Commerce](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/deploy/process) para aplicar los cambios. Compruebe el estado de implementación desde el [registro de implementación](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/test/log-locations#deploy-log).

>[!TAB Local]

Utilice este método para instalar [!DNL Catalog Service] para una instancia local.

1. Use Compositor para agregar el módulo Servicio de catálogo a su proyecto:

   ```bash
   composer require magento/catalog-service --no-update
   ```

1. Actualice las dependencias e instale la extensión:

   ```bash
   composer update  "magento/catalog-service"
   ```

1. Actualizar Adobe Commerce:

   ```bash
   bin/magento setup:upgrade
   ```

1. Borre la caché:

   ```bash
   bin/magento cache:clean
   ```

   >[!TIP]
   >
   >En algunos casos, especialmente cuando se implementa en producción, es posible que desee evitar borrar el código compilado porque puede tardar algún tiempo. Asegúrese de realizar una copia de seguridad del sistema antes de realizar cualquier cambio.

>[!ENDTABS]

### Configuración del servicio y exportación de datos

Después de instalar el [!DNL Catalog Service], complete las siguientes tareas para integrar el servicio de catálogo con su Adobe Systems Commerce instancia. Esta integración permite la sincronización de datos y la comunicación entre el instancia de comercio, el servicio de catálogo y otros servicios de soporte. La sincronización de datos está controlada por la [extensión de exportación de datos SaaS](../data-export/overview.md).

1. Configure [Commerce Services Connector](https://experienceleague.adobe.com/en/docs/commerce/user-guides/integration-services/saas) especificando las claves de API y seleccionando un espacio de datos SaaS.

   La configuración del Conector de servicios de Commerce es un proceso único necesario para utilizar servicios de Adobe Commerce como el Servicio de catálogo, Live Search y Recomendaciones de productos. Si ya ha configurado el conector para otro servicio, omita este paso.

1. Realice una sincronización de datos inicial desde [el panel de administración de datos](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard).

   La sincronización inicial puede tardar entre unos minutos y horas según el tamaño del catálogo. Puede monitor el estado de sincronización desde el panel de administración de datos. Después del sincronizar inicial, el catálogo exporta datos de productos de forma continua para mantener los servicios actualizados.

   >[!NOTE]
   >
   >También puede inicio el sincronizar inicial desde la línea de comandos mediante la CLI de comercio. Consulte [el sincronizar](../data-export/data-export-cli-commands.md#initial-sync) inicial en la Guía _de exportación de_ datos de SaaS.

Para asegurarse de que la exportación del catálogo se ejecuta correctamente:

- [Confirme que los trabajos cron se están ejecutando](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues).
- Compruebe que los indexadores se estén ejecutando desde [Admin](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) o mediante el comando `bin/magento indexer:info` de la CLI de Commerce.
- Compruebe que los indizadores `Catalog Attributes Feed, Product Feed, Product Overrides Feed` y `Product Variant Feed` estén establecidos en `Update by Schedule`.

### Monitorización y solución de problemas de sincronización de datos

Desde Commerce Admin, puede supervisar el proceso de sincronización mediante [el tablero de administración de datos](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard). Use la [CLI de Commerce](../data-export/data-export-cli-commands.md#troubleshooting) y los registros para administrar y solucionar problemas del proceso.

### Acceso al servicio

Se puede acceder a la API de GraphQL [!DNL Catalog Service] desde el extremo ` https://catalog-service.adobe.io/graphql` mediante comandos POST a través de HTTPS.

En las consultas de GraphQL, debe especificar varios encabezados HTTP, incluida la clave de API pública que agregó a la configuración del Conector de servicios de Adobe Commerce en Admin. Para obtener más información, consulte la [Documentación de servicios de tienda GraphQL](https://developer.adobe.com/commerce/services/graphql/).

### Configuración del cortafuegos

Para permitir [!DNL Catalog Service] el paso de un cortafuegos, agréguelo `commerce.adobe.io` a la lista de permitidos.

## Servicio de catálogo y malla de API

La [malla de API para Adobe Developer App Builder](https://developer.adobe.com/graphql-mesh-gateway/gateway/overview/) permite a los desarrolladores integrar API privadas o de terceros y otras interfaces con productos de Adobe mediante Adobe IO.

Consulte el tema [[!DNL Catalog Service] y API Mesh](mesh.md) para obtener detalles de instalación y configuración.

## Tablero de administración de datos

Para obtener más información acerca de la sincronización de datos de [!DNL Catalog Service], consulte [Panel de administración de datos](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard).
