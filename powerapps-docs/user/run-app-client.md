---
title: Ejecución de una aplicación basada en lienzo en un dispositivo móvil | Microsoft Docs
description: Vea cómo ejecutar una aplicación de lienzo en un dispositivo móvil.
author: Mattp123
ms.service: powerapps
ms.component: pa-user
ms.topic: quickstart
ms.date: 11/16/2018
ms.author: matp
ms.custom: ''
ms.reviewer: ''
ms.assetid: ''
search.audienceType:
- enduser
search.app:
- PowerApps
- D365CE
ms.openlocfilehash: 9f951167f56ffd3d211182a89a21d54916ee6b6e
ms.sourcegitcommit: 483c777a1537ccab6a2a2da6a5d1fe4470dd0e7e
ms.translationtype: MT
ms.contentlocale: es-ES
ms.lasthandoff: 06/19/2019
ms.locfileid: "61531950"
---
# <a name="run-a-canvas-app-on-a-mobile-device"></a>Ejecución de una aplicación de lienzo en un dispositivo móvil
Cuando crea una aplicación o alguien comparte una aplicación con usted, puede ejecutar la aplicación en Windows, iOS, Android o en un explorador web. En este tema aprenderá a ejecutar una aplicación de lienzo en un dispositivo móvil. Las aplicaciones que se ejecutan en un dispositivo móvil pueden aprovechar las funcionalidades del dispositivo, como los servicios de ubicación y la cámara.

Para seguir este procedimiento, si no está registrado en PowerApps, [regístrese gratuitamente](https://web.powerapps.com/signup?redirect=marketing&email=) antes de empezar y, después, descargue PowerApps desde [App Store](https://itunes.apple.com/app/powerapps/id1047318566?mt=8) o [Google Play](https://play.google.com/store/apps/details?id=com.microsoft.msapps) en dispositivos iPhone, iPad o Android que ejecuten un [sistema operativo compatible](../maker/canvas-apps/limits-and-config.md). Además, asegúrese de que tiene acceso a una aplicación de lienzo que ha creado o que otra persona ha creado y compartido con usted.

## <a name="open-powerapps-and-sign-in"></a>Abrir PowerApps e iniciar sesión
Abra PowerApps en el dispositivo móvil e inicie sesión con sus credenciales de Azure Active Directory.

![Usuario de inicio de sesión](./media/run-app-client/run-client-login.png)

Si tiene la aplicación Microsoft Authenticator instalada en el dispositivo móvil, simplemente escriba el nombre de usuario cuando se le solicite y, después, apruebe la notificación enviada al dispositivo.

## <a name="find-the-app"></a>Buscar la aplicación
Para que sea más fácil encontrar la aplicación, abra el menú **PowerApps** y, después, seleccione un filtro.

![Filtros de aplicación](./media/run-app-client/filter-menu.png)

Los siguientes filtros están disponibles:

* **Todas las aplicaciones**: Muestra todas las aplicaciones a las que tiene acceso, incluidas las aplicaciones que creó y las aplicaciones que otros compartieron con usted.

* **Mis aplicaciones**: Muestra las aplicaciones que ha ejecutado al menos una vez.

* **Aplicaciones de ejemplo**: Muestra aplicaciones de ejemplo de Microsoft que muestran escenarios de aplicaciones reales con datos ficticios para ayudarle a explorar las posibilidades de diseño.

* **Favoritos**: Muestra las aplicaciones que ha marcado pulsando el botón de puntos suspensivos (...) en el icono de la aplicación y, a continuación, puntee en **favorito**. Para quitar una aplicación de esta lista, pulse los puntos suspensivos (...) en el icono de la aplicación y, después, pulse **Quitar de Favoritos**.

    ![Marcar como favorito](./media/run-app-client/favorite.png)

Después de filtrar las aplicaciones, puede ordenar la lista filtrada por la fecha de la última vez que se abrieron o modificaron, o bien alfabéticamente por nombre. Estas preferencias se conservan cuando cierra y vuelve a abrir PowerApps.

![Menú Ordenar](./media/run-app-client/sort-menu.png)

Si conoce el nombre de la aplicación que quiere ejecutar, pulse el icono de búsqueda en la parte superior de Powerapps y, después, escriba parte del nombre en el cuadro de búsqueda.

![Buscar](./media/run-app-client/search.png)

Si filtró las aplicaciones, se buscará en la lista filtrada.

## <a name="run-an-app"></a>Ejecutar una aplicación
Para ejecutar una aplicación de lienzo en un dispositivo móvil, pulse el icono de la aplicación. Si otro usuario creó la aplicación de lienzo y la compartió con usted en un correo electrónico, puede ejecutar la aplicación, si pulsa el vínculo del correo electrónico.

Si es la primera vez que usa PowerApps, en una pantalla se muestra el gesto de deslizar rápidamente para cerrar la aplicación.

![Iniciar aplicación](./media/run-app-client/run-client-app.png)

## <a name="give-consent"></a>Dar consentimiento
Si una aplicación requiere una conexión a un origen de datos o permiso para usar las funcionalidades del dispositivo (como la cámara o los servicios de ubicación), debe dar su consentimiento antes de usar la aplicación. Habitualmente, solo se le solicitará la primera vez.

![Connection](./media/run-app-client/app-connection.png)

## <a name="pin-an-app-to-the-home-screen"></a>Anclar una aplicación a la pantalla de inicio
Puede anclar una aplicación a la pantalla de inicio del dispositivo para un acceso rápido. Pulse los puntos suspensivos (...) del icono de la aplicación, pulse **Anclar a página principal** y, luego, siga las instrucciones que aparecen.

![Anclar aplicación](./media/run-app-client/run-client-pin.png)

## <a name="close-an-app"></a>Cerrar una aplicación
Para cerrar una aplicación, use el dedo para deslizarlo desde el borde izquierdo de la aplicación a la derecha. En los dispositivos Android, también puede presionar el botón Atrás y luego confirmar que quiere cerrar la aplicación.

## <a name="next-steps"></a>Pasos siguientes
En este tema ha aprendido a ejecutar una aplicación de lienzo en un dispositivo móvil. También puede ejecutar aplicaciones controladas por modelos en un dispositivo móvil.

> [!div class="nextstepaction"]
> [Ejecución de una aplicación controlada por modelos en un dispositivo móvil](run-app-client-model-driven.md)
