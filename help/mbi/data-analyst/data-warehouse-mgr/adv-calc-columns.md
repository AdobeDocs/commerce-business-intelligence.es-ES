---
title: Tipos de columnas calculadas avanzadas
description: Conozca los conceptos básicos de la mayoría de los casos de columnas de uso, pero puede que desee una columna calculada que sea un poco más compleja de lo que puede crear el Administrador de Datas Warehouse.
exl-id: 9871fa19-95b3-46e4-ae2d-bd7c524d12db
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '902'
ht-degree: 0%

---

# Tipos de columnas calculadas avanzadas

Muchos análisis que puede intentar crear, implican el uso de un **nueva columna** que desea `group by` o `filter by`. La variable [Creación de columnas calculadas](../data-warehouse-mgr/creating-calculated-columns.md) Este tutorial trata los conceptos básicos de la mayoría de los casos de uso, pero es posible que desee calcular una columna un poco más compleja de lo que el Administrador de Datas Warehouse puede crear.
{: #top}

Nuestro equipo de analistas de Data Warehouse puede crear estos tipos de columnas. Para definir una nueva columna calculada, proporciónenos la siguiente información:

1. La variable **`definition`** de esta columna (incluyendo entradas, fórmulas o formato)
1. La variable **`table`** en el que desea crear la columna
1. Cualquiera **`example data points`** que describen lo que debe contener la columna

Estos son algunos ejemplos comunes de columnas calculadas avanzadas que los usuarios suelen encontrar útiles:

* [Evento de orden (o clasificación) secuencialmente](#compareevents)
* [Buscar el tiempo entre dos eventos](#twoevents)
* [Comparar valores de eventos secuenciales](#sequence)
* [Convertir moneda](#currency)
* [Convertir zonas horarias](#timezone)
* [Algo más](#else)

## Estoy intentando ordenar los eventos secuencialmente {#compareevents}

Lo llamamos **número de evento** columna calculada. Esto significa que estamos intentando encontrar la secuencia en la que se produjeron los eventos para un propietario de un evento en particular, como un cliente o un usuario.

Este es un ejemplo:

| **`event\_id`** | **`owner\_id`** | **`timestamp`** | **`Owner's event number`** |
|-----|-----|-----|-----|
| 1 | `A` | 01-01-2015:00:00 | 1 |
| 2 | `B` | 01-01-2015:30:00 | 1 |
| 3 | `A` | 01-01-2015:00:00 | 2 |
| 4 | `A` | 2015-01-02 14:00:00 | 3 |
| 5 | `B` | 2015-01-03 14:00:00 | 2 |

{style=&quot;table-layout:auto&quot;}

Se puede utilizar una columna calculada de número de evento para observar diferencias de comportamiento entre eventos nuevos, eventos repetidos o eventos nth en los datos.

¿Quiere ver la columna de número de pedido del cliente en acción? Haga clic en la imagen para verla utilizada como dimensión Agrupar por en un informe.

![Uso de una columna calculada de número de evento para Agrupar por el número de pedido del cliente.](../../assets/EventNumber.gif)<!--{: style="max-width: 500px;"}-->

Para crear este tipo de columna calculada, es necesario saber:

* La tabla en la que desea crear esta columna
* El campo que identifica al propietario de los eventos (`owner\_id` en este ejemplo)
* El campo por el que desea ordenar los eventos (`timestamp` en este ejemplo)

[Volver al principio](#top)

## Estoy tratando de encontrar el tiempo entre dos eventos. {#twoevents}

Lo llamamos `date difference` columna calculada. Esto significa que estamos intentando encontrar el tiempo entre dos eventos que pertenecen a un solo registro, en función de las marcas de tiempo del evento.

Este es un ejemplo:

| `id` | `timestamp\_1` | `timestamp\_2` | `Seconds between timestamp\_2 and timestamp\_1` |
|-----|-----|-----|-----|
| `A` | 01-01-2015:00:00 | 2015-01-01 12:30:00 | 45000 |
| `B` | 01-01-2015:00:00 | 2015-01-01 11:00:00 | 7200 |

{style=&quot;table-layout:auto&quot;}

Se puede usar una columna calculada de diferencia de fecha para crear una métrica que calcule el tiempo promedio o medio entre dos eventos. Haga clic en la imagen siguiente para comprobar cómo se muestra la variable `Average time to first order` en un informe.

![Uso de una columna calculada de diferencia de fecha para calcular el Tiempo promedio para el primer pedido.](../../assets/DateDifference.gif)<!--{: style="max-width: 500px;"}-->

Para crear este tipo de columna calculada, es necesario saber:

* La tabla en la que desea crear esta columna
* Las dos marcas de tiempo entre las que desea conocer la diferencia

[Volver al principio](#top)

## Estoy intentando comparar los valores de eventos secuenciales. {#sequence}

Lo llamamos **comparación de eventos secuenciales**. Esto significa que estamos intentando encontrar el delta entre un valor (moneda, número, marca de tiempo) y el valor correspondiente para el evento anterior del propietario.

Este es un ejemplo:

| **`event\_id`** | **`owner\_id`** | **`timestamp`** | **`Seconds since owner's previous event`** |
|-----|-----|-----|-----|
| 1 | `A` | 01-01-2015:00:00 | NULL |
| 2 | `B` | 01-01-2015:30:00 | NULL |
| 3 | `A` | 01-01-2015:00:00 | 7720 |
| 4 | `A` | 2015-01-02 14:00:00 | 126000 |
| 5 | `B` | 2015-01-03 14:00:00 | 217800 |

{style=&quot;table-layout:auto&quot;}

Se puede usar una comparación de evento secuencial para encontrar el tiempo promedio o medio entre cada evento secuencial. Haga clic en la imagen siguiente para ver la **Promedio y mediana de tiempo entre pedidos** métricas en acción.

=![Uso de una columna calculada de comparación de eventos secuencial para calcular el tiempo promedio y medio entre pedidos.](../../assets/SeqEventComp.gif)<!--{: style="max-width: 500px;"}-->

Para crear este tipo de columna calculada, es necesario saber:

* La tabla en la que desea crear esta columna
* El campo que identifica al propietario de los eventos (`owner\_id` en el ejemplo)
* El campo de valor que desea que vea la diferencia entre para cada evento secuencial (`timestamp` en este ejemplo)

[Volver al principio](#top)

## Estoy tratando de convertir moneda. {#currency}

A **conversión de moneda** la columna calculada convierte los importes de transacción de una moneda registrada a una moneda de generación de informes, según el tipo de cambio en el momento del evento.

Este es un ejemplo:

| **`id`** | **`timestamp`** | **`transaction\_value\_EUR`** | **`transaction\_value\_USD`** |
|-----|-----|-----|-----|
| `1` | 01-01-2015:00:00 | 30 | 33,57 |
| `2` | 2015-01-02 00:00:00 | 50 | 55,93 |

{style=&quot;table-layout:auto&quot;}

Para crear este tipo de columna calculada, es necesario saber:

* La tabla en la que desea crear esta columna
* La columna de importe de transacción que desea convertir
* La columna que indica la moneda en la que se registraron los datos (normalmente, un código ISO)
* La moneda preferida para la creación de informes

[Volver al principio](#top)

## Estoy tratando de convertir zonas horarias. {#timezone}

A **conversión de zona horaria** la columna calculada convierte las marcas de hora de una fuente de datos concreta de su zona horaria registrada a una zona horaria de informes.

Este es un ejemplo:

| **`id`** | **`timestamp\_UTC`** | **`timestamp\_ET`** |
|-----|-----|-----|
| `1` | 01-01-2015:00:00 | 2014-12-31 19:00:00 |
| `2` | 2015-01-01 12:00:00 | 01-01-2015:00:00 |

{style=&quot;table-layout:auto&quot;}

Para crear este tipo de columna calculada, es necesario saber:

* La tabla en la que desea crear esta columna
* La columna de marca de tiempo que desea convertir
* Zona horaria en la que se registraron los datos
* Zona horaria de informes preferida

[Volver al principio](#top)

## Estoy tratando de hacer algo que no figura aquí. {#else}

No hay que preocuparse. Solo porque no esté listado aquí no significa que no sea posible. Nuestro equipo de analistas de Data Warehouse le ha cubierto.

Para definir una nueva columna calculada, [enviar un ticket de asistencia](../../guide-overview.md) con detalles sobre exactamente lo que desea crear.

## Documentación relacionada

* [Creación de columnas calculadas](../data-warehouse-mgr/creating-calculated-columns.md)
* [Tipos de columnas calculadas](../data-warehouse-mgr/calc-column-types.md)
* [Creación [!DNL Google ECommerce] dimensiones con datos de pedidos y clientes](../data-warehouse-mgr/bldg-google-ecomm-dim.md)
