---
title: Instalar [!DNL Data Connection]
description: Obtenga información sobre cómo instalar, actualizar y desinstalar la extensión  [!DNL Data Connection] de Adobe Commerce.
role: Admin, Developer
feature: Install
exl-id: 853ef2d1-85cb-41a8-9b07-887a758ed401
TQID: https://experienceleague.adobe.com/EbYHB6L9Q7bZNnoz3-yT4aaBcRiLiatvjO-hQyGOwoo
product_v2: id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
source-git-commit: 2362159cd352d812f60838b42ade1e98bab5a0d3
workflow-type: tm+mt
source-wordcount: 491
ht-degree: 0%

---

# Instalar [!DNL Data Connection]

Antes de instalar la extensión, [revise los requisitos previos](overview.md#prerequisites).

## Instalación de la extensión

La extensión [!DNL Data Connection] está disponible en [Adobe Marketplace](https://commercemarketplace.adobe.com/magento-experience-platform-connector.html). Cuando instala esta extensión desde la línea de comandos del servidor, se conecta a su instalación de Adobe Commerce como un [servicio](../landing/saas.md). Una vez completado el proceso, **[!DNL Data Connection]** y **Commerce Services Connector** aparecen en el menú **Sistema** en **Servicios** en Commerce _Admin_.

![[!DNL Data Connection] vista de administración de la extensión](assets/epc-adminui.png)

>[!NOTE]
>
>Después de la instalación, configure [!DNL Data Connection] en el Administrador. Consulte [Ámbito de configuración](connect-data.md#configuration-scope) para ver la configuración global frente a la configuración de ámbito de sitio web.

>[!IMPORTANT]
>
>Aunque el nombre de la extensión ha cambiado del conector de Experience Platform a [!DNL Data Connection], el nombre del paquete permanece `experience-platform-connector` para admitir la compatibilidad con versiones anteriores.

1. Para descargar el paquete `experience-platform-connector`, ejecute lo siguiente desde la línea de comandos:

   ```bash
   composer require magento/experience-platform-connector
   ```

   Este metapaquete contiene los siguientes módulos y extensiones:

   - `magento/orders-connector`
   - `magento/data-services`
   - `magento/customers-connector`
   - `magento/module-experience-connector`
   - `magento/module-experience-connector-admin`
   - `magento/module-experience-connector-admin-graph-ql`
   - `magento/module-experience-connector-aep-integration`

1. (Opcional) Para incluir [!DNL Live Search] datos, que comprenden [eventos de búsqueda](events.md#search-events), instale la extensión [[!DNL Live Search]](../live-search/install.md).

1. (Opcional) Para incluir datos B2B, que comprenden [eventos de solicitud](events.md#b2b-events), instale la [extensión B2B](#install-the-b2b-extension).

1. (Opcional) Si es un comerciante de atención médica, instale la extensión de [Servicios de datos HIPAA](#install-the-data-services-hipaa-extension) para que los datos de su back office [!DNL Commerce] estén preparados para HIPAA.

### Instale Adobe I/O Events y configure el módulo del conector de clientes

Después de instalar la extensión `experience-platform-connector`, debe instalar Adobe I/O Events para Adobe Commerce y configurar el módulo `customers-connector`.

Los siguientes pasos se aplican tanto a Adobe Commerce en la infraestructura en la nube como a las instalaciones locales.

1. Si está ejecutando Commerce 2.4.4 o 2.4.5, utilice el siguiente comando para cargar los módulos de eventos:

   ```bash
   composer require magento/commerce-eventing=^1.0 --no-update
   ```

   Commerce 2.4.6 y versiones posteriores cargan estos módulos automáticamente.

1. Actualice las dependencias del proyecto.

   ```bash
   composer update
   ```

1. Habilite los nuevos módulos:

   ```bash
   bin/magento module:enable Magento_AdobeCommerceEventsClient Magento_AdobeCommerceEventsGenerator Magento_AdobeIoEventsClient Magento_AdobeCommerceOutOfProcessExtensibility
   ```

Finalice la instalación en función del tipo de implementación: Adobe Commerce en infraestructura en la nube o local.

#### Infraestructura en la nube

En Adobe Commerce en la infraestructura de la nube, habilite la variable global `ENABLE_EVENTING` en `.magento.env.yaml`. [Más información](https://experienceleague.adobe.com/docs/commerce-cloud-service/user-guide/configure/env/stage/variables-global.html#enable_eventing).

```bash
stage:
   global:
      ENABLE_EVENTING: true
```

Transfiera y envíe los archivos actualizados al entorno de Cloud. Cuando finalice la implementación, habilite el envío de eventos con el siguiente comando:

```bash
bin/magento config:set adobe_io_events/eventing/enabled 1
```

#### On-Premise

En entornos locales, debe habilitar manualmente la generación de código y los eventos de Adobe Commerce:

```bash
bin/magento events:generate:module
bin/magento module:enable Magento_AdobeCommerceEvents
bin/magento setup:upgrade
bin/magento setup:di:compile
bin/magento config:set adobe_io_events/eventing/enabled 1
```

### Instalación de la extensión B2B

Para los comerciantes B2B, instale la siguiente extensión para incluir [datos de evento de lista de solicitudes](events.md#b2b-events).

Descargue la extensión `magento/experience-platform-connector-b2b` ejecutando lo siguiente desde la línea de comandos:

```bash
composer require magento/experience-platform-connector-b2b
```

### Instale la extensión HIPAA de los servicios de datos

Para los comerciantes del sector sanitario, instale la siguiente extensión para asegurarse de que los datos de eventos del back office son compatibles con HIPAA.

Descargue la extensión `magento/module-data-services-hipaa` ejecutando lo siguiente desde la línea de comandos:

```bash
composer require magento/module-data-services-hipaa
```

## Actualizar la extensión [!DNL Data Connection] {#update}

Para actualizar la extensión [!DNL Data Connection], ejecute lo siguiente desde la línea de comandos:

```bash
composer update magento/experience-platform-connector --with-dependencies
```

O, para los comerciantes B2B:

```bash
composer update magento/experience-platform-connector-b2b --with-dependencies
```

Para actualizar a una versión principal como de 2.0.0 a 3.0.0, edite el archivo raíz [!DNL Composer] `.json` del proyecto de la siguiente manera:

1. Abra el archivo raíz `composer.json` y busque `magento/experience-platform-connector`.

1. En la sección `require`, actualice el número de versión de la siguiente manera:

   ```json
   "require": {
      ...
      "magento/experience-platform-connector": "^3.0",
      ...
    }
   ```

1. **Guardar** `composer.json`. A continuación, ejecute lo siguiente desde la línea de comandos:

   ```bash
   composer update magento/experience-platform-connector --with-dependencies
   ```

   O, para los comerciantes B2B:

   ```bash
   composer update magento/experience-platform-connector-b2b --with-dependencies
   ```

## Desinstalar la extensión [!DNL Data Connection] {#uninstall}

Para desinstalar la extensión [!DNL Data Connection], consulte [desinstalar módulos](https://experienceleague.adobe.com/docs/commerce-operations/installation-guide/tutorials/uninstall-modules.html).
