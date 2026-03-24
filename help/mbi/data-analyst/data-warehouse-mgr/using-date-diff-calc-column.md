---
title: Uso de la columna calculada Diferencia de fechas
description: Conozca el propósito y los usos de la columna calculada Diferencia de fechas.
exl-id: 6ecab794-3466-4b3a-a929-3e56287522aa
role: Admin, Developer, User
feature: Data Import/Export, Data Integration, Data Warehouse Manager, Commerce Tables
TQID: https://experienceleague.adobe.com/5SElfBoU6vqCNthFdj96eCNH26dC54ucjqknnhQXQy8
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8id: c1256247-af4b-46d8-9dca-0c654ecfa157id: dac87252-6066-4d6e-a9d2-f6d84c323de7
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 272
ht-degree: 0%

---

# Columna calculada de diferencia de fecha

Este tema describe el propósito y los usos de la columna calculada `Date Difference` disponible en la página **[!DNL Manage Data > Data Warehouse]**. A continuación se explica lo que hace, seguido de un ejemplo, y la mecánica de crearlo.

**Explicación**

El tipo de columna `Date Difference` calcula el tiempo entre dos eventos que pertenecen a un único registro, basándose en las marcas de tiempo del evento. El valor sin procesar calculado en esta columna se expresa en segundos, pero se convierte automáticamente a minutos, horas, días, etc., para que se muestre en los informes. Sin embargo, cuando se utiliza como filtro/grupo por, desea utilizar el valor en segundos.

Se puede usar una columna calculada `date difference` para crear una métrica que calcule el promedio o la mediana de tiempo entre dos eventos, como el tiempo promedio entre el registro de clientes y sus primeros pedidos.

**Ejemplo**

| **`id`** | **`timestamp_1`** | **`timestamp_2`** | **`Seconds between timestamp_2 and timestamp_1`** |
|--- |--- |--- |--- |
| `A` | 00:00:00 del 01-01-2015 | 01-01-2015 12:30:00 | 45000 |
| `B` | 08:00:00 de enero de 2015 | 01-01-2015 10:00:00 | 7200 |

{style="table-layout:auto"}


En el ejemplo anterior, la columna `Date Difference` es la columna `Seconds between timestamp_2 and timestamp_1`. Realiza el cálculo `timestamp_2 minus timestamp_1`.

**Mecánica**

Los pasos siguientes describen cómo crear una columna `Date Difference`.

1. Vaya a la página **[!DNL Manage Data > Data Warehouse]**.
1. Desplácese hasta la tabla en la que desee crear esta columna.
1. Haga clic en **[!UICONTROL Create a Column]** y configure la columna de la siguiente manera:
   * Seleccionar `Column Definition Type` > `Same Table`
   * Seleccionar `Column Definition Equation` > `DATE_DIFF = (Ending DATETIME - Starting DATETIME)`
   * Seleccione la columna `Ending DATETIME` > Elija el campo de fecha y hora de finalización, que suele ser el evento que se produce más adelante
   * Seleccione la columna `Starting DATETIME`** > Elija el campo de fecha y hora de inicio, que suele ser el evento que se produce antes

1. Proporcione un nombre a la columna y haga clic en **[!UICONTROL Save]**.
1. La columna está disponible para usar *inmediatamente*.

A modo de ejemplo, el siguiente ejemplo está configurado para calcular `Seconds between order date and customer's creation date`:

![Configuración de cálculo de diferencia de fecha que muestra selecciones de columna datetime](../../assets/date_diff.png)
