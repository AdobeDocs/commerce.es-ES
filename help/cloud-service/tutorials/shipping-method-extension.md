---
title: Tutorial de extensión de métodos de envío
description: Obtenga información sobre cómo crear una extensión de método de envío configurable para Adobe Commerce as a Cloud Service mediante App Builder, el kit de inicio de cierre de compra y las herramientas de desarrollo asistido por IA.
feature: App Builder, Cloud
role: Developer
level: Intermediate
source-git-commit: e55bc4db196d3d973b981bb2484be950dcd6b7c3
workflow-type: tm+mt
source-wordcount: '1849'
ht-degree: 0%

---

# Tutorial de extensión de métodos de envío

Este tutorial lo guiará a través del proceso de creación de una extensión de método de envío para [!DNL Adobe Commerce as a Cloud Service] mediante [!DNL Adobe App Builder], el [kit de inicio de cierre de compra](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/){target="_blank"} y las herramientas de desarrollo asistido por IA.

La extensión agrega un método de envío configurable al cierre de compra, donde las tarifas provienen de un servicio de tarifas de envío simuladas externo. Los comerciantes configuran la dirección URL del servicio, la clave de API y la dirección de almacén (origen de envío) en la interfaz de usuario de administración, y al cerrar la compra, las tarifas de solicitudes de extensión de ese servicio y muestran las opciones devueltas al cliente.

Antes de empezar, complete [requisitos previos](./tutorial-prerequisites.md).

## Comprobar requisitos previos {#tutorial-verify-prerequisites}

Compruebe que están instalados los siguientes requisitos previos:

```bash
# Check Node.js version (should be 22.x.x)
node --version

# Check npm version (should be 9.0.0 or higher)
npm --version

# Check Git installation
git --version

# Check Bash shell installation
bash --version
```

Si alguno de los comandos anteriores no devuelve los resultados esperados, consulte los [requisitos previos](./tutorial-prerequisites.md) para obtener instrucciones.

## Crear la API de tarifas de envío simuladas

Después de completar [los requisitos previos](./tutorial-prerequisites.md), cree la API de tarifas de envío simuladas, para que tenga la URL del servicio y la clave de API listas cuando configure la extensión en [!DNL Commerce Admin]. La extensión de llama a una API de tarifas de envío externa. Para este tutorial, utiliza una API ficticia que le permite ejecutar el flujo sin una cuenta de operador real. Creará la API de prueba usando [Pipedream](https://pipedream.com) (se requiere cuenta gratuita). La API ficticia utiliza un contrato de solicitud/respuesta similar a las API típicas de tarifas de envío reales, por lo que la conexión de esta extensión a un proveedor real más adelante debería ser sencilla.

Para crear la API ficticia, descargue el [archivo de especificación de API de tasas ficticias](../assets/mock-rates-api-spec.zip), ábralo y agregue el archivo `.md` a su proyecto (por ejemplo, `docs/mock-rates-api-spec.md`).

**Tiempo:** La creación de la API de simulación debería tardar entre **5 y 10 minutos**.

### Creación de un flujo de trabajo y un déclencheur HTTP

1. Vaya a [pipedream.com](https://pipedream.com) y regístrese o inicie sesión.
1. Haga clic en **Nuevo flujo de trabajo** (o **Agregar flujo de trabajo**).
1. Para el déclencheur, seleccione **HTTP / Webhook**.
1. En la configuración de déclencheur, establezca **Respuesta HTTP** en **Devolver una respuesta personalizada de su flujo de trabajo**. Esto permite que el paso Código envíe la respuesta JSON de prueba.
1. Pipedream muestra una **dirección URL de extremo HTTP** única, como `https://123456.m.pipedream.net`.
1. **Copie esta dirección URL** y utilícela como la **URL de servicio** al configurar la extensión en el administrador de Commerce.

   ![Flujo de trabajo Pipedream con déclencheur HTTP/Webhook y URL de punto de conexión visible](../assets/mock-api-trigger.png){width="600" zoomable="yes"}

No necesita configurar **Autorización** en el déclencheur; la API de prueba valida el encabezado `API-Key` en el paso Código.

### Añada el paso Código

1. Haga clic en el icono **+** para agregar un paso.
1. Elija **Ejecutar código de Node.js** (Paso de código).
1. **Reemplazar** el código predeterminado con el siguiente JavaScript.

   ```javascript
   export default defineComponent({
   async run({ steps, $ }) {
      const event = steps.trigger.event;
      const body = event.body ?? {};
      const headers = event.headers ?? {};
      const apiKey = headers["api-key"] ?? body.api_key ?? "";
   
      if (!apiKey || String(apiKey).trim() === "") {
         await $.respond({
         immediate: true,
         status: 401,
         headers: { "Content-Type": "application/json" },
         body: { error: "Missing or invalid API-Key header" },
         });
         return;
      }
   
      const shipment = body.shipment;
      if (!shipment || typeof shipment !== "object") {
         await $.respond({
         immediate: true,
         status: 400,
         headers: { "Content-Type": "application/json" },
         body: { error: "Missing or invalid shipment" },
         });
         return;
      }
   
      const rates = [
         {
         service_code: "mock_standard",
         service_name: "Mock Standard",
         carrier_friendly_name: "Mock Carrier",
         shipping_amount: { amount: 5.99 },
         shipment_cost: 5.99,
         cost: 5.99,
         },
         {
         service_code: "mock_express",
         service_name: "Mock Express",
         carrier_friendly_name: "Mock Carrier",
         shipping_amount: { amount: 12.99 },
         shipment_cost: 12.99,
         cost: 12.99,
         },
      ];
   
      await $.respond({
         immediate: true,
         status: 200,
         headers: { "Content-Type": "application/json" },
         body: { rates },
      });
   },
   });
   ```

1. Haga clic en **Implementar**.

   ![Paso de código de Pipedream con script de tarifas de envío simuladas](../assets/mock-api-code-step.png){width="600" zoomable="yes"}

La simulación devuelve dos opciones de tasa (Estándar simulada y Express simulada) para cualquier solicitud válida que incluya un encabezado `API-Key` no vacío y un objeto `shipment`. Configurará la clave de API en [!DNL Commerce Admin] más adelante en este tutorial. También especificará la dirección URL del flujo de trabajo de Pipedream en la misma pantalla de configuración, por lo que debe tomar nota de ella.

## Desarrollo de extensiones

Esta sección le guiará a través del desarrollo de una extensión de método de envío para [!DNL Adobe Commerce as a Cloud Service] mediante el kit de inicio de cierre de compra [y las herramientas de desarrollo asistido por IA.](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/){target="_blank"}

1. Vaya a la configuración de MCP del agente de codificación. Por ejemplo, en Cursor, vaya a **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**. Compruebe que el conjunto de herramientas `commerce-extensibility` esté habilitado sin errores. Si hay errores, active o desactive el conjunto de herramientas.

   ![Configuración del IDE de cursor que muestra el conjunto de herramientas de extensibilidad comercial MCP habilitado](../assets/cursor-settings-shipping.png){width="600" zoomable="yes"}

   >[!NOTE]
   >
   >Cuando trabaje con herramientas de desarrollo asistido por IA, espere variaciones naturales en el código y las respuestas generadas por el agente.
   >
   >Si tiene algún problema con el código, siempre puede pedir al agente que le ayude a depurarlo.

1. Si se ha añadido documentación al contexto del cursor, desactívela. Vaya a [!UICONTROL **Cursor**] > [!UICONTROL **Configuración**] > [!UICONTROL **Configuración del cursor**] > [!UICONTROL **Indexación y documentos**] y elimine cualquier documentación enumerada.

   ![Indexación de cursor y configuración de documentos con lista de documentación vacía](../assets/disable-documentation.png){width="600" zoomable="yes"}

1. Proporcione al agente acceso a la especificación de API de tasas de prueba, para que pueda implementar el cliente correctamente. Si aún no lo ha hecho, descargue el [archivo de especificación de API de tasas de prueba](../assets/mock-rates-api-spec.zip), ábralo y agregue el archivo `.md` a su proyecto (por ejemplo, `docs/mock-rates-api-spec.md`) y, a continuación, haga referencia a ese archivo en su solicitud.

1. Generar la extensión del método de envío:

   - En la ventana de chat del agente, seleccione el modo **Plan**, si está disponible. Esto evita que el agente continúe sin un plan.
   - Introduzca la siguiente solicitud:

   ```shell-session
   Build an Adobe Commerce extension that adds a shipping method at checkout. The rates come from an external mock shipping rates service: the merchant configures the service's URL and API key in Admin, and at checkout the extension asks that service for rates and shows the returned options to the customer.
   
   External service (mock shipping rates API):
   - The service endpoint URL is configurable by the merchant (for example https://123456.m.pipedream.net).
   - The API is specified in ./docs/mock-rates-api-spec.md.
   
   The merchant must be able to configure the following in the Adobe Commerce Admin UI. Use the Adobe Commerce Admin UI SDK (or equivalent App Builder extensibility options for the Admin) to add a configuration screen where the merchant can set:
   - The service URL (where the extension sends rate requests).
   - An API key the service expects (any non-empty value for the mock). The API key is sensitive data: it must be stored securely and must never appear in logs, error messages, or in the UI in full (e.g. mask in the UI).
   - The warehouse (ship-from) address: name, phone, street, city, state, postal code, country. This is the origin used when requesting rates.
   ```

   >[!NOTE]
   >
   >Si el agente solicita buscar en la documentación, permita.

   ![Ventana de chat del cursor en el modo Agente con el mensaje de extensión de envío ingresado](../assets/enter-prompt-shipping.png){width="600" zoomable="yes"}

1. Responda las preguntas del agente con precisión para ayudarle a generar el mejor código. Si el agente pregunta qué kit o plantilla usar, diríjalo al [kit de inicio de cierre de compra](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/){target="_blank"} con el dominio de envío y la extensión SDK de la IU de administración para que se implementen tanto el webhook de envío como la pantalla de configuración del comerciante.

   El agente puede crear un archivo de `requirements.md` (o equivalente) que sirva como fuente fiable para la implementación.

1. Revise el archivo `requirements.md` (o equivalente) y compruebe el plan. Si todo parece correcto, indique al agente que pase a la planificación de la arquitectura (o **Fase 2**). Confirme que:

   - Una acción **shipping-methods** (o equivalente) administra el webhook de Commerce y llama a la API de tarifas externas.
   - Una acción **shipping-config** (o equivalente) es compatible con GET (leer configuración, clave de API enmascarada) y SET (guardar URL del servicio, clave de API, dirección de almacén), con una configuración almacenada de forma segura, por ejemplo, en el estado de tiempo de ejecución.
   - La IU de administración incluye una ficha **Envío ficticio** (o similar) con campos para la URL del servicio, la clave de API (contraseña/enmascarada) y la dirección del almacén.

   ![Archivo de requisitos creado por el agente de IA con detalles de implementación de la extensión de envío](../assets/requirements-file-shipping.png){width="600" zoomable="yes"}

1. Revise el plan de arquitectura cuando el agente se lo proporcione.

   ![Plan de implementación del agente de IA para la extensión de tarifas de envío simuladas](../assets/implementation-plan-shipping.png){width="600" zoomable="yes"}

1. Indique al agente que continúe con la generación de código. El agente debe agregar un transportista **mock** a la configuración de los transportistas de envío para permitir que Commerce acepte los métodos devueltos y utilice el método de gancho web `plugin.magento.out_of_process_shipping_methods.api.shipping_rate_repository.get_rates` (tipo de gancho web **after**, obligatorio **Opcional**).

   El agente genera el código necesario y proporciona un resumen detallado de los pasos siguientes (incluyendo la instalación de dependencias, el registro del operador de prueba, la configuración del webhook de Commerce y el despliegue).

   ![Resumen del código generado y la implementación para la extensión de envío](../assets/code-generation-summary-shipping.png){width="600" zoomable="yes"}

   ![Pasos siguientes del agente de IA para instalar, configurar webhook e implementar la extensión de envío](../assets/next-steps-shipping.png){width="600" zoomable="yes"}

### Limpieza antes de la implementación

Antes de implementar, quite el código que no necesite la aplicación. El kit de inicio de pago y envío puede incluir dominios no utilizados (por ejemplo, pagos, impuestos o eventos) y andamios. Haga que el agente los quite y mantenga solamente el envío y las partes de [!DNL Admin UI] mediante un mensaje como:

```shell-session
Proceed with Phase 5 cleanup.
```

El agente genera un informe de limpieza, elimina las acciones, la configuración y los scripts no utilizados y actualiza el proyecto. Complete este paso antes de implementar.

![Informe de limpieza de fase 5 del agente de IA que muestra los componentes eliminados y conservados](../assets/cleanup-report-shipping.png){width="600" zoomable="yes"}

### Implementación de la extensión

1. Después de verificar el código generado, implemente la extensión mediante el siguiente mensaje:

   ```shell-session
   Deploy the app.
   ```

   El agente realiza una evaluación de la preparación previa al despliegue (por ejemplo, comprobando `.env` para las variables `COMMERCE_WEBHOOKS_PUBLIC_KEY`, `COMMERCE_BASE_URL` y OAuth/IMS si se utiliza la IU de administración o la API de Commerce).

   ![Preparación e implementación previas al despliegue del agente de IA para la extensión de envío simulada](../assets/pre-deployment-assessment-shipping.png){width="600" zoomable="yes"}

1. Cuando confíe en los resultados de la evaluación, indique al agente que continúe con el despliegue. El agente utiliza el kit de herramientas de MCP para verificar, crear e implementar automáticamente.

   ![Salida de implementación del kit de herramientas MCP con paquetes implementados y URL de gancho web para la extensión de envío](../assets/deployment-process-shipping.png){width="600" zoomable="yes"}

### Posterior a la implementación

Después de la implementación, complete los siguientes pasos para registrar el operador de prueba, configurar el webhook y [!DNL Admin UI] y comprobar la extensión al cerrar la compra.

1. **Registrar el operador ficticio en Commerce** (ejecutar una vez después de la implementación):

   ```bash
   npm run create-shipping-carriers
   ```

   Asegúrese de que `.env` tenga `COMMERCE_BASE_URL` y credenciales de OAuth/IMS válidas para que el script pueda registrar al operador.

1. **Configurar el webhook de envío en [!DNL Commerce Admin]:**

   - Vaya a **Tiendas** > Configuración > **Configuración** > **Servicios de Adobe** > **Webhooks de Commerce**.
   - Añadir un webhook:
      - **Método webhook:** `plugin.magento.out_of_process_shipping_methods.api.shipping_rate_repository.get_rates`
      - **Tipo de webhook:** **después de**
      - **URL:** la URL de acción web **shipping-methods** implementada (desde la salida de implementación o [!DNL Adobe Developer Console]).
      - **Obligatorio:** **Opcional**: esto permite que el cierre de compra siga funcionando si la API externa no devuelve tasas.

   ![Configuración del webhook de administración de Commerce para las tarifas de envío simuladas](../assets/admin-webhook-shipping.png){width="600" zoomable="yes"}

1. **Configurar la extensión [!DNL Admin UI SDK]:**

   - En [!DNL Commerce Admin], vaya a **Tiendas** > Configuración > **Configuración**.
   - Abra **Servicios de Adobe** > **IU de administración de SDK**.
   - Establezca **Habilitar la IU de administración de SDK** en **Sí** y haga clic en **Guardar configuración** si aún no está habilitada.
   - Haga clic en **Configurar extensiones**, elija el área de trabajo en la que se ha implementado la aplicación y, a continuación, haga clic en **Aplicar**. También puede seleccionar la opción **Personalizado** e introducir el nombre del área de trabajo.
   - Seleccione su aplicación [!DNL App Builder] en la lista y guárdela. Si la aplicación no aparece, haga clic en **Actualizar registros** e inténtelo de nuevo.

   ![IU de administración SDK Configure extensiones modales con espacio de trabajo y selección de extensiones](../assets/admin-ui-configure-extensions.png){width="600" zoomable="yes"}

1. **Configurar el método de envío simulado en la IU del administrador de Adobe Commerce:**
   - Abra **Aplicaciones** y seleccione su aplicación.
   - Abra la ficha **Envío ficticio** (o equivalente).
   - Introduzca la siguiente información:
      - **URL del servicio:** la URL del flujo de trabajo de Pipedream que copió (por ejemplo: `https://123456.m.pipedream.net`).
      - **Clave de API:** cualquier valor no vacío para el simulacro, por ejemplo `tutorial-key`.
      - **Dirección de origen del almacén:** nombre, teléfono, calle, ciudad, estado, código postal, país.
   - Haga clic en **Guardar**. La configuración se almacena en el estado de tiempo de ejecución y la utiliza la acción shipping-methods.

   ![Formulario de configuración de envío simulado con dirección URL de servicio, clave de API y dirección de almacén](../assets/admin-ui-mock-shipping.png){width="600" zoomable="yes"}

1. **Verificar al finalizar la compra:** Agrega un producto al carro de compras, ve al cierre de compra e ingresa una dirección de envío. Debería ver las opciones de envío ficticias, por ejemplo **Mock Standard** y **Mock Express**.

   ![Página de cierre de compra que muestra las opciones de envío simuladas de la API de tarifas externas](../assets/checkout-mock-shipping.png){width="600" zoomable="yes"}

### Resolución de problemas

- **La configuración no se guarda en la interfaz de usuario del administrador:** Si ve &quot;La respuesta no es válida &#39;message/http&#39;&quot; o valores que no se actualizan después de guardar, compruebe los registros de activación en tiempo de ejecución para la acción de configuración mediante un comando similar al siguiente:

  ```bash
  aio app logs --action CustomMenu/shipping-config --limit 20
  ```

  Entre las causas comunes se incluyen la puerta de enlace que espera un formato de respuesta específico (por ejemplo, un cuerpo de cadena y `Content-Type: application/json`) o la biblioteca de estados que requiere valores de cadena; asegúrese de que la acción almacena la configuración como una cadena y la analiza al leerla, y de que la acción métodos de envío utiliza el mismo análisis. Revise el chat o los registros del agente para ver la causa exacta y corregirla.

- **&quot;La respuesta debe contener al menos una operación&quot;** (en los registros de los ganchos web): Commerce requiere que el gancho web de envío devuelva al menos una operación. Pida al agente que se asegure de que la acción métodos de envío nunca devuelva una matriz de operaciones vacía (por ejemplo, devolviendo una tasa de reserva cuando la API externa no devuelve tasas).

- **No hay tarifas de envío en el cierre de compra:** Confirme que la URL y el método del webhook son correctos, que el operador de prueba está registrado (`npm run create-shipping-carriers`) y que la configuración de envío de prueba está establecida en [!DNL Admin UI]. Compruebe los registros de tiempo de ejecución para la acción shipping-methods en busca de errores de validación o API. Asegúrese de que la acción devuelva al menos una operación para que [!DNL Commerce] no muestre &quot;La respuesta debe contener al menos una operación&quot;.

### Resumen del tutorial

A continuación se muestra un resumen de los temas tratados en este tutorial:

- **Requisitos previos y configuración:** Verificación de herramientas y creación de la API de tarifas de envío simuladas.
- **Desarrollo impulsado por el agente:** Uso del conjunto de herramientas de extensibilidad comercial para generar requisitos, un plan de implementación y código para el webhook de envío y la IU de administración.
- **Limpieza de fase 5:** Se eliminarán los dominios y andamios del kit de inicio de cierre de compra no utilizados antes de la implementación.
- **Implementación:** implementación del conjunto de herramientas de MCP y evaluación previa a la implementación.
- **Configuración posterior a la implementación:** Registro del operador de prueba, configuración del webhook [!DNL Commerce], habilitación de la extensión [!DNL Admin UI SDK] y configuración del envío de prueba (URL de servicio, clave de API, almacén) en [!DNL Admin UI].
- **Verificación:** al confirmar las opciones de envío ficticio aparecen en el cierre de compra.

### Pasos siguientes

Para continuar la experimentación con este tutorial, tenga en cuenta lo siguiente:

- Automatice la configuración posterior a la implementación con un vínculo que registre el operador ficticio en [!DNL Commerce] y configure el webhook de envío después de cada implementación.
- Apunte la extensión a una API de tarifas de envío reales cambiando la URL del servicio y la clave de API en [!DNL Admin UI].
- Extienda [!DNL Admin UI] para mostrar el estado del operador o probar la conectividad con el servicio de tarifas.
