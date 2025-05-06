---
title: Integración de [!DNL Page Builder]
description: Aprenda a utilizar [!DNL Product Recommendations] unidades en Page Builder.
feature: Services, Recommendations, Page Builder
exl-id: 001e8e1d-3590-4b44-b5f8-dd8b9b61f370
badgePaas: label="Solo PaaS" type="Informative" url="https://experienceleague.adobe.com/en/docs/commerce/user-guides/product-solutions" tooltip="Se aplica solo a proyectos de Adobe Commerce en la nube (infraestructura PaaS administrada por Adobe) y a proyectos locales."
source-git-commit: be1c739f3821a5f1e846b3026088e3a3ff45a60f
workflow-type: tm+mt
source-wordcount: '272'
ht-degree: 0%

---

# Integración de [!DNL Page Builder]

Las recomendaciones de productos se pueden integrar en cualquier contenido de Page Builder que implemente en su sitio.

>[!NOTE]
>
> Puede tener hasta 25 unidades de recomendación en una página nativa de Page Builder. Las páginas no nativas del Page Builder pueden tener hasta 5 unidades de recomendación. Consulte [Crear nueva recomendación](create.md) para obtener más información.

## Uso de Recommendations de productos con contenido de Page Builder

1. Cree una unidad de Recommendations en la vista de tienda predeterminada de un sitio web. Deben crearse en la vista de tienda predeterminada aunque tenga pensado usarlos en distintas vistas de tienda.

   >[!NOTE]
   >
   >Las métricas de las unidades de recomendación de Page Builder solo aparecen en la vista de tienda predeterminada [!DNL Product Recommendations] del espacio de trabajo. Aunque coloque una unidad de recomendación de Page Builder en una vista de tienda que no sea la vista de tienda predeterminada, las métricas relacionadas con esas unidades de recomendación de Page Builder no se mostrarán en el espacio de trabajo de la vista de tienda no predeterminada [!DNL Product Recommendations]. Para ver las métricas de Page Builder en un área de trabajo [!DNL Product Recommendations] de vista de tienda no predeterminada, abra y [edite](edit.md) la unidad de recomendación de Page Builder en la vista de tienda no predeterminada y, a continuación, haga clic en [!UICONTROL **Guardar**]. Las métricas de Page Builder ahora aparecen en el área de trabajo [!DNL Product Recommendations] en la vista de tienda no predeterminada.

1. En Page Builder, seleccione el widget de contenido Recomendaciones de productos y colóquelo en el sitio.

![Insertar unidad de recomendación](assets/pb-insert.png)

1. Haga clic en **Editar recomendación de producto**
1. Haga clic en **Seleccionar**
1. Seleccione la unidad de Recommendations creada anteriormente y haga clic en **Agregar selección**

![Insertar unidad de recomendación](assets/pb-select.png)

1. Realice las demás ediciones en el contenido de Page Builder y guarde los cambios.

En el momento del procesamiento, la unidad Recommendations respeta el contexto y el ámbito del contenido de Page Builder.
