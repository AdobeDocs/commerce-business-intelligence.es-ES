---
title: Creación de un análisis de cohorte cualitativo
description: Descubra qué es una cohorte cualitativa, por qué podría estar interesado en crear este análisis y cómo puede crearlo en [!DNL MBI].
exl-id: 113244e4-409b-4129-b3d4-7a3433539ade
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '841'
ht-degree: 0%

---

# Crear un `Qualitative Cohort Analysis`

¿Sabe cómo es su [!DNL Adwords]Los segmentos de clientes no adquiridos aumentan su LTV en comparación con los clientes adquiridos mediante búsqueda orgánica. ¿Ha pensado alguna vez en realizar una `cohort` análisis en diferentes segmentos de clientes en paralelo en el mismo informe? En caso afirmativo, `qualitative cohort analysis` le ayuda a responder a esas preguntas.

Este artículo explora qué es una cohorte cualitativa, por qué podría interesarle crear este análisis y cómo puede crearlo en [!DNL MBI].

## Qué son `qualitative cohorts`¿De todos modos? {#whatare}

`Cohort` el análisis en general puede definirse en términos generales como el análisis de grupos de usuarios que comparten características similares a lo largo de sus ciclos de vida. Permite identificar tendencias de comportamiento entre diferentes grupos de usuarios.

Consulte [análisis de cohorte](https://www.cohortanalysis.com/).

Más `cohort` análisis en [!DNL MBI] agrupar usuarios por una fecha común (por ejemplo, el conjunto de todos los clientes que realizaron su primera compra en un mes determinado). A `qualitative cohort` es un poco diferente: es un grupo de usuarios definido por una característica que no está basada en el tiempo. Algunos ejemplos son:

* El conjunto de todos los usuarios adquiridos durante una campaña publicitaria
* El conjunto de todos los usuarios cuya primera compra incluyó un cupón (o no)
* El conjunto de todos los usuarios de una determinada edad

## ¿En qué se diferencia de lo normal? `cohort` ¿constructor? {#different}

El [`Cohort Analysis Builder`](../dev-reports/cohort-rpt-bldr.md) está optimizado para agrupar cohortes mediante una característica basada en el tiempo. Esto es bueno para los análisis centrados en un segmento específico de usuario (por ejemplo, todos los usuarios que fueron adquiridos a través de una campaña de búsqueda de pago). En el `Cohort Analysis Builder`, puede (1) centrarse en ese grupo de usuarios específico y (2) `cohort` en una fecha (como su primera fecha de pedido).

Sin embargo, si desea analizar el comportamiento de cohorte de varios segmentos de usuario en el mismo informe de cohorte (`paid` búsqueda frente a `organic` búsqueda frente al tráfico directo, quizás?), este análisis más avanzado se puede construir en la `Report Builder`.

## ¿Qué información debo enviar al servicio de asistencia para configurar mi análisis? {#support}

Creación de un `qualitative cohort` informe en el `Report Builder` implica que el equipo de analistas de Adobe cree algunos [columnas calculadas avanzadas](../data-warehouse-mgr/creating-calculated-columns.md) en las mesas necesarias.

Para compilarlos, envíe un [ticket de asistencia](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=en) (y haga referencia a este artículo). Esto es lo que debe saber:

* El `metric` desea realizar el análisis de cohorte con y qué tabla utiliza (por ejemplo: `Revenue`, creado en el `orders` tabla).

* El `user segments` desea definir y dónde se almacena esa información en la base de datos (por ejemplo: valores diferentes de `User's referral source`, nativo de `users` y se reubican hacia abajo en la `orders`).

* El `cohort date` desea que utilice su análisis (por ejemplo: la variable `User's first order date` timestamp). Este ejemplo nos permite ver cada segmento y preguntar `How does a user's revenue grow in the months following their first order date?`.

* El `time interval` sobre el que desea ver el análisis (ejemplo: `weeks`, `months`, o `quarters` después de `User's first order date`).

Una vez que el equipo del analista de Adobes responda a lo anterior, tendrá un par de nuevas columnas calculadas avanzadas para crear el informe. A continuación, puede seguir las instrucciones que se indican a continuación para hacerlo.

## Creación del análisis de cohorte cualitativo {#create}

En primer lugar, desea agregar la métrica que le interesa codificar, una vez para cada `cohort` está analizando. En este ejemplo, desea ver los datos acumulativos `Revenue` realizados en los meses posteriores al primer pedido de un cliente, segmentados por la variable `User's referral source`. Esto significa que, para cada segmento, agrega uno `Revenue` métrica y filtro para el segmento específico:

![](../../assets/qualcohort1.gif)

En segundo lugar, debe realizar dos cambios en las opciones de tiempo del informe:

1. Configure las variables `time interval` hasta `None`. Esto se debe a que finalmente se agrupa por intervalo de tiempo como una dimensión en lugar de utilizar las opciones de tiempo habituales.

1. Configure las variables `time range` a la ventana de tiempo que desea que cubra el informe.

En este ejemplo, se ve un `all time` vista de `Revenue`. Después de esto, debería terminar con una serie de puntos:

![](../../assets/qualcohort2.gif)

En tercer lugar, debe ajustar para configurar la variable `cohorts`. Basado en el `cohort date` y `time interval` Si ha especificado al equipo de analista de Adobe, tiene una dimensión en la cuenta que realiza las `cohort` citas. En este ejemplo, esa dimensión personalizada se llama `Months between this order and customer's first order date`. Con esta dimensión, debería:

* `Group by` la dimensión con la variable `group by` opción

* Seleccione todos los valores de la variable `dimension` en el que esté interesado

* Con el `Show top/bottom option`, seleccione los X meses principales que le interesan y ordene por el `Months between this order and customer's first order date` dimensión

Ahora, puede ver una línea para cada uno `cohort` que ha especificado. Consulte el ejemplo ahora: puede ver el `Revenue` aportadas por los usuarios de cada fuente de referencia, `grouped by` el número de meses entre su primer pedido y cualquier pedido posterior. En el ejemplo también se ha añadido una `Cumulative perspective` para ver la `cohorts'` crecimiento agregado: consulte la tabla de resultados para obtener más granularidad.

¿Qué nos dice esto? Aquí, la fuente de referencia específica `Paid search` es útil en el primer mes de la vida útil de compra de un cliente, pero no logra retener su base de clientes con ingresos repetidos. While `Direct Traffic` comienza en una cantidad menor, los ingresos en los meses siguientes se acumulan realmente a un ritmo similar.

No importa cómo lo cortas, `cohort` analysis es una potente herramienta en su caja de herramientas de análisis. Este tipo de análisis puede arrojar algunas perspectivas interesantes sobre su negocio que tradicionales `time-based cohorts` puede que no, lo que le permite tomar mejores decisiones basadas en datos.
