---
title: Crear un formulario de resumen en una aplicación de lienzo | Microsoft Docs
description: Crear un formulario de resumen en una aplicación de lienzo para administrar datos de Northwind Traders
author: gregli-msft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: tapanm
ms.date: 04/25/2019
ms.author: gregli
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: d151249caebdb2a6f142943074a409bc626ff662
ms.sourcegitcommit: 7dae19a44247ef6aad4c718fdc7c68d298b0a1f3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/07/2019
ms.locfileid: "71995864"
---
# <a name="create-a-summary-form-in-a-canvas-app"></a>Crear un formulario de resumen en una aplicación de lienzo

Siga las instrucciones paso a paso para crear un formulario de resumen en una aplicación de lienzo para administrar datos ficticios en la base de datos Northwind Traders. Este tema forma parte de una serie en la que se explica cómo compilar una aplicación empresarial en datos relacionales en Common Data Service. Para obtener los mejores resultados, explore estos temas en esta secuencia:

1. [Cree una galería de pedidos](northwind-orders-canvas-part1.md).
2. Crear un formulario de resumen (**este tema**).
3. [Cree una galería de detalles](northwind-orders-canvas-part3.md).

> [!div class="mx-imgBorder"]
> ![Definition de las áreas de pantalla @ no__t-1

## <a name="prerequisites"></a>Requisitos previos

1. [Instale la base de datos y las aplicaciones de Northwind Traders](northwind-install.md).
1. Revise la [información general de la aplicación Canvas](northwind-orders-canvas-overview.md) para Northwind Traders.
1. [Cree la galería de pedidos](northwind-orders-canvas-part1.md) usted mismo o abra la aplicación **Northwind Orders (canvas)-Begin Part 2** , que ya contiene esa Galería.

## <a name="add-a-title-bar"></a>Incorporación de una barra de título

En la parte superior de la aplicación, cree una barra de título, que contendrá los botones de acción al final de este tema.

1. En el panel de **vista de árbol** , seleccione **Screen1** para asegurarse de que no agrega accidentalmente un control a la galería de pedidos:

    > [!div class="mx-imgBorder"]
    > @no__t 0Select Screen1 en el panel de vista de árbol @ no__t-1

1. En la pestaña **Insertar** , seleccione **etiqueta** para insertar un control [**etiqueta**](controls/control-text-box.md) :

    > [!div class="mx-imgBorder"]
    > ![Insert etiqueta @ no__t-1

    La nueva etiqueta debe aparecer una sola vez, encima de la galería. Si aparece en cada elemento de la galería, elimine la primera instancia de la etiqueta, asegúrese de que la pantalla está seleccionada (como se describe en el paso anterior) y, a continuación, vuelva a insertar la etiqueta.

1. Mueva y cambie el tamaño de la nueva etiqueta para que abarque la parte superior de la pantalla:

    > [!div class="mx-imgBorder"]
    > ![Move y cambie el tamaño de la etiqueta @ no__t-1

1. Haga doble clic en el texto de la etiqueta y, a continuación, escriba **Northwind Orders**.

    Como alternativa, modifique la propiedad **texto** en la barra de fórmulas para lograr el mismo resultado:

    > [!div class="mx-imgBorder"]
    > @no__t: 0Change el texto en la barra de título @ no__t-1

1. En la pestaña **Inicio** , dé formato a la etiqueta:
    - Aumente el tamaño de fuente a 24 puntos.
    - Poner el texto en negrita.
    - Haga que el texto sea blanco.
    - Centre el texto.
    - Agregue un relleno azul oscuro al fondo.

    > [!div class="mx-imgBorder"]
    > @no__t opciones de 0Formatting en la pestaña Inicio @ no__t-1

## <a name="add-an-edit-form-control"></a>Agregar un control Editar formulario

En esta sección, agregará controles para mostrar un resumen de cualquier orden que el usuario seleccione en la galería.

1. En la pestaña **Insertar** , inserte un control [**Editar formulario**](controls/control-form-detail.md) :

    > [!div class="mx-imgBorder"]
    > ![Add un control de edición de formulario @ no__t-1

    De forma predeterminada, el formulario aparece en la esquina superior izquierda, donde otros controles pueden dificultar la búsqueda:

    > [!div class="mx-imgBorder"]
    > @no__t el control de formulario 0Edit en la ubicación predeterminada @ no__t-1

1. Mueva y cambie el tamaño del formulario para que cubra la esquina superior derecha de la pantalla en la barra de título:

    > [!div class="mx-imgBorder"]
    > @no__t 0Move y cambiar el tamaño del control de edición de formulario @ no__t-1

1. En la barra de fórmulas, establezca la propiedad **DataSource** del formulario en este valor:

    ```powerapps-dot
    Orders
    ```

    > [!div class="mx-imgBorder"]
    > ![Set la propiedad DataSource del control Edit Form @ no__t-1

    Puede establecer la misma propiedad en la pestaña **propiedades** cerca del borde derecho, pero ese enfoque agrega campos que no necesita al formulario. Si usa la barra de fórmulas, el formulario permanece vacío.

## <a name="add-and-arrange-fields"></a>Agregar y organizar campos

1. En la pestaña **propiedades** situada cerca del borde derecho, seleccione **Editar campos** para abrir el panel **campos** :

    > [!div class="mx-imgBorder"]
    > @no__t: 0Open el panel campos @ no__t-1

1. En el panel **campos** , seleccione **Agregar campo**y, a continuación, active las casillas de los campos **Customer** y **Employee** .

    > [!div class="mx-imgBorder"]
    > @no__t: 0Add los campos Customer y Employee al control Edit Form @ no__t-1

1. Desplácese hacia abajo hasta que aparezcan estos campos y, a continuación, active las casillas siguientes:

    - **Notas**
    - **Fecha del pedido**
    - **Número de pedido**
    - **Estado del pedido**
    - **Fecha de pago**

    > [!div class="mx-imgBorder"]
    > ![Add cinco campos más en el control Edit Form @ no__t-1

1. En la parte inferior del panel **campos** , seleccione **Agregar**y, a continuación, cierre el panel **campos** .

    El formulario muestra siete campos:

    > [!div class="mx-imgBorder"]
    > @no__t control de formulario de 0Edit muestra siete campos @ no__t-1

    > [!NOTE]
    > Si un campo muestra un icono de error rojo, es posible que se haya producido un problema al extraer los datos del origen. Para resolver el error, actualice los datos:
    >
    > 1. En la pestaña **Vista**, seleccione **Orígenes de datos**.
    > 1. En el panel **datos** , seleccione **orígenes de datos**.
    > 1. Junto a **pedidos**, seleccione los puntos suspensivos (...), seleccione **Actualizar**y, a continuación, cierre el panel **datos** .
    >
    > Si el cuadro combinado del nombre del cliente o del empleado sigue mostrando un error, compruebe el **texto principal** y **SearchField** de cada cuadro seleccionándolo y, a continuación, abra el panel **datos** . En el cuadro cliente, ambos campos deben establecerse en **nwind_company**. En el cuadro empleado, ambos campos deben establecerse en **nwind_lastname**.

1. Con el formulario seleccionado, cambie el número de columnas del formulario de 3 a 12 en la pestaña **propiedades** situada junto al borde derecho.

    Este paso agrega flexibilidad a medida que se organizan los campos:

    > [!div class="mx-imgBorder"]
    > ![Change a continuación, número de columnas en el control de edición de formulario @ no__t-1

    Muchos diseños de interfaz de usuario se basan en diseños de 12 columnas porque pueden acomodar uniformemente las filas de los controles 1, 2, 3, 4, 6 y 12. En este tema, creará filas que contengan 1, 2 o 4 controles.

1. Mueva y cambie el tamaño de los campos arrastrando sus controladores, al igual que haría con cualquier otro control, de modo que cada fila contenga estas tarjetas de datos en el orden especificado:

    - Primera fila: **Número de pedido**, **Estado del pedido**, fecha de **pedido**y fecha de **pago**
    - Segunda fila: **Cliente** y **empleado**
    - Tercera fila: **Notas**

    > [!NOTE]
    > Es posible que le resulte más fácil ampliar las tarjetas de datos de las **notas**, el **cliente**y el **empleado** antes de organizarlas.

    > [!div class="mx-imgBorder"]
    > @no__t 0Move y cambiar el tamaño de los campos @ no__t-1

    Más información sobre cómo organizar los campos en un formulario: [Comprender el diseño de formularios de datos para las aplicaciones de canvas](working-with-form-layout.md).

## <a name="hide-time-controls"></a>Ocultar controles de tiempo

En este ejemplo, no se necesitan las partes de tiempo de los campos de fecha porque ese nivel de granularidad puede distraer al usuario. Si los elimina, puede provocar problemas en las fórmulas que dependen de esos controles para actualizar los valores de fecha o determinar la posición de otro control en la tarjeta de datos. En su lugar, ocultará los controles de tiempo estableciendo su propiedad **visible** .

1. En el panel de **vista de árbol** , seleccione la tarjeta de datos **Order Date** .

    La tarjeta puede tener un nombre diferente, pero contiene la **fecha del pedido**.

1. Mientras mantiene presionada la tecla Mayús, seleccione los controles hora, minuto y separador de dos puntos en la tarjeta de datos **Order Date** .

    > [!div class="mx-imgBorder"]
    > ![Select los controles de tiempo en la tarjeta de fecha de pedido @ no__t-1

1. Establezca la propiedad **visible** de los controles en **false**.

    Todos los controles seleccionados desaparecen del formulario:

    > [!div class="mx-imgBorder"]
    > @no__t la propiedad visible 0Set en false. ](media/northwind-orders-canvas-part2/form-10.png)

1. Cambie el tamaño del control [**selector de fecha**](controls/control-date-picker.md) para mostrar la fecha de finalización:

    > [!div class="mx-imgBorder"]
    > @no__t: 0Resize el control selector de fecha @ no__t-1

    A continuación, repetirá los últimos pasos para el campo de **fecha de pago** .

1. En el panel de **vista de árbol** , seleccione los controles de tiempo en la tarjeta de datos de **fecha de pago** :

    > [!div class="mx-imgBorder"]
    > @no__t el control de tiempo de 0Select en la tarjeta de fecha de pago @ no__t-1

1. Establezca la propiedad **visible** de los controles seleccionados en **false**:

    > [!div class="mx-imgBorder"]
    > @no__t la propiedad visible 0Set en false. ](media/northwind-orders-canvas-part2/form-13.png)

1. Cambie el tamaño del selector de fecha en la tarjeta de **fecha pagada** :

    > [!div class="mx-imgBorder"]
    > @no__t: 0Resize el control selector de fecha @ no__t-1

## <a name="connect-the-order-gallery"></a>Conexión de la galería de pedidos

1. En el panel de **vista de árbol** , contraiga el formulario para encontrar más fácilmente el nombre de la galería de pedidos y, a continuación, si es necesario, cambie su nombre a **Gallery1**.

1. Establezca la propiedad **Item** del formulario de resumen en esta expresión:

    ```powerapps-dot
    Gallery1.Selected
    ```

    > [!div class="mx-imgBorder"]
    > propiedad de elemento ![Set con el formato @ no__t-1

    El formulario muestra un resumen del orden que el usuario de la aplicación selecciona en la lista.

    > [!div class="mx-imgBorder"]
    > @no__t: 0Select un pedido en la lista para mostrar su información general con el formato @ no__t-1

## <a name="replace-a-data-card"></a>Reemplazar una tarjeta de datos

El **número de pedido** es un identificador que Common Data Service asigna automáticamente al crear un registro. Este campo tiene un control [**entrada de texto**](controls/control-text-input.md) de forma predeterminada, pero se reemplazará por una etiqueta para que el usuario no pueda editar este campo.

1. Seleccione el formulario, seleccione **Editar campos** en la pestaña **propiedades** situada junto al borde derecho y, a continuación, seleccione el campo **número de pedido** :

    > [!div class="mx-imgBorder"]
    > @no__t: 0Select el campo de número de pedido @ no__t-1

1. Abra la lista **tipo de control** :

    > [!div class="mx-imgBorder"]
    > ![Open el * * tipo de control * * List @ no__t-1

1. Seleccione la tarjeta de datos de texto de la **vista** :

    > [!div class="mx-imgBorder"]
    > @no__t 0Select * * Ver texto * * tarjeta de datos @ no__t-1

1. Cierre el panel **campos** .

    El usuario ya no puede cambiar el número de pedido:

    > [!div class="mx-imgBorder"]
    > ![Order número es de solo lectura @ no__t-1

1. En la pestaña **Inicio** , cambie el tamaño de fuente del número de pedido a 20 puntos para que el campo sea más fácil de encontrar:

    > [!div class="mx-imgBorder"]
    > @no__t: 0Change el tamaño de fuente del número de pedido @ no__t-1

## <a name="use-a-many-to-one-relationship"></a>Usar una relación de varios a uno

La entidad **Orders** tiene una relación de varios a uno con la entidad **Employees** : cada empleado puede crear muchos pedidos, pero cada pedido solo se puede asignar a un empleado. Cuando el usuario selecciona un empleado en el control de [**cuadro combinado**](controls/control-combo-box.md) , su propiedad **seleccionada** proporciona el registro completo de ese empleado de la entidad **Employees** . Como resultado, puede configurar un control [**imagen**](controls/control-image.md) para mostrar la imagen de cualquier empleado que el usuario seleccione en el cuadro combinado.

1. Seleccione la tarjeta de datos **Employee** :

    > [!div class="mx-imgBorder"]
    > ![Select la tarjeta de datos del empleado @ no__t-1

1. En la pestaña **avanzadas** , cerca del borde derecho, desbloquee la tarjeta de datos para que pueda editar las fórmulas que eran de solo lectura:

    > [!div class="mx-imgBorder"]
    > ![Unlock la tarjeta de datos del empleado @ no__t-1

1. En la tarjeta de datos, reduzca el ancho del cuadro combinado para dejar espacio para la imagen del empleado:

    > [!div class="mx-imgBorder"]
    > @no__t: 0Resize el control de cuadro combinado @ no__t-1

1. En la pestaña **Insertar** , seleccione **media** > **Image**:

    > [!div class="mx-imgBorder"]
    > @no__t: 0Insert una imagen @ no__t-1

    Aparece una imagen en la tarjeta de datos, que se expande para acomodarla:

    > [!div class="mx-imgBorder"]
    > @no__t tarjeta de datos 0Employee con el control Image @ no__t-1

1. Cambie el tamaño de la imagen y muévala a la derecha del cuadro combinado:

    > [!div class="mx-imgBorder"]
    > ![Move y cambiar el tamaño del control Image @ no__t-1

1. Establezca la propiedad **imagen** de la imagen en esta fórmula, reemplazando el número al final de DataCardValue si es necesario:

    ```powerapps-dot
    DataCardValue7.Selected.Picture
    ```

    > [!div class="mx-imgBorder"]
    > ![Set la propiedad Image de la imagen @ no__t-1

    Aparece la imagen del empleado seleccionado.

1. Mientras mantiene presionada la tecla Alt, seleccione otro empleado en el cuadro combinado para confirmar que la imagen también cambia.

    > [!div class="mx-imgBorder"]
    > @no__t: 0Select un empleado para mostrar la imagen de ese empleado @ no__t-1

## <a name="add-a-save-icon"></a>Agregar un icono de guardar

1. En el panel de **vista de árbol** , seleccione **Screen1**y, a continuación, seleccione **insertar** > **iconos** > **check**:

    > [!div class="mx-imgBorder"]
    > ![Insert icono de marca de verificación @ no__t-1

    De forma predeterminada, el icono de [**comprobación**](controls/control-shapes-icons.md) aparece en la esquina superior izquierda, donde otros controles pueden dificultar la búsqueda del icono:

    > [!div class="mx-imgBorder"]
    > ![Icon en la ubicación predeterminada @ no__t-1

1. En la pestaña **Inicio** , cambie la propiedad **color** del icono a blanco, cambie el tamaño del icono y muévalo cerca del borde derecho de la barra de título:

    > [!div class="mx-imgBorder"]
    > ![Configure el color, el tamaño y la ubicación del icono de guardar @ no__t-1

1. En el panel de **vista de árbol** , confirme que el nombre del formulario es **Form1**y, a continuación, establezca la propiedad **alseleccionar** del icono en esta fórmula:

    ```powerapps-dot
    SubmitForm( Form1 )
    ```

    > [!div class="mx-imgBorder"]
    > ![Set la propiedad alseleccionar del icono de guardado @ no__t-1

    Cuando el usuario selecciona el icono, la función [**SubmitForm**](functions/function-form.md) recopila los valores modificados en el formulario y los envía al origen de datos. Los puntos de marzo a lo largo de la parte superior de la pantalla a medida que se envían los datos, y la galería de pedidos refleja los cambios después de que finalice el proceso.

1. Establezca la propiedad **DisplayMode** del icono en esta fórmula:

    ```powerapps-dot
    If( Form1.Unsaved, DisplayMode.Edit, DisplayMode.Disabled )
    ```

    > [!div class="mx-imgBorder"]
    > ![Set la propiedad DisplayMode del icono @ no__t-1

    Si se han guardado todos los cambios en el formulario, el icono está deshabilitado y aparece en **DisabledColor**, que se establecerá a continuación.

1. Establezca la propiedad **DisabledColor** del icono en este valor:

    ```powerapps-dot
    Gray
    ```

    > [!div class="mx-imgBorder"]
    > ![Set la propiedad DisabledColor del icono @ no__t-1

    El usuario puede guardar los cambios en un pedido seleccionando el icono de marca de verificación, que está deshabilitado y atenuado hasta que el usuario realice otro cambio:

    > [!div class="mx-imgBorder"]
    > ![saving cambia @ no__t-1

## <a name="add-a-cancel-icon"></a>Agregar un icono de cancelación

1. En la pestaña **Insertar** , seleccione **iconos** > **Cancelar**:

    > [!div class="mx-imgBorder"]
    > ![Add cancelar icono @ no__t-1

    De forma predeterminada, el icono aparece en la esquina superior izquierda, donde otros controles pueden dificultar la búsqueda del icono:

    > [!div class="mx-imgBorder"]
    > @no__t el icono de 0Cancel en la ubicación predeterminada @ no__t-1

1. En la pestaña **Inicio** , cambie la propiedad **color** del icono a blanco, cambie el tamaño del icono y muévalo a la izquierda del icono de comprobación:

    > [!div class="mx-imgBorder"]
    > ![Change el color, el tamaño y la ubicación del icono de cancelación @ no__t-1

1. Establezca la propiedad **alseleccionar** del icono cancelar en esta fórmula:

    ```powerapps-dot
    ResetForm( Form1 )
    ```

    > [!div class="mx-imgBorder"]
    > ![Set la propiedad alseleccionar del icono cancelar @ no__t-1

    La función [**ResetForm**](functions/function-form.md) descarta todos los cambios del formulario, lo que lo devuelve a su estado original.

1. Establezca la propiedad **DisplayMode** del icono de cancelación en esta fórmula:

    ```powerapps-dot
    If( Form1.Unsaved Or Form1.Mode = FormMode.New, DisplayMode.Edit, DisplayMode.Disabled )
    ```

    > [!div class="mx-imgBorder"]
    > ![Set la propiedad DisplayMode del icono de cancelación @ no__t-1

    Esta fórmula difiere ligeramente de la del icono de comprobación. El icono cancelar se deshabilita si se han guardado todos los cambios o el formulario está en modo **nuevo** , lo que se habilitará a continuación. En ese caso, **ResetForm** descarta el nuevo registro.

1. Establezca la propiedad **DisabledColor** del icono de cancelación en este valor:

    ```powerapps-dot
    Gray
    ```

    > [!div class="mx-imgBorder"]
    > ![Set la propiedad DisabledColor del icono de cancelación @ no__t-1

    El usuario puede cancelar los cambios en un pedido y los iconos comprobar y cancelar están deshabilitados y atenuados si se han guardado todos los cambios:

    > [!div class="mx-imgBorder"]
    > ![Saving y canceling Changes @ no__t-1

## <a name="add-an-add-icon"></a>Agregar un icono Agregar

1. En la pestaña **Insertar** , seleccione **iconos** > **Agregar**.

    > [!div class="mx-imgBorder"]
    > @no__t: 0Insert un icono de adición @ no__t-1

    El icono **Agregar** aparece en la esquina superior izquierda de forma predeterminada, donde otros controles pueden dificultar la búsqueda:

    > [!div class="mx-imgBorder"]
    > ![Default Ubicación del icono Agregar @ no__t-1

1. En la pestaña **Inicio** , establezca la propiedad **color** del icono Agregar en blanco, cambie el tamaño del icono y muévalo a la izquierda del icono cancelar:

    > [!div class="mx-imgBorder"]
    > ![Change el color, el tamaño y la ubicación del icono de adición @ no__t-1

1. Establezca la propiedad **alseleccionar** del icono Agregar en esta fórmula:

    ```powerapps-dot
    NewForm( Form1 )
    ```

    > [!div class="mx-imgBorder"]
    > ![Set la propiedad alseleccionar del icono Add @ no__t-1

    La función [**NewForm**](functions/function-form.md) muestra un registro en blanco en el formulario.  

1. Establezca la propiedad **DisplayMode** del icono Agregar en esta fórmula:

    ```powerapps-dot
    If( Form1.Unsaved Or Form1.Mode = FormMode.New, DisplayMode.Disabled, DisplayMode.Edit )
    ```

    > [!div class="mx-imgBorder"]
    > ![Set la propiedad DisplayMode del icono Add @ no__t-1

    La fórmula deshabilita el icono Agregar en estas condiciones:

    - El usuario realiza cambios pero no los guarda o los cancela, lo que es el comportamiento opuesto de los iconos comprobar y cancelar.
    - El usuario selecciona el icono Agregar pero no realiza ningún cambio.

1. Establezca la propiedad **DisabledColor** del icono Agregar en este valor:

    ```powerapps-dot
    Gray
    ```

    > [!div class="mx-imgBorder"]
    > ![Set la propiedad DisabledColor del icono Add @ no__t-1

    El usuario puede crear un pedido si no realiza ningún cambio o guarda o cancela los cambios realizados. (Si el usuario selecciona este icono, no podrá volver a seleccionarlo hasta que realice uno o varios cambios y, a continuación, guardar o cancelar los cambios):

    > [!div class="mx-imgBorder"]
    > @no__t: 0Create un pedido @ no__t-1

> [!NOTE]
> Si crea y guarda un pedido, es posible que tenga que desplazarse hacia abajo en la galería de pedidos para mostrar el nuevo pedido. No tendrá un precio total porque todavía no ha agregado ningún detalle de pedido.

## <a name="add-a-trash-icon"></a>Agregar un icono de papelera

1. En la pestaña **Insertar** , seleccione **iconos** > **Trash**.

    > [!div class="mx-imgBorder"]
    > @no__t: 0Insert un icono de papelera @ no__t-1

    De forma predeterminada, aparece el icono de la **papelera** en la esquina superior izquierda, donde otros controles pueden dificultar la búsqueda:

    > [!div class="mx-imgBorder"]
    > ![Default Ubicación del icono de la papelera @ no__t-1

1. En la pestaña **Inicio** , cambie la propiedad **color** del icono de la papelera a blanco, cambie el tamaño del icono y muévalo a la izquierda del icono Agregar:

    > [!div class="mx-imgBorder"]
    > @no__t: 0Change el color, el tamaño y la ubicación del icono de la papelera @ no__t-1

1. Establezca la propiedad **alseleccionar** del icono de la papelera en esta fórmula:

    ```powerapps-dot
    Remove( Orders, Gallery1.Selected )
    ```

    > [!div class="mx-imgBorder"]
    > ![Set la propiedad alseleccionar del icono de la papelera @ no__t-1

    La función [**Remove**](functions/function-remove-removeif.md) quita un registro de un origen de datos. En esta fórmula, la función quita el registro seleccionado en la galería de pedidos. El icono de la papelera aparece cerca del formulario de resumen (no de la galería de pedidos) porque el formulario muestra más detalles sobre el registro, por lo que el usuario puede identificar más fácilmente el registro que la fórmula eliminará.

1. Establezca la propiedad **DisplayMode** del icono de la papelera en esta fórmula:

    ```powerapps-dot
    If( Form1.Mode = FormMode.New, DisplayMode.Disabled, DisplayMode.Edit )
    ```

    > [!div class="mx-imgBorder"]
    > ![Set la propiedad DisplayMode del icono de la papelera @ no__t-1

    Esta fórmula deshabilita el icono de la papelera si el usuario está creando un registro. Hasta que el usuario guarda el registro, la función **Remove** no tiene ningún registro para eliminar.

1. Establezca la propiedad **DisabledColor** del icono de la papelera en este valor:

    ```powerapps-dot
    Gray
    ```

    > [!div class="mx-imgBorder"]
    > ![Set la propiedad DisabledColor del icono de la papelera @ no__t-1

    El usuario puede eliminar un pedido.

    > [!div class="mx-imgBorder"]
    > @no__t: 0Deleting Orders @ no__t-1

## <a name="summary"></a>Resumen

En Resumen, ha agregado un formulario en el que el usuario puede mostrar y editar un resumen de cada pedido, y ha usado estos elementos:

- Un formulario que muestra los datos de la entidad **Orders** : **Form1. DataSource =** `Orders`
- Una conexión entre el formulario y la galería de pedidos: **Form1. Item =** `Gallery1.Selected`
- Un control alternativo para el campo de **número de pedido** : **Ver texto**
- Una relación de varios a uno para mostrar la imagen del empleado en la tarjeta de datos del **empleado** : `DataCardValue1.Selected.Picture`
- Un icono para guardar los cambios en un pedido: `SubmitForm( Form1 )`
- Un icono para cancelar los cambios en un pedido: `ResetForm( Form1 )`
- Un icono para crear un pedido: `NewForm( Form1 )`
- Un icono para eliminar un pedido: `Remove( Orders, Gallery1.Selected )`

## <a name="next-step"></a>Paso siguiente

En el tema siguiente, agregará otra galería para mostrar los productos en cada pedido y podrá cambiar esos detalles mediante la función [**patch**](functions/function-patch.md) .

> [!div class="nextstepaction"]
> [Crear la galería de detalles](northwind-orders-canvas-part3.md)
