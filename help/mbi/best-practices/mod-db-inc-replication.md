---
title: Modificación de la Base de Datos para el Soporte de Replicación Incremental
description: Aprenda a modificar la base de datos para admitir la replicación incremental.
exl-id: c9a38892-6096-4eb5-8a53-35b8b7b083dc
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '336'
ht-degree: 0%

---

# Soporte para Replicación Incremental

Si las tablas actualmente no permiten la duplicación incremental, consulte las siguientes recomendaciones para posibles soluciones.

## Modificaciones para Modificado a

La variable `Modified At` , que es el método de replicación más ideal, utiliza un `datetime` para detectar datos nuevos o actualizados. Recuerde que `datetime` en las tablas que utilicen este método deben indexarse y no pueden contener valores nulos en ningún momento.

Si la tabla no tiene un `datetime` , puede añadir un índice `modified at` para abrir el Navegador. No se permiten valores nulos en una `modified at` para abrir el Navegador. Compruebe que la columna se rellene para cada fila.

Para garantizar que la variable `Modified At` funciona como se pretende, no se pueden eliminar filas de la tabla. En su lugar, debe marcar la fila como no válida agregando una `deleted` a la tabla. Esta columna devolverá un `1` si la fila no es válida y `0` en caso contrario. A continuación, puede utilizar esta columna para filtrar filas no válidas al crear métricas e informes.

## Modificaciones para la clave principal de aumento automático único

Si la variable `Modified At` no se puede habilitar, entonces la clave principal de aumento automático único es la siguiente mejor opción. En las tablas se descubren nuevos datos utilizando este método buscando valores de clave principal superiores al valor más alto actual de la Data Warehouse.

Recuerde que las tablas que utilizan este método son de una sola columna con un entero que incrementa automáticamente las claves principales. Para utilizar este método en la base de datos, realice las siguientes modificaciones:

* Si la clave principal es una clave compuesta o no un entero, cambie la clave principal a un entero que incremente automáticamente
* Si la clave principal es una única columna entera pero las claves se pueden asignar de forma no secuencial, cambie la clave principal a incremento automático

## Ajuste

Al realizar pequeñas modificaciones en las tablas, puede aprovechar los métodos de replicación incremental más rápidos y eficientes; sin embargo, si aún no es posible, puede seguir realizando otros pasos para [reducir el tiempo de actualización](../best-practices/reduce-update-cycle-time.md) y [optimizar la base de datos](../best-practices/opt-db-analysis.md).
