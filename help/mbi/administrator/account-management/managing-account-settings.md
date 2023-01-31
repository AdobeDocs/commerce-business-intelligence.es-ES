---
title: Administrar la configuración de la cuenta
description: Obtenga información sobre cómo personalizar una serie de configuraciones de cuenta para el almacén de datos.
exl-id: 847d51b1-287e-4c14-b64e-0bd9bfcccedc
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '363'
ht-degree: 0%

---

# Personalización de la configuración de la cuenta

>[!NOTE]
>
>Requiere [Permisos de administración.](../../administrator/user-management/user-management.md)

En [!DNL MBI] puede personalizar varias configuraciones de cuenta para el almacén de datos. Se puede acceder a ellas seleccionando el nombre de su organización en la esquina superior derecha de cualquier pantalla y luego eligiendo **[!UICONTROL Account Settings]** en la lista desplegable .

* **[!UICONTROL Client Name:]** Esta configuración aparece en la esquina superior derecha de todos los tableros y en cualquier otra parte de la cuenta. Si desea cambiar **[!UICONTROL "Vandelay Industries Co., Ltd]** a solo **[!UICONTROL "Vandelay]**, aquí es donde hacer eso.

* **[!UICONTROL Currency:]** Esta es la *moneda predeterminada* para todos los valores monetarios de su cuenta. Cada vez que se sincroniza un valor decimal o monetario en el almacén de datos, esta configuración determina el símbolo colocado antes de dicho valor en los informes.

* **[!UICONTROL Blackout Hours:]** Esta configuración garantiza que, durante las horas seleccionadas del día, el almacén de datos no acceda a las bases de datos conectadas. Todas las horas se expresan a cero horas y en la hora estándar del este (EST). Por ejemplo, si no desea que se acceda a la base de datos de producción entre las 9:00 EST y las 13:00 EST, debe escribir la siguiente matriz de dígitos: **9, 10, 11, 12**.

* **[!UICONTROL Forced update hours:]** Esta configuración garantiza que una actualización del almacén de datos comience automáticamente en la cuenta *en las horas* ha especificado. Como con las horas de apagón, también están en ET. Por ejemplo, si desea que las actualizaciones del almacén de datos comiencen automáticamente en **medianoche** y **mediodía** EST, debe escribir la siguiente matriz de dígitos: **0, 12**.

* **[!UICONTROL Send email summaries if the data has not updated yet:]** Esta opción indica al sistema qué hacer en situaciones en las que está programado el envío de un resumen por correo electrónico *antes de los datos de uno de sus informes* se actualiza hasta el presente. Si elige **No**, su cuenta omitirá el envío del correo electrónico a la hora programada y, en su lugar, lo enviará una vez que se hayan actualizado los datos. Si elige **[!UICONTROL Yes]**, su cuenta enviará el correo electrónico, incluirá un mensaje que explique que los datos están obsoletos y enviará otro correo electrónico una vez que los datos se hayan actualizado.

* **[!UICONTROL Enable data updates:]** Esta opción garantiza que las actualizaciones de datos se ejecuten en la cuenta. Si cambia la configuración a **[!UICONTROL No]**, las sincronizaciones de datos y los cálculos de columnas se detendrán completamente en su cuenta.

>[!NOTE]
>
>Asegúrese de seleccionar **[!UICONTROL Save Customizations]** después de realizar cualquier cambio.
