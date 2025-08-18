---
title: Creación de un análisis de cohorte cualitativo
description: Descubra qué es una cohorte cualitativa, por qué podría estar interesado en crear este análisis y cómo puede crearlo en Commerce Intelligence.
exl-id: 113244e4-409b-4129-b3d4-7a3433539ade
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '834'
ht-degree: 0%

---

# Crear un(a) `Qualitative Cohort Analysis`

¿Sabe cómo los segmentos de clientes adquiridos por [!DNL Google Adwords] aumentan su LTV en comparación con los clientes adquiridos mediante la búsqueda orgánica? ¿Alguna vez ha pensado en realizar un análisis de `cohort` en diferentes segmentos de clientes uno al lado del otro en el mismo informe? Si es así, `qualitative cohort analysis` le ayudará a responder esas preguntas.

En este tema se explica en detalle qué es una cohorte cualitativa, por qué podría interesarle generar este análisis y cómo puede crearlo en [!DNL Commerce Intelligence].

## ¿Cuáles son `qualitative cohorts`, de todos modos? {#whatare}

El análisis de `Cohort` en general se puede definir, en términos generales, como el análisis de grupos de usuarios que comparten características similares a lo largo de sus ciclos de vida. Permite identificar tendencias de comportamiento entre diferentes grupos de usuarios.

Consulte [análisis de cohorte](https://www.cohortanalysis.com/).

La mayoría de los análisis `cohort` de [!DNL Commerce Intelligence] agrupan a los usuarios según una fecha común (por ejemplo, el conjunto de todos los clientes que realizaron su primera compra en un mes determinado). Un `qualitative cohort` es un poco diferente: es un grupo de usuarios definido por una característica que no está basada en el tiempo. Algunos ejemplos son:

* El conjunto de todos los usuarios adquiridos durante una campaña publicitaria
* El conjunto de todos los usuarios cuya primera compra incluyó un cupón (o no)
* El conjunto de todos los usuarios de una determinada edad

## ¿En qué se diferencia eso del generador normal de `cohort`? {#different}

[`Cohort Analysis Builder`](../dev-reports/cohort-rpt-bldr.md) está optimizado para agrupar cohortes mediante una característica basada en el tiempo. Esto es ideal para análisis que se centran en un segmento específico de usuario (por ejemplo, todos los usuarios que fueron adquiridos a través de una campaña de búsqueda de pago). En `Cohort Analysis Builder`, puede (1) centrarse en ese grupo de usuarios específico y (2) `cohort` en una fecha (como su primera fecha de pedido).

Sin embargo, si desea analizar el comportamiento de la cohorte de varios segmentos de usuarios en el mismo informe de cohorte (`paid` búsqueda versus `organic` búsqueda vs. tráfico directo, quizás?), este análisis más avanzado se puede construir en `Report Builder`.

## ¿Qué información debo enviar al servicio de asistencia para configurar mi análisis? {#support}

Crear un informe `qualitative cohort` en `Report Builder` implica que el equipo de analistas de Adobe cree [columnas calculadas avanzadas](../data-warehouse-mgr/creating-calculated-columns.md) en las tablas necesarias.

Para compilarlos, envíe un [ticket de asistencia](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) (y mencione este artículo). Esto es lo que debe saber:

* `metric` con el que desea realizar el análisis de cohorte y qué tabla utiliza (ejemplo: `Revenue`, creado en la tabla `orders`).

* El `user segments` que desea definir y dónde se encuentra esa información en la base de datos (ejemplo: valores diferentes de `User's referral source`, nativos de la tabla `users` y reubicados hacia abajo en `orders`).

* El `cohort date` que desea que use su análisis (ejemplo: la marca de tiempo `User's first order date`). Este ejemplo nos permitiría ver cada segmento y preguntar `How does a user's revenue grow in the months following their first order date?`.

* `time interval` sobre el que desea ver el análisis (ejemplo: `weeks`, `months` o `quarters` después de `User's first order date`).

Una vez que el equipo de analistas de Adobe responda a lo anterior, tendrá un par de nuevas columnas calculadas avanzadas para crear el informe. A continuación, puede seguir las instrucciones que se indican a continuación para hacerlo.

## Creación del análisis de cohorte cualitativo {#create}

En primer lugar, desea agregar la métrica que le interesa codificar, una vez por cada `cohort` que esté analizando. En este ejemplo, desea ver los `Revenue` acumulativos realizados en los meses posteriores al primer pedido de un cliente, segmentados por el `User's referral source`. Esto significa que, para cada segmento, agrega una métrica `Revenue` y un filtro para el segmento específico:

![](../../assets/qualcohort1.gif)

En segundo lugar, debe realizar dos cambios en las opciones de tiempo del informe:

1. Establezca `time interval` en `None`. Esto se debe a que finalmente se agrupa por intervalo de tiempo como una dimensión en lugar de utilizar las opciones de tiempo habituales.

1. Establezca `time range` en el intervalo de tiempo que desea que cubra el informe.

En este ejemplo, observa una vista `all time` de `Revenue`. Después de esto, debería terminar con una serie de puntos:

![](../../assets/qualcohort2.gif)

En tercer lugar, debe ajustar para configurar `cohorts`. En función de `cohort date` y `time interval` que especificó para el equipo de analistas de Adobe, tiene una dimensión en su cuenta que realiza las citas de `cohort`. En este ejemplo, esa dimensión personalizada se llama `Months between this order and customer's first order date`. Con esta dimensión, debería:

* `Group by` la dimensión con la opción `group by`

* Seleccione todos los valores de `dimension` que le interesen

* Con `Show top/bottom option`, seleccione los X meses principales que le interesan y ordene por la dimensión `Months between this order and customer's first order date`

Ahora puede ver una línea por cada `cohort` que haya especificado. Vea el ejemplo ahora: vea los `Revenue` que han contribuido los usuarios de cada origen de referencia, `grouped by` el número de meses entre su primer pedido y cualquier pedido posterior. En el ejemplo también se agregó `Cumulative perspective` para ver el crecimiento agregado de `cohorts'`. Observe la tabla de resultados para ver más granularidad.

¿Qué nos dice esto? En este caso, el origen de referencia específico `Paid search` es valioso en el primer mes de la vida útil de compra de un cliente, pero no puede retener su base de clientes con ingresos repetidos. Mientras que `Direct Traffic` comienza con una cantidad menor, los ingresos en los meses siguientes se acumulan a un ritmo similar.

No importa cómo lo fragmente, el análisis `cohort` es una herramienta poderosa en su caja de herramientas de análisis. Este tipo de análisis puede arrojar algunas perspectivas interesantes acerca de su negocio que `time-based cohorts` tradicional podría no tener, lo que le permite tomar mejores decisiones basadas en datos.
