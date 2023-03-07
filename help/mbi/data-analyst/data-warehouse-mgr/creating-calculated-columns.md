---
title: Creación de columnas calculadas
description: Aprenda a consolidar datos de diferentes fuentes.
exl-id: 668cbc77-6a96-4687-9f40-3635b1be5c66
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '350'
ht-degree: 0%

---

# Crear columnas calculadas

Al analizar los datos, resulta beneficioso consolidar los datos de diferentes fuentes. ¿Desea agrupar los ingresos por fuente de adquisición, vinculando los datos de la tabla de pedidos con los Google Analytics? ¿O puede agrupar los ingresos por sexo del cliente o unir un atributo del cliente a los datos de transacción para la segmentación?

Esta guía le enseña cómo hacer precisamente eso. Antes de comenzar, el Adobe recomienda que compruebe el [Guía de tipos de columnas calculadas](../../data-analyst/data-warehouse-mgr/calc-column-types.md). El _Guía de tipos de columnas calculadas_ describe los tipos de columnas que puede crear en el Administrador de Datas Warehouse, junto con sus definiciones y ejemplos.

1. Para empezar, haga clic en **[!DNL Manage Data > Data Warehouse]** en la barra lateral.

1. Haga clic en la tabla en la que desea crear una columna. Por ejemplo, si desea crear una `Customer Gender` para la segmentación de ingresos, debe seleccionar la columna `sales_flat_order` tabla.

1. Se muestra el esquema de tabla. Clic **[!UICONTROL Create New Column]**.

1. Asigne un nombre a la columna como, por ejemplo, `Customer Gender`.

1. Seleccione la definición de la columna. Aquí es donde la variable [Guía de tipos de columnas calculadas](../data-warehouse-mgr/calc-column-types.md) ¡es útil!

1. Para ciertos tipos de columnas, se necesita un poco más de información para crear correctamente la columna:
   * Para `One to Many` (unido) y `Many to One` (acumulado), debe seleccionar las tablas y columnas.
   * Para un `Same Table calculation`, debe seleccionar el campo de fecha deseado en la lista desplegable.

Si está creando un `One to Many` (unido) o `Many to One` (acumulado), debe seleccionar una ruta para conectar las dos tablas. En este paso, puede utilizar una ruta de acceso existente o crear una.

>[!NOTE]
>
>Recuerde definir correctamente la tabla como varios o uno.

* Si lo desea, puede solicitar [filtros](../../data-user/reports/ess-manage-data-filters.md) a la nueva columna.
* Cuando termine, haga clic en **[!UICONTROL Save]**.

¡Eso es todo! La nueva columna aparece en la tabla actual con un `Pending` estado. Una vez que se complete la siguiente actualización, la columna estará disponible para usarla en métricas e informes.

## Mapa de referencia útil {#map}

Si tiene algún problema para recordar cuáles son todas las entradas al crear una columna calculada, intente mantener este mapa de referencia a mano cuando esté construyendo:

![](../../assets/Calculated_Columns_Example.png)

## Documentación relacionada

* [Tipos de columnas calculadas](../data-warehouse-mgr/calc-column-types.md)
* [Tipos de columnas calculadas avanzadas](../data-warehouse-mgr/adv-calc-columns.md)
* [Edificio [!DNL Google ECommerce] dimensiones con datos de pedidos y clientes](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
