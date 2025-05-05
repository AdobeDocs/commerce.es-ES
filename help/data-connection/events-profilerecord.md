---
title: Registros de perfil
description: Descubra qué datos captura un registro de perfil.
role: Admin, Developer
feature: Personalization, Integration, Eventing
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---

# [!DNL Data Connection] registros de perfil

A continuación se describen los datos de registro de perfil de Commerce que están disponibles al instalar la extensión [!DNL Data Connection]. Los datos de los registros de perfil se envían a Adobe Experience Platform.

## Registro de perfil

Las actualizaciones de registros de perfil están disponibles en Experience Platform cuando se crea, actualiza o elimina un perfil nuevo.

### Datos recopilados del registro de perfil

A continuación se describen los datos capturados para un registro de perfil.

| Campo | Descripción |
|---|---|
| `channel` | Contiene información sobre el origen de los datos. Tanto `_id` como `_type` contienen [valores con espacio de nombres](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/schema/namespaces). |
| `channel._id` | El identificador único del canal, como `"https://ns.adobe.com/xdm/channels/web"`. |
| `channel._type` | Identifica el origen de los datos del canal, como `"https://ns.adobe.com/xdm/channel-types/web"`. |
| `person` | Contiene información sobre el cliente. |
| `person.name` | Contiene información sobre el nombre del cliente. |
| `person.name.firstName` | Contiene el nombre del cliente. |
| `person.name.lastName` | Contiene los apellidos del cliente. |
| `person.birthDate` | Fecha de nacimiento del comprador. |
| `personalEmail` | Una dirección de correo electrónico personal. |
| `personalEmail.address` | La dirección técnica, por ejemplo, `name@domain.com`, tal como se define comúnmente en RFC2822 y estándares subsiguientes. |
| `billingAddress` | La dirección postal de facturación. |
| `billingAddress.street1` | Información principal de la dirección postal, número de piso, número de calle y nombre de la calle. |
| `billingAddress.street2` | Segunda línea para información de dirección (opcional) |
| `billingAddress.city` | El nombre de la ciudad. |
| `billingAddress.state` | El nombre del estado. Este es un campo de forma libre. |
| `billingAddress.country` | El nombre del territorio administrado por el gobierno. Aparte de `xdm:countryCode`, este es un campo de forma libre que puede tener el nombre del país en cualquier idioma. |
| `billingAddress.primary` | Indica si esta es la dirección de facturación principal. El valor siempre es `False`. |
| `billingAddressPhone` | El número de teléfono asociado con la dirección de facturación. |
| `billingAddressPhone.number` | El número de teléfono. Tenga en cuenta que el número de teléfono es una cadena y puede incluir caracteres clave como paréntesis `()`, guiones `-` o caracteres para indicar identificadores de marcado secundario como extensiones `x`, por ejemplo, `1-353(0)18391111` o `+613 9403600x1234`. |
| `billingAddressPhone.primary` | Indica si este es el número de teléfono principal de la dirección de facturación. El valor siempre es `False`. |
| `shippingAddress` | La dirección postal de envío. |
| `shippingAddress.street1` | Información principal de la dirección postal, número de piso, número de calle y nombre de la calle. |
| `shippingAddress.street2` | Segunda línea para información de dirección (opcional) |
| `shippingAddress.city` | El nombre de la ciudad. |
| `shippingAddress.state` | El nombre del estado. Este es un campo de forma libre. |
| `shippingAddress.country` | El nombre del territorio administrado por el gobierno. Aparte de `xdm:countryCode`, este es un campo de forma libre que puede tener el nombre del país en cualquier idioma. |
| `shippingAddress.primary` | Indica si esta es la dirección de envío principal. El valor siempre es `False`. |
| `shippingAddressPhone` | El número de teléfono asociado con la dirección de envío. |
| `shippingAddressPhone.number` | El número de teléfono. Tenga en cuenta que el número de teléfono es una cadena y puede incluir caracteres clave como paréntesis `()`, guiones `-` o caracteres para indicar identificadores de marcado secundario como extensiones `x`, por ejemplo, `1-353(0)18391111` o `+613 9403600x1234`. |
| `shippingAddressPhone.primary` | Indica si este es el número de teléfono principal de la dirección de envío. El valor siempre es `False`. |
| `userAccount` | Indica detalles de fidelidad, preferencias, procesos de inicio de sesión y otras preferencias de la cuenta. |
| `userAccount.startDate` | La fecha en la que se creó el perfil por primera vez. |

>[!NOTE]
>
>Cada registro de perfil también incluye el campo [`identityMap`](https://experienceleague.adobe.com/es/docs/experience-platform/xdm/field-groups/profile/identitymap), que incluye el ID de cliente de Commerce generado por el sistema como identificador principal del perfil y un ID de correo electrónico que se utiliza como identificador secundario.

Aprenda a [crear un esquema específico de un registro de perfil](profile-data.md) que pueda ingerir los datos de sus registros de perfil.
