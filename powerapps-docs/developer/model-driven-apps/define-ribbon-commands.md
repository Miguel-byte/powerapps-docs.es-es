---
title: Definir comandos de la cinta de opciones (aplicaciones basadas en modelos) | Microsoft Docs
description: Un comando de la cinta de opciones crea una definición reutilizable a la que los elementos de control de la cinta de opciones pueden hacer referencia.
keywords: ''
ms.date: 10/31/2018
ms.service: powerapps
ms.custom:
  - ''
ms.topic: article
ms.assetid: 60933770-8c7c-499c-12b4-8b64f6eedb35
author: JimDaly
ms.author: jdaly
manager: shilpas
ms.reviewer: null
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---

# <a name="define-ribbon-commands"></a>Definir comandos de la cinta de opciones

<!-- https://docs.microsoft.com/dynamics365/customer-engagement/developer/customize-dev/define-ribbon-commands -->

Un comando *de la cinta de opciones* crea una definición reutilizable a la que los elementos de control de la cinta de opciones pueden hacer referencia.  
  
## <a name="ribbon-command-elements"></a>Elementos del comando de la cinta de opciones  
 El elemento `<CommandDefinition>` define un comando en la cinta de opciones. El atributo `Id` especifica un identificador único para el comando al que los elementos de control de la cinta de opciones pueden hacer referencia con el parámetro `Command`.  
  
 Un comando de la cinta de opciones define tres cosas:  
  
- **Reglas de habilitación**: especifica si se habilita un control de la cinta de opciones específico.  
  
- **Reglas de visualización**: especifica si se puede ver un elemento específico de la cinta de opciones.  
  
- **Acciones**: especifica el código que se ejecuta cuando se usa un control de la cinta de opciones.  
  
> [!IMPORTANT]
>  Todas las definiciones del comando se descargan en el equipo de un usuario para poder evaluarlas en tiempo de ejecución. Esto significa que un usuario sin los privilegios para ver un determinado control en la cinta de opciones puede usar el comando del explorador **Ver código fuente**, revisar el código y determinar que existe un control que no puede ver.  
  
### <a name="see-also"></a>Vea también  
 [Personalización de comandos y la cinta de opciones](customize-commands-ribbon.md)   
 [Usar etiquetas localizadas con cintas de opciones](use-localized-labels-ribbons.md)   
 [Definir las reglas de habilitación de la cinta de opciones](define-ribbon-enable-rules.md)
