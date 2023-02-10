---
title: Filtros
description: Aprenda a utilizar filtros.
exl-id: eb683dfe-9a90-400a-a0c0-3dc00d1f28b5
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '354'
ht-degree: 0%

---

# Filtros

Se pueden agregar uno o más filtros para limitar los datos que se usan para generar un informe. Cada filtro es una expresión que incluye una columna de la tabla asociada, un operador y un valor. Por ejemplo, para incluir solo clientes repetidos, puede crear un filtro que incluya solo los clientes que hayan realizado más de un pedido. Se pueden usar varios filtros con `AND/OR` para agregar lógica al informe.

>[!TIP]
>
>Un informe puede tener un máximo de 3500 puntos de datos. Para reducir el número de puntos de datos, utilice un filtro para reducir la cantidad de datos que se utiliza para generar el informe.

MBI incluye una selección de filtros que puede utilizar &quot;fuera de la caja (OOTB)&quot; o modificarlos para adaptarlos a sus necesidades. No hay límite en el número de filtros que se pueden crear.

## Para agregar un filtro:

1. En el gráfico, pase el ratón sobre cada punto de datos.

   En este informe, cada punto de datos muestra la cantidad total de clientes para el mes.

1. En el panel izquierdo, haga clic en Filtros (![](../../assets/magento-bi-btn-filter.png)).

   ![Agregar filtro](../../assets/magento-bi-report-builder-filter-add.png)

1. Haga clic en **[!UICONTROL Add Filter]**.

   Los filtros se numeran alfabéticamente y el primero es `[A]`. Las dos primeras partes del filtro son opciones desplegables y la tercera parte es un valor.

   ![](../../assets/magento-bi-report-builder-filter-add-a.png)

   * Haga clic en la primera parte del filtro y seleccione la columna que desee utilizar como asunto de la expresión.

      ![Elegir primera parte del filtro](../../assets/magento-bi-report-builder-filter-part1.png)

   * Haga clic en la segunda parte del filtro y seleccione el operador .

      ![Seleccione el operador](../../assets/magento-bi-report-builder-filter-part2.png)

   * En la tercera parte del filtro, introduzca el valor necesario para completar la expresión.

      ![Introduzca el valor](../../assets/magento-bi-report-builder-filter-part3.png)

   * Cuando haya completado el filtro, haga clic en **[!UICONTROL Apply]**.

      Ahora, el informe solo incluye a los clientes habituales y el número de registros de cliente recuperados para el informe se ha reducido de 33.000 a 12.600.

      ![Informe filtrado](../../assets/magento-bi-report-builder-filter-report.png)<!--{: .zoom}-->

1. En la barra lateral, haga clic en la perspectiva ( ![](../../assets/magento-bi-btn-perspective.png)).

   ![Perspectiva](../../assets/magento-bi-report-builder-filter-perspective.png)<!--{: .zoom}-->

1. En la lista de configuraciones, elija `Cumulative`. A continuación, haga clic en **[!UICONTROL Apply]**.

   ![Perspectiva acumulada](../../assets/magento-bi-report-builder-filter-perspective-cumulative.png)

   La variable `Cumulative` Perspectiva distribuye el cambio a lo largo del tiempo, en lugar de mostrar los magullados arriba y abajo de cada mes.

1. Escriba un `Title` para el informe y haga clic en **[!UICONTROL Save]** como `Chart` al tablero.

   ![Guardar en tablero](../../assets/magento-bi-report-builder-filter-perspective-cumulative-save.png)
