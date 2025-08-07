---
title: Añadir atributos personalizados a los perfiles
description: Obtenga información sobre cómo añadir atributos personalizados a perfiles de clientes.
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: 5489910382edc70eea5d7c0ca94da41c653b577d
workflow-type: tm+mt
source-wordcount: '457'
ht-degree: 0%

---


# Añadir atributos personalizados a los perfiles

Los atributos de perfil personalizados le permiten mejorar la identificación del perfil del cliente en Experience Platform mediante el uso de identificadores adicionales además de los predeterminados `customerId` y `emailId`. Estos identificadores adicionales permiten una coincidencia de clientes más precisa y una integración de datos mejorada entre la plataforma de Commerce y Experience Platform.

>[!NOTE]
>
>Aprenda a [agregar atributos personalizados](custom-attributes.md) a los pedidos.

## Ventajas

- Utilice varios identificadores para mejorar la coincidencia de clientes.
- Asigne campos personalizados a atributos de identidad en función de sus necesidades comerciales.
- Reduzca los perfiles duplicados y mejore la precisión de los datos de los clientes.
- Habilite experiencias de cliente más específicas.

## Requisitos previos

Antes de implementar atributos de identidad personalizados, asegúrese de lo siguiente:

- [Instalación de la extensión de conexión de datos](install.md)
- [Conectar con Adobe Experience Platform](connect-data.md)
- [Envío de datos de perfil de cliente](connect-data.md#send-customer-profile-data)

## Paso 1: Configuración del esquema de Experience Platform

1. Inicie sesión en Adobe Experience Platform y seleccione su esquema de Commerce.
1. [Agregar campos de identidad personalizados](https://experienceleague.adobe.com/en/docs/experience-platform/xdm/ui/resources/schemas?lang=en#custom-fields-for-standard-groups) en el nivel raíz:
   - `hashedPID` (cadena): hash de identidad principal
   - `hashedSID` (cadena): hash de identidad secundario
   - `primaryID` (cadena): nombre del campo de identidad principal
   - `secondaryID` (cadena): nombre del campo de identidad secundario

![Configuración de esquema de Experience Platform](./assets/aep-schema-configuration.png)

>[!NOTE]
>
>Puede personalizar los nombres de campo exactos en función de sus necesidades. El ejemplo usa `hashedPID` y `hashedSID` como campos de identidad.

## Paso 2: Crear clases de procesador

Cree las siguientes clases de procesador PHP en su módulo personalizado:

### AddressCustomHashedId, clase

Este procesador almacena en hash `parent_id` y `entity_id` las direcciones de los clientes.

```php
<?php declare(strict_types=1);

namespace Magento\AepCustomerCustomAttributes\Event;
use Magento\AdobeCommerceEventsClient\Event\Event;
use Magento\AdobeCommerceEventsClient\Event\Processor\EventDataProcessorInterface;

class AddressCustomHashedId implements EventDataProcessorInterface
{
    public function process(Event $event, array $eventData): array
    {
        $pid = $eventData['parent_id'] ?? '';
        $sid = $eventData['entity_id'] ?? '';

        $eventData['profileAttributes']['hashedPID'] = hash('sha256', (string)$pid);
        $eventData['profileAttributes']['hashedSID'] = hash('sha256', (string)$sid);
        return $eventData;
    }
}
```

### AddressCustomId, clase

Este procesador establece los nombres de campo de ID principal y secundario para los eventos de dirección.

```php
<?php declare(strict_types=1);

namespace Magento\AepCustomerCustomAttributes\Event;
use Magento\AdobeCommerceEventsClient\Event\Event;
use Magento\AdobeCommerceEventsClient\Event\Processor\EventDataProcessorInterface;

class AddressCustomId implements EventDataProcessorInterface
{
    public function process(Event $event, array $eventData): array
    {
        $eventData['profileAttributes']['primaryID'] = 'hashedPID';
        $eventData['profileAttributes']['secondaryID'] = 'hashedSID';

        // Ensure both IDs are present, otherwise, Commerce will default primary to customerId and secondary to emailId
        if (empty($eventData['profileAttributes']['primaryID']) || empty($eventData['profileAttributes']['secondaryID'])) {
            $eventData['profileAttributes']['primaryID'] = $eventData['customerId'] ?? '';
            $eventData['profileAttributes']['secondaryID'] = $eventData['email'] ?? '';
        }

        return $eventData;
    }
}
```

### Clase CustomHashId

Este procesador almacena en hash `entity_id` y `email` los perfiles de los clientes.

```php
<?php declare(strict_types=1);

namespace Magento\AepCustomerCustomAttributes\Event;
use Magento\AdobeCommerceEventsClient\Event\Event;
use Magento\AdobeCommerceEventsClient\Event\Processor\EventDataProcessorInterface;

class CustomHashedId implements EventDataProcessorInterface
{
    public function process(Event $event, array $eventData): array
    {
        $pid = $eventData['entity_id'] ?? '';
        $sid = $eventData['email'] ?? '';

        $eventData['profileAttributes']['hashedPID'] = hash('sha256', (string)$pid);
        $eventData['profileAttributes']['hashedSID'] = hash('sha256', (string)$sid);
        return $eventData;
    }
}
```

### clase CustomId

Este procesador establece los nombres de campo de ID principal y secundario para los eventos de perfil.

```php
<?php declare(strict_types=1);

namespace Magento\AepCustomerCustomAttributes\Event;
use Magento\AdobeCommerceEventsClient\Event\Event;
use Magento\AdobeCommerceEventsClient\Event\Processor\EventDataProcessorInterface;

class CustomId implements EventDataProcessorInterface
{
    public function process(Event $event, array $eventData): array
    {
        $eventData['profileAttributes']['primaryID'] = 'hashedPID';
        $eventData['profileAttributes']['secondaryID'] = 'hashedSID';

        // Ensure both IDs are present, otherwise, Commerce will default primary to customerId and secondary to emailId
        if (empty($eventData['profileAttributes']['primaryID']) || empty($eventData['profileAttributes']['secondaryID'])) {
            $eventData['profileAttributes']['primaryID'] = $eventData['customerId'] ?? '';
            $eventData['profileAttributes']['secondaryID'] = $eventData['email'] ?? '';
        }

        return $eventData;
    }
}
```

>[!NOTE]
>Asegúrese de que `primaryID` y `secondaryID` se envíen en los datos de evento. Si falta alguna de las dos, el valor predeterminado de Commerce es:
>
>- primaryID = customerId
>- secondaryID = emailId

>[!BEGINSHADEBOX]

Después de completar estos dos pasos:

- El esquema de Commerce en Experience Platform puede introducir correctamente identidades personalizadas para los datos de evento de perfil.
- Las clases de procesador del código PHP de Commerce recopilan información de identificación personalizada a partir de eventos de perfil.

Ahora, cualquier dato de evento de perfil enviado desde Commerce contiene su información de identificación personalizada.

>[!ENDSHADEBOX]

## Ejemplos de formato de datos

Los siguientes ejemplos muestran la estructura JSON esperada para los atributos de identidad personalizados tanto en atributos de perfil como en formatos completos de datos de perfil del cliente.

### Formato de atributos de perfil

```json
{
  "profileAttributes": {
    "hashedPID": "d80eae6e96d148b3b2abbbc6760077b66c4ea071f847dab573d507a32c4d99a5",
    "hashedSID": "fa7359e288ce3104bd4317a4fb75f08c4a5feec472de2e415b8260fb3567ebe6",
    "warehousecode": "1256",
    "method": "ina2354",
    "source": "commerce",
    "primaryID": "hashedPID",
    "secondaryID": "hashedSID"
  }
}
```

### Estructura completa del perfil del cliente

```json
{
  "id": 137,
  "entity_id": "137",
  "created_at": "2025-02-10 20:10:30",
  "updated_at": "2022-02-10 20:10:31",
  "email": "customer@example.com",
  "firstname": "John",
  "lastname": "Doe",
  "dob": "2007-10-01 00:00:00",
  "profileAttributes": {
    "hashedPID": "d80eae6e96d148b3b2abbbc6760077b66c4ea071f847dab573d507a32c4d99a5",
    "hashedSID": "fa7359e288ce3104bd4317a4fb75f08c4a5feec472de2e415b8260fb3567ebe6",
    "primaryID": "137",
    "secondaryID": "customer@example.com"
  },
  "_metadata": {
    "commerceEdition": "Adobe Commerce",
    "commerceVersion": "2.4.6",
    "eventsClientVersion": "1.9.0",
    "storeId": "1",
    "websiteId": "1",
    "storeGroupId": "1",
    "websiteCode": "base",
    "storeCode": "default",
    "storeViewCode": "main_website_store"
  }
}
```

## Resolución de problemas

### Falta primaryID o secondaryID

- **Síntoma:** Los datos predeterminados son customerId/emailId en lugar de valores personalizados.
- **Solución:** Asegúrese de que `primaryID` y `secondaryID` estén establecidos en el objeto `profileAttributes`.

### Valores hash no válidos

- **Síntoma:** Los valores hash están vacíos o tienen un formato incorrecto.
- **Solución:** Compruebe que los campos de origen (`parent_id`, `entity_id`, `email`) contienen datos válidos antes del hash.

### Procesadores que no se ejecutan

- **Síntoma:** Los atributos personalizados no aparecen en los datos de evento.
- **Solución:** Compruebe que los procesadores están registrados correctamente en `events.xml` y que el módulo está habilitado.

### Discordancia de esquema de Experience Platform

- **Síntoma:** Los datos no aparecen en Experience Platform ni en errores de validación de esquema.
- **Solución:** Asegúrese de que el esquema de Experience Platform incluye los campos de identidad personalizados con los tipos de datos correctos.
