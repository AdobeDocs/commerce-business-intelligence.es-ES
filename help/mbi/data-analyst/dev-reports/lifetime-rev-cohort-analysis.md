---
title: Análisis de cohorte de ingresos por duración
description: Explore el poder del análisis de cohorte de Commerce Intelligence.
exl-id: f2b55745-d364-4ba6-9857-ce9cee05c3ae
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '937'
ht-degree: 0%

---

# Análisis de [!DNL Lifetime Revenue Cohort]

Hay muchas maneras de ver los datos de [!DNL Adobe Commerce Intelligence] y sabe que la interpretación y la comprensión son tan importantes como el cálculo y la visualización. En este tema se explora la potencia del análisis [!DNL Commerce Intelligence] `cohort`.

## ¿Qué significa análisis `lifetime revenue cohort`?

El gráfico siguiente muestra el gasto acumulado por usuario durante un período de tiempo después de adquirirlos. `Cohorts` de usuarios se dividen por el mes de adquisición.

Por ejemplo, la línea naranja anterior muestra el promedio de los usuarios adquiridos en noviembre de 2011. El primer punto de datos significa que en su primer mes, los usuarios adquiridos en noviembre invirtieron un promedio de `$200`. El segundo punto de datos significa que al final de su segundo mes, estos usuarios habían gastado un promedio de aproximadamente `$240`. Su gasto promedio en el mes dos fue de aproximadamente `$40 (240 - 200)`. Las distintas líneas representan diferentes cohortes de usuarios. La línea verde representa los usuarios adquiridos en diciembre y la azul los usuarios adquiridos en octubre.

## ¿Por qué es esto importante?

Este tipo de análisis de `cohort` puede ser útil para varios propósitos diferentes, pero el beneficio más inmediato a menudo son mejores decisiones de adquisición de clientes. Muchas empresas limitan su gasto en marketing a canales que generan rentabilidad con la primera compra de un cliente. Estas empresas pagan para adquirir clientes a través de un canal determinado, siempre y cuando su primera compra promedio rinda más de `gross margin` de lo que cuesta adquirirlos.

El problema con este enfoque es que a menudo resulta en una inversión insuficiente en crecimiento. Si sus competidores realizan marketing basado en una comprensión más profunda del comportamiento de compra, le superarán. El análisis `lifetime revenue cohort` le ayuda a comprender las consecuencias de ampliar el gasto en adquisición de clientes y proporciona una forma sencilla de transmitirlo al resto de su equipo. Si los clientes futuros se comportan como los clientes existentes, la adquisición de clientes para una CPA más alta resulta en un periodo de recuperación predecible. Dependiendo de la posición de efectivo de la empresa, puede definir con qué periodo de amortización se siente cómodo, encontrar el lugar relevante en el gráfico y gastar en consecuencia.

Además, puede utilizar este análisis para ver si mejora la incorporación, la participación y la generación de ingresos de los usuarios que adquiere. Por ejemplo, este análisis de `cohort` es una buena manera de ver si una promoción de envío gratis para nuevos usuarios resultó en compradores repetidos o compradores únicos que nunca regresan.

## ¿Cómo variará esto para los diferentes modelos de negocio?

Para la mayoría de las empresas, el gráfico de análisis `lifetime revenue cohort` mostrará una gran cantidad de gasto en el período inicial y luego aumentará más lentamente con el tiempo. Ese pico inicial se debe a que es más probable que los clientes realicen su primera compra poco después de adquirirla que en cualquier otro momento. En los casos en los que el propio evento de adquisición es una compra, el 100% de los clientes realiza una compra en su primer periodo. En los casos en los que el registro puede ocurrir antes de las compras, este efecto es menos drástico.

Por ejemplo, es probable que [!DNL Groupon] tenga un salto inicial mucho menor que [!DNL Amazon], ya que muchas de las personas que se suscriben a [!DNL Groupon] no realizan una compra de inmediato. A menos que haya un número elevado de reembolsos, este gráfico se inclinará hacia arriba y hacia la derecha después del salto inicial. La tasa de crecimiento tiende a disminuir con el tiempo porque los clientes son más activos cuando se registran por primera vez. Esto hace que la media baje porque el número de personas en la cohorte permanece constante independientemente de cuántas regresen para comprar más. En los negocios de suscripción, la pendiente se deteriorará de manera menos agresiva que en los negocios donde la gente hace compras únicas.

En ocasiones, un negocio de suscripción tendrá en realidad una pendiente que aumenta con el tiempo. Es raro ver esto, pero es una gran señal para el negocio cuando sucede. Esto no significa que no haya ningún cliente que pierda, sino que las actualizaciones para clientes que se quedan más que compensan a los clientes que se van.

## ¿Cómo se calcula?

Hay dos entradas simples para este cálculo: cuántos miembros hay en `cohort` (que nunca cambia) y cuántos ingresos generaron esos miembros en el período determinado. Para determinar los miembros de `cohort`, se cuenta el número de usuarios que se adquirieron en el período en cuestión. Una adquisición puede ser una primera compra, la creación de una cuenta, la suscripción a un boletín informativo o cualquier otro evento. El cálculo `revenue` es un poco más complicado. Desea sumar los ingresos de los pedidos realizados por los miembros de este(a) `cohort` y que se produjeron en un período de tiempo fijo a partir de la fecha de adquisición (por ejemplo, los primeros tres meses). Por último, divida los ingresos por el número de miembros en `cohort` para cada período de tiempo en el gráfico y agregue este valor de forma acumulativa a lo largo del tiempo.

## ¿Cuáles son las variaciones de este gráfico?

Existen muchos tipos diferentes de análisis útiles de `cohort`. La variación más común es el [filtrado por el origen de adquisición del usuario](../analysis/most-value-source-channel.md). Por ejemplo, es posible que desee ver este gráfico para los clientes que vinieron de `organic`, la búsqueda `paid` o un programa de afiliados. Esto le ayuda a saber si los clientes de una fuente de adquisición son más leales o valiosos que otra. También puede filtrar por datos demográficos u otros atributos del usuario.

Otra forma de ver los datos es con una perspectiva de datos incremental, en lugar de acumulativa. Muestra la cantidad incremental que un usuario promedio gasta en cada mes después de ser adquirido. Esto resulta útil para prever la cantidad de compras repetidas que obtiene de los usuarios existentes. Puede ver esto con otras cosas además de los ingresos. Algunos ejemplos incluyen métricas de margen y no financieras como invitaciones, votos o mensajes.
