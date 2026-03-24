---
title: Modificación de la Base de Datos para Apoyar la Replicación Incremental
description: Aprenda a modificar la base de datos para que admita la replicación incremental.
exl-id: c9a38892-6096-4eb5-8a53-35b8b7b083dc
role: Admin, Developer, User
feature: Data Integration, Data Import/Export, Data Warehouse Manager
TQID: https://experienceleague.adobe.com/VH5mhfRJteAxiQAmh14TzhnAqym65X6SFRMGuSuEvwM
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
  - id: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2:
  - id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 334
ht-degree: 0%

---

# Compatibilidad con replicación incremental

Si las tablas actualmente no permiten la replicación incremental, consulte las siguientes recomendaciones para posibles soluciones.

## Modificaciones para Modificado en

El método `Modified At`, que es el método de replicación más ideal, utiliza una columna `datetime` para detectar datos nuevos o actualizados. Recuerde que la columna `datetime` de las tablas que utilizan este método debe estar indizada y no puede contener valores nulos en ningún momento.

Si la tabla no tiene una columna `datetime`, puede agregar una columna de índice `modified at`. No se permiten valores nulos en una columna `modified at`. Compruebe que la columna se rellena para cada fila.

Para asegurarse de que el método `Modified At` funciona según lo previsto, no puede eliminar filas de la tabla. En su lugar, debe marcar la fila como no válida agregando una columna `deleted` a la tabla. Esta columna devuelve un `1` si la fila no es válida y `0` en caso contrario. A continuación, puede utilizar esta columna para filtrar las filas no válidas cuando cree métricas e informes.

## Modificaciones para clave principal de incremento automático único

Si el método `Modified At` no se puede habilitar, entonces la clave principal de incremento automático único es la siguiente mejor opción. Los nuevos datos se detectan en tablas utilizando este método al buscar valores de clave principal superiores al valor más alto actual en Data Warehouse.

Recuerde que las tablas que utilizan este método son de una sola columna con claves principales de aumento automático de enteros. Para utilizar este método en la base de datos, realice las siguientes modificaciones:

* Si la clave principal es una clave compuesta o una no entera, cambie la clave principal a un entero que incremente automáticamente
* Si la clave principal es una sola columna entera pero las claves se pueden asignar de forma no secuencial, cambie la clave principal a incremento automático

## Ajuste

Si realiza pequeñas modificaciones en las tablas, puede aprovechar los métodos de replicación incremental más rápidos y eficientes. Sin embargo, si esto no es posible, puedes seguir dando otros pasos para [reducir el tiempo de actualización](../best-practices/reduce-update-cycle-time.md) y [optimizar tu base de datos](../best-practices/opt-db-analysis.md).
