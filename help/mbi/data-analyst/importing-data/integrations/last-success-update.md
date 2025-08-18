---
title: Comprender los resultados entre la base de datos y el editor SQL
description: Aprenda a comprender los resultados entre la base de datos y el editor SQL.
exl-id: f31f3eef-791a-4984-901e-bc10554031bd
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '257'
ht-degree: 0%

---

# Resultados de base de datos vs. [!DNL SQL Editor] resultados

Puede que tenga curiosidad sobre cuál es el campo `Last successful update began` dentro de su página `Integrations`:

![Última_actualización_correcta.png](../../../assets/Last_successful_update.png)

## Comprender el campo `timestamp`

Muestra el inicio `timestamp` (en la zona horaria establecida en su cuenta) del _último ciclo de actualización correcto_ en su cuenta.

- Si alguna de las tablas sincronizadas encontró un problema durante el último ciclo de actualización, esta marca de tiempo es *no se ha actualizado*.
- Por lo tanto, puede haber casos en los que los informes se hayan actualizado con datos nuevos, pero la *última actualización correcta iniciada* todavía está rezagada.

## Identificar el último punto de datos &quot;real&quot;

El punto de datos más reciente de una integración determinada se determina mediante la marca de tiempo `Last Data Point Received` ubicada a la derecha de cada integración. Esa marca de tiempo hace referencia al último punto en el que Data Warehouse recibió correctamente los puntos de datos de esa fuente, ya sea una base de datos, una API o una integración de terceros.

Para comprobar la actualización de los datos de *tablas específicas*, Adobe recomienda crear un [[!DNL SQL] informe](../../dev-reports/sql-rpt-bldr.md) rápido que realice un `MAX(timestamp)` en la tabla más importante de su cuenta. Comparar esta marca de tiempo con `Last Data Point` indica si el problema afectó a toda la cuenta o a un subconjunto de las tablas. Adobe recomienda hacerlo de tres a cuatro tablas importantes de uso común.

- Si los valores de `MAX(timestamp)` son más recientes que `Last Data Point Received`, significa que un subconjunto de las tablas se vio afectado, pero el ciclo de actualización de la cuenta general es estable.
- Si los valores de `MAX(timestamp)` son iguales o anteriores a `Last Data Point Received`, significa que el ciclo de actualización de la cuenta se vio afectado. En esta situación, [envíe un vale de soporte técnico](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html).
