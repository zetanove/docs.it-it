---
title: "Comportamento di pubblicazione dei metadati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Esempio di comportamenti di pubblicazione dei metadati [Windows Communication Foundation]"
  - "comportamenti dei servizi, esempio di pubblicazione dei metadati"
ms.assetid: 78c13633-d026-4814-910e-1c801cffdac7
caps.latest.revision: 23
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 23
---
# Comportamento di pubblicazione dei metadati
L'esempio Comportamento di pubblicazione dei metadati illustra come controllare le caratteristiche di pubblicazione dei metadati di un servizio.Per impedire la rivelazione non intenzionale di metadati del servizio potenzialmente riservati, la configurazione predefinita per i servizi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] disabilita la pubblicazione dei metadati.Questo comportamento è protetto per impostazione predefinita, ma significa inoltre che non è possibile utilizzare uno strumento di importazione di metadati \(ad esempio Svcutil.exe\) per generare il codice client necessario per chiamare il servizio, a meno che il comportamento del servizio di pubblicazione dei metadati non venga abilitato in modo esplicito in fase di configurazione.  
  
> [!IMPORTANT]
>  Per maggior chiarezza, questo esempio illustra come creare un endpoint non protetto per la configurazione di metadati.Tali endpoint sono potenzialmente disponibili per utenti anonimi non autenticati anonimi e bisogna fare attenzione prima di distribuirli per garantire che la pubblicazione dei metadati di un servizio sia appropriata.Vedere l'esempio [Endpoint di metadati protetto personalizzato](../../../../docs/framework/wcf/samples/custom-secure-metadata-endpoint.md) per un esempio di protezione di un endpoint di metadati.  
  
 L'esempio si basa su [Guida introduttiva](../../../../docs/framework/wcf/samples/getting-started-sample.md), che implementa il contratto di servizio  `ICalculator`.In questo esempio, il client è un'applicazione console \(.exe\) e il servizio è ospitato da Internet Information Services \(IIS\).  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine dell'argomento.  
  
 Affinché un servizio esponga metadati, la classe <xref:System.ServiceModel.Description.ServiceMetadataBehavior> deve essere configurata nel servizio.Quando questo comportamento è presente, è possibile pubblicare metadati configurando un endpoint per esporre il contratto <xref:System.ServiceModel.Description.IMetadataExchange> come un'implementazione di un protocollo WS\-MetadataExchange \(MEX\).Per convenienza, a questo contratto è stato dato il nome di configurazione abbreviato seguente: "IMetadataExchange."In questo esempio viene utilizzata l'associazione `mexHttpBinding`, ovvero un'utile associazione standard equivalente all'associazione `wsHttpBinding` con la modalità di sicurezza impostata su `None`.Nell'endpoint viene utilizzato un indirizzo relativo "mex" che, quando risolto rispetto all'indirizzo di base dei servizi, produce l'indirizzo di endpoint "http:\/\/localhost\/servicemodelsamples\/service.svc\/mex".Di seguito viene illustrata la configurazione del comportamento:  
  
```  
<behaviors>  
  <serviceBehaviors>  
    <behavior name="CalculatorServiceBehavior">  
      <!-- The serviceMetadata behavior publishes metadata through   
           the IMetadataExchange contract. When this behavior is   
           present, you can expose this contract through an endpoint   
           as shown below. Setting httpGetEnabled to true publishes   
           the service's WSDL at the <baseaddress>?wsdl, for example,  
           http://localhost/servicemodelsamples/service.svc?wsdl -->  
      <serviceMetadata httpGetEnabled="True"/>  
      <serviceDebug includeExceptionDetailInFaults="False" />  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
```  
  
 Di seguito viene illustrato l'endpoint MEX.  
  
```  
<!-- the MEX endpoint is exposed at   
     http://localhost/servicemodelsamples/service.svc/mex   
     To expose the IMetadataExchange contract, you   
     must enable the serviceMetadata behavior as demonstrated                           
     previously. -->  
<endpoint address="mex"  
          binding="mexHttpBinding"  
          contract="IMetadataExchange" />  
```  
  
 Questo esempio imposta la proprietà <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpGetEnabled%2A> su `true`, che espone anche i metadati del servizio utilizzando HTTP GET.Per abilitare un endpoint di metadati HTTP GET, il servizio deve avere un indirizzo di base HTTP.La stringa di query `?wsdl` viene utilizzata sull'indirizzo di base del servizio per accedere ai metadati.Ad esempio, per vedere il linguaggio WSDL del servizio in un browser Web si utilizzerebbe l'indirizzo http:\/\/localhost\/servicemodelsamples\/service.svc? il wsdl.In alternativa, è possibile utilizzare questo comportamento per esporre metadati su HTTP impostando <xref:System.ServiceModel.Description.ServiceMetadataBehavior.HttpsGetEnabled%2A> su `true`.Ciò richiede un indirizzo di base HTTP.  
  
 Per accedere all'endpoint MEX del servizio utilizzare [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md).  
  
 `svcutil.exe /n:"http://Microsoft.ServiceModel.Samples,Microsoft.ServiceModel.Samples" http://localhost/servicemodelsamples/service.svc/mex /out:generatedClient.cs`  
  
 Ciò genera un client basato sui metadati del servizio.  
  
 Per accedere ai metadati del servizio utilizzando HTTP GET, puntare il browser su http:\/\/localhost\/servicemodelsamples\/service.svc? il wsdl.  
  
 Se si rimuove questo comportamento e si tenta di aprire il servizio si otterrà un'eccezione.Questo errore si verifica perché senza il comportamento, l'endpoint configurato con il contratto `IMetadataExchange` non viene implementato.  
  
 Se si imposta `HttpGetEnabled` su `false`, si vede la pagina della Guida di CalculatorService invece dei metadati del servizio.  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Verificare di avere eseguito [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare l'edizione in C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Per eseguire l'esempio in una configurazione con un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Services\Behaviors\Metadata`  
  
## Vedere anche