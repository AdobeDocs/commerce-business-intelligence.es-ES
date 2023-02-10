---
title: Asignar nombres a informes y elementos en MBI
description: Conozca las prácticas recomendadas para nombrar informes y elementos en [!DNL MBI].
exl-id: c662cedd-c779-4254-b04b-f3092a538c85
source-git-commit: fa954868177b79d703a601a55b9e549ec1bd425e
workflow-type: tm+mt
source-wordcount: '740'
ht-degree: 0%

---

# Nombrar informes y elementos

Antes de empezar a construir[!DNL MBI], queremos compartir algunos de nuestros secretos con éxito. Saber cómo crear métricas, filtros, etc. es importante, pero todo eso funcionará para nada si no encuentra lo que necesita o si no hay ambigüedad.

## ¿Por qué es importante la nomenclatura? {#why}

La forma en que nombra las columnas, métricas e informes calculados dicta la facilidad con la que los distintos usuarios pueden navegar por sus [!DNL MBI] cuenta. Al nombrar estas funciones, nos gusta tener en cuenta las tres C:

* **CLARIDAD** - De modo que puede saber de un vistazo qué muestra un informe, qué hace una métrica, etc.
* **COHERENCIA** - Para que usted (y nuestro equipo de asistencia técnica) puedan encontrar y comprender fácilmente los elementos y los informes de su cuenta.
* **CREDIBILIDAD** - Con el fin de inspirar y empoderar a otros datos [!DNL MBI] usuarios, debe infundir confianza en cómo comprenden y utilizan los datos.

Siga leyendo para ver nuestros consejos probados y verdaderos de la nomenclatura!

## Prácticas recomendadas generales {#general}

### Sea significativo {#meaningful}

Sea específico siempre que sea posible. Por ejemplo, si es el país, ¿sabe si es el envío o el país de facturación? ¿Es la ciudad del usuario, o es la ciudad del acuerdo?

**Ejemplo incorrecto:**
Ingresos

Esto es vago y no nos dice mucho.

**Buenos ejemplos:**
Ingresos (total general base + tarifa) País de envío del usuario

Estos ejemplos son específicos, lo que reduce el potencial de confusión.

### Sea coherente con las mayúsculas {#capitalize}

Somos grandes fans de la primera letra en mayúsculas, el resto de los caracteres en minúsculas a menos que el estilo adecuado de la letra en mayúsculas. Por ejemplo: **Número de pedido del usuario** en lugar de **Número de pedido del usuario.**

Esto es realmente una cuestión de preferencia, pero lo que hay que recordar es ser coherente con lo que elijas.

### Coherencia de entidades {#entity}

Es probable que ya tenga una nomenclatura en su empresa. Mantenga las métricas y dimensiones que haya implementado en consonancia con el uso que se hace en otras bases de datos y herramientas. Por ejemplo:

* Usuario vs. Cliente vs. Miembro vs. Cuenta
* Empresa frente a cuenta frente a organización
* Registro frente a creación

### Ortografía y gramática {#spelling}

¡Asegúrate de revisar tu ortografía y no te olvides de esos pesados posesivos!

## Gráficos {#charts}

Al dar nombre [gráficos](../tutorials/using-visual-report-builder.md), nos parece más útil seguir esta fórmula: **(Perspectiva de datos) + (Métrica) + (Periodo de tiempo) + (Intervalo de tiempo)**

**Ejemplo incorrecto:**
Ingresos

Esto no nos dice nada acerca del informe, lo que es malo.

**Ejemplo correcto:**
Ingresos acumulados de 30 días a mes

Esto nos dice **Exactamente** lo que figura en el informe, que es fantástico.

## Tableros {#dashboards}

Los tableros deben nombrarse de manera que representen temáticamente los informes que contienen. Por ejemplo, si el tablero contiene solo información relacionada con los ingresos y los pedidos, considere asignarle un nombre similar a **Nombre del almacén: ingresos y pedidos.**

Por el contrario, si el tablero es un lugar en el que está experimentando con diferentes informes, considere ponerle nombre **Sandbox de su nombre** por lo tanto, sabe que los informes contenidos en son borradores.

## Dimension (columnas calculadas) {#dimensions}

Al dar nombre a las nuevas [dimensiones](../data-analyst/data-warehouse-mgr/creating-calculated-columns.md), nos parece más útil seguir esta fórmula: **(Entidad) + (Nth) + (lapso de tiempo) + (cálculo) + (comentarios)**. Por ejemplo:

Primeros ingresos de 30 días del usuario
* Número de pedido del usuario
* Número de pedido del usuario (pendiente de auditoría)

## Conjuntos de filtros {#filterset}

[Conjuntos de filtros](../data-user/reports/ess-manage-data-filters.md) normalmente se denominan de manera que expliquen la información que incluyen o excluyen. Por ejemplo, dar nombre a un conjunto de filtros **Ordenar artículos que contamos** permitirá a cualquier usuario entrar, ver la lógica del conjunto de filtros y comprender qué información de pedidos determina qué se cuenta en la empresa. Recuerde que los conjuntos de filtros se pueden aplicar tanto a columnas calculadas como a métricas, y deben ser fáciles de entender.

## Métricas {#metrics}

[Métricas](../data-user/reports/ess-manage-data-metrics.md) son esencialmente preguntas a las que desea respuestas con regularidad. ¿Cuál fue el número de pedidos en el último mes? ¿Cuál es el valor promedio de duración de nuestros clientes? Por lo general, se recomienda nombrar métricas para reflejar la respuesta que dan a los usuarios. Además, si tiene la misma métrica filtrada para un almacén o departamento específico, debe etiquetarla como tal. Por ejemplo:

Media de LTV de clientes (primeros 30 días) Nombre de la tienda: Ingresos

Por último, a veces la misma métrica se puede organizar mediante distintas marcas de tiempo, en función de cómo las calculen los usuarios individuales. Si este es el caso, asegúrese de incluir la marca de tiempo en el nombre:

Ingresos (enviados\_at) Ingresos (creados\_at)

## Ajuste {#wrapup}

El establecimiento temprano de convenciones de estilo y nomenclatura le ayudará a configurar su [!DNL MBI] cuenta. Recuerde los tres C: claridad, coherencia y credibilidad.
