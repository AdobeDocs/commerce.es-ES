---
title: Instalación
description: Obtenga información sobre cómo instalar  [!DNL Catalog Service]
exl-id: 3f8492c3-f76d-49b7-a201-35deace36a1d
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."
source-git-commit: 1cb6443e79e0e3d813550f9b619b3a0f641cd989
workflow-type: tm+mt
source-wordcount: '754'
ht-degree: 0%

---

# Incorporación e instalación

Instale el servicio de catálogo para solicitar y recibir datos de producto de una instancia de Commerce mediante la [API de GraphQL del servicio de catálogo](https://developer.adobe.com/commerce/webapi/graphql/schema/catalog-service/). El servicio de catálogo se entrega como un metapaquete de compositor desde el repositorio repo.magento.com.

>[!NOTE]
>
>Si la instancia de Commerce utiliza Live Search o Product Recommendations, el servicio de catálogo se instala o actualiza automáticamente al incorporar o actualizar esos servicios. Para obtener más información, consulte las instrucciones de instalación de [Live Search](https://experienceleague.adobe.com/en/docs/commerce/live-search/install) y [Product Recommendations](https://experienceleague.adobe.com/en/docs/commerce/product-recommendations/getting-started/install-configure).


## Requisitos del sistema

**Requisitos de software**

- Adobe Commerce 2.4.4+
- PHP 8.1, 8.2, 8.3, 8.4
- Compositor: 2.x

**Plataformas compatibles**

- Adobe Commerce en infraestructura en la nube: 2.4.4+
- Adobe Commerce local: 2.4.4+

## Extremos

[!DNL Catalog Service] tiene dos extremos disponibles para la incorporación:

- Zona protegida (`https://catalog-service-sandbox.adobe.io/graphql`): se usa para pruebas y validación antes de activarse
- Producción (`https://catalog-service.adobe.io/graphql`): se usa para el tráfico en directo de comerciantes y sitios web de Commerce.

Todas las instancias de prueba de Commerce utilizan el extremo de zona protegida.

Realice todas las pruebas de carga en el extremo de la zona protegida. Antes de comenzar la prueba de carga, envíe un [ticket de asistencia](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/help-center-guide/magento-help-center-user-guide.html#submit-ticket) para que el equipo de servicios pueda anticipar el tráfico adicional del servidor.

## Instalación y configuración

Para comenzar con [!DNL Catalog Service] para Adobe Commerce, se requieren los siguientes pasos:

- Instalar la extensión del Servicio de catálogo (`magento/catalog-service`)
- Configuración del servicio y la exportación de datos
- Acceso al servicio

### Instalación de la extensión del servicio de catálogo

>[!BEGINSHADEBOX]

**Requisito previo**

- Acceda a [repo.magento.com](https://repo.magento.com) para instalar la extensión. Para obtener la generación de claves y los derechos necesarios, consulta [Obtener tus claves de autenticación](https://experienceleague.adobe.com/en/docs/commerce-operations/installation-guide/prerequisites/authentication-keys). Para instalaciones en la nube, consulte la [Guía de Commerce en infraestructura en la nube](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/authentication-keys)

- Acceso a la línea de comandos del servidor de aplicaciones de Adobe Commerce.

>[!ENDSHADEBOX]

Instale la última versión de la extensión de servicios de catálogo (`magento/catalog-service`) en una instancia de Adobe Commerce que ejecute Adobe Commerce versión 2.4.4 o posterior. El servicio de catálogo se entrega como un metapaquete de composición desde el repositorio [repo.magento.com](https://repo.magento.com).

>[!BEGINTABS]

>[!TAB Infraestructura en la nube]

Utilice este método para instalar [!DNL Catalog Service] para una instancia de Commerce Cloud.

1. En la estación de trabajo local, cambie al directorio del proyecto para su proyecto de Adobe Commerce en la nube.

   >[!NOTE]
   >
   >Para obtener información sobre cómo administrar los entornos de proyecto de Commerce localmente, consulte [Administración de ramas con la CLI](https://experienceleague.adobe.com/en/docs/commerce-cloud-service/user-guide/develop/cli-branches) en la _Guía del usuario de Adobe Commerce on Cloud Infrastructure_.

1. Consulte la rama de entorno para actualizar con la CLI de Adobe Commerce Cloud.

   ```shell
   magento-cloud environment:checkout <environment-id>
   ```

1. Añada el módulo Servicio de catálogo.

   ```bash
   composer require magento/catalog-service --no-update
   ```

1. Actualizar dependencias del paquete.

   ```bash
   composer update "magento/catalog-service"
   ```

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
   >En algunos casos, especialmente al implementar en producción, puede que desee evitar borrar el código compilado, ya que puede tardar algún tiempo. Asegúrese de realizar una copia de seguridad del sistema antes de realizar cualquier cambio.

>[!ENDTABS]

### Configuración del servicio y la exportación de datos

Después de instalar [!DNL Catalog Service], complete las siguientes tareas para integrar el servicio Catálogo con su instancia de Adobe Commerce. Esta integración permite la sincronización de datos y la comunicación entre la instancia de Commerce, el servicio de catálogo y otros servicios de soporte. La sincronización de datos está controlada por la [extensión de exportación de datos SaaS](../data-export/overview.md).

1. Configure [Commerce Services Connector](https://experienceleague.adobe.com/en/docs/commerce/user-guides/integration-services/saas) especificando las claves de API y seleccionando un espacio de datos SaaS.

   La configuración del Conector de servicios de Commerce es un proceso único necesario para utilizar servicios de Adobe Commerce como el Servicio de catálogo, Live Search y Recomendaciones de productos. Si ya ha configurado el conector para otro servicio, omita este paso.

1. Realice una sincronización de datos inicial desde [el panel de administración de datos](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard).

   La sincronización inicial puede tardar entre unos minutos y horas según el tamaño del catálogo. Puede monitorizar el estado de sincronización desde el panel de control de Data Management. Después de la sincronización inicial, el catálogo exporta datos de productos de forma continua para mantener los servicios actualizados.

   >[!NOTE]
   >
   >También puede iniciar la sincronización inicial desde la línea de comandos utilizando la CLI de Commerce. Consulte [Sincronización inicial](../data-export/data-export-cli-commands.md#initial-sync) en la _Guía de exportación de datos SaaS_.

Para asegurarse de que la exportación del catálogo se ejecuta correctamente:

- [Confirme que los trabajos cron se están ejecutando](https://experienceleague.adobe.com/en/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/cron-readiness-check-issues).
- Compruebe que los indexadores se estén ejecutando desde [Admin](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management) o mediante el comando `bin/magento indexer:info` de la CLI de Commerce.
- Compruebe que los indizadores `Catalog Attributes Feed, Product Feed, Product Overrides Feed` y `Product Variant Feed` estén establecidos en `Update by Schedule`.

### Monitorización y solución de problemas de sincronización de datos

Desde Commerce Admin, puede supervisar el proceso de sincronización mediante [el tablero de administración de datos](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/data-transfer/data-dashboard). Use la [CLI de Commerce](../data-export/data-export-cli-commands.md#troubleshooting) y los registros para administrar y solucionar problemas del proceso.
