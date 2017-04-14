---
title: "Formattazione di HTTP Web WCF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e2414896-5463-41cd-b0a6-026a713eac2c
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Formattazione di HTTP Web WCF
Il modello di programmazione HTTP Web WCF consente di determinare in modo dinamico il formato migliore in cui un'operazione di servizio debba restituire la risposta.  Vengono supportati due metodi per determinare un formato appropriato: automatico ed esplicito.  
  
## Formattazione automatica  
 Se abilitata, la formattazione automatica sceglie il formato migliore nel quale verrà restituita la risposta,  controllando gli elementi seguenti, in ordine:  
  
1.  i tipi di supporto nell'intestazione Accept del messaggio di richiesta;  
  
2.  il valore content\-type del messaggio di richiesta;  
  
3.  l'impostazione del formato predefinita nell'operazione;  
  
4.  l'impostazione del formato predefinita in WebHttpBehavior.  
  
 Se il messaggio di richiesta contiene un'intestazione Accept, l'infrastruttura di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] cerca un tipo supportato.  Se l'intestazione `Accept` specifica le priorità per i propri tipi di supporto, queste vengono rispettate.  Se non viene individuato alcun formato adatto nell'intestazione `Accept`, viene usato il valore content\-type del messaggio di richiesta.  Se non viene specificato alcun valore content\-type adatto, viene usata l'impostazione del formato predefinita per l'operazione.  Il formato predefinito viene impostato con il parametro `ResponseFormat` degli attributi <xref:System.ServiceModel.Web.WebGetAttribute> e <xref:System.ServiceModel.Web.WebInvokeAttribute>.  Se non viene specificato alcun formato predefinito nell'operazione, viene usato il valore della proprietà <xref:System.ServiceModel.Description.WebHttpBehavior.DefaultOutgoingResponseFormat%2A>.  La formattazione automatica si basa sulla proprietà <xref:System.ServiceModel.Description.WebHttpBehavior.AutomaticFormatSelectionEnabled%2A>.  Se tale proprietà è impostata su `true`, l'infrastruttura di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] determina il formato migliore da usare.  La selezione automatica del formato è disabilitata per impostazione predefinita per la compatibilità con le versioni precedenti.  La selezione automatica del formato automatica può essere abilitata a livello di codice o tramite la configurazione.  Nell'esempio seguente viene mostrato come abilitare la selezione automatica del formato nel codice.  
  
```  
// This code assumes the service name is MyService and the service contract is IMyContract     
Uri baseAddress = new Uri("http://localhost:8000");  
  
WebServiceHost host = new WebServiceHost(typeof(MyService), baseAddress)  
try  
{  
   ServiceEndpoint sep = host.AddServiceEndpoint(typeof(IMyContract), new WebHttpBinding(), "");  
   // Check it see if the WebHttpBehavior already exists  
   WebHttpBehavior whb = sep.Behaviors.Find<WebHttpBehavior>();  
  
   if (whb != null)  
   {  
      whb.AutomaticFormatSelectionEnabled = true;  
   }  
   else  
   {  
      WebHttpBehavior webBehavior = new WebHttpBehavior();  
      webBehavior.AutomaticFormatSelectionEnabled = true;  
      sep.Behaviors.Add(webBehavior);  
   }  
         // Open host to start listening for messages  
   host.Open();        
  
  // ...  
}  
  catch(CommunicationException ex)  
  {  
     Console.WriteLine(“An exception occurred: “ + ex.Message());  
  }  
  
```  
  
 La formattazione automatica può inoltre essere abilitata tramite la configurazione.  È possibile impostare la proprietà <xref:System.ServiceModel.Description.WebHttpBehavior.AutomaticFormatSelectionEnabled%2A> direttamente nell'elemento <xref:System.ServiceModel.Description.WebHttpBehavior> o mediante l'elemento <xref:System.ServiceModel.Description.WebHttpEndpoint>.  Nell'esempio seguente viene indicato come abilitare la selezione automatica del formato nell'elemento <xref:System.ServiceModel.Description.WebHttpBehavior>.  
  
```  
<system.serviceModel>  
  <behaviors>  
    <endpointBehaviors>  
      <behavior>  
        <webHttp automaticFormatSelectionEnabled="true" />  
      </behavior>  
    </endpointBehaviors>  
  </behaviors>  
  <standardEndpoints>  
    <webHttpEndpoint>  
      <!-- the "" standard endpoint is used by WebServiceHost for auto creating a web endpoint. -->  
      <standardEndpoint name="" helpEnabled="true" />  
    </webHttpEndpoint>  
  </standardEndpoints>  
</system.serviceModel>  
```  
  
 Nell'esempio seguente viene mostrato come abilitare la selezione automatica del formato mediante <xref:System.ServiceModel.Description.WebHttpEndpoint>.  
  
```  
<system.serviceModel>  
    <standardEndpoints>  
      <webHttpEndpoint>  
        <!-- the "" standard endpoint is used by WebServiceHost for auto creating a web endpoint. -->  
        <standardEndpoint name="" helpEnabled="true" automaticFormatSelectionEnabled="true"  />  
      </webHttpEndpoint>  
    </standardEndpoints>  
  </system.serviceModel>  
```  
  
## Formattazione esplicita  
 Come indicato nel nome, nella formattazione esplicita lo sviluppatore determina il formato migliore da usare all'interno del codice operativo.  Se il formato migliore è XML o JSON, lo sviluppatore imposta <xref:System.ServiceModel.Web.OutgoingWebResponseContext.Format%2A> su <xref:System.ServiceModel.Web.WebMessageFormat> o <xref:System.ServiceModel.Web.WebMessageFormat>.  Se la proprietà <xref:System.ServiceModel.Web.OutgoingWebResponseContext.Format%2A> non è impostata in modo esplicito, viene usato il formato predefinito dell'operazione.  
  
 Nell'esempio seguente viene verificato il parametro della stringa di query di formato per un formato da usare.  Se è stato specificato, viene impostato il formato dell'operazione mediante <xref:System.ServiceModel.Web.OutgoingWebResponseContext.Format%2A>.  
  
```  
public class Service : IService  
{  
    [WebGet]  
     public string EchoWithGet(string s)  
    {  
         // if a format query string parameter has been specified, set the response format to that. If no such  
         // query string parameter exists the Accept header will be used  
        string formatQueryStringValue = WebOperationContext.Current.IncomingRequest.UriTemplateMatch.QueryParameters["format"];  
        if (!string.IsNullOrEmpty(formatQueryStringValue))  
        {  
             if (formatQueryStringValue.Equals("xml", System.StringComparison.OrdinalIgnoreCase))  
             {  
                  WebOperationContext.Current.OutgoingResponse.Format = WebMessageFormat.Xml;  
             }  
             else if (formatQueryStringValue.Equals("json", System.StringComparison.OrdinalIgnoreCase))  
            {  
                WebOperationContext.Current.OutgoingResponse.Format = WebMessageFormat.Json;  
            }  
            else  
            {  
                 throw new WebFaultException<string>(string.Format("Unsupported format '{0}'", formatQueryStringValue), HttpStatusCode.BadRequest);  
            }  
        }  
        return "You said " + s;  
    }  
```  
  
 Se è necessario supportare formati diversi da XML o JSON, definire l'operazione per ottenere un tipo restituito di <xref:System.ServiceModel.Channels.Message>.  All'interno del codice operativo, determinare il formato appropriato da usare e creare quindi un oggetto <xref:System.ServiceModel.Channels.Message> usando uno dei metodi seguenti:  
  
-   `WebOperationContext.CreateAtom10Response`  
  
-   `WebOperationContext.CreateJsonResponse`  
  
-   `WebOperationContext.CreateStreamResponse`  
  
-   `WebOperationContext.CreateTextResponse`  
  
-   `WebOperationContext.CreateXmlResponse`  
  
 Ognuno di questi metodi usa il contenuto e crea un messaggio con il formato appropriato.  Il metodo `WebOperationContext.Current.IncomingRequest.GetAcceptHeaderElements` può essere usato per ottenere un elenco di formati preferiti dal client in ordine di preferenza decrescente.  Nell'esempio seguente viene indicato come usare `WebOperationContext.Current.IncomingRequest.GetAcceptHeaderElements` per determinare il formato da usare e viene quindi impiegato il metodo di risposta di creazione appropriato per creare il messaggio di risposta.  
  
```  
  
public class Service : IService  
{  
    public Message EchoListWithGet(string list)  
    {  
        List<string> returnList = new List<string>(list.Split(new char[] { ',' }, StringSplitOptions.RemoveEmptyEntries));  
        IList<ContentType> acceptHeaderElements = WebOperationContext.Current.IncomingRequest.GetAcceptHeaderElements();  
        for (int x = 0; x < acceptHeaderElements.Count; x++)  
        {  
            string normalizedMediaType = acceptHeaderElements[x].MediaType.ToLowerInvariant();  
            switch (normalizedMediaType)  
            {  
                case "image/jpeg": return CreateJpegResponse(returnList);  
                case "application/xhtml+xml": return CreateXhtmlResponse(returnList);  
                case "application/atom+xml": return CreateAtom10Response(returnList);  
                case "application/xml": return CreateXmlResponse(returnList);  
                case "application/json": return CreateJsonResponse(returnList);  
          }  
    }  
  
    // Default response format is XML  
    return CreateXmlResponse(returnList);  
    }  
}  
  
```  
  
## Vedere anche  
 <xref:System.UriTemplate>   
 <xref:System.UriTemplateMatch>   
 [Modello di programmazione HTTP Web WCF](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md)   
 [UriTemplate e UriTemplateTable](../../../../docs/framework/wcf/feature-details/uritemplate-and-uritemplatetable.md)   
 [Panoramica sul modello di programmazione HTTP Web WCF](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model-overview.md)   
 [Modello a oggetti per la programmazione HTTP Web di WCF](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-object-model.md)