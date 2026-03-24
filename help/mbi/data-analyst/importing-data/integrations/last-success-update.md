---
title: Comprender los resultados entre la base de datos y el editor SQL
description: Aprenda a comprender los resultados entre la base de datos y el editor SQL.
exl-id: f31f3eef-791a-4984-901e-bc10554031bd
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
TQID: https://experienceleague.adobe.com/pScH-yKW8hbSNZzsJ537CN7rxhcuygaLmCu3fdVaYgk
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: c1579802-ddd4-4214-8a91-97b2066abe11
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 257
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
