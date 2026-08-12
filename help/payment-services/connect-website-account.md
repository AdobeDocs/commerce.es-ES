---
title: Conectar una cuenta PayPal diferente para un sitio web
description: Incorporación completa de PayPal con alcance de sitio web en el administrador para conectar una cuenta de comerciante de PayPal diferente a un sitio web individual.
role: Admin, User
level: Intermediate
feature: Payments, Checkout, Configuration, Paas, Saas
TQID: 'https://experienceleague.adobe.com/U1zGAU6vYKjk2tc2KXnvyqnYdbA2HKTCNZSKhHdS0Vw'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
source-git-commit: d754c71e287d7d9ff297dd7d95efbaaae7ffc2fc
workflow-type: tm+mt
source-wordcount: 393
ht-degree: 0%

---

# Conectar una cuenta PayPal diferente para un sitio web

Para las instancias de Commerce con **varios sitios web**, es posible que necesites **diferentes cuentas de comerciante de PayPal**. [!DNL Payment Services] habilita la incorporación de PayPal de **ámbito de sitio web** después de la incorporación de **global**.

>[!NOTE]
>
> Esta función solo admite la conexión de nuevas cuentas.

## Requisitos previos para la incorporación con alcance de sitio web

La incorporación a nivel de sitio web solo está disponible una vez que su tienda cumple estos requisitos:

- La instalación de [Commerce Services Connector](https://experienceleague.adobe.com/es/docs/commerce/user-guides/integration-services/saas) se ha completado.
- Hay una cuenta PayPal conectada en el ámbito global (configuración predeterminada).

Puede confirmarlo comprobando que los siguientes campos se rellenen en el ámbito predeterminado:

- [!UICONTROL Payment Services Sandbox ID]
- [!UICONTROL Payment Services Production ID]
- [!UICONTROL PayPal Merchant ID]

Si estos campos están vacíos, primero debe [completar la incorporación global](configure-admin.md). El botón **[!UICONTROL Connect different account]** está deshabilitado hasta que complete los requisitos previos.

## Iniciar la conexión a nivel de sitio web

1. En la barra lateral _Admin_, vaya a **[!UICONTROL Stores]** > _[!UICONTROL Settings]_>**[!UICONTROL Configuration]**>**[!UICONTROL Sales]**&#x200B;y elija **[!UICONTROL Payment Methods]**.
1. En el selector de ámbito de la esquina superior izquierda, cambie de **[!UICONTROL Default Config]** al **[!UICONTROL Website]** que desee incorporar.
1. Haga clic en **[!UICONTROL Connect different account]**.

   Si el botón está deshabilitado, su tienda no ha cumplido los [requisitos previos](#prerequisites-global-scope) anteriores.

## Completar el modal de incorporación

Se abre una ventana emergente.

1. Seleccione su **[!UICONTROL Country]** en la lista desplegable.
1. Elija su tipo de incorporación: **[!UICONTROL Basic]** o **[!UICONTROL Advanced]**.
1. Haga clic en **[!UICONTROL Next]**.

>[!NOTE]
>
> Si va a realizar la incorporación en Hungría, España o Austria, debe abrir y ver el vínculo Términos y condiciones antes de hacer clic en el botón **[!UICONTROL I Accept]**. El botón se desactiva hasta que abra los Términos y condiciones.

## Iniciar sesión en PayPal

Cuando se le redirija al inicio de sesión en PayPal, inicie sesión y complete los pasos de incorporación en PayPal.

>[!IMPORTANT]
>
> Una vez que haga clic en **[!UICONTROL Confirm and Continue]**, la sesión del ámbito global finalizará y se iniciará la conexión a nivel de sitio web. Si hizo clic accidentalmente en **[!UICONTROL Connect different account]**, puede cancelar seleccionando **[!UICONTROL Cancel]** o haciendo clic en el icono **X** antes de confirmar.

## Finalice y vuelva al administrador

1. Después de completar los pasos de PayPal, cierra la ventana de PayPal.
1. Haga clic en **[!UICONTROL Finish]** o en **X**, en la esquina superior derecha, para cerrar la ventana emergente de incorporación.
1. La página de configuración de Commerce se actualiza automáticamente.

## Confirme el resultado

Una vez que la página se actualice, consulte la página de configuración de ámbito del sitio web para ver:

- Un **[!UICONTROL PayPal Merchant ID]** actualizado para ese sitio web.
- Una etiqueta de estado que muestra el resultado de la incorporación:

| Estado | Significado |
| --- | --- |
| `ACTIVE` | Incorporación completada correctamente |
| `PENDING` | La incorporación sigue procesándose |
| `ERROR` | La incorporación no se completó correctamente |

Si ve un estado de `ERROR`, aparecerá un mensaje de error que explica el problema. Para reintentar el proceso de incorporación, vuelva a hacer clic en **[!UICONTROL Connect different account]**.
