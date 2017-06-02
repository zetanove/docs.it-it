---
title: "Servizio AJAX senza configurazione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e6db7acd-5679-45d4-b98a-8449c6873838
caps.latest.revision: 23
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 23
---
# Servizio AJAX senza configurazione
Questo esempio illustra come usare [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] per creare un servizio AJAX \(ASP.NET Asynchronous JavaScript and XML\) di base, ovvero un servizio al quale è possibile accedere usando codice JavaScript da un client browser Web senza usare alcuna impostazione di configurazione.  Il servizio usa sintassi speciale nel file con estensione svc per abilitare automaticamente un endpoint AJAX.  
  
 Il supporto AJAX in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] è ottimizzato per l'uso con ASP.NET AJAX tramite il controllo `ScriptManager`.  Per un esempio d'uso di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] con ASP.NET AJAX, vedere [Ajax Samples](http://msdn.microsoft.com/it-it/f3fa45b3-44d5-4926-8cc4-a13c30a3bf3e).  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine di questo argomento.  
  
 Nell'esempio viene usato il servizio AJAX con il protocollo HTTP POST.  Come descritto nell'esempio [Servizio AJAX di base](../../../../docs/framework/wcf/samples/basic-ajax-service.md), <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory> è usato per ospitare il servizio.  
  
```  
<%ServiceHost  
    language=c#  
    Debug="true"  
    Service="Microsoft.Ajax.Samples.CalculatorService  
    Factory="System.ServiceModel.Activation.WebScriptServiceHostFactory"  
%>  
  
```  
  
 <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory> aggiunge automaticamente un elemento <xref:System.ServiceModel.Description.WebScriptEndpoint> al servizio.  Se non è necessario modificare la configurazione dell'endpoint, la sezione \<system.ServiceModel\> può essere rimossa completamente dal file Web.config del servizio.  Il file Web.config contiene alcune impostazioni di ASP.NET che vengono usate da ConfigFreeClientPage.aspx.  Se la situazione è diversa, il file Web.config potrebbe essere totalmente rimosso.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.  Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].  Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Ajax\ConfigFreeAjaxService`  
  
#### Per impostare, compilare ed eseguire l'esempio  
  
1.  Verificare l'esecuzione delle istruzioni di installazione descritte in [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Compilare la soluzione XmlAjaxService.sln come descritto in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Spostarsi alla pagina http:\/\/localhost\/ServiceModelSamples\/ConfigFreeClientPage.aspx \(non aprire ConfigFreeClientPage.aspx nel browser all'interno della directory del progetto\).  
  
> [!NOTE]
>  Quando si esegue questo esempio, assicurarsi che Autenticazione anonima e Autenticazione Windows non siano abilitate simultaneamente per la cartella ServiceModelSamples in IIS.  Se così dovesse essere, disabilitare l'autenticazione Windows.  Dopo aver eseguito l'esempio, abilitare l'autenticazione Windows ed eseguire "iisreset".  
  
## Vedere anche  
 [Servizio AJAX di base](../../../../docs/framework/wcf/samples/basic-ajax-service.md)