---
title: Responsabilidad compartida
description: Obtenga información acerca de las responsabilidades de seguridad de cada parte involucrada en su proyecto [!DNL Adobe Commerce as a Cloud Service].
feature: Cloud, Security
role: Admin, Developer, Leader
level: Intermediate
exl-id: 424fe5cd-5d54-425d-97ce-024476d18dde
badgeSaas: label="Solo SaaS" type="Positive" url="https://experienceleague.adobe.com/es/docs/commerce/user-guides/product-solutions" tooltip="Solo se aplica a los proyectos de Adobe Commerce as a Cloud Service y Adobe Commerce Optimizer (infraestructura de SaaS administrada por Adobe)."
autotag-review: '2026-06-18T16:19:21.186Z'
TQID: 'https://experienceleague.adobe.com/ZjR9eFTVz8RIrYIN1CxyEgegGoZljXJKrtWZStx-ln0'
product_v2:
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
  - id: de2e2e68-c5d7-4efe-be7b-27528698f06b
    internal-label: Commerce as a Cloud Service
feature_v2:
  - id: ba9e5be9-7de1-4f71-a5d2-baead0e425ee
    internal-label: Security
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
    internal-label: Accounts
  - id: 5a951749-fac9-5bc7-9a98-ebe4ff066437
    internal-label: Cloud
subfeature_v2:
  - id: d9ced453-36f4-4eb5-b2f3-1d593e32476b
    internal-label: Account management
role_v2:
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
  - id: f8a45b24-4be7-4f1b-909b-60d06b483a20
    internal-label: Leader
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
level_v2:
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
topic_v2:
  - id: bce87dde-a4ab-44c9-8a18-ad66e4ddb377
    internal-label: Customer experience
  - id: d095671a-1355-40aa-8b5f-06c33c68080b
    internal-label: Security
source-git-commit: 8b3db59ed02539646dd53a2e9c7a0925b7c3a804
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%
---
# Modelo operativo y de seguridad de responsabilidad compartida

[!DNL Adobe Commerce as a Cloud Service] es un servicio bajo demanda que depende de un modelo operativo y de seguridad de responsabilidad compartida. Adobe y los clientes comparten estas responsabilidades, y cada parte asume una responsabilidad distinta por garantizar y operar la aplicación de Adobe Commerce.

[!DNL Adobe Commerce as a Cloud Service with Managed Operations] es una oferta premium que agrega un ingeniero de éxito del cliente (Customer Success Engineer, CSE) designado y un equipo de soporte P1 de Operaciones administradas ininterrumpidamente, además del modelo de responsabilidad compartida estándar. Adobe sigue siendo propietario de la plataforma, la infraestructura, la seguridad y la aplicación principal, y usted sigue siendo propietario de sus personalizaciones e integraciones, pero con Operaciones administradas, Adobe Managed Services es consultado sobre sus:

- Integraciones
- Aplicaciones de App Builder
- Edge Delivery Storefront
- Administración de eventos
- Actualizaciones de plataforma

Adobe Managed Services también comparte la responsabilidad de las pruebas de recuperación ante desastres, la depuración y el aislamiento de problemas. Su CSE le guía en la incorporación a través de go-live y más allá, de modo que tenga a un experto en Adobe con usted en cada fase en lugar de operar por su cuenta.

>[!BEGINSHADEBOX]

Las siguientes tablas de resumen utilizan el modelo RACI para mostrar las responsabilidades de seguridad compartidas entre Adobe, Operaciones gestionadas por Adobe y los clientes.

**R** — Responsable
**A** — Responsable
**C** — Consultado
**I** — Informado

>[!ENDSHADEBOX]

| Tarea | Adobe | Operaciones administradas de Adobe | Cliente |
| --- | --- | --- | --- |
| Definición de reglas WAF de origen back-end | RA | | |
| Definición de reglas de WAF de CDN back-end | RA | | |
| Implementación y mantenimiento de [!DNL Adobe Developer App Builder] aplicaciones | | | RA |
| Implementación de reglas WAF de plataforma back-end | RA | | |
| Implementación de reglas WAF de CDN back-end | RA | | |
| Corrigiendo errores principales en [!DNL Adobe Commerce as a Cloud Service] | RA | | I |
| Publicando [!DNL Adobe Commerce as a Cloud Service] parches de infraestructura | RA | | |
| Escalado (infraestructura) | RA | | |
| Escala (aplicación principal) | RA | | |
| Integración de aplicaciones externas | | C | RA |
| Instalación de aplicaciones de App Builder | | C | RA |
| Prueba del rendimiento de todas las aplicaciones de App Builder | | C | RA |
| Temática y diseño de aplicaciones de App Builder personalizadas | | C | RA |
| Configuración del DNS back-end | RA | | I |
| Incorporación de CDN back-end | RA | | I |
| Compatibilidad con CDN back-end | RA | | I |
| Obtención de un proveedor DNS back-end | RA | | |
| Aprovisionamiento de los entornos de producción y de zona protegida | A | | R |
| Acceso a Dynamics for Adobe Commerce en la infraestructura en la nube | R | | C |
| Solución de problemas de seguridad del cliente back-end | RA | | I |
| Solución de problemas de seguridad de CDN back-end | RA | | |
| Asistencia a Adobe en la investigación de seguridad (análisis/auditorías) | RA | | |
| Realización de exploraciones ASV PCI | RA | | I |
| Remediación de exploraciones PCI de infraestructura de Adobe Commerce | R | | |
| Administración de secretos de plataforma y sistema operativo | RA | | |
| Supervisión de registros de seguridad back-end | RA | | |
| Control de la asistencia al cliente y acceso | A | C | R |
| Pruebas y documentación anuales del plan de recuperación ante desastres de Adobe, así como de las copias de seguridad y restauración | RA | C | |
| Pruebas y documentación anuales del plan de recuperación ante desastres | RA | RA | |
| Depuración y aislamiento de problemas | R | R | R |
| Compatibilidad oportuna con la depuración y el proceso de aislamiento de problemas | R | R | R |
| Publicación de actualizaciones y parches en Adobe Commerce Core | RA | C | I |
| Instalación de actualizaciones y parches en Adobe Commerce Core | RA | C | I |
| Calidad de aplicación principal de Adobe Commerce | RA | C | |
