---
title: Crear un análisis de cohorte cualitativo
description: Descubra qué es una cohorte cualitativa, por qué podría interesarle crear este análisis y cómo puede crearlo en [!DNL MBI].
exl-id: 113244e4-409b-4129-b3d4-7a3433539ade
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '848'
ht-degree: 0%

---

# Cree un `Qualitative Cohort Analysis`

¿Sabe cómo es su [!DNL Adwords]- los segmentos de clientes adquiridos aumentan su LTV comparado con aquellos clientes adquiridos a partir de la búsqueda orgánica? ¿Alguna vez ha pensado en realizar un `cohort` análisis en distintos segmentos de clientes en paralelo en el mismo informe? En caso afirmativo, `qualitative cohort analysis` le ayudará a responder a esas preguntas.

En este artículo analizamos qué es una cohorte cualitativa, por qué podría interesarle crear este análisis y cómo puede crearlo en [!DNL MBI].

## ¿Qué son los `qualitative cohorts`, de todos modos? {#whatare}

`Cohort` en general, el análisis puede definirse en términos generales como el análisis de grupos de usuarios que comparten características similares a lo largo de sus ciclos de vida. Permite identificar tendencias de comportamiento en diferentes grupos de usuarios.

Consulte [análisis de cohorte](https://www.cohortanalysis.com/) - ¡Escribimos el sitio en él!

Más `cohort` analiza en [!DNL MBI] agrupar usuarios por una fecha común (por ejemplo, el conjunto de todos los clientes que realizaron su primera compra en un mes determinado). A `qualitative cohort` es un poco diferente: es un grupo de usuarios definido por una característica que no está basada en el tiempo. Algunos ejemplos son:

* Conjunto de todos los usuarios adquiridos desde una campaña de publicidad
* El conjunto de todos los usuarios cuya primera compra incluyó un cupón (o no)
* Conjunto de todos los usuarios que tienen una edad determinada

## ¿En qué se diferencia eso de lo normal? `cohort` generador? {#different}

La variable [`Cohort Analysis Builder`](../dev-reports/cohort-rpt-bldr.md) está optimizado para agrupar cohortes utilizando una característica basada en el tiempo. Esto es bueno para análisis centrados en un segmento específico de usuarios (por ejemplo, todos los usuarios que fueron adquiridos a través de una campaña de búsqueda de pago). En el `Cohort Analysis Builder`, puede (1) centrarse en ese grupo de usuarios específico y (2) `cohort` en una fecha (como su primera fecha de pedido).

Sin embargo, si desea analizar el comportamiento de cohorte de varios segmentos de usuario en el mismo informe de cohorte (`paid` búsqueda versus `organic` búsqueda vs. tráfico directo, ¿quizás?), este análisis más avanzado se puede construir en la variable `Report Builder`.

## ¿Qué información debo enviar al servicio de asistencia para configurar mi análisis? {#support}

Creación de `qualitative cohort` en el informe `Report Builder` involucra a nuestro equipo de analistas creando algunos [columnas calculadas avanzadas](../data-warehouse-mgr/creating-calculated-columns.md) en las tablas necesarias.

Para crearlos, envíe un [ticket de asistencia](../../guide-overview.md) (y remítase a este artículo!). Esto es lo que necesitamos saber:

* La variable `metric` desea realizar el análisis de cohorte con y con qué tabla utiliza (ejemplo: `Revenue`, creado en el `orders` ).

* La variable `user segments` desea definir y dónde se encuentra esa información en la base de datos (ejemplo: diferentes valores de `User's referral source`, nativo del `users` y se ha trasladado a la `orders`).

* La variable `cohort date` desea que utilice el análisis (ejemplo: el `User's first order date` timestamp). Este ejemplo nos permitiría ver cada segmento y preguntar `How does a user's revenue grow in the months following their first order date?`.

* La variable `time interval` que desea ver el análisis (ejemplo: `weeks`, `months`o `quarters` después del `User's first order date`).

Una vez que nuestro equipo de analistas responda a lo anterior, tendrá un par de nuevas columnas calculadas avanzadas para crear su informe. Luego podrá seguir las indicaciones siguientes para hacerlo.

## Creación del análisis de cohorte cualitativo {#create}

En primer lugar, desea añadir la métrica que le interese en la cohorte, una vez para cada `cohort` está analizando. En este ejemplo, queremos ver el valor acumulado `Revenue` se realiza en los meses posteriores al primer pedido de un cliente, segmentado por la variable `User's referral source`. Esto significa que, para cada segmento, agregaremos uno `Revenue` métrica y filtro para el segmento específico:

![](../../assets/qualcohort1.gif)

En segundo lugar, debe realizar dos cambios en las opciones de tiempo del informe:

1. Configure las variables `time interval` a `None`. Esto se debe a que, finalmente, agrupamos por intervalo de tiempo como dimensión en lugar de usar las opciones de tiempo habituales.

1. Configure las variables `time range` a la ventana de tiempo que desea que abarque el informe.

En nuestro ejemplo, miramos un `all time` vista de `Revenue`. Después de esto, debería terminar con una serie de puntos:

![](../../assets/qualcohort2.gif)

En tercer lugar, se realizará un ajuste para configurar la variable `cohorts`. En función de la variable `cohort date` y `time interval` ha especificado para nuestro equipo de analistas, tendrá una dimensión en su cuenta que realizará el `cohort` citas. En este ejemplo, se llama a esa dimensión personalizada `Months between this order and customer's first order date`. Con esta dimensión, debe:

* `Group by` la dimensión con la variable `group by` option

* Seleccione todos los valores de la variable `dimension` en el que esté interesado

* Con la variable `Show top/bottom option`, seleccione los X meses principales en los que esté interesado y ordene por `Months between this order and customer's first order date` dimensión

Ahora, puede ver una línea para cada `cohort` que ha especificado. Consulte nuestro ejemplo ahora: vemos el `Revenue` aportados por los usuarios de cada fuente de referencia, `grouped by` número de meses entre el primer pedido y cualquier pedido posterior. También agregamos un `Cumulative perspective` para ver el `cohorts'` crecimiento agregado: eche un vistazo a la tabla de resultados para obtener más granularidad.

¿Qué nos dice esto? Aquí, la fuente de referencia específica `Paid search` es muy valioso en el primer mes de vida útil de compra de un cliente, pero no conserva su base de clientes con ingresos repetidos. While `Direct Traffic` comienza con una cantidad menor, los ingresos en los meses siguientes se acumulan realmente a un ritmo similar.

No importa cómo lo caigas, `cohort` analysis es una potente herramienta de su caja de herramientas de análisis. Este tipo de análisis puede arrojar algunas perspectivas muy interesantes sobre su negocio que `time-based cohorts` puede no ser así, lo que le permite tomar mejores decisiones basadas en datos.
