---
title: Operadores de filtros especiales
description: Obtenga información sobre algunos operadores especiales que se utilizan en los filtros al crear un informe o una métrica.
exl-id: 12837490-b9ca-4040-bb71-8988b5dde485
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
TQID: https://experienceleague.adobe.com/xUfPCWqheQFIG9faVsA5PEWiyn6hLO-Rrm8jPzmaWiw
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 143
ht-degree: 0%

---

# Opciones de filtro

En este tema se explican algunos `operators` especiales que se usaron en `filters` al [crear un informe](../../tutorials/using-visual-report-builder.md){: target="_blank"} o [crear una métrica](../../data-user/reports/ess-manage-data-metrics.md){: target="_blank"}.

## `Filter Operators`

* `LIKE` para coincidencia de patrones. Se debe utilizar con los caracteres comodín % (para un comodín con un número variable de letras) o _ (para una letra comodín única).  Por ejemplo, la restricción `LIKE \_ake%` devolverá true para `Jake Stein`, `Jake Smith` o `Fake Smith`.  Devolvería false para `Drake Smith`.

* `NOT LIKE` es similar a la coincidencia de patrones anterior, pero comprueba qué patrones no coinciden.

* `IS` comprueba si la columna es `NULL` o si está vacía.

* `IS NOT` es similar al operador `IS` anterior, pero comprueba si hay columnas que no sean nulas.

* `IN` comprueba la presencia de un valor en una lista separada por comas. (por ejemplo, &quot;Color `IN` rojo, naranja&quot; es el equivalente del color `equal to` rojo O del color `equal to` naranja).

* `NOT IN` es similar a `IN` anterior, pero comprueba la ausencia de un valor.
