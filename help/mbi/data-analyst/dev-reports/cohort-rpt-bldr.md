---
title: Report Builder de cohorte
description: Obtenga información acerca del análisis de grupos de usuarios que comparten características similares a lo largo de sus ciclos de vida.
exl-id: d80c5389-7256-40e0-86e0-49903113f93d
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '1569'
ht-degree: 0%

---

# Report Builder de cohorte

¿Alguna vez ha querido estudiar cómo se comportan los distintos subconjuntos de los usuarios a lo largo del tiempo? Por ejemplo, ¿se ha preguntado alguna vez si los usuarios que se registran durante un periodo de promoción tienen unos ingresos medios a largo plazo más altos que los que no lo tienen? Si la respuesta es `Yes`, entonces `Cohort Report Builder` es la herramienta perfecta para usted. [!DNL Adobe Commerce Intelligence] está optimizado para realizar este análisis y hacerlo relevante para su negocio.

## ¿Qué es el análisis de cohorte? {#what}

El análisis `Cohort` se puede definir, en términos generales, como el análisis de grupos de usuarios que comparten características similares a lo largo de sus ciclos de vida. Permite identificar tendencias de comportamiento entre diferentes grupos de usuarios.

Para obtener un manual detallado sobre el análisis de `cohort`, revise [esta página](https://www.cohortanalysis.com/).

En su tablero [!DNL Commerce Intelligence], es fácil crear el usuario `cohorts` en función de una fecha `cohort` y una métrica en su cuenta.

## Bueno, ¿por qué es importante el análisis de cohorte? {#important}

Como se mencionó anteriormente, el análisis `cohort` le permite identificar tendencias de comportamiento entre diferentes grupos de usuarios. Con una sólida comprensión de cómo se comportan ciertos grupos, puede adaptar sus decisiones y gastos para maximizar sus ventas. Por ejemplo, realice un análisis de ingresos `cohort` de por vida: aunque este tipo de análisis es beneficioso por muchas razones, lo inmediato son mejores decisiones de adquisición de clientes.

## ¿Cómo creo mi propio análisis de `cohort`?

### Nueva arquitectura

Estas son las instrucciones para usar `Cohort Report Builder` en la [nueva arquitectura](../../administrator/account-management/new-architecture.md).

1. Haga clic en **[!UICONTROL Report Builder]** en la ficha izquierda o en **[!UICONTROL Add Report** > **Create Report]** en cualquier panel.

1. En la pantalla de selección `Report Builder`, haga clic en **[!UICONTROL Create Report]** junto a la opción `Visual Report Builder`.

**Agregando una métrica**

Ahora que se encuentra en `Report Builder`, agregue la métrica en la que desea realizar el análisis (por ejemplo: `Revenue` o `Orders`).

>[!NOTE]
>
>Las métricas nativas [!DNL Google Analytics] no son compatibles con `Cohort Report Builder`.

**Cambiar la vista de métrica a`Cohort`**

![](../../assets/visual-report-builder-cohort-toggle.png)

Esto abre una nueva ventana para configurar los detalles del informe `Cohort`.

### Se necesitan cinco especificaciones para generar un informe de `Cohort`:

1. Cómo agrupar `cohorts`
1. El período de tiempo `cohort`
1. Número de `cohorts` que se van a ver
1. Cantidad mínima de datos que debe contener cada `cohort`
1. Intervalo de tiempo después de `cohort` ocurrencia

#### 1. Agrupación `cohorts`

`Cohorts` se agrupan por una marca de tiempo, como **fecha de registro** o **fecha del primer pedido**.

>[!NOTE]
>
>No puede usar la misma marca de tiempo en la que está generada la métrica para la fecha `cohort`. Para un análisis que requiera esto, puede usar `Standard report builder` en su lugar.

#### 2. Período de tiempo de `Cohort`

Elija el período de tiempo para agrupar `cohorts` por. En otras palabras, ¿qué parte de la marca de tiempo que seleccionó arriba es la más importante; la `week`, `month`, `quarter` o `year`? El informe muestra los datos en el intervalo que seleccione aquí

#### 3. y 4. Establezca el número de `cohorts` que desea ver y la cantidad de datos que debe tener cada `cohort`

Estos parámetros le ayudan a ver solamente los `cohorts` que le interesan, y el práctico cuadro `Preview` en la parte inferior de la ventana le muestra exactamente qué cohortes se muestran en el informe.

De manera predeterminada, el objeto `cohort` actual no se incluye a menos que cambie la cantidad mínima de datos necesarios para cada `cohort` a `0`. En este caso, `cohort` para el período de tiempo actual solo incluye datos parciales.

#### 5. Intervalo De Tiempo Después De `Cohort` Ocurrencia

Esta característica le permite establecer el intervalo de tiempo de los datos que visualiza para el(la) `cohorts` seleccionado(a). Por ejemplo, si desea ver 24 `cohorts` mensuales basados en `customer's first order date`, pero sólo está interesado en los primeros 3 meses de datos para cada `cohort`, puede establecer `number of cohorts to view` en `24` y `time range after cohort occurrence` en `3`.

El intervalo de este valor cambia independientemente de lo que haya seleccionado en `cohort time period` y el valor se establece en `12` de forma predeterminada; el valor no cambia a menos que haga clic en el icono del calendario para editarlo.

![](../../assets/cohort-time-range.png)

#### Otras notas

* [!UICONTROL Filters]: las métricas aplicadas permanecen intactas cuando cambia entre las vistas `Standard` y `Cohort`.

* Ver [`Perspectives`](#perspectives).

#### Ejemplo

Aquí tiene un ejemplo para unirlo todo. En este ejemplo, deseo comprobar el comportamiento de los pedidos después de la primera compra de un(a) `cohort` para ver si esa cohorte regresa para realizar compras repetidas en los próximos seis meses.

![Cohorte de pedidos](../../assets/crb_example.gif)

### Arquitectura heredada

#### Arquitectura heredada {#personalinfo}

A continuación se proporcionan instrucciones específicas para la versión heredada de `Cohort Report Builder`. Si está interesado en usar la nueva versión, consulte [Nueva arquitectura](../../administrator/account-management/new-architecture.md) para obtener más información sobre cómo migrar a una cuenta de [!DNL Commerce Intelligence] Nueva arquitectura.

#### ¿Cómo creo mi propio análisis de `cohort`? {#create}

![](../../assets/create-cohort-analysis.png)

Análisis `Cohort` en acción. Aquí puede ver el crecimiento de los ingresos a lo largo del tiempo de forma acumulativa y por usuario.

Esta sección le guiará en la creación de su propio análisis de `cohort`. Para ver ejemplos (y GIF animados que muestran el proceso), vea la [sección de ejemplos](#examples) de este tema.

1. Haga clic en **[!UICONTROL Report Builder]** en la ficha izquierda o en **[!UICONTROL Add Report** > **Create Report]** en cualquier panel.

1. En la pantalla `Report Builder Selection`, haga clic en **[!UICONTROL Create Report]** junto a la opción `Cohort Analysis`.

#### Adición de una métrica

Ahora que se encuentra en `Cohort Report Builder`, agregue la métrica (por ejemplo: `Revenue` o `Number of orders`) en la que desea realizar el análisis.

>[!NOTE]
>
>Las métricas nativas [!DNL Google Analytics] no son compatibles con `Cohort Report Builder`.

#### Selección de la fecha de cohorte {#date}

El siguiente paso es especificar `cohort date`. Es la fecha en la que se agrupan los usuarios. Por ejemplo, podría ser `User's first order date` o `User's registration date`.

>[!NOTE]
>
>No puede usar la misma fecha en la que se creó la métrica (ejemplo: `created at`) que `cohort date`.

#### Configuración del intervalo y el período de tiempo

A continuación, establezca `Interval` y `Time Period`.

`Interval`
La opción `Interval` le permite establecer `length` de su `cohorts`. Por ejemplo, si se establece en `Month`, el informe se mide en meses.

Puede cambiar la forma en que se muestran estos intervalos en el eje x mediante el menú **Duración**.

`Time Period`
Utilice el menú `Time Period` para elegir el usuario específico `cohorts` que desea analizar. Puede mostrar cada `cohort`, elegir de una lista, especificar un intervalo de tiempo o definir un intervalo de tiempo móvil de `cohorts` para incluir. Por ejemplo, si utilizó la opción `Specific Cohorts`, puede seleccionar meses específicos para incluirlos en el análisis:

![Usando el menú `Time Period` para agregar `Cohorts`](../../assets/Cohort_Time_Period.gif) específico

Si está agrupando `cohorts` por fecha de registro y después seleccionó abril, mayo y junio en la lista `Specific Cohorts`, se incluirán todos los usuarios que se registraron en esos meses.

#### Definición del eje X

En `duration`, puede definir la configuración del eje X del gráfico. Es decir, cuántos periodos de tiempo representa cada punto de datos y cuántos puntos de datos incluir en el análisis.

#### Seleccionando la tabla `counting members`

Si optó por agrupar usuarios por un(a) `cohort date` que se ha unido desde otra tabla, es posible que vea una opción `counting members in the … table`.

![](../../assets/Cohort_Counting_Members_option.png)

Vea un ejemplo para comprender esta configuración. Supongamos que creó un informe que cohorta una métrica de `Revenue` por `Customer's registration date`. También quisiste usar la perspectiva `Average value per cohort member` para ver los ingresos por comprador a lo largo del tiempo. Para encontrar el valor medio por comprador, debes decidir el número de compradores por los que dividir. ¿Es el número de clientes registrados en su tabla `customers` o es el número de compradores diferentes en su `orders table` durante el mismo período?

Esta configuración responde a esa pregunta. El recuento de miembros en la tabla `customers` incluye a todos los clientes (independientemente de si realizaron una compra o no) en el promedio. El recuento de miembros en la tabla `orders` incluye solamente los clientes que realizaron una compra.

#### Selección de una perspectiva {#perspective}

Una vez que haya definido la métrica y la forma en que desea analizarla, puede seleccionar el `perspective` que desee utilizar.

Justo encima de la visualización del informe hay un menú desplegable de `perspective` configuraciones.

Ver [perspectivas](#perspectives).

![](../../assets/Cohort_Perspective_Menu.png)

## Ejemplos de análisis de cohorte {#examples}

Ahora que ha visto cómo crear un análisis de `cohort`, vea algunos ejemplos.

### Quiero saber cómo está creciendo mi usuario `cohorts` con el paso del tiempo.

![Usuario `cohorts` creciendo con el tiempo](../../assets/cohort1.gif)

En este ejemplo, ha analizado la métrica `Revenue`, ha agrupado las cohortes por el `customer's first order date` y ha seleccionado los 8 `cohorts` más recientes (definidos en el menú `Time Period`) para incluirlos en el análisis. Para ver el crecimiento de las cohortes con el paso del tiempo, utilizó `Cumulative Average Value per Cohort Member` `perspective`.

### Quiero saber, en promedio, cuántos pedidos hace un usuario en diferentes momentos de su vida.

(../../assets/cohort2.gif

Para este ejemplo, ha analizado la métrica `Number of orders`, ha agrupado las cohortes por el `customer's first order date` y ha incluido las ocho cohortes más recientes (definidas en el menú `Time Period`) en el análisis. Para ver el número promedio de pedidos de cada cohorte, cambió `perspective` a `Average Value per Cohort Member`.

### Quiero comprender cómo se compara la actividad de compra futura de un usuario con la actividad de su primer mes con la empresa.

![Comparando la actividad de compra futura de un usuario con su primer mes de actividad](../../assets/cohort3.gif)

## `Perspectives` {#perspectives}

`Standard`
Esto muestra la contribución incremental de un grupo de cohortes determinado en cualquier punto de su ciclo de vida. (ejemplo: el punto &quot;Semana 6&quot; muestra todos los puntos de datos obtenidos por los usuarios en su sexta semana.)

`Average Value per Cohort Member`
Esto divide el análisis `Standard cohort` en (1) por el número de usuarios en cada grupo `cohort`. Esto puede resultar útil para comparar el rendimiento de las cohortes en función de manzanas, ya que es posible que no todos los grupos de cohortes incluyan el mismo número de usuarios. Por ejemplo, el promedio de ingresos por semana de 6 por usuario de un(a) determinado(a) `cohort`.

`Cumulative`
Este(a) `perspective` muestra el análisis tradicional `cohort` en base a `cumulative`. En otras palabras, muestra la contribución total de una cohorte determinada hasta la fecha en cualquier punto de su ciclo de vida. Por ejemplo, los ingresos acumulados después de seis semanas de usuarios de una cohorte determinada.

`Cumulative Average Value per Cohort Member`
Esto divide el análisis `Cumulative` en (3) por el número de usuarios en cada grupo `cohort`. Muestra la contribución promedio de duración (a menudo los ingresos promedio de duración) por miembro de `cohort` en cada período de la vida de `cohort's`. Por ejemplo, los ingresos promedio por duración después de seis meses de usuarios que se unieron en junio.

`Percent of First Value (show first value)`
Analiza la contribución agregada de `cohort` en un momento específico de un ciclo de vida de `cohort's` como porcentaje de su contribución en el primer período. Por ejemplo, los ingresos del mes 6 divididos por los ingresos del mes 1 de los usuarios que se unieron en junio.

`Percent of First Value (hide first value)`
Esto es lo mismo que el `perspective` anterior, excepto que el primer valor de período de tiempo del 100% está oculto.

## Ajuste {#finish}

`Cohort Report Builder` está optimizado para agrupar usuarios por un elemento común `cohort date`. Puede que le interese agrupar los usuarios por una actividad o atributo similar. El Adobe recomienda desproteger [este tutorial sobre cohortes cualitativas](../dev-reports/create-qual-cohort-analysis.md) para comenzar.
