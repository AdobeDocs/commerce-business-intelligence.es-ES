---
title: Operadores de filtros especiales
description: Obtenga información sobre algunos operadores especiales que se utilizan en los filtros al crear un informe o una métrica.
exl-id: 12837490-b9ca-4040-bb71-8988b5dde485
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
TQID: 'https://experienceleague.adobe.com/xUfPCWqheQFIG9faVsA5PEWiyn6hLO-Rrm8jPzmaWiw'
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
    internal-label: Commerce Intelligence
  - id: eadea719-cf89-469b-a6fd-a236a7138047
    internal-label: Commerce
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
    internal-label: Data Warehouse Manager
  - id: 5d2a63cb-5675-5572-9de5-bc904157ef45
    internal-label: Commerce Tables
  - id: f842eedf-96a8-52c7-891d-4e56f7441a7e
    internal-label: Reports
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
    internal-label: User
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
    internal-label: Admin
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
    internal-label: Developer
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
    internal-label: Intermediate
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
    internal-label: Beginner
source-git-commit: fdbaf74705fb224414ac8cb69f6a1b34277e3f79
workflow-type: tm+mt
source-wordcount: '145'
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
