---
title: Almacenamiento y publicación de una aplicación de lienzo | Microsoft Docs
description: Instrucciones paso a paso para guardar y publicar aplicaciones de lienzo para creadores de aplicaciones
author: tapanm-msft
manager: kvivek
ms.service: powerapps
ms.topic: conceptual
ms.custom: canvas
ms.reviewer: ''
ms.date: 09/14/2017
ms.author: tapanm
search.audienceType:
- maker
search.app:
- PowerApps
ms.openlocfilehash: 19d793b879d42e9446cc8ad366bc08879162185d
ms.sourcegitcommit: 7dae19a44247ef6aad4c718fdc7c68d298b0a1f3
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 10/07/2019
ms.locfileid: "71995767"
---
# <a name="save-and-publish-a-canvas-app-in-powerapps"></a>Almacenamiento y publicación de una aplicación de lienzo en PowerApps
Siempre que guarde cambios en una aplicación de lienzo, se publican automáticamente solo para usted y para quien tenga permisos para modificar la aplicación. Cuando termine de realizar cambios, publíquelos explícitamente para que estén disponibles para todos los usuarios con los que se comparta la aplicación.

Para información sobre cómo compartir una aplicación, consulte [Compartir una aplicación](share-app.md).

## <a name="save-changes-to-an-app"></a>Guardar cambios en una aplicación
En PowerApps Studio, pulse o haga clic en **Guardar** en el menú **Archivo** (en el borde izquierdo) y siga cualquiera de estos pasos:

* Si no ha guardado la aplicación nunca, proporciónele un nombre y pulse o haga clic en **Guardar**.

    ![Guardar nueva aplicación](./media/save-publish-app/save-as.png)
* Si alguna vez ha guardado la aplicación, pulse o haga clic en **Guardar**.  

    ![Guardar aplicación actualizada](./media/save-publish-app/save-app.png)

PowerApps también puede guardar la aplicación periódicamente cada 2 minutos. Si ha guardado la aplicación una vez, PowerApps volverá a guardar una versión de ella periódicamente sin que el usuario tenga que hacer clic o pulsar la acción Guardar. Los autores pueden habilitar o deshabilitar la opción **Guardado automático** de la pestaña **Cuenta** del menú **Archivo**.

![Opción Guardado automático](./media/save-publish-app/autosave.png)

## <a name="publish-an-app"></a>Publicar una aplicación
1. En PowerApps Studio, pulse o haga clic en **Guardar** en el menú **Archivo** (en el borde izquierdo) y, después, en **Publicar esta versión**.

    ![Publicar la aplicación](./media/save-publish-app/publish-app.png)
2. En el cuadro de diálogo **Publicar**, pulse o haga clic en **Publicar esta versión** para publicar la aplicación para todos los usuarios con los que se comparte la aplicación.

   ![Revisar la publicación](./media/save-publish-app/publish-review.png)

   > [!NOTE]
   > Siempre que publique una aplicación de lienzo, esta se actualizará para ejecutarse en la versión más reciente de PowerApps, lo que significa que obtendrá las ventajas de todas las características más recientes y las actualizaciones de rendimiento que se han agregado desde que publicó por última vez. Si no ha publicado una actualización desde hace varios meses, probablemente verá una mejora de rendimiento inmediata al volver a publicar ahora.

## <a name="identify-the-live-version"></a>Identificar la versión activa
En [powerapps.com](https://web.powerapps.com?utm_source=padocs&utm_medium=linkinadoc&utm_campaign=referralsfromdoc), pulse o haga clic en **Aplicaciones** en el menú **Archivo** (en el borde izquierdo), después en el icono de detalles para una aplicación y, por último, en la pestaña **Versiones**.

La versión **Activa** está publicada para todos los usuarios con quien se comparte la aplicación. La versión más reciente de cualquier aplicación está disponible solo para quienes tienen permisos de edición para ella.

![Publicar desde el portal](./media/save-publish-app/publish-portal.png)

Para publicar la versión más reciente, pulse o haga clic en **Publicar esta versión** y pulse o haga clic en **Publicar esta versión** en el cuadro de diálogo **Publicar**.

## <a name="next-steps"></a>Pasos siguientes
* Busque y ejecute la aplicación en un [Explorador](../../user/run-app-browser.md) o en un [teléfono](../../user/run-app-client.md).
* [Cambie el nombre de una aplicación](set-name-tile.md) desde powerapps.com.
* [Restaure una aplicación](restore-an-app.md) si tiene varias versiones de una aplicación.
