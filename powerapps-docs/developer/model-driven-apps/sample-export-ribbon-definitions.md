---
title: 'Ejemplo: Exportar definiciones de cinta de opciones (aplicaciones basadas en modelos) | Microsoft Docs'
description: El ejemplo muestra cómo exportar definiciones de cinta de opciones. Utiliza los mensajes RetrieveApplicationRibbonRequest y RetrieveEntityRibbonRequest.
ms.custom: ''
ms.date: 10/31/2018
ms.reviewer: ''
ms.service: powerapps
ms.topic: article
author: KumarVivek
ms.author: kvivek
manager: shilpas
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="sample-export-ribbon-definitions"></a>Ejemplo: exportar definiciones de cinta

<!-- https://docs.microsoft.com/en-us/dynamics365/customer-engagement/developer/customize-dev/sample-export-ribbon-definitions -->


Este código de ejemplo es para aplicaciones basadas en modelos. [Descargue el ejemplo de exportar definiciones de cinta de opciones](https://code.msdn.microsoft.com/Export-ribbon-definitions-df97a4cb).

## <a name="prerequisites"></a>Requisitos previos
[!INCLUDE[sdk-prerequisite](../../includes/sdk-prerequisite.md)]
  
<!--## Requirements  
[!INCLUDE[sdk_SeeConnectionHelper](../../includes/sdk-seeconnectionhelper.md)]-->

  
## <a name="demonstrates"></a>Demostraciones  
 Este ejemplo muestra cómo exportar definiciones de la cinta de opciones. Utiliza los mensajes <xref:Microsoft.Crm.Sdk.Messages.RetrieveApplicationRibbonRequest> y <xref:Microsoft.Crm.Sdk.Messages.RetrieveEntityRibbonRequest>.  
  
## <a name="example"></a>Ejemplo  
```C#
using System;
using System.ServiceModel;
using System.ServiceModel.Description;

// These namespaces are found in the Microsoft.Xrm.Sdk.dll assembly
// located in the SDK\bin folder of the SDK download.
using Microsoft.Xrm.Sdk;
using Microsoft.Xrm.Sdk.Query;
using Microsoft.Xrm.Sdk.Client;
using Microsoft.Xrm.Sdk.Messages;
using Microsoft.Xrm.Sdk.Metadata;



using Microsoft.Crm.Sdk.Messages;

//These references are required for this sample
using System.IO;
using System.IO.Packaging;

namespace Microsoft.Crm.Sdk.Samples
{
 /// <summary>
 /// Demonstrates how to export the RibbonXml definitions.</summary>
 /// <remarks>
 /// The generated XML files will be created in the ExportedRibbonXml folder of this project.</remarks>
 public class ExportRibbonXml
 {
  #region Class Level Members


  private OrganizationServiceProxy _serviceProxy;
  //This array contains all of the system entities that use the ribbon.
  public System.String[] entitiesWithRibbons = {"account",
"activitymimeattachment",
"activitypointer",
"appointment",
"bulkoperation",
"calendar",
"campaign",
"campaignactivity",
"campaignresponse",
"competitor",
"connection",
"contact",
"contract",
"contractdetail",
"convertrule",
"convertruleitem",
"customeraddress",
"discount",
"discounttype",
"email",
"emailserverprofile",
"entitlement",
"entitlementchannel",
"entitlementtemplate",
"entitlementtemplatechannel",
"fax",
"goal",
"goalrollupquery",
"importfile",
"incident",
"invoice",
"invoicedetail",
"kbarticle",
"kbarticlecomment",
"lead",
"letter",
"list",
"listmember",
"mailbox",
"metric",
"opportunity",
"opportunityproduct",
"partnerapplication",
"phonecall",
"postfollow",
"pricelevel",
"product",
"productpricelevel",
"queue",
"queueitem",
"quote",
"quotedetail",
"recurringappointmentmaster",
"report",
"rollupfield",
"routingrule",
"routingruleitem",
"salesliterature",
"salesliteratureitem",
"salesorder",
"salesorderdetail",
"service",
"serviceappointment",
"sharepointdocument",
"sharepointdocumentlocation",
"sharepointsite",
"site",
"sla",
"slaitem",
"socialactivity",
"socialprofile",
"systemuser",
"task",
"team",
"teamtemplate",
"territory",
"uom",
"uomschedule",
"userquery"};
  //Folder name for exported ribbon xml files.
  public String exportFolder = "ExportedRibbonXml";

  #endregion Class Level Members

  #region How To Sample Code
  /// <summary>
  /// This method first connects to the Organization service. Afterwards,
  /// basic create, retrieve, update, and delete entity operations are performed.
  /// </summary>
  /// <param name="serverConfig">Contains server connection information.</param>
  /// <param name="promptforDelete">When True, the user will be prompted to delete all
  /// created entities.</param>
  public void Run(ServerConnection.Configuration serverConfig, bool promptforDelete)
  {
   try
   {
    // Connect to the Organization service. 
    // The using statement assures that the service proxy will be properly disposed.
    using (_serviceProxy = new OrganizationServiceProxy(serverConfig.OrganizationUri, serverConfig.HomeRealmUri,serverConfig.Credentials, serverConfig.DeviceCredentials))
    {
     // This statement is required to enable early-bound type support.                  
     _serviceProxy.EnableProxyTypes();
     
     //Create export folder for ribbon xml files if not already exist.
     if (!Directory.Exists(exportFolder))
         Directory.CreateDirectory(exportFolder);

     //Retrieve the Appliation Ribbon
     RetrieveApplicationRibbonRequest appribReq = new RetrieveApplicationRibbonRequest();
     RetrieveApplicationRibbonResponse appribResp = (RetrieveApplicationRibbonResponse)_serviceProxy.Execute(appribReq);

     System.String applicationRibbonPath = Path.GetFullPath(exportFolder + "\\applicationRibbon.xml");
     File.WriteAllBytes(applicationRibbonPath, unzipRibbon(appribResp.CompressedApplicationRibbonXml));
     //Write the path where the file has been saved.
     Console.WriteLine(applicationRibbonPath);
     //Retrieve system Entity Ribbons
     RetrieveEntityRibbonRequest entRibReq = new RetrieveEntityRibbonRequest() { RibbonLocationFilter = RibbonLocationFilters.All };

     foreach (System.String entityName in entitiesWithRibbons)
     {
      entRibReq.EntityName = entityName;
      RetrieveEntityRibbonResponse entRibResp = (RetrieveEntityRibbonResponse)_serviceProxy.Execute(entRibReq);

      System.String entityRibbonPath = Path.GetFullPath(exportFolder + "\\" + entityName + "Ribbon.xml");
      File.WriteAllBytes(entityRibbonPath, unzipRibbon(entRibResp.CompressedEntityXml));
      //Write the path where the file has been saved.
      Console.WriteLine(entityRibbonPath);
     }

     //Check for custom entities
     RetrieveAllEntitiesRequest raer = new RetrieveAllEntitiesRequest() { EntityFilters = EntityFilters.Entity };

     RetrieveAllEntitiesResponse resp = (RetrieveAllEntitiesResponse)_serviceProxy.Execute(raer);

     foreach (EntityMetadata em in resp.EntityMetadata)
     {
      if (em.IsCustomEntity == true && em.IsIntersect == false)
      {
       entRibReq.EntityName = em.LogicalName;
       RetrieveEntityRibbonResponse entRibResp = (RetrieveEntityRibbonResponse)_serviceProxy.Execute(entRibReq);

       System.String entityRibbonPath = Path.GetFullPath(exportFolder + "\\" + em.LogicalName + "Ribbon.xml");
       File.WriteAllBytes(entityRibbonPath, unzipRibbon(entRibResp.CompressedEntityXml));
       //Write the path where the file has been saved.
       Console.WriteLine(entityRibbonPath);
      }
     }
    }
   }

   // Catch any service fault exceptions that Microsoft Dynamics CRM throws.
   catch (FaultException<Microsoft.Xrm.Sdk.OrganizationServiceFault>)
   {
    // You can handle an exception here or pass it back to the calling method.
    throw;
   }
  }

  /// <summary>
  /// A helper method that decompresses the the Ribbon data returned
  /// </summary>
  /// <param name="data">The compressed ribbon data</param>
  /// <returns></returns>
  public byte[] unzipRibbon(byte[] data)
  {
   System.IO.Packaging.ZipPackage package = null;
   MemoryStream memStream = null;

   memStream = new MemoryStream();
   memStream.Write(data, 0, data.Length);
   package = (ZipPackage)ZipPackage.Open(memStream, FileMode.Open);

   ZipPackagePart part = (ZipPackagePart)package.GetPart(new Uri("/RibbonXml.xml", UriKind.Relative));
   using (Stream strm = part.GetStream())
   {
    long len = strm.Length;
    byte[] buff = new byte[len];
    strm.Read(buff, 0, (int)len);
    return buff;
   }
  }

  #endregion How To Sample Code

  #region Main method

  /// <summary>
  /// Standard Main() method used by most SDK samples.
  /// </summary>
  /// <param name="args"></param>
  static public void Main(string[] args)
  {
   try
   {
    // Obtain the target organization's Web address and client logon 
    // credentials from the user.
    ServerConnection serverConnect = new ServerConnection();
    ServerConnection.Configuration config = serverConnect.GetServerConfiguration();

    ExportRibbonXml app = new ExportRibbonXml();
    app.Run(config, true);
   }
   catch (FaultException<Microsoft.Xrm.Sdk.OrganizationServiceFault> ex)
   {
    Console.WriteLine("The application terminated with an error.");
    Console.WriteLine("Timestamp: {0}", ex.Detail.Timestamp);
    Console.WriteLine("Code: {0}", ex.Detail.ErrorCode);
    Console.WriteLine("Message: {0}", ex.Detail.Message);
    Console.WriteLine("Plugin Trace: {0}", ex.Detail.TraceText);
    Console.WriteLine("Inner Fault: {0}",
        null == ex.Detail.InnerFault ? "No Inner Fault" : "Has Inner Fault");
   }
   catch (System.TimeoutException ex)
   {
    Console.WriteLine("The application terminated with an error.");
    Console.WriteLine("Message: {0}", ex.Message);
    Console.WriteLine("Stack Trace: {0}", ex.StackTrace);
    Console.WriteLine("Inner Fault: {0}",
        null == ex.InnerException.Message ? "No Inner Fault" : ex.InnerException.Message);
   }
   catch (System.Exception ex)
   {
    Console.WriteLine("The application terminated with an error.");
    Console.WriteLine(ex.Message);

    // Display the details of the inner exception.
    if (ex.InnerException != null)
    {
     Console.WriteLine(ex.InnerException.Message);

     FaultException<Microsoft.Xrm.Sdk.OrganizationServiceFault> fe = ex.InnerException
         as FaultException<Microsoft.Xrm.Sdk.OrganizationServiceFault>;
     if (fe != null)
     {
      Console.WriteLine("Timestamp: {0}", fe.Detail.Timestamp);
      Console.WriteLine("Code: {0}", fe.Detail.ErrorCode);
      Console.WriteLine("Message: {0}", fe.Detail.Message);
      Console.WriteLine("Plugin Trace: {0}", fe.Detail.TraceText);
      Console.WriteLine("Inner Fault: {0}",
          null == fe.Detail.InnerFault ? "No Inner Fault" : "Has Inner Fault");
     }
    }
   }
   // Additional exceptions to catch: SecurityTokenValidationException, ExpiredSecurityTokenException,
   // SecurityAccessDeniedException, MessageSecurityException, and SecurityNegotiationException.

   finally
   {
    Console.WriteLine("Press <Enter> to exit.");
    Console.ReadLine();
   }
  }
  #endregion Main method
 }
}
```
  
### <a name="see-also"></a>Vea también  
 [Personalización de comandos y la cinta de opciones](customize-commands-ribbon.md)   
 [Pasar parámetros a una dirección URL con la cinta de opciones](pass-parameters-url-by-using-ribbon.md)   
 [Esquema central de cinta de opciones](ribbon-core-schema.md) [Esquema de tipos de cinta de opciones](ribbon-types-schema.md) [Esquema WSS de cinta de opciones](ribbon-wss-schema.md) <xref:Microsoft.Crm.Sdk.Messages.RetrieveApplicationRibbonRequest>   
 <xref:Microsoft.Crm.Sdk.Messages.RetrieveEntityRibbonRequest>
