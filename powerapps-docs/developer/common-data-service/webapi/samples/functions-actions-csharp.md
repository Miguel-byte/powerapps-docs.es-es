---
title: 'Ejemplo de funciones y acciones de la API web (C#) (Common Data Service)| Microsoft Docs'
description: 'Este ejemplo muestra cómo llamar a funciones y acciones enlazadas y sin enlazar, incluidas acciones personalizadas, mediante la API web de Common Data Service y C#'
ms.custom: ''
ms.date: 1/09/2019
ms.service: powerapps
ms.suite: ''
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
  - Dynamics 365 (online)
ms.assetid: b14a8bff-bf05-412c-89f6-ba7b503dcb51
caps.latest.revision: 13
author: brandonsimons
ms.author: jdaly
ms.reviewer: susikka
search.audienceType:
  - developer
search.app:
  - PowerApps
  - D365CE
---
# <a name="web-api-functions-and-actions-sample-c"></a>Ejemplo de funciones y acciones de la API web (C#)

Este ejemplo muestra cómo llamar a funciones y acciones enlazadas y sin enlazar, incluidas acciones personalizadas, mediante la API web de Common Data Service.  
  
> [!NOTE]
> Este ejemplo implementa las operaciones detalladas en el [Ejemplo de funciones y acciones de la API web](../web-api-functions-actions-sample.md) y utiliza las construcciones comunes del lado cliente C# que se describen en [Ejemplos de API web (C#)](../web-api-samples-csharp.md).  
 
<a name="bkmk_prerequisites"></a>

## <a name="prerequisites"></a>Requisitos previos

Los requisitos previos de todos los ejemplos en C# de la API web Common Data Service se detallan en la sección [Requisitos previos](../web-api-samples-csharp.md#bkmk_prerequisites) del tema primario [Ejemplos de la API web (C#)](../web-api-samples-csharp.md).  
  
<a name="bkmk_runSample"></a>

## <a name="how-to-run-this-sample"></a>Cómo ejecutar esta muestra

Vaya a [Ejemplo de funciones y acciones de la API web (C#)](https://github.com/Microsoft/PowerApps-Samples/tree/master/cds/webapi/C%23/FunctionAndActions), clone o descargue el repositorio de ejemplos y extraiga su contenido a una carpeta local. Esta carpeta debe contener los siguientes archivos:  
  
|Archivo|Objetivo/descripción|  
|----------|--------------------------|  
|SampleProgram.cs|Contiene el código de origen primario para este ejemplo.|  
|App.config|El archivo de configuración de la aplicación, que contiene información de conexión con el servidor de Common Data Service con marcadores. Este archivo se comparte con todos los ejemplos de API web en el repositorio. Si configura la información de la conexión para un ejemplo, puede ejecutar los otros ejemplos con la misma configuración.|  
|SampleHelper.cs|Contiene el código auxiliar para ayudar a realizar tareas comunes, como la configuración, la autenticación y la administración de errores de respuestas `HTTP`.<br/> Este archivo se comparte con todos los ejemplos de API web en el repositorio. Contiene métodos auxiliares para administrar excepciones y el token OAuth. Consulte el ejemplo simple de la API web para obtener más información sobre los métodos de este archivo.|
|SampleMethod.cs|Contiene todos los métodos que admiten el código de origen en el ejemplo. Las funciones que se usan en `SampleProgram.cs` se pueden definir en este archivo. |
|FunctionsAndActions.sln <br />FunctionsAndActions.csproj <br />Packages.config <br />AssemblyInfo.cs|La solución de Visual Studio 2017 estándar, proyecto, configuración del paquete NuGet, y archivos de información de ensamblado para este ejemplo.|  
|WebAPIFunctionsandActions_1_0_0_0_managed.zip|Una solución administrada personalizada que contenga dos acciones personalizadas llamada por este ejemplo.|  
  
A continuación, use el procedimiento siguiente para ejecutar este servicio.  
  
1. Busque y haga doble clic en el archivo de la solución, FunctionsAndActions.sln, para cargar la solución en Visual Studio. Cree la solución **FunctionsAndActions**.  Debe descargar e instalar automáticamente todos los paquetes NuGet necesarios que faltan o deben actualizarse.  
  
2. Edite el archivo de configuración, App.config, para especificar información de conexión para el servidor de Common Data Service.  
  
3. Ejecute el proyecto **FunctionsAndActions** desde Visual Studio.  Todas las soluciones de ejemplo se configuran para ejecutarse en modo de depuración de forma predeterminada.  
  
<a name="bkmk_codeListing"></a>

## <a name="code-listing"></a>Lista de código

 `SampleProgram.cs`  
  
```csharp  
  
using Newtonsoft.Json.Linq;
using System;
using System.Collections.Generic;
using System.Configuration;
using System.IO;
using System.Linq;
using System.Net;
using System.Net.Http;
using System.Text;
using System.Threading.Tasks;

namespace PowerApps.Samples

{
    public partial class SampleProgram
    {
        static void Main(string[] args)
        {
            try
            {
                //Get configuration data from App.config connectionStrings
                string connectionString = ConfigurationManager.ConnectionStrings["Connect"].ConnectionString;

                using (HttpClient client = SampleHelpers.GetHttpClient(
                    connectionString,
                    SampleHelpers.clientId,
                    SampleHelpers.redirectUrl,
                    "v9.0"))
                {
                    CreateRequiredRecords(client);
                    //DeleteRequiredRecords(client, prompt);
                    HttpRequestMessage request;
                    HttpResponseMessage response;
                    #region Call an unbound function with no parameters.
                    //Retrieve the current user's full name from the WhoAmI function:
                    // https://msdn.microsoft.com/library/mt607925.aspx, which returns a WhoAmIResponse 
                    // complex type: https://msdn.microsoft.com/library/mt607982.aspx.

                    string currentUser;
                    Console.WriteLine("Unbound function: WhoAmI");
                    response = client.GetAsync("WhoAmI", HttpCompletionOption.ResponseContentRead).Result;

                    if (!response.IsSuccessStatusCode)
                    {
                        throw new Exception(string.Format("Failed to retrieve current user", response.Content));
                    }
                    JObject whoAmIresp = JObject.Parse(response.Content.ReadAsStringAsync().Result);
                    //First obtain the user's ID.
                    myUserId = (Guid)whoAmIresp["UserId"];
                    //Then retrieve the full name for that unique ID.
                    string requestUri = "systemusers(" + myUserId + ")?$select=fullname";
                    response = client.GetAsync(requestUri, HttpCompletionOption.ResponseHeadersRead).Result;
                    if (response.IsSuccessStatusCode)
                    {
                        JObject user = JObject.Parse(response.Content.ReadAsStringAsync().Result);
                        currentUser = user["fullname"].ToString();
                    }
                    else if (response.StatusCode == HttpStatusCode.NotFound)
                    { currentUser = "[not registered]"; }
                    else
                    {
                        Console.WriteLine("Error calling WhoAmI!");
                        throw new Exception(string.Format("Failed to retrieve the fullname for that unique ID", response.Content));
                    }
                    Console.WriteLine("\tCurrent user has system name '{0}'.", currentUser);
                    #endregion Call an unbound function with no parameters.

                    #region Call an unbound function that requires parameters.
                    //Retrieve the time zone code for the specified time zone, using the GetTimeZoneCodeByLocalizedName 
                    //function: https://msdn.microsoft.com/library/mt607644.aspx, which returns a GetTimeZoneCodeBy-
                    //LocalizedNameResponse complex type: https://msdn.microsoft.com/library/mt607889.aspx.
                    string timeZoneCode;
                    int localeID = 1033;
                    string timeZoneName = "Pacific Standard Time";
                    JObject LocalizedNameResponse;

                    //Demonstrates best practice of passing parameters.
                    string[] uria = new string[] {
                "GetTimeZoneCodeByLocalizedName",
                "(LocalizedStandardName=@p1,LocaleId=@p2)",
                "?@p1='" + timeZoneName + "'&@p2=" + localeID };
                    //This would also work:
                    //string[] uria = ["GetTimeZoneCodeByLocalizedName", "(LocalizedStandardName='" + 
                    //    timeZoneName + "',LocaleId=" + localeId + ")"]; 

                    Console.WriteLine("Unbound function: GetTimeZoneCodeByLocalizedName");
                    response = client.GetAsync(string.Join("", uria), HttpCompletionOption.ResponseHeadersRead).Result;
                    if (response.StatusCode == HttpStatusCode.OK)
                    {
                        LocalizedNameResponse = JObject.Parse(response.Content.ReadAsStringAsync().Result);
                    }
                    else
                    {
                        Console.WriteLine("Error calling GetTimeZoneCodeByLocalizedName!");
                        throw new Exception(string.Format("Faile calling GetTimeZoneCodeByLocalizedName!", response.Content));

                    }
                    timeZoneCode = LocalizedNameResponse["TimeZoneCode"].ToString();
                    Console.WriteLine("\tThe time zone '{0}' has the code '{1}'.", timeZoneName, timeZoneCode);
                    #endregion Call an unbound function that requires parameters.

                    #region Call a bound function.    
                    //Retrieve the total time, in minutes, spent on all tasks associated with an incident.
                    //Uses the CalculateTotalTimeIncident function: https://msdn.microsoft.com/library/mt593054.aspx, 
                    //which returns a CalculateTotalTimeIncidentResponse complex type: 
                    //https://msdn.microsoft.com/library/mt607924.aspx.

                    string totalTime;
                    string boundUri = incident1Uri + @"/Microsoft.Dynamics.CRM.CalculateTotalTimeIncident()";
                    Console.WriteLine("Bound function: CalculateTotalTimeIncident");
                    response = client.GetAsync(boundUri, HttpCompletionOption.ResponseHeadersRead).Result;
                    if (response.IsSuccessStatusCode)
                    {
                        JObject cttir = JObject.Parse(response.Content.ReadAsStringAsync().Result);
                        totalTime = cttir["TotalTime"].ToString();
                    }
                    else
                    {
                        Console.WriteLine("Error calling CalculateTotalTimeIncident!");
                        throw new Exception(string.Format("Failed calling CalculateTotalTimeIncident!", response.Content));
                    }
                    Console.WriteLine("\tThe total duration of tasks associated with the incident " +
                        "is {0} minutes.", totalTime);
                    #endregion Call a bound function.  

                    #region Call an unbound action that requires parameters.
                    //Close an opportunity and marks it as won. Uses the WinOpportunity action: 
                    //https://msdn.microsoft.com/library/mt607971.aspx, 
                    //which takes a int32 status code and an opportunityclose entity type: 
                    //https://msdn.microsoft.com/library/mt593099.aspx.

                    JObject opportClose = new JObject();
                    opportClose["subject"] = "Won Opportunity";
                    opportClose["opportunityid@odata.bind"] = opportunity1Uri;
                    JObject winOpportParams = new JObject();
                    winOpportParams["Status"] = 3;
                    winOpportParams["OpportunityClose"] = opportClose;
                    Console.WriteLine("Unbound action: WinOpportunity");

                    request = new HttpRequestMessage(HttpMethod.Post, client.BaseAddress + "WinOpportunity");
                    request.Content = new StringContent(winOpportParams.ToString(), Encoding.UTF8, "application/json");
                    response = client.SendAsync(request, HttpCompletionOption.ResponseHeadersRead).Result;
                    if (response.IsSuccessStatusCode)
                    {
                    }
                    else
                    {
                        Console.WriteLine("Error calling WinOpportunity!");
                        throw new Exception(string.Format("Failed to close an opportunity as won", response.Content));
                    }
                    Console.WriteLine("\tOpportunity won.");
                    #endregion Call an unbound action that requires parameters.

                    #region Call a bound action that requires parameters.
                    //Add a new letter tracking activity to the current user's queue. Uses the AddToQueue 
                    //action: https://msdn.microsoft.com/library/mt607880.aspx, which is bound to the queue 
                    //entity type: https://msdn.microsoft.com/library/mt607886.aspx, and returns a 
                    //AddToQueueResponse complex type: https://msdn.microsoft.com/library/mt608105.aspx.
                    string queueItemId;
                    //Create a letter tracking instance.
                    string letterUri;
                    JObject letter = new JObject();
                    letter["description"] = "Example letter";
                    Console.WriteLine("Bound action: AddToQueue");
                    request = new HttpRequestMessage(HttpMethod.Post, client.BaseAddress + "letters");
                    request.Content = new StringContent(letter.ToString(), Encoding.UTF8, "application/json");

                    response = client.SendAsync(request, HttpCompletionOption.ResponseHeadersRead).Result;
                    if (response.StatusCode == HttpStatusCode.NoContent)
                    {
                        letterUri = response.Headers.GetValues("OData-EntityId").FirstOrDefault();
                        entityUris.Add(letterUri);
                    }
                    else
                    {
                        Console.WriteLine("Error creating tracking letter!");
                        throw new Exception(string.Format("Failed to create a Letter", response.Content));
                    }

                    //Retrieve the ID associated with this new letter tracking activity.
                    string letterActivityId;
                    response = client.GetAsync(letterUri + "?$select=activityid",
                        HttpCompletionOption.ResponseHeadersRead).Result;
                    if (response.IsSuccessStatusCode)
                    {
                        JObject letterRetreived = JObject.Parse(response.Content.ReadAsStringAsync().Result);
                        letterActivityId = letterRetreived["activityid"].ToString();
                    }
                    else
                    {
                        Console.WriteLine("Error retrieving tracking letter activity ID!");
                        throw new Exception(string.Format("Failed to retrieve trscking letter activity ID", response.Content));
                    }

                    //Retrieve URL to current user's queue.
                    string myQueueUri;
                    response = client.GetAsync("systemusers(" + myUserId + ")/queueid/$ref",
                        HttpCompletionOption.ResponseHeadersRead).Result;
                    if (response.IsSuccessStatusCode)
                    {
                        JObject queueRef = JObject.Parse(response.Content.ReadAsStringAsync().Result);
                        myQueueUri = queueRef["@odata.id"].ToString();
                    }
                    else
                    {
                        Console.WriteLine("Error retrieving current user queue URL!");
                        throw new Exception(string.Format("Failed to retrieve URL to current user's queue", response.Content));
                    }

                    //Add letter activity to current user's queue, then return its queue ID.
                    JObject addToQueueParams = new JObject();
                    addToQueueParams["Target"] = JObject.Parse(
                      @"{activityid: '" + letterActivityId + @"', '@odata.type': 'Microsoft.Dynamics.CRM.letter' }");
                    request = new HttpRequestMessage(HttpMethod.Post, myQueueUri + "/Microsoft.Dynamics.CRM.AddToQueue");
                    request.Content = new StringContent(addToQueueParams.ToString());
                    response = client.SendAsync(request, HttpCompletionOption.ResponseHeadersRead).Result;
                    if (response.StatusCode == HttpStatusCode.OK)
                    {
                        JObject queueResponse = JObject.Parse(response.Content.ReadAsStringAsync().Result);
                        queueItemId = queueResponse["QueueItemId"].ToString();
                    }
                    else
                    {
                        Console.WriteLine("Error adding letter activity to queue!");
                        throw new Exception(string.Format("Failed to Add letter activity to current user's queue", response.Content));
                    }
                    Console.WriteLine("\tQueueItemId returned from AddToQueue action: {0}", queueItemId);
                    #endregion Call a bound action that requires parameters.

                    //Attempt to load the associated managed solution so that we can call its custom actions. 
                    //Check first if the solution is already installed by retrieving its ID.
                    customSolutionID = customSolutionName;
                    bool install = true;
                    //Request to install and solution is not already present
                    if (install == true && customSolutionID == null)
                    {
                        //Locate the custom solution zip file, which should have been copied over to the build 
                        //output directory.
                        string solutionPath = Directory.GetCurrentDirectory() + "\\" + customSolutionFilename;
                        if (!File.Exists(solutionPath))
                        { return; }
                        //Read the solution package into memory
                        byte[] packageBytes = File.ReadAllBytes(solutionPath);
                        //Import the solution package.
                        JObject importParams = new JObject();
                        importParams["CustomizationFile"] = packageBytes;
                        importParams["OverwriteUnmanagedCustomizations"] = false;
                        importParams["PublishWorkflows"] = false;
                        importParams["ImportJobId"] = Guid.NewGuid();

                        request = new HttpRequestMessage(HttpMethod.Post, "ImportSolution");
                        request.Content = new StringContent(importParams.ToString(), Encoding.UTF8, "application/json");
                        response = client.SendAsync(request, HttpCompletionOption.ResponseContentRead).Result;
                        if (response.IsSuccessStatusCode)
                        {
                            customSolutionID = customSolutionName;
                            string solutionUri = client.BaseAddress.ToString() + "solutions(" + customSolutionID + ")";
                            entityUris.Add(solutionUri);  //Add to lifetime-managed records.
                            return;
                        }
                        else
                        { throw new Exception(string.Format("Failed to import solution package", response.Content)); }
                    }
                    //Request to uninstall and solution is present. 
                    else if (install == false && customSolutionID != null)
                    {
                        string solutionUri = client.BaseAddress.ToString() + "solutions(" + customSolutionID + ")";
                        response = client.DeleteAsync(solutionUri).Result;
                        customSolutionID = null;
                    }
                    if (customSolutionID == null)
                    {
                        Console.WriteLine("Failed to install custom solution, so custom operations cannot be called.");
                        return;
                    }

                    string solutionID = null;

                    if (String.IsNullOrEmpty(solutionName))
                    { //return null;
                    }
                    string queryOptions = "solutions?$select=solutionid&$filter=uniquename eq '" + solutionName + "'";
                    response = client.GetAsync(queryOptions, HttpCompletionOption.ResponseHeadersRead).Result;
                    if (response.StatusCode == HttpStatusCode.OK)
                    {
                        JObject solutionArray = JObject.Parse(response.Content.ReadAsStringAsync().Result);
                        //There can only be zero or one returned record when filtering on a unique property.
                        if (!solutionArray["value"].Any())
                        { solutionID = null; }
                        else
                        { solutionID = solutionArray["value"].First()["solutionid"].ToString(); }
                    }
                    else
                    { throw new Exception(string.Format("Failed to get  solutionID", response.Content)); }
                    ///return solutionID;

                    #region Call a bound custom action that requires parameters.
                    //Add a note to a specified contact. Uses the custom action sample_AddNoteToContact, which
                    //is bound to the contact to annotate, and takes a single param, the note to add. It also  
                    //returns the URI to the new annotation. 
                    string annote1Url;
                    JObject note1 = JObject.Parse(
                        @"{NoteTitle: 'Note Title', NoteText: 'The text content of the note.'}");
                    string actionUri = contact1Uri + "/Microsoft.Dynamics.CRM.sample_AddNoteToContact";
                    Console.WriteLine("Custom action: sample_AddNoteToContact");
                    request = new HttpRequestMessage(HttpMethod.Post, actionUri);
                    request.Content = new StringContent(note1.ToString(), Encoding.UTF8, "application/json");
                    response = client.SendAsync(request, HttpCompletionOption.ResponseContentRead).Result;
                    if (response.StatusCode == HttpStatusCode.OK)
                    {
                        JObject contact = JObject.Parse(response.Content.ReadAsStringAsync().Result);
                        annote1Url = client.BaseAddress + "/annotations(" + contact["annotationid"] + ")";
                    }
                    else
                    {
                        Console.WriteLine("Error calling custom action sample_AddNoteToContact!");
                        throw new Exception(string.Format("Failed calling custom action sample_AddNoteToContact", response.Content));
                    }
                    Console.WriteLine("\tA note with the title '{0}' was created and " +
                        "associated with the contact {2}.",
                        note1["NoteTitle"], note1["NoteText"],
                        contact1["firstname"] + " '" + contact1["lastname"] + "'");
                    #endregion Call a bound custom action that requires parameters.

                    #region Call an unbound custom action that requires parameters.
                    //Create a customer of the specified type, using the custom action sample_CreateCustomer,
                    //which takes two prams: the type of customer ('account' or 'contact') and the name of 
                    //the new customer.
                    string customerName1 = "New account customer (sample)";
                    JObject customerParam = JObject.Parse(
                        @"{CustomerType: 'account', AccountName: '" + customerName1 + "'}");
                    Console.WriteLine("Custom action: sample_CreateCustomer");
                    request = new HttpRequestMessage(HttpMethod.Post, "sample_CreateCustomer");
                    request.Content = new StringContent(customerParam.ToString(), Encoding.UTF8, "application/json");
                    response = client.SendAsync(request, HttpCompletionOption.ResponseContentRead).Result;
                    if (!response.IsSuccessStatusCode)
                    {
                        Console.WriteLine("Error calling custom action sample_CreateCustomer!");
                        throw new Exception(string.Format("Failed calling custom action sample_CreateCustomer", response.Content));
                    }
                    Console.WriteLine("\tThe account '" + customerName1 + "' was created.");

                    //Try to call the same custom action with invalid parameters, here the same name is
                    //not valid for a contact. (ContactFirstname and ContactLastName parameters are  
                    //required when CustomerType is contact.)
                    customerParam = JObject.Parse(
                        @"{CustomerType: 'contact', AccountName: '" + customerName1 + "'}");
                    request = new HttpRequestMessage(HttpMethod.Post, "sample_CreateCustomer");
                    response = client.SendAsync(request, HttpCompletionOption.ResponseContentRead).Result;
                    if (response.IsSuccessStatusCode)
                    { Console.WriteLine("\tCall to CreateCustomer not expected to succeed."); }
                    else
                    {
                        Exception ex = new Exception(string.Format("Failed calling custom action", response.Content));
                        Console.WriteLine("\tExpected Error: " + ex.Message);
                    }
                    #endregion Call an unbound custom action that requires parameters.

                    DeleteRequiredRecords(client, prompt);
                }
            }
            catch (Exception ex)
            {
                SampleHelpers.DisplayException(ex);
                throw;
            }
            finally
            {
                Console.WriteLine("Press <Enter> to exit the program.");
                Console.ReadLine();
            }
        }
    }
}

```  
  
### <a name="see-also"></a>Vea también

[Usar la API web de Common Data Service](../overview.md)<br />
[Usar funciones de la API web](../use-web-api-functions.md)<br />
[Usar acciones de la API web](../use-web-api-actions.md)<br />
[Ejemplos de la API web](../web-api-samples.md)<br />
[Ejemplo de funciones y acciones de la API web](../web-api-functions-actions-sample.md)
[Ejemplo de operaciones básicas de la API web (C#)](basic-operations-csharp.md)<br />
[Ejemplo de datos de consulta API (C#)](query-data-csharp.md)<br />
[Ejemplo de operaciones condicionales de la API web (C#)](conditional-operations-csharp.md)
