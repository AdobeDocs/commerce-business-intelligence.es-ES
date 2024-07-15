---
title: Datos e información de actualizaciones
description: Obtenga información sobre cómo comprobar el estado del ciclo de actualización.
exl-id: a4a2e487-b826-4888-baf0-9d246a8ff153
role: Admin, Data Architect, Data Engineer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '378'
ht-degree: 0%

---

# Datos e información de actualizaciones

* [¿Por qué han cambiado mis datos?](#datachange)
* [¿Cuál es la diferencia entre una actualización regular y forzada?](#regularforcedupdates)
* [¿Por qué el ciclo de actualización tarda mucho tiempo?](#updatecycletime)
* [¿Se me puede notificar cuando se completa un ciclo de actualización?](#notifyupdate)
* [¿Por qué hay  [!DNL Google ECommerce] datos diferentes de mi base de datos?](#ecommdatabase)
* [¿Cómo puedo solucionar problemas de discrepancia de datos?](#datadiscrepancy)

## ¿Por qué han cambiado mis datos? {#datachange}

Los valores de los gráficos pueden cambiar durante el día debido a que los nuevos datos se sincronizan con la Data Warehouse. Además, los valores de las columnas de datos existentes pueden cambiar debido a [nuevas comprobaciones](../data-warehouse-mgr/cfg-data-rechecks.md). Una nueva comprobación es un proceso que busca valores modificados en columnas de datos, como un estado de pedido que se mueve de `open` a `shipped`.

Existen varias formas [de comprobar el estado del ciclo de actualización](../../best-practices/check-update-cycle.md), según la configuración de permisos del usuario.

## ¿Cuál es la diferencia entre una actualización regular y forzada? {#regularforcedupdates}

Las actualizaciones regulares son **procesos programados**, mientras que las actualizaciones forzadas son **procesos manuales iniciados por usted**. Si tiene horas de interrupción (o un período de tiempo en el que [!DNL Commerce Intelligence] no debe actualizar sus datos), forzar una actualización inicia un ciclo que no respeta las limitaciones del período de interrupción.

## ¿Por qué el ciclo de actualización tarda mucho tiempo? {#updatecycletime}

Numerosos factores pueden añadir a un tiempo de actualización ya largo. Algunos [métodos de replicación](../data-warehouse-mgr/cfg-replication-methods.md), [frecuencias de comprobación más altas](../data-warehouse-mgr/cfg-data-rechecks.md), y el número de paneles y gráficos son sólo algunos factores que contribuyen. El Adobe recomienda [reconfigurar algunos de tus ajustes](../../best-practices/reduce-update-cycle-time.md) y [optimizar tu base de datos para el análisis](../../best-practices/opt-db-analysis.md) para reducir los tiempos de actualización.

## ¿Se me puede notificar cuando se completa un ciclo de actualización? {#notifyupdate}

Si hay una actualización en curso, hay un vínculo en la página `Connections` que puede usar para solicitar una notificación por correo electrónico una vez que finalice el ciclo.

## ¿Por qué hay [!DNL Google ECommerce]datos diferentes de mi base de datos? {#ecommdatabase}

Las discrepancias entre [!DNL Google Analytics] y la base de datos pueden producirse por varios motivos. El seguimiento no se ha habilitado correctamente, los usuarios que visitan incógnito y los eventos de clic no funcionan correctamente son solo algunos ejemplos. Si los ingresos y los pedidos no se ven correctamente, [vea este tema](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-google-ecommerce-revenue-discrepancies.html) para diagnosticar un problema.

## ¿Cómo puedo solucionar problemas de discrepancia de datos? {#datadiscrepancy}

El Adobe sabe que ver datos incoherentes puede ser una experiencia frustrante. Intente usar la [lista de comprobación de discrepancias de datos](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/diagnosing-a-data-discrepancy.html) o el [tutorial de exportaciones de datos](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/using-data-exports-to-pinpoint-discrepancies.html) para diagnosticar el problema. Si sigues con errores, [ponte en contacto con el servicio de asistencia](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
