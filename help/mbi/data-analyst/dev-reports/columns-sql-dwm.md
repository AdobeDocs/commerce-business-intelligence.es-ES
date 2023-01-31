---
title: Diferencias entre SQL y Administrador de Datas Warehouse
description: Conozca las diferencias entre SQL y el Administrador de Datas Warehouse.
exl-id: 31dd7a04-5c03-4399-b67e-f51703eb9fea
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '223'
ht-degree: 0%

---

# Diferencias entre SQL y Administrador de Datas Warehouse

Existen dos diferencias clave entre las columnas creadas en la variable [Report Builder SQL](../dev-reports/sql-rpt-bldr.md) y los creados con el [Administrador de Datas Warehouse](../data-warehouse-mgr/creating-calculated-columns.md): una es la dependencia de los ciclos de actualización, la otra es cómo se guardan las columnas en la cuenta.

## Columnas del `SQL Report Builder`

Las columnas no dependen de los ciclos de actualización, por lo que ya no tendrá que esperar a que se complete una antes de poder iterar en la columna. Si comete un error, solo se tardan unas pocas pulsaciones de teclas en corregirlo, ya que no hay que esperar a que dos actualizaciones terminen antes de volver al trabajo.

>[!IMPORTANT]
>
>Las columnas que cree con el editor SQL no se guardan en la Data Warehouse. Siempre tiene acceso a la consulta que contiene la columna, pero si desea utilizar la columna en más de un informe, debe volver a crearla en la consulta de cada informe. Esto significa que las columnas creadas con el editor SQL no se pueden usar en la `Report Builder`.

## Columnas del Administrador de Datas Warehouse

Las columnas dependen de los ciclos de actualización, por lo que un ciclo completo debe completarse antes de editarse. Estas columnas se guardan en el Administrador de Datas Warehouse y se pueden utilizar en la `Report Builder` o `SQL Report Builder`.
