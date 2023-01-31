---
title: Configuración de comprobaciones de datos
description: Obtenga información sobre cómo configurar columnas de datos con valores que se pueden cambiar.
exl-id: c31ef32e-ba5a-4902-b632-fbab551cc632
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '575'
ht-degree: 0%

---

# Configuración de comprobaciones de datos

En una tabla de base de datos, puede haber columnas de datos con valores que se pueden cambiar. Por ejemplo, en un `orders`) tabla puede haber una columna llamada `status`. Cuando se escribe inicialmente una solicitud en la base de datos, la columna de estado puede contener el valor _pending_. El pedido se replicará en su [Data Warehouse](../data-warehouse-mgr/tour-dwm.md) con esto `pending` valor.

Los estados de los pedidos pueden cambiar, pero no siempre estarán en una `pending` estado. Con el tiempo podría llegar a ser `complete` o `cancelled`. Para garantizar que la Data Warehouse sincronice este cambio, será necesario volver a comprobar la columna para buscar nuevos valores.

¿Cómo encaja esto con el [métodos de replicación](../data-warehouse-mgr/cfg-replication-methods.md) ¿discutimos? El procesamiento de las comprobaciones varía en función del método de replicación elegido. La variable `Modified\_At` el método de replicación es la mejor opción para procesar los valores cambiantes, ya que no es necesario configurar las recomprobaciones. La variable `Auto-Incrementing Primary Key` y `Primary Key Batch Monitoring` los métodos requieren una nueva configuración de comprobación.

Al utilizar cualquiera de estos métodos, las columnas modificables deben marcarse para volver a comprobarse. Hay tres formas de hacerlo:

* Un proceso de auditoría que se ejecute como parte de la actualización marcará las columnas que se van a volver a comprobar.

   >[!NOTE]
   >
   >El auditor depende de un proceso de muestreo y es posible que las columnas cambiantes no se capten inmediatamente.

* Puede configurarlas usted mismo seleccionando la casilla de verificación situada junto a la columna en el administrador de Datas Warehouse, haciendo clic en **[!UICONTROL Set Recheck Frequency]**, y elegir un intervalo de tiempo adecuado para determinar cuándo debemos comprobar los cambios.
* Un miembro de [!DNL MBI] El equipo de Data Warehouse puede marcar manualmente las columnas para volver a comprobar en la Data Warehouse. Si tiene conocimiento de que se pueden cambiar las columnas, póngase en contacto con el equipo para solicitar que se establezcan comprobaciones adicionales. Incluya una lista de columnas, junto con la frecuencia, con su solicitud.

## Volver a comprobar las frecuencias {#frequency}

**¿Sabías?**
Configuración de una nueva comprobación en una `primary key` no comprueba si hay cambios en la columna. Se buscarán filas eliminadas en la tabla y las eliminaciones se purgarán de la Data Warehouse.

Cuando se marca una columna para volver a comprobarla, también se puede definir la frecuencia con la que se produce una nueva comprobación. Si una columna en particular cambia con menos frecuencia, la elección de una nueva comprobación menos frecuente puede [optimizar el ciclo de actualización](../../best-practices/reduce-update-cycle-time.md).

Las opciones de frecuencia son:

* `always` - la nueva comprobación se produce durante cada actualización
* `daily` - la nueva comprobación se produce la primera actualización posterior a la medianoche para la zona horaria declarada
* `weekly` - la nueva comprobación se produce después de las 21:00 h, actualización del viernes cada semana para su zona horaria declarada
* `monthly` - la nueva comprobación se produce después de las 21:00 h, actualización del viernes cada 4 semanas para su zona horaria declarada
* `once` - solo se produce en la siguiente actualización (una actualización única)

Como los tiempos de actualización se correlacionan con la cantidad de datos que deben sincronizarse, se recomienda elegir un `daily`, `weekly`o `monthly` vuelva a comprobar en lugar de cada actualización.

## Administración de frecuencias de recomprobación {#manage}

Para volver a comprobar las frecuencias, haga clic en el nombre de una tabla y compruebe las columnas individuales en la Data Warehouse. El estado de sincronización y la frecuencia de nueva comprobación (la variable **¿Cambios?** ) se muestra para cada columna de la tabla.

Para cambiar la frecuencia de la nueva comprobación, haga clic en la casilla de verificación situada junto a las columnas que desee cambiar y, a continuación, haga clic en el botón **[!UICONTROL Set Recheck Frequency]** y establezca la frecuencia deseada.

![](../../assets/dwm-recheck.png)

A veces puede ver `Paused` en el `Changes?` para abrir el Navegador. Este valor se mostrará cuando se use la variable [método de replicación](../../data-analyst/data-warehouse-mgr/cfg-data-rechecks.md) está configurado como `Paused`.

Se recomienda revisar estas columnas para optimizar las actualizaciones y garantizar que se vuelvan a comprobar las columnas modificables. Si la frecuencia de recomprobación de una columna es innecesariamente alta, dada la frecuencia con la que cambiarán los datos, se recomienda reducirla para optimizar las actualizaciones.

Póngase en contacto con nosotros con preguntas o para consultar sobre los métodos de replicación o recomprobaciones actuales.

**Relacionado:**

* [Reducción de los tiempos de actualización](../../best-practices/reduce-update-cycle-time.md)
* [Optimización de la base de datos para análisis](../../best-practices/opt-db-analysis.md)
