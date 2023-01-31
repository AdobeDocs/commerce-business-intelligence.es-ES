---
title: Operadores de filtro especiales
description: Obtenga información sobre algunos operadores especiales que se utilizan en los filtros al crear un informe o una métrica.
exl-id: 12837490-b9ca-4040-bb71-8988b5dde485
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '154'
ht-degree: 0%

---

# Opciones de filtro

En este artículo, vamos a explorar algunas `operators` se usa en `filters` when [creación de informes](../../tutorials/using-visual-report-builder.md){: target=&quot;_blank&quot;} o [creación de una métrica](../../data-user/reports/ess-manage-data-metrics.md){: target=&quot;_blank&quot;}.

## `Filter Operators`

* `LIKE` para la coincidencia de patrones. Debe utilizarse junto con los caracteres comodín % (para un comodín con un número variable de letras) o _ (para una letra única comodín).  Por ejemplo, la restricción `LIKE \_ake%` devolverá true como `Jake Stein`, `Jake Smith`o `Fake Smith`.  Devolvería false para `Drake Smith`.

* `NOT LIKE` es similar a la coincidencia de patrones anterior, pero comprueba qué patrones no coinciden.

* `IS` comprueba si la columna es `NULL`, o vacío.

* `IS NOT` es similar a la variable `IS` operador anterior, pero comprueba las columnas que no sean NULL.

* `IN` comprueba la presencia de un valor en una lista separada por comas. (por ejemplo, &quot;Color&quot; `IN` rojo,naranja&quot; es el equivalente de color `equal to` color rojo O `equal to` naranja).

* `NOT IN` es similar a `IN` más arriba, pero comprueba la ausencia de un valor.
