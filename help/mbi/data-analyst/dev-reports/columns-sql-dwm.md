---
title: Diferencias entre SQL y Data Warehouse Manager
description: Conozca las diferencias entre SQL y Data Warehouse Manager.
exl-id: 31dd7a04-5c03-4399-b67e-f51703eb9fea
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, SQL Report Builder, Reports
TQID: https://experienceleague.adobe.com/aWLLAi9e-A6Di7AGujRNd79W7GqSRo5yIgmQRZAHOEQ
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
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 210
ht-degree: 0%

---

# Diferencias entre [!DNL SQL] y [!DNL Data Warehouse Manager]

Hay dos diferencias clave entre las columnas creadas en [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) y las creadas con [[!DNL Data Warehouse Manager]](../data-warehouse-mgr/creating-calculated-columns.md). Una es la dependencia de los ciclos de actualización y la otra es cómo se guardan las columnas en la cuenta.

## Columnas en [!DNL SQL Report Builder]

Las columnas no dependen de los ciclos de actualización, por lo que ya no tiene que esperar a que una se complete para poder iterar en la columna. Si comete un error, solo se necesitan unas pocas pulsaciones para corregirlo: ya no tendrá que esperar a que se ajusten dos actualizaciones antes de volver al trabajo.

>[!IMPORTANT]
>
>Las columnas que cree con el editor [!DNL SQL] no se guardarán en el Data Warehouse. Siempre tiene acceso a la consulta que contiene la columna, pero si desea utilizar la columna en más de un informe, debe volver a crearla en la consulta de cada informe. Esto significa que las columnas creadas con el editor [!DNL SQL] no se pueden usar en el editor [!DNL Report Builder] tradicional.

## Columnas en el Administrador de Data Warehouse

Las columnas dependen de los ciclos de actualización, por lo que se debe completar un ciclo completo antes de poder editarlas. Estas columnas se guardan en el Administrador de Data Warehouse y se pueden usar en el [!DNL Report Builder] o [!DNL SQL Report Builder] tradicional.
