---
title: "Esempio di servizio AJAX che utilizza tipi complessi | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 88242b99-4811-4cbe-8201-52ddf48fb174
caps.latest.revision: 16
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 16
---
# Esempio di servizio AJAX che utilizza tipi complessi
Questo esempio illustra come utilizzare [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] per creare un servizio AJAX \(ASP.NET Asynchronous JavaScript e XML\) che crea istanze di tipi complessi e li invia tra servizio e client come JSON \(JavaScript Object Notation\).È possibile accedere a un servizio AJAX utilizzando codice JavaScript a partire da un client del browser Web.Questo esempio si basa sull'esempio [Servizio AJAX di base](../../../../docs/framework/wcf/samples/basic-ajax-service.md).  
  
 Il supporto AJAX in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] è ottimizzato per l'utilizzo con ASP.NET AJAX tramite il controllo <xref:System.Web.UI.ScriptManager>.Per un esempio di utilizzo di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] con ASP.NET AJAX, vedere [AJAX Samples](http://msdn.microsoft.com/it-it/f3fa45b3-44d5-4926-8cc4-a13c30a3bf3e).  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine dell'argomento.  
  
 Il servizio dell'esempio seguente è un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] senza codice specifico per AJAX.Perché l'attributo <xref:System.ServiceModel.Web.WebGetAttribute> non è applicato, viene utilizzato il verbo HTTP predefinito \("POST"\).Il servizio ha un'operazione, `DoMath` che restituisce un tipo complesso denominato `MathResult`.Il tipo complesso è un tipo di contratto dati standard che non contiene codice AJAX specifico.  
  
```  
[DataContract]  
    public class MathResult  
    {  
        [DataMember]  
        public double sum;  
        [DataMember]  
        public double difference;  
        [DataMember]  
        public double product;  
        [DataMember]  
        public double quotient;  
    }  
```  
  
 Creare un endpoint AJAX sul servizio utilizzando <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory>, proprio come nell'esempio del servizio AJAX di base.  
  
 La pagina Web ComplexTypeClientPage.aspx del client contiene il codice ASP.NET e JavaScript per richiamare il servizio quando l'utente fa clic sul pulsante **Esegui calcolo** nella pagina.Il codice per richiamare il servizio costruisce un corpo JSON e lo invia utilizzando HTTP POST, in modo simile all'esempio [Servizio AJAX con il protocollo HTTP POST](../../../../docs/framework/wcf/samples/ajax-service-using-http-post.md).  
  
 Dopo che la chiamata del servizio riesce, è possibile accedere ai membri dati singoli \(`sum`, `difference`, `product` e `quotient`\) sull'oggetto JavaScript risultante.  
  
```  
function onSuccess(mathResult){  
     document.getElementById("sum").value = mathResult.sum;  
     document.getElementById("difference").value = mathResult.difference;  
     document.getElementById("product").value = mathResult.product;  
     document.getElementById("quotient").value = mathResult.quotient;  
}  
  
```  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Assicurarsi di aver eseguito la [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Compilare la soluzione ComplexTypeAjaxService.sln come descritto in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Spostarsi alla pagina http:\/\/localhost\/ServiceModelSamples\/ComplexTypeClientPage.aspx \(non aprire ComplexTypeClientPage.aspx nel browser all'interno della directory del progetto\).  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Ajax\ComplexTypeAjaxService`  
  
## Vedere anche  
 [Servizio AJAX di base](../../../../docs/framework/wcf/samples/basic-ajax-service.md)