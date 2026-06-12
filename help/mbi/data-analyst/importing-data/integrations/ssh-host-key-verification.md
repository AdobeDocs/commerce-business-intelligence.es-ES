---
title: Verificación de la clave del host SSH
description: Obtenga información sobre cómo Commerce Intelligence inscribe las claves de host SSH, cómo actualizarlas, solucionar errores y cuándo ponerse en contacto con el servicio de asistencia para las conexiones de túnel SSH.
role: Admin, Developer, User
feature: Commerce Tables, Data Warehouse Manager, Data Integration, Data Import/Export
role_v2: id: b69b2659-1057-424e-8fc5-ed9e016dc554id: c66ffd68-0f65-42bb-aa23-b4020f12e0bdid: ff6a42d2-313e-452e-93a6-792e4fad9ff8
level_v2: id: b5a62a22-46f7-4f0d-b151-3fc640bef588id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
topic_v2: id: df401a2a-327d-468c-a5e4-b7b7ccd071a0
product_v2: id: cc9c1b69-d771-4a04-84d3-df2e3989418fid: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2: id: b0c4e988-b173-423f-88d4-345071a0bce8
source-git-commit: b51e9fceba0c62f4ef3dde340d26cd78641ef3a2
workflow-type: tm+mt
source-wordcount: 1130
ht-degree: 0%

---

# Verificación de la clave del host SSH {#ssh-host-keys}

[!DNL Commerce Intelligence] utiliza la verificación estricta de la clave del host SSH para las conexiones de base de datos cifradas (túnel SSH), incluidas [MySQL](mysql-via-ssh-tunnel.md), [MongoDB](mongodb-via-ssh-tunnel.md) y [PostgreSQL](postgresql.md).

Durante **[!UICONTROL Save & Test]**, el sistema inscribe las claves de host SSH bastion para su conexión y las almacena de forma segura por conexión. Después de la inscripción, la replicación y el túnel solo se realizan correctamente cuando las claves del host del bastión activo coinciden con las claves inscritas.

Este modelo mejora la seguridad al bloquear los ataques de intermediario y los cambios inesperados en el host. También significa que la rotación de la clave del host, la falta de material de confianza o los cambios de infraestructura pueden aparecer como errores de clave del host SSH en la conexión en lugar de errores genéricos de túnel.

>[!NOTE]
>
>**Administrador** se refiere a un usuario con permisos de administrador en su cuenta de [!DNL Commerce Intelligence], no en la consola de organización de Adobe a menos que se indique lo contrario. Solamente los administradores pueden ejecutar **[!UICONTROL Refresh SSH Host Keys]**. Si no ve este control, pídale a un administrador de su cuenta que ejecute la actualización o que se ponga en contacto con el Soporte técnico de Adobe.

No edita, carga ni administra `known_hosts` archivos. La inscripción y la actualización se ejecutan en la infraestructura de Adobe asignada a su cuenta.

>[!IMPORTANT]
>
>La rotación de clave de host requiere que un administrador ejecute **[!UICONTROL Refresh SSH Host Keys]**. Si cambiaron las claves de host del bastión o cambió la identidad del bastión (nombre de host, IP o puerto), volver a ejecutar **[!UICONTROL Save & Test]** o volver a guardar la conexión no actualiza las claves inscritas. La conexión puede seguir fallando hasta que un administrador actualice las claves de host.

## Guardar y probar {#save-and-test}

**[!UICONTROL Save & Test]** realiza **inscripción inicial de clave de host SSH solamente**. Es conservador por diseño y no gira ni sobrescribe las claves que ya están inscritas para la conexión.

| Estado de clave de host inscrito | Qué hace Guardar y probar |
| --- | --- |
| Las claves de host aún no están inscritas | **[!UICONTROL Save & Test]** analiza el host y el puerto del bastión, inscribe las claves de host y las almacena para esta conexión. |
| Las claves de host ya están inscritas | **[!UICONTROL Save & Test]** omite la inscripción. No sobrescribe, rota ni elimina las claves inscritas existentes, aunque las claves de los bastiones activos ya no coincidan. |
| Faltan las claves inscritas, están vacías o no son válidas | **[!UICONTROL Save & Test]** no repara por sí solo el material de confianza no válido. Un administrador debe ejecutar **[!UICONTROL Refresh SSH Host Keys]** o ponerse en contacto con el soporte técnico si continúan los errores |

Después de una primera inscripción correcta, **[!UICONTROL Save & Test]** ejecuta la configuración de validación de credenciales y conexión, pero deja sin cambios las claves de host SSH inscritas.

## Actualizar claves de host SSH {#refresh-ssh-host-keys}

**[!UICONTROL Refresh SSH Host Keys]** actualiza las claves de host SSH inscritas cuando el bastión ha cambiado o cuando se debe reparar el material de confianza. Un administrador inicia la actualización desde la conexión en **[!UICONTROL Data]** > **[!UICONTROL Connections]**.

La actualización se ejecuta de forma asíncrona en la infraestructura de Adobe asignada a su cuenta. [!DNL Commerce Intelligence] vuelve después de que la actualización se haya puesto en cola. No realiza el análisis en la estación de trabajo.

Una actualización **reescribe** claves de host inscritas solamente cuando una de estas condiciones es verdadera:

* Faltan las claves de host inscritas
* Las claves de host inscritas están vacías
* No se pueden leer las claves de host inscritas
* Error de validación de claves de host inscritas
* Un nuevo análisis devuelve líneas de clave de host diferentes a las claves inscritas
* Las huellas digitales del análisis y las claves inscritas no coinciden

Si las claves inscritas son actuales y válidas, la actualización finaliza sin cambiarlas.

>[!TIP]
>
>Ejecute **[!UICONTROL Refresh SSH Host Keys]** después de que su equipo gire las claves de host SSH en el bastión, cambie el nombre de host o la IP del bastión o reemplace el extremo SSH. Espere unos minutos y ejecute **[!UICONTROL Save & Test]** para confirmar la conexión.

## Migración de cuentas {#migration}

No almacena en déclencheur la migración de cuentas. Adobe realiza movimientos del servidor de datos durante el mantenimiento o el escalado y copia las claves de host SSH inscritas para que la verificación estricta siga funcionando después del movimiento.

Después de que Adobe le notifique que la migración se ha completado:

1. Ejecute **[!UICONTROL Save & Test]** para confirmar la conexión. La inscripción se debe omitir si las claves se copiaron correctamente.
1. Si persisten los errores de clave de host SSH, pídale a un administrador que ejecute **[!UICONTROL Refresh SSH Host Keys]**, espere unos minutos y vuelva a ejecutar **[!UICONTROL Save & Test]**.
1. Póngase en contacto con el Soporte técnico de Adobe si los errores continúan después de **[!UICONTROL Save & Test]** y hasta dos **[!UICONTROL Refresh SSH Host Keys]** intentos.

## Mensajes de error de clave de host SSH {#ssh-host-key-errors}

El estado de la conexión muestra un único mensaje de clave de host SSH fácil de usar. Los errores RAW OpenSSH no se muestran en el panel.

La siguiente tabla asigna mensajes comunes a causas probables y pasos siguientes típicos.

| Mensaje o estado | Lo que significa | Posibles causas | Paso siguiente típico |
| --- | --- | --- | --- |
| Error de verificación de clave de host SSH | La clave de host del bastión no coincide con las claves inscritas o el material de confianza no se puede utilizar | Claves de host SSH giradas en el bastión; nombre de host del bastión, IP o puerto cambiado; claves inscritas que faltan, vacías, no válidas o ilegibles | Confirmar **dirección remota** y **puerto SSH**. Pregunte al equipo de infraestructura si se han cambiado las claves del host del bastión. Pida a un administrador que ejecute **[!UICONTROL Refresh SSH Host Keys]**, espere unos minutos y luego ejecute **[!UICONTROL Save & Test]**. |
| No se han podido inscribir las claves de host SSH | **[!UICONTROL Save & Test]** no pudo analizar ni almacenar claves de host de bastión | Bastión inaccesible desde la infraestructura de Adobe; error de DNS; el firewall bloquea [!DNL Commerce Intelligence] direcciones IP; **Dirección remota** o **Puerto SSH** incorrectos; error de análisis de clave de host en el bastión | Compruebe la inclusión en la lista de permitidos del firewall utilizando las direcciones IP [!DNL Commerce Intelligence] en la página de credenciales de la base de datos. Confirme que el bastión acepta SSH en el puerto configurado. Corrija los campos de conexión y ejecute **[!UICONTROL Save & Test]** de nuevo. |
| Faltan las claves de host SSH o no son válidas | La verificación estricta bloqueó el túnel porque el material de confianza inscrito está ausente o dañado | La primera conexión nunca completó la inscripción; error de actualización anterior; la migración no copió claves; problema en la infraestructura de Adobe | Pida a un administrador que ejecute **[!UICONTROL Refresh SSH Host Keys]** y luego **[!UICONTROL Save & Test]**. Póngase en contacto con el Soporte técnico si el error persiste. |
| No se han podido actualizar las claves de host SSH | La actualización no actualizó las claves inscritas | Error de red, DNS o análisis durante la actualización; problema en la infraestructura de Adobe | Espere unos minutos. Solicite a un administrador que vuelva a ejecutar **[!UICONTROL Refresh SSH Host Keys]** (segundo intento si falla el primero). Confirmar la accesibilidad y la inclusión en la lista de permitidos del bastión. Póngase en contacto con el soporte técnico si la conexión sigue fallando después de dos intentos de actualización y **[!UICONTROL Save & Test]**. |

## Lista de comprobación de resolución {#troubleshooting}

1. Confirme que la configuración de **Dirección remota**, **Puerto SSH** y usuario Linux coincida con la configuración de su bastión.
1. Confirme que el firewall permite las [!DNL Commerce Intelligence] direcciones IP que se muestran en la página de credenciales de la base de datos.
1. Pregunte a su equipo de infraestructura si las claves de host SSH del bastión han cambiado recientemente.
1. Ejecute **[!UICONTROL Save & Test]** para validar la configuración e inscribir claves si todavía no existen.
1. Pida a un administrador que ejecute **[!UICONTROL Refresh SSH Host Keys]**, espere unos minutos y vuelva a ejecutar **[!UICONTROL Save & Test]**. Si la primera actualización no resuelve el error, repita este paso.
1. Si la conexión sigue mostrando un error de clave de host SSH después de dos intentos de actualización, haga clic en **[!UICONTROL Contact Support]** en la página de conexión (o en el canal de soporte técnico de la cuenta).

## Cuándo ponerse en contacto con el Soporte de Adobe {#contact-support}

Póngase en contacto con el servicio de asistencia cuando:

* Los errores de clave de host SSH continúan después de que un administrador ejecute **[!UICONTROL Refresh SSH Host Keys]** dos veces y **[!UICONTROL Save & Test]** siga fallando
* **[!UICONTROL Refresh SSH Host Keys]** nunca se completa o el estado de la conexión no cambia después de 15 a 30 minutos
* Los errores comenzaron inmediatamente después de que Adobe le notificara la migración de la cuenta o el mantenimiento del servidor de datos
* La configuración del bastión y la inclusión en la lista de permitidos del cortafuegos son correctas, su equipo no ha girado las claves de host y aún no puede conectarse
* Necesita un administrador para ejecutar **[!UICONTROL Refresh SSH Host Keys]**, pero no hay ningún administrador disponible en la cuenta

Incluya el nombre de la conexión, la hora aproximada del último **[!UICONTROL Save & Test]** o intento de actualización, y si las claves de host del bastión cambiaron recientemente. No envíe claves privadas ni frases de contraseña.

## Relacionado {#related}

* [Conectar MySQL a través del túnel SSH](mysql-via-ssh-tunnel.md)
* [Conexión de MongoDB a través del túnel SSH](mongodb-via-ssh-tunnel.md)
* [Conectar PostgreSQL a través del túnel SSH](postgresql.md)
* [Volver a autenticar integraciones](https://experienceleague.adobe.com/docs/commerce-knowledge-base/kb/how-to/mbi-reauthenticating-integrations.html)
