---
title: Elija un Report Builder
description: Aprenda a elegir su Report Builder.
exl-id: ec4204ef-975e-45c3-b09e-fb97ffc2c497
source-git-commit: 14777b216bf7aaeea0fb2d0513cc94539034a359
workflow-type: tm+mt
source-wordcount: '724'
ht-degree: 0%

---

# Elija un Report Builder

>[!NOTE]
>>Requiere [Permisos de administración](../../administrator/user-management/user-management.md).


Ahora que tiene más opciones para crear análisis, a veces es difícil saber con exactitud qué sabor del Report Builder se adapta a sus necesidades. Este artículo le guía a través de la elección de la mejor manera de generar su análisis.

## ¿Cuándo debo usar el `SQL Report Builder`? {#whensql}

Observe algunas de las razones más comunes por las que utilizaría el Report Builder SQL sobre el Report Builder tradicional.

### Si desea utilizar funciones específicas de SQL...

Parte de la belleza de la `SQL Report Builder` es que le permite utilizar funciones que actualmente no están disponibles en el Administrador de Datas Warehouse. En el pasado, es posible que un analista haya tenido que intervenir para ayudarle a hacer realidad su visión.

El Report Builder SQL admite funciones como [`LISTAGG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LISTAGG.html) y [`GETDATE`](https://docs.aws.amazon.com/redshift/latest/dg/r_GETDATE.html), que no se podía usar anteriormente. Puede acceder a las [`full list`](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html), pero algunas otras funciones específicas de SQL incluyen:

* [`Bitwise aggregate` Funciones](https://docs.aws.amazon.com/redshift/latest/dg/c_bitwise_aggregate_functions.html)
* [`CASE expression`](https://docs.aws.amazon.com/redshift/latest/dg/r_CASE_function.html)
* [`JSON_EXTRACT_PATH_TEXT`](https://docs.aws.amazon.com/redshift/latest/dg/JSON_EXTRACT_PATH_TEXT.html)
* [`LOG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LOG.html)
* [`MONTHS_BETWEEN`](https://docs.aws.amazon.com/redshift/latest/dg/r_MONTHS_BETWEEN_function.html)
* [`REPLACE`](https://docs.aws.amazon.com/redshift/latest/dg/r_REPLACE.html)
* [`SQRT`](https://docs.aws.amazon.com/redshift/latest/dg/r_SQRT.html)
* [`concatenation` operador](https://docs.aws.amazon.com/redshift/latest/dg/r_concat_op.html)

### Si quieres hacer algunas pruebas...

Si desea probar diferentes técnicas y estrategias para averiguar qué es lo que mejor funciona para el análisis, puede utilizar la variable `SQL Report Builder`. La creación de columnas en el Administrador de Datas Warehouse lleva tiempo y las columnas que se crean con el DWM dependen de los ciclos de actualización.

En el mejor de los casos, debe esperar a través de un ciclo de actualización antes de poder utilizar la columna. Si se da cuenta de que ha cometido un error al crear la columna, debe esperar *dos* ciclos: uno para rellenar inicialmente la columna y otro para que las revisiones se propaguen.

### Si solo usa una columna nueva una vez...

Como se ha mencionado en la sección anterior, la creación de una columna en el Administrador de Datas Warehouse lleva tiempo. Si solo planea utilizar una columna que crea en un informe, el Adobe sugiere utilizar la variable `SQL Report Builder`. Esto elimina la necesidad de esperar a que se complete un ciclo de actualización, lo que le permite volver al trabajo más rápidamente.

### Si está trabajando con datos que tienen una relación &quot;uno a varios&quot;...

A veces, la estructura de los datos puede hacer que la variable `SQL Report Builder` una opción más eficiente y lógica para crear su análisis. La creación de columnas para relaciones uno a uno es sencilla en el Administrador de Datas Warehouse, pero las cosas pueden resultar un poco confusas cuando se trata de relaciones uno a varios.

Supongamos que un solo producto se considera parte de varias categorías de productos y que desea ver los ingresos asociados con cada categoría de cada producto. Intentar crear esta relación con el DWM puede ser tedioso y difícil, pero escribir una consulta SQL puede ser un poco más sencillo:

![](../../assets/When_should_I_use_the_RB_2.png)

## ¿Cuándo debo usar el Report Builder tradicional? {#whentraditionalrb}

Mientras que el `SQL Report Builder` le proporciona más control y acceso a funcionalidades que antes no estaban disponibles, por lo que es posible que no siempre sea la opción correcta. El Adobe sugiere que, a la hora de decidir qué tipo de Report Builder utilizar, tenga en cuenta lo siguiente.

### Si está creando un informe simple...

Si lo que desea crear es sencillo, utilizar el Report Builder tradicional puede ser mucho más rápido que escribir una consulta SQL completa. Ayuda si alguna de las columnas que necesita para crear el análisis ya está en el Administrador de Datas Warehouse.

### Si comparte su trabajo con otros usuarios...

¿Los usuarios de su organización utilizan o ven este análisis? Dependiendo de con quién comparta su trabajo, puede que a veces sea mejor quedarse con el Report Builder visual. Los usuarios pueden ver rápidamente la definición en el Report Builder visual en lugar de leer una consulta SQL potencialmente larga.

Si hay algunas personas que necesitan el informe pero no están familiarizadas con SQL, el Adobe sugiere utilizar el sabor original del Report Builder. Les facilita las cosas.

## Ajuste {#wrapup}

Tanto la `SQL Report Builder` y `Visual Report Builder` son adecuados para una amplia variedad de casos de uso. Esto suele depender de cuáles sean sus necesidades analíticas y quién esté consumiendo el análisis.