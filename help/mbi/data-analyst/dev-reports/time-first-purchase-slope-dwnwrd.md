---
title: Promedio de tiempo hasta el primer informe de compra
description: Aprenda a utilizar el informe Promedio de tiempo para la primera compra .
exl-id: c18734ce-0ae0-4e84-b9d0-eb2c21a5c3a5
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '256'
ht-degree: 0%

---

# Promedio de tiempo hasta el primer informe de compra

Muchos de nuestros clientes tienen una métrica y un gráfico llamados `Average time to first purchase`, que muestra el tiempo promedio entre la fecha de registro de un grupo de usuarios y la fecha de la primera compra. Los datos casi invariablemente disminuyen a medida que el tiempo se acerca más al presente.

![tiempo promedio para el primer pedido](../../assets/average-time-to-first-order.png)

Esto se debe a que estos clientes más nuevos aún no han tenido la oportunidad de generar compras que se hayan realizado más de un mes desde su fecha de afiliación. Dado que los usuarios que nunca han realizado una compra no están incluidos en absoluto (hasta que no hagan una compra), esto prejuzga el promedio a la baja para los grupos de clientes más nuevos.

Hay otras formas potenciales de ver esta métrica que introducen menos sesgo. Analicemos un ejemplo.

## Ejemplo: Realizar una `cohort` análisis de los primeros pedidos

Puede tener un gráfico en su `Users` panel denominado `Time to first order cohort`. Este informe utiliza la variable `Distinct buyers` métrica, agrupa usuarios por `cohort` semanas o meses de registro y muestra la proporción (entre `0` y `1`) de usuarios que realizaron una primera compra en las siguientes semanas o meses después del registro.

El gráfico puede mostrar que para los usuarios registrados en diciembre de 2014, `0.56` (o `56%`) realizó un primer pedido por mes 2 (por ejemplo, enero de 2015).

Este análisis de cohorte es un buen indicador de la tasa de activación del usuario a lo largo del tiempo. Si este gráfico empieza a aplanarse o a estabilizarse, y aún no se ha aproximado a la conversión del 100 % a compradores, puede que sea hora de activar los usuarios restantes mediante campañas de correo electrónico.
