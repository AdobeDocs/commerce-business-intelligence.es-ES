---
title: Administración de dimensiones de datos
description: Descubra qué es una dimensión y cómo se puede utilizar para filtrar o segmentar gráficos basados en una métrica.
exl-id: 143a4b1e-2e6f-438a-90e6-bdda13b39cb9
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '412'
ht-degree: 0%

---

# Administración de dimensiones de datos

>[!NOTE]
>
>Requiere [permisos de administrador](../../administrator/user-management/user-management.md).

Una dimensión es un campo de la misma tabla que una métrica que se puede utilizar para filtrar o segmentar gráficos basados en esa métrica. Por ejemplo, una métrica de ingresos puede contener ciudad, estado, país, estado del pedido, código de cupón y otros tipos de dimensiones.

## Adición de dimensiones a varias métricas

Para agregar una o más dimensiones a varias métricas a la vez:

1. Ir a **[!UICONTROL Manage Data > Metrics]**.

1. Haga clic en **[!UICONTROL Add Dimensions To Metric(s)]**.

1. Elija la tabla que contiene las dimensiones.

1. En la columna `Choose Metric(s) to Add Dimensions`, seleccione las métricas a las que desee agregar dimensiones. Una vez seleccionada, la columna `Choose Dimensions to Add` aparece a la derecha. Compruebe las dimensiones que desea agregar a la métrica seleccionada.

   ![](../../assets/Add_Dimensions.png)

1. Si desea segmentar o agrupar por cualquiera de las dimensiones de datos en los informes, asegúrese de indicar que se pueden _agrupar_.

1. Haga clic en **[!UICONTROL Add]**.

## Eliminar dimensiones de varias métricas

Para eliminar una o más dimensiones de varias métricas:

1. Ir a **[!UICONTROL Data > Metrics]**.

1. Haga clic en **[!UICONTROL Remove Dimensions From Metric(s)]**.

1. Elija la tabla que contiene las dimensiones.

1. Seleccione las métricas de las que desea eliminar las dimensiones a la izquierda, y las dimensiones que desea eliminar a la derecha.

1. Haga clic en **[!UICONTROL Remove]**.

1. Si las dimensiones están en uso en los informes, se muestra una advertencia con la lista de gráficos que utilizan las dimensiones. Haga clic en **[!UICONTROL Delete]** para eliminar las dimensiones seleccionadas y todas sus dependientes, incluidos los informes.

## Administración de dimensiones en métricas

**Para agregar dimensiones en una métrica:**

1. Ir a **[!UICONTROL Data > Metrics]**.

1. Haga clic en **[!UICONTROL Edit]** en la métrica para la que desee una nueva dimensión.

1. En la sección `Dimensions`, utilice el menú desplegable `Add a dimension` para seleccionar una dimensión que agregar.

>[!NOTE]
>
>Cualquier dimensión por la que desee filtrar o agrupar ya debe estar rastreada en [!DNL Commerce Intelligence]. Si no encuentra la dimensión deseada, es posible que tenga que iniciar el seguimiento de una nueva columna de datos en la base de datos a través de la página [Data Warehouse](../data-warehouse-mgr/tour-dwm.md).


**Para eliminar dimensiones de una métrica:**

1. Ir a **[!UICONTROL Manage Data > Metrics]**.

1. Haga clic en **[!UICONTROL Edit]** en la métrica para la que desee una nueva dimensión.

1. En la sección `Dimensions`, active la casilla de verificación de la columna Eliminar situada junto a las dimensiones que desee eliminar.

>[!NOTE]
>
>Incluso después de eliminar una dimensión, sigue existiendo como una columna en la tabla de Data Warehouse. Puede volver a agregarlo a cualquier métrica y crear nuevas métricas con estas dimensiones. Para quitar la columna de datos a la que corresponde una dimensión de [!DNL Commerce Intelligence], simplemente quite el seguimiento de la columna de datos a través de la página [Data Warehouse](../data-warehouse-mgr/tour-dwm.md).

## Documentación relacionada

* [Prácticas recomendadas para segmentación y filtrado](../../best-practices/segment-filter.md)
