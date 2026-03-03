---
title: Operadores de filtros especiales
description: Obtenga información sobre algunos operadores especiales que se utilizan en los filtros al crear un informe o una métrica.
exl-id: 12837490-b9ca-4040-bb71-8988b5dde485
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 5e80ff8f8ec76996b88a22b115be696b110581be
workflow-type: tm+mt
source-wordcount: '143'
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
