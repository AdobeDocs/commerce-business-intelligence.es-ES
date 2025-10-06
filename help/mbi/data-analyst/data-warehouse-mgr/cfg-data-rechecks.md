---
title: Configuración de comprobaciones de datos
description: Aprenda a configurar columnas de datos con valores modificables.
exl-id: c31ef32e-ba5a-4902-b632-fbab551cc632
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager
source-git-commit: 4d04b79d55d02bee6dfc3a810e144073e7353ec0
workflow-type: tm+mt
source-wordcount: '569'
ht-degree: 0%

---

# Configuración de comprobaciones de datos

En una tabla de base de datos, puede haber columnas de datos con valores modificables. Por ejemplo, en una tabla `orders` puede haber una columna llamada `status`. Cuando un pedido se escribe inicialmente en la base de datos, la columna de estado puede contener el valor _pending_. El pedido se replica en su [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) con este valor de `pending`.

Los estados de los pedidos pueden cambiar, aunque no siempre se encuentran en un estado `pending`. Finalmente podría convertirse en `complete` o `cancelled`. Para asegurarse de que Data Warehouse sincronice este cambio, se debe volver a comprobar la columna para ver si hay nuevos valores.

¿Cómo encaja esto con los [métodos de replicación](../data-warehouse-mgr/cfg-replication-methods.md) que se discutieron? El procesamiento de las comprobaciones varía en función del método de replicación elegido. El método de replicación `Modified\_At` es la mejor opción para procesar valores cambiantes, ya que no es necesario configurar las comprobaciones de nuevo. Los métodos `Auto-Incrementing Primary Key` y `Primary Key Batch Monitoring` requieren volver a comprobar la configuración.

Al utilizar cualquiera de estos métodos, las columnas modificables deben marcarse para volver a comprobarlas. Hay tres formas de hacerlo:

1. Proceso de auditoría que se ejecuta como parte de las columnas de indicadores de actualización que se van a volver a comprobar.

   >[!NOTE]
   >
   >El auditor se basa en un proceso de muestreo y las columnas que cambian pueden no detectarse inmediatamente.

1. Puede configurarlos usted mismo seleccionando la casilla de verificación que hay junto a la columna en el administrador de Data Warehouse, haciendo clic en **[!UICONTROL Set Recheck Frequency]** y eligiendo un intervalo de tiempo apropiado para el momento en el que debe comprobar si hay cambios.

1. Un miembro del equipo de Data Warehouse [!DNL Adobe Commerce Intelligence] puede marcar manualmente las columnas para volver a comprobar en Data Warehouse. Si tiene conocimiento de columnas que se pueden cambiar, póngase en contacto con el equipo de para solicitar que se vuelvan a configurar las comprobaciones. Incluya una lista de columnas, junto con la frecuencia, con la solicitud.

## Volver a comprobar frecuencias {#frequency}

**¿Lo sabías?**
Al establecer una nueva comprobación en una columna `primary key`, no se comprueba si hay valores modificados en la columna. Se comprueba la existencia de filas eliminadas en la tabla y todas las eliminaciones se depuran de Data Warehouse.

Cuando se marca una columna para volver a comprobarla, también puede establecer la frecuencia con la que se realiza una nueva comprobación. Si una columna en particular no cambia con frecuencia, elegir una nueva comprobación menos frecuente puede [optimizar el ciclo de actualización](../../best-practices/reduce-update-cycle-time.md).

Las opciones de frecuencia son:

* `always`: se vuelve a comprobar con cada actualización
* `daily`: la nueva comprobación se produce después de la medianoche para la zona horaria declarada
* `weekly`: la nueva comprobación se realiza los viernes a las 21:00 (actualización semanal) para la zona horaria declarada
* `monthly`: la nueva comprobación se realiza después de las 21:00 los viernes, actualizar cada cuatro semanas para la zona horaria declarada
* `once` - solo se produce en la siguiente actualización (una actualización única)

Como los tiempos de actualización están correlacionados con la cantidad de datos que se deben sincronizar, Adobe recomienda elegir una nueva comprobación de `daily`, `weekly` o `monthly` en lugar de cada actualización.

## Administración de frecuencias de repetición {#manage}

Para volver a comprobar las frecuencias, en Data Warehouse, haga clic en el nombre de la tabla y marque las columnas individuales. El estado de sincronización y la frecuencia de repetición de comprobación (**¿Cambios?** (columna) se muestra para cada columna de la tabla.

Para cambiar la frecuencia de repetición de la comprobación, haga clic en la casilla de verificación situada junto a las columnas que desee cambiar. A continuación, haga clic en el menú desplegable **[!UICONTROL Set Recheck Frequency]** y establezca la frecuencia que desee.

![Data Warehouse Manager mostrando las opciones de configuración para volver a comprobar](../../assets/dwm-recheck.png)

A veces podría ver `Paused` en la columna `Changes?`. Este valor se muestra cuando el [método de replicación](../../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) de la tabla está establecido en `Paused`.

[!DNL Adobe] recomienda revisar estas columnas tanto para optimizar las actualizaciones como para asegurarse de que se vuelven a comprobar las columnas modificables. Si la frecuencia de nueva comprobación de una columna es alta, dada la frecuencia con la que cambian los datos, Adobe recomienda reducirla para optimizar las actualizaciones.

Póngase en contacto con nosotros si tiene alguna pregunta o pregunta sobre los métodos de replicación actuales o las comprobaciones nuevas.

**Relacionado:**

* [Reducción de los tiempos de actualización](../../best-practices/reduce-update-cycle-time.md)
* [Optimización de la base de datos para análisis](../../best-practices/opt-db-analysis.md)
