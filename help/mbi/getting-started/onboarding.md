---
title: Incorporación de Adobe Commerce Intelligence
description: Obtenga información acerca de la incorporación de Adobe Commerce Intelligence.
exl-id: e0cce957-af2c-4514-9afd-c9aaa651a4f0
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
TQID: https://experienceleague.adobe.com/36wmj-7QyDdemBWFwHTf1NJkd4H06tED9FZPqhFz8eg
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: b5f00040-57a0-4a6d-a39e-383b1936c2c9id: f42e0a1a-0d79-488d-a83f-f2c30672b137
subfeature_v2: id: bcbf87e7-9b75-4596-bffe-0f376b4c73a7
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: aa2f3246-cb95-4b30-8899-fdf7d73550ccid: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 194
ht-degree: 0%

---

# Incorporando [!DNL Adobe Commerce Intelligence]

Las preguntas de incorporación relacionadas con la configuración de `store` y `database` garantizan que los informes se hayan configurado correctamente. Con estas respuestas, Adobe entrega informes que se ajustan con precisión a la configuración de su tienda.

## Configuración de tienda

- *¿Acepta tu tienda el pago y envío de invitados?* - Selecciona **sí** si permites que los clientes hagan una compra en tu tienda sin registrarse para una cuenta.

- `Timezone`: seleccione el `timezone` en el que desea ver los informes.

- `Currency` - Seleccione el `currency` en el que opera su tienda.

- `Your week starts on...`: seleccione en sus informes el día de la semana en el que desea que comience la semana.

- *¿Qué versión de Commerce utiliza?* - Seleccione el `currency` en el que opera su tienda.

- *¿Su tienda se encuentra en la Unión Europea?*: si responde `Yes` a esta pregunta, Adobe alojará su Data Warehouse y todos sus datos en la Unión Europea, de conformidad con el RGPD.

## Configuración de base de datos

- `Database name` - ¿Cuál es el *nombre de la base de datos [!DNL MySQL]* en la que residen los datos transaccionales de Commerce?

- `Table prefix (optional)` - ¿Las tablas contenidas en su base de datos de Commerce van precedidas de algo (por ejemplo, `store_`)? Normalmente no es así, pero se puede llevar a cabo una personalización.
