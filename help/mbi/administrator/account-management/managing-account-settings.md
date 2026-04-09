---
title: Administrar la configuración de la cuenta
description: Aprenda a personalizar la configuración de la cuenta para su Data Warehouse.
exl-id: 847d51b1-287e-4c14-b64e-0bd9bfcccedc
role: Admin, User
feature: Accounts
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b6935462-7263-4ced-a703-60de6a5aeb2did: bd989d82-1e15-4534-88db-f1f51dd77ffa
subfeature_v2: id: a763c1a2-1d0a-40d7-9617-8139636fd12e
role_v2: id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: b69b2659-1057-424e-8fc5-ed9e016dc554
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588
topic_v2: id: eddd9b14-83bd-4ff4-9072-54a4a484abb7
source-git-commit: 4e01225a6bd285afbe988b9c24e07e2ea34649fc
workflow-type: tm+mt
source-wordcount: 349
ht-degree: 0%

---

# Personalizar la configuración de la cuenta

>[!NOTE]
>
>Requiere [permisos de administrador.](../../administrator/user-management/user-management.md)

En su cuenta de [!DNL Commerce Intelligence], puede personalizar la configuración de la cuenta para su Data Warehouse. Se puede acceder a ellos seleccionando su nombre de organización en la esquina superior derecha de cualquier pantalla y luego eligiendo **[!UICONTROL Account Settings]** de la lista desplegable.

* **[!UICONTROL Client Name:]** Esta configuración aparece en la esquina superior derecha de todos los paneles y en cualquier otra parte de la cuenta. Si desea cambiar **[!UICONTROL "Vandelay Industries Co., Ltd]** a solo **[!UICONTROL "Vandelay]**, aquí es donde debe hacerlo.

* **[!UICONTROL Currency:]** Esta es la *moneda predeterminada* para todos los valores monetarios de su cuenta. Cada vez que se sincroniza un valor decimal o monetario en Data Warehouse, esta configuración determina el símbolo colocado antes de ese valor en los informes.

* **[!UICONTROL Blackout Hours:]** Esta configuración garantiza que, durante las horas del día seleccionadas, Data Warehouse no acceda a las bases de datos conectadas. Todas las horas se expresan en hora cero y en hora estándar del Este (EST). Por ejemplo, si no desea tener acceso a la base de datos de producción entre las horas 9:00 a.m. EST y 1:00 p.m. EST, debe escribir la siguiente matriz de dígitos: **9, 10, 11, 12**.

* **[!UICONTROL Forced update hours:]** Esta configuración garantiza que una actualización de Data Warehouse comience automáticamente en su cuenta *durante las horas* que haya especificado. Al igual que con las horas de interrupción del servicio, estas también se encuentran en la TE. Por ejemplo, si desea que las actualizaciones de Data Warehouse comiencen automáticamente a las **medianoche** y a las **mediodía** EST, debe escribir la siguiente matriz de dígitos: **0, 12**.

* **[!UICONTROL Send email summaries if the data has not updated yet:]** Esta opción administra las situaciones en las que se programa el envío de un resumen de correo electrónico *antes de que se actualicen los datos de uno de sus informes*. Si elige **No**, su cuenta omitirá el envío del correo electrónico a la hora programada. En su lugar, la cuenta lo envía una vez que se han actualizado los datos. Si elige **[!UICONTROL Yes]**, su cuenta enviará el correo electrónico, incluirá un mensaje que explique que los datos están obsoletos y enviará otro correo electrónico una vez que se hayan actualizado los datos.

* **[!UICONTROL Enable data updates:]** Esta opción garantiza que las actualizaciones de datos se ejecuten en su cuenta. Si cambia la configuración a **[!UICONTROL No]**, las sincronizaciones de datos y los cálculos de columnas se detendrán en su cuenta.

>[!NOTE]
>
>Asegúrese de seleccionar **[!UICONTROL Save Customizations]** después de realizar los cambios.
