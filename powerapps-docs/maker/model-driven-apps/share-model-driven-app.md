---
title: Compartir una aplicación controlada por modelos con PowerApps | Microsoft Docs
description: Aprenda a compartir una aplicación basada en modelos
documentationcenter: ''
author: Mattp123
manager: kvivek
editor: ''
tags: ''
ms.service: powerapps
ms.devlang: na
ms.topic: conceptual
ms.component: model
ms.date: 03/19/2019
ms.author: matp
search.audienceType:
  - maker
search.app:
  - PowerApps
  - D365CE
---

# <a name="share-a-model-driven-app-with-powerapps"></a>Compartir una aplicación controlada por modelos con PowerApps

Las aplicaciones de [!INCLUDE [powerapps](../../includes/powerapps.md)] usan la seguridad basada en roles para compartir. El concepto básico en la seguridad basada en roles es que el rol de seguridad contiene privilegios que definen un conjunto de acciones que se pueden realizar en la aplicación. Todos los usuarios de la aplicación deben estar asignados a uno o más roles predefinidos o personalizados. O bien, también se pueden asignar roles a equipos. Cuando se asigna un usuario o un equipo a uno de estos roles, se concede a la persona o miembros del equipo el conjunto de privilegios asociados a este rol. 

En este tema realizará las tareas para compartir una aplicación controlada por modelos para que otros puedan usarla. Aprenderá a:
- Crear un rol de seguridad personalizado
- Asignar usuarios al rol de seguridad personalizado
- Asignar el rol de seguridad a una aplicación

## <a name="prerequisites"></a>Requisitos previos
Para compartir una aplicación debe tener el rol de administrador del entorno de [!INCLUDE [powerapps](../../includes/powerapps.md)] o el rol de administrador del sistema. 

## <a name="sign-in-to-powerapps"></a>Iniciar sesión en PowerApps
Iniciar sesión en [PowerApps](https://powerapps.microsoft.com/). Si aún no tiene una cuenta de [!INCLUDE [powerapps](../../includes/powerapps.md)], seleccione el vínculo **Introducción gratuita**.

## <a name="share-an-app"></a>Compartir una aplicación 
En este tema se realizará un seguimiento de la compañía, Contoso, que es una empresa de cuidado de mascotas orientada a perros y gatos. Una aplicación que contiene una entidad personalizada para realizar un seguimiento de la empresa de cuidado de mascotas ya se ha creado y publicado. Ahora la aplicación se debe compartir para que el personal de la empresa pueda usarla. Para compartir la aplicación, un administrador o el creador de la aplicación asigna uno o varios roles de seguridad a los usuarios y a la aplicación. 

## <a name="create-or-configure-a-security-role"></a>Crear o configurar un rol de seguridad
El entorno de [!INCLUDE [powerapps](../../includes/powerapps.md)] incluye [roles de seguridad predefinidos](#about-predefined-security-roles) que reflejan tareas de usuario comunes con niveles de acceso definidos para que coincidan con el objetivo de seguridad recomendado de proporcionar acceso a la cantidad mínima de datos profesionales necesarios para usar la aplicación. Recuerde que la aplicación de cuidado de mascotas de Contoso está basada en una entidad personalizada. Puesto que la entidad es personalizada, los privilegios se deben especificar explícitamente antes de que los usuarios puedan trabajar con ella. Para hacerlo, puede realizar lo siguiente.
- Expandir un rol de seguridad predefinido existente, de modo que incluya privilegios en registros en función de la entidad personalizada. 
- Crear un rol de seguridad personalizado con el fin de administrar privilegios para los usuarios de la aplicación. 

Puesto que el entorno que mantendrá los registros de cuidado de mascotas también se usa para otras aplicaciones de Contoso, se creará un rol de seguridad personalizado específico para la aplicación de cuidado de mascotas. Además, se necesitan dos conjuntos diferentes de privilegios de acceso.
- Los técnicos del cuidado de mascotas solo necesitan leer, actualizar y adjuntar otros registros, de modo que su rol de seguridad deberá tener privilegios de lectura, escritura y anexar. 
- Los programadores del cuidado de mascotas necesitan todos los privilegios que tienen los técnicos, además de la capacidad de crear, anexar a, eliminar y compartir, por lo que su rol de seguridad tendrá privilegios para crear, leer, escribir, anexar, eliminar, asignar y compartir.

Para obtener más información sobre los privilegios de acceso y de ámbito, consulte [Roles de seguridad](https://docs.microsoft.com/dynamics365/customer-engagement/admin/security-roles-privileges#security-roles).

## <a name="create-a-custom-security-role"></a>Crear un rol de seguridad personalizado
1. En el sitio de [!INCLUDE [powerapps](../../includes/powerapps.md)], seleccione **Aplicaciones** > **…**> **Compartir vínculo**.

2. En el cuadro de diálogo **Compartir esta aplicación**, en **Crear un rol de seguridad**, seleccione **Configuración de seguridad**.

3. En la página **Configuración**, seleccione **Nuevo**.  

4. En el diseñador de roles de seguridad, seleccione las acciones, como leer, escribir o eliminar, y el ámbito para realizar dicha acción. El ámbito determina la profundidad o altura dentro de la jerarquía de entornos en la que el usuario puede realizar una acción determinada. En el cuadro **Nombre del rol**, introduzca *Técnicos de cuidado de mascotas*.

5. Seleccione la pestaña **Entidades personalizadas** y, a continuación, localice la entidad personalizada que desee. Para este ejemplo, se utiliza la entidad personalizada **Mascota**. 

6. En la fila **Mascota**, seleccione cada uno de los siguientes privilegios cuatro veces hasta que se seleccione el ámbito global de la organización ![Ámbito global de la organización](media/share-model-driven-app/organizational-scope-privilege.png): **Leer, Escribir, Anexar**

   > [!div class="mx-imgBorder"] 
   > ![Nuevo rol de seguridad](media/share-model-driven-app/custom-security-role.png)

7. Puesto que la aplicación de cuidado de mascotas también tiene una relación con la entidad Cuenta, seleccione la pestaña **Registros principales** y, en la fila **Cuenta** seleccione **Leer** cuatro veces hasta que se haya seleccionado el ámbito global de la organización ![Ámbito global de la organización](media/share-model-driven-app/organizational-scope-privilege.png). 

8. Seleccione la pestaña **Personalización** y luego en la lista de privilegios seleccione el privilegio **Leer** junto a **Aplicación basada en modelo** para seleccionar el ámbito de organización. ![Ámbito global de la organización](media/share-model-driven-app/organizational-scope-privilege.png).

9. Seleccione **Guardar y cerrar**. 

10. En el diseñador de roles de seguridad, en el cuadro **Nombre del rol**, introduzca *Programadores del cuidado de mascotas*. 

11. Seleccione la pestaña **Entidades personalizadas** y, a continuación, localice la entidad **Mascota**. 

12. En la fila **Mascota**, seleccione cada uno de los siguientes privilegios cuatro veces hasta que se seleccione el ámbito global de la organización ![Ámbito global de la organización](media/share-model-driven-app/organizational-scope-privilege.png): **Crear, Leer, Escribir, Eliminar, Anexar, Anexar a, Asignar, Compartir**

13. Puesto que la aplicación de cuidado de mascotas también tiene una relación con la entidad Cuenta y los programadores deben poder crear y modificar registros de cuenta, seleccione la pestaña **Registros principales** y, en la fila **Cuenta** seleccione cada uno de los siguientes privilegios cuatro veces hasta que se haya seleccionado el ámbito global de la organización ![Ámbito global de la organización](media/share-model-driven-app/organizational-scope-privilege.png). 
    **Crear, Leer, Escribir, Eliminar, Anexar, Anexar a, Asignar, Compartir**

14. Seleccione **Guardar y cerrar**.

## <a name="assign-security-roles-to-users"></a>Asignar roles de seguridad a usuarios
Los roles de seguridad controlan el acceso del usuario a los datos a través de un conjunto de niveles de acceso y permisos. La combinación de niveles de acceso y permisos que se incluyen en un determinado rol de seguridad define los límites de visualización de datos para el usuario, así como las interacciones del usuario con estos.

### <a name="assign-a-security-role-to-pet-grooming-technicians"></a>Asignar un rol de seguridad a los técnicos del cuidado de mascotas
1. En el cuadro de diálogo **Compartir esta aplicación**, en **Asignar usuarios al rol de seguridad**, seleccione **Usuarios de seguridad**.
2. En la lista que se muestra, seleccione los cuidadores de mascotas.
3. Seleccione **Administrar roles**.

    > [!div class="mx-imgBorder"] 
    > ![Administrar roles](media/share-model-driven-app/select-users-for-security-roles.png)

4. En el cuadro de diálogo **Administrar roles de usuario**, seleccione el rol de seguridad **Técnicos del cuidado de mascotas** que creó antes y seleccione **Aceptar**.

### <a name="assign-a-security-role-to-pet-grooming-schedulers"></a>Asignar un rol de seguridad a los programadores del cuidado de mascotas
1. En el cuadro de diálogo **Compartir esta aplicación**, en **Asignar usuarios a un rol de seguridad**, seleccione **Usuarios de seguridad**.
2. En la lista que se muestra, seleccione los programadores del cuidado de mascotas.
3. Seleccione **Administrar roles**.
4. En el cuadro de diálogo **Administrar roles de usuario**, seleccione el rol de seguridad **Programadores del cuidado de mascotas** que creó antes y seleccione **Aceptar**.


## <a name="add-security-roles-to-the-app"></a>Agregar roles de seguridad a la aplicación
A continuación, es necesario asignar uno o varios roles de seguridad a la aplicación. Los usuarios tendrán acceso a aplicaciones en función de los roles de seguridad a los que se les asigne.
1. En el cuadro de diálogo **Compartir esta aplicación**, en **Agregar el rol de seguridad a la aplicación**, seleccione **Mis aplicaciones**.
2. En la esquina inferior derecha de la ventana de la aplicación de la aplicación de cuidado de mascotas de Contoso, seleccione **Más opciones (...)** y después seleccione **Administrar roles**.

    ![Administrar roles para la aplicación](media/share-model-driven-app/manage-roles.png)

4. En la sección **Roles**, puede elegir si va a conceder a la aplicación acceso a todos los roles de seguridad o a roles seleccionados. Seleccione los roles de **Programadores del cuidado de mascotas** y **Técnicos del cuidado de mascotas** que creó anteriormente.

    > [!div class="mx-imgBorder"] 
    > ![Seleccionar roles de seguridad para la aplicación](media/share-model-driven-app/app-security-roles.png)

5. Seleccione **Guardar**.
 
## <a name="share-the-link-to-your-app"></a>Compartir el vínculo a su aplicación
1. En el cuadro de diálogo **Compartir esta aplicación**, en **Compartir el vínculo a su aplicación directamente con usuarios**, copie la dirección URL que se muestra.
 
2. Seleccione **Cerrar**.
3. Pegue la dirección URL de la aplicación en una ubicación para que los usuarios puedan acceder a ella, como publicándola en un sitio de SharePoint o enviándola por correo electrónico.

> [!div class="mx-imgBorder"] 
> ![Compartir el vínculo](media/share-model-driven-app/share-model-driven-URL.PNG)

También puede buscar la dirección URL de la aplicación en la pestaña **Propiedades** del diseñador de aplicaciones. 

> [!div class="mx-imgBorder"] 
> ![Copiar URL de la aplicación](media/share-model-driven-app/app-designer-copy-web-url.png)

## <a name="about-predefined-security-roles"></a>Acerca de los roles de seguridad predefinidos
Estos roles predefinidos están disponibles con un entorno de [!INCLUDE [powerapps](../../includes/powerapps.md)].


|Rol de seguridad  |*Privilegios  |Descripción |
|---------|---------|---------|
|Creador de entornos     |  Ninguno       | Puede crear nuevos recursos asociados a un entorno incluyendo aplicaciones, conexiones, API personalizadas, puertas de enlace y flujos usando Microsoft Flow. Sin embargo, no tiene ningún privilegio para acceder a los datos en un entorno. Más información: [Información general de entornos](https://powerapps.microsoft.com/blog/powerapps-environments/)        |
|Administrador del sistema     |  Crear, Leer, Escribir, Eliminar, Personalizaciones, Roles de seguridad       | Tiene permiso completo para personalizar o administrar el entorno, incluida la creación, modificación y asignación de roles de seguridad. Puede ver todos los datos del entorno. Más información: [Privilegios necesarios para la personalización](https://docs.microsoft.com/dynamics365/customer-engagement/customize/privileges-required-customization)        |
|Personalizador del sistema     | Crear (propio), Leer (propio), Escribir (propio), Eliminar (propio), Personalizaciones         | Tiene permiso completo para personalizar el entorno. No obstante, solo puede ver los registros de las entidades del entorno que cree. Más información: [Privilegios necesarios para la personalización](https://docs.microsoft.com/dynamics365/customer-engagement/customize/privileges-required-customization)        |
|Usuario de Common Data Service     |  Leer, Crear (propio), Escribir (propio), eliminar (propio)       | Puede ejecutar una aplicación dentro del entorno y realizar las tareas comunes para los registros de su propiedad.        |
|Delegar     | Actúa en nombre de otro usuario        | Permite ejecutar código como otro usuario o la suplantación.  Se suele usar con otro rol de seguridad para permitir el acceso a los registros. Más información: [Suplantar a otro usuario](https://docs.microsoft.com/dynamics365/customer-engagement/developer/org-service/impersonate-another-user)        |

*El privilegio es ámbito global salvo que se especifique lo contrario.

## <a name="next-steps"></a>Pasos siguientes
[Ejecutar una aplicación controlada por modelos en un dispositivo móvil](../../user/run-app-client-model-driven.md)



