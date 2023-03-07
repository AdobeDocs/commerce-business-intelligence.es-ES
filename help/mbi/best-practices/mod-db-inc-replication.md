---
title: Modificación de la Base de Datos para Apoyar la Replicación Incremental
description: Aprenda a modificar la base de datos para que admita la replicación incremental.
exl-id: c9a38892-6096-4eb5-8a53-35b8b7b083dc
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '334'
ht-degree: 0%

---

# Compatibilidad con replicación incremental

Si las tablas actualmente no permiten la replicación incremental, consulte las siguientes recomendaciones para posibles soluciones.

## Modificaciones para Modificado en

El `Modified At` , que es el método de replicación más ideal, utiliza un `datetime` para detectar datos nuevos o actualizados. Recuerde que la variable `datetime` la columna de las tablas que utilizan este método debe estar indexada y no puede contener valores nulos en ningún momento.

Si la tabla no tiene un `datetime` columna, puede añadir un índice `modified at` columna. No se permiten valores nulos en `modified at` columna. Compruebe que la columna se rellena para cada fila.

Para garantizar que `Modified At` funciona según lo previsto, no se pueden eliminar filas de la tabla. En su lugar, debe marcar la fila como no válida agregando un `deleted` a la tabla. Esta columna devuelve un `1` si la fila no es válida y `0` de lo contrario. A continuación, puede utilizar esta columna para filtrar las filas no válidas cuando cree métricas e informes.

## Modificaciones para clave principal de incremento automático único

Si la variable `Modified At` no se puede activar, la clave principal de incremento automático único es la siguiente mejor opción. Los nuevos datos se detectan en tablas utilizando este método al buscar valores de clave principal superiores al valor más alto actual en la Data Warehouse.

Recuerde que las tablas que utilizan este método son de una sola columna con claves principales de aumento automático de enteros. Para utilizar este método en la base de datos, realice las siguientes modificaciones:

* Si la clave principal es una clave compuesta o una no entera, cambie la clave principal a un entero que incremente automáticamente
* Si la clave principal es una sola columna entera pero las claves se pueden asignar de forma no secuencial, cambie la clave principal a incremento automático

## Ajuste

Si realiza pequeñas modificaciones en las tablas, puede aprovechar los métodos de replicación incremental más rápidos y eficientes. Sin embargo, si esto no es posible, aún puede realizar otros pasos para lo siguiente [reducir el tiempo de actualización](../best-practices/reduce-update-cycle-time.md) y [optimizar la base de datos](../best-practices/opt-db-analysis.md).
