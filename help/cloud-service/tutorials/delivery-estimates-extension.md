---
title: Tutorial de extensión Delivery Estimates
description: Obtenga información sobre cómo crear una extensión de estimaciones de fecha de envío para Adobe Commerce as a Cloud Service mediante App Builder, Edge Delivery Services y herramientas de desarrollo asistido por IA.
solution: Commerce
feature: App Builder, Cloud
feature-set: Commerce
role: Developer
level: Intermediate
type: Tutorial
hide: true
hidefromtoc: true
source-git-commit: 3fc8982613df7b1155cdfb08ac4b56de6d1ce4f6
workflow-type: tm+mt
source-wordcount: '3334'
ht-degree: 0%

---

# Tutorial de extensión de estimaciones de envío

Este tutorial lo guiará a través de la creación de una extensión de estimaciones de fecha de entrega para [!DNL Adobe Commerce as a Cloud Service] mediante [!DNL Adobe App Builder], [!DNL Edge Delivery Services] y herramientas de desarrollo asistido por IA. La extensión obtiene las estimaciones de tiempo de envío y fecha de envío de una API externa y las muestra en la tienda.

Se construyen dos partes:

- **Extensión de App Builder**: una acción de back-end para front-end (BFF) que ajusta una API de estimación de envío externa, un webhook que enriquece los métodos de envío con las fechas de envío al cerrar la compra y una página de configuración de la IU de administración para administrar la configuración sin tener que volver a implementarla.
- **Integración de tienda**: las estimaciones de fecha de entrega se muestran en la página de detalles del producto (PDP), la página del carro de compras y la página de cierre de compra usando [!DNL Edge Delivery Services] componentes desplegables y un módulo de cliente compartido.

>[!NOTE]
>
>Los agentes de la IA no son deterministas. Los mensajes, preguntas y resultados de este tutorial son ejemplos. Su agente puede presentar diferentes preguntas, requisitos o propuestas de arquitectura. Utilice los ejemplos de este tutorial para dirigir al agente hacia un resultado similar.

Antes de empezar, complete [requisitos previos](./tutorial-prerequisites.md). Este tutorial usa el **kit de inicio de cierre de compra**. Compruebe que ya lo ha clonado y que ha completado los pasos de configuración descritos en la página de requisitos previos.

## Comprobar requisitos previos

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

Además, compruebe lo siguiente:

- Tiene una instancia de [!DNL Adobe Commerce as a Cloud Service] con datos del producto. Ver [instancias del servicio Commerce Cloud](https://experienceleague.adobe.com/es/docs/commerce/cloud-service/overview){target="_blank"}.
- Tiene un proyecto de tienda conectado a la instancia [!DNL Commerce]. Si no tienes una, sigue los pasos de [Crear una tienda](https://experienceleague.adobe.com/developer/commerce/storefront/get-started/create-storefront/?lang=es){target="_blank"}.
- La CLI `aem` está instalada:

  ```bash
  npm install -g @adobe/aem-cli
  ```

- Tiene una **cuenta de comprador**; un cliente registrado en [!DNL Commerce] con una dirección de envío predeterminada guardada. Las estimaciones de entrega de las páginas de PDP y del carro de compras solo se muestran a los compradores que iniciaron sesión. El cierre de compra muestra estimaciones para todos los compradores, independientemente del estado de autenticación.

>[!IMPORTANT]
>
>Este tutorial usa el **kit de inicio de cierre de compra** (no el kit de inicio de integración). El kit de inicio de cierre de compra proporciona extensibilidad basada en ganchos web para pagos, envíos, impuestos y eventos. Asegúrese de arrancar desde el kit de Pago y envío.

## Configuración de la API de estimación de entrega ficticia

La extensión llama a una API de estimación de envíos externa para obtener las estimaciones de fecha y hora de envío. Para este tutorial, utiliza una API ficticia para poder ejecutar el flujo completo sin una cuenta de operador real. Hay dos opciones disponibles:

- **Opción A: flujo de trabajo de Pipedream**: nivel gratuito, configuración rápida, pero con límites de invocación mensuales.
- **Opción B: acción del tiempo de ejecución de App Builder** — Sin dependencia externa, creada durante los pasos de desarrollo del servidor.

>[!TIP]
>
>Durante el desarrollo, puede comenzar con Pipedream (Opción A) y cambiar a una acción Runtime (Opción B) si alcanza la cuota de invocación de nivel libre. Ambas opciones implementan el mismo contrato de API.

### Especificación de API

La API ficticia acepta una solicitud POST y devuelve estimaciones de fecha de entrega con el transportista, los días de tránsito, el tiempo de corte y una mejor estimación.

**Cuerpo de solicitud** (todos los campos son opcionales para el simulacro):

```json
{
  "origin": { "country_code": "US", "postal_code": "90210", "city": "Beverly Hills" },
  "destination": { "country_code": "US", "postal_code": "10001", "city": "New York" },
  "ship_date": "2026-03-10",
  "carriers": ["standard", "express"],
  "service_levels": ["standard", "express"]
}
```

**Respuesta (200 OK):**

```json
{
  "estimates": [
    {
      "carrier_code": "standard",
      "service_code": "ground",
      "delivery_date": "2026-03-14",
      "safe_delivery_date": "2026-03-15",
      "transit_days": 4,
      "cutoff_datetime_utc": "2026-03-10T17:00:00.000Z"
    },
    {
      "carrier_code": "express",
      "service_code": "2day",
      "delivery_date": "2026-03-12",
      "safe_delivery_date": "2026-03-12",
      "transit_days": 2,
      "cutoff_datetime_utc": "2026-03-10T12:00:00.000Z"
    }
  ],
  "best_estimation": { "carrier_code": "express", "delivery_date": "2026-03-12", "transit_days": 2 }
}
```

**Respuestas de error:** 401 (falta clave de API o no válida), 400 (formato de `ship_date` no válido), 503 (tiempo de inactividad simulado).

### Configurar el simulacro

>[!BEGINTABS]

>[!TAB Flujo de trabajo Pipedream]

La opción Pipedream utiliza la autenticación de token de portador y acepta una solicitud POST a la URL de déclencheur del flujo de trabajo.

| Elemento | Descripción |
|------|-------------|
| URL básica | La dirección URL completa del déclencheur del flujo de trabajo de Pipedream (por ejemplo `https://<id>.m.pipedream.net`) |
| Auth | `Authorization: Bearer <API_KEY>` |
| Método | PUBLICAR |

{style="table-layout:auto"}

**Crear el flujo de trabajo:**

1. Cree un nuevo flujo de trabajo en [Pipedream](https://pipedream.com){target="_blank"} (**[!UICONTROL Workflows]** > **[!UICONTROL New Workflow]**).

1. Agregue un déclencheur **HTTP / Webhook** configurado para POST. Pipedream asigna una URL de webhook.

1. Agregue un paso **Ejecutar código de Node.js** y pegue el siguiente código de controlador:

   ```javascript
   const DEFAULT_CARRIERS = [
     { carrier_code: "standard", service_code: "ground", transit_days: 4 },
     { carrier_code: "express", service_code: "2day", transit_days: 2 },
     { carrier_code: "priority", service_code: "overnight", transit_days: 1 },
   ];
   
   const ISO_DATE = /^\d{4}-\d{2}-\d{2}$/;
   
   function parseShipDate(shipDate) {
     if (shipDate == null || typeof shipDate !== "string") return null;
     if (!ISO_DATE.test(shipDate)) return null;
     const d = new Date(shipDate + "T12:00:00.000Z");
     if (Number.isNaN(d.getTime())) return null;
     return shipDate;
   }
   
   function addBusinessDays(isoDate, days) {
     const d = new Date(isoDate + "T12:00:00.000Z");
     let added = 0;
     while (added < days) {
       d.setUTCDate(d.getUTCDate() + 1);
       const dow = d.getUTCDay();
       if (dow !== 0 && dow !== 6) added += 1;
     }
     return d.toISOString().slice(0, 10);
   }
   
   function cutoffUtc(isoDate, hour = 17) {
     return `${isoDate}T${String(hour).padStart(2, "0")}:00:00.000Z`;
   }
   
   function getBearerToken(headers) {
     const auth = headers?.Authorization ?? headers?.authorization ?? "";
     if (typeof auth !== "string" || !auth.startsWith("Bearer ")) return null;
     return auth.slice(7).trim() || null;
   }
   
   function handleDeliveryEstimate(body) {
     const shipDate = parseShipDate(body?.ship_date);
     const baseDate = shipDate ?? new Date().toISOString().slice(0, 10);
     let carriers = DEFAULT_CARRIERS;
     if (Array.isArray(body?.carriers) && body.carriers.length > 0) {
       const set = new Set(body.carriers.map((c) => String(c).toLowerCase()));
       carriers = DEFAULT_CARRIERS.filter((c) => set.has(c.carrier_code.toLowerCase()));
     }
     if (Array.isArray(body?.service_levels) && body.service_levels.length > 0) {
       const set = new Set(body.service_levels.map((s) => String(s).toLowerCase()));
       carriers = carriers.filter(
         (c) => set.has(c.service_code.toLowerCase()) || set.has(c.carrier_code.toLowerCase())
       );
     }
     if (carriers.length === 0) {
       return { status: 200, body: { estimates: [], best_estimation: null } };
     }
     const estimates = carriers.map((c) => {
       const delivery_date = addBusinessDays(baseDate, c.transit_days);
       const safe_delivery_date = addBusinessDays(baseDate, c.transit_days + 1);
       const cutoff_datetime_utc = cutoffUtc(baseDate, 17 - c.transit_days);
       return {
         carrier_code: c.carrier_code,
         service_code: c.service_code,
         delivery_date,
         safe_delivery_date,
         transit_days: c.transit_days,
         cutoff_datetime_utc,
       };
     });
     return { status: 200, body: { estimates, best_estimation: estimates[0] } };
   }
   
   export default defineComponent({
     async run({ steps, $ }) {
       const event = steps.trigger?.event ?? steps.trigger ?? {};
       const body = event.body ?? {};
       const headers = event.headers ?? {};
       const auth = getBearerToken(headers);
       const expectedKey =
         (typeof process.env.MOCK_API_KEY === "string" && process.env.MOCK_API_KEY.trim()) || null;
       if (expectedKey && (!auth || auth !== expectedKey)) {
         await $.respond({
           immediate: true,
           status: 401,
           headers: { "Content-Type": "application/json" },
           body: { error: "unauthorized", message: "Missing or invalid API key." },
         });
         return;
       }
       if (body?.ship_date != null && !parseShipDate(body.ship_date)) {
         await $.respond({
           immediate: true,
           status: 400,
           headers: { "Content-Type": "application/json" },
           body: { error: "bad_request", message: "Invalid ship_date; use YYYY-MM-DD." },
         });
         return;
       }
       const { status, body: responseBody } = handleDeliveryEstimate(body);
       await $.respond({
         immediate: true,
         status,
         headers: { "Content-Type": "application/json" },
         body: responseBody,
       });
     },
   });
   ```

1. (Opcional) Agregue una variable de entorno `MOCK_API_KEY` en la configuración del flujo de trabajo para aplicar la autenticación de token de portador. Si no se configura, se acepta cualquier solicitud.

1. Implemente el flujo de trabajo.

   El punto final es la URL de déclencheur del gancho web.

**Probar la simulación:**

```bash
curl -X POST \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer mock-api-key" \
  -d '{"destination": {"country_code": "US", "postal_code": "10001"}}' \
  "https://<your-endpoint>.m.pipedream.net"
```

>[!TAB Acción de tiempo de ejecución de App Builder]

La opción de acción App Builder en tiempo de ejecución implementa la acción simular como en tiempo de ejecución dentro del mismo proyecto [!DNL App Builder]. Este método no tiene dependencia externa ni cuotas de invocación.

Solicitar al agente que cree la acción de simulación:

```shell-session
Add a new runtime action to this project that implements the API in @docs/PIPEDREAM_API_SPEC.md
- Add it to a separate package
- Use the code in docs/pipedream as inspiration
```

El agente crea `actions/mock-delivery-api/index.js` con el mismo contrato de API que la opción de Pipedream. Después del despliegue, el punto final es:

```shell-session
https://<namespace>.adobeioruntime.net/api/v1/web/mock-delivery-api/delivery-estimate
```

Se validó la autenticación con una variable de entorno `MOCK_API_KEY` en `.env`.

>[!ENDTABS]

## Desarrollo de extensiones

Esta sección le guiará a través del desarrollo del back-end [!DNL App Builder] para la extensión de estimaciones de entrega. El backend de proporciona tres acciones:

| Acción | Tipo | Finalidad |
|--------|------|---------|
| `delivery-estimates` | Acción web independiente | BFF para tienda — PDP y carrito llaman a esto para las fechas de entrega |
| `shipping-methods` | Acción de webhook | Enriquece las tarifas de envío con fechas de entrega en `additional_data` al momento de pagar |
| `delivery-estimates-config` | Acción de back-end de administrador | CRUD para la configuración almacenada en `aio-lib-state` |

{style="table-layout:auto"}

1. En la configuración de MCP de los agentes de codificación, compruebe que el conjunto de herramientas `commerce-extensibility` esté habilitado sin errores.

   Por ejemplo, en Cursor, vaya a **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**.

   Si hay errores, active o desactive el conjunto de herramientas.

   >[!NOTE]
   >
   >Cuando trabaje con herramientas de desarrollo asistido por IA, espere variaciones naturales en el código y las respuestas generadas por el agente.
   >Si encuentra algún problema con su código, pídale al agente que le ayude a depurarlo.

1. Si se ha añadido documentación al contexto del cursor, desactívela.

   Vaya a **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Indexing & Docs]** y elimine cualquier documentación enumerada.

### Paso 1: Proporcione la solicitud inicial

Asigne al agente la especificación de API externa para el contexto y solicite que comience. Indicar al agente que se detenga y haga preguntas le ayuda a dirigir la implementación desde el principio.

Introduzca el siguiente mensaje en la ventana de chat del agente:

```shell-session
I want to build an Adobe App Builder extension that extends the checkout with shipping date and time estimates taken from an external API described in @docs/API_SPEC.md.
Delivery dates for a product will be shown in the product details page and on the cart page.
Implement this feature by using the skills in this workspace for backend code, and a separate workspace with storefront skills. For this extension, focus on the backend skills and create an API_SPEC to hand work over to the storefront skills.

STOP and ask me clarifying questions about the requirements before you do any work.
```

>[!TIP]
>
>La referencia al archivo de especificaciones de API externo (`@docs/API_SPEC.md`) en el mensaje proporciona al agente un contexto concreto sobre el contrato de API de terceros. El agente utiliza esto para diseñar la acción de BFF, el cliente HTTP compartido y los campos de configuración de la IU de administración. Indicar al agente que se DETENGA y haga preguntas déclencheur el flujo de trabajo guiado y le ayuda a dirigir la implementación desde el principio.

### Paso 2: Responda las preguntas del agente

El agente regresa con una serie de preguntas aclaratorias que abarcan temas como el entorno de destino (PaaS vs SaaS), ámbito (acción independiente de BFF, enriquecimiento de ganchos web, o ambos), origen de la dirección de origen, estrategia de almacenamiento en caché y preferencia de prueba. El siguiente ejemplo muestra preguntas y respuestas típicas. Su agente puede hacer diferentes preguntas, pero los temas generalmente son los mismos.

**Ejemplo de preguntas del agente:**

1. **Entorno de destino**: ¿está creando para PaaS (local) o SaaS (Adobe Commerce as a Cloud Service)?
2. **Ámbito**: ¿Debe ser una acción independiente de BFF (la tienda la llama directamente), enriquecimiento de gancho web (ampliar los métodos de envío al cierre de compra) o ambas?
3. **Configurabilidad de la administración**: ¿Deben configurarse opciones como la URL de la API, la clave de la API y la dirección de origen a través de la administración de Commerce o almacenarse en `.env`?
4. **Dirección de origen** — ¿De dónde proviene la dirección de origen (almacén) del envío? ¿Debe ser una configuración estática o resolverse dinámicamente?
5. **Almacenamiento en caché**: ¿deben almacenarse en caché las estimaciones de envío en el servidor para reducir las llamadas a la API externa? Si es así, ¿qué TTL?

**Respuestas de ejemplo:**

```shell-session
Clarifications:
1. Let's build for SaaS
2. Let's do this:
(A) Can the PDP/cart call the 3rd party API directly — or are there any benefits of wrapping this call with a runtime action?
(B) Let's use the shipping-methods webhook
3. Let's use a Single-page application (SPA) that uses the Admin UI SDK to integrate with the admin. Since we are adding this config screen, let's make anything else that makes sense configurable to avoid redeployments when changing settings
4. Static configuration — origin address should be configurable in the Admin UI (e.g. warehouse address)
5. Yes, cache on the server side; suggest a TTL (e.g. 30 minutes) and make it configurable in the Admin UI
```

>[!TIP]
>
>Preguntar al agente si la tienda debe llamar a la API de terceros directamente o pasar por una acción de tiempo de ejecución déclencheur un útil análisis de arquitectura. El agente explica las ventajas del patrón BFF (back-end-for-Frontend): la clave de API permanece en el lado del servidor, CORS se gestiona, el almacenamiento en caché está centralizado y se obtiene la abstracción del proveedor. Si se solicita la configuración de la IU de administración, el agente almacenará toda la configuración en `aio-lib-state` en lugar de `.env`, lo que eliminará las reimplementaciones al cambiar la configuración.

>[!NOTE]
>
>Su agente puede hacer diferentes preguntas. Utilice estas respuestas como guía para dirigir al agente hacia el mismo resultado funcional: una acción de mejor precio para las llamadas de tienda, un webhook de métodos de envío para enriquecer el cierre de compra y una página de configuración de la IU de administración que almacene la configuración en `aio-lib-state`.

### Paso 3: Revisar los requisitos y la arquitectura

El agente genera requisitos y documentos de arquitectura para que los revise. Compruebe que los requisitos coinciden con las respuestas proporcionadas y que la arquitectura cubre lo siguiente:

- Una **acción de BFF** (`delivery-estimates`): una acción web independiente que la tienda llama desde páginas de carrito y PDP. Lee la configuración de `aio-lib-state`, llama a la API de estimación de envío externa y devuelve estimaciones con formato.
- Una **acción de gancho web** (`shipping-methods`): enriquece las tarifas de envío con fechas de entrega en `additional_data` durante el cierre de compra. Utiliza el método webhook `plugin.out_of_process_shipping_methods.api.shipping_rate_repository.get_rates`.
- Una **acción de configuración del administrador** (`delivery-estimates-config`): CRUD para la configuración (URL de API, clave de API, dirección de origen, operadores, TTL de caché) almacenada en `aio-lib-state`.
- **Bibliotecas compartidas**: Un cliente HTTP para la API externa y un módulo de configuración para leer y escribir `aio-lib-state`.

>[!NOTE]
>
>Los agentes de IA son no deterministas y sus comportamientos difieren según el modelo y el IDE. Puede obtener un conjunto diferente de preguntas que producen un conjunto diferente de requisitos y arquitectura. Si es así, intente dirigir el agente en una dirección tal que la implementación coincida estrechamente con lo que se presenta en este tutorial antes de continuar.

### Paso 4: Selección de un plan de implementación

El agente le da la opción de crear un plan de implementación detallado o completar una implementación directa.

- Si desea un plan revisable que se pueda ejecutar por fases con más control, seleccione la primera opción.
- Si desea que el agente realice la implementación completa con una intervención mínima, seleccione la segunda opción.

### Paso 5: Limpieza e implementación

Una vez que el agente completa la implementación, procede a la limpieza. Dado que solo el dominio de envío está en uso, el agente elimina los andamios que no se utilizan:

- Acciones de pago y configuración (`validate-payment/`, `filter-payment/`, `payment-methods.yaml`)
- Acciones y configuración de impuestos (`collect-taxes/`, `collect-adjustment-taxes/`, `tax-integrations.yaml`)
- Acciones de eventos y configuración (`commerce-events/`, `3rd-party-events/`, `events.config.yaml`)
- Andamiaje genérico (`generic/`)
- Componentes de SPA de la IU de administración de otros dominios (por ejemplo, páginas relacionadas con impuestos y enlaces)
- Scripts, archivos de prueba y variables de entorno no utilizados

>[!TIP]
>
>Pida al agente que también compruebe el SPA de la IU de administración para ver si hay restos de otros dominios. La página Clases de Impuestos y sus ganchos pueden seguir presentes desde el andamiaje del kit de inicio y deben eliminarse.

Después de la limpieza, implemente siguiendo estos pasos **en este orden**:

```bash
# 1. Copy env template and fill in credentials.
cp env.dist .env

# 2. Select your App Builder workspace.
aio app use --merge

# 3. Sync OAuth credentials from workspace.
npm run sync-oauth-credentials

# 4. Deploy the extension.
aio app deploy

# 5. Register shipping carriers in Commerce.
npm run create-shipping-carriers
```

>[!IMPORTANT]
>
>No omita ni vuelva a ordenar los pasos. Los pasos del 1 al 3 son requisitos previos para la implementación. El comando `aio app deploy` produce un error si no se han configurado credenciales.

### Paso 6: Configurar el webhook y la IU de administración

Después del despliegue, configure el webhook de envío. El agente puede crear un script para suscribirse mediante programación:

```bash
npm run subscribe-webhook
```

Este comando se suscribe al webhook de envío con la siguiente configuración:

| Campo | Valor |
|-------|-------|
| Método Webhook | `plugin.out_of_process_shipping_methods.api.shipping_rate_repository.get_rates` |
| Tipo de webhook | `after` |
| Requerido | Opcional (permite el envío alternativo predeterminado) |
| Tiempo de espera | 5000 ms |

{style="table-layout:auto"}

>[!NOTE]
>
>Para SaaS, el nombre del método webhook descarta `magento.` de la ruta. El nombre del gancho web para SaaS es `plugin.magento.out_of_process_shipping_methods...`, mientras que el nombre del gancho web para SaaS es `plugin.out_of_process_shipping_methods...`.

A continuación, configure la IU de administración:

1. Habilite la **IU de administración SDK** (**[!UICONTROL Stores]** > **[!UICONTROL Settings]** > **[!UICONTROL Configuration]** > **[!UICONTROL Adobe Services]** > **[!UICONTROL Admin UI SDK]** > **[!UICONTROL Enable]** > **[!UICONTROL Yes]**).

1. Configure las extensiones seleccionando su área de trabajo y extensión [!DNL App Builder].

1. Haga clic en **[!UICONTROL Refresh registrations]**.

1. Vaya a **[!UICONTROL Apps]** > **[!UICONTROL Delivery Estimates]** en la barra lateral de [!DNL Admin].

1. Complete la configuración habilitando la función y especificando la configuración necesaria, incluida la URL de la API y la clave de la API, la dirección de origen, los operadores predeterminados, el TTL de la caché y las asignaciones del código de operador.

### Paso 7: Prueba de la extensión

Prueba de la acción BFF de estimaciones de entrega directamente:

```bash
curl -s -X POST \
  -H "Content-Type: application/json" \
  -d '{"destination": {"country_code": "US", "postal_code": "10001"}}' \
  "https://<your-runtime-url>/api/v1/web/commerce-checkout-starter-kit/delivery-estimates" | jq .
```

La respuesta debe ser similar a:

```json
{
  "estimates": [
    {
      "carrier": "standard",
      "service_level": "ground",
      "delivery_date": "2026-03-12",
      "safe_delivery_date": "2026-03-13",
      "transit_days": 4,
      "cutoff_datetime_utc": "2026-03-06T18:00:00Z"
    },
    {
      "carrier": "express",
      "service_level": "2day",
      "delivery_date": "2026-03-10",
      "safe_delivery_date": "2026-03-10",
      "transit_days": 2,
      "cutoff_datetime_utc": "2026-03-06T20:00:00Z"
    }
  ],
  "best_estimation": {
    "carrier": "express",
    "delivery_date": "2026-03-10",
    "transit_days": 2
  }
}
```

### Creación del contrato de servicio

Ahora que el servidor ha finalizado, pídale al agente que cree un contrato de servicio para el trabajo de la tienda:

```shell-session
Produce a spec called STOREFRONT_API_SPEC that I can use in the storefront workspace with the corresponding agent. Also give me a prompt that I could use in that workspace.
```

El agente genera `docs/STOREFRONT_API_SPEC.md` con el contrato de extremo de BFF completo (formato de solicitud y respuesta, cargas útiles de ejemplo, control de errores) y un aviso listo para usar para el espacio de trabajo de la tienda.

Copie este archivo en el proyecto de tienda antes de iniciar los pasos de desarrollo de tienda.

>[!TIP]
>
>Hacer que el agente genere un contrato de servicio **y** un aviso para el otro espacio de trabajo garantiza un traspaso limpio entre los equipos back-end y de tienda (o agentes). El agente de tienda puede empezar a trabajar inmediatamente sin necesidad de hacer preguntas sobre la API.

## Conectar con la tienda

Esta sección lo guía a través de la implementación de la parte de tienda de la extensión de estimaciones de entrega mediante [!DNL Edge Delivery Services] y las herramientas de desarrollo asistido por IA. Las estimaciones de fecha de entrega se agregan a la PDP, la página del carro y la página de cierre de compra.

>[!NOTE]
>
>Las indicaciones proporcionadas son puntos de partida. Aunque puede utilizarlas sin modificaciones, considere la posibilidad de mantener una conversación natural con el agente.
>
>Al trabajar con herramientas de desarrollo asistido por IA, siempre hay variaciones naturales en el código y las respuestas generadas por el agente.
>
>Si encuentra algún problema con su código, pídale al agente que le ayude a depurarlo.

### Requisitos previos de Storefront

Antes de iniciar la integración de tienda, comprueba que tienes lo siguiente:

- Un proyecto de tienda conectado a su instancia [!DNL Commerce]
- Herramientas de IA de tienda de Commerce [instaladas con CLI](./tutorial-prerequisites.md#install-the-storefront-ai-tools)
- El archivo `STOREFRONT_API_SPEC.md` se copió en la carpeta `docs/` del proyecto de tienda

### Paso 1: Validar el entorno

Abra el archivo `config.json` y compruebe que los valores de `commerce-core-endpoint` y `commerce-endpoint` apuntan al extremo de GraphQL [!DNL Adobe Commerce as a Cloud Service].

```json
"commerce-core-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
"commerce-endpoint": "https://na1-sandbox.api.commerce.adobe.com/<your-instance-id>/graphql",
```

### Paso 2: Proporcione la solicitud inicial

Con el contrato de servicio ya en el proyecto, pídale al agente que implemente la integración de tienda. Utilice el modo **Plan** si está disponible en su agente, para evitar que el agente continúe sin un plan.

```shell-session
I need to implement delivery date estimates on the storefront for an Adobe Commerce (SaaS) store using Edge Delivery Services with storefront drop-ins. The backend is already built and deployed as an App Builder extension.

The full integration contract is in the `docs/STOREFRONT_API_SPEC.md` file— please read it first. It covers two integration points:

PDP and Cart pages — Call the delivery-estimates BFF action (HTTP POST) to fetch estimates for a destination and display the best delivery date.

Checkout shipping step — Delivery dates are already injected into each shipping method's `additional_data` by a webhook. No API call is needed. Just read `additional_data` from the shipping methods and display the delivery date next to each option.

Requirements:
- Show "Get it by [date]" on PDP using best_estimation.delivery_date
- Show a delivery date range on the cart page using delivery_date / safe_delivery_date
- Show delivery dates next to each shipping method at checkout, reading from additional_data
- Show "Order within X hours" countdown using cutoff_datetime_utc where appropriate
- Cache estimates client-side in sessionStorage to avoid redundant calls
- Never block the purchase flow — if estimates are unavailable, hide the UI silently

STOP and ask me any clarifying questions you have about the requirements before you do any work.
```

>[!TIP]
>
>El mensaje se detalla porque el contrato de API completo ya está disponible en el agente backend. Al hacer referencia a `@docs/STOREFRONT_API_SPEC.md`, el agente conoce la dirección URL de extremo exacta, el formato de solicitud y respuesta y la administración de errores. La lista de requisitos explícitos impide que el agente invente el ámbito. En concreto, la solicitud del modo de planificación déclencheur el flujo de trabajo por fases que le ayuda a dirigir la implementación desde el principio.

### Paso 3: Responder preguntas aclaratorias

El agente vuelve con preguntas sobre el ámbito de autenticación, el método de cierre de compra y el estilo. El siguiente ejemplo muestra preguntas y respuestas típicas.

**Ejemplo de preguntas del agente:**

1. **Usuarios anónimos frente a usuarios que iniciaron sesión**: ¿Deben mostrarse las estimaciones en las páginas de PDP y del carro de compras para todos los compradores o solo para los autenticados?
2. **Método de cierre de compra** — El contenedor desplegable Métodos de envío no expone `additional_data`, por lo que el agente propone dos opciones:
   - **Opción A:** Llame al mejor amigo en las fechas de pago y envío de la inyección de DOM (más simple, coherente con el PDP/carrito)
   - **Opción B:** Ampliar el fragmento de GraphQL de cierre de compra a través de `overrideGQLOperations` para incluir `additional_data`
3. **Estilo**: Emojis frente a tokens de diseño existentes

**Respuestas de ejemplo:**

```shell-session
1. Only for logged-in users — that way we can use the shopper's default shipping address and avoid a zip code input
2. Let's do Option A if feasible
3. Use anything that matches the current styling
```

>[!TIP]
>
>Mostrar estimaciones solo para compradores conectados es una opción pragmática. El agente puede utilizar automáticamente la dirección de envío predeterminada del comprador (a través de GraphQL), por lo que no se necesita introducir ningún código postal. Los compradores anónimos en PDP y Carro de compras necesitarían introducir un código postal, lo que añade fricción. Al cerrar la compra, todos los compradores ven las fechas de entrega porque ya se ha introducido la dirección de envío.

>[!NOTE]
>
>Su agente puede hacer diferentes preguntas. Utilice estas respuestas como guía:
>
>- Mostrar las estimaciones de PDP y del carro de compras solo para los compradores que iniciaron sesión (no se necesita entrada de código postal).
>- Para pagar, use la Opción A (llamada BFF + inyección DOM) por simplicidad.
>- Utilice tokens de diseño existentes para el estilo.

### Paso 4: Revisar los requisitos y la arquitectura

El agente diseña una arquitectura de módulo compartido. Compruebe que cubre:

| Componente | Finalidad |
|-----------|---------|
| `scripts/delivery-estimates.js` | Módulo compartido: cliente BFF, almacenamiento en caché (sessionStorage, TTL de 30 minutos), formato de fecha, lógica de cuenta atrás, búsqueda de direcciones de clientes, asignación de operadores |
| Integración de PDP | Muestra &quot;Consíguelo antes del [fecha]&quot; con una cuenta atrás opcional entre precio y descripción |
| Integración con carrito | Muestra el intervalo de fechas (&quot;Jue, 12 de marzo - Vie, 13 de marzo&quot;) en la columna derecha sobre el resumen del pedido |
| Integración de extracción | Llama a BFF cuando el paso de envío está activo, DOM introduce las fechas de envío a través de `MutationObserver` |

{style="table-layout:auto"}

Decisiones clave de diseño que verificar:

- Todas las llamadas BFF son sin bloqueo: las páginas se procesan primero, las estimaciones aparecen de forma asíncrona.
- Todos los errores son silenciosos: solo `console.debug`, sin errores de cara al comprador.
- `CARRIER_MAP` asigna códigos de operador de Commerce (DPS, Fedex) a códigos de operador de BFF (estándar, rápido).
- El elemento dinámico `import()` mantiene el módulo de envío fuera de la ruta de procesamiento crítica.

>[!NOTE]
>
>Los agentes de IA son no deterministas y sus comportamientos difieren según el modelo y el IDE. Puede obtener un conjunto diferente de preguntas que producen un conjunto diferente de requisitos y arquitectura. Si es así, intente dirigir el agente en una dirección tal que la implementación coincida estrechamente con lo que se presenta en este tutorial antes de continuar.

### Paso 5: Selección de un plan de implementación

El agente le da la opción de crear un plan de implementación detallado o completar una implementación directa.

- Si desea un plan revisable que se pueda ejecutar por fases con más control, seleccione la primera opción.
- Si desea que el agente realice la implementación completa con una intervención mínima, seleccione la segunda opción.

Durante la implementación, el agente crea y modifica los siguientes archivos:

**Nuevo archivo:**

- `scripts/delivery-estimates.js` — Módulo compartido con `fetchDeliveryEstimates()`, `getCustomerShippingAddress()`, `formatDeliveryDate()`, `buildCountdownText()`, `findEstimateForCarrier()`

**Archivos modificados:**

- `blocks/product-details/product-details.js` + `.css` — Div de estimación de envío en la columna derecha, captura asincrónica después del procesamiento principal
- `blocks/commerce-cart/commerce-cart.js` + `.css` — Div de estimación de envío por encima del resumen del pedido
- Inyección de DOM basada en `blocks/commerce-checkout/commerce-checkout.js`, `containers.js`, `.css` — `MutationObserver` para etiquetas de método de envío

Observe el código que se está generando y haga preguntas o redirija el agente según sea necesario.

### Paso 6: Inicio del servidor y prueba

Una vez que el agente haya completado la implementación, inicie el servidor de desarrollo y pruebe las estimaciones de entrega.

1. Inicie el servidor de desarrollo local:

   ```bash
   npm run start
   ```

1. En un navegador, inicie sesión en su cuenta de comprador.

   Las estimaciones de entrega en PDP y Carro de compras requieren una sesión autenticada con una dirección de envío predeterminada guardada.

1. Vaya a una página de producto y compruebe los siguientes resultados:

   | Página | Resultado esperado | Se requiere autenticación |
   |------|-----------------|---------------|
   | PDP | &quot;Consíguelo antes del jueves 12 de marzo&quot; con cuenta atrás opcional | Sí (solo sesión iniciada) |
   | Carrito | &quot;Entrega estimada: jueves, 12 de marzo - viernes, 13 de marzo&quot; | Sí (solo sesión iniciada) |
   | Finalizar compra | &quot;Envío estimado: jueves, 12 de marzo&quot; por método de envío | No (dirección introducida al cerrar la compra) |

   {style="table-layout:auto"}

>[!NOTE]
>
>Los métodos de envío sin un transportista coincidente (por ejemplo, Tarifa fija) no muestran ninguna estimación. Esto es por diseño — solamente los operadores asignados en `CARRIER_MAP` obtienen fechas de entrega.

Puede realizar pruebas manuales o pedir al agente que utilice sus capacidades de explorador para realizar pruebas:

```shell-session
Run complete browser testing using the following product page 'http://localhost:3000/products/<product-slug>/<sku>'
```

### Paso 7: Limpiar

Después de omitir o completar la prueba, el agente le pedirá que continúe con la limpieza. Tras la confirmación, el agente archiva cualquier artefacto de documentación producido durante la implementación.

## Resolución de problemas

Utilice las siguientes sugerencias si encuentra problemas durante el tutorial.

### Servidor (App Builder)

| Síntoma | Causa | Fix |
|---------|-------|-----|
| La acción de configuración de la IU de administración devuelve `400 Bad Request` con &quot;La solicitud define parámetros no permitidos (propiedades reservadas)&quot; | El vínculo de front-end está enviando `__ow_method` en el cuerpo de la solicitud. OpenWhisk reserva las propiedades con el prefijo `__ow_` y las rechaza cuando la acción tiene `final: true`. | Enviar una propiedad `method` personalizada en lugar de `__ow_method`. La acción back-end lee `params.method` primero y después vuelve a `params.__ow_method` (que Runtime proporciona automáticamente). |
| `aio app deploy` produce el error &quot;maxVersion is required in productDependencies&quot; | La validación de CLI requiere `minVersion` y `maxVersion` en `app.config.yaml` dependencias de producto. | Agregue un valor `maxVersion` a cada entrada `productDependencies` en `app.config.yaml`. |
| Error del comando de implementación | Credenciales no configuradas antes de la implementación. `.env`, la selección del espacio de trabajo y la sincronización con OAuth deben realizarse primero. | Siga el orden correcto: `cp env.dist .env` > `aio app use --merge` > `npm run sync-oauth-credentials` > `aio app deploy`. |

{style="table-layout:auto"}

### Tienda (Edge Delivery Services)

| Síntoma | Causa | Fix |
|---------|-------|-----|
| La estimación de envío de PDP no aparece para los compradores que iniciaron sesión | El bloque PDP no inicializa el complemento `account`, por lo que `getCustomerAddress()` produce un error de forma silenciosa y no se obtiene ninguna estimación. | Use `CORE_FETCH_GRAPHQL.fetchGraphQl()` directamente para consultar las direcciones de los compradores en lugar de depender de la API desplegable de la cuenta. Esto funciona en cualquier página. |
| La PDP sigue sin mostrarse después de la corrección de GraphQL | Se usó un error tipográfico en el nombre del método: `CORE_FETCH_GRAPHQL.fetch()` en lugar de `CORE_FETCH_GRAPHQL.fetchGraphQl()`. | Utilice el nombre de método correcto: `fetchGraphQl` (Q mayúscula, l minúscula). |
| Las fechas de envío de cierre de compra no aparecen en la primera carga | El detector de eventos `checkout/updated` se registró después de que `checkout/initialized` se hubiera activado, por lo que se omitieron los datos iniciales. | Agregue un oyente `checkout/initialized` con `{ eager: true }` para capturar los eventos emitidos antes del registro. Mantener la escucha `checkout/updated` para cambios posteriores. |
| La estimación de envío del carro de compras no aparece | `block.appendChild(fragment)` mueve todos los elementos secundarios fuera del fragmento, por lo que `fragment.querySelector('.cart__delivery-estimate')` devuelve un valor nulo. | Consulte desde `block` en lugar de `fragment` después de la operación de anexar. |
| El envío con tarifa única no muestra ninguna fecha de envío en el cierre de compra | Por diseño: `CARRIER_MAP` solo asigna DPS a standard y Fedex a express. La tarifa plana no tiene un operador correspondiente en la API externa. | No es un error. Para agregar estimaciones para otros operadores, amplíe `CARRIER_MAP` en `scripts/delivery-estimates.js` y configure el operador en la extensión del servidor. |

{style="table-layout:auto"}

### Entorno aislado SaaS de Commerce

| Síntoma | Causa | Fix |
|---------|-------|-----|
| El webhook devuelve `429 Too Many Requests` | El espacio de trabajo [!DNL App Builder] está en modo de depuración, que tiene límites estrictos de velocidad por minuto. [!DNL Commerce] recalcula las tarifas de envío con frecuencia durante el cierre de compra, agotando la cuota. | Implementar en un espacio de trabajo de producción (`aio app use` para cambiar y después `aio app deploy`). Los espacios de trabajo de producción no tienen límites de velocidad de depuración. |
| Advertencia de tiempo de espera de software de webhook (>1000 ms) | La acción del webhook de métodos de envío tardó más tiempo que el tiempo de espera del software de 1000 ms de [!DNL Commerce]. | Habilite el almacenamiento en caché del lado del servidor en `aio-lib-state` de forma más agresiva o aumente el tiempo de espera del gancho web en [!DNL Commerce Admin] (configuración de los ganchos web de Commerce). |

{style="table-layout:auto"}

## Resumen del tutorial

A continuación se muestra un resumen de los temas tratados en este tutorial:

- **Configuración de API simulada:** Creación de una API de estimación de entrega simulada mediante Pipedream o una acción de tiempo de ejecución de [!DNL App Builder].
- **Patrón de BFF:** al crear una acción de back-end para front-end que ajusta la API externa, mantiene las credenciales del lado del servidor y centraliza el almacenamiento en caché.
- **Enriquecimiento de webhook:** Ampliación de los métodos de envío webhook para introducir las fechas de envío en cada opción de envío en el cierre de compra.
- **Configuración de la IU de administración:** Agregar una página de configuración con [!DNL Admin UI SDK] para que los comerciantes puedan administrar la configuración de la API, la dirección de origen y las asignaciones de operadores sin tener que volver a implementarla.
- **Contratos de servicio:** Creación de contratos de API que vinculan extensiones backend e implementaciones de tienda.
- **Integración de tienda:** muestra las estimaciones de envío en PDP (&quot;Obtenerlo por&quot;), carro (intervalo de fechas) y cierre de compra (por método de envío) mediante un módulo de cliente compartido.
- **UX sin bloqueo:** Garantiza que las estimaciones de entrega nunca bloqueen el flujo de compra: las páginas se procesan primero y las estimaciones aparecen de forma asíncrona.

## Pasos siguientes

Utilice las siguientes sugerencias para ampliar el servicio de estimaciones de entregas:

- **Conecta una API de operador real:** Reemplaza el simulacro con una API de envío en vivo como UPS, FedEx o USPS cambiando la URL del servicio y la clave de API en [!DNL Admin UI].
- **Admitir compradores anónimos:** Agregue una entrada de código postal en las páginas de PDP y del carro de compras para que los compradores que no hayan iniciado sesión también puedan ver las estimaciones de entrega.
- **Extender asignaciones de transportistas:** Agregue más códigos de transportistas a `CARRIER_MAP` para mostrar las fechas de entrega de métodos de envío adicionales.
- **Agregar almacenamiento en caché del lado del servidor:** Implemente el almacenamiento en caché de `aio-lib-state` en la acción BFF para reducir las llamadas a la API externa para pares de origen y destino repetidos.
- **Mostrar estimaciones en la confirmación del pedido:** Mostrar la fecha de envío estimada en la página de confirmación del pedido y en los correos electrónicos transaccionales.
