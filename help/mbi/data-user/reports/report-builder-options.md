---
title: Elija un Report Builder
description: Aprenda a elegir su Report Builder.
exl-id: ec4204ef-975e-45c3-b09e-fb97ffc2c497
role: Admin, Data Architect, Data Engineer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
source-git-commit: 6e2f9e4a9e91212771e6f6baa8c2f8101125217a
workflow-type: tm+mt
source-wordcount: '634'
ht-degree: 0%

---

# Elija un Report Builder

>[!NOTE]
>&#x200B;>Requiere [permisos de administrador](../../administrator/user-management/user-management.md).

Ahora que tiene más opciones para crear análisis, a veces es difícil saber con exactitud qué sabor del Report Builder se adapta a sus necesidades. Este tema le guía a través de la elección de la mejor manera de generar su análisis.

## ¿Cuándo debo usar [!DNL SQL Report Builder]? {#whensql}

Observe algunas de las razones más comunes por las que usaría el [!DNL SQL Report Builder] sobre el [!DNL traditional Report Builder].

### Si desea usar funciones específicas de [!DNL SQL]...

Parte de la ventaja de [!DNL SQL Report Builder] es que le permite utilizar funciones que actualmente no están disponibles en el Administrador de Datas Warehouse. En el pasado, es posible que un analista haya tenido que intervenir para ayudarle a hacer realidad su visión.

[!DNL SQL Report Builder] admite funciones como [`LISTAGG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LISTAGG.html) y [`GETDATE`](https://docs.aws.amazon.com/redshift/latest/dg/r_GETDATE.html), que no se podían usar anteriormente. Puede obtener acceso a [`full list`](https://docs.aws.amazon.com/redshift/latest/dg/c_SQL_functions.html), pero algunas otras funciones específicas de SQL incluyen:

* [`Bitwise aggregate` funciones](https://docs.aws.amazon.com/redshift/latest/dg/c_bitwise_aggregate_functions.html)
* [`CASE expression`](https://docs.aws.amazon.com/redshift/latest/dg/r_CASE_function.html)
* [`JSON_EXTRACT_PATH_TEXT`](https://docs.aws.amazon.com/redshift/latest/dg/JSON_EXTRACT_PATH_TEXT.html)
* [`LOG`](https://docs.aws.amazon.com/redshift/latest/dg/r_LOG.html)
* [`MONTHS_BETWEEN`](https://docs.aws.amazon.com/redshift/latest/dg/r_MONTHS_BETWEEN_function.html)
* [`REPLACE`](https://docs.aws.amazon.com/redshift/latest/dg/r_REPLACE.html)
* [`SQRT`](https://docs.aws.amazon.com/redshift/latest/dg/r_SQRT.html)
* Operador [`concatenation`](https://docs.aws.amazon.com/redshift/latest/dg/r_concat_op.html)

### Si quieres hacer algunas pruebas...

Si desea probar diferentes técnicas y estrategias para averiguar cuál funciona mejor para su análisis, puede que desee utilizar el [!DNL SQL Report Builder]. La creación de columnas en el Administrador de Datas Warehouse lleva tiempo y las columnas que se crean con el DWM dependen de los ciclos de actualización.

En el mejor de los casos, debe esperar a través de un ciclo de actualización antes de poder utilizar la columna. Si se da cuenta de que ha cometido un error al crear la columna, tiene que esperar *dos* ciclos: uno para rellenar inicialmente la columna y otro ciclo para que las revisiones se propaguen.

### Si solo usa una columna nueva una vez...

Como se ha mencionado en la sección anterior, la creación de una columna en el Administrador de Datas Warehouse lleva tiempo. Si solo planea usar una columna que creó en un informe, el Adobe sugiere usar [!DNL SQL Report Builder]. Esto elimina la necesidad de esperar a que se complete un ciclo de actualización, lo que le permite volver al trabajo más rápidamente.

### Si está trabajando con datos que tienen una relación &quot;uno a varios&quot;...

En ocasiones, la estructura de los datos podría hacer que [!DNL SQL Report Builder] sea una opción más lógica y eficaz para generar el análisis. La creación de columnas para relaciones uno a uno es sencilla en el Administrador de Datas Warehouse, pero las cosas pueden resultar un poco confusas cuando se trata de relaciones uno a varios.

Supongamos que un solo producto se considera parte de varias categorías de productos y que desea ver los ingresos asociados con cada categoría de cada producto. Intentar crear esta relación con el DWM puede ser tedioso y difícil, pero escribir una consulta [!DNL SQL] puede ser un poco más sencillo:

![](../../assets/When_should_I_use_the_RB_2.png)

## ¿Cuándo debo usar el Report Builder tradicional? {#whentraditionalrb}

Aunque [!DNL SQL Report Builder] le proporciona más control y acceso a funciones que antes no estaban disponibles, puede que no siempre sea la opción correcta. El Adobe sugiere que, a la hora de decidir qué tipo de Report Builder utilizar, tenga en cuenta lo siguiente.

### Si está creando un informe simple...

Si lo que desea crear es sencillo, el uso del Report Builder tradicional puede ser mucho más rápido que escribir una consulta [!DNL SQL] completa. Ayuda si alguna de las columnas que necesita para crear el análisis ya está en el Administrador de Datas Warehouse.

### Si comparte su trabajo con otros usuarios...

¿Los usuarios de su organización utilizan o ven este análisis? Dependiendo de con quién comparta su trabajo, puede que a veces sea mejor quedarse con el Report Builder visual. Los usuarios pueden ver rápidamente la definición de [!DNL Visual Report Builder] en lugar de leer una consulta [!DNL SQL] potencialmente larga.

Si hay algunas personas que necesitan el informe pero no están familiarizadas con [!DNL SQL], el Adobe sugiere utilizar el sabor original del Report Builder. Les facilita las cosas.

## Ajuste {#wrapup}

Tanto [!DNL SQL Report Builder] como [!DNL Visual Report Builder] son adecuados para una amplia variedad de casos de uso. Esto suele depender de cuáles sean sus necesidades analíticas y quién esté consumiendo el análisis.
