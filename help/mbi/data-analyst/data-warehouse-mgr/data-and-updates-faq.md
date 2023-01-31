---
title: Información sobre actualizaciones y datos
description: Obtenga información sobre cómo comprobar el estado del ciclo de actualización.
exl-id: a4a2e487-b826-4888-baf0-9d246a8ff153
source-git-commit: 09b6983c3e06a1f18035542dfa3b9de9ac3ceb38
workflow-type: tm+mt
source-wordcount: '401'
ht-degree: 0%

---

# Información sobre actualizaciones y datos

* [¿Por qué han cambiado mis datos?](#datachange)
* [¿Cuál es la diferencia entre una actualización regular y forzada?](#regularforcedupdates)
* [¿Por qué el ciclo de actualización lleva mucho tiempo?](#updatecycletime)
* [¿Se puede notificar cuando se completa un ciclo de actualización?](#notifyupdate)
* [Por qué [!DNL Google ECommerce] datos diferentes de mi base de datos?](#ecommdatabase)
* [¿Cómo puedo solucionar una discrepancia en los datos?](#datadiscrepancy)

## ¿Por qué han cambiado mis datos? {#datachange}

Los valores de los gráficos pueden cambiar a lo largo del día debido a que los nuevos datos se sincronizan con el almacén de datos. Además, los valores de las columnas de datos existentes pueden cambiar debido a [recomprobaciones](../data-warehouse-mgr/cfg-data-rechecks.md). Una nueva comprobación es un proceso que busca valores modificados en las columnas de datos; por ejemplo, un estado de pedido que se mueve de `open` a `shipped`.

Hay varias formas [para comprobar el estado del ciclo de actualización](../../best-practices/check-update-cycle.md), según el tipo de permisos de usuario que tenga.

## ¿Cuál es la diferencia entre una actualización regular y forzada? {#regularforcedupdates}

Las actualizaciones regulares **programado** procesos mientras las actualizaciones forzadas son **procesos manuales iniciados por usted**. Si tiene horas de interrupción o un período de tiempo en el que [!DNL MBI] no debería actualizar sus datos. Si fuerza una actualización, se iniciará un ciclo que no respete las limitaciones del periodo de interrupción.

## ¿Por qué el ciclo de actualización lleva mucho tiempo? {#updatecycletime}

Muchos factores pueden agregar a un tiempo de actualización ya largo. Cierto [métodos de replicación](../data-warehouse-mgr/cfg-replication-methods.md), [frecuencias de recomprobación superiores](../data-warehouse-mgr/cfg-data-rechecks.md), y el número de tableros y gráficos son solo algunos colaboradores. Recomendamos [reconfiguración de algunos de los ajustes](../../best-practices/reduce-update-cycle-time.md) y [optimización de la base de datos para su análisis](../../best-practices/opt-db-analysis.md) para reducir los tiempos de actualización.

## ¿Se puede notificar cuando se completa un ciclo de actualización? {#notifyupdate}

¡Absolutamente! Si una actualización está actualmente en curso, habrá un vínculo en la variable `Connections` que puede utilizar para solicitar una notificación por correo electrónico una vez que se haya completado el ciclo.

## Por qué[!DNL Google ECommerce]datos diferentes de mi base de datos? {#ecommdatabase}

Discrepancias entre [!DNL Google Analytics] y la base de datos puede aparecer por varios motivos. El seguimiento no está correctamente habilitado, los usuarios que visitan incógnito y los eventos de clic que no funcionan correctamente son solo algunos ejemplos. Si sus ingresos y pedidos no parecen correctos, [utilice este artículo](https://support.magento.com/hc/en-us/articles/360016505232) para diagnosticar el problema.

## ¿Cómo puedo solucionar una discrepancia en los datos? {#datadiscrepancy}

Sabemos que ver datos incoherentes puede ser una experiencia frustrante. Pruebe con nuestra [Lista de comprobación de discrepancia de datos](https://support.magento.com/hc/en-us/articles/360016731271) o [Tutorial sobre exportaciones de datos](https://support.magento.com/hc/en-us/articles/360016730631) para diagnosticar el problema. Si todavía estás tropezado, [póngase en contacto con el servicio de asistencia técnica](../../guide-overview.md).
