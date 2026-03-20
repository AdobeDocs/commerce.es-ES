---
title: Puntos finales REST de cuenta de tarjeta regalo
description: Aprenda a utilizar las API de REST de cuenta de tarjeta regalo para crear, actualizar, eliminar y consultar cuentas de tarjeta regalo mediante programación en  [!DNL Adobe Commerce as a Cloud Service].
role: Admin, Developer
level: Experienced
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
source-git-commit: 160180d9d779514f6faee3c7de46531ebf191c7d
workflow-type: tm+mt
source-wordcount: '807'
ht-degree: 0%

---

# API de cuenta de tarjeta regalo

{{accs-sandbox-experimental}}

Los extremos REST de la cuenta de tarjetas de regalo proporcionan administración programática de las cuentas de tarjetas de regalo en el nivel de cuenta, no en el nivel de carrito o presupuesto. Utilice esta API para crear, recuperar, actualizar y eliminar cuentas de tarjetas regalo, o para aprovisionar cuentas de tarjetas regalo de forma masiva a través del punto final de importación JSON.

Estos extremos están diseñados para:

* Administradores que administran programas de tarjetas regalo
* Integraciones de terceros que aprovisionan tarjetas regalo de sistemas externos como ERP, CRM y plataformas de marketing
* Flujos de trabajo automatizados para la creación masiva de tarjetas regalo

## Autenticación

Todos los extremos requieren un token de administrador o de portador de integración. El token debe estar asociado con un rol que incluya el recurso de lista de control de acceso (ACL) `Magento_GiftCardAccount::giftcardaccount`.

Para las operaciones de importación masiva, la función también debe incluir el recurso ACL `Magento_ImportExport::import_api`.

## Contexto del sitio web y la tienda

Los valores de vista de sitio web y tienda se resuelven desde los encabezados de solicitud HTTP, no desde el cuerpo de la solicitud. Pase uno de los siguientes encabezados con cada solicitud:

* `Store: <store_view_code>`
* `Magento-Website-Code: <website_code>`

La API resuelve el sitio web automáticamente a partir de estos encabezados. No incluya `website_id` en la carga de la solicitud REST.

>[!NOTE]
>
>El punto final de la importación masiva es una excepción. Dado que la importación funciona de forma masiva y puede dirigirse a sitios web específicos, cada fila de la carga útil de importación requiere un valor `website_id` explícito.

## Referencia de API de REST

La API expone las siguientes operaciones en `/V1/giftcardaccounts`, todas ellas protegidas por el recurso ACL `Magento_GiftCardAccount::giftcardaccount`:

| Método | URL | Descripción |
|--------|-----|-------------|
| PUBLICAR | `/rest/V1/giftcardaccounts` | Crear una cuenta de tarjeta regalo |
| GET | `/rest/V1/giftcardaccounts` | Enumerar cuentas (admite searchCriteria) |
| GET | `/rest/V1/giftcardaccounts/:id` | Obtener cuenta por identificador |
| GET | `/rest/V1/giftcardaccounts/code/:code` | Obtener cuenta por código |
| PUT | `/rest/V1/giftcardaccounts/:id` | Actualizar cuenta (combinar semántica) |
| DELETE | `/rest/V1/giftcardaccounts/:id` | Eliminar cuenta |

### Referencia de campo

| Campo | Tipo | Valores válidos | Crear REST | Importar |
|---|---|---|---|---|
| `code` | cadena | Máximo de 255 caracteres | Requerido | Requerido |
| `balance` | float | >= 0 | Requerido | Requerido |
| `status` | int | `0` (deshabilitado), `1` (habilitado) | Opcional, el valor predeterminado es `1` | Opcional, el valor predeterminado es `1` |
| `state` | int | `0` (disponible), `1` (usado), `2` (canjeado), `3` (caducado) | Opcional, el valor predeterminado es `0` | Opcional, el valor predeterminado es `0` |
| `is_redeemable` | int | `0` o `1` | Opcional, el valor predeterminado es `1` | Opcional, el valor predeterminado es `1` |
| `date_expires` | cadena | `YYYY-MM-DD` o nulo | Opcional | Opcional |
| `date_created` | cadena | `YYYY-MM-DD` | Ajuste automático | Opcional, se establece automáticamente si se omite |
| `website_id` | int | ID de sitio web válido | No aceptado (resuelto automáticamente desde los encabezados) | Requerido |

### Crear una cuenta de tarjeta regalo

Crea una nueva cuenta de tarjeta regalo con detección de código duplicado.

| Elemento | Valor |
|---|---|
| **Método** | `POST` |
| **URL** | `/V1/giftcardaccounts` |

**Cuerpo de solicitud:**

```json
{
  "giftcardAccount": {
    "code": "GIFT-1234-ABCD",
    "balance": 100.00,
    "status": 1,
    "state": 0,
    "is_redeemable": 1,
    "date_expires": "2027-12-31"
  }
}
```

**Respuesta (200):**

```json
{
  "account_id": 42,
  "code": "GIFT-1234-ABCD",
  "balance": 100,
  "status": 1,
  "state": 0,
  "is_redeemable": 1,
  "date_expires": "2027-12-31",
  "date_created": "2026-03-12"
}
```

### Recuperar una cuenta de tarjeta regalo por identificador

| Elemento | Valor |
|---|---|
| **Método** | `GET` |
| **URL** | `/V1/giftcardaccounts/:id` |

**Respuesta (200):**

Devuelve un solo objeto de cuenta de tarjeta regalo.

### Recuperar una cuenta de tarjeta regalo por código

| Elemento | Valor |
|---|---|
| **Método** | `GET` |
| **URL** | `/V1/giftcardaccounts/code/:code` |

>[!IMPORTANT]
>
>Si el código de una tarjeta regalo es meramente numérico (por ejemplo, `12345`), una solicitud a `/V1/giftcardaccounts/12345` coincide con la ruta de identificación, no con la ruta de código. Utilice siempre `/V1/giftcardaccounts/code/12345` para búsquedas basadas en código cuando el código pueda ser numérico.

**Respuesta (200):**

Devuelve un solo objeto de cuenta de tarjeta regalo.

### Enumerar las cuentas de tarjetas regalo con criterios de búsqueda

| Elemento | Valor |
|---|---|
| **Método** | `GET` |
| **URL** | `/V1/giftcardaccounts` |

Pase los criterios de búsqueda como parámetros de consulta. El siguiente ejemplo devuelve cuentas de tarjetas regalo donde `status` es igual a `1` (habilitado):

```text
GET /V1/giftcardaccounts?searchCriteria[filterGroups][0][filters][0][field]=status&searchCriteria[filterGroups][0][filters][0][value]=1&searchCriteria[pageSize]=10&searchCriteria[currentPage]=1
```

**Respuesta (200):**

```json
{
  "items": [
    {
      "account_id": 42,
      "code": "GIFT-1234-ABCD",
      "balance": 100,
      "status": 1,
      "state": 0,
      "is_redeemable": 1,
      "date_expires": "2027-12-31",
      "date_created": "2026-03-12"
    }
  ],
  "search_criteria": { ... },
  "total_count": 1
}
```

### Actualizar una cuenta de tarjeta regalo

Actualiza una cuenta de tarjeta de regalo existente mediante la semántica de combinación. Solo se aplican los campos no nulos de la solicitud. El campo `code` es inmutable. Pasar un código diferente devuelve un error de validación.

| Elemento | Valor |
|---|---|
| **Método** | `PUT` |
| **URL** | `/V1/giftcardaccounts/:id` |

**Cuerpo de solicitud:**

```json
{
  "giftcardAccount": {
    "balance": 75.00,
    "status": 1
  }
}
```

**Respuesta (200):**

Devuelve el objeto de cuenta de tarjeta regalo actualizado.

### Eliminar una cuenta de tarjeta regalo

| Elemento | Valor |
|---|---|
| **Método** | `DELETE` |
| **URL** | `/V1/giftcardaccounts/:id` |

**Respuesta (200):**

```json
true
```

## Importación masiva mediante JSON

Las cuentas de tarjetas de regalo se pueden aprovisionar en lotes usando `POST /V1/import/json` con el tipo de entidad `giftcardaccount`. Este extremo requiere el recurso de la Lista de control de acceso (ACL) `Magento_ImportJsonApi::import_api` además de la ACL de la cuenta de la tarjeta regalo.

### Comportamientos admitidos

| Comportamiento | Descripción |
|---|---|
| `append` | Crea nuevas cuentas de tarjetas regalo. Si ya existe un código, esa fila falla y la importación continúa con las filas restantes. |
| `replace` | Actualiza e inserta las cuentas de tarjetas regalo por código. Crea la cuenta si el código no existe y la reemplaza si existe. |
| `delete` | Elimina las cuentas de tarjetas regalo por código. |

### Solicitar ejemplo

```json
{
  "source": {
    "entity": "giftcardaccount",
    "behavior": "append",
    "validation_strategy": "validation-stop-on-errors",
    "allowed_error_count": "10",
    "items": [
      {
        "code": "BULK-001",
        "balance": 50.00,
        "website_id": 1,
        "status": 1,
        "state": 0,
        "is_redeemable": 1,
        "date_expires": "2027-06-30"
      },
      {
        "code": "BULK-002",
        "balance": 25.00,
        "website_id": 1
      }
    ]
  }
}
```

### Importar detalles de comportamiento

* Cada fila de la carga de importación requiere un `website_id` explícito, a diferencia de los extremos REST que deducen el sitio web de los encabezados de solicitud.
* Cada fila se valida de forma independiente. Las filas no válidas producen errores por fila sin afectar a las filas válidas del mismo lote.
* Los códigos duplicados dentro del mismo lote se detectan y se registran como errores por fila en lugar de provocar una reversión de la transacción.
* La importación escribe directamente en la base de datos para el rendimiento y omite el ciclo de vida guardado del modelo del proveedor. Las entradas del historial de cambios de saldo no se crean durante la importación.
* Las operaciones de creación de REST rechazan fechas de caducidad pasadas. La importación acepta fechas de caducidad pasadas por diseño para admitir la migración de datos históricos.

## Control de errores

La API devuelve códigos de estado HTTP estándar:

| Código de estado | Condición |
|---|---|
| `400` | Error de validación. Faltan campos obligatorios, valores no válidos o fecha de caducidad pasada en la creación de REST. |
| `401` | Falta el token de portador o no es válido. |
| `403` | El token carece del recurso ACL necesario. |
| `404` | Cuenta de tarjeta de regalo no encontrada. |
| `409` | Código de tarjeta regalo duplicado. |

La validación de entrada abarca los campos obligatorios, los intervalos de valores (el estado debe ser `0` o `1`, el estado debe ser `0`-`3`, el saldo debe ser no negativo), el formato de fecha y la seguridad de tipo. Los valores no numéricos de los campos numéricos se rechazan.
