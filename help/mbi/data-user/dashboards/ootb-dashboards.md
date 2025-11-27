---
title: Paneles incluidos
description: Aprenda a comprobar el estado de las métricas esenciales, como los ingresos de por vida del usuario, la cantidad de compras repetidas y mucho más, lo que crea una base sólida para la exploración futura.
exl-id: f50fc417-e5d4-401c-9baa-cda1468196a2
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Dashboards
source-git-commit: 3a7423c9dd0f957b77baa27b3447a715caad017b
workflow-type: tm+mt
source-wordcount: '956'
ht-degree: 0%

---

# Paneles incluidos

[!DNL Adobe] ofrece `eCommerce` y `SaaS` paquetes de inicio. Estos paquetes, creados por analistas de Adobe, contienen un conjunto personalizado de paneles e informes para su conjunto de datos. Los análisis contenidos en estos paquetes le permiten comprobar el estado de las métricas esenciales, como los ingresos de por vida del usuario, el número de compras repetidas y más, lo que crea una base sólida para la exploración futura.

>[!NOTE]
>
>La disponibilidad de algunos paneles depende del conjunto de datos.

Si tiene preguntas o está interesado en agregar un paquete a su cuenta, envíe un [ticket de asistencia](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/troubleshooting/miscellaneous/mbi-service-policies.html?lang=es) para obtener ayuda.

## Información general ejecutiva

El tablero `executive overview` se ha creado a partir de gráficos de otros tableros. Este tablero es una descripción general de alto nivel de los datos y contiene gráficos que se revisarían diariamente, mientras que otros tableros contenían información más detallada. Inicialmente, se establece como el panel predeterminado en cada cuenta.

Se incluye un conjunto general de gráficos para usted. Adobe recomienda adaptar este tablero a sus necesidades añadiendo otros gráficos que utilice con más frecuencia.

## Análisis de cohorte

El panel `cohort analysis` incluye un conjunto de gráficos que muestran el crecimiento promedio de los ingresos durante toda la vida del usuario y el crecimiento de los ingresos incrementales agrupados por cohortes de registro. Esto revela si el valor de duración del cliente (LTV), el valor de un cliente para una empresa, aumenta con el tiempo y también identifica tendencias en torno al crecimiento de LTV. De manera predeterminada, *todos los usuarios registrados (compradores y no compradores) se contabilizan* en el cálculo de LTV promedio; consulte el [tema de análisis de cohorte](../../data-analyst/dev-reports/cohort-rpt-bldr.md).

Este panel también puede incluir gráficos de cohorte que analizan los ingresos de duración de los usuarios procedentes de una fuente de adquisición, canal o población específicos (por ejemplo, Nueva York o California). Esto sirve para demostrar cómo puede analizar LTV para segmentos específicos de su base de usuarios y ver si un grupo u otro genera un LTV más alto con el tiempo.

Para obtener más información sobre las cohortes, vea [Realización de análisis de cohorte](../../data-analyst/dev-reports/cohort-rpt-bldr.md).

Si actualmente no está realizando el seguimiento de la fuente de adquisición de usuarios, consulte [Seguimiento de la adquisición de usuarios en Información general de datos de Source](../../data-analyst/analysis/google-track-user-acq.md).

## Resumen de correo electrónico

El panel `Email Summary` incluye un conjunto de gráficos de ejemplo que se pueden usar en un resumen diario automatizado de correo electrónico. Consulte [creación de resúmenes de correo electrónico automatizados](../../data-user/export-data/email-summaries.md) para obtener más información sobre la configuración de resúmenes de correo electrónico.  

## Retención de mantenimiento

El panel `Retention health` revela el comportamiento de compra repetida de su base de usuarios.

El gráfico `Time between orders` muestra el tiempo promedio o la mediana transcurrido entre el primer y el segundo orden de un usuario, el segundo y el tercer orden, etc. Considere la posibilidad de utilizar estos datos para configurar sus campañas de marketing por correo electrónico.

El gráfico `Users by lifetime number of orders` enumera la cantidad total de usuarios para cada número de pedidos de por vida a fin de proporcionar una visión general del comportamiento de compra repetida.  

El gráfico `Repeat order probability` muestra la probabilidad de que un usuario con un determinado número de pedido realice una compra de forma repetida. Para ver la probabilidad de que los clientes que hicieron `x` pedidos hagan `(x+1)`, simplemente divida el número de personas que han hecho al menos `(x+1)` compras por el número de personas que han hecho al menos `x` compras.

### Ejemplo

Número de clientes que realizaron una compra en su duración: `90`

Número de clientes que realizaron dos compras en el período de duración: `30`

Número de clientes que realizaron tres compras en el período de duración: `10`

En este ejemplo, la probabilidad de que los clientes que han realizado una compra en su vida útil repitan el pedido para realizar una segunda compra es: `(30 + 10) / (30+10+90) = 30.77%`.

## Crecimiento de LTV del cliente

El panel `Customer LTV growth` incluye un conjunto de gráficos que encuentran el promedio de ingresos por usuario. Los gráficos se segmentan según los ingresos promedio que se generan en los primeros 30, 60, 90 o 365 días después del registro.  

La fila inferior de gráficos muestra que estos promedios segmentados por fuentes de adquisición o demografías para revelar qué grupos de usuarios generan la mayor cantidad de ingresos con el tiempo.

## Rendimiento del producto

El panel `Product Performance` incluye gráficos que muestran el rendimiento general del producto al mostrar el número de artículos vendidos y los ingresos por artículo, así como al identificar los productos de mayor rendimiento.

## Actividad reciente

El panel `Recent Activity` muestra datos de rendimiento de los últimos 30 días.

## Salud transaccional

El panel `Transaction Health` incluye gráficos generales de ingresos, pedidos y valor de pedido promedio. Estos gráficos pueden segmentarse por canales de marketing, datos demográficos o códigos de cupones especiales.

## Usuarios para segmentar

El panel `Users to target` incluye gráficos de estilo tabla que enumeran usuarios con comportamientos de compra específicos en común. Algunos ejemplos son:

* Lista de compradores únicos que compraron hace `X` meses (que es posible que quieras reactivar)

* Lista de los principales gastadores (que puede que desee mantener feliz)

* Lista de los principales gastadores que han estado activos en los últimos `X` días (a quienes quizá desee recompensar)

Puede utilizar las herramientas de exportación de datos para crear listas de correo electrónico de usuarios con un comportamiento de compra similar para el marketing de destino.

## Actividad del usuario

El panel `User activity` incluye gráficos que segmentan a los usuarios según varios datos, incluidos el origen de adquisición, la demografía y el promedio de la primera vez que se realiza un pedido. También incluye el análisis de cohorte de usuarios, incluidos los ingresos promedio generales por duración y por mes de registro de los usuarios.

El gráfico `% of cohort members who have purchased` es valioso, ya que muestra la proporción de conversión (de 0 a 1) de los usuarios en función del momento de registro (cada línea representa una cohorte de usuarios). También muestra cuándo realizan su primera compra (por ejemplo, en el mes 1, 2, 3... después del registro). Esto puede mostrarle que el 10% de los usuarios se activaron en el mes 1, mientras que este número crece en el mes 2, 3, 4... y puede estabilizarse más adelante.

Normalmente, las líneas de este gráfico se vuelven horizontales después de algún período de tiempo. Esto indica que pocos miembros de cohorte adicionales se están convirtiendo de forma orgánica después de ese punto: la mayoría de los usuarios que van a realizar una compra ya lo han hecho. En este punto, es muy poco probable que estos miembros se conviertan en compradores sin intervención. Ponerse en contacto con ellos mediante promociones personalizadas o correos electrónicos dirigidos es una forma de bajo riesgo de impulsar la conversión de esta población.
