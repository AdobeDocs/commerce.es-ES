---
title: Preparación para HIPAA para  [!DNL Commerce] Servicios
description: 'Aprenda a utilizar la extensión  [!DNL Data Connection] para compartir datos con Experience Platform y mantener el cumplimiento de la HIPAA. [!DNL Commerce] '
role: Admin, Leader
feature: Security, Compliance
exl-id: 8851e6d2-c466-4d8e-bfa4-20d0ad6522b5
TQID: https://experienceleague.adobe.com/PxrtL1nHtJsRJuAehDVKRk0ZuJz0ta7i84j1K6An1QU
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
  - id: d1e21356-0064-4f48-9089-16e3f0dbd2a6
  - id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2:
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
topic_v2:
  - id: c7d04a2c-412a-4c9d-9d7a-4456eaa5adeb
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
  - id: f4e6943a-c91a-4134-a2c7-f4f20cfff2f0
source-git-commit: 33cd0e217447351b690646ec8d230f76060a74da
workflow-type: tm+mt
source-wordcount: 601
ht-degree: 1%

---

# Preparación para HIPAA para [!DNL Commerce] servicios

La extensión [!DNL Data Connection] le permite compartir datos de evento de back office [!DNL Commerce] con Experience Platform y mantener el cumplimiento de la HIPAA.

>[!IMPORTANT]
>
>Dado que los eventos de tienda se generan en el lado del cliente, es responsabilidad del comerciante [no enviar los datos de evento de tienda](connect-data.md#data-collection) a Experience Platform.

En este artículo, aprenderá lo siguiente:

- Qué desea instalar
- Asegurarse de que los datos enviados a Experience Platform están preparados para HIPAA
- Cifrado de datos en [!DNL Commerce]

## Instalación

Si adquirió el complemento de atención médica para Adobe [!DNL Commerce], lo más probable es que ya haya instalado la [extensión compatible con HIPAA](https://experienceleague.adobe.com/es/docs/commerce-admin/start/compliance/hipaa-ready-service/overview#installation). Para asegurarse de que los datos del evento de back office [!DNL Commerce] estén preparados para HIPAA, también debe instalar la extensión [!DNL Data Connection] con la extensión adicional **Servicios de datos HIPAA**. La extensión **Data Services HIPAA** garantiza que cualquier dato de back office que envíe a Experience Platform esté preparado para HIPAA. Obtenga información [sobre cómo instalar la extensión](install.md#install-the-data-services-hipaa-extension).

>[!IMPORTANT]
>
>Al instalar la extensión **Data Services HIPAA**, ya no se capturan los datos de evento de tienda que usan Live Search y Product Recommendations. Esto se debe a que los datos de evento de tienda se generan en el lado del cliente. Para seguir capturando y enviando datos de evento de tienda, vuelva a habilitar la recopilación de eventos para estos servicios. Consulte [configuración general](https://experienceleague.adobe.com/es/docs/commerce-admin/config/general/general#data-services) para obtener más información.

## Asegurarse de que los datos enviados a Experience Platform están preparados para HIPAA

Todos los datos de eventos de back office que la extensión [!DNL Data Connection] envía a Experience Platform se consideran confidenciales en [!DNL Commerce]. Sin embargo, es responsabilidad del comerciante aplicar etiquetas de uso de datos a su esquema [!DNL Commerce] en Experience Platform para identificar explícitamente datos concretos como confidenciales. Cuando se aplican etiquetas de uso de datos directamente a un esquema, esas etiquetas se propagan a todos los conjuntos de datos existentes y futuros basados en ese esquema.

Para obtener una descripción general de las etiquetas de uso de datos y su función dentro del marco de trabajo de control de datos, consulte la [descripción general de las etiquetas de uso de datos](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/labels/overview) en la documentación de Experience Platform.

### Aplicar etiquetas de uso de datos a [!DNL Commerce] campos

Siga los pasos del tutorial [administrar etiquetas de uso de datos para un esquema](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/tutorials/labels) para aprender a aplicar etiquetas a su esquema [!DNL Commerce].

Consulte el [glosario de etiquetas confidenciales](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/labels/reference#sensitive) para obtener más información sobre las etiquetas disponibles que puede aplicar a los campos del esquema [!DNL Commerce]. Por ejemplo, la etiqueta `RHD` identifica información médica protegida (PHI) o información sobre un paciente que Adobe le permite cargar de manera contractual.

Cuando los datos de [!DNL Commerce] están etiquetados como confidenciales, puede aplicar directivas para evitar operaciones de datos que constituyan violaciones de directivas. Más información sobre [aplicación de políticas](https://experienceleague.adobe.com/es/docs/experience-platform/data-governance/enforcement/overview) en Experience Platform.

## Cifrado de datos en Commerce

Adobe [!DNL Commerce] utiliza cifrado de nivel de bloque. Para almacenamiento, [!DNL Commerce] usa Amazon Elastic Block Store (EBS). Todos los volúmenes EBS se cifran con el algoritmo AES-256, lo que significa que los datos se cifran en reposo. Los datos de [!DNL Commerce] en tránsito se transmiten a través de conexiones seguras y cifradas usando HTTPS [TLS v1.2](https://datatracker.ietf.org/doc/html/rfc5246).

>[!IMPORTANT]
>
>Commerce no admite el cifrado o cifrado de nivel de columna o fila cuando los datos no están en reposo o no están en tránsito entre los servidores.

### Cifrado de datos en Experience Platform

Cuando los comerciantes envían sus datos a Experience Platform, estos se envían mediante HTTPS TLS v1.2. Más información sobre cómo [Experience Platform](https://experienceleague.adobe.com/es/docs/experience-platform/landing/governance-privacy-security/encryption) cifra los datos.

## Cómo gestiona [!DNL Commerce] las solicitudes de privacidad

Descubra cómo [!DNL Commerce] [administra las solicitudes de privacidad](handle-privacy-request.md).
