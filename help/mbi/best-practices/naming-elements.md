---
title: Nombrar informes y elementos en MBI
description: Conozca las prácticas recomendadas para nombrar informes y elementos en [!DNL MBI].
exl-id: c662cedd-c779-4254-b04b-f3092a538c85
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 0%

---

# Nombrar informes y elementos

Antes de empezar a generar en[!DNL MBI]Sin embargo, el Adobe quiere compartir algunos secretos para el éxito. Saber cómo crear métricas, filtros, etc., es importante, pero todo su trabajo puede ser en vano si no encuentra lo que necesita o si hay ambigüedad.

## ¿Por qué es importante la nomenclatura? {#why}

La forma en que asigne un nombre a las columnas, métricas e informes calculados dicta la facilidad con la que los distintos usuarios pueden navegar por el [!DNL MBI] cuenta. Al nombrar estas funciones, tenga en cuenta las tres C:

* **CLARIDAD** : para poder saber de un vistazo lo que muestra un informe, lo que hace una métrica, etc.
* **COHERENCIA** - Para que usted (y el equipo de asistencia de Adobe) puedan encontrar y comprender fácilmente los elementos e informes de su cuenta.
* **CREDIBILIDAD** - Con el fin de inspirar y empoderar a otras fuentes de datos [!DNL MBI] Para los usuarios de, debe infundir confianza en cómo entienden y utilizan los datos.

Sigue leyendo para consejos de nomenclatura probados y verdaderos!

## Prácticas recomendadas generales {#general}

### Ser significativo {#meaningful}

¡Sea específico siempre que sea posible! Por ejemplo, si es el país, ¿sabe si es el país de envío o de facturación? ¿Es la ciudad del usuario, o es la ciudad del trato?

**Ejemplo incorrecto:**
Ingresos

Esto es vago y no nos dice mucho.

**Buenos ejemplos:**
Ingresos (total general base + tarifa) País de envío del usuario

Estos ejemplos son específicos, lo que reduce el potencial de confusión.

### Ser coherente con las mayúsculas {#capitalize}

El Adobe recomienda que la primera letra esté en mayúsculas y el resto de los caracteres en minúsculas, a menos que el estilo de sustantivo adecuado sea mayúsculas. Por ejemplo, **Número de pedido del usuario** en lugar de **Número de pedido del usuario.**

Esto es realmente una cuestión de preferencia, pero lo que hay que recordar es ser coherente con lo que usted elija.

### Coherencia de entidad {#entity}

Es probable que ya tenga una nomenclatura en vigor en su empresa. Mantenga la coherencia de las métricas y dimensiones que establezca con lo que se utiliza en otras bases de datos y herramientas. Por ejemplo:

* Usuario vs. Cliente vs. Miembro vs. Cuenta
* Empresa vs. Cuenta vs. Organización
* Registro y creación

### Ortografía y gramática {#spelling}

¡Asegúrate de revisar tu ortografía y no te olvides de esos molestos posesivos!

## Gráficos {#charts}

Al nombrar [tablas](../tutorials/using-visual-report-builder.md)Sin embargo, es más útil seguir esta fórmula: **(Perspectiva de datos) + (Métrica) + (Período de tiempo) + (Intervalo de tiempo)**

**Ejemplo incorrecto:**
Ingresos

Esto no nos dice nada sobre el informe, lo cual es malo.

**Buen ejemplo:**
Ingresos acumulados pasados 30 días por mes

Esto nos dice **exacto** lo que figura en el informe, que es fantástico.

## Paneles {#dashboards}

Los paneles deben nombrarse de manera que representen temáticamente los informes contenidos en ellos. Por ejemplo, si el tablero contiene únicamente información relacionada con los ingresos y los pedidos, considere ponerle un nombre similar al siguiente **Nombre de la tienda: ingresos y pedidos.**

Por el contrario, si el tablero es un lugar en el que está experimentando con distintos informes, considere la posibilidad de ponerle un nombre **Su nombre es Sandbox** por lo tanto, sabe que los informes que contiene son borradores.

## Dimension (Columnas calculadas) {#dimensions}

Al nombrar nuevo [dimensiones](../data-analyst/data-warehouse-mgr/creating-calculated-columns.md)Sin embargo, es más útil seguir esta fórmula: **(Entidad) + (Nth) + (lapso de tiempo) + (cálculo) + (comentarios)**. Por ejemplo:

Ingresos de los primeros 30 días del usuario
* Número de pedido del usuario
* Número de pedido del usuario (a la espera de auditoría)

## Conjuntos de filtros {#filterset}

[Conjuntos de filtros](../data-user/reports/ess-manage-data-filters.md) suelen denominarse de manera que explican la información que incluyen o excluyen. Por ejemplo, asignar un nombre a un conjunto de filtros **Ordenar elementos que contamos** permite a cualquier usuario entrar, ver la lógica del conjunto de filtros y comprender qué información de pedidos determina qué se cuenta en la empresa. Recuerde que los conjuntos de filtros se pueden aplicar tanto a columnas calculadas como a métricas y deben ser fáciles de entender.

## Métricas {#metrics}

[Métricas](../data-user/reports/ess-manage-data-metrics.md) Son esencialmente preguntas a las que desea respuestas con regularidad. ¿Cuál fue el número de pedidos en el último mes? ¿Cuál es el valor promedio de duración de sus clientes? Se recomienda asignar nombres a las métricas para reflejar la respuesta que dan a los usuarios. Además, si tiene la misma métrica filtrada para un almacén o departamento específico, debe etiquetarlos como tal. Por ejemplo:

Promedio de clientes LTV (primeros 30 días) Nombre de la tienda - Ingresos

Por último, la misma métrica a veces se puede organizar por marcas de tiempo diferentes, según la forma en que lo calculen los usuarios individuales. Si es así, asegúrese de incluir la marca de tiempo en el nombre:

Ingresos (enviado\_at) Ingresos (creado\_at)

## Ajuste {#wrapup}

El establecimiento anticipado de convenciones de estilo y nomenclatura le ayuda a configurar para que tenga éxito en su [!DNL MBI] cuenta. Recuerde las tres C: claridad, coherencia y credibilidad.
