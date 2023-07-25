---
title: Operadores de filtros especiales
description: Obtenga información sobre algunos operadores especiales que se utilizan en los filtros al crear un informe o una métrica.
exl-id: 12837490-b9ca-4040-bb71-8988b5dde485
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '147'
ht-degree: 0%

---

# Opciones de filtro

En este tema se explican algunas características especiales `operators` se usa en `filters` cuando [creación de un informe](../../tutorials/using-visual-report-builder.md){: target=&quot;_blank&quot;} o [creación de una métrica](../../data-user/reports/ess-manage-data-metrics.md){: target=&quot;_blank&quot;}.

## `Filter Operators`

* `LIKE` para la coincidencia de patrones. Se debe utilizar con los caracteres comodín % (para un comodín con un número variable de letras) o _ (para una letra comodín única).  Por ejemplo, la restricción `LIKE \_ake%` devolvería el valor verdadero durante `Jake Stein`, `Jake Smith`, o `Fake Smith`.  Devolvería false para `Drake Smith`.

* `NOT LIKE` es similar a la coincidencia de patrones anterior, pero comprueba qué patrones no coinciden.

* `IS` comprueba si la columna es `NULL`, o vacío.

* `IS NOT` es similar a la `IS` operador anterior, pero comprueba las columnas no nulas.

* `IN` comprueba la presencia de un valor en una lista separada por comas. (por ejemplo, &quot;Color `IN` rojo, &quot;naranja&quot; es el equivalente de color `equal to` color rojo OR `equal to` naranja).

* `NOT IN` es similar a `IN` arriba, pero comprueba la ausencia de un valor.
