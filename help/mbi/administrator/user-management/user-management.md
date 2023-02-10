---
title: Administración de usuarios y permisos
description: Obtenga información sobre cómo administrar su [!DNL MBI] usuarios.
exl-id: 2a5eeabb-3c13-4ca1-b845-ed255b389c9f
source-git-commit: 03a5161930cafcbe600b96465ee0fc0ecb25cae8
workflow-type: tm+mt
source-wordcount: '415'
ht-degree: 0%

---

# Administrar permisos de usuario

MBI está diseñado para ser una única fuente de verdad en toda la organización. Cada usuario tendrá su propio conjunto de tableros que puede [compartir con otros usuarios](../../data-user/dashboards/share-dashboard-with-users.md).

## Niveles de permisos de usuario

En [!DNL MBI], hay tres niveles de permisos generales que se aplican a los usuarios, que se seleccionan cuando se crea una cuenta:

* `Admin`
* `Standard`
* `Read-Only`

Estos permisos permiten a los usuarios realizar determinadas acciones o acceder a partes específicas de [!DNL MBI]. Esta es una tabla de lo que puede hacer cada nivel de permisos en MBI:

|  | `Admin` | `Standard` | `Read Only` |
| -----|-----|-----|----|
| **Crear/administrar usuarios** | ✔ |  |  |
| **Crear resúmenes de correo electrónico** | ✔ | ✔ |  |
| **Crear/editar/compartir tableros** | ✔ | ✔ |  |
| **Ver tableros** | ✔ | ✔ | ✔ |
| **Creación, edición o eliminación de informes visuales** | ✔ | ✔* |  |
| **Crear/editar/eliminar informes SQL** | ✔ |  |  |
| **Clonar tableros** | ✔ |  |  |
| **Agregar y administrar integraciones** | ✔ |  |  |
| **Acceso al Administrador de Datas Warehouse** | ✔ |  |  |
| **Tablas y columnas de sincronización/dessincronización** | ✔ |  |  |
| **Crear/editar métricas** | ✔ |  |  |
| **Crear/editar conjuntos de filtros** | ✔ |  |  |
| **Crear/editar columnas calculadas** | ✔ |  |  |
| **Crear lista de informes dependientes** | ✔ |  |  |
| **Resumen del sistema de acceso** | ✔ |  |  |
| **Acceso a la configuración de zona horaria** | ✔ |  |  |
| **Acceso a la facturación** | ✔ | ✔** |  |
| **Contacto con el servicio de asistencia** | ✔ | ✔ | ✔ |

{style=&quot;table-layout:auto&quot;}

>[!NOTE]
>
>_Puede limitar un **[!UICONTROL Standard]**user&#39;s [acceso a métricas específicas](../../administrator/user-management/restrict-metric-access.md)._
>
>**[!UICONTROL Standard] _los usuarios pueden acceder a Facturación con una configuración de permisos adicional._
>
>**[!UICONTROL Read-Only]** los usuarios solo pueden _ver_ tableros que se han compartido con ellos; no pueden crear ni editar nada en [!DNL MBI], tampoco pueden buscar y agregar nuevos tableros a su cuenta. Le recomendamos que comparta un conjunto específico de tableros con **[!UICONTROL Read-Only]** usuarios que usted u otro miembro de su equipo mantenga. No clone un conjunto de tableros para ellos.

## Permisos adicionales: Facturación y asistencia técnica {#billingtech}

Además de los niveles generales de permisos, también existen otras dos designaciones de usuario: `Billing` y `Technical`. Estas designaciones están destinadas a utilizarse junto con los niveles generales de permisos.

### Facturación

`Billing` los usuarios tienen acceso a la página de facturación y pueden cambiar la información de pago. Además, nuestros equipos también pueden ponerse en contacto con ellos para plantear preguntas de facturación.

`Admin` los usuarios tienen acceso a la pestaña Facturación de forma predeterminada, pero los usuarios de Standard también pueden obtener acceso si tienen la variable `Billing` en su perfil.

![facturación](../../assets/billing.png)<!--{: width="550" height="363"}-->

### Técnico

`Technical` Los usuarios no tienen permisos específicos; esta configuración solo marca un contacto técnico dentro de la organización. Nuestros equipos pueden ponerse en contacto con estos usuarios por cuestiones técnicas.

`Admin` los usuarios pueden agregar nuevos usuarios a su cuenta haciendo clic en **[!UICONTROL Account Settings]** > **[!UICONTROL Create Users]** y siguiendo las indicaciones. Una vez creado el usuario en [!DNL MBI], la persona afortunada a la que está invitando recibirá instrucciones por correo electrónico sobre cómo completar el proceso de configuración de la cuenta.

En cualquier momento, `Admins` puede ver todos los usuarios de su cuenta haciendo clic en **[!UICONTROL Account Settings]** > **[!UICONTROL Manage Users]**. Esta página muestra los permisos del usuario y las métricas y tableros a los que tiene acceso.
