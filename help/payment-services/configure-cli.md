---
title: Configuración de la línea de comandos
description: Después de la instalación, puede configurar  [!DNL Payment Services] usando la Interfaz de línea de comandos (CLI).
role: Admin, Developer
level: Intermediate
exl-id: 265ab1be-fe52-41f3-85cb-addbc2ddfb17
feature: Payments, Checkout, Configuration, Integration, Paas
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."
source-git-commit: 5271668c99e7a66fbe857cd3ae26edfa54211621
workflow-type: tm+mt
source-wordcount: '621'
ht-degree: 0%

---

# Configuración de la línea de comandos

Después de instalar [!DNL Payment Services], puede configurarlo fácilmente desde [el inicio](payments-home.md) o a través de la interfaz de línea de comandos (CLI).

## Configuración de exportación de datos

[!DNL Payment Services] combina datos de pedidos exportados desde [!DNL Magento Open Source] y [!DNL Adobe Commerce] con datos de pagos agregados de proveedores de pagos para crear informes útiles. La extensión [!DNL Payment Services] usa indizadores para recopilar de manera eficaz todos los datos necesarios para los informes.

Para obtener más información sobre los datos utilizados en los informes de [!DNL Payment Services], consulte [Informe del estado de pago del pedido](order-payment-status.md#data-used-in-the-report).

### Configurar cron en [!DNL Magento Open Source]

Si desea usar un modo de índice `BY SCHEDULE` en [!DNL Magento Open Source], debe configurar cron. Consulte [Configurar y ejecutar cron](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs).

### Establecer indizadores

Los datos de pedidos se exportan y se mantienen en el servicio de pagos, utilizando uno de los dos modos de índice: `ON SAVE` (predeterminado) o `BY SCHEDULE` (recomendado).

Los siguientes índices son para [!DNL Payment Services]:

| Código | Nombre | Descripción |
|    ---    |  ---  |  ---  |
| `sales_order_data_exporter` | Fuente de pedidos de ventas | Crea un índice de datos de pedidos |
| `sales_order_status_data_exporter` | Fuente de estados de pedidos de ventas | Crea un índice de datos de estados de pedidos de ventas |
| `store_data_exporter` | Almacena fuente | Crea un índice de datos almacenados |

Para cambiar el modo de índice de los tres indexadores, ejecute:

```bash
bin/magento indexer:set-mode schedule sales_order_data_exporter sales_order_status_data_exporter store_data_exporter
```

>[!TIP]
>
>Si no especifica ningún indizador en el comando, todos los indizadores se actualizarán con el mismo valor. Si desea cambiar un indizador específico, debe enumerarlo en el comando.

Para obtener más información sobre cómo cambiar manualmente el modo de un indizador, consulte [Configurar indizadores](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers#configure-indexers){target="_blank"} en la documentación para desarrolladores. Para obtener información sobre cómo cambiarlo en Admin, consulte [Administración de índices](https://experienceleague.adobe.com/en/docs/commerce-admin/systems/tools/index-management#change-the-index-mode){target="_blank"} en la guía del usuario principal.

### Reindexación manual de datos

Puede reindexar los datos manualmente, en lugar de esperar a que se produzca automáticamente. Consulte [Reindex](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers#reindex){target="_blank"} en [Administrar los indizadores](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers){target="_blank"} para obtener más información.

Cuando se establece el modo `BY SCHEDULE`, el sistema rastrea las entidades cambiadas y el trabajo cron actualiza el índice para ellas en función de una programación establecida. Consulte [Ejecutar cron desde la línea de comandos](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs#config-cli-cron-group-run) en [Configuración y ejecución de cron](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/configure-cron-jobs)) para obtener información sobre cómo almacenar en déclencheur manualmente la indexación mediante trabajos cron.

### Enviar datos reindexados al servicio de pago

Una vez indizados los datos, se enviarán automáticamente a [!DNL Payment Services]. También puede almacenar en déclencheur manualmente el proceso de envío de datos indexados con este comando:

```bash
bin/magento saas:resync --feed [feedName]
```

Utilice las siguientes opciones de comando:

| Comando | Descripción |
|  ---  |  ---  |
| `bin/magento saas:resync --feed [feedName]` | Realiza una reindexación de la fuente especificada y la envía al servicio correspondiente |
| `bin/magento saas:resync --no-reindex` | Omite la indexación y envía datos sin sincronizar desde los índices |

El parámetro `--feed` le permite especificar qué fuente desea enviar:

| Fuente | Descripción |
|  ---  |  ---  |
| `paymentServicesOrdersProduction` | Fuente de pedidos en modo de producción |
| `paymentServicesOrdersSandbox` | Fuente de pedidos en modo de espacio aislado |
| `paymentServicesOrderStatusesProduction` | Estados de pedidos en modo de producción |
| `paymentServicesOrderStatusesSandbox` | Estados de pedidos en modo de espacio aislado |
| `paymentServicesStoresProduction` | Tiendas en modo de producción |
| `paymentServicesStoresSandbox` | Tiendas en modo de espacio aislado |

Todos los datos necesarios para los informes se envían a [!DNL Payment Services] automáticamente si cron está configurado e instalado. También puede almacenar en déclencheur manualmente el proceso de envío de datos cron a [!DNL Payment Services].

```bash
bin/magento cron:run --group payment_services_data_export
```

Para obtener más información sobre la reindexación y los indexadores, consulte el tema [Administrar los indexadores](https://experienceleague.adobe.com/en/docs/commerce-operations/configuration-guide/cli/manage-indexers) en la documentación para desarrolladores.

## Configurar el ámbito mediante CLI

[!DNL Payment Services] permite que los comerciantes usen [varias cuentas de PayPal](settings.md#use-multiple-paypal-accounts). Ahora puede cambiar los ámbitos de estas cuentas a través de CLI.

Para establecer el ámbito en el nivel `website`, ejecute:

```bash
bin/magento config:set payment/payment_services/mba_scoping_level website
```

Para establecer el ámbito en el nivel `store`, utilice:

```bash
bin/magento config:set payment/payment_services/mba_scoping_level store
```

>[!TIP]
>
> Si desea cambiar el ámbito a nivel de tienda, póngase en contacto con su representante de ventas [!DNL Payment Services].

Una vez cambiado el ámbito, vacíe la caché para mostrar los cambios:

```bash
bin/magento cache:clean:payment_services_merchant_scopes
```

## Configuración del procesamiento de L2/L3

[!DNL Payment Services] puede procesar datos de nivel 2 y nivel 3 de transacciones de pago con tarjeta para proporcionar información adicional a los comerciantes.

>[!WARNING]
>
> La integración con el procesamiento de nivel 2 y nivel 3 con PayPal solo está disponible para comerciantes estadounidenses. Consulta [procesamiento de pagos](https://developer.paypal.com/docs/checkout/advanced/processing/){target=_blank} en la documentación para desarrolladores de PayPal para obtener más información.

Si desea usar datos de procesamiento L2/L3 para [!DNL Payment Services], o si tiene alguna pregunta, póngase en contacto con el administrador de cuentas de [!DNL Payment Services].

Para obtener información acerca del procesamiento de L2 y L3 usado en [!DNL Payment Services], vea [Procesamiento de nivel 2 y nivel 3](levels-card-payment-transactions.md).
