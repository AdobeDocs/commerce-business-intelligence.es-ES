---
title: 'Análisis de la probabilidad de repetición: declive y pérdida'
description: Conozca y comprenda cómo transcurre el tiempo entre los pedidos y cuándo se espera que se produzcan los clientes.
exl-id: ea26052d-ac74-43b7-a4a6-977800d4c719
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '959'
ht-degree: 0%

---

# Repetición de la probabilidad: Declive y pérdida

Si una parte de sus ingresos proviene de compras repetidas, probablemente sea consciente del enorme valor de una base de clientes leal. Con este fin, es fundamental comprender cómo transcurre el tiempo entre los pedidos y cuándo se espera que se produzcan los clientes.

En este tema se analizan los análisis que pueden ayudarle a responder a las siguientes preguntas:

* ¿Cuál es la probabilidad de que un cliente realice otra compra?
* ¿Cómo varía la probabilidad de que se repita el pedido con el tiempo desde la compra más reciente del cliente?
* ¿Cuándo se debe considerar que se produce un cliente? Por lo tanto, ¿cuándo debería iniciarse una campaña de reactivación?

## Métricas recomendadas

Cuando analice la disminución y la pérdida de la probabilidad de repetición, considere la posibilidad de utilizar ([o construcción](../../data-user/reports/ess-manage-data-metrics.md)) estas métricas:

### Probabilidad de pedido de repetición inicial

Esta medida se define como el número total de pedidos repetidos, como un porcentaje del total de pedidos. En otras palabras, es probable que una orden sea seguida por otra orden. Cuando esta probabilidad es superior al 50%, implica que más de la mitad de todos los pedidos van seguidos de un pedido posterior.

### Probabilidad de pedido de repetición a partir de meses desde el pedido

Esta medida demuestra la probabilidad de que un usuario vuelva a realizar un pedido teniendo en cuenta el número de meses que han transcurrido desde el último pedido. La fórmula utilizada para generar esta métrica simplifica:

![Fórmula de probabilidad de repetición](../../assets/Repeat_probability_formula.png)

Según el modelo empresarial, la probabilidad de que se repita el pedido puede disminuir inmediatamente después de que un cliente realice un pedido y seguir disminuyendo en los meses siguientes o puede mostrar variaciones de temporada y picos.

En cualquier caso, comprender qué porcentaje de sus clientes se espera que realicen compras repetidas y cómo estas tendencias a lo largo del tiempo le permiten dirigirse a sus clientes a intervalos críticos para maximizar la probabilidad de una compra repetida. Por lo tanto, cuando la probabilidad de compra repetida está disminuyendo, puede elegir un tiempo para identificar a un cliente como producido y cambiar sus esfuerzos de retención a reactivación.

## Ejemplo de hoy

Eche un vistazo al deterioro de la probabilidad de repetición para un negocio de comercio electrónico típico.

![Probabilidad de repetición inicial del pedido repetida probabilidad determinados meses desde el pedido.](../../assets/Order_probability_reports.png)

### Probabilidad de pedido de repetición inicial

En este ejemplo, la probabilidad de repetición inicial (o la probabilidad de que un pedido vaya seguido de otro pedido) es del 60 %. Esto significa que el 60% de todos los pedidos realizados con esta empresa son seguidos por un pedido posterior.

### Probabilidad de pedido de repetición a partir de meses desde el pedido

Este informe muestra la probabilidad de que un cliente vuelva a realizar un pedido dado que han transcurrido varios meses desde que se realizó el último pedido. Aunque no hay una definición única para el umbral de pérdida dado este informe, se recomienda definir la pérdida como el punto en el que la probabilidad de deterioro sobrepasa el valor que es la mitad de la tasa inicial de probabilidad de repetición.

Dado que la tasa de probabilidad de repetición inicial para este ejemplo es del 60 %, la fecha de reproducción sería la hora en la que la probabilidad de repetición de pedido cae por debajo del 60 %/2 = 30 % o a unos 6 meses. De un 60% de los pedidos que se van a seguir con otro pedido, la mitad se realizaron en los primeros 6 meses.

En otras palabras, si un cliente iba a realizar un pedido de seguimiento, es más probable que lo haya hecho en los 6 meses posteriores a su último pedido que después de la marca de los 6 meses. Si un cliente no ha vuelto a comprar después de 6 meses, se debe iniciar una campaña de reactivación para volver a atraer a este cliente.

Según el modelo empresarial, es posible que desee elegir un umbral diferente, como el punto en el que la probabilidad de repetición de pedidos cae por debajo del 50 % o el 10 %. Si sus conocimientos internos sugieren un número diferente, entonces, por todos los medios, debe usarlo!

En última instancia, el objetivo es seleccionar el umbral en el que tiene sentido pasar de la retención a los esfuerzos de reactivación. Los esfuerzos de retención pueden incluir correos electrónicos para volver a interactuar con clientes existentes con compras de seguimiento sugeridas que realizar, mientras que los esfuerzos de reactivación pueden incluir correos electrónicos a clientes caducados con cupones y ofertas.

## ¿Qué preguntas debo considerar?

Para ayudarle a comprender la probabilidad de que se repita un pedido a medida que se aplica a su negocio, le sugerimos que tenga en cuenta estas preguntas al explorar sus propios datos:

* ¿Se espera la probabilidad de repetición inicial del pedido? Si no es así, ¿por qué cree que debería ser mayor o menor?
* ¿Hay alguna gran disminución en la probabilidad de pedidos repetidos para meses específicos desde el último pedido? En caso afirmativo, ¿se esperan estos cambios?
* ¿Cuál es tu umbral de pérdida actual?
* ¿El umbral de pérdida actual se alinea con uno de los valores de la probabilidad de pedidos repetidos dados meses desde el informe de último pedido?
* ¿El umbral actual refleja los esfuerzos publicitarios que cambian de la retención a la reactivación?
* ¿Tiene sentido que su empresa cambie el umbral al mes en el que la disminución de probabilidad cruce el valor que es la mitad de la tasa inicial de probabilidad de repetición?

## ¿Qué más debo analizar?

Después de crear el análisis anterior y determinar un umbral de pérdida, puede generar más análisis para identificar tendencias comunes en los usuarios que se producen. Por ejemplo, ¿los clientes que han obtenido productos adquiridos durante el mismo período de tiempo o compraron productos similares en su último pedido? Una vez establecido un umbral de pérdida, puede profundizar en los rasgos específicos de estos clientes que se producen.

Si ofrece más de un producto, probablemente se pregunte cómo se comportan los clientes que compran un producto específico de forma diferente a lo largo del tiempo en comparación con otros clientes. ¿Quieres saber más? Consulte este tutorial para explorar el comportamiento de compra de las cohortes de clientes en función de los productos específicos que han comprado.

Esta práctica recomendada la proporciona [!DNL MBI] Servicios de análisis de datos (DAS). Esperamos poder responder a sus preguntas comerciales específicas. [Contacto con el servicio de asistencia](../../guide-overview.md) para obtener más información.

### Relacionado

* [Análisis del impacto de los cupones en la adquisición y retención de clientes](../analysis/coupon-impact.md)
* [Análisis del comportamiento de recompra de los clientes](../analysis/repurchase-behavior.md)
