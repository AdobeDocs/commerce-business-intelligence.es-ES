---
title: Tipos de columnas calculadas avanzadas
description: Aprenda los conceptos básicos de la mayoría de los casos de columnas de uso, pero es posible que desee una columna calculada que sea un poco más compleja de lo que puede crear el Administrador de Datas Warehouse.
exl-id: 9871fa19-95b3-46e4-ae2d-bd7c524d12db
source-git-commit: c7f6bacd49487cd13c4347fe6dd46d6a10613942
workflow-type: tm+mt
source-wordcount: '898'
ht-degree: 4%

---

# Tipos de columnas calculadas avanzadas

Muchos de los análisis que puede interesarle crear implican el uso de una **nueva columna** que desea que `group by` o `filter by`. El [Creación de columnas calculadas](../data-warehouse-mgr/creating-calculated-columns.md) Este tutorial trata los conceptos básicos de la mayoría de los casos de uso, pero es posible que desee una columna calculada que sea un poco más compleja de lo que puede crear el Administrador de Datas Warehouse.
{: #top}

El equipo de Adobe de analistas de Datas Warehouse puede crear estos tipos de columnas. Para definir una nueva columna calculada, proporciónenos la siguiente información:

1. El **`definition`** de esta columna (incluidas entradas, fórmulas o formato)
1. El **`table`** en el que desea crear la columna
1. Cualquiera **`example data points`** que describen qué debe contener la columna

Estos son algunos ejemplos comunes de columnas calculadas avanzadas que los usuarios suelen encontrar útiles:

* [Ordenar (o clasificar) evento secuencialmente](#compareevents)
* [Encuentre el tiempo entre dos eventos](#twoevents)
* [Comparar valores de eventos secuenciales](#sequence)
* [Convertir moneda](#currency)
* [Convertir husos horarios](#timezone)
* [Algo más](#else)

## Estoy intentando ordenar los eventos secuencialmente {#compareevents}

Esto se denomina **número de evento** columna calculada. Esto significa que está intentando encontrar la secuencia en la que se produjeron los eventos para un propietario de evento determinado, como un cliente o un usuario.

A continuación se muestra un ejemplo:

| **`event\_id`** | **`owner\_id`** | **`timestamp`** | **`Owner's event number`** |
|-----|-----|-----|-----|
| 1 | `A` | 2015-01-01 00:00:00 | 1 |
| 2 | `B` | 2015-01-01 00:30:00 | 1 |
| 3 | `A` | 2015-01-01 02:00:00 | 2 |
| 4 | `A` | 2015-01-02 13:00:00 | 3 |
| 5 | `B` | 2015-01-03 13:00:00 | 2 |

{style="table-layout:auto"}

Se puede utilizar una columna calculada de número de evento para observar las diferencias de comportamiento entre los eventos de primera vez, los eventos de repetición o los eventos n en los datos.

¿Quiere ver la columna de número de pedido del cliente en acción? Haga clic en la imagen para verla utilizada como dimensión Agrupar por en un informe.

![Uso de una columna calculada de número de evento para agrupar por el número de pedido del cliente.](../../assets/EventNumber.gif)<!--{: style="max-width: 500px;"}-->

Para crear este tipo de columna calculada, debe saber:

* La tabla en la que desea crear esta columna
* El campo que identifica al propietario de los eventos (`owner\_id` en este ejemplo)
* El campo por el que desea ordenar los eventos (`timestamp` en este ejemplo)

[Volver al principio](#top)

## Estoy tratando de encontrar el tiempo entre dos eventos. {#twoevents}

Esto se denomina `date difference` columna calculada. Esto significa que está intentando encontrar el tiempo entre dos eventos que pertenecen a un único registro, en función de las marcas de tiempo del evento.

A continuación se muestra un ejemplo:

| `id` | `timestamp\_1` | `timestamp\_2` | `Seconds between timestamp\_2 and timestamp\_1` |
|-----|-----|-----|-----|
| `A` | 2015-01-01 00:00:00 | 2015-01-01 12:30:00 | 45000 |
| `B` | 2015-01-01 08:00:00 | 2015-01-01 10:00:00 | 7200 |

{style="table-layout:auto"}

Se puede utilizar una columna calculada de diferencia de fecha para crear una métrica que calcule el promedio o la mediana de tiempo entre dos eventos. Haga clic en la siguiente imagen para ver cómo se muestra la `Average time to first order` Esta métrica se utiliza en un informe.

![Uso de una columna calculada de diferencia de fecha para calcular el tiempo promedio para el primer pedido.](../../assets/DateDifference.gif)<!--{: style="max-width: 500px;"}-->

Para crear este tipo de columna calculada, debe saber:

* La tabla en la que desea crear esta columna
* Las dos marcas de tiempo entre las que desea saber la diferencia

[Volver al principio](#top)

## Estoy intentando comparar valores de eventos secuenciales. {#sequence}

Esto se denomina **comparación de eventos secuenciales**. Esto significa que está intentando encontrar el delta entre un valor (moneda, número, marca de tiempo) y el valor correspondiente para el evento anterior del propietario.

A continuación se muestra un ejemplo:

| **`event\_id`** | **`owner\_id`** | **`timestamp`** | **`Seconds since owner's previous event`** |
|-----|-----|-----|-----|
| 1 | `A` | 2015-01-01 00:00:00 | NULL |
| 2 | `B` | 2015-01-01 00:30:00 | NULL |
| 3 | `A` | 2015-01-01 02:00:00 | 7720 |
| 4 | `A` | 2015-01-02 13:00:00 | 126000 |
| 5 | `B` | 2015-01-03 13:00:00 | 217800 |

{style="table-layout:auto"}

Se puede utilizar una comparación de eventos secuenciales para encontrar el tiempo promedio o medio entre cada evento secuencial. Haga clic en la siguiente imagen para ver la **Tiempo medio y medio entre pedidos** métricas en acción.

=![Uso de una columna calculada de comparación de eventos secuenciales para calcular el tiempo promedio y la mediana entre pedidos.](../../assets/SeqEventComp.gif)<!--{: style="max-width: 500px;"}-->

Para crear este tipo de columna calculada, debe saber:

* La tabla en la que desea crear esta columna
* El campo que identifica al propietario de los eventos (`owner\_id` en el ejemplo)
* El campo de valor entre el que desea ver la diferencia para cada evento secuencial (`timestamp` en este ejemplo)

[Volver al principio](#top)

## Estoy intentando convertir moneda. {#currency}

A **conversión de moneda** la columna calculada convierte los importes de las transacciones de una divisa registrada a una divisa funcional, según el tipo de cambio del momento del evento.

A continuación se muestra un ejemplo:

| **`id`** | **`timestamp`** | **`transaction\_value\_EUR`** | **`transaction\_value\_USD`** |
|-----|-----|-----|-----|
| `1` | 2015-01-01 00:00:00 | 30 | 33.57 |
| `2` | 2015-01-02 00:00:00 | 50 | 55.93 |

{style="table-layout:auto"}

Para crear este tipo de columna calculada, debe saber:

* La tabla en la que desea crear esta columna
* La columna de importe de transacción que desea convertir
* La columna que indica la moneda en la que se registraron los datos (normalmente un código ISO)
* La moneda de notificación preferida

[Volver al principio](#top)

## Estoy intentando convertir zonas horarias. {#timezone}

A **conversión de huso horario** la columna calculada convierte las marcas de tiempo de una fuente de datos determinada de su zona horaria registrada a una zona horaria de sistema de informes.

A continuación se muestra un ejemplo:

| **`id`** | **`timestamp\_UTC`** | **`timestamp\_ET`** |
|-----|-----|-----|
| `1` | 2015-01-01 00:00:00 | 2014-12-31 19:00:00 |
| `2` | 2015-01-01 12:00:00 | 2015-01-01 07:00:00 |

{style="table-layout:auto"}

Para crear este tipo de columna calculada, debe saber:

* La tabla en la que desea crear esta columna
* La columna de marca de tiempo que desea convertir
* Zona horaria en la que se registraron los datos
* La zona horaria preferida para los informes

[Volver al principio](#top)

## Estoy tratando de hacer algo que no está en la lista. {#else}

No te preocupes. El hecho de que no aparezca en la lista no significa que no sea posible. El equipo de Adobe de analistas de Data Warehouse puede ayudarle.

Para definir una nueva columna calculada, [enviar un ticket de asistencia](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html) con detalles sobre exactamente lo que desea crear.

## Documentación relacionada

* [Creación de columnas calculadas](../data-warehouse-mgr/creating-calculated-columns.md)
* [Tipos de columnas calculadas](../data-warehouse-mgr/calc-column-types.md)
* [Edificio [!DNL Google ECommerce] dimensiones con datos de pedidos y clientes](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
