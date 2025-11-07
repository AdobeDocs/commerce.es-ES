---
title: Requisitos previos de laboratorio de ADL Commerce
description: Conozca los requisitos previos del laboratorio de extensión de clasificaciones.
role: Developer
hide: true
hidefromtoc: true
source-git-commit: ba4d096bcb99420c029d0b0674fc00f1f1445cea
workflow-type: tm+mt
source-wordcount: '451'
ht-degree: 0%

---

# Adobe Developers Live: Requisitos previos de Adobe Commerce Lab

Esta página lista los requisitos previos y otros pasos de configuración manuales para el [laboratorio de extensión de clasificaciones](./workbook.md). El laboratorio también contiene una secuencia de comandos que automatiza la mayoría de estos pasos.

## Requisitos previos de extensión

Antes de empezar, complete los siguientes requisitos previos:

* Instalar [!DNL Adobe I/O CLI]

  ```bash
  npm install -g @adobe/aio-cli
  ```

* Instalación del complemento de Commerce

  ```bash
  aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce
  ```

* Descargue un IDE asistido por IA, como [Cursor](https://cursor.com/download) (recomendado), otros IDE, como Claude Code, Gemini CLI o Copilot también son compatibles, pero podrían requerir modificaciones en las indicaciones y otros pasos en este tutorial.
<!-- 
### Create a new project on Adobe Developer Console

1. Navigate to [Adobe Developer Console](https://developer.adobe.com/).
1. Click [!UICONTROL **Create project from a template**].
1. Select the [!UICONTROL **App Builder**] template.
1. Enter a [!UICONTROL **Project Title**] and [!UICONTROL **App Name**].
1. Ensure the **[!UICONTROL Include Runtime]** checkbox is marked.

   ![Create project with App Builder template](./assets/app-builder-template.png){width="600" zoomable="yes"}

1. Click **Save**.

### Add APIs to the workspace

1. Click the [!UICONTROL **Stage**] workspace and then repeat the following steps for each API.

   ![APIs added to workspace](./assets/add-apis-workspace.png){width="600" zoomable="yes"}

1. Click [!UICONTROL **Add Service**] and select [!UICONTROL **API**].

1. Select the [!UICONTROL **Adobe Services**] filter and select one of the following APIs:

   * [!UICONTROL **I/O Management API**]
   * [!UICONTROL **I/O Events**]

1. Select the [!UICONTROL **Experience Cloud**] filter and select one of the following APIs:

   * [!UICONTROL **Adobe I/O Events for Adobe Commerce**]

1. Click [!UICONTROL **Next**].

1. Click[!UICONTROL **Save configured API**].

1. Repeat the previous steps until all APIs are added to the workspace.

   ![APIs added to workspace](./assets/apis-added.png){width="600" zoomable="yes"} -->

### Configurar la CLI de AIO

1. Borre la configuración existente:

   ```bash
   aio config clear
   ```

   Inicie sesión con la CLI de AIO:

   ```bash
   aio auth login -f
   ```

1. Seleccione su organización, proyecto y espacio de trabajo con cada uno de los siguientes comandos:

   ```bash
   aio console org select
   ```

   ```bash
   aio console project select
   ```

   ```bash
   aio console workspace select
   ```

   ![Configuración de CLI](./assets/cli-configuration.png){width="600" zoomable="yes"}

### Clonar kit de inicio de integración

Clone el repositorio del Starter Kit de integración de Commerce y prepare su proyecto:

```bash
git clone --branch adl https://github.com/adobe/commerce-integration-starter-kit.git extension
cd extension
```

![Clonar kit de inicio](./assets/clone-starter-kit.png){width="600" zoomable="yes"}

### Cree el archivo .env.

Cree el archivo de configuración de entorno:

```bash
cp env.dist .env
```

<!-- Open the `.env` file in a text editor and add the following OAuth credentials:

```text
OAUTH_CLIENT_ID=
OAUTH_CLIENT_SECRET=
OAUTH_TECHNICAL_ACCOUNT_ID=
OAUTH_TECHNICAL_ACCOUNT_EMAIL=
OAUTH_ORG_ID=
```

You can copy these values from the **[!UICONTROL Credential details]** page in [Developer Console](https://developer.adobe.com/) by clicking the **[!UICONTROL OAuth Server-to-Server]** tab on your workspace.

![OAuth credentials](./assets/oauth-credentials.png){width="600" zoomable="yes"}

#### Add the Commerce configuration

Add the following Commerce instance details to your `.env` file:

```text
COMMERCE_BASE_URL=
COMMERCE_GRAPHQL_ENDPOINT=
```

To find these values:

1. Go to [Commerce Cloud Service instances](https://experience.adobe.com/#/@commerce/commerce/cloud-service/instances).
1. Click the information icon next to your assigned seat.
1. Copy the REST endpoint as `COMMERCE_BASE_URL`.
1. Copy the GraphQL Endpoint as `COMMERCE_GRAPHQL_ENDPOINT`.

#### Set event prefix

Set a temporary value for the event prefix:

```text
EVENT_PREFIX=test
```
 -->

### Descargar configuración de Workspace

Ejecute el siguiente comando para descargar el archivo de configuración de Workspace:

```bash
aio console workspace download workspace.json
```

### Conectar el espacio de trabajo local al remoto

Vincule el proyecto local al espacio de trabajo remoto:

```bash
aio app use workspace.json -m
```

![Conectarse al espacio de trabajo](./assets/connect-workspace.png){width="600" zoomable="yes"}

## Requisitos previos de Storefront

Se requieren los siguientes elementos para completar la sección [tienda](#connect-to-the-storefront) de este tutorial y ver las clasificaciones de productos en su tienda.
<!-- 
* Install [!DNL Node.js] (version `22.x.x`) and npm (`9.0.0` or higher). Verify your installation:

   ```bash
   node --version
   npm --version
   ```

* Install [Git](https://git-scm.com) (Optional) - Required only if [cloning the repository directly](#option-a-clone-the-repository-recommended)(recommended), not needed if you [download the zip file](#option-b-download-the-zip-file). Verify your installation:

  ```bash
  git --version
  ```

* Bash shell
  * macOS/Linux: No installation required
  * Windows: Use [Git Bash](https://git-scm.com/install) or [Windows Subsystem for Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/install).

* [Google Chrome](https://www.google.com/chrome/) - Required for testing the storefront -->

### Obtener los archivos del proyecto

Puede obtener los archivos de proyecto de una de las dos maneras siguientes:

<!-- 
#### Option A: Clone the repository (recommended) -->

Si tiene [!DNL Git] instalado, abra el terminal y clone el repositorio:

```bash
git clone --branch agentic-dev https://github.com/hlxsites/aem-boilerplate-commerce.git storefront
cd storefront
```

<!-- #### Option B: Download the zip file

If you don't have [!DNL Git] installed:

1. Download the project zip file from: [https://github.com/hlxsites/aem-boilerplate-commerce/archive/refs/heads/agentic-dev.zip](https://github.com/hlxsites/aem-boilerplate-commerce/archive/refs/heads/agentic-dev.zip)
1. Extract the zip file to a folder on your machine.
1. Open your terminal and navigate into the unzipped folder:

   ```bash
   cd path/to/aem-boilerplate-commerce-agentic-dev
   ``` -->

### Instalación de dependencias raíz

Instale las dependencias principales del proyecto:

```bash
npm install
```

Esto instalará todos los paquetes necesarios para la aplicación de tienda.

### Instalar dependencias del servidor MCP

Vaya al directorio del servidor MCP e instale sus dependencias:

```bash
cd mcp-server
npm install
cd ..
```

<!-- ### Configure environment variables

The MCP server requires certain environment variables to connect to the RAG service.

Create a `.env` file in the `mcp-server` directory:

```bash
cd mcp-server
cp env.example .env
```

Edit the `.env` file and add the following values (we'll provide the actual URL during the lab):

```env
RAG_MODE=worker
WORKER_RAG_URL=<provided-during-lab>
```

>[!NOTE]
>
>The actual value for `WORKER_RAG_URL` will be provided by the lab facilitator at the start of the session. -->

### Habilitar MCP en el cursor

El servidor de Protocolo de contexto de modelo (MCP) proporciona a los agentes de IA acceso a la documentación de la tienda [!DNL Adobe Commerce].

#### Abrir configuración de MCP de cursor

![Abrir configuración de MCP del cursor](./assets/cursor-mcp-settings.png){width="600" zoomable="yes"}

1. Abrir [!DNL Cursor]
1. Ir a **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**

#### Habilitar y configurar las características de MCP

El proyecto incluye un archivo de configuración de MCP en `.cursor/mcp.json`. Este archivo ya debe estar configurado para usar el servidor MCP local.

Compruebe la configuración de MCP:

1. Asegúrese de que el servidor &quot;commerce-documentation-rag&quot; aparece en la lista y esté habilitado

La configuración debería ser similar a la siguiente:

![Configuración de MCP](./assets/mcp-configuration.png){width="600" zoomable="yes"}

>[!NOTE]
>
>El script `start-mcp.sh` cargará automáticamente las variables de entorno desde el archivo `.env` en el directorio `mcp-server`.

#### Cursor de reinicio

Después de habilitar MCP y configurar el servidor:

1. Salir de [!DNL Cursor] por completo
1. Volver a abrir [!DNL Cursor] y abrir el proyecto `aem-boilerplate-commerce`

#### Verificar conexión MCP

Compruebe que el servidor MCP se está ejecutando correctamente:

1. Abrir un nuevo chat en [!DNL Cursor]
1. Busque un indicador que indique que el servidor MCP está conectado (normalmente en la interfaz de chat)
1. Intente hacer una pregunta como: &quot;Busque en los documentos de la tienda información sobre las ranuras&quot;

Si el servidor MCP funciona, debería ver los resultados relevantes de la documentación.

![Conexión MCP verificada](./assets/mcp-connection-verified.png){width="600" zoomable="yes"}

### Inicio del servidor de desarrollo

Inicie el servidor de desarrollo local:

```bash
npm run start
```

El servidor de desarrollo se iniciará a las `http://localhost:3000`.

Vaya a la página de ropa en `http://localhost:3000/apparel`.

![Servidor de desarrollo en ejecución](./assets/development-server-running.png){width="600" zoomable="yes"}
