---
title: Inicio
description: Use la página de inicio  [!DNL Payment Services] del administrador para incorporarse (incluido ACCS), abrir los informes de transacciones, administrar los puntos de entrada de pedidos y pagos en PaaS y acceder a Información, ayuda y configuración.
role: Admin, User
level: Intermediate
exl-id: d7a4c87f-33cb-446a-b442-3cdf05b518a2
feature: Payments, Checkout, Paas, Saas
source-git-commit: e4aede88f8470f79e5987afcb7311bf6ef44c16e
workflow-type: tm+mt
source-wordcount: '405'
ht-degree: 1%

---

# Inicio de [!DNL Payment Services]

[!DNL Payment Services] para Adobe Commerce y Magento Open Source proporciona una vista Inicio con la información que necesita para configurar y utilizar la extensión. Las opciones de la parte superior de Inicio dependen de la implementación: Adobe Commerce en la nube o en línea (PaaS), o [!DNL Adobe Commerce as a Cloud Service] o [!DNL Adobe Commerce Optimizer] (SaaS).

En la barra lateral _Admin_, vaya a **[!UICONTROL Sales]** > **[!UICONTROL [!DNL Payment Services]]**:

>[!BEGINTABS]

>[!TAB Adobe Commerce en la nube y local]

![Vista de inicio](assets/home-view.png){width="700" zoomable="yes"}

>[!TAB Adobe Commerce as a Cloud Service y Commerce Optimizer]

Hasta que complete la incorporación, **[!UICONTROL Home]** mostrará **[!UICONTROL ACCS Onboarding Required]**. El aviso se vincula a [configurar el servicio de espacio aislado](sandbox.md#enable-sandbox-testing) (con una cuenta de procesamiento PayPal de prueba) o a [habilitar pagos activos](production.md#enable-live-payments) si ya lo ha probado en otro entorno:

Se requiere la incorporación de ![ACCS en la página principal de servicios de pago](assets/payment-services-home-accs-onboarding.png){width="700" zoomable="yes"}

Una vez completada la incorporación (o en una instancia ya configurada), **[!UICONTROL Home]** muestra **[!UICONTROL Transactions]** con **[!UICONTROL View Report]** para el informe tabular, además de las áreas **[!UICONTROL Learn]** y **[!UICONTROL Help]**:

Inicio de ![Servicios de pago en SaaS](assets/payment-services-home-saas.png){width="700" zoomable="yes"}

>[!ENDTABS]

En esta vista de Inicio, puedes acceder a _Inicio_, _Obtener información_ sobre [!DNL Payment Services], configurar la extensión _Configuración_ o obtener _Ayuda_. Use **[!UICONTROL View Report]** (SaaS) o los puntos de entrada **[!UICONTROL Orders]** y **[!UICONTROL Payouts]** (Adobe Commerce en la nube y local) para abrir los informes; consulte [Informes](reporting.md).

## Inicio

[!BADGE Solo PaaS]{type=Informative url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."}

| Campo | Descripción |
|---|---|
| [!UICONTROL Orders] | Estos informes le permiten ver rápidamente el estado de pago de sus pedidos e identificar cualquier problema potencial. |
| [!UICONTROL Payouts] | Los informes de pagos muestran información completa sobre los pagos de un vistazo, lo que permite una total transparencia sobre el importe del pago, el volumen procesado y la creación de informes detallados sobre las transacciones para la reconciliación financiera. |

[!BADGE Solo SaaS]{type=Positive url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."}

| Campo | Descripción |
|---|---|
| [!UICONTROL Transactions] | Resume el informe Transacciones, que le ayuda a comprender el resultado de transacciones específicas. Haga clic en **[!UICONTROL View Report]** para abrir la cuadrícula de transacciones (por ejemplo, ID de transacción de pedidos y PayPal, método de pago, resultado y códigos de respuesta). Ver [vista de informe de transacciones](reporting.md#transactions-report-view). |

## Aprender

| Campo | Descripción |
|---|---|
| [!UICONTROL Read documentation] | Consulte los documentos más recientes para usuarios y desarrolladores de [!DNL Payment Services]. |
| [!UICONTROL How to onboard] | Encuentre todo lo que necesita para configurar y empezar a utilizar la característica [!DNL Payment Services]. |
| [!UICONTROL Understand financial reports] | Explicación detallada de los informes de administración de flujo de efectivo en [!DNL Payment Services]. |

## Ayuda

| Campo | Descripción |
|---|---|
| [!UICONTROL Visit help center] | El Centro de ayuda de [!DNL Adobe Commerce] tiene artículos de Knowledge Base sobre [!DNL Payment Services]. |
| [!UICONTROL Get support] | Visite el portal de soporte técnico de [!DNL Adobe Commerce] para obtener ayuda con [!DNL Payment Services]. |

## Configuración

En la vista Inicio, haga clic en **[!UICONTROL Settings]**. Consulte [[!DNL Payment Services] configuración](configure-admin.md) para obtener más información.

El pie de página del área Servicios de pago mostrará las etiquetas de versión **Servicios de pago** y **Tablero de servicios de pago**, por ejemplo, cuando recopile detalles para obtener soporte técnico.
