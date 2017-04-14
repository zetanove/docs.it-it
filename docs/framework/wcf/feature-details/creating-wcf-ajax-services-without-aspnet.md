---
title: "Creazione di servizi WCF AJAX senza ASP.NET | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ba4a7d1b-e277-4978-9f62-37684e6dc934
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Creazione di servizi WCF AJAX senza ASP.NET
È possibile accedere ai servizi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] AJAX da qualsiasi pagina Web compatibile con JavaScript, senza la necessità di ASP.NET AJAX.  In questo argomento viene descritto come tale servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
 Per istruzioni sull'utilizzo di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] con ASP.NET AJAX, vedere [Creazione di servizi WCF per ASP.NET AJAX](../../../../docs/framework/wcf/feature-details/creating-wcf-services-for-aspnet-ajax.md).  
  
 La creazione di un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] AJAX implica tre passaggi:  
  
-   Creazione di un endpoint AJAX a cui sia possibile accedere dal browser.  
  
-   Creazione di un contratto di servizio compatibile con AJAX.  
  
-   Accesso ai servizi WCF AJAX.  
  
## Creazione di un endpoint AJAX  
 Il modo più semplice per attivare il supporto AJAX in un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] consiste nell'usare <xref:System.ServiceModel.Activation.WebServiceHostFactory> nel file con estensione SVC associato al servizio, come illustrato nell'esempio seguente.  
  
```  
<%ServiceHost   
    language=c#  
    Debug="true"  
    Service="Microsoft.Ajax.Samples.CityService"  
    Factory=System.ServiceModel.Activation.WebServiceHostFactory  
%>  
```  
  
 In alternativa, è anche possibile usare la configurazione per aggiungere un endpoint AJAX.  Usare <xref:System.ServiceModel.WebHttpBinding> sull'endpoint del servizio e configurare tale endpoint con <xref:System.ServiceModel.Description.WebHttpBehavior>, come illustrato nel frammento di codice seguente.  
  
```  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <endpointBehaviors>  
        <behavior name="AjaxBehavior">  
          <webHttp/>  
        </behavior>  
      </endpointBehaviors>  
    </behaviors>  
    <services>  
      <service name="Microsoft.Ajax.Samples.CityService">  
        <endpoint   
          address="ajaxEndpoint"  
          behaviorConfiguration="AjaxBehavior"  
          binding="webHttpBinding"  
          contract="Microsoft.Ajax.Samples.ICityService" />  
      </service>  
    </services>  
  </system.serviceModel>  
</configuration>  
```  
  
 Per un esempio funzionante, vedere [Servizio AJAX con esempi JSON e XML](../../../../docs/framework/wcf/samples/ajax-service-with-json-and-xml-sample.md).  
  
## Creazione di un contratto di servizio compatibile con AJAX  
 Per impostazione predefinita, i contratti di servizio esposti su un endpoint AJAX restituiscono dati in formato XML.  Inoltre, le operazioni del servizio sono accessibili, per impostazione predefinita, tramite richieste HTTP POST agli URL che includono l'indirizzo endpoint seguito dal nome dell'operazione, come illustrato nell'esempio seguente.  
  
```  
[OperationContract]  
string[] GetCities(string firstLetters);  
```  
  
 Questa operazione può essere eseguita mediante un HTTP POST a `http://serviceaddress/endpointaddress/GetCities` e restituirà un messaggio XML.  
  
 È possibile usare il Modello di programmazione Web completo per personalizzare questi aspetti di base.  Ad esempio, è possibile usare gli attributi <xref:System.ServiceModel.Web.WebGetAttribute> o <xref:System.ServiceModel.Web.WebInvokeAttribute> per controllare il verbo HTTP al quale risponde l'operazione o usare la proprietà `UriTemplate` di questi rispettivi attributi per specificare gli URI personalizzati.  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] l'argomento [Modello di programmazione HTTP Web WCF](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md).  
  
 Nei servizi AJAX viene spesso usato il formato dati JSON.  Per creare un'operazione che restituisce JSON invece di XML, impostare la proprietà <xref:System.ServiceModel.Web.WebGetAttribute.ResponseFormat%2A> \(o <xref:System.ServiceModel.Web.WebInvokeAttribute.ResponseFormat%2A>\) su <xref:System.ServiceModel.Web.WebMessageFormat>.  Nell'argomento [Serializzazione JSON autonoma](../../../../docs/framework/wcf/feature-details/stand-alone-json-serialization.md) viene illustrato come viene eseguito il mapping dei tipi .NET incorporati e dei tipi di contratto dati a JSON.  
  
 In genere, le richieste e le risposte JSON sono costituite da un solo elemento.  Nell'operazione `GetCities` precedente, la richiesta assomiglia all'istruzione seguente.  
  
```  
“na”  
```  
  
 La risposta a questa richiesta è simile all'istruzione seguente.  
  
```  
[“Nairobi”, “Naples”, “Nashville”]  
```  
  
 Se l'operazione accetta un parametro aggiuntivo, lo stile della richiesta deve essere "incapsulato", per eseguire il wrapping di entrambi parametri in un solo oggetto JSON.  Un esempio di questo stile di messaggio JSON è riportato nell'esempio seguente.  
  
```  
{“firstLetters”: “na”, “maxNumber”: 2}  
```  
  
 Il contratto seguente accetta questo messaggio.  
  
```  
[WebInvoke(BodyStyle=WebMessageBodyStyle.WrappedRequest, ResponseFormat=WebMessageFormat.Json)]  
[OperationContract]  
string[] GetCities(string firstLetters, int maxNumber);  
```  
  
## Accesso ai servizi AJAX.  
 Gli endpoint AJAX [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]accettano sempre richieste JSON e XML.  
  
 Le richieste HTTP POST con il tipo di contenuto "application\/json" vengono trattate come JSON, mentre quelle con tipo di contenuto che indica XML, ad esempio "text\/xml", vengono trattate come XML.  
  
 Le richieste HTTP GET contengono tutti i parametri di richiesta presenti nell'URL stesso.  
  
 Spetta all'utente decidere come creare la richiesta HTTP per l'endpoint.  Inoltre, l'utente ha il pieno controllo sulla costruzione del codice JSON che forma il corpo della richiesta.  Per un esempio di creazione di una richiesta da JavaScript, vedere l'[Servizio AJAX con esempi JSON e XML](../../../../docs/framework/wcf/samples/ajax-service-with-json-and-xml-sample.md).