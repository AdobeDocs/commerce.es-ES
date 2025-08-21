---
title: Crear una audiencia en Real-Time CDP con  [!DNL Commerce] datos de evento
description: Aprenda a utilizar  [!DNL Commerce] datos de evento para crear una audiencia en Real-Time CDP
role: Admin, Developer
feature: Personalization, Integration
exl-id: 0e9d286b-c459-44db-bbf8-2cb46e21739d
source-git-commit: a3e19940e2a3d8a240bb17703cfdd9903df311aa
workflow-type: tm+mt
source-wordcount: '1026'
ht-degree: 0%

---

# Crear audiencias en Real-Time CDP utilizando [!DNL Commerce] datos de evento

Utilice los datos de evento capturados del almacén de [!DNL Commerce] para crear audiencias en Real-Time CDP. Los datos capturados se basan en el comportamiento de navegación, compras anteriores, atributos de perfil, tendencias de conversión o cancelación, estado de lealtad, valor de cliente alto y bajo, etc.

## ¿Qué datos debo considerar al usar?

Cree audiencias en Real-Time CDP con datos de eventos de tienda, back office y perfil.

| Tipos de datos | Datos De Tienda (Eventos De Comportamiento) | Datos del back office (eventos del lado del servidor) | Datos de segmentos y perfil del cliente |
|---|---|---|---|
| **Definición** | Clics o acciones que los clientes realizan en el sitio. | Información sobre el ciclo de vida y detalles de cada pedido (anterior y actual). | Quiénes son sus compradores y para qué segmentos cumplen los requisitos. |
| **Eventos capturados por Adobe Commerce** | `productPageView`<br>`addToCart` | `placeOrder`<br>`orderplaced`<br>`orderLineItemRefunded`<br>`order Canceled`<br>`order history` | `createAccount`<br>`editAccount`<br>`Profile Record` |

## ¿Qué han conseguido otros clientes?

Los clientes de Adobe [!DNL Commerce] han logrado un impacto comercial significativo al activar audiencias creadas en Real-Time CDP e implementarlas en su instancia de [!DNL Commerce].

Un retailer global de ropa multimarca logró:

- Una fuente fiable con 10 millones de perfiles de clientes unificados
- Se han creado más de 40 audiencias únicas de &quot;clientes de alta intención&quot; para interactuar con todos los canales

Una compañía global de bebidas recopiló:

- 98 millones de perfiles de clientes de más de 100 países

## Vamos a empezar.

En este artículo, aprenderá lo siguiente:

- Cree una audiencia en Real-Time CDP basada en los datos de [!DNL Commerce] que recopilan los eventos
- Active esa audiencia para su tienda [!DNL Commerce]
- Usar la audiencia de [!DNL Commerce] para informar una regla de precios del carro de compras

>[!IMPORTANT]
>
>Complete las tareas descritas en este artículo usando su entorno de espacio aislado [!DNL Commerce]. Esto garantiza que los datos de evento de la tienda y del back office que envía a Experience Platform no diluyan los datos de evento de producción.

### Requisitos previos

Antes de empezar, asegúrese de lo siguiente:

- Se le ha aprovisionado para utilizar Real-Time CDP. Si no está seguro, póngase en contacto con el integrador de sistemas o con el equipo de desarrollo que administra los proyectos y entornos.
- Ha [instalado](install.md) y [configurado](connect-data.md) la extensión [!DNL Data Connection] en [!DNL Commerce].
- Usted [confirmó](connect-data.md#confirm-that-event-data-is-collected) que sus datos de evento de [!DNL Commerce] están llegando al perímetro de Experience Platform.

### &#x200B;1. Crear una audiencia

Una audiencia es un conjunto de clientes que comparten un comportamiento o características similares. En este ejercicio, crea una audiencia que clasifica a las personas interesadas en un producto en particular de su tienda.

Para simplificar este ejercicio, se utilizan datos de evento del evento `productPageView`. Este evento captura detalles sobre el producto que se visualizó, como el nombre del producto, el SKU, el precio, etc.

Utilice estos datos de evento para especificar que la audiencia incluye personas que tienen al menos un evento de &quot;Vistas del producto&quot; en el que el SKU (identificador de producto) es igual a un producto específico del sitio y el evento se produce en el último día. palo de golf

1. Abra Experience Platform y seleccione **[!UICONTROL Audiences]** en el menú de navegación de la izquierda.

   ![Tablero de audiencia](assets/audience-left-rail.png)

1. Haga clic en **[!UICONTROL Create Audience]**.

   ![Crear audiencia](assets/browse-create-audience.png)

   Se muestra el área de trabajo **Generador de segmentos**.

1. En el área de trabajo **Generador de segmentos**, seleccione el método de creación **Generar regla**.

   ![Generar regla](assets/build-rule.png)

   El área de trabajo **Generador de segmentos** es donde usted define las reglas y condiciones para su audiencia.&#x200B; Estas reglas y condiciones se basan en datos de evento y perfil de la tienda Commerce y definen los criterios que determinan si un usuario cumple los requisitos para la audiencia. Por ejemplo, puede crear una regla que incluya a los usuarios que han visto un producto específico o a los usuarios que han realizado una compra en un lapso de tiempo determinado. Más información sobre [Generador de segmentos](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/ui/segment-builder) y las reglas y condiciones.

1. Seleccione la ficha [Eventos](https://experienceleague.adobe.com/es/docs/experience-platform/segmentation/ui/segment-builder#events).

   ![Ficha Eventos](assets/audience-events-tab.png)

1. Busque el tipo de evento &quot;Vistas del producto&quot;. A continuación, arrástrelo y suéltelo en el área de trabajo **Generador de segmentos**.

1. Vuelva a la ficha **Eventos** y busque &quot;SKU&quot;, que es el campo de datos en el campo `productListItems`. Arrástrelo y suéltelo en el área de trabajo **Generador de segmentos** sobre el evento **Vista de producto**.

   Se muestra la sección **Reglas de evento** donde puede especificar el producto específico con el que desea generar su audiencia.

   ![Seleccionar SKU](assets/audience-addsku.png)

1. Establezca el intervalo de tiempo en un día. Para ello, haga clic en **Cualquier hora** y seleccione *En los últimos* con un valor de *1*.

   Al crear una audiencia, puede especificar un intervalo de tiempo para capturar la actividad reciente. La configuración de un intervalo de tiempo permite dirigirse a los usuarios en función de sus interacciones o comportamientos recientes dentro de un periodo de tiempo específico.

1. En la sección **Propiedades de audiencia** en el lado derecho del área de trabajo, establezca las propiedades de audiencia proporcionando un nombre, una descripción y un método de evaluación para la audiencia.

1. Para guardar la audiencia, haga clic en **[!UICONTROL Save and Close]**.

   Los detalles de la audiencia se mostrarán en el panel **Audiencia**.

### &#x200B;2. Activar la audiencia en el destino [!DNL Commerce]

Una audiencia está disponible en [!DNL Commerce] al activarla para el destino [!DNL Commerce].

>[!IMPORTANT]
>
>Si aún no ha establecido [!DNL Commerce] como destino disponible para recibir datos, consulte el tema [Adobe [!DNL Commerce] Conexión](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/catalog/personalization/adobe-commerce).

1. En la ficha **Detalles** de la audiencia, haga clic en **Activar en destino**.

1. Seleccione su destino [!DNL Commerce]. A continuación, haga clic en **Siguiente**.

1. Complete el proceso de activación haciendo clic en **[!UICONTROL Finish]**.

## &#x200B;3. Vea la audiencia en el panel de audiencias

En [!DNL Commerce], puede ver todas las [audiencias activas](https://experienceleague.adobe.com/es/docs/experience-platform/destinations/ui/activate/activate-edge-personalization-destinations) que se pueden personalizar para su instancia de [!DNL Commerce] mediante el panel **Audiencias de Real-Time CDP**.

Para acceder al panel de **Audiencias de Real-Time CDP**, ve a la barra lateral de _Administración_ y luego ve a **[!UICONTROL Customers]** > **[!UICONTROL Real-time CDP Audience]**.

En el tablero, busque la audiencia que ha creado. Tenga en cuenta que no se utiliza en una regla de precios de carro de compras o en un bloque dinámico. En la siguiente sección, vincula la audiencia a una regla de precios del carro de compras.

![Panel de audiencias de Real-Time CDP](assets/real-time-cdp-dashboard.png)

### &#x200B;4. Cree una regla de precios de carro basada en la audiencia

Esta sección muestra cómo crear una regla de precios de carro de compras basada en la nueva audiencia.

1. Confirme que la nueva audiencia se mostrará en el tablero **Audiencias de Real-Time CDP**.
1. [Crear una regla de precios de carro de compras](https://experienceleague.adobe.com/es/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart-create).
1. [Establezca la condición](https://experienceleague.adobe.com/es/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart-create#use-real-time-cdp-audiences-to-set-a-condition) de la regla de precio del carro de compras con su nueva audiencia.
1. [Establece la acción](https://experienceleague.adobe.com/es/docs/commerce-admin/marketing/promotions/cart-rules/price-rules-cart-create#step-3-define-the-actions) que desea que tenga lugar cuando se agregue el producto al carro de compras.
1. Continúe configurando la regla de precios del carro de compras.
1. Vaya a la vista del cliente de la instancia de zona protegida.
1. Añada al carro de compras el producto en el que basó la audiencia. Observe que la regla de precios del carro de compras está habilitada.

## Ajustar

En este ejercicio, creó una audiencia en Real-Time CDP y la activó en el destino [!DNL Commerce]. A continuación, en el administrador de [!DNL Commerce], creó una regla de precio de carro de compras basada en esa audiencia y habilitó la regla en su entorno de zona protegida.
