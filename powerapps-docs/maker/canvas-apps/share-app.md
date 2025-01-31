---
title: Compartir una aplicación de lienzo | Microsoft Docs
description: Compartir la aplicación de lienzo proporcionando a otros usuarios permiso para ejecutarla o modificarla
author: tapanm-msft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: ''
ms.date: 08/09/2019
ms.author: tapanm
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: cb8c77b60caa1f1ddf07e12f50e3cd52df764627
ms.sourcegitcommit: 7dae19a44247ef6aad4c718fdc7c68d298b0a1f3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/07/2019
ms.locfileid: "71995606"
---
# <a name="share-a-canvas-app-in-powerapps"></a>Compartir una aplicación de lienzo en PowerApps

Después de compilar una aplicación que responde a una necesidad empresarial, especifique qué usuarios de su organización pueden ejecutarla y cuáles pueden modificarla e incluso volver a compartirla. Especifique cada usuario por nombre, o indique un grupo de seguridad en Azure Active Directory. Si todos los usuarios se beneficiarán de la aplicación, especifique que toda la organización puede ejecutarla.

> [!IMPORTANT]
> Para que una aplicación compartida funcione como se espera, también debe administrar los permisos para el origen de datos o los orígenes en los que se basa la aplicación, como [Common Data Service](#common-data-service) o [Excel](share-app-data.md). Es posible que también deba compartir [otros recursos](share-app-resources.md) de los que depende la aplicación, como flujos, puertas de enlace o conexiones.

## <a name="prerequisites"></a>Requisitos previos

Para poder compartir una aplicación, debe guardarla en la nube, no de forma local, y después publicarla.

- Asigne a la aplicación un nombre descriptivo y una descripción clara, para que los usuarios sepan qué hace la aplicación y puedan encontrarla fácilmente en una lista. En el menú **Archivo** en PowerApps Studio, seleccione **Configuración de la aplicación**, especifique un nombre y después escriba o pegue una descripción.

- Siempre que realice cambios, debe guardar y volver a publicar la aplicación si desea que otros usuarios puedan verlos.

## <a name="share-an-app"></a>Compartir una aplicación

1. [Inicie sesión](https://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc) en PowerApps y después seleccione **Aplicaciones** cerca del borde izquierdo.

    ![Mostrar la lista de aplicaciones](./media/share-app/file-apps.png)

1. Seleccione la aplicación que desea compartir seleccionando su icono.

    ![Seleccionar una aplicación](./media/share-app/select-app.png)

1. En el banner, seleccione **compartir**.

    ![Abrir la pantalla Compartir](./media/share-app/banner-share.png)

1. Especifique el nombre o el alias de los usuarios o grupos de seguridad de Azure Active Directory con los que desea compartir la aplicación.

    - Para que toda la organización pueda ejecutar la aplicación (pero no modificarla ni compartirla), escriba **todos** en el panel de uso compartido.
    - Puede compartir una aplicación con una lista de alias, nombres descriptivos o una combinación de ellos (por ejemplo, **Jane Doe &lt; @ no__t-2 >** ) si los elementos están separados por punto y coma. Si hay más de una persona con el mismo nombre pero con distintos alias, se agregará a la lista la primera persona encontrada. Aparece una información sobre herramientas si un nombre o alias ya tiene permiso o no se puede resolver. 

    ![Especificar usuarios y copropietarios](./media/share-app/share-everyone.png)

    > [!NOTE]
    > No se puede compartir una aplicación con un grupo de distribución de la organización o con un usuario o grupo ajeno a la organización.

1. Si quiere permitir que los usuarios con quienes está compartiendo la aplicación la editen y lo compartan (además de ejecutarlo), active la casilla **copropietario** .

    No se puede conceder el permiso de **copropietario** a un grupo de seguridad si se ha [creado la aplicación desde una solución](add-app-solution.md).

    > [!NOTE]
    > Independientemente de los permisos, no hay dos personas que puedan editar una aplicación al mismo tiempo. Si una persona abre la aplicación para su edición, otras personas pueden ejecutarla, pero no modificarla.

1. Si la aplicación se conecta a los datos para los que los usuarios necesitan permisos de acceso, especifíquelo.

    Por ejemplo, la aplicación podría conectarse a una entidad en una base de datos de Common Data Service. Cuando comparta una aplicación de este tipo, el panel de uso compartido le pedirá que administre la seguridad de esa entidad.

    > [!div class="mx-imgBorder"]
    > ![Assign un rol de seguridad @ no__t-1

    Para obtener más información sobre la administración de la seguridad de una entidad, vea [administrar permisos de entidad](share-app.md#manage-entity-permissions) más adelante en este tema.

1. Si desea ayudar a los usuarios a encontrar la aplicación, active la casilla **enviar una invitación por correo electrónico a los nuevos usuarios** .

1. En la parte inferior del panel compartir, seleccione **compartir**.

    Todos los usuarios con quienes haya compartido la aplicación pueden ejecutarla en PowerApps Mobile en un dispositivo móvil o en AppSource en [Dynamics 365](https://home.dynamics.com) en un explorador. Los copropietarios pueden editar y compartir la aplicación en [PowerApps](https://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc).

    Si ha enviado una invitación por correo electrónico, todos los usuarios con quienes haya compartido la aplicación pueden ejecutarla seleccionando un vínculo en la invitación.

    - Si un usuario selecciona el vínculo en un dispositivo móvil, la aplicación se abre en PowerApps Mobile.
    - Si un usuario selecciona el vínculo en un equipo de escritorio, la aplicación se abre en un explorador.

    Los copropietarios que reciben una invitación obtienen otro vínculo que abre la aplicación para su edición en PowerApps Studio.

Para cambiar los permisos de un usuario o un grupo de seguridad, seleccione su nombre y, a continuación, realice cualquiera de estos pasos:

- Para permitir que los **copropietarios** ejecuten la aplicación pero ya no la editen ni compartirla, desactive la casilla copropietario.
- Para dejar de compartir la aplicación con ese usuario o grupo, seleccione el icono Quitar (x).

## <a name="security-group-considerations"></a>Consideraciones de grupo de seguridad

- Si comparte una aplicación con un grupo de seguridad, los miembros de ese grupo y cualquiera que se una a él tendrán los permisos que especifique para dicho grupo. Cualquier persona que abandone el grupo perderá esos permisos a menos que pertenezca a un grupo diferente que tenga acceso o le otorgue permisos como usuario individual.

- Todos los miembros de un grupo de seguridad tienen los mismos permisos para una aplicación que el grupo general. Sin embargo, puede especificar mayores permisos para uno o varios miembros de ese grupo para permitirles mayor acceso. Por ejemplo, puede conceder a un grupo de seguridad un permiso para ejecutar una aplicación, pero también puede proporcionar al usuario B, que pertenece a ese grupo, **el permiso de copropietario** . Todos los miembros del grupo de seguridad pueden ejecutar la aplicación, pero solo el usuario B puede modificarla. Si concede al grupo de seguridad un permiso de **copropietario** y el permiso de usuario B para ejecutar la aplicación, ese usuario todavía puede editar la aplicación.

## <a name="manage-entity-permissions"></a>Administrar permisos de entidad

### <a name="common-data-service"></a>Common Data Service

Si crea una aplicación basada en Common Data Service, también debe asegurarse de que los usuarios con quienes comparte la aplicación tengan los permisos adecuados para la entidad o entidades en las que se basa la aplicación. En concreto, los usuarios deben pertenecer a un rol de seguridad que pueda realizar tareas como crear, leer, escribir y eliminar registros relevantes. En muchos casos, querrá crear uno o varios roles de seguridad personalizados con los permisos exactos que los usuarios necesitan para ejecutar la aplicación. Después, puede asignar un rol a cada usuario según corresponda.

> [!NOTE]
> En el que se redactó este artículo, puede asignar roles de seguridad a usuarios individuales y grupos de seguridad en Azure Active Directory pero no a grupos de Office.

#### <a name="prerequisite"></a>Requisito previo

Para asignar un rol, debe tener permisos de **Administrador del sistema** para una base de datos de Common Data Service.

#### <a name="assign-a-security-group-in-azure-ad-to-a-role"></a>Asignación de un grupo de seguridad en Azure AD a un rol

1. En el panel uso compartido, seleccione **asignar un rol de seguridad** en **permisos de datos**.

1. Seleccione el rol o los roles de Common Data Service que desea asignar al usuario o al grupo de seguridad en Azure AD con el que desea compartir la aplicación.
     > [!div class="mx-imgBorder"] 
     > (media/share-app/cds-assign-security-role-list.png "Lista de roles de seguridad") lista de roles de ![seguridad]

### <a name="common-data-service-previous-version"></a>Common Data Service (versión anterior)

Cuando comparte una aplicación basada en una versión anterior de Common Data Service, debe compartir el permiso de tiempo de ejecución con el servicio por separado. Si no tiene permiso para hacerlo, consulte al administrador del entorno.

## <a name="share-with-guests"></a>Compartir con invitados

> [!IMPORTANT]
> - Las características de versión preliminar no están diseñadas para su uso en producción y pueden tener funcionalidad restringida. Estas características están disponibles antes de una versión oficial para que los clientes puedan obtener un acceso anticipado y proporcionar comentarios. 
> - Las características de vista previa tienen compatibilidad limitada por Soporte técnico de Microsoft y pueden estar disponibles solo en las áreas geográficas seleccionadas. 

Las aplicaciones de lienzo de PowerApps se pueden compartir con los usuarios invitados de un inquilino de Azure Active Directory. Esto permite invitar a socios comerciales externos, contratistas y terceros a ejecutar las aplicaciones de lienzo de la empresa. 

> [!NOTE]
> Los invitados solo pueden tener asignado el rol de **usuario** y no el rol de **copropietario** para las aplicaciones que se comparten con ellos.

### <a name="prerequisites"></a>Requisitos previos
- En Azure Active Directory (Azure AD), habilite la colaboración externa B2B para el inquilino. Más información: [Habilitar la colaboración externa B2B y administrar quién puede invitar a invitados](/azure/active-directory/b2b/delegate-invitations)
    - Habilitar la colaboración externa B2B está activada de forma predeterminada. Sin embargo, un administrador de inquilinos puede cambiar la configuración.  Para obtener más información acerca de Azure AD B2B, consulte [¿Qué es el acceso de usuarios invitados en Azure ad B2B?](/azure/active-directory/b2b/what-is-b2b)  
- Acceso a una cuenta que puede Agregar usuarios invitados a un inquilino de Azure AD. Los administradores y los usuarios con el rol de invitador invitado pueden agregar invitados a un inquilino.   
- El usuario invitado debe tener una licencia de PowerApps asignada a través de uno de los inquilinos siguientes:
    - El inquilino que hospeda la aplicación que se comparte.
    - El inquilino principal del usuario Guest.

### <a name="steps-to-grant-guest-access"></a>Pasos para conceder acceso de invitado
1. Seleccione **nuevo usuario invitado** para agregar usuarios invitados en Azure ad. Más información: [Inicio rápido: Agregue un nuevo usuario invitado en Azure AD @ no__t-0.
    > [!div class="mx-imgBorder"] 
    > ![Agregar invitado en Azure ad](media/share-app/guest_access_doc_1.png "agregar invitado en Azure ad")
2. Si el usuario invitado todavía no tiene una licencia en su inquilino principal, asigne una licencia al usuario invitado.
   - Para asignar usuarios invitados desde admin.microsoft.com, consulte [asignación de licencias a un usuario](/office365/admin/subscriptions-and-billing/assign-licenses-to-users).
   - Para asignar usuarios invitados desde portal.azure.com, consulte [asignación o eliminación de licencias](/azure/active-directory/fundamentals/license-users-groups).
 
   > [!IMPORTANT]
   > Es posible que tenga que deshabilitar la vista previa del centro de administración de Microsoft 365 para asignar una licencia a un invitado. 

3. Compartir la aplicación Canvas. 
    1. Iniciar sesión en https://make.powerapps.com  
    2. Vaya a **aplicaciones**, seleccione una aplicación de lienzo y, en la barra de comandos, seleccione **compartir**. 
    3. Escriba una dirección de correo electrónico para un usuario invitado de un inquilino de Azure AD. Más información: [¿Qué es el acceso de usuarios invitados en Azure AD B2B?](/azure/active-directory/b2b/what-is-b2b)
          > [!div class="mx-imgBorder"] 
          > ![Compartir con]invitado(media/share-app/guest_access_doc_2.png "compartido con invitado")
 
Después de compartir una aplicación para el acceso de invitado, los invitados pueden detectar y acceder a las aplicaciones compartidas con ellas desde el correo electrónico que se les envía como parte del uso compartido.

> [!div class="mx-imgBorder"]  
> Los invitados reciben el correo electrónico del ![recurso compartido de aplicaciones](media/share-app/guest_access_doc_4.png "recibir correo electrónico del recurso compartido de aplicaciones")

### <a name="frequently-asked-questions"></a>Preguntas más frecuentes

#### <a name="whats-the-difference-between-canvas-app-guest-access-and-powerapps-portals"></a>¿Cuál es la diferencia entre el acceso de invitado de la aplicación de lienzo y los portales de PowerApps? 
Las aplicaciones de lienzo permiten compilar una aplicación, adaptada a la digitalización de procesos empresariales, sin necesidad de escribir código C#en un lenguaje de programación tradicional como. El acceso de invitado para las aplicaciones de canvas permite a los equipos de personas compuestas por diferentes organizaciones que participan en un proceso empresarial común tener acceso a los mismos recursos de la aplicación que se pueden integrar con una amplia variedad de orígenes de Microsoft y de terceros. Más información: [Información general de los conectores de canvas-app para PowerApps](/powerapps/maker/canvas-apps/connections-list).

Los [portales de PowerApps](/powerapps/maker/portals/overview) provide la capacidad de compilar sitios web de bajo código y con capacidad de respuesta que permiten a los usuarios externos interactuar con los datos almacenados en Common Data Service. Permite a las organizaciones crear sitios web que se pueden compartir con usuarios externos a su organización, ya sea de forma anónima o a través del proveedor de inicio de sesión de su elección, como LinkedIn, una cuenta de Microsoft u otros proveedores de inicio de sesión comerciales. 

En la tabla siguiente se describen algunas diferencias de funcionalidad principales entre portales y aplicaciones de lienzo de PowerApps.  

| | Interfaz | Autenticación | Orígenes de datos accesibles |
|------|--------|----------|-------------------|
| Portales de PowerApps | Experiencia solo en explorador | Permite el acceso anónimo y autenticado | Common Data Service |
| Aplicaciones de lienzo | Exploradores y aplicaciones móviles | Requiere autenticación a través de Azure AD | Todos los conectores integrados de ~ 150 y cualquier conector personalizado  |
||

#### <a name="can-guests-access-customized-forms-in-sharepoint"></a>¿Pueden los invitados tener acceso a formularios personalizados en SharePoint?
Sí. Cualquier usuario que pueda acceder a una lista de SharePoint con un formulario personalizado puede crear y editar los elementos de la lista mediante el formulario, sin ninguna licencia de PowerApps.

#### <a name="can-guests-access-apps-embedded-in-sharepoint"></a>¿Pueden los invitados acceder a las aplicaciones incrustadas en SharePoint? 
Sí. Sin embargo, el acceso a las aplicaciones independientes del lienzo requiere una licencia de PowerApps, incluidas las aplicaciones que se insertan. Al insertar una aplicación Canvas en SharePoint a través del control Microsoft PowerApps embed, escriba el identificador de la aplicación. Para ello, escriba el identificador de la aplicación en el cuadro **vínculo Web de la aplicación o identificador** . 

> [!div class="mx-imgBorder"]  
> ![Insertar aplicación de lienzo en SharePoint para invitados](media/share-app/guest_access_doc_5.PNG "Insertar aplicación de lienzo en SharePoint para invitados")

Al incrustar una aplicación de lienzo en SharePoint a través de la etiqueta HTML de iFrame, haga referencia a la aplicación con la dirección URL completa de Web. Para buscar la dirección URL, vaya a http://make.powerapps.com, seleccione una aplicación, seleccione la pestaña **detalles** y la dirección URL se muestra en **vínculo Web**.

> [!div class="mx-imgBorder"]  
> Detalles de la ![aplicación Canvas]detalles de la(media/share-app/guest_access_doc_6.PNG "aplicación Canvas")

#### <a name="how-come-guests-can-launch-the-app-shared-with-them-but-connections-fail-to-be-created"></a>¿Cómo pueden iniciar los invitados la aplicación compartida con ellos, pero no se pueden crear las conexiones?
Al igual que con los no invitados, los orígenes de datos subyacentes a los que tiene acceso la aplicación también deben ser accesibles para el invitado.

#### <a name="what-license-must-be-assigned-to-my-guest-so-they-can-run-an-app-shared-with-them"></a>¿Qué licencia debe asignarse a mi invitado para poder ejecutar una aplicación compartida con ellas?
La misma licencia necesaria para que los usuarios no invitados ejecuten una aplicación. Por ejemplo, si la aplicación no usa los conectables Premium, una licencia de PowerApps P1 es suficiente para asignarla al invitado.  


|                                 | Formulario personalizado de SharePoint | Aplicación de lienzo independiente con conectores no Premium | Aplicación de lienzo independiente con conectores Premium | Aplicación controlada por modelos |
|---------------------------------|----------------------------|----------------------------------------------------|------------------------------------------------|------------------|
| Usuario de SharePoint (sin licencia de PA) | x                          |                                                    |                                                |                  |
| PowerApps incluido en la oficina    | x                          |                                                    |                                                |                  |
| Plan 1 de PowerApps                | x                          | x                                                  |                                                |                  |
| Plan2 de PowerApps                 | x                          | x                                                  | x                                              | x                |

#### <a name="in-powerapps-mobile-how-does-a-guest-see-apps-for-their-home-tenant"></a>En PowerApps Mobile, ¿cómo ven los invitados las aplicaciones de su inquilino principal?
Cualquier usuario que tenga acceso a una aplicación de lienzo, en su dispositivo móvil, que se publique en un inquilino de Azure AD que no sea su inquilino principal debe cerrar la sesión de PowerApps y volver a iniciar sesión en PowerApps Mobile.  

#### <a name="must-a-guest-accept-the-azure-ad-guest-invitation-prior-to-sharing-an-app-with-the-guest"></a>¿Un invitado debe aceptar la invitación Azure AD invitado antes de compartir una aplicación con el invitado?
No. Si un invitado inicia una aplicación compartida con ellos antes de aceptar una invitación de invitado, se solicitará al invitado que acepte la invitación como parte de la experiencia de inicio de sesión mientras se inicia la aplicación.  

#### <a name="what-azure-ad-tenant-are-connections-for-a-guest-user-created-in"></a>¿Qué Azure AD inquilino son las conexiones para un usuario invitado creado en?
Las conexiones para una aplicación siempre se realizan en el contexto del inquilino de Azure AD la aplicación está asociada. Por ejemplo, si se crea una aplicación en el inquilino de Contoso, las conexiones realizadas para los usuarios internos e invitados de Contoso se realizan en el contexto del inquilino de contoso.

#### <a name="can-guests-use-microsoft-graph-via-microsoft-security-graph-connector-or-a-custom-connector-using-microsoft-graph-apis"></a>¿Pueden los invitados usar Microsoft Graph mediante Microsoft Security Graph Connector o un conector personalizado mediante Microsoft Graph API?
No, Azure AD invitados no pueden consultar Microsoft Graph para recuperar información de un inquilino en el que son invitados.

#### <a name="what-intune-policies-apply-to-guests-using-my-powerapps"></a>¿Qué directivas de Intune se aplican a los invitados que usan mi PowerApps?
Intune solo aplica las directivas del inquilino principal de un usuario. Por ejemplo, si Alice@Contoso.com comparte una aplicación con Vikram@Fabrikam.com, Intune seguirá aplicando las directivas de Fabrikam.com en el dispositivo de Virkam independientemente del PowerApps que ejecute.

#### <a name="what-connectors-support-guest-access"></a>¿Qué conectores admiten el acceso de invitado?
Todos los conectores que no realizan Azure AD autenticación de cualquier tipo admiten el acceso de invitado. En la tabla siguiente se enumeran todos los conectores que realizan la autenticación Azure AD y los conectores que admiten actualmente el acceso de invitado. Muchos de ellos se actualizarán a la disponibilidad general.

| **Conectores**                                     | **Admite el acceso de invitado**                                              |
|---------------------------------------------------|------------------------------------------------------------------------|
| 10to8 Appointment Scheduling                      | No                                                                     |
| Adobe Creative Cloud                              | No                                                                     |
| Adobe Sign                                        | No                                                                     |
| Asana                                             | No                                                                     |
| Administrador de AtBot                                       | No                                                                     |
| Lógica de AtBot                                       | No                                                                     |
| Azure AD                                          | Sí                                                                    |
| Azure Automation                                  | Sí                                                                    |
| Instancia de Azure Container                          | Sí                                                                    |
| Azure Data Factory                                | Sí                                                                    |
| Azure Data Lake                                   | Sí                                                                    |
| DevOps de Azure                                      | No                                                                     |
| Azure Event Grid                                  | No                                                                     |
| IoT Central de Azure                                 | Sí                                                                    |
| Azure Key Vault                                   | No                                                                     |
| Kusto de Azure                                       | Sí                                                                    |
| Azure Log Analytics                               | Sí                                                                    |
| Azure Resource Manager                            | Sí                                                                    |
| Basecamp 2                                        | No                                                                     |
| Bitbucket                                         | No                                                                     |
| Bitly                                             | No                                                                     |
| bttn                                              | No                                                                     |
| Buffer                                            | No                                                                     |
| Centro de negocios                                  | No                                                                     |
| CandidateZip                                      | No                                                                     |
| Cápsula CRM                                       | No                                                                     |
| Administración de PKI de nube                              | No                                                                     |
| Cognito Forms                                     | No                                                                     |
| Common Data Service                               | No                                                                     |
| Common Data Service (heredado)                      | No                                                                     |
| Optimizador D & B                                     | No                                                                     |
| Derdack convierte SIGNL4                                    | No                                                                     |
| Disqus                                            | No                                                                     |
| Combinación de documentos                                    | No                                                                     |
| Dynamics 365                                      | No                                                                     |
| Dynamics 365 AI para ventas                         | Sí                                                                    |
| Dynamics 365 para operaciones de fin &                        | No                                                                     |
| Enadoc                                            | No                                                                     |
| Eventbrite                                        | No                                                                     |
| Excel online (Business)                           | No                                                                     |
| Excel online (OneDrive)                           | No                                                                     |
| Recordatorio de expiración                               | No                                                                     |
| FreshBooks                                        | No                                                                     |
| GoToMeeting                                       | No                                                                     |
| GoToTraining                                      | No                                                                     |
| GoToWebinar                                       | No                                                                     |
| Harvest                                           | No                                                                     |
| HTTP con Azure AD                                | No                                                                     |
| Infusionsoft                                      | No                                                                     |
| Inoreader                                         | No                                                                     |
| Intercom                                          | No                                                                     |
| JotForm                                           | No                                                                     |
| kintone                                           | No                                                                     |
| LinkedIn                                          | No                                                                     |
| Centro de contenido de marketing                             | No                                                                     |
| Mediana                                            | No                                                                     |
| Metatarea                                          | No                                                                     |
| Microsoft Forms                                   | No                                                                     |
| Microsoft Forms Pro                               | No                                                                     |
| Seguridad de Microsoft Graph                          | No                                                                     |
| Microsoft Kaizala                                 | No                                                                     |
| Microsoft School Data Sync                        | No                                                                     |
| Microsoft StaffHub                                | No                                                                     |
| Microsoft Teams                                   | Sí                                                                    |
| Microsoft to-do (Business)                        | No                                                                     |
| Muhimbi PDF                                       | No                                                                     |
| NetDocuments                                      | No                                                                     |
| Office 365 Groups                                 | Sí                                                                    |
| Office 365 Outlook                                | No                                                                     |
| Usuarios de Office 365                                  | Sí                                                                    |
| Office 365 Video                                  | No                                                                     |
| OneDrive                                          | No                                                                     |
| OneDrive para la Empresa                             | No                                                                     |
| OneNote (empresas)                                | No                                                                     |
| Outlook Customer Manager                          | No                                                                     |
| Tareas de Outlook                                     | Sí                                                                    |
| Outlook.com                                       | No                                                                     |
| Paylocity                                         | No                                                                     |
| Planner                                           | No                                                                     |
| Formularios de Plumsail                                    | No                                                                     |
| Power BI                                          | Sí                                                                    |
| Project Online                                    | No                                                                     |
| Integración del diseño de ProjectWise                    | No                                                                     |
| Recurso compartido ProjectWise                                 | No                                                                     |
| SharePoint                                        | Sí                                                                    |
| SignNow                                           | No                                                                     |
| Skype empresarial online                         | No                                                                     |
| Soft1                                             | No                                                                     |
| Stormboard                                        | No                                                                     |
| Survey123                                         | No                                                                     |
| SurveyMonkey                                      | No                                                                     |
| Toodledo                                          | No                                                                     |
| Typeform                                          | No                                                                     |
| Vimeo                                             | No                                                                     |
| Equipos de WebEx                                       | No                                                                     |
| Protección contra amenazas avanzada de Windows Defender (ATP) | No                                                                     |
| Word online (empresa)                            | No                                                                     |
