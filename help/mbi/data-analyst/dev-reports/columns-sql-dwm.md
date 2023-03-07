---
title: Diferencias entre SQL y el Administrador de Datas Warehouse
description: Conozca las diferencias entre SQL y el Administrador de Datas Warehouse.
exl-id: 31dd7a04-5c03-4399-b67e-f51703eb9fea
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '222'
ht-degree: 0%

---

# Diferencias entre SQL y el Administrador de Datas Warehouse

Existen dos diferencias clave entre las columnas creadas en la variable [REPORT BUILDER SQL](../dev-reports/sql-rpt-bldr.md) y los creados con la variable [Administrador de Datas Warehouse](../data-warehouse-mgr/creating-calculated-columns.md). Una es la dependencia de los ciclos de actualización y la otra es cómo se guardan las columnas en la cuenta.

## Columnas en la `SQL Report Builder`

Las columnas no dependen de los ciclos de actualización, por lo que ya no tiene que esperar a que una se complete para poder iterar en la columna. Si comete un error, solo se necesitan unas pocas pulsaciones para corregirlo: ya no tendrá que esperar a que se ajusten dos actualizaciones antes de volver al trabajo.

>[!IMPORTANT]
>
>Las columnas que cree con el editor SQL no se guardarán en la Data Warehouse. Siempre tiene acceso a la consulta que contiene la columna, pero si desea utilizar la columna en más de un informe, debe volver a crearla en la consulta de cada informe. Esto significa que las columnas creadas con el editor SQL no se pueden utilizar en el `Report Builder`.

## Columnas del Administrador de Datas Warehouse

Las columnas dependen de los ciclos de actualización, por lo que se debe completar un ciclo completo antes de poder editarlas. Estas columnas se guardan en el Administrador de Datas Warehouse y se pueden utilizar en el `Report Builder` o `SQL Report Builder`.
