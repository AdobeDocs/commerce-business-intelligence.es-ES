---
title: Optimización de la base de datos para análisis
description: Aprenda a optimizar la base de datos para realizar análisis.
exl-id: e73e1a1e-c933-476d-97bc-bd8f52bb2fa1
role: Admin, Data Architect, Data Engineer, User
feature: Business Performance, Data Integration, Data Import/Export, Data Warehouse Manager
source-git-commit: adb7aaef1cf914d43348abf5c7e4bec7c51bed0c
workflow-type: tm+mt
source-wordcount: '864'
ht-degree: 0%

---

# Optimización de la base de datos

La ventaja principal de utilizar una base de datos operativa para [!DNL Adobe Commerce Intelligence] es que no es necesario generar ni modificar nada para recopilar datos. Información valiosa ya está allí, solo tiene que desbloquearla.

Este tema contiene algunas recomendaciones para ayudarle a optimizar la base de datos para el análisis y extraer perspectivas procesables de los datos sin procesar.

## No eliminar datos

>[!TIP]
>
>Las leyes locales e internacionales que afectan su negocio (y sus propios términos de servicio) pueden afectar a qué tipos de datos puede conservar y durante cuánto tiempo. El cumplimiento de estas leyes debería ser su prioridad.

Cuando se cancela un pedido, un usuario desactiva su cuenta o se interrumpe un producto, es tentador eliminar la información asociada en la base de datos. Las mesas crecen y eliminar el desorden parece una idea prudente. Sin embargo, eliminar filas significa que esta información se pierde para siempre o que necesita explorar las copias de seguridad antiguas para encontrarla.

En su lugar, puede agregar una columna de estado a la tabla que indique cuándo la fila ya no está activa o es relevante. También se recomienda agregar una columna que almacene la fecha en la que se realizó el cambio o crear un registro para los cambios históricos. Si las tablas crecen lo suficiente como para que el rendimiento empiece a verse afectado, considere la posibilidad de archivar los datos antiguos en una tabla utilizada para el análisis.

## Sobrescribir datos con poca frecuencia

La sobrescritura de datos debe realizarse con moderación y precaución.

Si utilizamos las fechas de inicio de sesión como ejemplo, muchas empresas almacenan la fecha del último inicio de sesión en lugar de una tabla de inicios de sesión históricos. Aunque es posible que solo necesite la última fecha de inicio de sesión con fines funcionales, los datos sobrescritos suponen una gran pérdida desde el punto de vista del análisis. Al no mantener un registro completo de estas acciones, se elimina la capacidad de ver cuántos usuarios permanecieron fuera durante largos períodos de tiempo y, a continuación, se reactivaron. También hace imposible crear cosas como análisis de cohortes de participación de usuarios basados en inicios de sesión.

Por lo general, si actualiza un registro debido a algún tipo de acción del usuario, no sobrescriba la información sobre una acción anterior o independiente del usuario.

## Incluir `Updated_at` columnas para datos actualizados con el paso del tiempo

Si las filas de una tabla van a tener valores que cambian con el tiempo, por ejemplo, **order\_status** cambia de`processing` a `complete`, incluya una columna **updated\_at** para registrar cuándo se produce el cambio más reciente. Asegúrese de que haya un valor **updated\_at** disponible la primera vez que inserte la nueva fila de datos, cuando la fecha **updated\_at** corresponda a la fecha **created\_at**.

Además de optimizar para el análisis, las columnas **updated\_at** también le permiten utilizar [métodos de replicación incremental](../data-analyst/data-warehouse-mgr/cfg-replication-methods.md), que pueden ayudarle a acortar la duración de sus ciclos de actualización.

## Source de adquisición de usuarios de tienda

Uno de los errores más comunes es que [user acquisition source](../data-analyst/analysis/google-track-user-acq.md) (UAS) no está almacenada en la base de datos operativa. En la mayoría de los casos, cuando esto es un problema, UAS solo se rastrea a través de [!DNL Google Analytics] o alguna otra herramienta de análisis web. Aunque estas herramientas pueden ser útiles, el almacenamiento exclusivo de UAS en ellas presenta algunos inconvenientes; por ejemplo, no es posible extraer datos de nivel de usuario de estas herramientas. Cuando es posible, suele ser un proceso difícil. Debería ser fácil obtener esta información y combinarla con datos de otras fuentes, como la información de comportamiento y transaccional que también se almacena en la base de datos.

El almacenamiento de UAS en su propia base de datos es a menudo la mayor mejora que un negocio en línea puede hacer a sus capacidades analíticas. Esto permite a UAS analizar las ventas, la participación del usuario, los períodos de devolución, el valor de duración del cliente, la pérdida y otras métricas críticas. [Estos datos son cruciales para decidir dónde invertir los recursos de marketing](../data-analyst/analysis/most-value-source-channel.md).

Demasiadas empresas se centran únicamente en encontrar canales que proporcionen nuevos usuarios al menor coste. Si no realiza el seguimiento de la calidad de los usuarios adquiridos en cada canal, corre el riesgo de atraer usuarios que no generan valor empresarial.

## Configuración de tabla de datos

### Establecer una clave principal

Una [clave principal](https://en.wikipedia.org/wiki/Unique_key) es una columna (o conjunto de columnas) que no cambia y que produce valores únicos dentro de una tabla. Las claves principales son muy importantes, ya que garantizan que las tablas se replican correctamente en [!DNL Commerce Intelligence].

Cuando cree claves principales, utilice un tipo de datos de número entero para la columna que aumenta automáticamente. El Adobe recomienda evitar el uso de claves principales de varias columnas siempre que sea posible.

Si la tabla es una vista SQL, agregue una columna que pueda actuar como clave principal. [!DNL Commerce Intelligence] puede identificar automáticamente esta columna como clave principal.

### Asignar un tipo de datos a su columna de datos

Si una columna de datos no tiene un tipo de datos [asignado](https://en.wikipedia.org/wiki/Data_type), [!DNL Commerce Intelligence] adivina qué tipo de datos usar. Si el sistema no lo adivina correctamente, es posible que no pueda realizar los análisis relevantes hasta que el equipo de soporte de Adobe ajuste la columna al tipo de datos adecuado. Por ejemplo, si una columna de fecha se adivina como un tipo de datos numérico, puede generar tendencias a lo largo del tiempo utilizando esa dimensión de fecha.

### Agregar prefijos a las tablas de datos si tiene varias bases de datos

Si tiene más de una base de datos conectada a [!DNL Commerce Intelligence], Adobe recomienda agregar prefijos a las tablas para evitar confusiones. Los prefijos le ayudan a recordar de dónde provienen las métricas o dimensiones de datos.
