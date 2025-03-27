---
title: Filtros
description: Aprenda a utilizar los filtros.
exl-id: eb683dfe-9a90-400a-a0c0-3dc00d1f28b5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 0854d644cb72b3fc8b8b31a0bf7e8dca4cc99724
workflow-type: tm+mt
source-wordcount: '356'
ht-degree: 0%

---

# Filtros

Se pueden añadir uno o más filtros para limitar los datos que se utilizan para generar un informe. Cada filtro es una expresión que incluye una columna de la tabla asociada, un operador y un valor. Por ejemplo, para incluir solo clientes repetidos, puede crear un filtro que incluya solo clientes que hayan realizado más de un pedido. Se pueden usar varios filtros con operadores lógicos `AND/OR` para agregar lógica al informe.

>[!TIP]
>
>Un informe puede tener un máximo de 3500 puntos de datos. Para reducir el número de puntos de datos, utilice un filtro para reducir la cantidad de datos que se utilizan para generar el informe.

[!DNL Adobe Commerce Intelligence] incluye una selección de filtros que puede usar &quot;listos para usar (OOTB)&quot; o modificar para adaptarlos a sus necesidades. No hay límite en el número de filtros que se pueden crear.

## Para añadir un filtro:

1. En el gráfico, pase el ratón sobre cada punto de datos.

   En este informe, cada punto de datos muestra la cantidad total de clientes durante el mes.

1. En el panel izquierdo, haga clic en el icono Filtros (![](../../assets/magento-bi-btn-filter.png)).

   ![Agregar filtro](../../assets/magento-bi-report-builder-filter-add.png)

1. Haga clic en **[!UICONTROL Add Filter]**.

   Los filtros se numeran alfabéticamente y el primero es `[A]`. Las dos primeras partes del filtro son opciones desplegables y la tercera parte es un valor.

   ![](../../assets/magento-bi-report-builder-filter-add-a.png)

   * Haga clic en la primera parte del filtro y elija la columna que desea utilizar como asunto de la expresión.

     ![Elegir la primera parte del filtro](../../assets/magento-bi-report-builder-filter-part1.png)

   * Haga clic en la segunda parte del filtro y seleccione el operador.

     ![Elija el operador](../../assets/magento-bi-report-builder-filter-part2.png)

   * En la tercera parte del filtro, introduzca el valor necesario para completar la expresión.

     ![Escriba el valor](../../assets/magento-bi-report-builder-filter-part3.png)

   * Una vez completado el filtro, haga clic en **[!UICONTROL Apply]**.

     Ahora, el informe solo incluye clientes que repiten y el número de registros de clientes recuperados para el informe se ha reducido de 33 000 a 12 600.

     ![Informe filtrado](../../assets/magento-bi-report-builder-filter-report.png)<!--{: .zoom}-->

1. En la barra lateral, haga clic en el icono de perspectiva (![Icono de perspectiva](../../assets/magento-bi-btn-perspective.png)).

   ![Perspectiva](../../assets/magento-bi-report-builder-filter-perspective.png)<!--{: .zoom}-->

1. En la lista de configuraciones, elija `Cumulative`. A continuación, haga clic en **[!UICONTROL Apply]**.

   ![Perspectiva acumulativa](../../assets/magento-bi-report-builder-filter-perspective-cumulative.png)

   La perspectiva `Cumulative` distribuye el cambio con el paso del tiempo, en lugar de mostrar los desgloses desglosados de cada mes.

1. Escriba un(a) `Title` para el informe y haga clic en **[!UICONTROL Save]** como `Chart` en el tablero.

   ![Guardar en el panel](../../assets/magento-bi-report-builder-filter-perspective-cumulative-save.png)
