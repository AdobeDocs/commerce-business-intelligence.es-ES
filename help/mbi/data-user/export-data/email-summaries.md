---
title: Crear resúmenes de correo electrónico automatizados
description: Aprenda a crear resúmenes de correo electrónico automatizados.
exl-id: a9aea4fc-9193-467f-8554-3ad77ac3fa73
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '521'
ht-degree: 0%

---

# Crear resúmenes de correo electrónico automatizados

Los resúmenes de correo electrónico son una potente herramienta de comunicación que puede utilizar para compartir el estado y las tendencias actuales de su negocio con las partes interesadas clave. Con los resúmenes de correo electrónico puede:

* Enviar por correo electrónico resúmenes gráficos que incluyan informes
* Incluya o excluya al autor del resumen de correo electrónico de la recepción del correo electrónico
* Programar cuando se envíe el correo electrónico
* Editar, eliminar y pausar resúmenes de correo electrónico programados existentes

## Crear nuevo resumen de correo electrónico

1. Haga clic en **[!DNL Manage Data]** then **[!UICONTROL Email Summary]** en la barra lateral.

   Si es la primera vez que crea un resumen por correo electrónico, esta página no muestra ningún resumen guardado.

1. Haga clic en **[!UICONTROL Create New Email Summary]** en la esquina superior derecha.

1. Introduzca un nombre para el resumen.

   Elija un nombre que transmita lo que se incluye en el resumen. Por ejemplo, `AOV Comparison`.

1. En el `Choose Content` , seleccione los informes que desee incluir en el resumen.

   Puede seleccionar hasta 10 informes de su propiedad. Después de seleccionar un informe, utilice los iconos que aparecen para seleccionar si desea que el informe se envíe como una tabla o un gráfico. Si guardó el informe como un número, solo puede enviarlo como un número. Para obtener información sobre el envío de un resumen por correo electrónico que contiene un informe con datos antiguos, consulte [Administración de la configuración de la cuenta](../../administrator/account-management/managing-account-settings.md).

   >[!NOTE]
   >
   >`Cohort` solo están disponibles si utiliza la nueva arquitectura.

1. (Opcional) Seleccione `Send Email To Me` si desea recibir el correo electrónico.

1. Para incluir a otros usuarios en el correo electrónico, introduzca sus direcciones de correo electrónico en la `Add Email Recipients` campo separado por comas, espacios, pestañas o punto y coma.

## Programar resumen de correo electrónico

En el `Set when to send the Email Summary` , puede especificar cuándo enviar los resúmenes de correo electrónico. Las opciones son:

* `Manual`
* `Once`
* `Repeating`

### Guardar resumen de correo electrónico para enviarlo posteriormente

1. Select `Manual` de la variable `Set when to send the Email Summary` campo .

1. Haga clic en **[!UICONTROL Save]**.

   Esto guarda el resumen en la lista de resúmenes de correo electrónico.

1. Cuando esté listo para enviar el resumen, haga clic en el icono de engranaje y seleccione `Send Now`.

### Enviar resumen de correo electrónico una vez

1. Select `Once` de la variable `Set when to send the Email Summary` campo .

1. Especifique la fecha de inicio en la variable `Select Start Date` calendario.

1. Especifique la hora a la que enviar el correo electrónico en la `Select time to send` campo .

### Crear programación repetida

1. Select `Repeating` de la variable `Set when to send the Email Summary` campo .

1. En el `Set Frequency` campo, seleccione `Daily`, `Weekly`o `Monthly`.

1. Especifique la fecha de inicio en la variable `Select Start Date` calendario.

1. Especifique la hora a la que enviar el correo electrónico en la `Select time to send` campo .

1. (Opcional) Para especificar una fecha de finalización, seleccione `End Date` y seleccione la fecha de finalización del calendario.

## Modificar resumen de correo electrónico existente

Después de crear y guardar un resumen por correo electrónico, la variable `Email Summaries` muestra una lista de todos los resúmenes guardados. Puede expandir (`+`) cada fila para obtener más información. Las columnas de esta vista son:

* `Email Name` - Nombre del resumen del correo electrónico
* `Content` - Tipo de contenido dentro del resumen, como los nombres de cualquier informe. Para obtener información sobre el envío de un resumen por correo electrónico que contiene un informe con datos antiguos, consulte [Administración de la configuración de la cuenta](../../administrator/account-management/managing-account-settings.md).
* `Scheduled` - Frecuencia, fecha y hora de envío del resumen por correo electrónico
* `Recipients` : Resumen de destinatarios del correo electrónico
* `Created Date` - Fecha en que se creó el resumen del correo electrónico
* `Status` - `Paused` o `Active`

Haga clic en el icono de engranaje a la derecha de cada fila para:

* `Send Now` : envía el resumen del correo electrónico inmediatamente a todos los destinatarios especificados
* `Edit` - Permite modificar los detalles del resumen del correo electrónico
* `Pause/Active` : le permite pausar el resumen del correo electrónico para que no se envíe o activar el resumen en función de cómo esté configurado
* `Delete` - Elimina el resumen del correo electrónico
