---
title: Informe de tiempo promedio hasta la primera compra
description: Aprenda a utilizar el informe Promedio de tiempo para la primera compra.
exl-id: c18734ce-0ae0-4e84-b9d0-eb2c21a5c3a5
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 330832e2668024b00edb2b7c49b92bb042bd004a
workflow-type: tm+mt
source-wordcount: '258'
ht-degree: 0%

---

# Informe de tiempo promedio hasta la primera compra

Muchos clientes de Adobe tienen una métrica y un gráfico con el nombre `Average time to first purchase`, que muestra el tiempo promedio entre la fecha de registro de un grupo de usuarios y la fecha de la primera compra. Los datos casi invariablemente se inclinan hacia abajo a medida que el tiempo se acerca al presente.

![tiempo promedio para el primer pedido](../../assets/average-time-to-first-order.png)

Esto se debe a que estos clientes más nuevos aún no han tenido la oportunidad de generar ninguna compra que se haya realizado más de un mes desde la fecha de su unión. Dado que los usuarios que nunca han realizado una compra no se incluyen en absoluto (hasta que realizan una compra), esto sesga la media a la baja para los grupos de clientes más nuevos.

Hay otras formas potenciales de ver esta métrica que introducen menos sesgo. Explore un ejemplo.

## Ejemplo: Realizar un análisis `cohort` de los primeros pedidos

Es posible que tenga un gráfico en el tablero `Users` llamado `Time to first order cohort`. Este informe usa la métrica `Distinct buyers`, agrupa a los usuarios por `cohort` semanas o meses de registro y muestra la proporción (entre `0` y `1`) de usuarios que realizaron una primera compra en las semanas o meses siguientes después del registro.

El gráfico puede mostrar que para los usuarios que se registraron en diciembre de 2014, `0.56` (o `56%`) realizó un primer pedido en el mes 2 (por ejemplo, enero de 2015).

Este análisis de cohorte es un buen indicador de la tasa de activación del usuario a lo largo del tiempo. Si este gráfico empieza a aplanarse o a estabilizarse y aún no estás cerca del 100 % de conversión a compradores, puede que sea el momento de activar los usuarios restantes a través de campañas de correo electrónico.
