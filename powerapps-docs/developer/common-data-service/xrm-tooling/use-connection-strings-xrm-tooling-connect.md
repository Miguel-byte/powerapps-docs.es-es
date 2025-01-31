---
title: Usar cadenas de conexión en útiles de XRM para conectarse a Common Data Service (Common Data Service)| Microsoft Docs
description: Los útiles de XRM le permiten conectarse a su entorno de Common Data Service mediante las cadenas de conexión
ms.custom: ''
ms.date: 03/27/2019
ms.reviewer: ''
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: a98b2fce-df49-4b60-91f4-a4446aa61cd3
caps.latest.revision: 21
author: MattB-msft
ms.author: nabuthuk
manager: kvivek
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="use-connection-strings-in-xrm-tooling-to-connect-to-common-data-service"></a>Usar cadenas de conexión en útiles de XRM para conectarse a Common Data Service

Con Common Data Service, los útiles de XRM le permiten conectarse a su entorno de Common Data Service mediante las cadenas de conexión. Esto es similar al concepto de cadenas de conexión que se utilizan con **SQL Server**. Las cadenas de conexión tienen compatibilidad nativa en archivos de configuración, incluida la capacidad de cifrar las secciones de configuración para máxima seguridad. Esto permite configurar las conexiones de Common Data Service en tiempo de implementación, y no codificar de forma rígida en su aplicación para conectarse al entorno de Common Data Service.  

> [!NOTE]
> [!INCLUDE[cc-d365ce-note-topic](../includes/cc-d365ce-note-topic.md)] [Usar cadenas de conexión para conectarse a Customer Engagement](/dynamics365/customer-engagement/developer/xrm-tooling/use-connection-strings-xrm-tooling-connect)

<a name="Create"></a> 

## <a name="create-a-connection-string"></a>Crear una cadena de conexión

 Especifique la cadena de conexión en el archivo `app.config` o `web.config` del proyecto, como se muestra en el ejemplo siguiente.  
  
```xml  
<connectionStrings>  
    <add name="MyCDSServer" connectionString="AuthType=Office365;Url=http://contoso:8080/Test;UserName=jsmith@contoso.onmicrosoft.com; 
  Password=passcode" />  
</connectionStrings>  
```  
  
> [!IMPORTANT]
> Si agrega alguna información confidencial al `web.config file` o `app.config`, como la contraseña de una cuenta, asegúrese de tomar las precauciones de seguridad adecuadas para proteger la información.  
  
 Después de crear la cadena de conexión, úsela para crear un objeto <xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient>.  
  
```csharp  
//Use the connection string named "MyCDSServer"  
//from the configuration file  
CrmServiceClient svc = new CrmServiceClient(ConnectionString);  
```  
  
> [!NOTE]
> Tendrá que usar la directiva `using` en siguiente el código para hacer referencia al espacio de nombres de `System.Configuration` para obtener acceso a la cadena de conexión en el código: `using System.Configuration;`  
  
 Después de crear un objeto <xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient>, puede usar el objeto para realizar acciones en Common Data Service. Más información: [Use los útiles XRM para ejecutar acciones en Common Data Service](use-xrm-tooling-execute-actions.md)  
  
<a name="Parameters"></a>

## <a name="connection-string-parameters"></a>Parámetros de la cadena de conexión

 La cadena de conexión contiene una serie de pares de name=value separados por punto y coma. La siguiente tabla muestra los parámetros admitidos, que se pueden escribir en cualquier orden.  
  
|Nombre del parámetro|Descripción|  
|--------------------|-----------------|  
|`ServiceUri`, `Service Uri`, `Url` o `Server`|Especifica la dirección URL del entorno de Common Data Service La URL puede utilizar el protocolo http o https, y el puerto es opcional. El puerto predeterminado es 80 para el protocolo http y 443 para el protocolo https. La dirección URL del servidor suele encontrarse en el formato `https://`*`<organization-name>`*`.crm.dynamics.com`<br /><br /> Se requiere el nombre de la organización.|  
|`Domain`|Especifica el dominio que comprobará las credenciales de usuario.|  
|`UserName`, `User Name`, `UserId` o `User Id`|Especifica el nombre de identificación del usuario asociado con las credenciales.|  
|`Password`|Especifica la contraseña del nombre de usuario asociado con las credenciales.|  
|`HomeRealmUri` o `Home Realm Uri`|Especifica el Uri de dominio de inicio|  
|`AuthenticationType` o `AuthType`|Especifica el tipo de autenticación para conectarse al entorno de Common Data Service. Los valores válidos son: `AD`, `IFD` (AD FS habilitado), `OAuth` o `Office365`.<br /><br /> -   `AD` y `IFD` se permiten para entornos locales de Common Data Service únicamente.<br />-   `OAuth` se permite para entornos de Common Data Service y locales.<br />-   `Office365` se permite solo para entornos de Common Data Service y locales.|  
|`RequireNewInstance`|Indica si se debe volver a usar una conexión existente si se vuelve a hacer la llamada mientras la conexión sigue activa. El valor predeterminado es `false` que indica que la conexión existente se reutilizará. Si se establece en `true`, se obliga al sistema a crear una conexión única.|  
|`ClientId`, `AppId` o `ApplicationId`|Especifica el `ClientID` asignado cuando se registró su aplicación en Azure Active Directory o Servicios de federación de Active Directory (AD FS).<br /><br /> Este parámetro es aplicable solo cuando especifica el tipo de autenticación como `OAuth`.|  
|`RedirectUri` o `ReplyUrl`|Especifica el URI de redirección de la aplicación que registró en Azure Active Directory o Servicios de federación de Active Directory (AD FS).<br /><br /> Este parámetro es aplicable solo cuando especifica el tipo de autenticación como `OAuth`.|  
|`TokenCacheStorePath`|Especifica la ruta de acceso completa a la ubicación donde la memoria caché del símbolo de usuario debe ser almacenada. El proceso en ejecución debe tener acceso a la ruta especificada. Es responsabilidad de los procesos establecer y configurar esta ruta.<br /><br /> Este parámetro es aplicable solo cuando especifica el tipo de autenticación como `OAuth`.|  
|`LoginPrompt`|Especifica si se le piden al usuario credenciales si las credenciales no se proporcionan. Los valores válidos son:<br /><br /> -   `Always`: Pide siempre al usuario que especifique credenciales.<br />-   `Auto`: Permite que el usuario seleccione en la interfaz de control de inicio de sesión si se muestra un mensaje o no.<br />-   `Never`: No pide al usuario que especifique credenciales. Si usa un método de conexión que no tiene interfaz de usuario, debe usar este valor.<br /><br /> Este parámetro es aplicable solo cuando especifica el tipo de autenticación como `OAuth`.|  
|`StoreName` o `CertificateStoreName`|Especifica el nombre del almacén donde el certificado identificado por huella digital se encuentra. Cuando está establecida, se requiere Huella digital.|
|`Thumbprint` o `CertThumbprint`| Especifica la huella digital del certificado que se usará durante una conexión S2S. Cuando se establece, se requiere AppID y se omiten los valores UserID y Password.|
|`SkipDiscovery`|Especifica si se llama detección de instancia para determinar el uri de conexión para una instancia determinada. A partir de la versión de NuGet Microsoft.CrmSdk.XrmTooling.CoreAssembly Versión 9.0.2.7, predeterminado = true. Las versiones más antiguas establecen de forma predeterminada como false. <br/> Nota: Si se establece en true, es importante que el usuario proporcione el URI correcto y preciso para la instancia de destino.|

<a name="Examples"></a>

## <a name="connection-string-examples"></a>Ejemplos de cadena de conexión
 
Los ejemplos siguientes muestran cómo usar cadenas de conexión para conectar con implementaciones y escenarios de autenticación. Los ejemplos de la cadena de conexión para instancias locales y de implementación IFD están ahora disponibles en la documentación de Customer Engagement en: [Usar cadenas de conexión en útiles de XRM para conectarse a Customer Engagement](/dynamics365/customer-engagement/developer/xrm-tooling/use-connection-strings-xrm-tooling-connect) 

### <a name="named-account-using-office-365"></a>Cuenta con nombre utilizando Office 365  
  
```xml
<add name="MyCDSServer" 
 connectionString="
  AuthType=Office365;
  Username=jsmith@contoso.onmicrosoft.com; 
  Password=passcode;
  Url=https://contoso.crm.dynamics.com"/>  
```  
  
### <a name="oauth-using-named-account-in-office-365-with-ux-to-prompt-for-authentication"></a>OAuth utilizando cuenta con nombre en Office 365 con UX para solicitar autenticación  
  
```xml
<add name="MyCDSServer"
 connectionString="
  AuthType=OAuth;
  Username=jsmith@contoso.onmicrosoft.com;
  Password=passcode;
  Url=https://contosotest.crm.dynamics.com;
  AppId=<GUID>;
  RedirectUri =app://<GUID>;
  TokenCacheStorePath =c:\MyTokenCache;
  LoginPrompt=Auto"/>  
```  

### <a name="certificate-based-authentication"></a>Autenticación basada en certificados

```xml
<add name="MyCDSServer" 
  connectionString="
  AuthType=Certificate;
  SkipDiscovery=true;
  url={InstanceUri};
  thumbprint={CertThumbPrintId};
  ClientId={AppId};
  RequireNewInstance=true"
  />
```

<a name="ConnectionStatus"></a>

## <a name="determine-your-connection-status"></a>Determinación del estado de la conexión

 Para determinar si la solicitud de conexión se realizó correctamente, compruebe el valor de la propiedad <xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient>.<xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient.IsReady> . Si es **true**, la conexión se realizó correctamente y está listo para trabajar. De lo contrario, compruebe los valores de las propiedades <xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient>.<xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient.LastCrmError> y <xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient>.<xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient.LastCrmException>. para la causa del error de conexión.  
  
### <a name="see-also"></a>Vea también

[Crear aplicaciones cliente de Windows mediante las herramientas XRM](build-windows-client-applications-xrm-tools.md)<br />
[Usar constructores CrmServiceClient para conectarse a Common Data Service](use-crmserviceclient-constructors-connect.md)<br />
[Use los útiles XRM para ejecutar acciones en Common Data Service](use-xrm-tooling-execute-actions.md)<br />
<xref:Microsoft.Xrm.Tooling.Connector.CrmServiceClient>
