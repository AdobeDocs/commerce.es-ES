---
title: Requisitos previos del tutorial
description: Conozca los requisitos previos del laboratorio de extensión de clasificaciones.
feature: App Builder, Cloud
role: Developer
level: Intermediate
source-git-commit: 68e34cecbc1b16194ccc2e0296c2d66f37855b7c
workflow-type: tm+mt
source-wordcount: '691'
ht-degree: 0%

---

# Requisitos previos del tutorial

En esta página se enumeran los requisitos previos y los pasos de configuración de [!DNL Adobe Commerce as a Cloud Service] tutoriales, como el [tutorial de extensión de clasificaciones](./ratings-extension.md) y el [tutorial de extensión de método de envío](./shipping-method-extension.md).

## Requisitos previos de Adobe Commerce as a Cloud Service

* Instalar [!DNL Adobe I/O CLI]

  ```bash
  npm install -g @adobe/aio-cli
  ```

* Instale los complementos [Adobe I/O CLI Commerce](https://github.com/adobe-commerce/aio-cli-plugin-commerce), [Adobe I/O CLI Runtime](https://github.com/adobe/aio-cli-plugin-runtime) y [App Builder CLI](https://github.com/adobe/aio-cli-plugin-app-dev):

  ```bash
  aio plugins:install https://github.com/adobe-commerce/aio-cli-plugin-commerce @adobe/aio-cli-plugin-app-dev @adobe/aio-cli-plugin-runtime
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

   ![Creación de proyecto de Adobe Developer Console con la plantilla de App Builder seleccionada](../assets/app-builder-template.png){width="600" zoomable="yes"}

1. Haga clic en [!UICONTROL **Guardar**].

#### Añadir API al espacio de trabajo

1. Haga clic en el área de trabajo [!UICONTROL **Stage**] y, a continuación, repita los pasos siguientes para cada API.

   ![Espacio de trabajo de fase con la opción Agregar servicio para las API](../assets/add-apis-workspace.png){width="600" zoomable="yes"}

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

   ![Workspace muestra todas las API requeridas agregadas correctamente](../assets/apis-added.png){width="600" zoomable="yes"}

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

   ![Terminal que muestra la selección del espacio de trabajo y el proyecto de la organización Adobe I/O CLI](../assets/cli-configuration.png){width="600" zoomable="yes"}

### Clona los starter kits

Clone uno de los siguientes repositorios de Commerce starter kit para la extensión que está creando y prepare su proyecto:

Kit de inicio de integración:

```bash
git clone https://github.com/adobe/commerce-integration-starter-kit.git extension
cd extension
```

Kit de inicio de compra:

```bash
git clone https://github.com/adobe/commerce-checkout-starter-kit.git extension
cd extension
```

>[!BEGINTABS]

>[!TAB Kit de inicio de integración]

### Creación de un archivo .env

Cree el archivo de configuración de entorno:

```bash
cp env.dist .env
```

Abra el archivo `.env` en un editor de texto y agregue las siguientes credenciales de OAuth:

```shell-session
OAUTH_CLIENT_ID=
OAUTH_CLIENT_SECRET=
OAUTH_TECHNICAL_ACCOUNT_ID=
OAUTH_TECHNICAL_ACCOUNT_EMAIL=
OAUTH_ORG_ID=
```

Puede copiar estos valores de la página **[!UICONTROL Credential details]** en [Developer Console](https://developer.adobe.com/) haciendo clic en la pestaña **[!UICONTROL OAuth Server-to-Server]** del área de trabajo.

![Página de credenciales de servidor a servidor OAuth en Adobe Developer Console](../assets/oauth-credentials.png){width="600" zoomable="yes"}

#### Añadir la configuración de Commerce

Agregue los siguientes detalles de la instancia de Commerce al archivo `.env`:

```shell-session
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

```shell-session
EVENT_PREFIX=test
```

### Descargar configuración de Workspace

Ejecute el siguiente comando para descargar el archivo de configuración de Workspace:

```bash
aio console workspace download workspace.json
```

Copie el archivo de configuración de área de trabajo en el directorio `scripts`:

```bash
cp workspace.json scripts/
```

### Conectar el espacio de trabajo local al remoto

Vincule el proyecto local al espacio de trabajo remoto:

```bash
aio app use workspace.json -m
```

![El terminal muestra una conexión correcta del espacio de trabajo con el comando de uso de la aplicación aio](../assets/connect-workspace.png){width="600" zoomable="yes"}

>[!TAB Kit de inicio de cierre de compra]

### Conectar el espacio de trabajo local al remoto

Vincule el proyecto local al espacio de trabajo remoto. Desde la raíz del proyecto (la carpeta `extension`), ejecute:

```bash
aio app use --merge
```

Cuando se le solicite, elija la opción que utiliza la organización, el proyecto y el espacio de trabajo que seleccionó al configurar la CLI de Adobe I/O. Esto escribe la configuración del espacio de trabajo en la aplicación para que la implementación y el desarrollo local utilicen ese espacio de trabajo.

![El terminal muestra una conexión correcta del espacio de trabajo con el comando de uso de la aplicación aio](../assets/connect-workspace.png){width="600" zoomable="yes"}

>[!ENDTABS]

### Instalación de herramientas de IA de extensibilidad

Este proceso crea la configuración de MCP (`.<agent>/mcp.json`), el directorio de aptitudes (`.<agent>/skills/`) y agrega `AGENTS.md` a la raíz del proyecto. Se le pedirá que elija un Starter Kit, un agente de codificación y un gestor de paquetes.


1. Configure las herramientas de desarrollo asistido por IA en la carpeta `extension` mediante los siguientes comandos:

   ```bash
   cd extension
   ```

   ```bash
   aio commerce extensibility tools-setup
   ```

   ![Terminal que muestra la salida del comando de configuración de las herramientas de extensibilidad de IA](../assets/install-ai-tools.png){width="600" zoomable="yes"}

1. Una vez finalizada la instalación, reinicie el agente de codificación para que pueda cargar las nuevas herramientas y habilidades de MCP. Las herramientas de Commerce App Builder ya están disponibles en su entorno.

   >[!NOTE]
   >
   >Si ve una advertencia que indica que no se encontraron aptitudes para el Starter Kit, se produjo un error, a menudo porque la configuración se ejecutó en una carpeta distinta de la carpeta en la que se clonó el Starter Kit. Ejecute `aio commerce extensibility tools-setup` desde la carpeta `extension` (la raíz del proyecto del Starter Kit) y seleccione el Starter Kit apropiado cuando se le solicite.

   ![Terminal que muestra la configuración de las herramientas de extensibilidad de IA con el kit de inicio de pago seleccionado](../assets/tools-setup-checkout.png){width="600" zoomable="yes"}

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

   ```shell-session
   Search the storefront docs for information about slots
   ```

If the MCP server is working, you should see relevant documentation results.

![MCP Connection Verified](../assets/mcp-connection-verified.png){width="600" zoomable="yes"}

If this works, you are ready to continue with the [tutorial](./ratings-extension.md).
 -->
