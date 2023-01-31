---
title: Administración de dimensiones de datos
description: Descubra cómo se generan los datos, qué hace exactamente que se inserte una nueva fila en uno de los principales negocios, cómo se registran acciones como realizar una compra o crear una cuenta en la base de datos de comercio.
exl-id: 143a4b1e-2e6f-438a-90e6-bdda13b39cb9
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '463'
ht-degree: 0%

---

# Administración de dimensiones de datos

>[!NOTE]
>
>Requiere [Permisos de administrador](../../administrator/user-management/user-management.md).

Una dimensión es un campo de la misma tabla que una métrica que puede utilizarse para filtrar o segmentar gráficos basados en esa métrica. Por ejemplo, una métrica de ingresos puede contener ciudad, estado, país, estado de pedido, código de cupón y otros tipos de dimensiones.

## Añadir dimensiones a varias métricas

Para agregar una o más dimensiones a varias métricas a la vez:

1. En la barra de navegación principal, vaya a **[!UICONTROL Manage Data > Metrics]**.

1. En la parte superior de la página, haga clic en **[!UICONTROL Add Dimensions To Metric(s)]**.

1. Elija la tabla que contiene las dimensiones.

1. En el `Choose Metric(s) to Add Dimensions` , seleccione las métricas a las que desee agregar dimensiones. Una vez seleccionada, la variable `Choose Dimensions to Add` a la derecha. Marque las dimensiones que desee agregar a la métrica seleccionada.

   ![](../../assets/Add_Dimensions.png)

1. Si desea segmentar o agrupar por cualquiera de las dimensiones de datos de los informes, asegúrese de indicar que se encuentran _Agrupable_.

1. Haga clic en **[!UICONTROL Add]**.

## Eliminar dimensiones de varias métricas

Para eliminar una o más dimensiones de varias métricas:

1. En la barra de navegación principal, vaya a **[!UICONTROL Data > Metrics]**.

1. En la parte superior de la página, haga clic en **[!UICONTROL Remove Dimensions From Metric(s)]**.

1. Elija la tabla que contiene las dimensiones.

1. Seleccione las métricas de las que desea eliminar las dimensiones a la izquierda y las dimensiones que desea eliminar a la derecha.

1. Haga clic en **[!UICONTROL Remove]**.

1. Si las dimensiones están en uso en los informes, se mostrará una advertencia y una lista de gráficos que están usando las dimensiones. Haga clic en **[!UICONTROL Delete]** para eliminar las dimensiones comprobadas y todos sus dependientes, incluidos los informes.

## Administración de dimensiones en métricas

**Para añadir dimensiones en una métrica:**

1. En la barra de navegación principal, vaya a **[!UICONTROL Data > Metrics]**.

1. Haga clic en **[!UICONTROL Edit]** en la métrica desea una nueva dimensión.

1. En el `Dimensions` utilice la `Add a dimension` lista desplegable para seleccionar una dimensión que agregar.

>[!NOTE]
>
>Las dimensiones por las que desee filtrar o agrupar ya deben rastrearse en [!DNL MBI]. Si no encuentra la dimensión deseada, es posible que tengamos que empezar a rastrear una nueva columna de datos en la base de datos a través del [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) página.


**Para eliminar dimensiones de una métrica:**

1. En la barra de navegación principal, vaya a **[!UICONTROL Manage Data > Metrics]**.

1. Haga clic en **[!UICONTROL Edit]** en la métrica desea una nueva dimensión.

1. En el `Dimensions` , seleccione la casilla de verificación de la columna eliminar situada junto a las dimensiones que desea eliminar.

>[!NOTE]
>
>Incluso después de eliminar una dimensión, sigue existiendo como una columna de la tabla en nuestro almacén de datos. Puede volver a agregarla a cualquier métrica y crear nuevas métricas utilizando estas dimensiones. Para eliminar la columna de datos a la que corresponde una dimensión [!DNL MBI], solo tiene que cancelar el seguimiento de la columna de datos mediante la función [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) página.

## Documentación relacionada

* [Prácticas recomendadas para la segmentación y el filtrado](../../best-practices/segment-filter.md)
