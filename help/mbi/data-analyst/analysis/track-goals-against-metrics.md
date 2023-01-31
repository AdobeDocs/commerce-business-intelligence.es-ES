---
title: Seguimiento de objetivos con métricas
description: Aprenda a configurar un tablero que le ayude a realizar un seguimiento de sus objetivos comerciales en relación con los datos reales, incluidos los ingresos, los usuarios registrados nuevos y los pedidos a lo largo del tiempo.
exl-id: 9d621f40-f9c2-4310-bd96-a46ab7159930
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '408'
ht-degree: 0%

---

# Seguimiento de objetivos con métricas de rendimiento

A menudo, una gran mayoría de nuestros clientes desean realizar un seguimiento de sus **objetivos empresariales**, pero no se dé cuenta de que esto es posible en [!DNL MBI]. En este artículo, demostramos cómo configurar un panel que le ayudará a realizar un seguimiento de sus objetivos comerciales en relación con los datos reales, incluidos los ingresos, los usuarios registrados nuevos y los pedidos a lo largo del tiempo. También le mostramos cómo comparar el rendimiento año tras año, todo en un panel como este:

![](../../assets/Goals-_dashboard_2.png)

Antes de comenzar, debe familiarizarse con nuestra [cargador de archivos](../importing-data/connecting-data/using-file-uploader.md) y asegúrese de haber definido sus objetivos comerciales durante un período de tiempo determinado.

## Introducción

En primer lugar, deberá cargar un archivo que contenga objetivos específicos diarios, mensuales o trimestrales para su empresa.

Puede usar la variable [cargador de archivos](../importing-data/connecting-data/using-file-uploader.md) y la siguiente imagen para dar formato a su archivo. Los objetivos más comunes en los que nuestros clientes realizan un seguimiento [!DNL MBI] incluyen Pedidos, Ingresos y Nuevas cuentas registradas.

![](../../assets/Goals-_Excel.png)

## Métricas

Debe crear una nueva métrica para cada objetivo. Por ejemplo, si carga los objetivos de ingresos y pedidos mensuales, deberá crear dos métricas nuevas:

* **Objetivo de ingresos mensuales**
* En el **`Monthly goals`** tabla
* Esta métrica realiza una **Sum**
* En el **`Revenue target`** column
* Solicitado por el **`Month`** timestamp

* **Objetivo de pedidos mensuales**
* En el **`Monthly goals`** tabla
* Esta métrica realiza una **Sum**
* En el **`Orders target`** column
* Solicitado por el **`Month`** timestamp

* **Objetivo de las nuevas cuentas registradas mensuales**
* En el **`Monthly goals`** tabla
* Esta métrica realiza una **Sum**
* En el **`New registered accounts target`** column
* Solicitado por el **`Month`** timestamp

## Informes

Como siempre, resulta útil tener una combinación de valores estáticos y gráficos visuales al analizar los objetivos. A continuación se muestran tres informes de ejemplo para empezar a realizar un seguimiento del rendimiento de los ingresos.

* **Ingresos que quedan para alcanzar el objetivo**
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
* [!UICONTROL Time period]: (El período de tiempo que desee)*
* 
   [!UICONTROL Interval]: `Month`
* [!UICONTROL Chart Type]: `Line Chart`

Una vez que haya completado los informes anteriores para los objetivos de ingresos, puede crear informes idénticos para los objetivos relacionados con los pedidos, las cuentas registradas o cualquier otro valor que haya incluido en la carga del archivo de objetivos.

Después de compilar todos los informes, puede organizarlos en el panel como desee. El resultado final puede ser similar a la imagen de la parte superior de esta página.
