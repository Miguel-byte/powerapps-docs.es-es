---
title: Referencia de la plantilla de pantalla de reunión para aplicaciones de Canvas | Microsoft Docs
description: Información detallada sobre cómo funciona la plantilla de pantalla de reunión para las aplicaciones de canvas en PowerApps
author: emcoope-msft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: tapanm
ms.date: 01/03/2019
ms.author: emcoope
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: c62c3de56534201a81e9f4d453796ebd9b3a0366
ms.sourcegitcommit: 7dae19a44247ef6aad4c718fdc7c68d298b0a1f3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/07/2019
ms.locfileid: "71989569"
---
# <a name="reference-information-about-the-meeting-screen-template-for-canvas-apps"></a>Información de referencia sobre la plantilla de pantalla de reunión para las aplicaciones de Canvas

En el caso de las aplicaciones de canvas en PowerApps, comprenda cómo contribuye cada control significativo de la plantilla de pantalla de reunión a la funcionalidad predeterminada general de la pantalla. Esta profundización presenta las fórmulas de comportamiento y los valores de otras propiedades que determinan cómo responden los controles a los datos proporcionados por el usuario. Para obtener una descripción de alto nivel de la funcionalidad predeterminada de esta pantalla, consulte [información general sobre la pantalla](meeting-screen-overview.md)de la reunión.

En este tema se resaltan algunos controles significativos y se explican las expresiones o fórmulas en las que se establecen varias propiedades (como **Items** y **alseleccionar**) de estos controles:

* [Pestaña invitar (LblInviteTab)](#invite-tab)
* [Pestaña programación (LblScheduleTab)](#schedule-tab)
* [Cuadro de búsqueda de texto](#text-search-box)
* [Icono Agregar (AddIcon)](#add-icon)
* [Galería de exploración de personas](#people-browse-gallery) (+ controles secundarios)
* [Galería de personas](#meeting-people-gallery) de la reunión (+ controles secundarios)
* [Selector de fecha de reunión (MeetingDateSelect)](#meeting-date-picker)
* [Lista desplegable duración de la reunión (MeetingDurationSelect)](#meeting-duration-drop-down)
* [Buscar la galería de horas de reunión](#find-meeting-times-gallery) (+ controles secundarios)
* [Galería de exploración de salón](#room-browse-gallery) (+ controles secundarios)
* [Cheurón atrás (RoomsBackNav)](#back-chevron) (puede que no esté visible si el inquilino no tiene listas de salones)
* [Icono de envío](#send-icon)

## <a name="prerequisite"></a>Requisito previo

Está familiarizado con cómo agregar y configurar pantallas y otros controles a medida que [crea una aplicación en PowerApps](../data-platform-create-app-scratch.md).

## <a name="invite-tab"></a>Pestaña invitar

   ![Control LblInviteTab](media/meeting-screen/meeting-invite-text.png)

* Propiedad **Color**<br>
    Valor: `If( _showDetails, LblRecipientCount.Color, RectQuickActionBar.Fill )`

    **_showDetails** es una variable que se usa para determinar si se ha seleccionado el control **LblInviteTab** o el control **LblScheduleTab** . Si el valor de **_showDetails** es **true**, **LblScheduleTab** está seleccionado; Si el valor es **false**, se selecciona **LblInviteTab** . Esto significa que si el valor de **_showDetails** es **true** (esta pestaña *no está* seleccionada), el color de la pestaña coincide con el de **LblRecipientCount**. De lo contrario, coincide con el valor de relleno de **RectQuickActionBar**.

* Propiedad **Alseleccionar**<br> 
    Valor: `Set( _showDetails, false )`

    Establece la variable **_showDetails** en **false**, lo que significa que el contenido de la pestaña invite está visible y el contenido de la pestaña **Schedule** está oculto.

## <a name="schedule-tab"></a>Pestaña programación

   ![Control LblInviteTab](media/meeting-screen/meeting-schedule-text.png)

* Propiedad **Color**<br>
    Valor: `If( !_showDetails, LblRecipientCount.Color, RectQuickActionBar.Fill )`

    **_showDetails** es una variable que se usa para determinar si se ha seleccionado el control **LblInviteTab** o el control **LblScheduleTab** . Si es true, **LblScheduleTab** está seleccionado; Si es false, **LblInviteTab** es. Esto significa que, si **_showDetails** es true (esta pestaña *está* seleccionada), el color de la pestaña coincide con el valor de relleno de **RectQuickActionBar**. De lo contrario, coincide con el valor de color de **LblRecipientCount**.

* Propiedad **Alseleccionar**<br>
    Valor: `Set( _showDetails, true )`

    Establece la variable **_showDetails** en **true**, lo que significa que el contenido de la pestaña programación es visible y el contenido de la pestaña invite está oculto.

## <a name="text-search-box"></a>Cuadro de búsqueda de texto

   ![Control TextSearchBox](media/meeting-screen/meeting-search-box.png)

<!--Include description of text search box control?-->

Otros controles de la pantalla dependen de este:

* Si un usuario comienza a escribir cualquier texto, **PeopleBrowseGallery** se vuelve visible.
* Si un usuario escribe una dirección de correo electrónico válida, **AddIcon** se vuelve visible.
* Cuando un usuario selecciona una persona dentro de **PeopleBrowseGallery** , se restablece el contenido de la búsqueda.

## <a name="add-icon"></a>Icono Agregar

   ![Control AddIcon](media/email-screen/email-add-icon.png)

Este control permite a los usuarios agregar personas que no existen dentro de su organización a la lista de asistentes para la reunión que se va a componer.

* Propiedad **Estarán**<br>
    Valor Tres comprobaciones lógicas que deben evaluarse como **true** para que el control sea visible:

    ```powerapps-dot
    !IsBlank( TextSearchBox.Text ) &&
        IsMatch( TextSearchBox.Text, Match.Email ) &&
        Not( Trim( TextSearchBox.Text ) in MyPeople.UserPrincipalName )
    ```

  Línea por línea, este bloque de código indica que el control **AddIcon** solo está visible si:

  * **TextSearchBox** contiene texto.
  * El texto de **TextSearchBox** es una dirección de correo electrónico válida.
  * El texto de **TextSearchBox** ya no existe en la colección **People** .

* Propiedad **Alseleccionar**<br> 
    Valor Una instrucción **Collect** para agregar el usuario a la lista de asistentes, otra para actualizar las horas de reunión disponibles y varios alternancias de variables:

    ```powerapps-dot
    Collect( MyPeople,
        { 
            DisplayName: TextSearchBox.Text, 
            UserPrincipalName: TextSearchBox.Text, 
            Mail: TextSearchBox.Text
        }
    );
    Concurrent(
        Reset( TextSearchBox ),
        Set( _showMeetingTimes, false ),
        UpdateContext( { _loadMeetingTimes: true } ),
        Set( _selectedMeetingTime, Blank() ),
        Set( _selectedRoom, Blank() ),
        Set( _roomListSelected, false ),
        ClearCollect( MeetingTimes, 
            AddColumns(
                'Office365'.FindMeetingTimes(
                    { 
                        RequiredAttendees: Concat(MyPeople, UserPrincipalName & ";")
                        MeetingDuration: MeetingDurationSelect.Selected.Minutes,
                        Start: Text( DateAdd( MeetingDateSelect.SelectedDate, 8, Hours ), UTC ),
                        End: Text( DateAdd( MeetingDateSelect.SelectedDate, 17, Hours ), UTC ),
                        MaxCandidates: 15, 
                        MinimumAttendeePercentage:1, 
                        IsOrganizerOptional: false, 
                        ActivityDomain: "Work"
                    }
                ).MeetingTimeSuggestions,
                "StartTime", MeetingTimeSlot.Start.DateTime, 
                "EndTime", MeetingTimeSlot.End.DateTime
            )
        )
    );
    UpdateContext( { _loadingMeetingTimes: false } );
    Set( _showMeetingTimes, true )
    ```

  Al seleccionar este control, se agrega la dirección de correo electrónico válida (solo es visible si se escribe una dirección de correo electrónico válida en **TextSearchBox**) en la colección **People** (esta colección es la lista de asistentes) y, a continuación, se actualizan las horas de reunión disponibles con la nueva entrada de usuario.

  En un nivel bajo, este bloque de código:
  1. Recopila la dirección de correo electrónico en la colección **People** , recopilando la dirección de correo electrónico en los campos **displayName**, **UserPrincipalName**y **mail** .
  1. Restablece el contenido del control **TextSearchBox** .
  1. Establece la variable **_showMeetingTimes** en **false**. Esta variable controla la visibilidad de **FindMeetingTimesGallery**, que muestra las horas abiertas que los asistentes seleccionados deben cumplir.
  1. Establece la variable de contexto **_loadMeetingTimes** en **true**. Esta variable establece un estado de carga, que alterna la visibilidad de los controles de estado de carga como **_LblTimesEmptyState** para indicar al usuario que se están cargando sus datos.
  1. Establece **_selectedMeetingTime** en **Blank ()** . **_selectedMeetingTime** es el registro seleccionado del control **FindMeetingTimesGallery** . Está en blanco aquí porque la adición de otro asistente podría significar que la definición anterior de **_selectedMeetingTime** no está disponible para ese asistente.
  1. Establece **_selectedRoom** en **Blank ()** . **_selectedRoom** es el registro de salón seleccionado de **RoomBrowseGallery**. Las disponibilidades de salón se determinan a partir del valor de **_selectedMeetingTime**. Con ese valor en blanco, el valor de **_selectedRoom** ya no es válido, por lo que debe estar en blanco.
  1. Establece **_roomListSelected** en **false**. Es posible que esta línea no sea aplicable a todos los usuarios. En Office, puede agrupar sus salones por diferentes "listas de salones". Si tiene listas de salas, esta pantalla cuenta para eso, lo que le permite seleccionar primero una lista de salas antes de seleccionar una sala de esa lista. El valor de **_roomListSelected** es lo que determina si un usuario (en un inquilino con listas de habitación solo) estará viendo los salones en una lista de salas o en el conjunto de listas de salas. Se establece en **false** para obligar a los usuarios a volver a seleccionar una nueva lista de salones.
  1. Usa la operación [Office365. FindMeetingTimes](https://docs.microsoft.com/connectors/office365/#find-meeting-times) para determinar y recopilar las horas de reunión disponibles para los asistentes. Esta operación pasa:
      * El **UserPrincipalName** de cada usuario seleccionado en el parámetro *RequiredAttendees* .
      * **MeetingDurationSelect**. Seleccionado. minutes en el parámetro *MeetingDuration* .
      * MeetingDateSelect. SelectedDate + 8 horas en el parámetro de *Inicio* . Se agregan ocho horas porque, de forma predeterminada, la fecha y hora completas del control de calendario es 12:00 A.M. de la fecha seleccionada. Probablemente quiera recuperar las disponibilidades en las horas de trabajo normales. Una hora de inicio de trabajo normal sería de 8:00 A.M.
      * **MeetingDateSelect**. SelectedDate + 17 horas en el parámetro *End* . se agregan 17 horas porque 12:00 AM + 17 = 5:00 PM. Una hora de finalización de trabajo normal sería 5:00 PM.
      * *15* en el parámetro *MaxCandidates* . Esto significa que la operación devuelve solo las 15 horas disponibles principales para la fecha seleccionada. Esto tiene sentido porque solo hay fragmentos de 16 30 minutos en un día de trabajo de 8 horas y una reunión de 30 minutos es el mínimo que se puede establecer en esta pantalla.
      * *1* en el parámetro *MinimumAttendeePercentage* . Esencialmente, a menos que no haya ningún asistente disponible, se recupera la hora de la reunión.
      * **false** en el parámetro *IsOrganizerOptional* . El usuario de la aplicación no es un asistente opcional para esta reunión.
      * "Work" en el parámetro *ActivityDomain* . Esto significa que las horas recuperadas son solo las de un período de tiempo de trabajo normal.
  1. La función **ClearCollect** también agrega dos columnas: "StartTime" y "EndTime". Esto simplifica los datos devueltos. 
  El campo que contiene las horas de inicio y finalización disponibles es el campo **MeetingTimeSlot** . Este campo es un registro que contiene los registros inicial y final, que contienen los valores **DateTime** y **TimeZone** de su sugerencia correspondiente. En lugar de intentar recuperar este anidamiento de registros, al agregar las columnas "StartTime" y "EndTime" a la colección **MeetingTimes** , los valores **Start > datetime** y **End > DateTime** se convierten en la superficie de la colección.
  1. Una vez completadas todas estas funciones, la variable **_loadingMeetingTimes** se establece en **false**, se quita el estado de carga y **_showMeetingTimes** se establece en **true**, lo que muestra **FindMeetingTimesGallery**.

## <a name="people-browse-gallery"></a>Galería de exploración de personas

   ![Control PeopleBrowseGallery](media/meeting-screen/meeting-browse-gall.png)

* Propiedad **Elementos**<br>
    Valor 
    ```powerapps-dot
    If( !IsBlank( Trim( TextSearchBox.Text ) ), 
        'Office365Users'.SearchUser( { searchTerm: Trim(TextSearchBox.Text), top: 15 } )
    )
    ```

Los elementos de esta galería se rellenan con los resultados de búsqueda de la operación [Office365. SearchUser](https://docs.microsoft.com/connectors/office365users/#searchuser) . La operación toma el texto de `Trim(**TextSearchBox**)` como término de búsqueda y devuelve los 15 resultados principales en función de la búsqueda.
  
**TextSearchBox** está encapsulado en una función **Trim** porque un usuario que busca espacios no es válido. La operación `Office365Users.SearchUser` se encapsula en una función `If(!IsBlank(Trim(TextSearchBox.Text)) ... )` porque la recuperación de los resultados de la búsqueda antes de que un usuario haya buscado es un desperdicio de rendimiento.

### <a name="people-browse-gallery-title"></a>Título de la galería de exploración de personas

   ![Control de título de PeopleBrowseGallery](media/meeting-screen/meeting-browse-gall-title.png)

* Propiedad **Texto**<br>
    Valor: `ThisItem.DisplayName`

    Muestra el nombre para mostrar de la persona de su perfil de Office 365.

* Propiedad **Alseleccionar**<br>
    Valor Una instrucción **Collect** para agregar el usuario a la lista de asistentes, otra para actualizar las horas de reunión disponibles y varios alternancias de variables:

    ```powerapps-dot
    Concurrent(
        Reset( TextSearchBox ),
        Set( _selectedUser, ThisItem ),
        If( Not( ThisItem.UserPrincipalName in MyPeople.UserPrincipalName ), 
            Collect( MyPeople, ThisItem ); 
            Concurrent(
                Set( _showMeetingTimes, false ),
                UpdateContext( { _loadMeetingTimes: true } ),
                Set( _selectedMeetingTime, Blank() ),
                Set( _selectedRoom, Blank() ),
                Set( _roomListSelected, false ),
                ClearCollect( MeetingTimes, 
                    AddColumns(
                        'Office365'.FindMeetingTimes(
                            {
                                RequiredAttendees: Concat( MyPeople, UserPrincipalName & ";" ),
                                MeetingDuration: MeetingDurationSelect.Selected.Minutes,
                                Start: Text( DateAdd( MeetingDateSelect.SelectedDate, 8, Hours ), UTC ),
                                End: Text( DateAdd( MeetingDateSelect.SelectedDate, 17, Hours ), UTC ),
                                MaxCandidates: 15, 
                                MinimumAttendeePercentage: 1, 
                                IsOrganizerOptional: false, 
                                ActivityDomain: "Work"
                            }
                        ).MeetingTimeSuggestions,
                        "StartTime", MeetingTimeSlot.Start.DateTime, 
                        "EndTime", MeetingTimeSlot.End.DateTime
                    )
                )
            );
            UpdateContext( { _loadingMeetingTimes: false } );
            Set( _showMeetingTimes, true )
        )
    )
    ```

    En un nivel alto, al seleccionar este control se agrega la persona a la colección **People** (el almacenamiento de la aplicación de la lista de asistentes) y se actualizan las horas de reunión disponibles en función de la nueva adición de usuarios.

    La selección de este control es muy similar a la selección del control **AddIcon** . la única diferencia es que la instrucción `Set(_selectedUser, ThisItem)` y el orden de ejecución de las operaciones. Como tal, este debate no será tan profundo. Para obtener una explicación más completa, lea la sección sobre el [control AddIcon](#add-icon) .

    Al seleccionar este control se restablece **TextSearchBox**. Después, si la selección no está en la colección **People** , el control:
    1. Establece el estado **_loadMeetingTimes** en **true** y el estado **_showMeetingTimes** en **false**, en blanco las variables **_selectedMeetingTime** y **_selectedRoom** y actualiza el **MeetingTimes** colección con la nueva adición a la colección **People** . 
    1. Establece el estado de **_loadMeetingTimes** en **false**y establece **_showMeetingTimes** en **true**. Si la selección ya está en la colección **People** , solo restablece el contenido de **TextSearchBox**.

## <a name="meeting-people-gallery"></a>Galería de reuniones de personas

   ![Control MeetingPeopleGallery](media/meeting-screen/meeting-people-gall.png)

* Propiedad **Elementos**<br>
    Valor: `MyPeople`

    La **colección People es la colección de** personas inicializadas o agregadas a seleccionando el control de **título PeopleBrowseGallery** .

* Propiedad **Alto**<br>
    Valor Lógica para permitir que la Galería crezca hasta un alto máximo de 350:

    ```powerapps-dot
    Min( 
        76 * RoundUp( CountRows( MeetingPeopleGallery.AllItems ) / 2, 0 ),
        350
    )
    ```

  
   El alto de esta galería se ajusta al número de elementos de la galería, con un alto máximo de 350. La fórmula toma 76 como alto de una sola fila de **MeetingPeopleGallery**y, a continuación, lo multiplica por el número de filas. La propiedad **WrapCount** se establece en 2, por lo que el número de filas verdaderas es `RoundUp(CountRows(MeetingPeopleGallery.AllItems) / 2, 0)`.

* Propiedad **ShowScrollbar**<br>
    Valor: `MeetingPeopleGallery.Height >= 350`

    Cuando se alcanza el alto máximo de la galería (350), la barra de desplazamiento está visible.

### <a name="meeting-people-gallery-title"></a>Título de la galería de personas de reuniones

   ![Control de título de MeetingPeopleGallery](media/meeting-screen/meeting-people-gall-title.png)

* Propiedad **Alseleccionar**<br>
    
    Valor: `Set(_selectedUser, ThisItem)`
    
    Establece la variable **_selectedUser** en el elemento seleccionado en **MeetingPeopleGallery**.

### <a name="meeting-people-gallery-iconremove"></a>Galería de reuniones iconRemove

   ![Control MeetingPeopleGallery iconRemove](media/meeting-screen/meeting-people-gall-delete.png)

* Propiedad **Alseleccionar**<br>
    Valor Una instrucción **Remove** para quitar el usuario de la lista de asistentes, una instrucción **Collect** para actualizar las horas de reunión disponibles y varios alternancias de variables:

    ```powerapps-dot
    Remove( MyPeople, LookUp( MyPeople, UserPrincipalName = ThisItem.UserPrincipalName ) );
    Concurrent(
        Reset( TextSearchBox ),
        Set( _showMeetingTimes, false ),
        UpdateContext( { _loadMeetingTimes: true } ),
        Set( _selectedMeetingTime, Blank() ),
        Set( _selectedRoom, Blank() ),
        Set( _roomListSelected, false ),
        ClearCollect( MeetingTimes, 
            AddColumns(
                'Office365'.FindMeetingTimes(
                    {
                        RequiredAttendees: Concat( MyPeople, UserPrincipalName & ";" ), 
                        MeetingDuration: MeetingDurationSelect.Selected.Minutes,
                        Start: Text( DateAdd( MeetingDateSelect.SelectedDate, 8, Hours ), UTC ), 
                        End: Text( DateAdd( MeetingDateSelect.SelectedDate, 17, Hours ), UTC ),
                        MaxCandidates: 15, 
                        MinimumAttendeePercentage: 1, 
                        IsOrganizerOptional: false, 
                        ActivityDomain: "Work"
                    }
                ).MeetingTimeSuggestions,
                "StartTime", MeetingTimeSlot.Start.DateTime, 
                "EndTime", MeetingTimeSlot.End.DateTime
            )
        )
    );
    UpdateContext( { _loadingMeetingTimes: false } );
    Set( _showMeetingTimes, true )
    ```

  En un nivel alto, al seleccionar este control se quita la persona de la lista de asistentes y se actualizan las horas de reunión disponibles en función de la eliminación de esta persona.

  Después de la primera línea del código anterior, la selección de este control es casi idéntica a seleccionar el control **AddIcon** . Como tal, este debate no será tan profundo. Para obtener una explicación más completa, lea la sección sobre el [control AddIcon](#add-icon).

  En la primera línea de código, el elemento seleccionado se quita de la colección **People** . Después, el código:
  1. Restablece **TextSearchBox**y, a continuación, quita la selección de la colección **People** . 
  1. Establece el estado **_loadMeetingTimes** en **true** y el estado **_showMeetingTimes** en **false**, en blanco las variables **_selectedMeetingTime** y **_selectedRoom** y actualiza el **MeetingTimes** colección con la nueva adición a la colección **People** . 
  1. Establece el estado de **_loadMeetingTimes** en **false**y establece **_showMeetingTimes** en **true**.

## <a name="meeting-date-picker"></a>Selector de fecha de reunión

   ![Control MeetingDateSelect](media/meeting-screen/meeting-datepicker.png)

* Propiedad **DisplayMode**<br>
    Valor: `If( IsEmpty(MyPeople), DisplayMode.Disabled, DisplayMode.Edit )`

    No se puede elegir una fecha para una reunión hasta que se haya agregado al menos un asistente a la colección **People** .

* Propiedad **OnChange**<br>
    Valor: `Select( MeetingDateSelect )`

    Al cambiar la fecha seleccionada, se desencadena el código de la propiedad **alseleccionar** de este control para que se ejecute.

* Propiedad **Alseleccionar**<br>
    Valor Una instrucción **Collect** para actualizar las horas de reunión disponibles y varios alternancias de variables:
  
    ```powerapps-dot
    Concurrent(
        Reset( TextSearchBox ),
        Set( _showMeetingTimes, false ),
        UpdateContext( { _loadingMeetingTimes: true } ),
        Set( _selectedMeetingTime, Blank() ),
        Set( _selectedRoom, Blank() ),
        Set( _roomListSelected, false ),
        ClearCollect( MeetingTimes, 
            AddColumns(
                'Office365'.FindMeetingTimes(
                    {
                        RequiredAttendees: Concat( MyPeople, UserPrincipalName & ";" ), 
                        MeetingDuration: MeetingDurationSelect.Selected.Minutes,
                        Start: Text( DateAdd( MeetingDateSelect.SelectedDate, 8, Hours ), UTC ), 
                        End: Text( DateAdd( MeetingDateSelect.SelectedDate, 17, Hours ), UTC ),
                        MaxCandidates: 15, 
                        MinimumAttendeePercentage: 1, 
                        IsOrganizerOptional: false, 
                        ActivityDomain: "Work"
                    }
                ).MeetingTimeSuggestions,
                "StartTime", MeetingTimeSlot.Start.DateTime, 
                "EndTime", MeetingTimeSlot.End.DateTime
            )
        )
    );
    UpdateContext( { _loadingMeetingTimes: false } );
    Set( _showMeetingTimes, true )
    ```

  En un nivel alto, al seleccionar este control se actualizan las horas de reunión disponibles. Es muy útil porque, si un usuario cambia la fecha, las horas de reunión disponibles deben actualizarse para reflejar la disponibilidad de los asistentes durante ese día.

  A excepción de la instrucción **Collect** inicial, es idéntica a la funcionalidad **alseleccionar** del control **AddIcon** . Como tal, este debate no será tan profundo. Para obtener una explicación más completa, lea la sección sobre el [control AddIcon](#add-icon) .

  Al seleccionar este control se restablece **TextSearchBox**. A continuación: 
  1. Establece el estado **_loadMeetingTimes** en **true** y el estado **_showMeetingTimes** en **false**, en blanco las variables **_selectedMeetingTime** y **_selectedRoom** y actualiza el **MeetingTimes** colección con la nueva selección de fecha. 
  1. Establece el estado de **_loadMeetingTimes** en **false**y establece **_showMeetingTimes** en **true**.

## <a name="meeting-duration-drop-down"></a>Lista desplegable duración de la reunión

   ![Control MeetingDateSelect](media/meeting-screen/meeting-timepicker.png)

* Propiedad **DisplayMode**<br>
    Valor: `If( IsEmpty(MyPeople), DisplayMode.Disabled, DisplayMode.Edit )`

    No se puede elegir una duración para una reunión hasta que al menos un asistente se haya agregado a la colección de mis **personas** .

* Propiedad **OnChange**<br>
    Valor: `Select(MeetingDateSelect1)`

    Al cambiar la duración seleccionada, se desencadena el código de la propiedad **alseleccionar** del control **MeetingDateSelect** para que se ejecute.

## <a name="find-meeting-times-gallery"></a>Buscar la galería de horarios de reunión

   ![Control FindMeetingTimesGallery](media/meeting-screen/meeting-time-gall.png)

* Propiedad **Elementos**<br>
    Valor: `MeetingTimes`

    Colección de horas de reunión potenciales recuperada de la operación de [Office365. FindMeetingTimes](https://docs.microsoft.com/connectors/office365/#find-meeting-times) .

* Propiedad **Estarán**<br>
    Valor: `_showMeetingTimes && _showDetails && !IsEmpty( MyPeople )`

    La Galería solo es visible si **_showMeetingTimes** está establecido en **true**, el usuario ha seleccionado el control **LblScheduleTab** y se ha agregado al menos un asistente a la reunión.

### <a name="find-meeting-times-gallery-title"></a>Título de la Galería buscar horas de reunión

   ![Control de título de FindMeetingTimesGallery](media/meeting-screen/meeting-time-gall-title.png)

* Propiedad **Texto**<br>
    Valor Conversión de la hora de inicio que se va a mostrar en la hora local del usuario:

    ```powerapps-dot
    Text(
        DateAdd(
            DateTimeValue( ThisItem.StartTime ),
            - TimeZoneOffset(), 
            Minutes
        ),
        DateTimeFormat.ShortTime
    )
    ```

  El valor recuperado de **startTime** está en formato UTC. Para [convertir la hora UTC a la hora local](../functions/function-dateadd-datediff.md#converting-from-utc), se aplica la función **DateAdd** .
  La [función Text](../functions/function-text.md#datetime) toma una fecha y hora como primer argumento y la da formato según su segundo argumento. Le pasa la conversión de hora local de **ThisItem. startTime**y la muestra como **DateTimeFormat. ShortTime**.

* Propiedad **Alseleccionar**<br>
    Valor Varias instrucciones **Collect** para recopilar salas de reuniones y sus sugerencias de disponibilidad, así como varias alternancias de variables:

    ```powerapps-dot
    Set( _selectedMeetingTime, ThisItem );
    UpdateContext( { _loadingRooms: true } );
    If( IsEmpty( RoomsLists ),
        ClearCollect( RoomsLists, 'Office365'.GetRoomLists().value) );
    If( CountRows( RoomsLists ) <= 1,
        Set( _noRoomLists, true );
        ClearCollect( AllRooms, 'Office365'.GetRooms().value );
        Set( _allRoomsConcat, Concat( FirstN( AllRooms, 20 ), Address & ";" ) );
        ClearCollect( RoomTimeSuggestions, 
            'Office365'.FindMeetingTimes(
                {
                    RequiredAttendees: _allRoomsConcat, 
                    MeetingDuration: MeetingDurationSelect.Selected.Minutes,
                    Start: _selectedMeetingTime.StartTime & "Z", 
                    End: _selectedMeetingTime.EndTime & "Z", 
                    MinimumAttendeePercentage: "1",
                    IsOrganizerOptional: "false", 
                    ActivityDomain: "Unrestricted"
                }
            ).MeetingTimeSuggestions
        );
        ClearCollect( AvailableRooms, 
            AddColumns(
                AddColumns(
                    Filter( 
                        First( RoomTimeSuggestions ).AttendeeAvailability,
                        Availability="Free"
                    ), 
                    "Address", Attendee.EmailAddress.Address
                ), 
                "Name", LookUp( AllRooms, Address = Attendee.EmailAddress.Address ).Name 
            )
        );
        ClearCollect( AvailableRoomsOptimal, 
            DropColumns(
                DropColumns( AvailableRooms, "Availability" ), 
                "Attendee" 
            )
        ),
        Set( _roomListSelected, false) 
    );
    UpdateContext( {_loadingRooms: false} )
    ```

  En un nivel alto, este bloque de código recopila los salones disponibles para los usuarios que no tienen listas de salones, en función de la fecha y hora seleccionadas para la reunión. De lo contrario, simplemente recupera las listas de salones.

  En un nivel bajo, este bloque de código:
  1. Establece **_selectedMeetingTime** en el elemento seleccionado. Se usa para averiguar qué salones están disponibles en ese momento.
  1. Establece la variable de estado de carga **_loadingRooms** en **true**, lo que activa el estado de carga.
  1. Si la colección **RoomsLists** está vacía, recupera las listas de salones de tenant's del usuario y las almacena en la colección **RoomsLists** .
  1. Si el usuario no tiene una lista de salones o una lista de salas:
      1. La variable **noRoomLists** se establece en **true**y esta variable se usa para determinar los elementos que se muestran en el control **RoomBrowseGallery** .
      1. La operación `Office365.GetRooms()` se usa para recuperar las primeras 100 salas de su inquilino. Estos se almacenan en la colección **AllRooms** .
      1. La variable **_allRoomsConcat** se establece en una cadena separada por punto y coma de las 20 primeras direcciones de correo electrónico de los salones de la colección **AllRooms** . Esto se debe a que [Office365. FindMeetingTimes](https://docs.microsoft.com/connectors/office365/#find-meeting-times) está limitado a buscar las horas disponibles de 20 objetos Person en una sola operación.
      1. La colección **RoomTimeSuggestions** usa [Office365. FindMeetingTimes](https://docs.microsoft.com/connectors/office365/#find-meeting-times) para recuperar la disponibilidad de los 20 primeros salones de la colección **AllRooms** , en función de los valores de tiempo de la variable **_selectedMeetingTime** . Tenga en cuenta que el `& "Z"` se usa para dar formato correctamente al valor **DateTime** .
      1. Se crea la colección **AvailableRooms** . Esto es simplemente la colección **RoomTimeSuggestions** de la disponibilidad de los asistentes con dos columnas adicionales agregadas: "Address" y "Name". "Address" es la dirección de correo electrónico de la habitación y "Name" es el nombre de la habitación.
      1. A continuación, se crea la colección **AvailableRoomsOptimal** . Esta es solo la colección **AvailableRooms** con las columnas "Availability" y "attendees" quitadas. Esto coincide con los esquemas de **AvailableRoomsOptimal** y **AllRooms**. Esto le permite usar ambas colecciones en la propiedad **Items** de **RoomBrowseGallery**.
      1. **_roomListSelected** está establecido en **false**.
  1. El estado de carga, **_loadingRooms**, se establece en **false** una vez que todo lo demás ha terminado de ejecutarse.

## <a name="room-browse-gallery"></a>Galería de exploración de salón

   ![Control RoomBrowseGallery](media/meeting-screen/meeting-rooms-gall.png)

* Propiedad **Elementos**<br>
    Valor Se establece lógicamente en dos colecciones internas de esquema idéntico, en función de si el usuario ha seleccionado una lista de salas o tiene listas de salones en su inquilino:

    ```powerapps-dot
    Search(
        If( _roomListSelected || _noRoomLists, AvailableRoomsOptimal, RoomsLists ),
        Trim(TextMeetingLocation1.Text), 
        "Name", 
        "Address"
    )
    ```

  Esta galería muestra la colección **AvailableRoomsOptimal** si **_roomListSelected** o **_noRoomLists** es **true**. De lo contrario, muestra la colección **RoomsLists** . Esto puede hacerse porque el esquema de estas colecciones es idéntico.

* Propiedad **Estarán**<br>
    Valor: ```_showDetails && !IsBlank( _selectedMeetingTime ) && !_loadingRooms```

    La Galería solo es visible si las tres instrucciones anteriores se evalúan como **true**.

### <a name="roombrowsegallery-title"></a>Título de RoomBrowseGallery

   ![Control de título de RoomBrowseGallery](media/meeting-screen/meeting-rooms-gall-title.png)

* Propiedad **Alseleccionar**<br>
    Valor Conjunto de instrucciones **Collect** y **set** enlazadas lógicamente, que pueden o no desencadenarse, en función de si el usuario está viendo listas o salones de habitación:

    ```powerapps-dot
    UpdateContext( { _loadingRooms: true } );
    If( !_roomListSelected && !noRoomLists,
        Set( _roomListSelected, true );
        Set( _selectedRoomList, ThisItem.Name );
        ClearCollect( AllRooms, 'Office365'.GetRoomsInRoomList( ThisItem.Address ).value );
        Set( _allRoomsConcat, Concat( FirstN( AllRooms, 20 ), Address & ";" ) );
        ClearCollect( RoomTimeSuggestions, 
            'Office365'.FindMeetingTimes(
                {
                    RequiredAttendees: _allRoomsConcat, 
                    MeetingDuration: MeetingDurationSelect.Selected.Minutes,
                        Start: _selectedMeetingTime.StartTime & "Z", 
                    End: _selectedMeetingTime.EndTime & "Z", 
                    MinimumAttendeePercentage: "1",
                    IsOrganizerOptional: "false", 
                    ActivityDomain: "Unrestricted"
                }
            ).MeetingTimeSuggestions
        );
        ClearCollect( AvailableRooms, 
            AddColumns(
                AddColumns(
                    Filter(
                        First( RoomTimeSuggestions ).AttendeeAvailability, 
                        Availability = "Free"
                    ),
                    "Address", Attendee.EmailAddress.Address 
                ), 
                "Name", LookUp( AllRooms, Address = Attendee.EmailAddress.Address ).Name
            )
        );
        ClearCollect( AvailableRoomsOptimal, 
            DropColumns(
                DropColumns( AvailableRooms, "Availability" )
            ), 
            "Attendee" )
        ),
        Set( _selectedRoom, ThisItem )
    );
    UpdateContext( {_loadingRooms: false} )
    ```

  Las acciones que se producen cuando se selecciona este control dependen de si un usuario está viendo actualmente un conjunto de listas de salas o un conjunto de salones. Si es el primero, al seleccionar este control se recuperan los salones disponibles a la hora seleccionada de la lista de salones seleccionada. Si es el último, al seleccionar este control se establece la variable **_selectedRoom** en el elemento seleccionado. La instrucción anterior es muy similar a la instrucción **Select** para el [**título FindMeetingTimesGallery**](#find-meeting-times-gallery).

  En un nivel bajo, el bloque de código anterior:
  1. Activa el estado de carga de las salas estableciendo **_loadingRooms** en **true**.
  1. Comprueba si se ha seleccionado una lista de salas y si el inquilino tiene listas de salones. En caso afirmativo:
      1. Establece **_roomListSelected** en **true** y establece **_selectedRoomList** en el elemento seleccionado.
      1. La variable **_allRoomsConcat** se establece en una cadena separada por punto y coma de las 20 primeras direcciones de correo electrónico de los salones de la colección **AllRooms** . Esto se debe a que la operación [Office365. FindMeetingTimes](https://docs.microsoft.com/connectors/office365/#find-meeting-times) está limitada a la búsqueda de las horas disponibles de 20 objetos Person en una sola operación.
      1. La colección **RoomTimeSuggestions** usa la operación [Office365. FindMeetingTimes](https://docs.microsoft.com/connectors/office365/#find-meeting-times) para recuperar las disponibilidades de los 20 primeros salones de la colección **AllRooms** , en función de los valores de tiempo de **_selectedMeetingTime** variable. Tenga en cuenta que `& "Z"` se usa para dar formato al valor **DateTime** correctamente.
      1. Se crea la colección **AvailableRooms** . Esto es simplemente la colección **RoomTimeSuggestions** de la disponibilidad de los asistentes con dos columnas adicionales agregadas: "Address" y "Name". "Address" es la dirección de correo electrónico de la habitación y "Name" es el nombre de la habitación.
      1. A continuación, se crea la colección **AvailableRoomsOptimal** . Esta es solo la colección **AvailableRooms** con las columnas "Availability" y "attendees" quitadas. Esto coincide con los esquemas de **AvailableRoomsOptimal** y **AllRooms**. Esto le permite usar ambas colecciones en la propiedad **Items** de **RoomBrowseGallery**.
      1. **_roomListSelected** está establecido en **false**.
  1. El estado de carga, **_loadingRooms**, se establece en **false** una vez que todo lo demás ha terminado de ejecutarse.

## <a name="back-chevron"></a>Cheurón atrás

   ![Control RoomsBackNav](media/meeting-screen/meeting-back.png)

* Propiedad **Estarán**<br>
    Valor: `_roomListSelected && _showDetails`

    Este control solo es visible si se ha seleccionado una lista de sala y se selecciona la pestaña **programación** .

* Propiedad **Alseleccionar**<br>
    Valor: `Set( _roomListSelected, false )`

    Cuando **_roomListSelected** se establece en **false**, cambia el control **RoomBrowseGallery** para mostrar los elementos de la colección **RoomsLists** .

## <a name="send-icon"></a>Icono de envío

   ![Control IconSendItem](media/meeting-screen/meeting-send-icon.png)

* Propiedad **DisplayMode**<br>
    Valor Lógica para obligar al usuario a especificar determinados detalles de la reunión antes de que el icono se vuelva editable.
    
    ```powerapps-dot
    If( Len( Trim( TextMeetingSubject1.Text ) ) > 0
        && !IsEmpty( MyPeople ) && !IsBlank( _selectedMeetingTime ),
        DisplayMode.Edit, DisplayMode.Disabled
    )
    ```
  El icono solo es seleccionable si el asunto de la reunión se rellena, hay al menos un asistente para la reunión y se ha seleccionado una hora de reunión. De lo contrario, está deshabilitado.

* Propiedad **Alseleccionar**<br>

    Valor Código para enviar la invitación de reunión a los asistentes seleccionados y borrar todos los campos de entrada:

    ```powerapps-dot
    Set( _myCalendarName, LookUp( 'Office365'.CalendarGetTables().value, DisplayName = "Calendar" ).Name );
    Set( _myScheduledMeeting, 
        'Office365'.V2CalendarPostItem( _myCalendarName,
            TextMeetingSubject1.Text, 
            Text(DateAdd(DateTimeValue( _selectedMeetingTime.StartTime), -TimeZoneOffset(), Minutes) ),
            Text(DateAdd(DateTimeValue( _selectedMeetingTime.EndTime), -TimeZoneOffset(), Minutes) ),
            {
                RequiredAttendees: Concat( MyPeople, UserPrincipalName & ";" ) & _selectedRoom.Address, 
                Body: TextMeetingMessage1.Text, 
                Location: _selectedRoom.Name, 
                Importance: "Normal", 
                ShowAs: "Busy", 
                ResponseRequested: true
            }
        )
    );
    Concurrent(
        Reset( TextMeetingLocation1 ),
        Reset( TextMeetingSubject1 ),
        Reset( TextMeetingMessage1 ),
        Clear( MyPeople ),
        Set( _selectedMeetingTime, Blank() ),
        Set( _selectedRoomList, Blank() ),
        Set( _selectedRoom, Blank() ),
        Set( _roomListSelected, false )
    )
    ```
  
  En un nivel bajo, este bloque de código:
  1. Establece **_myCalendarName** en el calendario de la operación [Office365. CalendarGetTables ()](https://docs.microsoft.com/connectors/office365/#get-calendars) con un **displayName** de "Calendar".
  1. Programa la reunión con todos los valores de entrada de las distintas selecciones realizadas por el usuario en la pantalla mediante la operación [Office365. V2CalendarPostItem](https://docs.microsoft.com/connectors/office365/#create-event--v2-) .
  1. Restablece todos los campos de entrada y las variables utilizadas en la creación de la reunión.

> [!NOTE]
> En función de su región, es posible que el calendario que desee no tenga el nombre para mostrar "Calendar". Vaya a Outlook para ver cuál es el título del calendario y realice el cambio adecuado en la aplicación.

## <a name="next-steps"></a>Pasos siguientes

* [Más información acerca de esta pantalla](./meeting-screen-overview.md)
* [Más información sobre el conector de Office 365 Outlook en PowerApps](../connections/connection-office365-outlook.md)
* [Más información sobre el conector de usuarios de Office 365 en PowerApps](../connections/connection-office365-users.md)
