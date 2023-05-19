---
title: Incorporación de Adobe Commerce Intelligence
description: Obtenga información acerca de la incorporación de Adobe Commerce Intelligence.
exl-id: e0cce957-af2c-4514-9afd-c9aaa651a4f0
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '194'
ht-degree: 0%

---

# Incorporación [!DNL Adobe Commerce Intelligence]

Las preguntas de incorporación relacionadas con `store` y `database` La configuración de garantiza que los informes se configuran correctamente. Con estas respuestas, Adobe entrega informes que se adaptan con precisión a la configuración de su tienda.

## Configuración de tienda

- *¿Acepta tu tienda el pago y envío de invitados?* - Seleccionar **yes** si permite a los clientes realizar una compra en su tienda sin registrarse para obtener una cuenta.

- `Timezone` - Seleccione el `timezone` que le gustaría ver sus informes en.

- `Currency` - Seleccione el `currency` en el que opera su tienda.

- `Your week starts on...` : seleccione en los informes el día de la semana que desea que sea el inicio de la semana.

- *¿Qué versión de Commerce utiliza?* - Seleccione el `currency` en el que opera su tienda.

- *¿Tiene su tienda su sede en la Unión Europea?* - Si responde `Yes` Ante esta pregunta, Adobe alojará su Data Warehouse y todos sus datos en la Unión Europea, de conformidad con el RGPD.

## Configuración de base de datos

- `Database name` - ¿Qué es el *nombre del [!DNL MySQL] database* ¿dónde residen los datos transaccionales de Commerce?

- `Table prefix (optional)` - ¿Las tablas contenidas en su base de datos de Commerce van precedidas de algo (por ejemplo, `store_`)? Normalmente no es así, pero se puede llevar a cabo una personalización.
