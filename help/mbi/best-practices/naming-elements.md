---
title: Asignar nombres a informes y elementos en Commerce Intelligence
description: Conozca las prácticas recomendadas para nombrar informes y elementos en  [!DNL Commerce Intelligence].
exl-id: c662cedd-c779-4254-b04b-f3092a538c85
role: Admin, User
feature: Reports
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '725'
ht-degree: 0%

---

# Nombrar informes y elementos

Antes de empezar a generar en [!DNL Adobe Commerce Intelligence], Adobe desea compartir algunos secretos para tener éxito. Saber cómo crear métricas, filtros, etc., es importante, pero todo su trabajo puede ser en vano si no encuentra lo que necesita o si hay ambigüedad.

## ¿Por qué es importante la nomenclatura? {#why}

La forma en que asigne nombres a las columnas calculadas, las métricas y los informes dicta la facilidad con que los distintos usuarios pueden navegar por la cuenta de [!DNL Commerce Intelligence]. Al nombrar estas funciones, tenga en cuenta las tres C:

* **CLARIDAD**: de este modo podrá saber de un vistazo qué está mostrando un informe, qué hace una métrica, etc.
* **COHERENCIA**: para que usted (y el equipo de soporte técnico de Adobe) puedan encontrar y comprender fácilmente los elementos e informes de su cuenta.
* **CREDIBILIDAD**: para inspirar y empoderar a otros usuarios de [!DNL Commerce Intelligence] impulsados por datos, debe infundir confianza en cómo entienden y utilizan los datos.

Sigue leyendo para consejos de nomenclatura probados y verdaderos!

## Prácticas recomendadas generales {#general}

### Ser significativo {#meaningful}

¡Sea específico siempre que sea posible! Por ejemplo, si es el país, ¿sabe si es el país de envío o de facturación? ¿Es la ciudad del usuario, o es la ciudad del trato?

**Ejemplo incorrecto:**
Ingresos

Esto es vago y no nos dice mucho.

**Buenos ejemplos:**
Ingresos (total general base + tarifa)
País de envío del usuario

Estos ejemplos son específicos, lo que reduce el potencial de confusión.

### Ser coherente con las mayúsculas {#capitalize}

[!DNL Adobe] recomienda la primera letra en mayúscula con el resto de los caracteres en minúscula, a menos que se utilice el sustantivo adecuado como estilo de uso de mayúsculas. Por ejemplo, **número de pedido del usuario** en lugar de **número de pedido del usuario**.

Esto es realmente una cuestión de preferencia, pero lo que hay que recordar es ser coherente con lo que usted elija.

### Coherencia de entidad {#entity}

Es probable que ya tenga una nomenclatura en vigor en su empresa. Mantenga la coherencia de las métricas y dimensiones que establezca con lo que se utiliza en otras bases de datos y herramientas. Por ejemplo:

* Usuario vs. Cliente vs. Miembro vs. Cuenta
* Empresa vs. Cuenta vs. Organización
* Registro y creación

### Ortografía y gramática {#spelling}

¡Asegúrate de revisar tu ortografía y no te olvides de esos molestos posesivos!

## Gráficos {#charts}

Al nombrar [gráficos](../tutorials/using-visual-report-builder.md), es muy útil seguir esta fórmula: **(Perspectiva de datos) + (Métrica) + (Período de tiempo) + (Intervalo de tiempo)**

**Ejemplo incorrecto:**
Ingresos

Esto no nos dice nada sobre el informe, lo cual es malo.

**Buen ejemplo:**
Ingresos acumulados pasados 30 días por mes

Esto nos dice **exactamente** lo que hay en el informe, lo cual es fantástico.

## Paneles {#dashboards}

Los paneles deben nombrarse de manera que representen temáticamente los informes contenidos en ellos. Por ejemplo, si el tablero contiene únicamente información relacionada con los ingresos y pedidos, considere ponerle un nombre similar a **Nombre de tienda - Ingresos y pedidos.**

Por el contrario, si el tablero es un lugar en el que experimenta con distintos informes, considere la posibilidad de ponerle el nombre **Espacio aislado de su nombre** para saber que los informes contenidos en él son borradores.

## Dimension (Columnas calculadas) {#dimensions}

Al nombrar las nuevas [dimensiones](../data-analyst/data-warehouse-mgr/creating-calculated-columns.md), es muy útil seguir esta fórmula: **(Entidad) + (Nth) + (lapso de tiempo) + (cálculo) + (comentarios)**. Por ejemplo:

Ingresos de los primeros 30 días del usuario
* Número de pedido del usuario
* Número de pedido del usuario (a la espera de auditoría)

## Conjuntos de filtros {#filterset}

[Los conjuntos de filtros](../data-user/reports/ess-manage-data-filters.md) suelen tener nombres que explican la información que incluyen o excluyen. Por ejemplo, nombrar un conjunto de filtros **Elementos de pedidos que contamos** permite a cualquier usuario entrar, ver la lógica del conjunto de filtros y comprender qué información de pedidos determina qué se cuenta en la empresa. Recuerde que los conjuntos de filtros se pueden aplicar tanto a columnas calculadas como a métricas y deben ser fáciles de entender.

## Métricas {#metrics}

[Las métricas](../data-user/reports/ess-manage-data-metrics.md) son esencialmente preguntas a las que desea respuestas con regularidad. ¿Cuál fue el número de pedidos en el último mes? ¿Cuál es el valor promedio de duración de sus clientes? Se recomienda asignar nombres a las métricas para reflejar la respuesta que dan a los usuarios. Además, si tiene la misma métrica filtrada para un almacén o departamento específico, debe etiquetarlos como tal. Por ejemplo:

LTV promedio del cliente (primeros 30 días)
Nombre de tienda - Ingresos

Por último, la misma métrica a veces se puede organizar por marcas de tiempo diferentes, según la forma en que lo calculen los usuarios individuales. Si es así, asegúrese de incluir la marca de tiempo en el nombre:

Ingresos (enviados\_at)
Ingresos (creado\_at)

## Ajuste {#wrapup}

El establecimiento anticipado de convenciones de estilo y nomenclatura le ayudará a configurar correctamente su cuenta de [!DNL Commerce Intelligence]. Recuerde las tres C: claridad, coherencia y credibilidad.
