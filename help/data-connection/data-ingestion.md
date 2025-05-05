---
title: Tipos de datos de Commerce
description: Conozca los tipos de datos que puede recopilar y enviar a Experience Platform.
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '312'
ht-degree: 0%

---

# Tipos de datos de Commerce

La [extensión de conexión de datos](overview.md) conecta los datos de Commerce con Experience Platform. Los datos que se van a usar en Experience Platform se agrupan en dos tipos de comportamiento: datos de series temporales, que pertenecen a la clase **Experience Event**, y datos de registros, que pertenecen a la clase **Individual Profile**.

Obtenga más información acerca de [comportamiento de los datos](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=es#data-behaviors) y [clases](https://experienceleague.adobe.com/docs/experience-platform/xdm/schema/composition.html?lang=es#class) en Experience Platform.

## Datos de series temporales

Los datos de series temporales proporcionan una instantánea del sistema en el momento en que un sujeto del registro realizó una acción, ya sea directa o indirectamente. Por ejemplo, cuando un comprador explora un producto en su sitio, agrega un producto al carro de compras, realiza un pedido, etc. Los datos de series de tiempo se incorporan en Experience Platform mediante un esquema que tiene la clase establecida en **Experience Event**.

### Datos de series temporales capturadas

Consulte [eventos de comportamiento](events.md) y [eventos de back-office](events-backoffice.md) para saber qué datos se capturan cuando se genera un evento de serie temporal.

### Esquema necesario para introducir datos de eventos de series temporales

Aprenda a [crear un esquema](update-xdm.md) que pueda ingerir datos de eventos de series temporales de procedimientos administrativos y de comportamiento.

## Registrar datos

Los datos de registro proporcionan información sobre los atributos de un asunto. Un sujeto podría ser una organización o un individuo. Por ejemplo, un comprador del sitio crea una cuenta de y que genera datos de registro. Estos datos se incorporan en Experience Platform mediante un esquema que tiene la clase establecida en **Perfil individual**. Puede enviar esos datos de registro al servicio de segmentación y administración de perfiles de Adobe: [Real-Time CDP](https://experienceleague.adobe.com/docs/experience-platform/rtcdp/intro/rtcdp-intro/overview.html?lang=es).

### Datos de registro de perfil capturados

Consulte [datos de registro de perfil de cliente](events-profilerecord.md) para saber qué datos se capturan cuando se genera un registro de perfil.

### Esquema necesario para introducir datos de registro de perfil

Aprenda a [crear un esquema](profile-data.md) que pueda ingerir datos de registro de perfil.
