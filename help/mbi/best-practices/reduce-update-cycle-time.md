---
title: Reducir el tiempo del ciclo de actualización
description: Aprenda a reducir el tiempo del ciclo de actualización.
exl-id: 0b211e2d-770f-480d-a7fb-8d10e3e7272e
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 0%

---

# Reducir el tiempo de procesamiento del ciclo de actualización

[!DNL MBI] se sincroniza con la base de datos a lo largo del día para replicar nuevos datos, lo que garantiza que los tableros siempre muestren la información más reciente.

Muchos factores pueden agregar a un tiempo de actualización ya largo. Ciertos métodos de replicación, frecuencias de recomprobación más altas y la cantidad de tableros y gráficos son solo algunos factores que contribuyen. En este tema se describen algunas prácticas recomendadas para reducir los tiempos de actualización.

## Reducir Frecuencia De Comprobación

En una tabla de base de datos, puede haber columnas de datos con valores que se pueden cambiar. Por ejemplo, en un **pedidos** tabla puede haber una columna llamada **status**. Cuando se escribe inicialmente una solicitud en la base de datos, la columna de estado puede contener el valor `pending`. El pedido se replicará en su [Data Warehouse](../data-analyst/data-warehouse-mgr/tour-dwm.md) con esto `pending` valor.

Es necesario cambiar las columnas [volver a comprobar los valores actualizados](../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) con el tiempo. De forma predeterminada, [!DNL MBI] vuelve a comprobar estas columnas durante cada actualización, pero si hay una gran cantidad de datos que volver a comprobar y replicar, puede afectar negativamente al tiempo de actualización. En lugar de ejecutar recomprobaciones durante cada actualización, se recomienda establecer la frecuencia de recomprobación en diaria, semanal o mensual.

## Uso de métodos de replicación incremental

Como se ha mencionado anteriormente, los tiempos de actualización largos se correlacionan directamente con la cantidad de datos que se deben volver a comprobar y replicar. [Métodos de replicación incremental](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md) puede reducir en gran medida la cantidad de datos procesados durante el ciclo de actualización. Siempre que sea posible, se recomienda utilizar estos métodos o realizar modificaciones en la base de datos para admitir un método incremental.

## Eliminar gráficos no utilizados de los tableros

Al final del ciclo de actualización, [!DNL MBI] realiza una operación de caché para todos los gráficos. Una caché almacena datos para que las futuras solicitudes de información se puedan completar más rápido. En [!DNL MBI], esto significa que los tableros se cargarán rápidamente porque los gráficos no necesitan consultar los datos cada vez que se cargan.

Since [!DNL MBI] solo realiza operaciones de caché para gráficos encontrados en un tablero, eliminar gráficos no utilizados de los tableros reducirá el tiempo de actualización. Tenga en cuenta que el mismo gráfico puede estar en varios tableros; consulte con su equipo para asegurarse de que también se han eliminado los gráficos que no se hayan utilizado.

>[!NOTE]
>
>Al eliminar gráficos del tablero, no se elimina el gráfico. Puede [añadir en cualquier momento](../data-user/dashboards/add-charts-dashboard.md).

## Optimizar la base de datos para análisis

Además de reevaluar las frecuencias de recomprobación, los métodos de replicación y la utilidad de los gráficos, también puede [optimizar la base de datos para su análisis](../best-practices/opt-db-analysis.md).

## Ajuste

Si el tiempo de actualización sigue pareciendo lento incluso después de implementar estas recomendaciones, [póngase en contacto con nuestro equipo de asistencia](../guide-overview.md).
