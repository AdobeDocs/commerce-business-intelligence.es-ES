---
title: Fórmulas
description: Aprenda a utilizar las fórmulas.
exl-id: b6432d93-739f-410c-b732-e09a278f8dae
source-git-commit: df81d2b036d00cd53274ec1ae22031dbf06cc948
workflow-type: tm+mt
source-wordcount: '468'
ht-degree: 0%

---

# Fórmulas

Una fórmula combina varias métricas y lógica matemática para responder a una pregunta. Por ejemplo, ¿qué parte de los ingresos por producto durante la temporada de vacaciones los generaron los nuevos clientes?

![Ventas de vacaciones en Dashboard](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-holiday-sales-dashboard.png)

## Paso 1: Crear el informe básico

1. En el menú, elija `Report Builder`.

1. Clic **[!UICONTROL Add Metric]** y elija la primera métrica para el informe.

   Para este ejemplo, la variable `Revenue by products ordered` se utiliza la métrica de.

1. Clic **[!UICONTROL Add Metric]** de nuevo y elija la segunda métrica para el informe.

   Para este ejemplo, la variable `New Customers` se utiliza la métrica de.

1. En la barra lateral, haga clic en **[!UICONTROL Details]** para mostrar información sobre cada métrica.

   ![Ingresos por productos pedidos](../../assets/magento-bi-report-builder-revenue-by-products.png)

1. En la barra lateral, haga clic en el nombre de cada métrica para abrir la página de configuración en una nueva pestaña del explorador. Desplácese hacia abajo para ver cada componente de la métrica, incluidas la consulta de métrica, el filtro y las dimensiones.

   ![Configuración de métricas](../../assets/magento-bi-report-builder-revenue-by-products-metric-detail.png)

1. Para volver al informe, haga clic en la pestaña del explorador anterior.

1. En el gráfico, pase el ratón sobre unos pocos puntos de datos de cada línea para ver las cantidades asociadas a cada métrica.

## Paso 2: Añadir una fórmula

1. En la parte superior de la barra lateral, haga clic en **[!UICONTROL Add Formula]**.

   El cuadro de fórmula muestra las métricas como entradas disponibles `A` y `B`e incluye un cuadro de entrada en el que puede introducir la fórmula.

   Haga lo siguiente:

   * En el `Enter your Formula` cuadro de entrada, escriba `A/B`.

      Esto divide los ingresos por productos ordenados por el número de clientes nuevos.

   * Establecer `Select format` hasta `123Number`.

   * En la barra lateral, reemplace `Untitled` con un nombre para la fórmula.

   ![Configuración de fórmula](../../assets/magento-bi-report-builder-revenue-by-products-add-formula-detail.png)

1. Cuando termine, haga clic en **[!UICONTROL Apply]**.

   El informe tiene ahora una nueva línea para la fórmula, `New Customer Revenue`y la barra lateral muestra la cantidad total de ingresos generados por los nuevos clientes.

   ![Informe con fórmula](../../assets/magento-bi-report-builder-revenue-by-products-formula-report.png)

## Paso 3: Añadir un intervalo de fechas

1. Clic **[!UICONTROL Date Range]** en la esquina superior derecha.

1. En el `Fixed Date Range` pestaña, haga lo siguiente:

   * En los calendarios, elija el intervalo de fechas.

      Para este ejemplo, la temporada de vacaciones es de `November 1` mediante `December 31`.

   * En `Select Time Interval`, elija `Day`.

      ![Intervalo de fecha fijo](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-fixed-date-range.png)

   * Cuando termine, haga clic en **[!UICONTROL Apply]**.

   El informe ahora se limita a la temporada de vacaciones, con un punto de datos para cada día.

   ![Intervalo de fecha fijo](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-fixed-date-range-report.png)

## Paso 4: Guardar el informe

En este paso, guarda el informe como un gráfico y también como una tabla.

1. Clic `Untitled Report` en la parte superior de la página e introduzca un título descriptivo. Para este ejemplo, el título del informe es `2017 Holiday Sales`.

   A continuación, haga lo siguiente:

   * En la esquina superior derecha, haga clic en **[!UICONTROL Save]**.

   * Para `Type`, acepte el valor predeterminado `Chart` configuración.

   * Elija la `Dashboard` donde el informe va a estar disponible.

   * Clic **[!UICONTROL Save to Dashboard]**.

1. Haga clic en el título del informe y cambie el nombre. Para este ejemplo, el título del informe se cambia a `2017 Holiday Sales Data`.

   A continuación, haga lo siguiente:

   * En la esquina superior derecha, haga clic en **[!UICONTROL Save a Copy]**.

   * Establecer `Type` hasta `Table`.

   * Elija la `Dashboard` donde el informe va a estar disponible.

   * Clic **[!UICONTROL Save a Copy to Dashboard]**.

1. Para ver los informes en el panel, siga uno de estos procedimientos:

   * Clic **[!UICONTROL Go to Dashboard]** en el mensaje, en la parte superior de la página.

   * En el menú, elija **[!UICONTROL Dashboards]**. Haga clic en el nombre del tablero actual para mostrar la lista. A continuación, haga clic en el nombre del tablero en el que se guardó el informe.
