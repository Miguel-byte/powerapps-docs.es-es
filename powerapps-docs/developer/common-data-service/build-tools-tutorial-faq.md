---
title: Tutorial sobre herramientas de compilación y preguntas más frecuentes| Microsoft Docs
description: 'Las herramientas de compilación de PowerApps son una colección de tareas de compilación de Azure DevOps específicas de PowerApps que eliminan la necesidad de descargar manualmente los scripts para administrar el desarrollo de PowerApps. En este tema se describen el tutorial y las preguntas más frecuentes a los que puede tener acceso para obtener más información sobre estas herramientas. '
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

# <a name="tutorial-and-faq"></a>Tutorial y preguntas más frecuentes


[!INCLUDE [cc-beta-prerelease-disclaimer](../../includes/cc-beta-prerelease-disclaimer.md)]
Utilice el tutorial y las preguntas más frecuentes para obtener más información acerca de las herramientas de compilación de PowerApps para Azure DevOps. 

## <a name="hands-on-lab"></a>Laboratorio práctico

El laboratorio práctico está disponible [aquí](https://github.com/microsoft/PowerApps-Samples/tree/master/azure/build-tools)

El laboratorio práctico proporciona un tutorial con instrucciones paso a paso sobre cómo crear el siguiente escenario:

1. Configurar los entornos de desarrollo, compilación y producción.
2. Crear una aplicación de ejemplo.
3. Exportar una solución que contiene la aplicación de ejemplo desde un entorno de desarrollo.
4. Desempaquete la solución.
5. Confirme solución a origen (informe).
6. Importe la solución no administrada a un entorno de compilación.
7. Genere un artefacto de compilación (solución administrada).
8. Implemente la solución a un entorno de bajada.

> [!NOTE]
> El laboratorio práctico se proporciona para ofrecer experiencia práctica para los usuarios nuevos en Azure DevOps que desean aprender a crear canalizaciones en Azure DevOps. Las canalizaciones terminadas que terminará desarrollando también se pueden descargar del tutorial y usarse tal como están con unos pocos ajustes en variables de entorno, carpetas de origen y destino, y repositorios.  

## <a name="frequently-asked-question-faq"></a>Preguntas más frecuentes (P+F)

**¿Las herramientas de compilación de PowerApps funcionan sólo para PowerApps?**  

*Las herramientas de compilación de PowerApps funciona para PowerApps y Dynamics for Customer Engagement (las aplicaciones de Dynamics 365 CE están basadas en modelo). Hay disponibles tareas de compilación aparte para Microsoft Dynamics Finance and Operations.*

**¿Puedo incluir aplicaciones de flujo y de lienzo?**

*Sí, las aplicaciones de flujo y lienzo son compatibles con las soluciones. Por tanto, si se agregan a la solución, pueden participar en el ciclo de vida de su aplicación. Sin embargo, algunos pasos siguen requiriendo configuraciones manuales. Este aspecto se abordará más adelante este año cuando introduzcamos variables de entorno y conectores.*

**¿Cuánto cuestan las herramientas de compilación de PowerApps?**

*Las herramientas de compilación de PowerApps están disponibles sin coste alguno. Sin embargo, una suscripción válida a Azure DevOps es necesaria para usar las herramientas de compilación. Más información está disponible [aquí](https://azure.microsoft.com/en-us/pricing/details/devops/azure-devops-services/).*

**Veo la extensión, pero ¿por qué no tengo la opción de instalarla?**

*Si no ve la opción **instalar** (que se muestra en la captura de pantalla siguiente) es probable que le falten los privilegios de instalación necesarios en la Organización de Azure DevOps. Más información disponible [aquí](https://docs.microsoft.com/en-us/azure/devops/marketplace/how-to/grant-permissions?view=azure-devops).*

![Pantalla de tareas de compilación](media/build-tasks.png)