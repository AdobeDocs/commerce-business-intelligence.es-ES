---
title: Crear columnas calculadas
description: Aprenda a consolidar datos de diferentes fuentes.
exl-id: 668cbc77-6a96-4687-9f40-3635b1be5c66
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '352'
ht-degree: 0%

---

# Crear columnas calculadas

Al analizar los datos, resulta beneficioso consolidar los datos de diferentes fuentes. ¿Quiere agrupar los ingresos por fuente de adquisición, vinculando los datos de la tabla de pedidos con los Google Analytics? ¿O qué sucede si se agrupan los ingresos por sexo de cliente o si se une un atributo de cliente a los datos de transacción para la segmentación?

Esta guía le enseñará a hacer justamente eso. Antes de comenzar, le recomendamos que consulte la [Guía de tipos de columnas calculadas](../../data-analyst/data-warehouse-mgr/calc-column-types.md). La variable _Guía de tipos de columnas calculadas_ describe los tipos de columnas que se pueden crear en el Administrador de Datas Warehouse, junto con sus definiciones y ejemplos.

1. Para empezar, haga clic en **[!DNL Manage Data > Data Warehouse]** en la barra lateral.

1. Haga clic en la tabla en la que desee crear una columna. Por ejemplo, si queremos crear un `Customer Gender` para la segmentación de ingresos, se seleccionaría la columna `sales_flat_order` tabla.

1. Se mostrará el esquema de tabla. Haga clic en **[!UICONTROL Create New Column]**.

1. Asigne un nombre a la columna (por ejemplo, `Customer Gender`.

1. Seleccione la definición de la columna. Aquí es donde la variable [Guía de tipos de columnas calculadas](../data-warehouse-mgr/calc-column-types.md) ¡será útil!

1. Para ciertos tipos de columnas, se necesita un poco más de información para crear correctamente la columna:
   * Para `One to Many` (unido) y `Many to One` (acumulado), es necesario seleccionar las tablas y las columnas.
   * Para un `Same Table calculation`, debe seleccionar el campo de fecha deseado en la lista desplegable.

Si está creando un `One to Many` (unido) o `Many to One` (agregado), debe seleccionar una ruta para conectar las dos tablas. En este paso, puede utilizar una ruta existente o crear una nueva.

>[!NOTE]
>
>Recuerde definir correctamente la tabla como muchas o una.

* Si lo desea, puede aplicar [filtros](../../data-user/reports/ess-manage-data-filters.md) a la nueva columna.
* Cuando termine, haga clic en **[!UICONTROL Save]**.

¡Eso es! La nueva columna aparecerá en la tabla actual con un `Pending` estado. Una vez completada la siguiente actualización, la columna estará disponible para su uso en métricas e informes.

## Mapa de referencia práctico {#map}

Si tiene problemas para recordar cuáles son todas las entradas al crear una columna calculada, intente mantener este mapa de referencia a mano cuando esté creando:

![](../../assets/Calculated_Columns_Example.png)

## Documentación relacionada

* [Tipos de columnas calculadas](../data-warehouse-mgr/calc-column-types.md)
* [Tipos de columnas calculadas avanzadas](../data-warehouse-mgr/adv-calc-columns.md)
* [Creación [!DNL Google ECommerce] dimensiones con datos de pedidos y clientes](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
