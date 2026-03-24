---
title: Informe de tiempo promedio hasta la primera compra
description: Aprenda a utilizar el informe Promedio de tiempo para la primera compra.
exl-id: c18734ce-0ae0-4e84-b9d0-eb2c21a5c3a5
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
TQID: https://experienceleague.adobe.com/LWbb4E4IMPQd-hUpsylSGt4lgrrvYI1VUhmovjvcfu4
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 258
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
