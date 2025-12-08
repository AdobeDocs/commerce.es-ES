---
title: Requisitos previos del tutorial de extensión Clasificaciones
description: Conozca los requisitos previos del laboratorio de extensión de clasificaciones.
role: Developer
hide: true
hidefromtoc: true
source-git-commit: e153e974be1dc5ec8ff2eff8d699ce87ef6708dc
workflow-type: tm+mt
source-wordcount: '454'
ht-degree: 0%

---

# Requisitos previos del tutorial de extensión de clasificaciones (Beta)

>[!NOTE]
>
>Las herramientas de IA utilizadas en este tutorial se encuentran actualmente en Beta y podrían incluir errores u otros problemas.

En esta página se enumeran los requisitos previos y los pasos de configuración para los tutoriales que utilizan [!DNL Adobe Commerce as a Cloud Service], como el [tutorial de extensión de clasificaciones](./ratings-extension.md).

## Requisitos previos de Adobe Commerce as a Cloud Service

* Instalar [!DNL Adobe I/O CLI]

  ```bash
  npm install -g @adobe/aio-cli
  ```

* Instalación del complemento de Commerce

  ```bash
  aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce
  ```

* Descargue un IDE asistido por IA, como [Cursor](https://cursor.com/download) (recomendado), otros IDE, como Claude Code, Gemini CLI o Copilot también son compatibles, pero podrían requerir modificaciones en las indicaciones y otros pasos en el tutorial.

### Requisitos previos de Adobe Developer Console

1. Vaya a [Adobe Developer Console](https://developer.adobe.com/console){target="_blank"}.
1. Inicie sesión con su correo electrónico y contraseña.

#### Creación de un nuevo proyecto

1. Vaya a [Adobe Developer Console](https://developer.adobe.com/).
1. Haga clic en [!UICONTROL **Crear proyecto a partir de una plantilla**].
1. Seleccione la plantilla [!UICONTROL **App Builder**].
1. Escriba un [!UICONTROL **Título de proyecto**] y [!UICONTROL **Nombre de aplicación**].
1. Asegúrese de que la casilla de verificación **[!UICONTROL Include Runtime]** esté marcada.

   ![Crear proyecto con plantilla de App Builder](../assets/app-builder-template.png){width="600" zoomable="yes"}

1. Haga clic en **Guardar**.

#### Añadir API al espacio de trabajo

1. Haga clic en el área de trabajo [!UICONTROL **Stage**] y, a continuación, repita los pasos siguientes para cada API.

   ![API agregadas al espacio de trabajo](../assets/add-apis-workspace.png){width="600" zoomable="yes"}

1. Haga clic en [!UICONTROL **Agregar servicio**] y seleccione [!UICONTROL **API**].

1. Seleccione una de las siguientes API. Deberá repetir este proceso para cada API enumerada a continuación:

   * Filtro de [!UICONTROL **Adobe Services**]:
      * [!UICONTROL **API de administración de E/S**]
      * API [!UICONTROL **Eventos de E/S**]
   * Filtro [!UICONTROL **Experience Cloud**]:
      * API de [!UICONTROL **Adobe I/O Events for Adobe Commerce**]

1. Haga clic en [!UICONTROL **Siguiente**].

1. Haga clic en [!UICONTROL **Guardar API configurada**].

1. Repita los pasos anteriores hasta que todas las API se agreguen al espacio de trabajo.

   ![API agregadas al espacio de trabajo](../assets/apis-added.png){width="600" zoomable="yes"}

### Configuración de la CLI de Adobe I/O

1. Borre cualquier configuración existente:

   ```bash
   aio config clear
   ```

   Iniciar sesión con [!DNL Adobe I/O CLI]:

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

   ![Configuración de CLI](../assets/cli-configuration.png){width="600" zoomable="yes"}

### Clonar el Starter Kit de integración

Clone el repositorio del Starter Kit de integración de Commerce y prepare su proyecto:

```bash
git clone https://github.com/adobe/commerce-integration-starter-kit.git extension
cd extension
```

![Clonar kit de inicio](../assets/clone-starter-kit.png){width="600" zoomable="yes"}

### Creación de un archivo .env

Cree el archivo de configuración de entorno:

```bash
cp env.dist .env
```

Abra el archivo `.env` en un editor de texto y agregue las siguientes credenciales de OAuth:

```text
OAUTH_CLIENT_ID=
OAUTH_CLIENT_SECRET=
OAUTH_TECHNICAL_ACCOUNT_ID=
OAUTH_TECHNICAL_ACCOUNT_EMAIL=
OAUTH_ORG_ID=
```

Puede copiar estos valores de la página **[!UICONTROL Credential details]** en [Developer Console](https://developer.adobe.com/) haciendo clic en la pestaña **[!UICONTROL OAuth Server-to-Server]** del área de trabajo.

![Credenciales de OAuth](../assets/oauth-credentials.png){width="600" zoomable="yes"}

#### Añadir la configuración de Commerce

Agregue los siguientes detalles de la instancia de Commerce al archivo `.env`:

```text
COMMERCE_BASE_URL=
COMMERCE_GRAPHQL_ENDPOINT=
```

Para buscar estos valores:

1. Vaya a [Instancias del servicio Commerce Cloud](https://experience.adobe.com/#/@commerce/commerce/cloud-service/instances).
1. Haga clic en el icono de información junto a la instancia.
1. Copie el extremo REST como `COMMERCE_BASE_URL`.
1. Copie el extremo de GraphQL como `COMMERCE_GRAPHQL_ENDPOINT`.

#### Establecer prefijo de evento

Establezca un valor temporal para el prefijo de evento:

```text
EVENT_PREFIX=test
```

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

![Conectarse al espacio de trabajo](../assets/connect-workspace.png){width="600" zoomable="yes"}

### Instalación de herramientas de IA de extensibilidad

Actualice el archivo de reglas de cursor y la configuración de MCP para incluir el paquete `commerce-extensibility-tools`.

1. Configure las herramientas de desarrollo asistido por IA en la carpeta `extension` mediante los siguientes comandos:

   ```bash
   cd extension
   ```

   ```bash
   aio commerce extensibility tools-setup
   ```

   ![Instalar herramientas de IA](../assets/install-ai-tools.png){width="600" zoomable="yes"}
<!--
## Storefront prerequisites

The following items are required to complete the [storefront](./ratings-extension.md#connect-to-the-storefront) section of [this tutorial](./ratings-extension.md) and see the product ratings in your store.

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
  * Windows: Use [Git Bash](https://git-scm.com/install) or [Windows Subsystem for Linux (WSL)](https://learn.microsoft.com/en-us/windows/wsl/install)

* [Google Chrome](https://www.google.com/chrome/) - Required for testing the storefront

### Get the project files

You can obtain the project files using one of the following methods:

#### Option A: Clone the repository (recommended)

If you have [!DNL Git] installed, open your terminal and clone the repository:

```bash
git clone --branch agentic-dev https://github.com/hlxsites/aem-boilerplate-commerce.git storefront
cd storefront
```

#### Option B: Download the zip file

If you do not have [!DNL Git] installed:

1. Download the project zip file from: [https://github.com/hlxsites/aem-boilerplate-commerce/archive/refs/heads/agentic-dev.zip](https://github.com/hlxsites/aem-boilerplate-commerce/archive/refs/heads/agentic-dev.zip)
1. Extract the zip file to a folder on your machine.
1. Open your terminal and navigate into the unzipped folder:

   ```bash
   cd path/to/aem-boilerplate-commerce-agentic-dev
   ```

### Install root dependencies

Install the main project dependencies:

```bash
npm install
```

This will install all the necessary packages for the storefront application.

### Install MCP server dependencies

Navigate to the MCP server directory and install its dependencies:

```bash
cd mcp-server
npm install
cd ..
```

### Configure environment variables

The MCP server requires certain environment variables to connect to the RAG service.

Create an `.env` file in the `mcp-server` directory:

```bash
cd mcp-server
cp env.example .env
```

Edit the `.env` file and add the following values:

```env
RAG_MODE=worker
WORKER_RAG_URL=
```

### Enable MCP in Cursor

The Model Context Protocol (MCP) server provides AI agents with access to [!DNL Adobe Commerce] Storefront documentation.

#### Open Cursor MCP settings

![Open Cursor MCP Settings](../assets/cursor-mcp-settings.png){width="600" zoomable="yes"}

1. Open [!DNL Cursor].
1. Navigate to **[!UICONTROL Cursor]** > **[!UICONTROL Settings]** > **[!UICONTROL Cursor Settings]** > **[!UICONTROL Tools & MCP]**.

#### Enable and configure MCP features

The project includes an MCP configuration file at `.cursor/mcp.json`. This file should already be configured to use the local MCP server.

Verify the MCP configuration:

1. Ensure the "commerce-documentation-rag" server is listed and enabled

The configuration should look similar to this:

![MCP Configuration](../assets/mcp-configuration.png){width="600" zoomable="yes"}

>[!NOTE]
>
>The `start-mcp.sh` script will automatically load the environment variables from your `.env` file in the `mcp-server` directory.

#### Restart Cursor

After enabling MCP and configuring the server:

1. Quit [!DNL Cursor] completely.
1. Reopen [!DNL Cursor] and open the `aem-boilerplate-commerce` project.

#### Verify MCP connection

Check that the MCP server is running correctly:

1. Open a new chat in [!DNL Cursor].
1. Look for an indicator showing the MCP server is connected. This indicator is typically located in the chat interface.
1. Try entering a prompt like the following:

   ```text
   Search the storefront docs for information about slots
   ```

If the MCP server is working, you should see relevant documentation results.

![MCP Connection Verified](../assets/mcp-connection-verified.png){width="600" zoomable="yes"}

If this works, you are ready to continue with the [tutorial](./ratings-extension.md).
 -->
