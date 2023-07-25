---
title: Filtros
description: Aprenda a utilizar los filtros.
exl-id: eb683dfe-9a90-400a-a0c0-3dc00d1f28b5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '351'
ht-degree: 0%

---

# Filtros

Se pueden añadir uno o más filtros para limitar los datos que se utilizan para generar un informe. Cada filtro es una expresión que incluye una columna de la tabla asociada, un operador y un valor. Por ejemplo, para incluir solo clientes repetidos, puede crear un filtro que incluya solo clientes que hayan realizado más de un pedido. Se pueden utilizar varios filtros con `AND/OR` para añadir lógica al informe.

>[!TIP]
>
>Un informe puede tener un máximo de 3500 puntos de datos. Para reducir el número de puntos de datos, utilice un filtro para reducir la cantidad de datos que se utilizan para generar el informe.

[!DNL Adobe Commerce Intelligence] incluye una selección de filtros que puede utilizar &quot;listos para usar (OOTB)&quot; o modificar para adaptarlos a sus necesidades. No hay límite en el número de filtros que se pueden crear.

## Para añadir un filtro:

1. En el gráfico, pase el ratón sobre cada punto de datos.

   En este informe, cada punto de datos muestra la cantidad total de clientes durante el mes.

1. En el panel izquierdo, haga clic en el botón Filtros (![](../../assets/magento-bi-btn-filter.png)) icono.

   ![Añadir filtro](../../assets/magento-bi-report-builder-filter-add.png)

1. Clic **[!UICONTROL Add Filter]**.

   Los filtros se numeran alfabéticamente y el primero es `[A]`. Las dos primeras partes del filtro son opciones desplegables y la tercera parte es un valor.

   ![](../../assets/magento-bi-report-builder-filter-add-a.png)

   * Haga clic en la primera parte del filtro y elija la columna que desea utilizar como asunto de la expresión.

     ![Elegir la primera parte del filtro](../../assets/magento-bi-report-builder-filter-part1.png)

   * Haga clic en la segunda parte del filtro y seleccione el operador.

     ![Selección del operador](../../assets/magento-bi-report-builder-filter-part2.png)

   * En la tercera parte del filtro, introduzca el valor necesario para completar la expresión.

     ![Introduzca el valor](../../assets/magento-bi-report-builder-filter-part3.png)

   * Cuando haya completado el filtro, haga clic en **[!UICONTROL Apply]**.

     Ahora, el informe solo incluye clientes que repiten y el número de registros de clientes recuperados para el informe se ha reducido de 33 000 a 12 600.

     ![Informe filtrado](../../assets/magento-bi-report-builder-filter-report.png)<!--{: .zoom}-->

1. En la barra lateral, haga clic en la perspectiva ( ![](../../assets/magento-bi-btn-perspective.png)) icono.

   ![Perspectiva](../../assets/magento-bi-report-builder-filter-perspective.png)<!--{: .zoom}-->

1. En la lista de configuraciones, elija `Cumulative`. A continuación, haga clic en **[!UICONTROL Apply]**.

   ![Perspectiva acumulativa](../../assets/magento-bi-report-builder-filter-perspective-cumulative.png)

   El `Cumulative` La perspectiva distribuye el cambio con el tiempo, en lugar de mostrar los desgloses y ascendentes escalonados de cada mes.

1. Introduzca una `Title` para el informe y haga clic en **[!UICONTROL Save]** it as a `Chart` a su tablero.

   ![Guardar en el panel](../../assets/magento-bi-report-builder-filter-perspective-cumulative-save.png)
