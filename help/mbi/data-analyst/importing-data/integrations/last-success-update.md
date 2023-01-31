---
title: Comprender los resultados entre Database y SQL Editor
description: Aprenda a comprender los resultados entre la base de datos y el editor SQL.
exl-id: f31f3eef-791a-4984-901e-bc10554031bd
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '259'
ht-degree: 0%

---

# Resultados de la base de datos frente a `SQL Editor` Resultados

Puede que tenga curiosidad sobre qué es `Last successful update began` el campo está dentro de la `Integrations` página:

![Last_success_update.png](../../../assets/Last_successful_update.png)

## Comprender el `timestamp` field

Muestra el inicio `timestamp` (en la zona horaria configurada en su cuenta) de la variable _último ciclo de actualización correcto_ en su cuenta.

- Si alguna de las tablas sincronizadas ha encontrado un problema durante el último ciclo de actualización, esta marca de tiempo es *no actualizado*.
- Por lo tanto, puede haber casos en que los informes se hayan actualizado con datos nuevos, pero la variable *Última actualización correcta iniciada* sigue rezagado.

## Identificar el último punto de datos &quot;real&quot;

El último punto de datos para una integración en particular se determina mediante la variable `Last Data Point Received` `timestamp` situado a la derecha de cada integración. Esa marca de tiempo hace referencia al último punto en el que el almacén de datos recibió puntos de datos correctamente de esa fuente, ya sea una base de datos, API o integración de terceros.

Para comprobar la actualización de los datos de *tablas específicas*, le recomendamos que cree un [Informe SQL](../../dev-reports/sql-rpt-bldr.md) que realiza una `MAX(timestamp)` en la tabla más importante de su cuenta. Comparación de esta marca de tiempo con la variable `Last Data Point` indicará si el problema afectó a toda la cuenta o a un subconjunto de las tablas. Se recomienda hacer esto para tres a cuatro tablas importantes de uso común.

- Si la variable `MAX(timestamp)` los valores son más recientes que `Last Data Point Received`, significa que un subconjunto de las tablas se vio afectado, pero el ciclo de actualización general de la cuenta es estable.
- Si la variable `MAX(timestamp)` los valores son iguales o anteriores a `Last Data Point Received`, significa que el ciclo de actualización de la cuenta se vio afectado. En esta situación, [enviar un ticket de asistencia](../../../guide-overview.md).
