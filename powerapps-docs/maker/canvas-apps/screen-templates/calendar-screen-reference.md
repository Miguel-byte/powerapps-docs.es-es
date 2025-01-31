---
title: Referencia de la plantilla de pantalla calendario para aplicaciones de Canvas | Microsoft Docs
description: Conozca los detalles sobre cómo funciona la plantilla de pantalla calendario para las aplicaciones de lienzo en PowerApps.
author: emcoope-msft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: tapanm
ms.date: 12/31/2018
ms.author: emcoope
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: b9e5425244d819816fa05c4b780a6be092b0d22c
ms.sourcegitcommit: 7dae19a44247ef6aad4c718fdc7c68d298b0a1f3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/07/2019
ms.locfileid: "71995720"
---
# <a name="reference-information-about-the-calendar-screen-template-for-canvas-apps"></a>Información de referencia sobre la plantilla de pantalla calendario para aplicaciones de Canvas

En el caso de las aplicaciones de canvas en PowerApps, comprenda cómo contribuye cada control significativo de la plantilla de pantalla calendario a la funcionalidad predeterminada general de la pantalla. Esta profundización presenta las fórmulas de comportamiento y los valores de otras propiedades que determinan cómo responden los controles a los datos proporcionados por el usuario. Para obtener una descripción de alto nivel de la funcionalidad predeterminada de esta pantalla, consulte la [información general](calendar-screen-overview.md)de la pantalla de calendario.

En este tema se resaltan algunos controles significativos y se explican las expresiones o fórmulas en las que se establecen varias propiedades (como **Items** y **alseleccionar**) de estos controles:

- [Lista desplegable de calendario (dropdownCalendarSelection)](#calendar-drop-down)
- [Icono de calendario (iconCalendar)](#calendar-icon)
- [Cheurón anterior (iconPrevMonth)](#previous-month-chevron)
- [Botón de contenido adicional del mes siguiente (iconNextMonth)](#next-month-chevron)
- [Galería de calendarios (MonthDayGallery) (+ controles secundarios)](#calendar-gallery)
- [Galería de eventos (CalendarEventsGallery)](#events-gallery)

## <a name="prerequisite"></a>Requisito previo

Está familiarizado con cómo agregar y configurar pantallas y otros controles a medida que [crea una aplicación en PowerApps](../data-platform-create-app-scratch.md).

## <a name="calendar-drop-down"></a>Lista desplegable de calendario

![control dropdownCalendarSelection](media/calendar-screen/calendar-dropdown.png)

- Propiedad **Elementos**<br>
    Valor: `Office365.CalendarGetTables().value`

    Este valor es una operación de conector que recupera los calendarios de Outlook del usuario de la aplicación. Puede ver [el valor](https://docs.microsoft.com/connectors/office365/#entitylistresponse[table]) que recupera esta operación.

- Propiedad **OnChange**<br>Valor: `Select(dropdownCalendarSelection)`

    Cuando el usuario selecciona una opción en la lista, se ejecuta la función de la propiedad **alseleccionar** del control.

- Propiedad **Alseleccionar**<br>
    Valor Una función **If** , que aparece en el siguiente bloque de código, y varias funciones adicionales, que aparecen en el bloque de código después de eso.

   Esta parte de la fórmula se ejecuta solo la primera vez que el usuario selecciona una opción en la lista desplegable después de abrir la aplicación:

    ```powerapps-dot
    If( IsBlank( _userDomain ),
        UpdateContext( {_showLoading: true} );
        Set( _userDomain, Right( User().Email, Len( User().Email ) - Find( "@", User().Email ) ) );
        Set( _dateSelected, Today() );
        Set( _firstDayOfMonth, DateAdd( Today(), 1 - Day( Today() ), Days ) );  
        Set( _firstDayInView, DateAdd( _firstDayOfMonth, -(Weekday(_firstDayOfMonth) - 1), Days ) );
        Set( _lastDayOfMonth, DateAdd( DateAdd( _firstDayOfMonth, 1, Months ), -1, Days ) )  
    );
    ```

    El código anterior define las siguientes variables:
    
  - **@no__t 1userDomain**: El dominio de la empresa del usuario de la aplicación, tal y como se refleja en la dirección de correo electrónico del usuario.
  - **@no__t 1dateSelected**: Fecha de hoy (de forma predeterminada). La galería de calendarios resalta esta fecha y la galería de eventos muestra los eventos que están programados para esa fecha.
  - **@no__t 1firstDayOfMonth**: Primer día del mes actual. Dado que `(Today + (1 - Today)) = Today - Today + 1 = 1`, esta función **DateAdd** siempre devuelve el primer día del mes.
  - **@no__t 1firstDayInView**: Primer día que puede mostrar la galería de calendarios. Este valor no es el mismo que el primer día del mes, a menos que el mes se inicie en un domingo. Para evitar que se muestre una semana completa del mes anterior, el valor de **\_firstDayInView** es `_firstDayOfMonth - Weekday(_firstDayOfMonth) + 1`.
  - **@no__t 1lastDayOfMonth**: El último día del mes actual, que es el mismo que el primer día del mes siguiente, menos un día.

   Las funciones después de la función **If** se ejecutan cada vez que el usuario selecciona una opción en la lista desplegable calendario (no solo la primera vez que el usuario abre la aplicación):

    ```powerapps-dot
    Set( _calendarVisible, false );
    UpdateContext( {_showLoading: true} );
    Set( _myCalendar, dropdownCalendarSelection2.Selected );
    Set( _minDate, 
        DateAdd( _firstDayOfMonth, -(Weekday( _firstDayOfMonth ) - 2 + 1), Days )
    );
    Set(_maxDate, 
        DateAdd(
            DateAdd( _firstDayOfMonth, -(Weekday( _firstDayOfMonth ) - 2 + 1), Days ), 
            40, 
            Days
        )
    );
    ClearCollect( MyCalendarEvents, 
        'Office365'.GetEventsCalendarViewV2( _myCalendar.Name, 
            Text( _minDate, UTC ), 
            Text( _maxDate, UTC )
        ).value
    );
    UpdateContext( {_showLoading: false} );
    Set( _calendarVisible, true )
    ```

    El código anterior define estas variables y una colección:

    - **@no__t 1calendarVisible**: Establézcalo en **false** para que el calendario no aparezca mientras se carga la nueva selección.
    - **@no__t 1showLoading**: Establézcalo en **true** para que aparezcan los indicadores de carga mientras se carga la nueva selección.
    - **@no__t 1myCalendar**: Establezca en el valor actual del control **desplegable de calendario** para recuperar los eventos del calendario correcto.
    - **@no__t 1minDate**: Establézcalo en el mismo valor que **@no__t 1firstDayInView**. Esta variable determina qué eventos ya se han recuperado de Outlook y se han almacenado en la memoria caché de la aplicación.
    - **@no__t 1maxDate**: Se establece en el último día visible del calendario. La fórmula es `_firstDayInView + 40`. El calendario muestra un máximo de 41 días, por lo que la variable **\_maxDate** siempre refleja el último día visible y determina qué eventos ya se han recuperado de Outlook y se han almacenado en la memoria caché de la aplicación.
    - **MyCalendarEvents**: Se establece en una colección de eventos del usuario del calendario seleccionado, que van desde **\_minDate** a **\_maxDate**.
    - **@no__t 1showLoading**: Se establece en **false**; **\_calendarVisible** se establece en **true** una vez que se ha cargado todo lo demás.

## <a name="calendar-icon"></a>Icono de calendario

![control iconCalendar](media/calendar-screen/calendar-today-icon.png)

- Propiedad **Alseleccionar**<br>
    Valor Cuatro funciones **set** que restablecen la galería de calendario a la fecha de hoy:

    ```powerapps-dot
    Set( _dateSelected, Today() );
    Set( _firstDayOfMonth, DateAdd( Today(), 1 - Day( Today() ), Days) );
    Set( _firstDayInView, DateAdd(_firstDayOfMonth, -(Weekday( _firstDayOfMonth ) - 2 + 1), Days));
    Set( _lastDayOfMonth, DateAdd( DateAdd( _firstDayOfMonth, 1, Months ), -1, Days ) )
    ```

    El código anterior restablece todas las variables de fecha necesarias para mostrar la vista de calendario adecuada:

    - **\_dateSelected** se restablece a hoy.
    - **\_firstDayOfMonth** se restablece al primer día del mes de hoy.
    - **\_firstDayInView** se restablece al primer día visible cuando se selecciona el mes de hoy.
    - **\_lastDayOfMonth** se restablece en el último día del mes de hoy.

    En la sección desplegable [**calendario**](#calendar-drop-down) de este tema se explican estas variables con más detalle.

## <a name="previous-month-chevron"></a>Botón de contenido adicional de mes anterior

![control iconPrevMonth](media/calendar-screen/calendar-back.png)

- Propiedad **Alseleccionar**<br>Valor Cuatro funciones **set** y una función **If** que muestran el mes anterior en la galería de calendario:

    ```powerapps-dot
    Set( _firstDayOfMonth, DateAdd( _firstDayOfMonth, -1, Months ) );
    Set( _firstDayInView, 
        DateAdd( _firstDayOfMonth, -(Weekday( _firstDayOfMonth ) - 2 + 1), Days )
    );
    Set( _lastDayOfMonth, DateAdd(DateAdd( _firstDayOfMonth, 1, Months ), -1, Days ) );
    If( _minDate > _firstDayOfMonth,
        Collect( MyCalendarEvents,
            'Office365'.GetEventsCalendarViewV2( _myCalendar.Name,
                Text( _firstDayInView, UTC ), 
                Text( DateAdd( _minDate, -1, Days ), UTC )
            ).value
        );
        Set( _minDate, _firstDayInView )
    )
    ```

    > [!NOTE]
    > Las definiciones de **\_firstDayOfMonth**, **\_firstDayInView**y **\_lastDayOfMonth** son casi idénticas a las de la sección desplegable [calendario](#calendar-drop-down) de este tema.

    Las tres primeras líneas del código anterior se ejecutan cada vez que el usuario selecciona el botón de contenido adicional del mes anterior. El código establece las variables necesarias para mostrar la vista de calendario adecuada. El código restante se ejecuta solo si el usuario no ha seleccionado previamente este mes para el calendario seleccionado.

    En este caso, **\_minDate** es el primer día que aparece cuando se muestra el mes anterior. Antes de que el usuario seleccione el icono, **\_minDate** tiene un valor mínimo posible de la 23 del mes actual. (Cuando el 1 de marzo cae en sábado, **\_firstDayInView** para marzo es el 23 de febrero). Esto significa que, si un usuario no ha seleccionado este mes, **\_minDate** es mayor que el nuevo **\_firstDayOfMonth**y la función **If** devuelve **true**. El código se ejecuta y se actualiza una colección y una variable:

    - **MyCalendarEvents** recupera eventos del calendario seleccionado con la operación [Office365. GetEventsCalendarViewV2](https://docs.microsoft.com/connectors/office365/#get-calendar-view-of-events--v2-) . El intervalo de fechas se encuentra entre la fecha **\_firstDayInView** y **\_minDate** -1. Dado que **MyCalendarEvents** ya contiene eventos en la fecha **\_minDate** , 1 se resta de esa fecha para el valor máximo de este nuevo intervalo de fechas.

    - **\_minDate** se establece en el **@no__t actual-3firstDayInView** porque se trata de la primera fecha para la que se han recuperado eventos. Si un usuario vuelve a esta fecha seleccionando el botón de contenido adicional del mes anterior, la función **If** devuelve **false**. el código no se ejecuta porque los eventos de esta vista ya están almacenados en caché en **MyCalendarEvents**.

## <a name="next-month-chevron"></a>Botón de contenido adicional del mes siguiente

![control iconNextMonth](media/calendar-screen/calendar-forward.png)

- Propiedad **Alseleccionar**<br>
    Valor Cuatro funciones **set** y una función **If** que muestran el mes siguiente en la galería de calendario:

    ```powerapps-dot
    Set( _firstDayOfMonth, DateAdd( _firstDayOfMonth, 1, Months ) );
    Set( _firstDayInView, 
        DateAdd( _firstDayOfMonth, -(Weekday( _firstDayOfMonth ) - 2 + 1), Days ) );
    Set( _lastDayOfMonth, DateAdd( DateAdd( _firstDayOfMonth, 1, Months ), -1, Days ) );
    If( _maxDate < _lastDayOfMonth,
        Collect( MyCalendarEvents, 
            'Office365'.GetEventsCalendarViewV2( _myCalendar.Name, 
                Text( DateAdd( _maxDate, 1, Days ), UTC ), 
                DateAdd( _firstDayInView, 40, Days )
            ).value
        );
        Set( _maxDate, DateAdd( _firstDayInView, 40, Days) )    
    )
    ```

    > [!NOTE]
    > Las definiciones de **\_firstDayOfMonth**, **\_firstDayInView**y **\_lastDayOfMonth** son casi idénticas a las de la sección desplegable [calendario](#calendar-drop-down) de este tema.

    Las tres primeras líneas del código anterior, que se ejecutan cuando el usuario selecciona el botón de contenido adicional del mes siguiente, establezca las variables necesarias para mostrar la vista de calendario adecuada. El código restante se ejecuta solo si el usuario no ha seleccionado previamente este mes para el calendario seleccionado.

    En ese caso, **\_maxDate** es el último día que aparece cuando se muestra el mes anterior. Antes de que el usuario seleccione el cheurón siguiente, **\_maxDate** tiene un valor máximo posible del decimotercer del mes siguiente. (Cuando el 1 de febrero cae en un domingo de año no bisiesto, **\_maxDate** es el 13 de marzo, que es **\_firstDayInView** + 40 días). Esto significa que, si un usuario no ha seleccionado este mes, **\_maxDate** es mayor que el nuevo **\_lastDayOfMonth**y la función **If** devuelve **true**. El código se ejecuta y se actualiza una colección y una variable:

    - **MyCalendarEvents** recupera eventos del calendario seleccionado con la operación [Office365. GetEventsCalendarViewV2](https://docs.microsoft.com/connectors/office365/#get-calendar-view-of-events--v2-) . El intervalo de fechas se encuentra entre **\_maxDate** + 1 día y **\_firstDayInView** + 40 días. Dado que **MyCalendarEvents** ya contiene eventos en la fecha **\_minDate** , se agrega 1 a esa fecha para el valor mínimo de este nuevo intervalo de fechas. **\_firstDayInView** + 40 es la fórmula de **\_maxDate**, por lo que la segunda fecha del intervalo es simplemente la nueva **\_maxDate**.

    - **\_maxDate** se establece en **\_firstDayInView** + 40 días, ya que se trata del último día para el que se han recuperado eventos. Si un usuario vuelve a esta fecha seleccionando el botón de contenido adicional del mes siguiente, la función **If** devuelve **false**. el código no se ejecuta porque los eventos de esta vista ya están almacenados en caché en **MyCalendarEvents**.

## <a name="calendar-gallery"></a>Galería de calendarios

![Control MonthDayGallery](media/calendar-screen/calendar-month-gall.png)

- Propiedad **Elementos**<br>
    Valor: `[0,1,2,3,4,5,6,7,8,9,10,11,12,13,14,15,16,17,18,19,
    20,21,22,23,24,25,26,27,28,29,30,31,32,33,34,35,36,37,38,39,40,41]`
  
  El conjunto de 0 a 41 se usa para los elementos de la galería de calendarios porque, en el peor de los casos, la vista de calendario tendrá que mostrar 42 días completos. Esto sucede cuando el primer día del mes se produce el sábado y el último del mes se produce el domingo. En este caso, el calendario muestra seis días del mes anterior de la fila que contiene el primero del mes y seis días desde el mes siguiente en la fila que contiene la última del mes. Se trata de valores únicos 42, de los cuales 30 son para el mes seleccionado.

- Propiedad **WrapCount**<br>
    Valor: `7`

  Este valor refleja una semana de siete días.

### <a name="title-control-in-the-calendar-gallery"></a>Control de título en la galería de calendarios

![Control de título de MonthDayGallery](media/calendar-screen/calendar-month-text.png)

- Propiedad **Texto**<br>
    Valor: `Day( DateAdd( _firstDayInView, ThisItem.Value, Days ) )`

    Recuerde que **\_firstDayInView** se define como ( **\_firstDayOfMonth** -su valor de día de la semana) + 1. Esto indica que **\_firstDayInView** es siempre un domingo y **\_firstDayOfMonth** siempre está en la primera fila de **MonthDayGallery**. Debido a estos dos hechos, **\_firstDayInView** siempre está en la primera celda de **MonthDayGallery**. **ThisItem. Value** es el número de esa celda en la propiedad del elemento **MonthDayGallery** . Por lo tanto, tomando **@no__t 1firstDayInView** como punto de partida, cada celda muestra el incremento de **\_firstDayInView** + su valor de celda respectivo.

- Propiedad **Relleno**<br>
    Valor Una función **If** :

    ```powerapps-dot
    If( DateAdd( _firstDayInView, ThisItem.Value ) = Today() && 
                DateAdd( _firstDayInView, ThisItem.Value ) = _dateSelected, 
            RGBA( 0, 0, 0, 0 ),
        DateAdd( _firstDayInView, ThisItem.Value) = Today(), 
            ColorFade( Subcircle.Fill, 0.67 ),
        Abs( Title.Text - ThisItem.Value) > 10,
            RGBA( 200, 200, 200, 0.3 ),
        RGBA( 0, 0, 0, 0 )
    )
    ```

  Como se describe en la descripción de la propiedad **Text** , `DateAdd(_firstDayInView, ThisItem.Value)` representa el día en la celda visible. Teniendo esto en cuenta, el código anterior realiza estas comparaciones:
  1. Si el valor de la celda es la fecha de hoy y esta celda es equivalente a **\_dateSelected**, no proporcione un valor de relleno.
  1. Si el valor de la celda es la fecha de hoy pero no equivalente a **\_dateSelected**, proporcione el relleno **ColorFade** .
  1. La última comparación no es tan clara. Se trata de una comparación entre el valor de texto real de la celda y el valor del elemento de celda (el número en la pantalla y el número de elemento).<br>

      Para comprender mejor esto, tenga en cuenta el 2018 de septiembre, un mes que comienza un sábado y termina en domingo. En este caso, el calendario muestra el 26 al 31 de agosto y el 1 de septiembre en la primera fila, y `Abs(Title.Text - ThisItem.Value) = 26` hasta el 1 de septiembre. A continuación `Abs(Title.Text - ThisItem.Value) = 5`. Permanecerá en 5 hasta la última fila del calendario, que muestra el 30 de septiembre y el 1 de octubre al sexto. En ese `Abs(Title.Text - ThisItem.Value)` seguirá siendo 5 para el 30 de septiembre, pero será 35 para las fechas de octubre.<br>

      Este es el patrón: En los días mostrados desde el mes anterior, `Abs(Title.Text - ThisItem.Value)` siempre será igual al valor `Title.Text` del primer día de la pantalla. En los días que se muestran en el mes siguiente, `Abs(Title.Text - ThisItem.Value)` siempre será igual al valor del elemento **MonthDayGallery** de la primera celda de ese mes (en este caso, el 1 de octubre) menos 1. Y, lo que es más importante, en el caso de los días mostrados en el mes seleccionado actualmente, `Abs(Title.Text - ThisItem.Value)` siempre será igual al valor del primer elemento de ese mes menos 1 y nunca superará los 5, como se muestra en el ejemplo anterior. Por lo tanto, es absolutamente válido escribir la fórmula como `Abs(Title.Text - ThisItem.Value) > 5`.

      Esta instrucción comprueba si el valor de fecha está fuera del mes seleccionado actualmente. Si es así, **Fill** es un gris parcialmente opaco.

    > [!NOTE]
    > Puede comprobar la validez de esta última comparación para sí mismo insertando un control **etiqueta** en la galería y estableciendo su propiedad **texto** en este valor:<br>`Abs(Title.Text - ThisItem.Value)`.

- Propiedad **Estarán**<br>
    Valor

    ```powerapps-dot
    !(
        DateAdd( _firstDayInView, ThisItem.Value, Days ) - 
            Weekday( DateAdd( _firstDayInView, ThisItem.Value,Days ) ) + 1 
        > _lastDayOfMonth
    )
    ```

    La instrucción anterior comprueba si la celda está en una fila en la que no se producen días del mes seleccionado actualmente. Recuerde que si se resta el valor de día de la semana de cualquier día de su valor de fecha y se agrega 1 siempre se devuelve el primer elemento de la fila en la que vive el día. Por lo tanto, esta instrucción comprueba si el primer día de la fila es posterior al último día del mes visible. Si es así, no aparecerá porque la fila completa contiene días del mes siguiente.

- Propiedad **Alseleccionar**<br>
    Valor Una función **set** que establece la variable **\_dateSelected** en la fecha de la celda seleccionada:

    ```powerapps-dot
    Set( _dateSelected, DateAdd( _firstDayInView, ThisItem.Value, Days ) )
    ```

### <a name="circle-control-in-the-calendar-gallery"></a>Control de círculo en la galería de calendarios

![Control de círculo MonthDayGallery](media/calendar-screen/calendar-month-event.png)

- Propiedad **Estarán**<br>
    Valor Una fórmula que determina si hay eventos programados para la fecha seleccionada y si los controles de **título** y **subcírculo** están visibles:

    ```powerapps-dot
    CountRows(
        Filter( MyCalendarEvents, 
            DateValue( Text( Start ) ) = DateAdd( _firstDayInView, ThisItem.Value, Days )
        )
    ) > 0 && !Subcircle.Visible && Title.Visible
    ```

    El control de **círculo** es visible si el campo de **Inicio** de cualquier evento es equivalente a la fecha de esa celda, si el control de **título** está visible y si el control de **subcírculo** no está visible. En otras palabras, este control es visible cuando se produce al menos un evento en este día y este día no está seleccionado. Si está seleccionada, los eventos de ese día se muestran en el control **CalendarEventsGallery** .

### <a name="subcircle-control-in-the-calendar-gallery"></a>Control de subcírculo en la galería de calendarios

![Control de subcírculo MonthDayGallery](media/calendar-screen/calendar-month-selected.png)

- Propiedad **Estarán**<br>
    Valor

    ```powerapps-dot
    DateAdd( _firstDayInView, ThisItem.Value ) = _dateSelected && Title.Visible
    ```

  El control de **subcírculo** está visible cuando **\_dateSelected** es equivalente a la fecha de la celda y el control de **título** está visible. En otras palabras, este control aparece cuando la celda es la fecha seleccionada actualmente.

## <a name="events-gallery"></a>Galería de eventos

![Control CalendarEventsGallery](media/calendar-screen/calendar-events-gall.png)

- Propiedad **Elementos**<br>
    Valor Una fórmula que ordena y filtra la galería de eventos:

    ```powerapps-dot
    SortByColumns(
        Filter( MyCalendarEvents,
            Text( Start, DateTimeFormat.ShortDate ) = Text( _dateSelected, DateTimeFormat.ShortDate )
        ),
        "Start"
    )
    ```

   La colección **MyCalendarEvents** contiene todos los eventos entre **\_minDate** y **\_maxDate**. Para mostrar los eventos solo para la fecha seleccionada, se aplica un filtro en **MyCalendarEvents** para mostrar los eventos que tienen una fecha de inicio equivalente a **\ _dateSelected**. A continuación, los elementos se ordenan por sus fechas de inicio para colocarlos en orden secuencial.

## <a name="next-steps"></a>Pasos siguientes

- [Más información acerca de esta pantalla](./calendar-screen-overview.md)
- [Más información sobre el conector de Office 365 Outlook en PowerApps](../connections/connection-office365-outlook.md)
- [Más información sobre el conector de usuarios de Office 365 en PowerApps](../connections/connection-office365-users.md)
