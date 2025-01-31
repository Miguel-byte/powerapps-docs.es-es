---
title: 'Ejemplo: Crear un correo electrónico utilizando una plantilla (Common Data Service) | Microsoft Docs'
description: Este ejemplo muestra cómo crear una instancia de un registro de correo electrónico.
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: samples
author: brandonsimons
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="sample-create-an-email-using-a-template"></a>Ejemplo: crear un mensaje de correo electrónico usando una plantilla

Este ejemplo muestra cómo crear una instancia de registro de mensaje de correo electrónico usando el mensaje [InstantiateTemplateRequest](https://docs.microsoft.com/dotnet/api/microsoft.crm.sdk.messages.instantiatetemplaterequest?view=dynamics-general-ce-9). Puede descargar el ejemplo desde [aquí](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/orgsvc/C%23/EmailTemplate). 

## <a name="how-to-run-this-sample"></a>Cómo ejecutar esta muestra

[!include[cc-how-to-run-samples](../../includes/cc-how-to-run-samples.md)]

## <a name="what-this-sample-does"></a>Qué hace este ejemplo

El mensaje `InstantiateTemplateRequest` está diseñado para usarse en un escenario donde crea instancias de un registro de correo electrónico.

## <a name="how-this-sample-works"></a>Cómo funciona esta muestra

Para simular el escenario descrito en [Qué hace este ejemplo](#what-this-sample-does), la muestra hará lo siguiente:

### <a name="setup"></a>Configuración

1. Comprobaciones para la versión actual de la organización.
1. Crea un registro de cuenta. 
2. Define el cuerpo y el tema de la plantilla de correo electrónico en el formato **XML**.
3. Crea una plantilla de correo electrónico.

### <a name="demonstrate"></a>Demostración

1. El mensaje `InstantiateTemplateRequest` se usa para crear un mensaje de correo electrónico mediante una plantilla. 
2. Serialice el correo electrónico en **XML** y guárdelo en un archivo.


### <a name="clean-up"></a>Limpiar

1. Muestra una opción para eliminar el registro creado en [Configuración](#setup).
    La eliminación es opcional en caso de que desee examinar las entidades y los datos creados por el ejemplo. Puede eliminar manualmente los registros para obtener el mismo resultado.
