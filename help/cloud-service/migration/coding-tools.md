---
title: Herramientas para desarrolladores de codificación de IA para Adobe Commerce App Builder
description: Aprenda a utilizar las herramientas de IA para crear aplicaciones de Commerce App Builder.
feature: App Builder, Cloud
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
role: Developer
level: Intermediate
source-git-commit: 4e3f593ead4b0e32bdf474498421b20475dcbe52
workflow-type: tm+mt
source-wordcount: '2470'
ht-degree: 0%

---

# Herramientas para desarrolladores de codificación de IA para Adobe Commerce App Builder

Al migrar a [!DNL Adobe Commerce as a Cloud Service], puede usar las herramientas de codificación de IA para convertir las extensiones PHP [!DNL Adobe Commerce] existentes en aplicaciones [!DNL Adobe Developer App Builder]. También puede usar estas herramientas para crear nuevas aplicaciones de [!DNL App Builder].

Las herramientas de codificación de IA ofrecen las siguientes ventajas:

* **Flujo de trabajo de desarrollo mejorado**: herramientas de desarrollo de Adobe Commerce integradas.
* **Asistencia con tecnología de IA**: generación y depuración de código según el contexto.
* **Características específicas de Commerce**: Herramientas especializadas para el desarrollo de Adobe Commerce App Builder.
* **Flujos de trabajo automatizados**: procesos optimizados de desarrollo e implementación.

Al instalar las herramientas de codificación de IA, obtiene acceso a:

* Aptitudes: conjunto de aptitudes específicas de Adobe Commerce y App Builder diseñado para guiar e informar el desarrollo de aplicaciones.
* Servidor MCP para desarrolladores
* Servidor MCP de App Builder

## Actualización a la versión más reciente

Después de [instalar la herramienta para desarrolladores de programación de IA](#installation), puede actualizar a la versión más reciente ejecutando el siguiente comando:

```bash
aio commerce extensibility tools-setup
```

Esto actualizará las herramientas a la versión más reciente.

## Requisitos previos

* Cualquier agente de codificación que admita [aptitudes de agente](https://agentskills.io/home#adoption), como:

   * [Cursor](https://cursor.com/download)
   * [Código Claude](https://www.claude.com/product/claude-code)
   * [Copiloto de GitHub](https://github.com/features/copilot)
   * [Windsurf](https://windsurf.com)
   * [CLI de Gemini](https://github.com/google-gemini/gemini-cli)
   * [Códice OpenAI](https://openai.com/index/introducing-codex/)
   * [Cline](https://cline.bot)

* [Node.js](https://nodejs.org/en/download): versión LTS
* Administrador de paquetes: [npm](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm) o [yarn](https://classic.yarnpkg.com/lang/en/docs/install/#mac-stable)
* [Git](https://github.com/git-guides/install-git): para la clonación del repositorio y el control de versiones

## Instalación

>[!NOTE]
>
>Si solo desea instalar el servicio RAG de documentación y no todo el paquete de herramientas de codificación de IA, consulte [Servicio RAG de documentación](./doc-rag.md).

1. Instale la última [CLI de Adobe I/O](https://github.com/adobe/aio-cli) globalmente:

   ```bash
   npm install -g @adobe/aio-cli
   ```

1. Instale los siguientes complementos:

   * [Commerce CLI de Adobe I/O](https://github.com/adobe-commerce/aio-cli-plugin-commerce)
   * [Tiempo de ejecución de CLI de Adobe I/O](https://github.com/adobe/aio-cli-plugin-runtime)
   * [CLI de App Builder](https://github.com/adobe/aio-cli-plugin-app-dev)

   ```bash
   aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce @adobe/aio-cli-plugin-app-dev @adobe/aio-cli-plugin-runtime
   ```

1. Clone una de las siguientes opciones:

   * Commerce [kit de inicio de integración](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/create-integration) - para generar integraciones de back-office.

     ```bash
     git clone git@github.com:adobe/commerce-integration-starter-kit.git
     ```

   * Commerce [kit de inicio de cierre de compra](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/) para crear o ampliar la experiencia de cierre de compra, incluidos pagos, envíos e impuestos.

     ```bash
     git clone git@github.com:adobe/commerce-checkout-starter-kit.git
     ```

1. Vaya al directorio del Starter Kit:

   ```bash
   cd commerce-integration-starter-kit
   ```

1. Instale las herramientas de extensibilidad de Commerce AI ejecutando el comando de configuración interactivo:

   ```bash
   aio commerce extensibility tools-setup
   ```

   El proceso de instalación le pedirá que especifique las opciones de configuración. Siga las indicaciones para completar la instalación. Las herramientas se instalarán en el directorio seleccionado.

   * Seleccione el Starter Kit que desee utilizar para el proyecto.

     ```shell-session
     ? Which starter kit would you like to use?
     ❯ Integration starter kit
        Checkout starter kit
     ```

   * Seleccione su agente de codificación preferido. Se admiten más de 40 agentes de codificación, pero si no ve su agente preferido, puede utilizar la opción `Other` para instalar habilidades para cualquier agente de codificación. Consulte la documentación del agente de codificación para obtener instrucciones sobre cómo configurar las aptitudes.

     ```shell-session
     ? Which coding agent would you like to install skills for?
     ❯ Cursor
        Claude Code
        GithubCopilot
        Windsurf
        Gemini CLI
        OpenAI Codex
        Cline
        ...
     ```

   * El instalador detectará si tiene instalado NPM o Yarn y realizará la selección adecuada automáticamente. Sin embargo, si no tiene ninguno instalado, se le pedirá que seleccione el administrador de paquetes, Adobe recomienda utilizar `npm` para mantener la coherencia:

     ```shell-session
     ? Which package manager would you like to use?
     ❯ npm
        yarn
     ```

1. Después de instalar correctamente las herramientas de codificación, el proceso de instalación configura:

   * Integración del servidor MCP para el desarrollo de Adobe Commerce
   * [Aptitudes de agente](#skills) para mejorar la experiencia de desarrollo
   * Flujos de trabajo y herramientas de desarrollo específicas de Commerce

   Ya están instaladas las habilidades y las herramientas de MCP. Si no ve las habilidades y herramientas de MCP, reinicie el agente de codificación.

>[!NOTE]
>
>Antes de implementar el proyecto, deberá completar las siguientes tareas de configuración:
>
>* Inicie sesión en [Adobe Developer Console](https://developer.adobe.com/console) mediante la CLI de Adobe I/O.
>* Cree un proyecto de App Builder (consulte [Configuración del proyecto](https://developer.adobe.com/commerce/extensibility/events/project-setup)).
>* Configurar variables de entorno en un archivo de `.env`.
>
>Puede completar estos pasos de configuración manualmente o aprovechar las herramientas de codificación de IA para guiarle a través del proceso. Consulte [Crear una integración](https://developer.adobe.com/commerce/extensibility/starter-kit/integration/create-integration/) para obtener instrucciones de configuración detalladas.

## Configuración posterior a la instalación

### Inicie sesión en Adobe I/O CLI

Después de instalar [!DNL Adobe I/O CLI], debe iniciar sesión siempre que desee utilizar el servidor MCP.

```bash
aio auth login
```

Para comprobar que ha iniciado sesión, ejecute el siguiente comando:

```bash
aio where
```

Si tiene problemas, intente cerrar la sesión y volver a iniciarla:

```bash
aio auth logout
aio auth login
```

>[!NOTE]
>
>Algunas funciones del servidor MCP funcionarán sin iniciar sesión, pero el servicio RAG (Retrieval-Augmented Generation) no funcionará. El servicio RAG proporciona al agente de codificación de IA acceso en tiempo real al conjunto completo de documentación de Adobe Commerce, lo que le permite responder preguntas y generar código basado en las prácticas de desarrollo, API y patrones arquitectónicos actuales de Commerce.
>
>Para instalar el servicio RAG de forma independiente, consulte [Servicio RAG de documentación](./doc-rag.md).

### Cursor

1. Reinicie el IDE del cursor para cargar las nuevas herramientas y configuración de MCP.

1. Compruebe la instalación confirmando que las habilidades están presentes en la carpeta `.cursor/skills/`.

1. Habilite el servidor MCP:

   * Abra la configuración del MCP del cursor con **Cmd+Mayús+P** (macOS) o **Ctrl+Mayús+P** (Windows y Linux).
   * Tipo **Vista: Abrir configuración de MCP**
   * Busque **commerce-extensibility MCP Server** en la lista
   * Active el servidor **ON** para habilitar las herramientas de codificación

1. Comprobar el estado del servidor: el servidor MCP de extensibilidad de Commerce debe aparecer de la siguiente manera:

   ```shell-session
   Status: Connected/Active
   Server: commerce-extensibility
   Configuration: Automatically configured via .cursor/mcp.json
   ```

1. Utilice el siguiente mensaje para ver si el agente utiliza el servidor MCP. Si no es así, pídale al agente que utilice explícitamente las herramientas de MCP disponibles.

   ```shell-session
   What are the differences between Adobe Commerce PaaS and Adobe Commerce as a Cloud Service when configuring a webhook that activates an App Builder runtime action?
   ```

### Copiloto

1. Reinicie Visual Studio Code para cargar las nuevas herramientas y configuración de MCP.

1. Compruebe la instalación confirmando que el archivo `copilot-instructions.md` existe en la carpeta `.github`.

1. Habilite el servidor MCP:

   * Abra el panel Extensiones haciendo clic en el icono **Extensiones** en la barra de actividades de la barra lateral izquierda, o bien, use **Cmd+Mayús+X** (macOs) o **Ctrl+Mayús+X** (Windows y Linux).
   * Haga clic en [!UICONTROL **SERVIDORES MCP - INSTALADOS**].
   * Haga clic en el icono de engranaje situado junto a [!UICONTROL **commerce-extensibility MCP Server**] y seleccione [!UICONTROL **Start Server**], si el servidor está detenido.
   * Vuelva a hacer clic en el icono de engranaje y seleccione [!UICONTROL **Mostrar salida**].

1. Compruebe el estado del servidor. La salida `MCP:commerce-extensibility` debe coincidir con lo siguiente:

   ```shell-session
   2025-11-13 12:58:50.652 [info] Starting server commerce-extensibility
   2025-11-13 12:58:50.652 [info] Connection state: Starting
   2025-11-13 12:58:50.652 [info] Starting server from LocalProcess extension host
   2025-11-13 12:58:50.657 [info] Connection state: Starting
   2025-11-13 12:58:50.657 [info] Connection state: Running
   
   (...)
   
   2025-11-13 12:58:50.753 [info] Discovered 10 tools
   ```

1. Utilice el siguiente mensaje para ver si el agente utiliza el servidor MCP. Si no es así, pídale al agente que utilice explícitamente las herramientas de MCP disponibles.

   ```shell-session
   What are the differences between Adobe Commerce PaaS and SaaS when configuring a webhook that activates an App Builder runtime action?
   ```

## Mensaje de ejemplo

El siguiente mensaje de ejemplo utiliza el Starter Kit de integración para crear una aplicación para enviar notificaciones cuando se realiza un pedido.

```shell-session
Implement an Adobe Commerce SaaS application that will send an ERP notification when a customer places an order. The ERP notification must be sent as a POST HTTP call to <ERP URL> with the following details in the request JSON body:

Order ID -> orderID
Order Total -> total
Customer Email ID -> emailID
Payment Type -> pType
```

El siguiente mensaje de ejemplo utiliza el Starter Kit de desprotección para crear una aplicación que proporciona métodos de envío personalizados.

```shell-session
Implement an Adobe Commerce SaaS application that provides custom shipping methods.
The extension should:
1. Return shipping options based on the destination postal code
2. If postal code is in California, add an "Express California" option for $15
3. If postal code is outside US, add an "International Standard" option for $25
4. The carrier code should be "MYSHIP"
```



## Pedir comandos

Además de preguntar, puede usar el comando `/search-commerce-docs` para buscar documentación en conversaciones con el agente. Por ejemplo:

```shell-session
/search-commerce-docs "How do I subscribe to Commerce events?"
```

## Aptitudes

Aunque las habilidades se invocarán automáticamente al conversar con el agente de codificación, también puede invocarlas manualmente con los siguientes comandos:

* `/architect`: diseña la arquitectura para las extensiones de Adobe Commerce usando [!DNL App Builder] y el Starter Kit seleccionado. Se utiliza para planificar integraciones, seleccionar eventos, diseñar flujos de datos o tomar decisiones de arquitectura.
* `/developer`: implementa extensiones de Adobe Commerce siguiendo [!DNL App Builder] patrones y la estructura de archivos. Se utiliza al generar código, actualizar archivos de configuración o implementar acciones de tiempo de ejecución.
* `/devops-engineer` - Implementa y opera extensiones de [!DNL App Builder]. Se utiliza para implementar aplicaciones, configurar entornos, solucionar problemas de implementación, configurar CI/CD o resolver errores de incorporación.
* `/product-manager`: recopila y documenta los requisitos para las extensiones de Adobe Commerce. Se utiliza al iniciar un nuevo proyecto, definir criterios de aceptación, aclarar objetivos empresariales o crear documentación de `REQUIREMENTS.md`.
* `/technical-writer`: crea documentación completa para [!DNL App Builder] aplicaciones. Se utiliza al escribir `README.md`, guías del usuario, documentación de la API o registros de cambios, para garantizar la integridad de la documentación.
* `/tester` - Crea pruebas completas para [!DNL App Builder] aplicaciones. Se utiliza al escribir pruebas unitarias, pruebas de integración, validar la seguridad o garantizar la calidad y la cobertura del código.
* `/tutor` (experimental): enseña conceptos de desarrollo de aplicaciones de [!DNL Adobe Commerce] con explicaciones y ejemplos claros. Úselo cuando aprenda [!DNL App Builder], comprenda los eventos o necesite ayuda sobre los patrones de desarrollo.

## Prácticas recomendadas

Adobe recomienda seguir las siguientes prácticas recomendadas al utilizar las herramientas de codificación de IA:

### Modo de planificación

Al conversar con su agente de codificación, debería seleccionar el modo **Plan** para crear un plan de implementación detallado para su proyecto.

El método para seleccionar el modo **Plan** varía según el agente que esté usando. Consulte la documentación de su agente para obtener instrucciones. Por ejemplo:

* [Cursor](https://cursor.com/docs/agent/modes)
* [Código Claude](https://code.claude.com/docs/en/common-workflows#when-to-use-plan-mode)
* [CLI de Gemini](https://geminicli.com/docs/cli/plan-mode/)

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
* [Kit de inicio de cierre de compra](https://developer.adobe.com/commerce/extensibility/starter-kit/checkout/)
* [plantillas de Adobe Commerce starter kit](https://github.com/adobe/adobe-commerce-samples/tree/main/starter-kit)
* [Plantillas de inicio de Adobe I/O Events](https://experienceleague.adobe.com/es/docs/commerce-learn/tutorials/adobe-developer-app-builder/io-events/getting-started-io-events)
* [aplicaciones de ejemplo de App Builder](https://developer.adobe.com/app-builder/docs/resources/sample_apps)

#### Por qué debería utilizar estos recursos

* **Patrones comprobados**: los Starter Kits representan las prácticas recomendadas y las decisiones de arquitectura de Adobe
* **Desarrollo más rápido**: reduce el tiempo invertido en plantillas y configuración
* **Coherencia**: garantiza que la aplicación siga las convenciones establecidas
* **Mantenimiento**: más fácil de mantener y actualizar cuando se siguen patrones estándar
* **Documentación**: los Starter Kits incluyen ejemplos y documentación
* **Soporte técnico de la comunidad**: Es más fácil obtener ayuda cuando se utilizan enfoques estándar
* **Eficiencia del contexto de IA**: use patrones y estructuras familiares para trabajar, reduciendo la necesidad de explicaciones extensas y mejorando la precisión de generación de código
* **Uso de tokens reducido**: Haga referencia a patrones existentes en lugar de generar todo desde cero, lo que permite conversaciones más eficientes y menos resúmenes de contexto

### Protocol

Las habilidades instaladas aplican automáticamente el siguiente protocolo de cuatro fases. Las herramientas deben seguir este protocolo automáticamente al desarrollar aplicaciones:

* Fase 1: Análisis y aclaración de los requisitos
   * Cuando se le pregunte para aclarar preguntas, proporcione respuestas completas.
* Fase 2: Planificación arquitectónica y aprobación de usuarios
   * Cuando se presente un plan, revíselo cuidadosamente antes de aprobarlo.
* Fase 3: Generación e implementación de código
* Fase 4: Documentación y validación

### Solicitar planes de implementación para un desarrollo complejo

Para el desarrollo complejo que implica varias acciones de tiempo de ejecución, puntos de contacto o integraciones, solicite explícitamente que las herramientas de IA creen un plan de implementación detallado. Cuando vea un plan de alto nivel en [Phase 2](#protocol) que involucra varios componentes, pida un plan de implementación detallado para dividirlo en tareas manejables:

```shell-session
Create a detailed implementation plan for this complex development.
```

Las aplicaciones complejas de Adobe Commerce suelen implicar:

* Varias acciones de tiempo de ejecución
* Configuración de eventos en varios puntos de contacto
* Integración con sistemas externos
* Requisitos de administración de estado
* Pruebas en varios componentes

### Uso de las herramientas MCP

>[!NOTE]
>
>Antes de usar las herramientas de MCP, asegúrese de haber [iniciado sesión en la CLI de Adobe I/O](#log-in-to-the-adobe-io-cli).

La herramienta toma como valor predeterminado las herramientas MCP, pero en determinadas circunstancias puede utilizar comandos CLI en su lugar. Para garantizar el uso de la herramienta MCP, solicítelas explícitamente en el mensaje.

Si ve que se están utilizando comandos CLI y desea utilizar herramientas MCP en su lugar, utilice el siguiente indicador:

```shell-session
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

Interrogue la complejidad innecesaria creada por las herramientas de IA.

Cuando se agregan archivos innecesarios (`validator.js`, `transformer.js`, `sender.js`) para extremos de solo lectura simples, use las siguientes indicaciones:

```shell-session
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

```shell-session
Help me test the customer-created runtime action running locally
```

**Errores de depuración**:

```shell-session
Why did the subscription-updated runtime action activation fail?
```

**Comprobar registros**:

```shell-session
Help me check the logs for the last stock-monitoring runtime action invocation
```

**Crear cargas útiles de prueba**:

```shell-session
Generate test data for this Commerce event
```

```shell-session
Create a test payload for the customer_save_after event
```

**Buscar extremos de tiempo de ejecución**:

```shell-session
What's the URL for this deployed action?
```

**Identificar autenticación**:

```shell-session
How do I authenticate with this external API?
```

**Solucionar problemas**:

```shell-session
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

Implementar solo las acciones modificadas para acelerar el desarrollo. Este método reduce el riesgo de dañar la funcionalidad existente y proporciona comentarios más rápidos sobre los cambios.

* Uso de herramientas de MCP para implementar acciones específicas

  ```bash
  aio-app-deploy --actions action-name
  ```

* Implementar acciones individuales después de realizar pruebas localmente
* Implementar gradualmente y evitar implementaciones de aplicaciones completas durante el desarrollo

#### Limpieza en tiempo de ejecución

Después de realizar cambios importantes, aproveche las herramientas para limpiar las acciones huérfanas. Permita que las herramientas de IA gestionen el proceso de limpieza sistemáticamente. Puede identificar de forma eficaz las acciones huérfanas, verificar su estado y eliminarlas de forma segura sin intervención manual.

```shell-session
Help me identify and clean up orphaned runtime actions
```

Solicite las herramientas de IA para enumerar las acciones implementadas e identificar las que no se utilizan

```shell-session
List all deployed actions and identify which ones are no longer needed
```

Haga que las herramientas de IA eliminen las acciones huérfanas utilizando los comandos adecuados

```shell-session
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

Evite los siguientes antipatrones al utilizar las herramientas de codificación de IA:

* **No omita la fase de aclaración**. Asegúrese siempre de que la fase 1 se complete antes de la implementación.
* **No omita la prueba después de cada característica**: realice la prueba gradualmente, no espere hasta que se complete todo.
* **No agregue complejidad sin el análisis de causa raíz**: cuestione las adiciones de archivos innecesarias y solicite una investigación adecuada.
* **No declare que se ha realizado correctamente sin una prueba de datos real**. Realice siempre pruebas con datos reales, no solo con casos puntuales.
* **No olvides la limpieza en tiempo de ejecución**: limpia siempre las acciones huérfanas después de cambios importantes.

## Proporcionar comentarios

Los desarrolladores interesados en proporcionar comentarios sobre las herramientas de codificación de IA pueden utilizar el comando `/feedback`.

Este comando le permite proporcionar comentarios de texto y enviar registros a Adobe. Cualquier registro que envíe se saneará para eliminar cualquier información privada o personal.

>[!TIP]
>
>La experiencia del usuario variará ligeramente según el IDE que utilice. El siguiente proceso describe la experiencia en Cursor.

1. En su agente, escriba `/feedback` y seleccione el comando `commerce-extensibility/feedback`.

1. Proporcione sus comentarios sobre las herramientas del campo **Comentarios** que aparece en la parte superior del IDE y presione la tecla **Intro**.

   ![Campo de entrada de comando de comentarios del cursor](../assets/feedback-response.png){width="600" zoomable="yes"}

1. En el campo **Guardar localmente**, escriba `yes` o `no` y presione **Entrar** para indicar si desea guardar una copia local de sus registros.

   ![Campo local de guardado del comando de comentarios del cursor](../assets/feedback-save.png){width="600" zoomable="yes"}

   Si seleccionó **Sí**, puede revisar los registros de su carpeta `chats` después de enviar sus comentarios.

1. El comando `commerce-extensibility/feedback` aparece en el campo de entrada de chat del agente. Pulse **Intro** o haga clic en **Enviar** para enviar sus comentarios a Adobe.

>[!NOTE]
>
>Si no ve el comando `/feedback`, es posible que tenga que [actualizar a la versión más reciente](#updating-to-the-latest-version).
