---
title: Reducir el tiempo del ciclo de actualización
description: Aprenda a reducir el tiempo del ciclo de actualización.
exl-id: 0b211e2d-770f-480d-a7fb-8d10e3e7272e
role: Admin, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager, Dashboards
TQID: https://experienceleague.adobe.com/DFlzL9E95teiWI31j7qWRU8Ab6GkbFX7iPPdaxGq48A
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
  - id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 398
ht-degree: 0%

---

# Reducir tiempo de procesamiento del ciclo de actualización

[!DNL Adobe Commerce Intelligence] se sincroniza con su base de datos a lo largo del día para replicar nuevos datos, asegurándose de que los paneles siempre muestren la información más reciente.

Muchos factores pueden agregar a un tiempo de actualización ya largo. Algunos métodos de replicación, las frecuencias de comprobación más altas y el número de paneles y gráficos son solo algunos factores que contribuyen. En este tema se describen algunas prácticas recomendadas para reducir los tiempos de actualización.

## Reducir frecuencia de comprobación

En una tabla de base de datos, puede haber columnas de datos con valores modificables. Por ejemplo, en una tabla **orders** puede haber una columna llamada **status**. Cuando se escribe inicialmente un pedido en la base de datos, la columna de estado puede contener el valor `pending`. El pedido se replica en su [Data Warehouse](../data-analyst/data-warehouse-mgr/tour-dwm.md) con este valor de `pending`.

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
