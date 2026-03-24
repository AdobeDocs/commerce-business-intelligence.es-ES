---
title: Fórmulas
description: Aprenda a utilizar las fórmulas.
exl-id: b6432d93-739f-410c-b732-e09a278f8dae
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
TQID: https://experienceleague.adobe.com/FYpOkbam6YFAKQtrLQZsZefke8baiqpK9pwsRI1z2n0
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 472
ht-degree: 0%

---

# Fórmulas

Una fórmula combina varias métricas y lógica matemática para responder a una pregunta. Por ejemplo, ¿qué parte de los ingresos por producto durante la temporada de vacaciones los generaron los nuevos clientes?

![Ventas de vacaciones en el panel](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-holiday-sales-dashboard.png)

## Paso 1: Crear el informe básico

1. En el menú, elija `Report Builder`.

1. Haga clic en **[!UICONTROL Add Metric]** y elija la primera métrica para el informe.

   Para este ejemplo, se utiliza la métrica `Revenue by products ordered`.

1. Vuelva a hacer clic en **[!UICONTROL Add Metric]** y elija la segunda métrica para el informe.

   Para este ejemplo, se utiliza la métrica `New Customers`.

1. En la barra lateral, haga clic en **[!UICONTROL Details]** para mostrar información sobre cada métrica.

   ![Ingresos por productos pedidos](../../assets/magento-bi-report-builder-revenue-by-products.png)

1. En la barra lateral, haga clic en el nombre de cada métrica para abrir la página de configuración en una nueva pestaña del explorador. Desplácese hacia abajo para ver cada componente de la métrica, incluidas la consulta de métrica, el filtro y las dimensiones.

   ![Configuración de métrica](../../assets/magento-bi-report-builder-revenue-by-products-metric-detail.png)

1. Para volver al informe, haga clic en la pestaña del explorador anterior.

1. En el gráfico, pase el ratón sobre unos pocos puntos de datos de cada línea para ver las cantidades asociadas a cada métrica.

## Paso 2: Añadir una fórmula

1. En la parte superior de la barra lateral, haga clic en **[!UICONTROL Add Formula]**.

   El cuadro de fórmula muestra las métricas como entradas disponibles `A` y `B`, e incluye un cuadro de entrada en el que puede escribir la fórmula.

   Haga lo siguiente:

   * En el cuadro de entrada `Enter your Formula`, escriba `A/B`.

     Esto divide los ingresos por productos ordenados por el número de clientes nuevos.

   * Establezca `Select format` en `123Number`.

   * En la barra lateral, reemplace `Untitled` por un nombre para la fórmula.

   ![Configuración de fórmula](../../assets/magento-bi-report-builder-revenue-by-products-add-formula-detail.png)

1. Una vez finalizado, haga clic en **[!UICONTROL Apply]**.

   El informe ahora tiene una nueva línea para la fórmula `New Customer Revenue`, y la barra lateral muestra la cantidad total de ingresos generados por los nuevos clientes.

   ![Informe con fórmula](../../assets/magento-bi-report-builder-revenue-by-products-formula-report.png)

## Paso 3: Añadir un intervalo de fechas

1. Haga clic en **[!UICONTROL Date Range]** en la esquina superior derecha.

1. En la ficha `Fixed Date Range`, haga lo siguiente:

   * En los calendarios, elija el intervalo de fechas.

     Para este ejemplo, la temporada de vacaciones es de `November 1` a `December 31`.

   * En `Select Time Interval`, elija `Day`.

     ![Intervalo de fecha fijo](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-fixed-date-range.png)

   * Una vez finalizado, haga clic en **[!UICONTROL Apply]**.

   El informe ahora se limita a la temporada de vacaciones, con un punto de datos para cada día.

   ![Intervalo de fecha fijo](../../assets/magento-bi-report-builder-revenue-by-products-formula-report-fixed-date-range-report.png)

## Paso 4: Guardar el informe

En este paso, guarda el informe como un gráfico y también como una tabla.

1. Haga clic en `Untitled Report` en la parte superior de la página e introduzca un título descriptivo. Para este ejemplo, el título del informe es `2017 Holiday Sales`.

   A continuación, haga lo siguiente:

   * En la esquina superior derecha, haga clic en **[!UICONTROL Save]**.

   * Para `Type`, acepte la configuración predeterminada `Chart`.

   * Elija el `Dashboard` en el que el informe va a estar disponible.

   * Haga clic en **[!UICONTROL Save to Dashboard]**.

1. Haga clic en el título del informe y cambie el nombre. Para este ejemplo, el título del informe se cambia a `2017 Holiday Sales Data`.

   A continuación, haga lo siguiente:

   * En la esquina superior derecha, haga clic en **[!UICONTROL Save a Copy]**.

   * Establezca `Type` en `Table`.

   * Elija el `Dashboard` en el que el informe va a estar disponible.

   * Haga clic en **[!UICONTROL Save a Copy to Dashboard]**.

1. Para ver los informes en el panel, siga uno de estos procedimientos:

   * Haga clic en **[!UICONTROL Go to Dashboard]** en el mensaje en la parte superior de la página.

   * En el menú, elija **[!UICONTROL Dashboards]**. Haga clic en el nombre del tablero actual para mostrar la lista. A continuación, haga clic en el nombre del tablero en el que se guardó el informe.
