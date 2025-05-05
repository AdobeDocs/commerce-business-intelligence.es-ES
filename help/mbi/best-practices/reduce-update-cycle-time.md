---
title: Reducir el tiempo del ciclo de actualización
description: Aprenda a reducir el tiempo del ciclo de actualización.
exl-id: 0b211e2d-770f-480d-a7fb-8d10e3e7272e
role: Admin, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager, Dashboards
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '398'
ht-degree: 0%

---

# Reducir tiempo de procesamiento del ciclo de actualización

[!DNL Adobe Commerce Intelligence] se sincroniza con su base de datos a lo largo del día para replicar nuevos datos, asegurándose de que los paneles siempre muestren la información más reciente.

Muchos factores pueden agregar a un tiempo de actualización ya largo. Algunos métodos de replicación, las frecuencias de comprobación más altas y el número de paneles y gráficos son solo algunos factores que contribuyen. En este tema se describen algunas prácticas recomendadas para reducir los tiempos de actualización.

## Reducir frecuencia de comprobación

En una tabla de base de datos, puede haber columnas de datos con valores modificables. Por ejemplo, en una tabla **orders** puede haber una columna llamada **status**. Cuando se escribe inicialmente un pedido en la base de datos, la columna de estado puede contener el valor `pending`. El pedido se replica en su [Data Warehouse](../data-analyst/data-warehouse-mgr/tour-dwm.md) con este valor `pending`.

Se deben [volver a comprobar las columnas modificables en busca de valores actualizados](../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) con el tiempo. De manera predeterminada, [!DNL Commerce Intelligence] vuelve a comprobar estas columnas durante cada actualización, pero si hay una gran cantidad de datos que volver a comprobar y replicar, puede afectar negativamente al tiempo de actualización. En lugar de ejecutar comprobaciones nuevas durante cada actualización, Adobe recomienda establecer la frecuencia de las comprobaciones en diaria, semanal o mensual.

## Uso de métodos de replicación incremental

Como se ha mencionado anteriormente, los tiempos de actualización largos están directamente relacionados con la cantidad de datos que deben volver a comprobarse y replicarse. [Los métodos de replicación incremental](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md) pueden reducir en gran medida la cantidad de datos procesados durante el ciclo de actualización. Si es posible, Adobe recomienda utilizar estos métodos o modificar la base de datos para admitir un método incremental.

## Eliminar gráficos no utilizados de los paneles

Al final del ciclo de actualización, [!DNL Commerce Intelligence] realiza una operación de caché para todos los gráficos. Una caché almacena datos para que las futuras solicitudes de información se puedan completar más rápido. En [!DNL Commerce Intelligence], esto significa que los paneles se cargan rápidamente porque los gráficos no necesitan consultar los datos cada vez que se cargan.

Dado que [!DNL Commerce Intelligence] solo realiza operaciones de caché para los gráficos encontrados en un panel, la eliminación de los gráficos no utilizados de los paneles reduce el tiempo de actualización. Tenga en cuenta que el mismo gráfico puede estar en varios paneles. Consulte con su equipo para asegurarse de que también se eliminaron los gráficos no utilizados.

>[!NOTE]
>
>Al eliminar gráficos del tablero, no se elimina el gráfico. Puedes [volver a agregarlo en cualquier momento](../data-user/dashboards/add-charts-dashboard.md).

## Optimización de la base de datos para análisis

Además de volver a evaluar las frecuencias de comprobación, los métodos de replicación y la utilidad de los gráficos, también puede [optimizar la base de datos para el análisis](../best-practices/opt-db-analysis.md).

## Ajuste

Si el tiempo de actualización parece lento incluso después de implementar estas recomendaciones, [comuníquese con el equipo de atención](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=es).
