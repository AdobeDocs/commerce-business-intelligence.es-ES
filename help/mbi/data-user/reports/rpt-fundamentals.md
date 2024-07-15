---
title: Uso de un informe
description: Aprenda a utilizar los datos del informe.
exl-id: 94d4db27-0e06-4066-9c03-036b109d2d9b
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '985'
ht-degree: 0%

---

# Uso de un informe

Use los informes de [!DNL Adobe Commerce Intelligence] para responder preguntas comerciales: si simplemente desea ver los ingresos de este mes en comparación con los del año pasado o comprender los costos de adquisición de la última campaña [!DNL Google AdWords].

¿Cómo se ve exactamente ese camino de la pregunta a la respuesta?

Para ayudarle a visualizar este proceso, esa ruta se asigna a continuación. Este tema aclara cómo abordar una pregunta analítica y la logística back-end necesaria para obtener los datos que necesita.

## Empezando por la pregunta

Usted sabe que constantemente está haciendo preguntas para mejorar su negocio, desde aumentar la satisfacción del cliente hasta reducir los costos de suministro. Usted se centra en cómo traducir sus preguntas en análisis que le ayuden a tomar decisiones.

Para este ejemplo, supongamos que desea responder a la siguiente pregunta:

* ¿Con qué rapidez se convierten mis nuevos inscritos?

## Identificación de una medición

Es hora de identificar una lista de posibles análisis y mediciones que ayuden a responder la pregunta. Para este ejemplo, céntrese en la siguiente métrica:

* Tiempo promedio desde el registro hasta la primera fecha de compra por uso.

Esto revela el tiempo promedio que transcurre entre la fecha de registro y la primera fecha de compra de los usuarios, y da una idea de cómo se comportan los usuarios en este paso final del canal de conversión.

## Búsqueda de los datos

Entender qué medir solo nos lleva a parte del camino. Para evaluar el tiempo promedio desde el registro hasta la primera fecha de compra por usuario, debe identificar todos los puntos de datos de los que se compone la medida.

Desglose la medida en sus componentes principales. Debe saber el número de personas que se registraron, el número de personas que realizaron una compra y el tiempo que transcurrió entre esos dos eventos.

En un nivel superior, necesita saber dónde encontrar estos datos en la base de datos, específicamente:

* La tabla que registra una fila de datos cada vez que alguien se registra
* La tabla que registra una fila de datos que cada vez que alguien realiza una compra
* La columna que se puede usar para unir o hacer referencia a la tabla `purchase` a la tabla `customer` - esto nos permite saber quién hizo una compra

En un nivel más granular, debe identificar los campos de datos exactos que se utilizan para este análisis:

* La tabla de datos y la columna que contienen la fecha de registro de un cliente: por ejemplo `user.created\_at`
* Tabla de datos y columna que contienen una fecha de compra: por ejemplo `order.created\_at`

## Creación de columnas de datos para su análisis

Además de las columnas de datos nativos descritas anteriormente, también necesita un conjunto de campos de datos calculados para habilitar este análisis, que incluye:

* `Customer's first purchase date` que devuelve `MIN(order.created_at` de un usuario específico)

A continuación, se utiliza para crear:

* `Time between a customer's registration date and first purchase date`, que devuelve el tiempo de un usuario específico transcurrido entre el registro y la fecha de la primera compra. Esta es la base de la métrica más adelante.

Ambos campos deben crearse en el nivel de usuario (por ejemplo, en la tabla `user`). Esto permite que los usuarios puedan normalizar el análisis promedio (es decir, el denominador en este cálculo de promedio es el recuento de usuarios).

¡Aquí es donde [!DNL Commerce Intelligence] interviene! Puede usar su Data Warehouse [!DNL Commerce Intelligence] para crear las columnas anteriores. Póngase en contacto con el equipo de analistas de Adobe y proporciónenos la definición específica de sus nuevas columnas para la creación. También puede usar el [Editor de columnas](../../data-analyst/data-warehouse-mgr/creating-calculated-columns.md).

Se recomienda evitar la creación de estos campos de datos calculados directamente en la base de datos, ya que supone una carga innecesaria para los servidores de producción.

## Creación de la métrica

Ahora que tiene los campos de datos requeridos para el análisis, es hora de buscar o crear la métrica relevante para construir el análisis.

Aquí desea realizar el siguiente cálculo:


_[SUMA de `Time between a customer's registration date and first purchase date`] / [Cantidad total de clientes que se registraron y compraron]_

Y desea ver este cálculo trazado en el tiempo, o tendencias, según la fecha de registro de un cliente. Y así es como [crear esta métrica](../../data-user/reports/ess-manage-data-metrics.md) en [!DNL Commerce Intelligence]:

1. Vaya a **[!UICONTROL Data]** y seleccione la ficha `Metrics`.
1. Haga clic en **[!UICONTROL Add New Metric]** y seleccione la tabla `user` (donde creó las dimensiones anteriores).
1. En el menú desplegable, seleccione `Average` en la columna `Time between a customer's registration date and first purchase date` de la tabla `user` ordenada por la columna `Customer's registration date`.
1. Añada los filtros o conjuntos de filtros relevantes.

Esta métrica ya está lista.

## Creación del informe

Con la nueva métrica configurada, puede utilizarla para informar sobre el tiempo promedio entre el registro y la fecha de la primera compra por fecha de registro.

Simplemente, ve a cualquier panel y [crea un informe](../../data-user/reports/ess-manage-data-metrics.md) con la métrica creada anteriormente.

### `Visual Report Builder` {#visualrb}

[El `Visual Report Builder`](../../data-user/reports/ess-rpt-build-visual.md) es la forma más sencilla de visualizar los datos. Si no está familiarizado con SQL o desea crear rápidamente un informe, lo mejor es utilizar el Report Builder visual. Con solo unos clics, puede agregar métricas, segmentar los datos y crear informes en toda la organización. Esta opción es perfecta tanto para principiantes como para expertos, ya que no requiere ninguna experiencia técnica.

|  |  |
|--- |--- |
| **Esto es perfecto para...** | **Esto no es tan bueno para...** |
| - Todos los niveles de experiencia de análisis/tecnología<br>- Creación rápida de informes<br>- Creación de análisis para compartirlos con otros usuarios | - Análisis que requieren funciones específicas de SQL<br>- Prueba de nuevas columnas: las columnas calculadas dependen de los ciclos de actualización para la población de datos inicial, mientras que las creadas con SQL no. |

{style="table-layout:auto"}

### Descripciones e imágenes del informe

#### Adición de descripciones a informes

Al crear informes que se comparten con otros miembros de su equipo, Adobe recomienda añadir descripciones que permitan a otros usuarios comprender mejor su análisis.

1. Haga clic en **[!UICONTROL i]** en la parte superior de cualquier informe.
1. Escriba una descripción en el cuadro de texto.
1. Haga clic en **[!UICONTROL Save Description]**.

Consulte lo siguiente:

![Descripción del gráfico](../../assets/Chart_Description.gif)

#### Exportación de informes como imágenes

¿Necesita incluir un informe en una presentación o documento? Cualquier informe se puede guardar como una imagen (en formato PNG, PDF o SVG) mediante el menú `Report Options`, que se encuentra en la esquina superior derecha de cada informe.

1. Haga clic en el icono de engranaje en la esquina superior derecha de cualquier informe.
1. En el menú desplegable, seleccione `Enlarge`.
1. Cuando se agrande el informe, haga clic en **[!UICONTROL Download]**, en la esquina superior derecha del informe.
1. Seleccione el formato de imagen preferido en la lista desplegable. La descarga comienza inmediatamente.

Consulte lo siguiente:

![](../../assets/exp-rep-as-image.gif)
