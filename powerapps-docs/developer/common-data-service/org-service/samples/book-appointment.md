---
title: 'Ejemplo: Reservar una cita (Common Data Service) | Microsoft Docs'
description: 'En este ejemplo muestra cómo reservar o programar una cita '
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: brandonsimons
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="sample-book-an-appointment"></a>Ejemplo: reservar una cita

<!-- https://docs.microsoft.com/dynamics365/customer-engagement/developer/sample-book-appointment -->

Este ejemplo muestra cómo reservar o programar una cita mediante el mensaje [BookRequest](https://docs.microsoft.com/dotnet/api/microsoft.crm.sdk.messages.bookrequest?view=dynamics-general-ce-9). Puede descargar el ejemplo desde [aquí](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/BookAppointment).

## <a name="how-to-run-this-sample"></a>Cómo ejecutar esta muestra

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="what-this-sample-does"></a>Qué hace este ejemplo

El mensaje `BookRequest` está diseñado para usarse en un escenario para reservar o para programar una cita.

## <a name="how-this-sample-works"></a>Cómo funciona esta muestra

Para simular el escenario descrito en [Qué hace este ejemplo](#what-this-sample-does), la muestra hará lo siguiente:

### <a name="setup"></a>Configuración

1. Comprueba la versión actual de la organización.
1. Obtiene la información de usuario actual y crea la instancia de ActivityParty.

### <a name="demonstrate"></a>Demostración

1. Crea la instancia de la cita con el mensaje [BookRequest](https://docs.microsoft.com/dotnet/api/microsoft.crm.sdk.messages.bookrequest?view=dynamics-general-ce-9) y comprueba si se ha programado la cita o no.

### <a name="clean-up"></a>Limpiar

1. Muestra una opción para eliminar los registros creados en la [Configuración](#setup).

    La eliminación es opcional en caso de que desee examinar las entidades y los datos creados por el ejemplo. Puede eliminar manualmente los registros para obtener el mismo resultado.
