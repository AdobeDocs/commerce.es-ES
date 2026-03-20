---
title: Activación de correo electrónico mediante REST
description: Aprenda a almacenar en déclencheur los correos electrónicos transaccionales bajo demanda mediante la API de REST especificando un ID de plantilla, un correo electrónico de destinatario y variables de plantilla para  [!DNL Adobe Commerce as a Cloud Service].
role: Admin
level: Experienced
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
source-git-commit: 9661e368f7a0dc85edcd3e52a67ae2a98355d8b5
workflow-type: tm+mt
source-wordcount: '523'
ht-degree: 0%

---

# Activación de correo electrónico mediante la API de REST

Anteriormente, solo se podía enviar correos electrónicos cuando se activaban eventos, como durante el registro de clientes o la compra de pedidos. En [!DNL Adobe Commerce as a Cloud Service], puede enviar correos electrónicos a través de la API de REST bajo demanda especificando un ID de plantilla, un correo electrónico de destinatario y variables de plantilla.

>[!NOTE]
>
>Actualmente, solo se pueden enviar las plantillas personalizadas recién creadas. No se admiten las plantillas predefinidas y del sistema.

El extremo `V1/custom-email/send` permite que **sistemas de terceros**, como integraciones y servicios externos, envíen correos electrónicos bajo demanda especificando:

- **ID de plantilla** - ID de plantilla de correo electrónico.
- **Correo electrónico del destinatario** - La dirección de correo electrónico de destino para esta solicitud.
- **Variables**: (Opcional) pares de clave-valor definidos personalizados para insertarlos en la plantilla, como `customer_name` o `order_id`.

>[!NOTE]
>
>El correo electrónico se envía sincrónicamente usando el ámbito de almacenamiento actual y la dirección de correo electrónico predeterminada **De** o la dirección de correo electrónico definida para las plantillas.

## Contrato REST

En la siguiente sección se explica cómo enviar correos electrónicos transaccionales bajo demanda mediante la API de REST.

### Extremo

- **URL** - `POST /rest/V1/custom-email/send`
- **Autorización** - Solo se admite la **autorización IMS de servicio a servicio**. El llamador debe tener acceso al recurso **Enviar correo electrónico personalizado mediante API** (`Magento_CustomEmailSend::send_custom_email`). Consulte [Autenticación REST](https://developer.adobe.com/commerce/webapi/rest/authentication/) para obtener más información.
- **Uso asincrónico** (recomendado): aunque este extremo se implementa sincrónicamente, recomendamos llamarlo mediante la **API REST asincrónica** para que un consumidor ponga en cola y procese la solicitud, evitando así conexiones HTTP de larga duración. En [!DNL Adobe Commerce as a Cloud Service], puede utilizar la ruta con `/async` después de `V1`, por ejemplo: `POST https://<server>.api.commerce.adobe.com/<tenant-id>/V1/async/custom-email/send`.

  Consulte [Puntos finales web asíncronos (SaaS)](https://developer.adobe.com/commerce/webapi/rest/use-rest/asynchronous-web-endpoints/) para obtener más información.

### Cuerpo de solicitud

- **templateId** (entero, obligatorio): ID de plantilla de correo electrónico según se define en el Administrador en [!UICONTROL **Marketing**] > [!UICONTROL _Comunicaciones_] > [!UICONTROL **Plantillas de correo electrónico**].

- **recipientEmail** (cadena, obligatorio): La dirección de correo electrónico de destino. Debe tener un formato de correo electrónico válido. Los valores que faltan o están vacíos almacenan en déclencheur un error de validación.
- **variables** (objeto, opcional): asignación clave-valor insertada en la plantilla como `UnstructuredArray`.

  Si no utiliza variables, pase un objeto vacío u ómitelo. En el cuerpo y el asunto de la plantilla de correo electrónico, utilice la sintaxis de la variable para hacer referencia a una variable, por ejemplo `var order_id`. El asunto también admite las mismas variables y sintaxis personalizadas descritas en [Escenarios de plantilla admitidos](#supported-template-scenarios).

### Respuesta de éxito (HTTP 200)

La API devuelve HTTP 200 cuando el envío se realiza correctamente.

### Respuestas de error

- **HTTP 400 - Error de validación**

  La integración debe proporcionar un(a) `templateId` y un(a) `recipientEmail` válidos para cada solicitud.

   - `"message": "Invalid recipient email format"` - dirección de destinatario no válida o mal formada
   - `"message": "Recipient email is required."` - falta o vacío `recipientEmail`
   - `"message": "Template ID must be a positive integer."` - falta, cero o no válido `templateId`

- **HTTP 404 - Plantilla no encontrada**

  Ejemplo: `"message": "Email template with ID \"999\" does not exist."`

## Escenarios de plantilla admitidos

Las siguientes características de la plantilla son compatibles con **cuerpo del correo electrónico** y con **asunto de la plantilla**:

>[!NOTE]
>
>El asunto de la plantilla también admite variables personalizadas. Utilice `var variableName` y otras sintaxis como se describe en la siguiente sección.

- **Incluir directiva** - para incluir otras plantillas de diseño, como un encabezado de correo electrónico.

  ```javascript
  {{template config_path="design/email/header_template"}}
  ```

- **Variables simples** - use `var variableName`, por ejemplo `var order_id` o `var g`.

  ```javascript
  {{var order.test}}
  {{var g}}
  {{var order_id}}
  ```

- **Notación anidada/con punto**: para las claves anidadas pasadas en la solicitud `variables`, en las traducciones se usan nombres con prefijo de dólar, como `$order_data.customer_name`, `$order.increment_id` o `$order_data.frontend_status_label`.

  ```javascript
  {{trans "%name," name=$order_data.customer_name}}
  {{trans "Your order #%increment_id has been updated with a status of **%order_status**." increment_id=$order.increment_id order_status=$order_data.frontend_status_label |raw}}
  ```

- **Traducción (trans)**: texto parametrizado, traducciones multilínea con varios marcadores de posición y etiquetas HTML.

  ```javascript
  {{trans "%name," name=$order_data.customer_name}}
  {{trans "Your order #%increment_id has been updated with a status of **%order_status**." increment_id=$order.increment_id order_status=$order_data.frontend_status_label |raw}}
  ```

- **Salida en bruto**: use el filtro `|raw` cuando el contenido traducido o variable contenga HTML (por ejemplo, `<strong>` o `<a>`).

  ```javascript
  {{trans "Your order #%increment_id has been updated with a status of **%order_status**." increment_id=$order.increment_id order_status=$order_data.frontend_status_label |raw}}
  ```

- **ayudante de URL**: para URL de tienda dentro de traducciones.

  ```javascript
  {{trans 'You can check the status of your order by [logging into your account](%account_url).' account_url=$this.getUrl($store,'customer/account/',[_nosid:1]) |raw}}
  ```
