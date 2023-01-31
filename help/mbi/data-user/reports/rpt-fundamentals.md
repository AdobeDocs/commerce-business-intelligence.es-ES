---
title: Uso de un informe
description: Aprenda a utilizar los datos del informe.
exl-id: 94d4db27-0e06-4066-9c03-036b109d2d9b
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '1024'
ht-degree: 0%

---

# Uso de un informe

Uso de informes en [!DNL MBI] para ayudarle a responder preguntas comerciales: si solo desea ver los ingresos de este mes en comparación con el año pasado o comprender los costes de adquisición de su [!DNL Google AdWords] campaña.

¿Cómo es exactamente ese camino de la pregunta a la respuesta?

Para ayudarle a visualizar este proceso, hemos diseñado esa ruta a continuación. En este tema se aclarará cómo abordamos una pregunta analítica y la logística back-end necesaria para obtener los datos que necesita.

## Comenzando con la pregunta

Sabemos que usted está constantemente haciendo preguntas para mejorar su negocio, desde aumentar la satisfacción del cliente hasta reducir los costos de suministro. Nos centraremos en cómo traducir sus preguntas en análisis que le ayuden a tomar decisiones.

Para nuestro ejemplo, suponemos que queremos responder a la siguiente pregunta:

* ¿A qué velocidad se convierten mis nuevos inscritos?

## Identificación de una medición

Con nuestra pregunta en mano, es hora de identificar una lista de posibles análisis y mediciones para ayudar a responder a la pregunta. Para este ejemplo, céntrese en la siguiente métrica:

* Promedio de tiempo desde el registro hasta la primera fecha de compra por uso.

Esto revelará el tiempo promedio que transcurre entre la fecha de registro y la fecha de la primera compra de los usuarios y dará una idea de cómo se comportan los usuarios en este último paso del canal de conversión.

## Búsqueda de datos

Comprender lo que se debe medir solo nos lleva a una parte del camino. Para evaluar el tiempo promedio desde el registro hasta la primera fecha de compra por usuario, necesitamos identificar todos los puntos de datos de los que se compone nuestra medida.

Desglose nuestra medida en sus componentes principales: necesitamos saber el número o número de personas que se registraron; el número de personas que realizaron una compra; y el tiempo que transcurrió entre esos dos eventos.

En un nivel superior, necesitamos saber dónde encontrar estos datos en la base de datos, específicamente:

* La tabla que registra una fila de datos cada vez que alguien se registra
* La tabla que registra una fila de datos cada vez que alguien realiza una compra
* La columna que se puede usar para unir o hacer referencia a la variable `purchase` a `customer` tabla - esto nos permitirá saber quién realizó una compra

A un nivel más granular, necesitamos identificar los campos de datos exactos que se utilizarán para este análisis:

* La tabla de datos y la columna que contienen la fecha de registro de un cliente: por ejemplo `user.created\_at`
* La tabla de datos y la columna que contienen una fecha de compra: por ejemplo `order.created\_at`

## Creación de columnas de datos para análisis

Además de las columnas de datos nativas descritas anteriormente, también necesitamos un conjunto de campos de datos calculados para habilitar este análisis, que incluye:

* `Customer's first purchase date` que devuelve el valor de `MIN(order.created_at`)

Esto se utilizará para crear:

* `Time between a customer's registration date and first purchase date`, que devuelve el tiempo que un usuario específico ha transcurrido entre el registro y la primera fecha de compra. Esta será la base de nuestra métrica más adelante.

Ambos campos deben crearse a nivel de usuario (por ejemplo, en la variable `user` ), de modo que los usuarios puedan normalizar el análisis promedio (es decir, el denominador de este cálculo promedio será el recuento de usuarios).

Aquí es donde [!DNL MBI] ¡entra! Puede aprovechar el [!DNL MBI] almacén de datos para crear las columnas anteriores. Simplemente contacte con nuestro equipo de analistas y proporciónenos la definición específica de sus nuevas columnas y las crearemos. También puede aprovechar nuestra [Editor de columnas](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md).

Se recomienda evitar crear estos campos de datos calculados directamente en la base de datos, ya que esto supone una carga innecesaria para los servidores de producción.

## Creación de la métrica

Ahora que tenemos los campos de datos requeridos para nuestro análisis, es hora de encontrar o crear la métrica relevante para construir nuestro análisis.

Aquí sabemos que, matemáticamente, queremos realizar el siguiente cálculo:


_[SUMA de `Time between a customer's registration date and first purchase date`] / [Número total de clientes que se registraron y compraron]_

Y queremos ver este cálculo planeado a lo largo del tiempo, o de tendencias, según la fecha de registro de un cliente. Y aquí está cómo [crear esta métrica](../../data-user/reports/ess-manage-data-metrics.md) en [!DNL MBI]:

1. Vaya a **[!UICONTROL Data]** y seleccione `Metrics` pestaña .
1. Haga clic en **[!UICONTROL Add New Metric]** y seleccione `user` (donde hemos creado las dimensiones anteriores).
1. En el menú desplegable, seleccione `Average` en el`Time between a customer's registration date and first purchase date` en la columna `user` tabla ordenada por el `Customer's registration date`  para abrir el Navegador.
1. Añada filtros o conjuntos de filtros relevantes.

Esta métrica ya está lista.

## Creación del informe

Con la nueva métrica configurada, podemos utilizarla para informar sobre el tiempo promedio entre el registro y la primera fecha de compra por fecha de registro.

Simplemente vaya a cualquier panel y [crear un nuevo informe](../../data-user/reports/ess-manage-data-metrics.md) usando la métrica creada anteriormente.

### `Visual Report Builder` {#visualrb}

[La variable `Visual Report Builder`](../../data-user/reports/ess-rpt-build-visual.md) es la forma más sencilla de visualizar los datos. Si no está familiarizado con SQL o solo desea crear rápidamente un informe, el Report Builder visual es su mejor opción. Con tan solo unos clics, puede agregar métricas, segmentar los datos y crear informes para toda la organización. Esta opción es perfecta tanto para principiantes como para expertos, ya que no requiere ninguna experiencia técnica.

|  |  |
|--- |--- |
| **Esto es perfecto para...** | **Esto no es tan bueno para...** |
| - Todos los niveles de análisis/experiencia tecnológica<br>- Creación rápida de informes<br>- Creación de análisis para compartirlos con otros usuarios | - Análisis que requieren funciones específicas de SQL<br>- Prueba de nuevas columnas: las columnas calculadas dependen de los ciclos de actualización para la población de datos inicial, mientras que las creadas con SQL no |

{style=&quot;table-layout:auto&quot;}

### Descripciones e imágenes de informes

#### Adición de descripciones a los informes

Al crear informes que se compartirán con otros miembros de su equipo, se recomienda agregar descripciones que permitan a otros usuarios comprender mejor su análisis.

1. Haga clic en **[!UICONTROL i]** en la parte superior de cualquier informe.
1. Escriba una descripción en el cuadro de palabras.
1. Haga clic en **[!UICONTROL Save Description]**.

Echemos un vistazo:

![Descripción del gráfico](../../assets/Chart_Description.gif)

#### Exportación de informes como imágenes

¿Necesita incluir un informe en una presentación o documento? Cualquier informe se puede guardar como una imagen (en formato PNG, PDF o SVG) utilizando la variable `Report Options` , ubicado en la esquina superior derecha de cada informe.

1. Haga clic en el icono de engranaje en la esquina superior derecha de cualquier informe.
1. En el menú desplegable, seleccione `Enlarge`.
1. Cuando el informe aumente, haga clic en **[!UICONTROL Download]** en la esquina superior derecha del informe.
1. Seleccione el formato de imagen preferido en la lista desplegable. La descarga comenzará inmediatamente.

Eche un vistazo:

![](../../assets/exp-rep-as-image.gif)
