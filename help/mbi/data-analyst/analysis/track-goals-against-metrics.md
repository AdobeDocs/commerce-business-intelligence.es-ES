---
title: Seguimiento de objetivos con métricas
description: Aprenda a configurar un tablero que le ayude a realizar un seguimiento de los objetivos de su empresa en relación con los datos reales, incluidos los ingresos, los nuevos usuarios registrados y los pedidos a lo largo del tiempo.
exl-id: 9d621f40-f9c2-4310-bd96-a46ab7159930
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '391'
ht-degree: 0%

---

# Seguimiento De Objetivos Con Métricas De Rendimiento

La mayoría de los clientes desea realizar un seguimiento de sus **objetivos empresariales**, pero no se da cuenta de que esto es posible en [!DNL MBI]. Este artículo muestra cómo configurar un tablero que le ayudará a realizar un seguimiento de los objetivos de su empresa en relación con los datos reales, incluidos los ingresos, los nuevos usuarios registrados y los pedidos a lo largo del tiempo. También aprenderá a comparar el rendimiento año tras año, todo en un tablero como este:

![](../../assets/Goals-_dashboard_2.png)

Antes de empezar, debe familiarizarse con el [cargador de archivos](../importing-data/connecting-data/using-file-uploader.md) y asegúrese de haber definido sus objetivos empresariales para un periodo determinado.

## Primeros pasos

Primero debe cargar un archivo que contenga objetivos diarios, mensuales o trimestrales específicos para su empresa.

Puede usar el complemento [cargador de archivos](../importing-data/connecting-data/using-file-uploader.md) y la imagen siguiente para dar formato al archivo. Los destinos más comunes en los que los clientes realizan el seguimiento [!DNL MBI] incluir pedidos, ingresos y nuevas cuentas registradas.

![](../../assets/Goals-_Excel.png)

## Métricas

Cree una nueva métrica para cada destino. Por ejemplo, si carga objetivos de ingresos y pedidos mensuales, debe crear dos métricas nuevas:

* **Objetivo de ingresos mensuales**
* En el **`Monthly goals`** tabla
* Esta métrica realiza una **Sum**
* En el **`Revenue target`** columna
* Ordenado por el **`Month`** timestamp

* **Destino de pedidos mensuales**
* En el **`Monthly goals`** tabla
* Esta métrica realiza una **Sum**
* En el **`Orders target`** columna
* Ordenado por el **`Month`** timestamp

* **Destino de nuevas cuentas registradas mensuales**
* En el **`Monthly goals`** tabla
* Esta métrica realiza una **Sum**
* En el **`New registered accounts target`** columna
* Ordenado por el **`Month`** timestamp

## Informes

Como siempre, es útil tener una combinación de valores estáticos y gráficos visuales al analizar los destinatarios. A continuación se muestran tres informes de ejemplo para ayudarle a empezar a rastrear el rendimiento de los ingresos.

* **Ingresos restantes para alcanzar el objetivo**
* Métrica `A`: `Revenue`
* 

   [!UICONTROL Métrica]: `Revenue`

* Métrica `B`: `Target Revenue`
* [!UICONTROL Metric]: `Monthly Revenue Target`

* [!UICONTROL Formula]: `Revenue left to achieve target`
* 
   [!UICONTROL Fórmula]: `(B-A)`
* 

   [!UICONTROL Format]: `Number`

* [!UICONTROL Time period]: (el período de tiempo relevante que desee)
* 
   [!UICONTROL Interval]: `Month`
* 

   [!UICONTROL Tipo de gráfico]: `Scalar`

* **Destinos de ingresos**
* Métrica `A`: `Revenue`
* 

   [!UICONTROL Métrica]: `Revenue`

* Métrica `B`: `Target Revenue`
* [!UICONTROL Metric]: `Monthly Revenue Target`

* Métrica `C`: `Revenue (amount change since previous year)` (ocultar)
* 
   [!UICONTROL Métrica]: `Revenue`
* [!UICONTROL Perspective]: `Amount change vs. Previous year`

* [!UICONTROL Formula]: (Este mes del año pasado)
* 
   [!UICONTROL Fórmula]: `(A-C)`
* 

   [!UICONTROL Format]: `Currency`

* Desactivar `Multiple Y-Axes`
* [!UICONTROL Time period]: (independientemente del período de tiempo relevante que desee)*
* 
   [!UICONTROL Interval]: `Month`
* [!UICONTROL Chart Type]: `Line Chart`

Una vez completados los informes anteriores para los objetivos de ingresos, puede crear informes idénticos para los objetivos relacionados con pedidos, cuentas registradas o cualquier otro valor que haya incluido en la carga del archivo de objetivos.

Después de compilar todos los informes, puede organizarlos en el panel según lo desee. El resultado puede ser similar a la imagen de la parte superior de esta página.