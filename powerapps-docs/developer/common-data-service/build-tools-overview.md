---
title: Información general sobre herramientas de compilación para Azure DevOps| Microsoft Docs
description: Las herramientas de compilación de PowerApps son una colección de tareas de compilación de Azure DevOps específicas de PowerApps que eliminan la necesidad de descargar manualmente los scripts para administrar el desarrollo de PowerApps
ms.custom: ''
ms.date: 07/21/2019
ms.reviewer: Dean-Haas
ms.service: powerapps
ms.topic: article
author: mikkelsen2000
ms.author: pemikkel
manager: kvivek
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---

# <a name="powerapps-build-tools-for-azure-devops-overview"></a>Información general sobre las herramientas de compilación de PowerApps para Azure DevOps


[!INCLUDE [cc-beta-prerelease-disclaimer](../../includes/cc-beta-prerelease-disclaimer.md)]

Utilice las herramientas de compilación de PowerApps para automatizar tareas comunes de compilación y de implementación relacionadas con PowerApps. Esto incluye la sincronización de los metadatos de la solución (es decir, las soluciones) entre entornos de desarrollo y control de origen, generar artefactos de compilación, implementar en entornos descendentes, aprovisionamiento o desaprovisionamiento de entornos, y la capacidad de realizar comprobaciones de análisis estático con la solución utilizando el servicio del comprobador de PowerApps.

> [!IMPORTANT]
>
> - Las herramientas de compilación de PowerApps son una característica de vista previa.
> - [!INCLUDE [cc-preview-features-definition](../../includes/cc-preview-features-definition.md)]

  
## <a name="what-are-powerapps-build-tools"></a>¿Qué son las herramientas de compilación de PowerApps?

Las herramientas de compilación de PowerApps son una colección de tareas de compilación de Azure DevOps específicas de PowerApps que eliminan la necesidad de descargar manualmente las herramientas y los scripts personalizados para administrar el ciclo de vida de la aplicación de PowerApps. Las tareas pueden usarse individualmente para realizar una tarea simple, como importar una solución en un entorno descendente, o usarse juntas en una canalización para coordinar un escenario, como “Genera artefacto de compilación”, “Implementa para probar“ o “Recoger cambios del creador”. Las tareas de compilación se pueden clasificar en general en cuatro tipos:

- Ayuda 
- Comprobación de calidad 
- Solución 
- Administración de entornos 

## <a name="get-the-powerapps-build-tools"></a>Obtener las herramientas de compilación de PowerApps 
Las herramientas de compilación de PowerApps se pueden instalar en la organización de Azure DevOps desde el [Azure Marketplace](https://marketplace.visualstudio.com/items?itemName=microsoft-IsvExpTools.PowerApps-BuildTools). Una vez instaladas, todas las taras incluidas en las herramientas de compilación de PowerApps estarán disponibles para agregar en cualquier canalización nueva o existente y son fáciles de encontrar buscando **PowerApps**.

![Obtener herramientas de compilación](media/build-tools-download.png)
 
## <a name="next-step"></a>Paso siguiente

[Tareas de herramientas de compilación](build-tools-tasks.md)
