---
title: Duración del análisis de cohorte de ingresos
description: Explorar el poder de [!DNL MBI] análisis de cohorte.
exl-id: f2b55745-d364-4ba6-9857-ce9cee05c3ae
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '952'
ht-degree: 0%

---

# `Lifetime Revenue Cohort` Análisis

Existen muchas formas diferentes de ver los datos en [!DNL MBI], y sabemos que la interpretación y el entendimiento son tan importantes como el cálculo y la visualización. Este artículo explorará el poder de [!DNL MBI] `cohort` análisis.

## Qué hace `lifetime revenue cohort` ¿significado de análisis?

El gráfico siguiente muestra el gasto acumulado por usuario durante un período de tiempo después de adquirirse. `Cohorts` de usuarios se dividen por su mes de adquisición.

Por ejemplo, la línea naranja anterior muestra el promedio para los usuarios adquiridos en noviembre de 2011. El primer punto de datos significa que, en su primer mes, los usuarios adquiridos en noviembre gastaron un promedio de aproximadamente `$200`. El segundo punto de datos significa que para finales de su segundo mes, estos usuarios habían gastado un promedio de aproximadamente `$240`. Su gasto promedio en el mes dos fue aproximadamente `$40 (240 - 200)`. Las diferentes líneas representan diferentes cohortes de usuarios. La línea verde representa a los usuarios que se adquirieron en diciembre y la azul a los usuarios que se adquirieron en octubre.

## ¿Por qué es importante?

Este tipo de `cohort` el análisis puede resultar útil para diferentes propósitos, pero el beneficio más inmediato suele ser tomar mejores decisiones de adquisición de clientes. Muchas empresas limitan su gasto en marketing a canales que generan rentabilidad en la primera compra de un cliente. Estas empresas pagarán por adquirir clientes a través de un canal determinado siempre y cuando su primera compra promedio genere más `gross margin` de lo que cuesta adquirirlas.

El problema con este enfoque es que a menudo resulta en una inversión insuficiente en crecimiento. Si sus competidores se basan en una comprensión más profunda del comportamiento de compra, crecerán más que usted. La variable `lifetime revenue cohort` analysis le ayuda a comprender las consecuencias de ampliar el gasto en adquisición de clientes y le ofrece una forma sencilla de transmitirlo al resto de su equipo. Si los clientes futuros se comportan como los clientes existentes, la adquisición de clientes para una CPA más alta resultará en un periodo de recuperación predecible. Dependiendo de la posición de efectivo de la empresa, puede definir con qué periodo de devolución se siente cómodo, encontrar el punto relevante en la tabla y gastar en consecuencia.

Además, puede utilizar este análisis para ver si está mejorando la incorporación, la participación y la generación de ingresos de los usuarios que adquiere.  Por ejemplo, esto `cohort` análisis es una buena manera de ver si una promoción de envío gratuita para nuevos usuarios tuvo como resultado compradores repetidos o compradores únicos que nunca regresaron.

## ¿Cómo variará esto para los diferentes modelos de negocio?

Para la mayoría de las empresas, la variable `lifetime revenue cohort` el gráfico de análisis mostrará una gran cantidad de gasto en el período inicial y luego aumentará más lentamente con el tiempo. Ese pico inicial se debe a que los clientes tienen más probabilidades de realizar su primera compra poco después de haberlas adquirido que en cualquier otro momento. En los casos en los que el evento de adquisición en sí es una compra, el 100 % de los clientes realiza una compra en su primer periodo. En los casos en que el registro puede ocurrir antes de las compras, este efecto es menos drástico.

Como ejemplo, [!DNL Groupon] probablemente tendría un salto inicial mucho menor que [!DNL Amazon], porque muchas de las personas que se inscriben en [!DNL Groupon] no realice una compra de inmediato. A menos que haya un número elevado de reembolsos, este gráfico se inclinará hacia arriba y hacia la derecha después del salto inicial. La tasa de crecimiento tiende a disminuir con el tiempo porque los clientes suelen ser más activos cuando se registran por primera vez. Esto hace que el promedio caiga porque el número de personas en la cohorte se mantiene constante independientemente de cuántas regresen a comprar más. En las empresas de suscripción, la pendiente se deteriorará menos agresivamente que en las empresas donde la gente realiza compras únicas.

Ocasionalmente, un negocio de suscripción tendrá una pendiente que aumenta con el tiempo. Es raro verlo, pero es una señal buena para el negocio cuando ocurre. Esto no significa que no haya ningún cliente que produzca nada, sino que las actualizaciones para los clientes que se quedan más que para los clientes que se van.

## ¿Cómo se calcula esto?

Hay dos entradas simples para este cálculo: cuántos miembros hay en el `cohort` (que nunca cambia), y cuántos ingresos generaron esos miembros en el periodo en cuestión. Para determinar los miembros en la variable `cohort`, contamos el número de usuarios adquiridos en el periodo en cuestión. Una adquisición puede ser una primera compra, la creación de cuentas, el registro en un boletín informativo o cualquier otro evento. La variable `revenue` el cálculo es un poco más complicado. Queremos sumar los ingresos para los pedidos que realizaron los miembros de esta `cohort` y se produjeron en un período de tiempo fijo desde la fecha de adquisición (por ejemplo, los tres primeros meses). Por último, dividimos los ingresos por el número de miembros de la `cohort` para cada periodo de tiempo en el gráfico y añada este valor de forma acumulativa a lo largo del tiempo.

## ¿Cuáles son las variaciones de este gráfico?

Hay muchas clases diferentes de útiles `cohort` análisis.  La variación más común es [filtrado por fuente de adquisición de usuario](../analysis/most-value-source-channel.md). Por ejemplo, es posible que desee consultar este gráfico para los clientes de `organic` buscar, `paid` o un programa afiliado. Esto le ayudará a comprender si los clientes de una fuente de adquisición son más leales o valiosos que otros. Por supuesto, también puede filtrar por demografía u otros atributos de usuario.

Otra manera de ver los datos es con una perspectiva de datos incremental, en lugar de acumulativa.  Esto muestra la cantidad incremental que un usuario promedio gasta en cada mes después de ser adquirido.  Esto resulta útil para predecir la cantidad de compras repetidas que obtendrá de los usuarios existentes. Podemos ver esto con otras cosas además de los ingresos también. Algunos ejemplos incluyen métricas de margen y no financieras, como invitaciones, votos o mensajes.
