---
title: Elija un Report Builder
description: Aprenda a elegir su Report Builder.
exl-id: ec4204ef-975e-45c3-b09e-fb97ffc2c497
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Reports, Data Integration
TQID: https://experienceleague.adobe.com/xXSDN9dKTWp8SdeZHBmDYZhnNbxn8F-D6UvKa4qJlCI
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
source-git-commit: db7e4a13f32f02292f9c33d8d7d942461fea4bb4
workflow-type: tm+mt
source-wordcount: 644
ht-degree: 0%

---

# Elija un Report Builder

>[!NOTE]
>>Requiere [permisos de administrador](../../administrator/user-management/user-management.md).

Ahora que tiene más opciones para crear análisis, a veces es difícil saber con exactitud qué sabor del Report Builder se adapta a sus necesidades. Este tema le guía a través de la elección de la mejor manera de generar su análisis.

## ¿Cuándo debo usar [!DNL SQL Report Builder]? {#whensql}

Observe algunas de las razones más comunes por las que usaría el [!DNL SQL Report Builder] sobre el [!DNL traditional Report Builder].

### Si desea usar funciones específicas de [!DNL SQL]...

Parte de la ventaja de [!DNL SQL Report Builder] es que le permite utilizar funciones que actualmente no están disponibles en Data Warehouse Manager. En el pasado, es posible que un analista haya tenido que intervenir para ayudarle a hacer realidad su visión.

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

Si desea probar diferentes técnicas y estrategias para averiguar cuál funciona mejor para su análisis, puede que desee utilizar el [!DNL SQL Report Builder]. La creación de columnas en el Administrador de Data Warehouse lleva tiempo y las columnas que se crean con el DWM dependen de los ciclos de actualización.

En el mejor de los casos, debe esperar a través de un ciclo de actualización antes de poder utilizar la columna. Si se da cuenta de que ha cometido un error al crear la columna, tiene que esperar *dos* ciclos: uno para rellenar inicialmente la columna y otro ciclo para que las revisiones se propaguen.

### Si solo usa una columna nueva una vez...

Como se ha mencionado en la sección anterior, la creación de una columna en el Administrador de Data Warehouse lleva tiempo. Si solo planea usar una columna que creó en un informe, Adobe sugiere usar el [!DNL SQL Report Builder]. Esto elimina la necesidad de esperar a que se complete un ciclo de actualización, lo que le permite volver al trabajo más rápidamente.

### Si está trabajando con datos que tienen una relación &quot;uno a varios&quot;...

En ocasiones, la estructura de los datos podría hacer que [!DNL SQL Report Builder] sea una opción más lógica y eficaz para generar el análisis. La creación de columnas para relaciones uno a uno es sencilla en Data Warehouse Manager, pero las cosas pueden resultar un poco confusas cuando se trata de relaciones uno a varios.

Supongamos que un solo producto se considera parte de varias categorías de productos y que desea ver los ingresos asociados con cada categoría de cada producto. Intentar crear esta relación con el DWM puede ser tedioso y difícil, pero escribir una consulta [!DNL SQL] puede ser un poco más sencillo:

![Consulta SQL que muestra los ingresos por categoría de producto con relaciones &quot;uno a varios&quot;](../../assets/When_should_I_use_the_RB_2.png)

## ¿Cuándo debo usar la versión tradicional de Report Builder? {#whentraditionalrb}

Aunque [!DNL SQL Report Builder] le proporciona más control y acceso a funciones que antes no estaban disponibles, puede que no siempre sea la opción correcta. Adobe le sugiere que, a la hora de decidir qué tipo de Report Builder utilizar, tenga en cuenta lo siguiente.

### Si está creando un informe simple...

Si lo que desea crear es sencillo, el uso de la Report Builder tradicional puede ser mucho más rápido que escribir una consulta [!DNL SQL] completa. Ayuda si alguna de las columnas que necesita para crear el análisis ya está en el Administrador de Data Warehouse.

### Si comparte su trabajo con otros usuarios...

¿Los usuarios de su organización utilizan o ven este análisis? En función de con quién comparta su trabajo, puede que a veces sea mejor seguir usando Visual Report Builder. Los usuarios pueden ver rápidamente la definición de [!DNL Visual Report Builder] en lugar de leer una consulta [!DNL SQL] potencialmente larga.

Si hay algunas personas que necesitan el informe pero no están familiarizadas con [!DNL SQL], Adobe sugiere utilizar el sabor original de Report Builder. Les facilita las cosas.

## Ajuste {#wrapup}

Tanto [!DNL SQL Report Builder] como [!DNL Visual Report Builder] son adecuados para una amplia variedad de casos de uso. Esto suele depender de cuáles sean sus necesidades analíticas y quién esté consumiendo el análisis.
