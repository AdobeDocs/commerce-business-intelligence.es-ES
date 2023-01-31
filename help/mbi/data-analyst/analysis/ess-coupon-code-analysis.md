---
title: Análisis del código de cupón (básico)
description: Descubra el rendimiento de los cupones de su negocio es una forma interesante de segmentar sus pedidos y comprender mejor los hábitos de los clientes.
exl-id: 0d486259-b210-42ae-8f79-cd91cc15c2c2
source-git-commit: 82882479d4d6bea712e8dd7c6b2e5b7715022cc3
workflow-type: tm+mt
source-wordcount: '443'
ht-degree: 0%

---

# Análisis básico del código de cupón

Comprender el rendimiento de los cupones de su negocio es una forma interesante de segmentar sus pedidos y comprender mejor los hábitos de los clientes.

Hemos documentado los pasos necesarios para crear este análisis con el fin de comprender el rendimiento de los clientes adquiridos con cupones, ver las tendencias y realizar un seguimiento del uso del código de cupones individual.

![](../../assets/coupon_analysis_dash_720.png)<!--{: width="807" height="471"}-->

## Introducción

En primer lugar, una nota sobre cómo se realiza el seguimiento de los códigos de cupones. Si un cliente aplica un cupón a un pedido, ocurren tres cosas:

* Un descuento se refleja en la variable `base_grand_total` importe (su `Revenue` en MBI)
* El código de cupón se almacena en la variable `coupon_code` campo . Si este campo es NULL (vacío), el pedido no tiene un cupón asociado.
* La cantidad descontada se almacena en `base_discount_amount`. Según la configuración, este valor puede parecer negativo o positivo.

## Creación de una métrica

El primer paso será construir una nueva métrica con los siguientes pasos:

* Vaya a **[!UICONTROL Manage Data > Metrics > Create New Metric]**.

* Seleccione el `sales_order`.
* Esta métrica realiza una **Sum** en el **base_billetes_descuento_cantidad** columna, ordenada por **created_at**.
   * [!UICONTROL Filters]:
      * Agregue la variable `Orders we count` (Conjunto de filtros guardados)
      * Añada lo siguiente:
         * `coupon_code`**IS NOT**`[NULL]`
      * Asigne un nombre a la métrica, como `Coupon discount amount`.

## Creación de un tablero

* Una vez creada la métrica:
   * Vaya a [!UICONTROL Dashboards > Dashboard Options > Create New Dashboard]**.
   * Asigne un nombre al tablero como `_Coupon Analysis_`.

* Aquí es donde creamos y agregamos todos los informes.

## Creación de informes

* **Nuevos informes:**

>[!NOTE]
>
>La variable [!UICONTROL Time Period]** para cada informe se enumera como `All-time`. Puede modificarlo para adaptarlo a sus necesidades de análisis. Recomendamos que todos los informes de este tablero cubran el mismo período de tiempo, como `All time`, `Year-to-date`o `Last 365 days`.

* **Pedidos con cupones**
   * 
      [!UICONTROL Métrica]: `Orders`
      * Añadir filtro:
         * [`A`] `coupon_code` **IS NOT** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [Intervalo !UICONTROL]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`


* **Pedidos sin cupones**
   * 
      [!UICONTROL Métrica]: `Orders`
      * Añadir filtro:
         * [`A`] `coupon_code` **IS** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [Intervalo !UICONTROL]: `None`
   * [!UICONTROL Chart type]:`Number (scalar)`


* **Ingresos netos de pedidos con cupones**
   * 
      [!UICONTROL Métrica]: `Revenue`
      * Añadir filtro:
         * [`A`] `coupon_code` **IS NOT** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [Intervalo !UICONTROL]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`


* **Descuentos de cupones**
   * [!UICONTROL Metric]: `Coupon discount amount`
   * [!UICONTROL Time period]: `All time`
   * 
      [Intervalo !UICONTROL]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`

* **Ingresos medios de duración: Clientes con cupones adquiridos**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Añadir filtro:
         * [`A`] `Customer's first order's coupon_code` **IS NOT** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [Intervalo !UICONTROL]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`


* **Ingresos medios de duración: Clientes adquiridos sin cupones**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Añadir filtro:
         * [A] `Customer's first order's coupon_code` **IS**`[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [Intervalo !UICONTROL]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`


* **Detalles de uso de cupones (pedidos por primera vez)**
   * Métrica `1`: `Orders`
      * Añadir filtro:
         * [`A`] `coupon_code` **IS NOT**`[NULL]`
         * [`B`] `Customer's order number` **Igual a** `1`
   * Métrica `2`: `Revenue`
      * Añadir filtro:
         * [`A`] `coupon_code` **IS NOT**`[NULL]`
         * [`B`] `Customer's order number` **Igual a** `1`
      * Cambiar nombre:  `Net revenue`
   * Métrica `3`: `Coupon discount amount`
      * Añadir filtro:
         * [`A`] `coupon_code` **IS NOT**`[NULL]`
         * [`B`] `Customer's order number` **Igual a** `1`
   * Crear nueva fórmula: `Gross revenue`
      * [!UICONTROL Formula]: `(B – C)`
      * 
         [!UICONTROL Format]: `Currency`
   * Crear nueva fórmula:**% descuento**
      * Fórmula: `(C / (B - C))`
      * 
         [!UICONTROL Format]: `Percentage`
   * Crear nueva fórmula: `Average order discount`
      * [!UICONTROL Formula]: `(C / A)`
      * 
         [!UICONTROL Format]: `Percentage`
   * [!UICONTROL Time period]: `All time`
   * 
      [Intervalo !UICONTROL]: `None`
   * 

      [!UICONTROL Tipo de gráfico]: `Table`








* **Media de ingresos por vida útil por cupón de primer pedido**
   * [!UICONTROL Metric]:**Promedio de ingresos de por vida**
      * Añadir filtro:
         * [`A`] `coupon_code` **IS**`[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [Intervalo !UICONTROL]: `None`
   * [!UICONTROL Chart type]: `Number (scalar)`


* **Detalles de uso de cupones (pedidos por primera vez)**
   * [!UICONTROL Metric]: `Avg lifetime revenue`
      * Añadir filtro:
         * [`A`] `Customer's first order's coupon_code` **IS NOT** `[NULL]`
   * [!UICONTROL Time period]: `All time`
   * 
      [Intervalo !UICONTROL]: `None`
   * [!UICONTROL Group by]: `Customer's first order's coupon_code`
   * 

      [!UICONTROL Tipo de gráfico]: **Column**


* **Clientes nuevos por adquisición de cupones/no de cupones**
   * Métrica `1`: `New customers`
      * Añadir filtro:
         * [`A`] `Customer's first order's coupon_code` **IS NOT** `[NULL]`
      * [!UICONTROL Rename]: `Coupon acquisition customer`
   * Métrica `2`: `New customers`
      * Añadir filtro:
         * [`A`] `coupon_code` **IS**`[NULL]`
      * [!UICONTROL Rename]: `Non-coupon acquisition customer`
   * [!UICONTROL Time period]: `All time`
   * [!UICONTROL Interval]: `By Month`
   * [!UICONTROL Chart type]: `Stacked Column`





Después de crear los informes, consulte la imagen de la parte superior de este tema para saber cómo organizar los informes en el tablero.
