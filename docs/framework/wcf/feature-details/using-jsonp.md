---
title: "Uso di JSONP | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f386718c-b4ba-4931-a610-40c27a46672a
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Uso di JSONP
JSON Padding \(JSONP\) è un meccanismo che abilita il supporto di script tra siti nei Web browser.  JSONP è progettato sulla base della capacità dei Web browser di caricare script da un sito diverso rispetto a quello da cui è stato recuperato il documento attualmente caricato.  Il meccanismo funziona riempiendo il payload JSON con un nome di funzione di callback definito dall'utente, come indicato nell'esempio seguente.  
  
```  
callback({"a" = \"b\" });  
```  
  
 Nell'esempio precedente viene eseguito il wrapping del payload JSON, `{"a" = \"b\"}`, in una chiamata di funzione, `callback`.  La funzione di callback deve essere già definita nella pagina Web corrente.  Il tipo di contenuto di una risposta JSONP è "application\/javascript".  
  
## Uso di JSONP  
 JSONP non è automaticamente abilitato.  Per abilitarlo, impostare l'attributo `javascriptCallbackEnabled` su `true` in uno degli endpoint HTTP standard \(<xref:System.ServiceModel.Description.WebHttpEndpoint> o <xref:System.ServiceModel.Description.WebScriptEndpoint>\), come indicato nell'esempio seguente.  
  
```xml  
<system.serviceModel>  
    <standardEndpoints>  
      <webHttpEndpoint>  
        <standardEndpoint name="" javascriptCallbackEnabled="true"/>  
      </webHttpEndpoint>  
    </standardEndpoints>     
  </system.serviceModel>  
```  
  
 È possibile specificare il nome della funzione di callback in una variabile della query denominata callback, come indicato nell'URL seguente.  
  
```  
http://baseaddress/Service/RestService?callback=functionName  
```  
  
 Se richiamato, il servizio invia una risposta analoga alla seguente.  
  
```jscript  
functionName({"root":"Something});  
```  
  
 È inoltre possibile specificare il nome della funzione di callback applicando <xref:System.ServiceModel.Web.JavascriptCallbackBehaviorAttribute> alla classe di servizio, come indicato nell'esempio seguente.  
  
```csharp  
[ServiceContract]  
[JavascriptCallbackBehavior(ParameterName = "$callback")]  
public class Service1  
{  
    [OperationContract]  
    [WebGet(ResponseFormat=WebMessageFormat.Json)]  
    public string GetData()  
    {              
    }  
}  
```  
  
 Per il servizio mostrato in precedenza, una richiesta è analoga alla seguente.  
  
```  
http://baseaddress/Service/RestService?$callback=anotherFunction  
```  
  
 Se richiamato, il servizio risponde come segue.  
  
```  
anotherFunction ({"root":"Something});  
```  
  
## Codici di stato HTTP  
 Le risposte JSONP con codici di stato HTTP diversi da 200 includono un secondo parametro con la rappresentazione numerica del codice di stato HTTP, come indicato nell'esempio seguente.  
  
```  
anotherFunction ({"root":"Something}, 201);  
```  
  
## Convalide  
 Se JSONP è abilitato, vengono eseguite le convalide indicate di seguito.  
  
-   L'infrastruttura WCF genera un'eccezione se `javascriptCallback` è abilitato, è presente un parametro della stringa di query di callback nella richiesta e il formato della risposta è impostato su JSON.  
  
-   Se la richiesta contiene il parametro della stringa di query di callback ma l'operazione non è un'operazione HTTP GET, il parametro di callback viene ignorato.  
  
-   Se il nome del callback è `null` o una stringa vuota, la risposta non è formattata come JSONP.  
  
## Vedere anche  
 [Panoramica sul modello di programmazione HTTP Web WCF](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model-overview.md)