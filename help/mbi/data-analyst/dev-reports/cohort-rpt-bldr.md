---
title: Report Builder de cohorte
description: Obtenga información acerca del análisis de grupos de usuarios que comparten características similares a lo largo de sus ciclos de vida.
exl-id: d80c5389-7256-40e0-86e0-49903113f93d
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1556'
ht-degree: 0%

---

# Report Builder de cohorte

¿Alguna vez ha querido estudiar cómo se comportan los distintos subconjuntos de los usuarios a lo largo del tiempo? Por ejemplo, ¿se ha preguntado alguna vez si los usuarios que se registran durante un periodo de promoción tienen unos ingresos medios a largo plazo más altos que los que no lo tienen? Si la respuesta es `Yes`y, a continuación, el `Cohort Report Builder` es la herramienta perfecta para ti. [!DNL Adobe Commerce Intelligence] está optimizado para realizar este análisis y hacerlo relevante para su negocio.

## ¿Qué es el análisis de cohorte? {#what}

`Cohort` el análisis puede definirse, en términos generales, como el análisis de grupos de usuarios que comparten características similares a lo largo de sus ciclos de vida. Permite identificar tendencias de comportamiento entre diferentes grupos de usuarios.

Para obtener una imprimación detallada sobre `cohort` análisis, revisión [esta página](https://www.cohortanalysis.com/).

En su [!DNL Commerce Intelligence] panel, es fácil crear un usuario `cohorts` basado en un `cohort` fecha y una métrica en su cuenta.

## Bueno, ¿por qué es importante el análisis de cohorte? {#important}

Como se mencionó anteriormente, `cohort` El análisis de permite identificar tendencias de comportamiento entre diferentes grupos de usuarios. Con una sólida comprensión de cómo se comportan ciertos grupos, puede adaptar sus decisiones y gastos para maximizar sus ventas. Por ejemplo, imagine ingresos de por vida `cohort` análisis: aunque este tipo de análisis es beneficioso por muchas razones, la inmediata es tomar mejores decisiones de adquisición de clientes.

## ¿Cómo puedo crear los míos? `cohort` ¿análisis?

### Nueva arquitectura

Estas son las instrucciones para usar la variable `Cohort Report Builder` en el [Nueva arquitectura](../../administrator/account-management/new-architecture.md).

1. Clic **[!UICONTROL Report Builder]** en la pestaña izquierda o **[!UICONTROL Add Report** > **Create Report]** en cualquier tablero.

1. En el `Report Builder` pantalla de selección, haga clic en **[!UICONTROL Create Report]** junto al `Visual Report Builder` opción.

**Adición de una métrica**

Ahora que está en la `Report Builder`A continuación, añada la métrica en la que desea realizar el análisis (por ejemplo: `Revenue` o `Orders`).

>[!NOTE]
>
>Nativo [!DNL Google Analytics] Las métricas de no son compatibles con `Cohort Report Builder`.

**Cambie la Vista de métrica a`Cohort`**

![](../../assets/visual-report-builder-cohort-toggle.png)

Esto abre una nueva ventana para configurar los detalles de la `Cohort` Informe.

### Se necesitan cinco especificaciones para crear un `Cohort` informe:

1. Cómo agrupar los `cohorts`
1. El `cohort` período de tiempo
1. El número de `cohorts` para ver
1. La cantidad mínima de datos cada `cohort` debe contener
1. Intervalo de tiempo después de `cohort` Ocurrencia

#### 1. Agrupación `cohorts`

`Cohorts` se agrupan por una marca de tiempo, como **fecha de registro** o **fecha del primer pedido**.

>[!NOTE]
>
>No puede usar la misma marca de tiempo en la que está creada la métrica para `cohort` fecha. Para un análisis que lo requiera, puede utilizar el `Standard report builder` en su lugar.

#### 2. `Cohort` período de tiempo

Elija el período de tiempo que desea agrupar `cohorts` por. En otras palabras, qué parte de la marca de tiempo seleccionada arriba es la más importante; la `week`, `month`, `quarter`, o `year`? El informe muestra los datos en el intervalo que seleccione aquí

#### 3. y 4. Establezca el número de `cohorts` para ver y cuántos datos necesita cada `cohort` debe tener

Estos parámetros le ayudan a ver solo los `cohorts` que le interesan, y el práctico `Preview` en la parte inferior de la ventana se muestra exactamente qué cohortes aparecen en el informe.

De forma predeterminada, la variable `cohort` no se incluye a menos que cambie la cantidad mínima de datos necesaria para cada `cohort` hasta `0`. En este caso, la variable `cohort` para el periodo de tiempo actual solo incluye datos parciales.

#### 5. Intervalo de tiempo después de `Cohort` Ocurrencia

Esta función le permite establecer el intervalo de tiempo de datos que ve para el seleccionado `cohorts`. Por ejemplo, si desea ver 24 informes mensuales `cohorts` basado en `customer's first order date`, pero solo le interesan los 3 primeros meses de datos de cada uno `cohort`, puede configurar el `number of cohorts to view` hasta `24` y el `time range after cohort occurrence` hasta `3`.

El intervalo de este valor cambia independientemente de lo que haya seleccionado en la `cohort time period` y el valor se establece en `12` de forma predeterminada; el valor no cambia a menos que haga clic en el icono de calendario para editarlo.

![](../../assets/cohort-time-range.png)

#### Otras notas

* [!UICONTROL Filters]: aplicado a las métricas, permanece intacto al alternar entre `Standard` y `Cohort` vistas.

* Consulte [`Perspectives`](#perspectives).

#### Ejemplo

Aquí tiene un ejemplo para unirlo todo. En este ejemplo, deseo comprobar el comportamiento de los pedidos después de un `cohort`La primera compra de para ver si esa cohorte regresa para realizar compras repetidas en los próximos seis meses.

![Cohorte de pedidos](../../assets/crb_example.gif)

### Arquitectura heredada

#### Arquitectura heredada {#personalinfo}

A continuación se ofrecen instrucciones específicas para la versión heredada de `Cohort Report Builder`. Si está interesado en utilizar la nueva versión, consulte [Nueva arquitectura](../../administrator/account-management/new-architecture.md) para obtener más información sobre la migración a una [!DNL Commerce Intelligence] Nueva cuenta de arquitectura.

#### ¿Cómo puedo crear los míos? `cohort` ¿análisis? {#create}

![](../../assets/create-cohort-analysis.png)

`Cohort` ¡análisis en acción! Aquí puede ver el crecimiento de los ingresos a lo largo del tiempo de forma acumulativa y por usuario.

Esta sección le explica cómo crear los suyos propios `cohort` análisis. Para ver ejemplos (y GIF animados que muestran el proceso), consulte la [Sección Ejemplos](#examples) de este tema.

1. Clic **[!UICONTROL Report Builder]** en la pestaña izquierda o **[!UICONTROL Add Report** > **Create Report]** en cualquier tablero.

1. En el `Report Builder Selection` , haga clic en **[!UICONTROL Create Report]** junto al `Cohort Analysis` opción.

#### Adición de una métrica

Ahora que está en la `Cohort Report Builder`, añada la métrica (por ejemplo: `Revenue` o `Number of orders`) en el que desea realizar el análisis.

>[!NOTE]
>
>Nativo [!DNL Google Analytics] Las métricas de no son compatibles con `Cohort Report Builder`.

#### Selección de la fecha de cohorte {#date}

El siguiente paso es especificar la variable `cohort date`. Es la fecha en la que se agrupan los usuarios. Por ejemplo, podría ser `User's first order date` o `User's registration date`.

>[!NOTE]
>
>No se puede usar la misma fecha en la que se creó la métrica (por ejemplo: `created at`) como `cohort date`.

#### Configuración del intervalo y el período de tiempo

A continuación, configure el `Interval` y `Time Period`.

`Interval`
El `Interval` permite configurar las opciones de `length` de su `cohorts`. Por ejemplo, si se establece en `Month`, el informe se medirá en meses.

Puede cambiar la forma en que se muestran estos intervalos en el eje x mediante la variable **Duración** menú.

`Time Period`
Utilice el `Time Period` para elegir el usuario específico `cohorts` para analizar. Puede mostrar cada `cohort`, elija de una lista, especifique un intervalo de tiempo o defina un intervalo de tiempo móvil de `cohorts` para incluir. Por ejemplo, si utilizó la variable `Specific Cohorts` , puede seleccionar meses específicos para incluirlos en el análisis:

![Uso del `Time Period` menú para añadir específico `Cohorts`](../../assets/Cohort_Time_Period.gif)

Si lo está agrupando `cohorts` por fecha de registro y, a continuación, se seleccionan abril, mayo y junio en la `Specific Cohorts` , se incluirían todos los usuarios que se registraran en esos meses.

#### Definición del eje X

En `duration`, puede definir la configuración del eje X del gráfico. Es decir, cuántos periodos de tiempo representa cada punto de datos y cuántos puntos de datos incluir en el análisis.

#### Selección de la `counting members` tabla

Si optó por agrupar a los usuarios por un `cohort date` que se ha unido desde otra tabla, es posible que vea un `counting members in the … table` opción.

![](../../assets/Cohort_Counting_Members_option.png)

Vea un ejemplo para comprender esta configuración. Supongamos que crea un informe de cohorte con una `Revenue` métrica por `Customer's registration date`. También quería usar la perspectiva `Average value per cohort member` para ver los ingresos por comprador con el tiempo. Para encontrar el valor medio por comprador, debes decidir el número de compradores por los que dividir. ¿Es el número de clientes registrados en su `customers` , o es el número de compradores diferentes en su `orders table` para el mismo periodo?

Esta configuración responde a esa pregunta. Recuento de miembros en la `customers` La tabla incluye todos los clientes (independientemente de si han realizado una compra o no) en la media. Recuento de miembros en la `orders` La tabla solo incluye los clientes que han realizado una compra.

#### Selección de una perspectiva {#perspective}

Una vez definida la métrica y cómo desea analizarla, puede seleccionar el `perspective` que desee utilizar.

Justo encima de la visualización del informe hay un menú desplegable de `perspective` configuración.

Consulte [Perspectivas](#perspectives).

![](../../assets/Cohort_Perspective_Menu.png)

## Ejemplos de análisis de cohorte {#examples}

Ahora que ha pasado por cómo crear un `cohort` análisis, miren algunos ejemplos.

### Quiero saber cómo mi usuario `cohorts` están creciendo con el tiempo.

![Usuario `cohorts` crecimiento con el tiempo](../../assets/cohort1.gif)

En este ejemplo, ha analizado la variable `Revenue` métrica, agrupó las cohortes por el `customer's first order date`y seleccionó los 8 más recientes `cohorts` (definido en la variable `Time Period` menú) para incluir en el análisis. Para ver cómo crecieron las cohortes con el tiempo, utilizó el `Cumulative Average Value per Cohort Member` `perspective`.

### Quiero saber, en promedio, cuántos pedidos hace un usuario en diferentes momentos de su vida.

(../../assets/cohort2.gif

Para este ejemplo, ha analizado el `Number of orders` métrica, agrupó las cohortes por el `customer's first order date`e incluyó las ocho cohortes más recientes (definidas en la `Time Period` menú) en el análisis. Para ver el número promedio de pedidos de cada cohorte, ha cambiado la variable `perspective` hasta `Average Value per Cohort Member`.

### Quiero comprender cómo se compara la actividad de compra futura de un usuario con la actividad de su primer mes con la empresa.

![Comparación de la actividad de compra futura de un usuario con su primer mes de actividad](../../assets/cohort3.gif)

## `Perspectives` {#perspectives}

`Standard`
Esto muestra la contribución incremental de un grupo de cohortes determinado en cualquier punto de su ciclo de vida. (ejemplo: el punto &quot;Semana 6&quot; muestra todos los puntos de datos obtenidos por los usuarios en su sexta semana.)

`Average Value per Cohort Member`
Esto divide el `Standard cohort` análisis en (1) por el número de usuarios en cada `cohort` grupo. Esto puede resultar útil para comparar el rendimiento de las cohortes en función de manzanas, ya que es posible que no todos los grupos de cohortes incluyan el mismo número de usuarios. Por ejemplo, el promedio de ingresos por semana de 6 por usuario de un determinado `cohort`.

`Cumulative`
Esta `perspective` muestra la tradicional `cohort` análisis en un `cumulative` base. En otras palabras, muestra la contribución total de una cohorte determinada hasta la fecha en cualquier punto de su ciclo de vida. Por ejemplo, los ingresos acumulados después de seis semanas de usuarios de una cohorte determinada.

`Cumulative Average Value per Cohort Member`
Esto divide el `Cumulative` análisis en (3) por el número de usuarios en cada `cohort` grupo. Muestra la contribución media a lo largo de la vida útil (a menudo, los ingresos medios a lo largo de la vida útil) por `cohort` miembro en cada periodo de la `cohort's` la vida. Por ejemplo, los ingresos promedio por duración después de seis meses de usuarios que se unieron en junio.

`Percent of First Value (show first value)`
Esto analiza el acumulado `cohort` contribución en un momento específico en un `cohort's` ciclo de vida como porcentaje de su contribución en el primer período. Por ejemplo, los ingresos del mes 6 divididos por los ingresos del mes 1 de los usuarios que se unieron en junio.

`Percent of First Value (hide first value)`
Esto es lo mismo que el `perspective` arriba, excepto que el primer valor de período de tiempo de 100% está oculto.

## Ajuste {#finish}

El `Cohort Report Builder` está optimizado para agrupar usuarios por un `cohort date`. Puede que le interese agrupar los usuarios por una actividad o atributo similar. El Adobe recomienda desprotegerse [este tutorial sobre cohortes cualitativas](../dev-reports/create-qual-cohort-analysis.md) para empezar.
