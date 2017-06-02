---
title: "Servizio AJAX di base | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d66d0c91-0109-45a0-a901-f3e4667c2465
caps.latest.revision: 30
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 30
---
# Servizio AJAX di base
In questo esempio viene illustrato come usare [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] per creare un servizio AJAX \(ASP.NET Asynchronous JavaScript and XML\), ovvero un servizio al quale è possibile accedere usando codice JavaScript da un client browser Web.  Il servizio usa l'attributo <xref:System.ServiceModel.Web.WebGetAttribute> per garantire che il servizio risponda alle richieste HTTP GET ed è configurato per usare il formato dati JSON \(JavaScript Object Notation\) per le risposte.  
  
 Il supporto AJAX in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] è ottimizzato per l'uso con ASP.NET AJAX tramite il controllo `ScriptManager`.  Per un esempio d'uso di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] con ASP.NET AJAX, vedere [AJAX Samples](http://msdn.microsoft.com/it-it/f3fa45b3-44d5-4926-8cc4-a13c30a3bf3e).  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine di questo argomento.  
  
 Nel seguente codice, l'attributo <xref:System.ServiceModel.Web.WebGetAttribute> viene applicato all'operazione `Add` per assicurare che il servizio risponda alle richieste HTTP GET.  Il codice usa GET per semplicità \(è possibile costruire una richiesta HTTP GET da qualsiasi browser Web\).  È inoltre possibile usare GET per abilitare la memorizzazione nella cache.  HTTP POST è l'impostazione predefinita nel caso in cui l'attributo `WebGetAttribute` non sia presente.  
  
```  
[ServiceContract(Namespace = "SimpleAjaxService")]  
public interface ICalculator  
{  
  
    [WebGet]  
    double Add(double n1, double n2);  
    //Other operations omitted…  
}  
  
```  
  
 Nel file di esempio con estensione svc viene usato <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory>, che aggiunge un endpoint standard <xref:System.ServiceModel.Description.WebScriptEndpoint> al servizio.  Tale endpoint viene configurato in un indirizzo vuoto relativo al file con estensione svc.  Ciò significa che l'indirizzo del servizio è http:\/\/localhost\/ServiceModelSamples\/service.svc, senza suffissi aggiuntivi tranne il nome dell'operazione.  
  
```  
<%@ServiceHost language="C#" Debug="true" Service="Microsoft.Samples.SimpleAjaxService.CalculatorService" Factory="System.ServiceModel.Activation.WebScriptServiceHostFactory" %>  
```  
  
 L'oggetto <xref:System.ServiceModel.Description.WebScriptEndpoint> è pre\-configurato in modo che una pagina client AJAX ASP.NET sia in grado di accedere al servizio.  La sezione seguente in Web.config può essere usata per effettuare modifiche di configurazione aggiuntive all'endpoint  e può essere rimossa se tali modifiche non sono necessarie.  
  
```xml  
<system.serviceModel>  
  <standardEndpoints>  
    <webScriptEndpoint>  
      <!-- Use this element to configure the endpoint -->  
      <standardEndpoint name=""  />  
    </webScriptEndpoint>  
  </standardEndpoints>  
</system.serviceModel>  
  
```  
  
 L'oggetto <xref:System.ServiceModel.Description.WebScriptEndpoint> imposta il formato dei dati predefinito per il servizio su JSON anziché su XML.  Per richiamare il servizio, spostarsi su http:\/\/localhost\/ServiceModelSamples\/service.svc\/Add?  n1\=100&n2\=200 dopo avere completato i passaggi di configurazione e di compilazione illustrati più avanti in questo argomento.  Questa semplice funzionalità di test viene abilitata dall'uso di una richiesta HTTP GET.  
  
 La pagina Web SimpleAjaxClientPage.aspx del client contiene il codice ASP.NET per richiamare il servizio quando l'utente fa clic su uno dei pulsanti di operazione nella pagina.  Il controllo `ScriptManager` viene usato per rendere accessibile un proxy al servizio tramite JavaScript.  
  
```  
<asp:ScriptManager ID="ScriptManager" runat="server">  
     <Services>  
          <asp:ServiceReference Path="service.svc" />  
     </Services>  
</asp:ScriptManager>  
  
```  
  
 Viene creata un'istanza del proxy locale e le operazioni vengono richiamate usando il codice JavaScript seguente.  
  
```  
// Code for extracting arguments n1 and n2 omitted…  
// Instantiate a service proxy  
var proxy = new SimpleAjaxService.ICalculator();  
// Code for selecting operation omitted…  
proxy.Add(parseFloat(n1), parseFloat(n2), onSuccess, onFail, null);  
  
```  
  
 Se la chiamata al servizio riesce, il codice richiama il gestore `onSuccess` e il risultato dell'operazione viene visualizzato in una casella di testo.  
  
```  
function onSuccess(mathResult){  
     document.getElementById("result").value = mathResult;  
}  
  
```  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.  Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].  Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Ajax\SimpleAjaxService`  
  
## Vedere anche