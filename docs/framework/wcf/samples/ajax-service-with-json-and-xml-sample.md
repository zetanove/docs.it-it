---
title: "Servizio AJAX con esempi JSON e XML | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8ea5860d-0c42-4ae9-941a-e07efdd8e29c
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# Servizio AJAX con esempi JSON e XML
Questo esempio illustra come utilizzare [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] per creare un JavaScript asincrono e un servizio XML \(AJAX\) che restituiscono JSON \(JavaScript Object Notation\) o dati XML.È possibile accedere a un servizio AJAX utilizzando codice JavaScript a partire da un client del browser Web.Questo esempio si basa sull'esempio [Servizio AJAX di base](../../../../docs/framework/wcf/samples/basic-ajax-service.md).  
  
 A differenza degli altri esempi AJAX, questo esempio non utilizza ASP.NET AJAX e il controllo <xref:System.Web.UI.ScriptManager>.Con alcune configurazioni aggiuntive, è possibile accedere ai servizi AJAX [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] da qualsiasi pagina HTML tramite JavaScript e questo scenario viene illustrato qui di seguito.Per un esempio di utilizzo di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] con ASP.NET AJAX, vedere [AJAX Samples](http://msdn.microsoft.com/it-it/f3fa45b3-44d5-4926-8cc4-a13c30a3bf3e).  
  
 Questo esempio mostra come cambiare il tipo di risposta di un'operazione da JSON a XML.Questa funzionalità è disponibile indipendentemente dal fatto che il servizio sia configurato per l'accesso da ASP.NET AJAX o da una pagina client HTML\/JavaScript semplice.  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine dell'argomento.  
  
 Per abilitare l'utilizzo di client AJAX non ASP.NET, utilizzare l'oggetto <xref:System.ServiceModel.Activation.WebServiceHostFactory> \(non l'oggetto <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory>\) nel file con estensione svc.L'oggetto <xref:System.ServiceModel.Activation.WebServiceHostFactory> aggiunge un endpoint <xref:System.ServiceModel.Description.WebHttpEndpoint> standard al servizio.L'endpoint viene configurato su un indirizzo vuoto relativo al file con estensione svc. Ciò significa che l'indirizzo del servizio è http:\/\/localhost\/ServiceModelSamples\/service.svc, senza suffissi aggiuntivi tranne il nome dell'operazione.  
  
```html  
<%@ServiceHost language="c#" Debug="true" Service="Microsoft.Samples.XmlAjaxService.CalculatorService" Factory="System.ServiceModel.Activation.WebServiceHostFactory" %>  
  
```  
  
 La sezione seguente in Web.config può essere utilizzata per effettuare modifiche di configurazione aggiuntive all'endpoint.Può essere rimossa se non sono necessarie modifiche aggiuntive.  
  
```xml  
<system.serviceModel>  
  <standardEndpoints>  
    <webHttpEndpoint>  
      <!-- Use this element to configure the endpoint -->  
      <standardEndpoint name="" />  
    </webHttpEndpoint>  
  </standardEndpoints>  
</system.serviceModel>  
  
```  
  
 Il formato di dati predefinito per <xref:System.ServiceModel.Description.WebHttpEndpoint> è XML, mentre il formato di dati predefinito [for T:System.ServiceModel.Description.WebScriptEndpoint](assetId:///for T:System.ServiceModel.Description.WebScriptEndpoint?qualifyHint=False&autoUpgrade=True) è JSON.Per ulteriori informazioni, vedere [Creazione di servizi WCF AJAX senza ASP.NET](../../../../docs/framework/wcf/feature-details/creating-wcf-ajax-services-without-aspnet.md).  
  
 Il servizio nell'esempio seguente è un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] standard con due operazioni.Entrambe le operazioni richiedono lo stile del corpo <xref:System.ServiceModel.Web.WebMessageBodyStyle> sugli attributi <xref:System.ServiceModel.Web.WebGetAttribute> o <xref:System.ServiceModel.Web.WebInvokeAttribute> che è specifico del comportamento `webHttp` e non è rilevante per il cambiamento di formato JSON\/XML.  
  
```  
[OperationContract]  
[WebInvoke(ResponseFormat = WebMessageFormat.Xml, BodyStyle = WebMessageBodyStyle.Wrapped)]  
MathResult DoMathXml(double n1, double n2);  
```  
  
 Il formato della risposta per l'operazione è specificato come XML, ovvero l'impostazione predefinita per il comportamento [\<webHttp\>](../../../../docs/framework/configure-apps/file-schema/wcf/webhttp.md).Tuttavia, si consiglia di specificare esplicitamente il formato della risposta.  
  
 L'altra operazione utilizza l'attributo `WebInvokeAttribute` e specifica in modo esplicito JSON anziché XML per la risposta.  
  
```  
[OperationContract]  
[WebInvoke(ResponseFormat = WebMessageFormat.Json, BodyStyle = WebMessageBodyStyle.Wrapped)]  
MathResult DoMathJson(double n1, double n2);  
```  
  
 Notare che in entrambi i casi che le operazioni restituiscono un tipo complesso, `MathResult`, che è un tipo di contratto dati [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] standard.  
  
 La pagina Web client XmlAjaxClientPage.htm contiene codice JavaScript che richiama una delle due precedenti operazioni quando l'utente fa clic sui pulsanti **Esegui calcolo \(restituire JSON\)** o **Esegui calcolo \(restituire XML\)** nella pagina.Il codice per richiamare il servizio costruisce un corpo JSON e lo invia utilizzando HTTP POST.La richiesta viene creata manualmente in JavaScript, a differenza dall'esempio [Servizio AJAX di base](../../../../docs/framework/wcf/samples/basic-ajax-service.md) e degli altri esempi che utilizzano ASP.NET AJAX.  
  
```  
// Create HTTP request  
var xmlHttp;  
// Request instantiation code omitted…  
// Result handler code omitted…  
  
// Build the operation URL  
var url = "service.svc/ajaxEndpoint/";  
url = url + operation;  
  
// Build the body of the JSON message  
var body = '{"n1":';  
body = body + document.getElementById("num1").value + ',"n2":';  
body = body + document.getElementById("num2").value + '}';  
  
// Send the HTTP request  
xmlHttp.open("POST", url, true);  
xmlHttp.setRequestHeader("Content-type", "application/json");  
xmlHttp.send(body);  
```  
  
 Quando il servizio risponde, la risposta viene visualizzata senza nessuna ulteriore elaborazione in una casella di testo nella pagina.Viene implementata a mero scopo esemplificativo per consentire di osservare direttamente i formati dati XML e JSON utilizzati.  
  
```  
// Create result handler   
xmlHttp.onreadystatechange=function(){  
     if(xmlHttp.readyState == 4){  
          document.getElementById("result").value = xmlHttp.responseText;  
     }  
}  
```  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\AJAX\XmlAjaxService`  
  
#### Per impostare, compilare ed eseguire l'esempio  
  
1.  Verificare di avere eseguito [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Compilare la soluzione XmlAjaxService.sln come descritto in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Spostarsi alla pagina http:\/\/localhost\/ServiceModelSamples\/XmlAjaxClientPage.htm \(non aprire XmlAjaxClientPage.htm nel browser dalla directory del progetto\).  
  
## Vedere anche  
 [Servizio AJAX con il protocollo HTTP POST](../../../../docs/framework/wcf/samples/ajax-service-using-http-post.md)