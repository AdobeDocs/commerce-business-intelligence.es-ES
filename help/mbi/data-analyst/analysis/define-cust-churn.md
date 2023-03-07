---
title: Definir cancelación de cliente
description: Aprenda a configurar un tablero que le ayude a definir la pérdida para sus clientes transaccionales.
exl-id: fea8f7e9-c84c-4d49-a657-8b75140c113a
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '486'
ht-degree: 0%

---

# Cancelación de cliente transaccional

Este artículo muestra cómo configurar un panel que le ayuda a definir la pérdida para sus clientes transaccionales.

![](../../assets/churn-deashboard.png)

Este análisis contiene [columnas calculadas avanzadas](../data-warehouse-mgr/adv-calc-columns.md).

## Columnas calculadas

Columnas para crear

* `customer_entity` tabla
* `Customer's lifetime number of orders`
* Seleccione una definición: `Count`
* Seleccione una [!UICONTROL table]: `sales_flat_order`
* Seleccione una [!UICONTROL column]: **`entity_id`**
* [!UICONTROL Path]: sales_plain_order.customer_id = customer_entity.entity_id
* [!UICONTROL Filter]:
* Pedidos que se cuentan

* `sales_flat_order` tabla
* `Customer's lifetime number of orders`
* Seleccione una definición: Columna combinada
* Seleccione una [!UICONTROL table]: `customer_entity`
* Seleccione una [!UICONTROL column]: `Customer's lifetime number of orders`
* [!UICONTROL Path]: `sales_flat_order.customer_id = customer_entity.entity_id`
* [!UICONTROL Filter]: `Orders we count`

* `Seconds since created_at`
* Seleccione una definición: `Age`
* Seleccione una [!UICONTROL column]: `created_at`

* **`Customer's order number`** es creado por un analista como parte de su **[DEFINICIÓN DE PÉRDIDA]** boleto
* **`Is customer's last order`** es creado por un analista como parte de su **[DEFINICIÓN DE PÉRDIDA]** boleto
* **`Seconds since previous order`** es creado por un analista como parte de su **[DEFINICIÓN DE PÉRDIDA]** boleto
* **`Months since order`** es creado por un analista como parte de su **[DEFINICIÓN DE PÉRDIDA]** boleto
* **`Months since previous order`** es creado por un analista como parte de su **[DEFINICIÓN DE PÉRDIDA]** boleto

## Métricas

No hay métricas nuevas.

>[!NOTE]
>
>Asegúrese de lo siguiente [añadir todas las columnas nuevas como dimensiones a las métricas](../data-warehouse-mgr/manage-data-dimensions-metrics.md) antes de crear nuevos informes.

## Informes

* **Probabilidad de orden repetido inicial**
* Métrica A: Pedidos repetidos de todo el tiempo
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* Métrica B: Pedidos permanentes
* [!UICONTROL Metric]: Número de pedidos

* [!UICONTROL Formula]: Probabilidad de orden repetido inicial
* 
   [!UICONTROL Fórmula]: `A/B`
* 

   [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* 

   [!UICONTROL Chart type]: `Scalar`

* **Probabilidad de repetición de pedido dada meses desde el pedido**
* Métrica A: Repetir pedidos por meses desde el pedido anterior (ocultar)
* [!UICONTROL Metric]: `Number of orders`
* 
   [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* Métrica B: últimos pedidos por meses desde el pedido (ocultar)
* [!UICONTROL Metric]: `Number of orders`
* 
   [!UICONTROL Perspective]: `Cumulative`
* [!UICONTROL Filter]: `Is customer's last order? (Yes/No) = Yes`

* Métrica C: Todos los pedidos repetidos (ocultar)
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Customer's order number greater than 1`

* 

   [!UICONTROL Agrupar por]: `Independent`

* ID de métrica: últimos pedidos permanentes (ocultar)
* [!UICONTROL Metric]: `Number of orders`
* [!UICONTROL Filter]: `Is customer's last order? (Yes/No) = Yes`

* 

   [!UICONTROL Agrupar por]: `Independent`

* [!UICONTROL Formula]: Probabilidad de orden repetido inicial
* 
   [!UICONTROL Fórmula]: `(C-A)/(C+D-A-B)`
* 

   [!UICONTROL Format]: `Percent`

* [!UICONTROL Time period]: `All time`
* 
   [!UICONTROL Interval]: `None`
* [!UICONTROL Group by]: `Months since previous order`
* Mostrar top.bottom: Las 24 categorías principales, ordenadas por nombre de categoría

* 

   [!UICONTROL Chart type]: `Line`

El informe de probabilidad de pedido repetido inicial representa el total de pedidos repetidos/total de pedidos. Cada pedido es una oportunidad para hacer un pedido repetido; el número de pedidos repetidos es el subconjunto de los que realmente lo hacen.

La fórmula que utiliza simplifica a (Total de pedidos repetidos que se produjeron después de X meses)/ (Total de pedidos que tienen al menos X meses de antigüedad). Nos muestra que históricamente, dado que han pasado X meses desde un pedido, hay un Y% de probabilidad de que el usuario realice otro pedido.

Una vez que haya creado su panel, la pregunta más común es: ¿Cómo utilizo esto para determinar un umbral de pérdida?

**No hay &quot;una respuesta correcta&quot; a esto.** Sin embargo, Adobe recomienda encontrar el punto en el que la línea cruza el valor que es la mitad de la tasa de probabilidad de repetición inicial. Este es el punto en el que puede decir &quot;Si un usuario va a hacer un pedido repetido, probablemente ya lo habría hecho&quot;. En última instancia, el objetivo es seleccionar el umbral en el que tiene sentido cambiar de los esfuerzos de &quot;retención&quot; a &quot;reactivación&quot;.

Después de compilar todos los informes, puede organizarlos en el panel según lo desee. El resultado puede ser similar a la imagen de la parte superior de la página

Si tiene alguna pregunta mientras realiza este análisis o simplemente desea contactar con el equipo de Servicios profesionales, [soporte de contacto](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en).
