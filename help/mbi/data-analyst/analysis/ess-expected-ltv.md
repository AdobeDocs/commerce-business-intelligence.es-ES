---
title: Análisis del valor de duración esperado (LTV) (básico)
description: Aprenda a crear análisis para comprender el valor de duración de sus clientes actuales y predecir cómo aumenta el valor de duración con más pedidos.
exl-id: e6f02cf6-f542-4768-969c-3ec998a7caa9
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '331'
ht-degree: 0%

---

# Análisis de valor de duración esperada

Pronosticar el valor de vida útil de los clientes a medida que realizan más pedidos es uno de los aspectos más importantes de cualquier negocio de cualquier tamaño.

A continuación se indican los pasos para crear análisis con el fin de comprender el valor de duración de los clientes actuales y prever cómo aumenta este valor con más pedidos.

![valor de duración esperado](../../assets/expected_ltv_720.png)

## Creación de una métrica

El primer paso es construir una nueva métrica con los siguientes pasos:
* Vaya a **[!UICONTROL Manage Data > Metrics]**
   * Ver los existentes **[!UICONTROL Avg lifetime revenue]**.

   >[!NOTE]
   >
   >La tabla en la que se construye esta métrica (probablemente `customer_entity` o `sales_order` dependiendo de la capacidad de su tienda para aceptar pago y envío de invitados).

   * Clic **[!UICONTROL Create New Metric]** y seleccione la tabla de arriba.
   * Esta métrica realiza una **Mediana** en el `Customer's lifetime revenue` columna, ordenada por `created_at`.
      * [!UICONTROL Filters]:
         * Añada el `Customers we count (Saved Filter Set)` (o `Registered accounts we count`)
   * Asigne un nombre a la métrica, como `Median lifetime revenue`.



## Creación del tablero

Una vez creada la métrica, puede **crear un tablero** haciendo esto:
* Vaya a **[!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**.
* Asigne un nombre al tablero, como `Expected LTV`.

* Aquí es donde se crean y agregan todos los informes.

## Creación de informes

>[!NOTE]
>
>Activado **[!UICONTROL Time Period:]**, el período de tiempo de cada informe se muestra como `All-time`. No dude en modificar esto para adaptarlo a sus necesidades de análisis. El Adobe recomienda que todos los informes de este tablero abarquen el mismo periodo de tiempo, como `All time`, `Year-to-date`, o `Last 365 days`.

* **[!UICONTROL Average LTV (all)]**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
   * [!UICONTROL Time period]: `All time`
   * 
      [!INTERVALO UICONTROL]: `None`
   * [!UICONTROL Chart Type]: `Number (scalar)`

* **[!UICONTROL Average LTV (customers / non-guest checkout)]**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Añadir [!UICONTROL filters]:
         * [`A`] `Customer's group code` **Not Equal To** `Not Logged In`
         * [`B`] `Customer's lifetime number of orders` **Bueno que**`0`
   * [!UICONTROL Time period]: `All time`
   * 
      [!INTERVALO UICONTROL]: `None`
   * [!UICONTROL Chart Type]: `Number (scalar)`


* **[!UICONTROL Average and Median LTV]**
   * Métrica `1`: `Avg lifetime revenue`
   * Métrica `2`: `Median lifetime revenue`
   * [!UICONTROL Time period]: `All time`
   * [!UICONTROL Interval]: `By Month`
   * 
      [!UICONTROL Tipo de gráfico]: `Line`
   * Desmarcar `Multiple Y-Axes`

* **LTV por número de pedidos de duración**
   * Métrica `1`: `Avg lifetime revenue`
   * Métrica `2`: `New customers`
   * [!UICONTROL Time period]: `All time`
   * 
      [!INTERVALO UICONTROL]: `None`
   * [!UICONTROL Group by]: `Customer's lifetime number of orders`
   * 

      [!UICONTROL Tipo de gráfico]: `Line`
   >[!NOTE]
   >
   >No agregue todos los valores para `Customer's lifetime number of orders`. En su lugar, observe un punto en el que el número de Nuevos clientes alcanza un número pequeño y añada manualmente el número de duración de cada cliente del valor de pedido a ese punto. Por ejemplo, si hay 200 clientes en un pedido, 75 en dos, 15 en tres y 3 en cuatro, agregue *1, 2 y 3*.

* Añadir el existente [!UICONTROL Avg customer lifetime revenue by cohort] informe.

Después de crear los informes, consulte la imagen de la parte superior de este tema para saber cómo organizar los informes en el panel.
