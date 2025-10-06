---
title: Informes anuales, mensuales y semanales
description: Aprenda a ver fácilmente las tendencias a lo largo del tiempo y a cambiar la perspectiva de los períodos de tiempo que desee comparar.
exl-id: 74cf11c3-7ce0-477f-9a28-9d782e5da3d9
role: Admin, Data Architect, Data Engineer, Leader, User
feature: Reports, Dashboards
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '301'
ht-degree: 0%

---

# Informes en períodos de tiempo

>[!NOTE]
>
>Este tema contiene instrucciones para los clientes que utilizan la arquitectura original y la nueva arquitectura. Se encuentra en la [nueva arquitectura](../../administrator/account-management/new-architecture.md) si tiene disponible la sección [!DNL _Vistas de Data Warehouse_] después de seleccionar [!DNL Manage Data] en la barra de herramientas principal.

Report Builder le permite ver fácilmente las tendencias a lo largo del tiempo y cambiar la perspectiva de los períodos de tiempo que desee comparar. En este tema se muestra cómo configurar un tablero para que profundice un nivel y le permita crear informes para el análisis semana tras semana, mes tras mes y año tras año.

![Panel que muestra comparaciones semana tras semana, mes tras mes y año tras año](../../assets/Wow__mom__yoy.png)

Antes de comenzar, debería revisar las perspectivas de exploración con más detalle [aquí](../../tutorials/using-visual-report-builder.md) y las opciones de tiempo independientes [aquí](../../tutorials/time-options-visual-rpt-bldr.md).

Este análisis contiene [columnas calculadas avanzadas](../data-warehouse-mgr/adv-calc-columns.md).

## Columnas calculadas

* **`Sales_flat_order`** tabla
* **Arquitectura original:** las siguientes columnas las crea un analista como parte de su vale `[YoY WoW MoM ANALYSIS]`
* `created_at (month-day)`
* `created_at (month)`
* `created_at (day of the month)`
* `created_at (day of the week)`
* `created_at (hour of the day)`

* **Nueva arquitectura:** SQL enumerado a continuación con una foto de un ejemplo para crear este cálculo
   * `created_at (month-day)` [!UICONTROL Calculation]: **to_char(A, &#39;mm-dd&#39;)**
   * `created_at (month)` [!UICONTROL Calculation]: **to_char(A, &#39;mm-mes&#39;)**
   * `created_at (day of the month)`&lt; [!UICONTROL Calculation]: **to_char(A, &#39;dd&#39;)**
   * `created_at (day of the week)` [!UICONTROL Calculation]: **to_char(A, &#39;d-Day&#39;)**
   * **`created_at (hour of the day)` [!UICONTROL Calculation]: &#x200B;** to_char(A, &#39;hh24&#39;)**
     ![Crear interfaz de columna calculada en Data Warehouse Manager](../../assets/new-arch-create-calc.png)

## Métricas

Ninguna.

>[!NOTE]
>
>Asegúrese de [agregar todas las columnas nuevas como dimensiones a las métricas](../data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de crear nuevos informes.

## Informes

* **Gráfico año a año**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Time options]: `Time range (Custom)`: `2 years ago to 1 year ago`

   * [!UICONTROL Show top/bottom]: 100% superior ordenado por **`created_at (month-day)`***

* Métrica `A`: `This year`
* Métrica `B`: `Last year`
* [!UICONTROL Time period]: `1 year ago to 0 years ago`
* &#x200B;
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `created_at (month-day)`
* &#x200B;
  [!UICONTROL Chart Type]: `Line`

* **Gráfico MoM**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * Opciones de tiempo: `Time range (Custom)`: `2 months ago to 1 month ago`

   * Mostrar superior/inferior: 100% superior ordenado por **`created_at (day of month)`***

* Métrica `A`: este mes*
* Métrica `B`: mes pasado*
* [!UICONTROL Time period]: hace un mes hasta hace 0 meses
* &#x200B;
  [!UICONTROL Interval]: None
* [!UICONTROL Group by]: `created_at (day of month)`
* &#x200B;
  [!UICONTROL Chart Type]: Line

* **Gráfico WoW**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Time options]: `Time range (Custom)`: `2 weeks ago to 1 week ago`

   * [!UICONTROL Show top/bottom]: 100% superior ordenado por `created_at (day of week)`

* Métrica `A`: `This week`
* Métrica `B`: `Last week`
* [!UICONTROL Time period]: `1 week ago to 0 weeks ago`
* &#x200B;
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `created_at (day of week)`
* &#x200B;
  [!UICONTROL Chart Type]: `Line`

* **Gráfico DoD**
   * [!UICONTROL Metric]: `Number of orders`

   * [!UICONTROL Metric]: `Number of orders`
   * [!UICONTROL Time options]: `Time range (Custom)`: `2 days ago to 1 day ago`

   * [!UICONTROL Show top/bottom]: 100% superior ordenado por `created_at (hour of day)`

* Métrica `A`: `Today`
* Métrica B: `Yesterday`
* [!UICONTROL Time period]: `1 day ago to 0 days ago`
* &#x200B;
  [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `created_at (hour of day)`
* &#x200B;
  [!UICONTROL Chart Type]: `Line`

Después de compilar todos los informes, puede organizarlos en el panel según lo desee. El resultado puede ser similar a la imagen de la parte superior de esta página.
