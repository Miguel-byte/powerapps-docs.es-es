---
title: Uso sin conexión de los servicios de Dynamics 365 (Common Data Service) | Microsoft Docs
description: Obtenga información sobre cómo los distintos servicios de Dynamics 365 se pueden utilizar sin conexión. Hay varios mensajes que se admiten sin conexión. También puede determinar si un mensaje IOrganizationService funciona sin conexión si comprueba el atributo SdkMessage.Availability del mensaje deseado.
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: sriharibs
ms.author: jdaly
manager: ryjones
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---

# <a name="offline-use-of-services"></a>Uso sin conexión de servicios

Dynamics 365 for Microsoft Office Outlook con acceso sin conexión le permite continuar el trabajo cuando está desconectado del servidor.  
  
 Además, la infraestructura de evento y complemento le permite aprovechar las inversiones de desarrollo en todas las soluciones ya que utiliza las mismas API y el mismo modelo de programación. Los métodos de <xref:Microsoft.Xrm.Sdk.IOrganizationService> y los métodos del servicio OData de Customer Common Data Service funcionan con conexión y sin conexión. Cuando se usa un método como `Create` o `Update` sin conexión, los datos se escriben localmente y, cuando el usuario se conecta al servidor, las acciones se reproducen en el servidor.  
  
 Para obtener más información acerca de si se admite un mensaje sin conexión, consulte <xref:Microsoft.Crm.Sdk.Messages>. También puede determinar si un mensaje de <xref:Microsoft.Xrm.Sdk.IOrganizationService> funciona sin conexión al comprobar el atributo `SdkMessage.Availability` para el mensaje deseado. Si el mensaje funciona para varios tipos de entidades, también debe comprobar el atributo `SdkMessageFilter.Availability` para ver si el mensaje está disponible sin conexión para la entidad con la que desea trabajar. Por ejemplo, el mensaje `Create` está disponible sin conexión, pero no para la cola, el usuario o las entidades del sitio.  
  
 El seguimiento se puede habilitar en Dynamics 365 for Microsoft Office Outlook con acceso sin conexión para depurar. Para obtener más información sobre cómo realizar un seguimiento del visor de eventos y de la plataforma, consulte [Supervisión y solución de problemas de Dynamics 365](https://technet.microsoft.com/library/hh699694.aspx).  
  
### <a name="see-also"></a>Vea también  
 [Ampliar Dynamics 365 Customer Engagement en el servidor](/dynamics365/customer-engagement/developer/extend-dynamics-365-server)   
 [Solución de problemas y control de errores](/dynamics365/customer-engagement/developer/org-service/troubleshooting-error-handling)   
 <xref:Microsoft.Xrm.Sdk.IOrganizationService>   
 [Métodos de servicio de organización](/dynamics365/customer-engagement/developer/org-service/organization-service-methods)   
 <xref:Microsoft.Xrm.Sdk.IOrganizationService.Create*>   
 <xref:Microsoft.Xrm.Sdk.IOrganizationService.Update*>