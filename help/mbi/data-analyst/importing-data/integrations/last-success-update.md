---
title: Comprender los resultados entre la base de datos y el editor SQL
description: Aprenda a comprender los resultados entre la base de datos y el editor SQL.
exl-id: f31f3eef-791a-4984-901e-bc10554031bd
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '266'
ht-degree: 0%

---

# Resultados de base de datos vs [!DNL SQL Editor] Resultados

Puede que tengas curiosidad por saber qué `Last successful update began` El campo está dentro de su `Integrations` página:

![Last_successful_update.png](../../../assets/Last_successful_update.png)

## Comprender el `timestamp` campo

Muestra el inicio `timestamp` (en la zona horaria establecida en su cuenta) del _último ciclo de actualización correcto_ en su cuenta.

- Si alguna de las tablas sincronizadas encuentra un problema durante el último ciclo de actualización, esta marca de tiempo es *sin actualizar*.
- Por lo tanto, puede haber casos en los que los informes se hayan actualizado con datos nuevos, pero la variable *Se inició la última actualización correcta* todavía está rezagado.

## Identificar el último punto de datos &quot;real&quot;

El punto de datos más reciente para una integración en particular está determinado por la variable `Last Data Point Received` marca de tiempo situada a la derecha de cada integración. Esa marca de tiempo hace referencia al último punto en el que la Data Warehouse recibió correctamente los puntos de datos de esa fuente, ya sea una base de datos, una API o una integración de terceros.

Para comprobar la actualización de los datos de *tablas específicas*, el Adobe recomienda crear un [[!DNL SQL] informe](../../dev-reports/sql-rpt-bldr.md) que realiza una `MAX(timestamp)` en la tabla más importante de su cuenta. Comparación de esta marca de tiempo con la `Last Data Point` indica si el problema afectó a toda la cuenta o a un subconjunto de las tablas. El Adobe recomienda hacer esto de tres a cuatro tablas importantes de uso común.

- Si la variable `MAX(timestamp)` Los valores son más recientes que `Last Data Point Received`, significa que un subconjunto de las tablas se vio afectado, pero el ciclo de actualización de la cuenta general es estable.
- Si la variable `MAX(timestamp)` valores iguales o anteriores a `Last Data Point Received`, significa que el ciclo de actualización de la cuenta se vio afectado. En esta situación, [enviar un ticket de asistencia](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
