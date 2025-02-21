---
title: Usar Adobe Journey Optimizer para enviar un correo electrónico de carro de compras abandonado
description: Aprenda a utilizar Adobe Journey Optimizer para enviar un correo electrónico de carro de compras abandonado.
role: Admin, Developer
feature: Personalization, Integration
source-git-commit: cb69e11cd54a3ca1ab66543c4f28526a3cf1f9e1
workflow-type: tm+mt
source-wordcount: '1262'
ht-degree: 0%

---

# Usar Adobe Journey Optimizer para enviar un correo electrónico de carro de compras abandonado

Obtenga información sobre cómo enviar un correo electrónico de renovación de la participación personalizado o una notificación si se ha abandonado una sesión del carro de compras o del explorador. En este artículo, se utilizan datos generados a partir de clientes que han visto una serie de productos y categorías, que han interactuado con un producto o que han invertido tiempo en una página.

## ¿Qué datos debo considerar al usar?

Cree un carro de compras abandonado, examine el correo electrónico o las notificaciones con datos de eventos de tienda y back office.

| Tipos de datos | Datos De Tienda (Eventos De Comportamiento) | Datos del back office (eventos del lado del servidor) |
|---|---|---|
| **Definición** | Clics o acciones que los clientes realizan en el sitio. | Información sobre el ciclo de vida y detalles de cada pedido (anterior y actual). |
| **Eventos capturados por Adobe Commerce** | [pageView](https://experienceleague.adobe.com/en/docs/commerce/data-connection/event-forwarding/events#pageview)<br>[productPageView](https://experienceleague.adobe.com/en/docs/commerce/data-connection/event-forwarding/events)<br>[addToCart](https://experienceleague.adobe.com/en/docs/commerce/data-connection/event-forwarding/events#addtocart)<br>[openCart](https://experienceleague.adobe.com/en/docs/commerce/data-connection/event-forwarding/events#opencart)<br>[startCheckout](https://experienceleague.adobe.com/en/docs/commerce/data-connection/event-forwarding/events#startcheckout)<br>[completeCheckout](https://experienceleague.adobe.com/en/docs/commerce/data-connection/event-forwarding/events#completecheckout) | [pedido realizado](https://experienceleague.adobe.com/en/docs/commerce/data-connection/event-forwarding/events-backoffice#orderplaced)<br>[Historial de pedidos](https://experienceleague.adobe.com/en/docs/commerce/data-connection/fundamentals/connect-data#send-historical-order-data) |

### ¿Qué han conseguido otros clientes?

Los clientes de Adobe [!DNL Commerce] han logrado un impacto comercial significativo al implementar campañas de abandono personalizadas con Adobe [!DNL Commerce], Adobe [!DNL Journey Optimizer] y Adobe [!DNL Real-Time CDP].

Un minorista de ropa global y multimarca logró:

- Conversión 1.9x al hacer clic desde nuevas campañas
- Aumento del 57 % en los ingresos procedentes de los recorridos de abandono omnicanal
- Aumento del 41 % en la tasa de conversión de las campañas de renovación de la participación
- Más de 1000 nuevos compradores comprometidos por semana

Una compañía global de bebidas logró:

- Tasas de apertura de correo electrónico de renovación de participación del 36 %
- Aumento del 21 % en las tasas de clics
- Aumento del 8,5 % en la tasa de conversión
- El 89% de los abandonadores que vuelven a comprometerse convierten

## Vamos a empezar.

Este caso de uso en particular se centra en la creación de un correo electrónico de carro de compras abandonado mediante los datos de su instancia de [!DNL Commerce] y el envío a Adobe [!DNL Journey Optimizer].

### ¿Qué es Adobe Journey Optimizer?

[Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/get-started.html) le ayuda a personalizar la experiencia comercial de sus compradores. Por ejemplo, puede utilizar Journey Optimizer para crear y enviar campañas de marketing programadas, como promociones semanales de una tienda minorista, o generar un correo electrónico de carro de compras abandonado si un cliente agregó un producto a un carro de compras pero luego no completó el proceso de cierre de compra.

En este tema, aprenderá a generar un correo electrónico de carro de compras abandonado al escuchar un evento `checkout` generado desde la instancia [!DNL Commerce] y al responder a ese evento en Journey Optimizer.

>[!IMPORTANT]
>
>Para fines de demostración, use su entorno de espacio aislado [!DNL Commerce] para no diluir los datos del evento de producción con los datos del evento de tienda y del back office que envía a Experience Platform.

### Requisitos previos

Antes de comenzar con estos pasos, asegúrese de lo siguiente:

- Se le ha proporcionado el uso de Adobe [!DNL Journey Optimizer]. Si no está seguro, póngase en contacto con el integrador de sistemas o con el equipo de desarrollo que administra los proyectos y entornos.
- Ha [instalado](install.md) y [configurado](connect-data.md) la extensión [!DNL Data Connection] en [!DNL Commerce].
- Usted [confirmó](connect-data.md#confirm-that-event-data-is-collected) que sus datos de evento de [!DNL Commerce] están llegando al perímetro de Experience Platform.

## Paso 1: Crear un usuario en el entorno de espacio aislado [!DNL Commerce]

Cree un usuario en el entorno de zona protegida y confirme que la información de esa cuenta de usuario aparece en Experience Platform. Asegúrese de que el correo electrónico especificado sea válido, ya que se utiliza más adelante en esta sección para enviar el correo electrónico del carro de compras abandonado.

1. Inicie sesión o cree una cuenta en su entorno de espacio aislado de [!DNL Commerce].

   ![Inicia sesión en tu cuenta de prueba](assets/sign-in-account.png){width="700" zoomable="yes"}

   Con la extensión [!DNL Data Connection] instalada y configurada, esta información de cuenta se envía a Experience Platform como perfil.

1. Confirme que la información de su cuenta de usuario aparece en la sección **[!UICONTROL Profile]** de Experience Platform.

   Ir a **[!UICONTROL Profiles]** en Adobe Experience Platform. Haga clic en **[!UICONTROL Detail]** en el perfil para ver el perfil que ha creado.

   ![Confirmar perfil](assets/check-event-profile.png){width="700" zoomable="yes"}

## Paso 2: Ver eventos en Journey Optimizer

En su entorno de espacio aislado [!DNL Commerce], déclencheur eventos en su tienda mediante la visualización de páginas de productos, la adición de elementos a un carro de compras y la realización de otras actividades que realizaría un comprador. A continuación, confirme que estos eventos fluyen a Journey Optimizer.

1. Iniciar [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/user-interface.html).
1. Seleccione **[!UICONTROL Profiles]**.
1. Establezca **[!UICONTROL Identity namespace]** en `Email`.
1. Establezca **[!UICONTROL Identity value]** en su dirección de correo electrónico.
1. Seleccione su perfil y, a continuación, seleccione la ficha **[!UICONTROL Events]**.

   ![Comprobar detalles del evento](assets/check-event-details.png){width="700" zoomable="yes"}

   Busque el evento `commerce.checkouts` y examine la carga útil del evento:

   ```json
   "personID": "84281643067178465783746543501073369488", 
   "eventType": "commerce.checkouts", 
   "_id": "4b41703f-e42e-485b-8d63-7001e3580856-0", 
   "commerce": { 
       "cart": {}, 
       "checkouts": { 
           "value": 1 
       } 
   ```

   Como puede ver, la carga útil de evento completa contiene datos de evento enriquecidos. En la siguiente sección, configurará eventos en Journey Optimizer para detectar y responder al evento `commerce.checkouts` generado desde la tienda [!DNL Commerce].

## Paso 3: Configuración de eventos en Journey Optimizer

Configure dos eventos en Journey Optimizer: un evento escucha el evento `commerce.checkouts` desde Commerce y el otro es un evento de tiempo de espera básico que espera una cantidad de tiempo específica para pasar antes de activar un correo electrónico de carro de compras abandonado.

### Crear un evento de escucha

1. Iniciar [Adobe Journey Optimizer](https://experienceleague.adobe.com/docs/journey-optimizer/using/get-started/user-interface.html).

1. Haga clic en **[!UICONTROL Configurations]** en la sección **[!UICONTROL Administration]** del panel izquierdo.

1. En el mosaico **[!UICONTROL Events]**, haga clic en **[!UICONTROL Manage]**.

   ![Configuración de evento de Journey Optimizer](assets/ajo-config.png){width="700" zoomable="yes"}

1. En la página **[!UICONTROL Events]**, haga clic en **[!UICONTROL Create Event]**.

1. En el panel de navegación derecho, configure el evento de la siguiente manera:

   1. Establezca **[!UICONTROL Name]** en: `firstname_lastname_checkout`.
   1. Establezca **[!UICONTROL Type]** en **[!UICONTROL Unitary]**.
   1. Establecer **[!UICONTROL Event id typ]e** en **[!UICONTROL Rule based]**.
   1. Establezca **[!UICONTROL Schema]** en su [!DNL Commerce] [esquema](update-xdm.md).
   1. Seleccione **[!UICONTROL Fields]** para abrir la página **[!UICONTROL Fields]**. A continuación, seleccione los campos útiles para este evento. Por ejemplo, seleccione todos los campos bajo **[!UICONTROL Product list items]**, **[!UICONTROL Commerce]**, **[!UICONTROL eventType]** y **[!UICONTROL Web]**.
   1. Haga clic en **[!UICONTROL OK]** para guardar los campos seleccionados.
   1. Haga clic dentro del campo **[!UICONTROL Event id condition]**. A continuación, cree una condición: `eventType` es igual a `commerce.checkouts` Y `personalEmail.address` es igual a la dirección de correo electrónico que utilizó cuando creó el perfil en la sección anterior.

      ![Condición del conjunto de Journey Optimizer](assets/ajo-set-condition.png){width="700" zoomable="yes"}

   1. Haga clic en **[!UICONTROL OK]**.
   1. Haga clic **[!UICONTROL Save]** para guardar el evento.

### Creación de un evento de tiempo de espera

1. Cree un evento en Journey Optimizer como lo hizo anteriormente.

1. En el panel de navegación derecho, configure el evento de la siguiente manera:

   1. Establezca **[!UICONTROL Name]** en: `firstname_lastname_timeout`.
   1. Establezca **[!UICONTROL Type]** en **[!UICONTROL Unitary]**.
   1. Establezca **[!UICONTROL Event id type]** en **[!UICONTROL Rule based]**.
   1. Establezca **[!UICONTROL Schema]** en su [!DNL Commerce] [esquema](update-xdm.md).
   1. Establezca **[!UICONTROL Schema]**, **[!UICONTROL Fields]** y **[!UICONTROL Event id condition]** en el mismo valor que arriba.
   1. Haga clic **[!UICONTROL Save]** para guardar el evento.

Con estos dos eventos configurados, cree un recorrido que envíe un correo electrónico del carro de compras abandonado.

## Paso 4: Crear un recorrido de cierre de compra

Cree un recorrido que escuche el evento `commerce.checkouts` y luego envíe un correo electrónico de carro de compras abandonado después de que haya transcurrido un tiempo determinado.

1. En Journey Optimizer, seleccione **[!UICONTROL Journeys]** en **J[!UICONTROL OURNEY MANAGEMENT]**.
1. Haga clic en **[!UICONTROL Create Journey]**.
1. Especifique el nombre del recorrido.
1. Haga clic en **[!UICONTROL OK]** para guardar el recorrido.
1. En el panel de navegación izquierdo bajo la sección **[!UICONTROL EVENTS]**, busque el evento de cierre de compra que creó anteriormente: `firstname_lastname_checkout` y arrástrelo y suéltelo en el lienzo.

   >[!TIP]
   >
   >Al hacer doble clic en el evento, se agrega automáticamente al lienzo.

1. Busque el evento de tiempo de espera y añádalo al lienzo.
1. Haga doble clic en el evento de tiempo de espera.

   1. En la sección **[!UICONTROL Timeout]**, seleccione la casilla de verificación **[!UICONTROL Define the event time]**.
   1. En el campo **[!UICONTROL Wait for]**, escriba `1` y `Minute`.
   1. Seleccione la casilla de verificación **[!UICONTROL Set a timeout path]**.

   Con esta configuración de tiempo de espera, un comprador que realiza un cierre de compra pero no completa el pedido en un minuto déclencheur esta rama de tiempo de espera. En un entorno de producción real, establecería esto para un período más largo, como de 24 horas.

1. En el panel de navegación izquierdo bajo **[!UICONTROL ACTIONS]**, agregue la acción **[!UICONTROL Email]** a la rama de tiempo de espera. El recorrido debería tener el siguiente aspecto:

   ![Lienzo de Journey Optimizer](assets/ajo-canvas.png){width="700" zoomable="yes"}

### Crear un correo electrónico de carro de compras abandonado

Cree un correo electrónico de carro de compras abandonado que se enviará cuando se detecte un carro de compras abandonado.

1. En el recorrido que creó anteriormente, haga doble clic en el icono **[!UICONTROL Email]** del lienzo.

1. Siga los [pasos](https://experienceleague.adobe.com/docs/journey-optimizer/using/content-management/personalization/personalization-use-cases/personalization-use-case-helper-functions.html#configure-email) de la guía de Journey Optimizer para crear el correo electrónico del carro de compras abandonado.

Ahora tiene un recorrido en Journey Optimizer que escucha el evento `commerce.checkouts` desde su tienda [!DNL Commerce] y un mensaje de correo electrónico del carro de compras abandonado que se envía después de que transcurra un período de tiempo. La siguiente sección muestra cómo probar el recorrido.

## Paso 5: Déclencheur del evento de cierre de compra en tiempo real

En esta sección, probará el evento en tiempo real.

1. En Journey Optimizer, active el modo de prueba.

   ![Habilitar modo de prueba](assets/ajo-enable-test.png){width="700" zoomable="yes"}

1. Para probar este recorrido en tiempo real, abra otra pestaña del explorador y vaya al sitio web de [!DNL Commerce] en su entorno de espacio aislado.

   1. Añadir un producto al carro de compras.
   1. Vaya a la página de cierre de compra.
   1. En la página de cierre de compra, abandone el carro de compras volviendo a la página principal o cerrando la pestaña.

      El recorrido se activa. Para confirmarlo, abra la pestaña que tenga el recorrido en Journey Optimizer. Debería ver una flecha verde que muestra la ruta que siguió el usuario.

1. Busque el correo electrónico en su bandeja de entrada.
