---
title: Herramientas de codificación de IA para extensiones
description: Aprenda a utilizar las herramientas de IA para crear extensiones de Commerce App Builder.
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
role: Architect
hide: true
hidefromtoc: true
source-git-commit: 4ee3a547aa292f3e52cf424e368c9fba12d3e4e0
workflow-type: tm+mt
source-wordcount: '1454'
ht-degree: 0%

---

# Herramientas de codificación de IA para extensiones

Al migrar a [!DNL Adobe Commerce as a Cloud Service], puede usar las herramientas de codificación de IA para convertir las extensiones PHP [!DNL Adobe Commerce] existentes en extensiones [!DNL Adobe Developer App Builder]. También se puede usar para crear nuevas extensiones de [!DNL App Builder].

El uso de las herramientas de codificación de IA ofrece las siguientes ventajas:

* **Flujo de trabajo de desarrollo mejorado**: herramientas de desarrollo de Adobe Commerce integradas.
* **Asistencia con tecnología de IA**: generación y depuración de código según el contexto.
* **Características específicas de Commerce**: Herramientas especializadas para el desarrollo de Adobe Commerce App Builder.
* **Flujos de trabajo automatizados**: procesos optimizados de desarrollo e implementación.

## Requisitos previos

* Un agente de codificación, como [Cursor](https://cursor.com/download)&#x200B;(recomendado), [Copiloto de Github](https://github.com/features/copilot), [CLI de Google Gemini](https://github.com/google-gemini/gemini-cli) o [Código Claude](https://www.claude.com/product/claude-code)
* [Node.js](https://nodejs.org/en/download): versión LTS
* Administrador de paquetes: [npm](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) o [yarn](https://classic.yarnpkg.com/lang/en/docs/install/#mac-stable)
* [Git](https://github.com/git-guides/install-git): para la clonación del repositorio y el control de versiones

## Instalación

1. Instale la última [CLI de Adobe I/O](https://github.com/adobe/aio-cli) globalmente:

   ```bash
   npm install -g @adobe/aio-cli
   ```

1. Instale el [complemento Commerce CLI de Adobe I/O](https://github.com/adobe-commerce/aio-cli-plugin-commerce):

   ```bash
   aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce
   ```

1. Clonar el Commerce [kit de inicio de integración](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/create-integration):

   ```bash
   git clone git@github.com:adobe/commerce-integration-starter-kit.git
   ```

1. Vaya al directorio del Starter Kit:

   ```bash
   cd commerce-integration-starter-kit
   ```

1. Instale las herramientas de extensibilidad de Commerce AI ejecutando el comando de configuración interactivo:

   ```bash
   aio commerce extensibility tools-setup
   ```

El proceso de instalación le pedirá las opciones de configuración. Para la ubicación de configuración, elija &quot;Directorio actual&quot; para instalar las herramientas en el espacio de trabajo actual:

```terminal
? Where would you like to setup the tools?
❯ Current directory
  New directory
```

Al seleccionar el agente de codificación, Adobe recomienda seleccionar `Cursor` para obtener la mejor experiencia de desarrollo:

```terminal
? Which coding agent would you like to use?
❯ Cursor
  Copilot
  Gemini CLI
  Claude Code
```

Al seleccionar el administrador de paquetes, Adobe recomienda usar `npm` para mantener la coherencia:

```terminal
? Which package manager would you like to use?
❯ npm
  yarn
```

1. Después de instalar correctamente las herramientas de codificación, el proceso de instalación configura:

   * Integración del servidor MCP para el desarrollo de Adobe Commerce
   * Reglas del IDE de cursor para una experiencia de desarrollo mejorada
   * Flujos de trabajo y herramientas de desarrollo específicas de Commerce

   Los siguientes archivos se añaden al espacio de trabajo:

   * Configuración de MCP: `.cursor/mcp.json`
   * Directorio de reglas: `.cursor/rules/`

## Configuración posterior a la instalación

1. Reinicie el IDE del cursor para cargar las nuevas herramientas y configuración de MCP.

1. Compruebe la instalación confirmando que las reglas están presentes en la carpeta `.cursor/rules/`.

1. Habilite el servidor MCP:

   * Abra la configuración del MCP del cursor con **Cmd+Mayús+P** (macOS) o **Ctrl+Mayús+P** (Windows y Linux).
   * Tipo **Vista: Abrir configuración de MCP**
   * Busque **commerce-extensibility MCP Server** en la lista
   * Active el servidor **ON** para habilitar las herramientas de codificación

1. Comprobar el estado del servidor: el servidor MCP de extensibilidad de Commerce debe aparecer de la siguiente manera:

   ```terminal
   Status: Connected/Active
   Server: commerce-extensibility
   Configuration: Automatically configured via .cursor/mcp.json
   ```

## Mensaje de ejemplo

El siguiente mensaje de ejemplo crea una extensión para enviar notificaciones cuando se realiza un pedido.

```terminal
Implement an Adobe Commerce SaaS extension that will send an ERP notification when a customer places an order. The ERP notification must be sent as a POST HTTP call to <ERP URL> with the following details in the request JSON body:

Order ID -> orderID
Order Total -> total
Customer Email ID -> emailID
Payment Type -> pType
```

## Prácticas recomendadas

Adobe recomienda seguir las siguientes prácticas recomendadas al utilizar las herramientas de codificación de IA:

### Lista de comprobación

Antes de iniciar cualquier sesión de desarrollo:

* Seleccionar para `REQUIREMENTS.md`
* Verificar que las herramientas de MCP funcionen
* Revisar fase y objetivos actuales
* Empezar con código de ejemplo o proyectos andamiados

Durante el desarrollo:

* Confíe en el [protocolo](#protocol) de cuatro fases
* Solicitar planes de implementación para un desarrollo complejo
* Utilizar las herramientas de MCP cuando estén disponibles
* Prueba de cada función después de la implementación
* Realice primero una prueba local y luego implemente y vuelva a realizar la prueba
* Aproveche las herramientas de codificación para probar la compatibilidad
* Pregunta de complejidad innecesaria
* Implementación incremental para un desarrollo más rápido

Al iniciar un nuevo chat:

* Proporcionar el traspaso de sesión adecuado
* Archivos de claves de referencia con `@`
* Establecer objetivos claros para la sesión
* Uso de límites basados en fases

### Flujo de trabajo

Al desarrollar con las herramientas de codificación de IA, comience con proyectos de código de muestra o andamios. Este enfoque garantiza que se esté construyendo sobre una base sólida en lugar de empezar desde la nada, al tiempo que optimiza el flujo de trabajo de desarrollo de IA.

Esto también le permite aprovechar las plantillas de Adobe y basarse en patrones y arquitecturas probados, al tiempo que mantiene estructuras y convenciones de directorio establecidas.

Consulte los siguientes recursos para empezar:

* [Kit de inicio de integración](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/create-integration)
* [plantillas de Adobe Commerce starter kit](https://github.com/adobe/adobe-commerce-samples/tree/main/starter-kit)
* [Plantillas de inicio de Adobe I/O Events](https://experienceleague.adobe.com/en/docs/commerce-learn/tutorials/adobe-developer-app-builder/io-events/getting-started-io-events)
* [aplicaciones de ejemplo de App Builder](https://developer.adobe.com/app-builder/docs/resources/sample_apps)

#### Por qué debería utilizar estos recursos

* **Patrones comprobados**: los Starter Kits representan las prácticas recomendadas y las decisiones de arquitectura de Adobe
* **Desarrollo más rápido**: reduce el tiempo invertido en plantillas y configuración
* **Coherencia**: garantiza que la extensión siga las convenciones establecidas
* **Mantenimiento**: más fácil de mantener y actualizar cuando se siguen patrones estándar
* **Documentación**: los Starter Kits incluyen ejemplos y documentación
* **Soporte técnico de la comunidad**: Es más fácil obtener ayuda cuando se utilizan enfoques estándar
* **Eficiencia del contexto de IA**: use patrones y estructuras familiares para trabajar, reduciendo la necesidad de explicaciones extensas y mejorando la precisión de generación de código
* **Uso de tokens reducido**: Haga referencia a patrones existentes en lugar de generar todo desde cero, lo que permite conversaciones más eficientes y menos resúmenes de contexto

### Protocol

El sistema de reglas aplica automáticamente el siguiente protocolo de cuatro fases. Las herramientas deben seguir este protocolo automáticamente al desarrollar extensiones:

* Fase 1: Análisis y aclaración de los requisitos
   * Cuando se le pregunte para aclarar preguntas, proporcione respuestas completas.
* Fase 2: Planificación arquitectónica y aprobación de usuarios
   * Cuando se presente un plan, revíselo cuidadosamente antes de aprobarlo.
* Fase 3: Generación e implementación de código
* Fase 4: Documentación y validación

### Solicitar planes de implementación para un desarrollo complejo

Para el desarrollo complejo que implica varias acciones de tiempo de ejecución, puntos de contacto o integraciones, solicite explícitamente que las herramientas de IA creen un plan de implementación detallado. Cuando vea un plan de alto nivel en [Phase 2](#protocol) que involucra varios componentes, pida un plan de implementación detallado para dividirlo en tareas manejables:

```terminal
Create a detailed implementation plan for this complex development.
```

Las extensiones de Adobe Commerce complejas suelen incluir:

* Varias acciones de tiempo de ejecución
* Configuración de eventos en varios puntos de contacto
* Integración con sistemas externos
* Requisitos de administración de estado
* Pruebas en varios componentes

### Uso de las herramientas MCP

La herramienta toma como valor predeterminado las herramientas MCP, pero en determinadas circunstancias, puede utilizar comandos CLI en su lugar. Si desea garantizar el uso de la herramienta MCP, solicítelas explícitamente en el mensaje.

Si ve que se están utilizando comandos CLI y desea utilizar herramientas MCP en su lugar, utilice el siguiente indicador:

```terminal
Use only MCP tools and not CLI commands
```

* Herramientas de MCP: aio-app-deploy, aio-app-dev, aio-dev-invoke
* Comandos CLI: implementación de aplicación aio, desarrollo de aplicación aio

Los comandos CLI se pueden utilizar en los siguientes casos:

* Situaciones de implementación complejas
* Depuración de problemas específicos
* Cuando las herramientas de MCP tienen limitaciones
* Operaciones únicas que no se benefician de la integración de MCP

### Desarrollo

Es importante cuestionar la complejidad innecesaria creada por las herramientas de IA.

Cuando se agregan archivos innecesarios (`validator.js`, `transformer.js`, `sender.js`) para extremos de solo lectura simples, use las siguientes indicaciones:

```terminal
Why do we need these files for a simple read-only endpoint?
Perform a root cause analysis before adding complexity
Verify if simpler solutions exist
```

### Pruebas

Siga estas prácticas recomendadas al realizar pruebas:

#### Prueba de cada función después de la implementación

Después de completar el desarrollo de una función en el plan de implementación, pruébela inmediatamente. Las pruebas tempranas evitan problemas compuestos y facilitan la depuración.

* No espere hasta que se hayan completado todas las funciones
* Realizar pruebas de forma incremental para detectar problemas de forma temprana
* Valide la funcionalidad antes de pasar a la siguiente función

#### Probar localmente primero

Realice siempre las primeras pruebas locales con la herramienta `aio-app-dev`. Esto proporciona comentarios inmediatos y permite ciclos de iteración más rápidos, una depuración más sencilla y sin sobrecarga de implementación.

1. Inicie el servidor de desarrollo local:

   ```bash
   aio-app-dev
   ```

1. Acciones de prueba localmente:

   ```bash
   aio-dev-invoke action-name --parameters '{"test": "data"}'
   ```

#### Implementación y prueba de nuevo

Una vez que las pruebas locales se hayan realizado correctamente, implemente y realice pruebas en el entorno de tiempo de ejecución. Los entornos de tiempo de ejecución pueden tener un comportamiento diferente al desarrollo local.

1. Implementar en tiempo de ejecución:

   ```bash
   aio-app-deploy
   ```

1. Prueba de acciones implementadas

1. Uso del explorador web o solicitudes HTTP directas

1. Comprobar registros de activación para depuración

#### Aproveche las herramientas de codificación para probar la compatibilidad

Pida ayuda con las pruebas. Las herramientas pueden ayudarle con la depuración, el análisis de registros y la creación de datos de prueba adecuados para sus acciones de tiempo de ejecución específicas.

**Acciones de tiempo de ejecución de pruebas**:

```terminal
Help me test the customer-created runtime action running locally
```

**Errores de depuración**:

```terminal
Why did the subscription-updated runtime action activation fail?
```

**Comprobar registros**:

```terminal
Help me check the logs for the last stock-monitoring runtime action invocation
```

**Crear cargas útiles de prueba**:

```terminal
Generate test data for this Commerce event
```

```terminal
Create a test payload for the customer_save_after event
```

**Buscar extremos de tiempo de ejecución**:

```terminal
What's the URL for this deployed action?
```

**Identificar autenticación**:

```terminal
How do I authenticate with this external API?
```

**Solucionar problemas**:

```terminal
Help me debug why this action is returning 500 errors
```

### Depuración

Deténgase y evalúe cuándo las cosas salen mal. Si tiene problemas:

* Detener y evaluar: no continuar en estado roto
* Comprobar registros: utilice registros de activación para identificar problemas
* Simplificar: elimine la complejidad para aislar los problemas
* Probar de forma incremental: corregir un problema a la vez
* Validar: pruebe cada corrección antes de continuar

### Implementación

Siga estas prácticas recomendadas al implementar:

#### Implementación incremental

Implementar solo las acciones modificadas para acelerar el desarrollo. Esto reducirá el riesgo de romper la funcionalidad existente y proporcionará comentarios más rápidos sobre los cambios. También reduce el riesgo de dañar la funcionalidad existente.

* Uso de herramientas de MCP para implementar acciones específicas

  ```bash
  aio-app-deploy --actions action-name
  ```

* Implementar acciones individuales después de realizar pruebas localmente
* Implementar gradualmente y evitar implementaciones de aplicaciones completas durante el desarrollo

#### Limpieza en tiempo de ejecución

Después de realizar cambios importantes, aproveche las herramientas para limpiar las acciones huérfanas. Permita que las herramientas de IA gestionen el proceso de limpieza de forma sistemática, puede identificar de forma eficaz las acciones huérfanas, verificar su estado y eliminarlas de forma segura sin intervención manual.

```terminal
Help me identify and clean up orphaned runtime actions
```

Solicite las herramientas de IA para enumerar las acciones implementadas e identificar las que no se utilizan

```terminal
List all deployed actions and identify which ones are no longer needed
```

Haga que las herramientas de IA eliminen las acciones huérfanas utilizando los comandos adecuados

```terminal
Remove the orphaned actions that are no longer part of the current implementation
```

### Monitorización

Siga estas prácticas recomendadas al supervisar la aplicación:

#### Observe los indicadores de calidad del contexto

* **Buen contexto**: AI recuerda decisiones recientes, hace referencia a archivos correctos
* **Contexto deficiente**: AI solicita información proporcionada anteriormente y repite los problemas resueltos

#### Rastrear velocidad de desarrollo

* **Alta velocidad**: Se necesita un progreso claro y una aclaración mínima
* **Baja velocidad**: Explicaciones repetidas, confusión de IA, progreso lento

#### Monitorización de la rentabilidad

Rastrear patrones de uso de tokens:

* **Eficiente**: uso de tokens bajo, pocos resúmenes de contexto
* **Ineficiente**: Alto uso de tokens, múltiples resúmenes, trabajo repetido

## Qué se debe evitar

Debe evitar los siguientes antipatrones al utilizar las herramientas de codificación de IA:

* **No omita la fase de aclaración**. Asegúrese siempre de que la fase 1 se complete antes de la implementación.
* **No omita la prueba después de cada característica**: realice la prueba gradualmente, no espere hasta que se complete todo.
* **No agregue complejidad sin el análisis de causa raíz**: cuestione las adiciones de archivos innecesarias y solicite una investigación adecuada.
* **No declare que se ha realizado correctamente sin una prueba de datos real**. Realice siempre pruebas con datos reales, no solo con casos puntuales.
* **No olvides la limpieza en tiempo de ejecución**: limpia siempre las acciones huérfanas después de cambios importantes.
