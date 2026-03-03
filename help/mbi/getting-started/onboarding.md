---
title: Incorporación de Adobe Commerce Intelligence
description: Obtenga información acerca de la incorporación de Adobe Commerce Intelligence.
exl-id: e0cce957-af2c-4514-9afd-c9aaa651a4f0
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 5e80ff8f8ec76996b88a22b115be696b110581be
workflow-type: tm+mt
source-wordcount: '194'
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
