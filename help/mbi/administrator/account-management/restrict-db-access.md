---
title: Restricción del acceso a la base de datos
description: Descubra cómo puede restringir el acceso y limitar el acceso al servidor que aloja la base de datos.
role: Admin, User
feature: Accounts, User Management
TQID: https://experienceleague.adobe.com/O2cS-hbhjqktc4LpJD6agxgIwabrypgCY9fnJTCR2XM
product_v2:
  - id: cc9c1b69-d771-4a04-84d3-df2e3989418f
  - id: eadea719-cf89-469b-a6fd-a236a7138047
feature_v2:
  - id: bd989d82-1e15-4534-88db-f1f51dd77ffa
role_v2:
  - id: b69b2659-1057-424e-8fc5-ed9e016dc554
  - id: c66ffd68-0f65-42bb-aa23-b4020f12e0bd
level_v2:
  - id: b5a62a22-46f7-4f0d-b151-3fc640bef588
  - id: e8ccd51f-da0d-4e3b-939b-e30d5ebb1ea5
exl-id: 7a0bc0d7-086e-4a6e-b1dd-6db13814710e
source-git-commit: fac3c5724cab4a90422fad310a4573a7268a56c4
workflow-type: tm+mt
source-wordcount: 225
ht-degree: 0%

---


# Restringir el acceso

Cuando crea un túnel SSH al servidor, no es necesario que [!DNL Adobe Commerce Intelligence] tenga acceso a nada excepto a la base de datos. Para obtener información sobre la inscripción, los errores y la solución de problemas en la clave de host SSH, consulte [Verificación de la clave de host SSH](../../data-analyst/importing-data/integrations/ssh-host-key-verification.md). Si no desea que [!DNL Commerce Intelligence] tenga acceso total al servidor que aloja su base de datos, puede restringir el acceso forzando al usuario [!DNL Commerce Intelligence Linux] a un [shell de bash restringido](https://www.gnu.org/software/bash/manual/html_node/The-Restricted-Shell.html).

Puede que haya adivinado por el nombre, pero se usa un shell de bash restringido para configurar un entorno más controlado que el shell estándar. Lo importante de este tipo de shell es que los usuarios de shell restringidos no pueden acceder a las funciones del sistema ni realizar ningún tipo de modificación.

Para restringir el usuario [!DNL Commerce Intelligence Linux], debe hacer dos cosas:

1. Cambie la variable de entorno PATH para que sea la cadena vacía. Esto significa que el usuario no puede acceder a los ejecutables del sistema.
1. Asegúrese de que el shell ejecutado sea `bash -r`

Ambos se pueden realizar dentro del archivo `authorized_keys` en el directorio principal `dir/.ssh` del usuario como parte del comando que se ejecuta cuando el usuario inicia sesión. Tiene un aspecto similar al siguiente:

```bash
... other keys ...
command="env PATH="" /bin/bash -r" <rjmetrics public key goes here>
... other keys ...
```

Cuando se complete esto, el usuario que creó para [!DNL Commerce Intelligence] no podrá realizar cambios en el sistema.
