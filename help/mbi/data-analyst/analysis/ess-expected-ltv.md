---
title: Análisis del valor de duración esperado (LTV) (básico)
description: Aprenda a crear análisis para comprender el valor de duración de sus clientes actuales y prevea cómo el valor de duración aumentará con más pedidos.
exl-id: e6f02cf6-f542-4768-969c-3ec998a7caa9
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '335'
ht-degree: 0%

---

# Análisis del valor de duración esperado

La previsión del valor de duración de los clientes a medida que realizan más pedidos es uno de los aspectos más importantes de cualquier negocio de cualquier tamaño.

Estos son los pasos para crear análisis para comprender el valor de duración de sus clientes actuales y para pronosticar cómo aumentará el valor de duración con más pedidos:

![valor de duración esperado](../../assets/expected_ltv_720.png)

## Creación de una métrica

El primer paso será construir una nueva métrica con los siguientes pasos:
* Vaya a **[!UICONTROL Manage Data > Metrics]**
   * Ver el **[!UICONTROL Avg lifetime revenue]**.

   >[!NOTE]
   >
   >Tabla en la que se construye esta métrica (probablemente `customer_entity` o `sales_order` dependiendo de la capacidad de su tienda para aceptar el cierre de compra de invitado).

   * Haga clic en **[!UICONTROL Create New Metric]** y seleccione la tabla de arriba.
   * Esta métrica realiza una **Mediana** en el `Customer's lifetime revenue` columna, ordenada por `created_at`.
      * [!UICONTROL Filters]:
         * Agregue la variable `Customers we count (Saved Filter Set)` (o `Registered accounts we count`)
   * Asigne un nombre a la métrica, como `Median lifetime revenue`.



## Creación de un tablero

Una vez creada la métrica, puede **crear un tablero** haciendo esto:
* Vaya a **[!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**.
* Asigne un nombre al tablero como `Expected LTV`.

* Aquí es donde creamos y agregamos todos los informes.

## Creación de informes

>[!NOTE]
>
>Activado **[!UICONTROL Time Period:]**, el período de tiempo de cada informe se enumera como `All-time`. Puede modificarlo para adaptarlo a sus necesidades de análisis. Recomendamos que todos los informes de este tablero cubran el mismo período de tiempo, como `All time`, `Year-to-date`o `Last 365 days`.

* **[!UICONTROL Average LTV (all)]**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
   * [!UICONTROL Time period]: `All time`
   * 
      [Intervalo !UICONTROL]: `None`
   * [!UICONTROL Chart Type]: `Number (scalar)`

* **[!UICONTROL Average LTV (customers / non-guest checkout)]**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Agregar [!UICONTROL filters]:
         * [`A`] `Customer's group code` **Distinto a** `Not Logged In`
         * [`B`] `Customer's lifetime number of orders` **Bueno que**`0`
   * [!UICONTROL Time period]: `All time`
   * 
      [Intervalo !UICONTROL]: `None`
   * [!UICONTROL Chart Type]: `Number (scalar)`


* **[!UICONTROL Average and Median LTV]**
   * Métrica `1`: `Avg lifetime revenue`
   * Métrica `2`: `Median lifetime revenue`
   * [!UICONTROL Time period]: `All time`
   * [!UICONTROL Interval]: `By Month`
   * 
      [!UICONTROL Tipo de gráfico]: `Line`
   * Desmarcar `Multiple Y-Axes`

* **LTV por número de pedidos acumulado**
   * Métrica `1`: `Avg lifetime revenue`
   * Métrica `2`: `New customers`
   * [!UICONTROL Time period]: `All time`
   * 
      [Intervalo !UICONTROL]: `None`
   * [!UICONTROL Group by]: `Customer's lifetime number of orders`
   * 

      [!UICONTROL Tipo de gráfico]: `Line`
   >[!NOTE]
   >
   >No agregue todos los valores para `Customer's lifetime number of orders`, en su lugar, observe un punto en el que el número de clientes nuevos alcanza un número pequeño y agregue manualmente el número de pedidos de cada cliente a ese punto. Por ejemplo, si hay 200 clientes en un pedido, 75 en dos, 15 en tres y 3 en cuatro, agregue *1, 2 y 3*.

* Agregue la [!UICONTROL Avg customer lifetime revenue by cohort] informe.

Después de crear los informes, consulte la imagen de la parte superior de este tema para saber cómo organizar los informes en el tablero.
