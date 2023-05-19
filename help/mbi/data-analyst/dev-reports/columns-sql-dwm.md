---
title: Diferencias entre SQL y el Administrador de Datas Warehouse
description: Conozca las diferencias entre SQL y el Administrador de Datas Warehouse.
exl-id: 31dd7a04-5c03-4399-b67e-f51703eb9fea
source-git-commit: 6b1bd96a0f9ae8bda3ae8db8ca78ad655079f2a4
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---

# Diferencias entre [!DNL SQL] y [!DNL Data Warehouse Manager]

Existen dos diferencias clave entre las columnas creadas en la variable [[!DNL SQL Report Builder]](../dev-reports/sql-rpt-bldr.md) y los creados con la variable [[!DNL Data Warehouse Manager]](../data-warehouse-mgr/creating-calculated-columns.md). Una es la dependencia de los ciclos de actualización y la otra es cómo se guardan las columnas en la cuenta.

## Columnas en la [!DNL SQL Report Builder]

Las columnas no dependen de los ciclos de actualización, por lo que ya no tiene que esperar a que una se complete para poder iterar en la columna. Si comete un error, solo se necesitan unas pocas pulsaciones para corregirlo: ya no tendrá que esperar a que se ajusten dos actualizaciones antes de volver al trabajo.

>[!IMPORTANT]
>
>Las columnas que cree con la variable [!DNL SQL] Los editores de no se guardan en la Data Warehouse. Siempre tiene acceso a la consulta que contiene la columna, pero si desea utilizar la columna en más de un informe, debe volver a crearla en la consulta de cada informe. Esto significa que las columnas creadas con [!DNL SQL] el editor no se puede usar en la versión tradicional [!DNL Report Builder].

## Columnas del Administrador de Datas Warehouse

Las columnas dependen de los ciclos de actualización, por lo que se debe completar un ciclo completo antes de poder editarlas. Estas columnas se guardan en el Administrador de Datas Warehouse y se pueden utilizar en el [!DNL Report Builder] o [!DNL SQL Report Builder].
