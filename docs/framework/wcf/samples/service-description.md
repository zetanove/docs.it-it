---
title: "Descrizione del servizio | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7034b5d6-d608-45f3-b57d-ec135f83ff24
caps.latest.revision: 16
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 16
---
# Descrizione del servizio
L'esempio Descrizione del servizio illustra come un servizio può recuperare le informazioni di descrizione del servizio nella fase di esecuzione.L'esempio è basato su [Guida introduttiva](../../../../docs/framework/wcf/samples/getting-started-sample.md), con un'operazione del servizio aggiuntiva definita per restituire informazioni descrittive sul servizio.Le informazioni restituite elencano indirizzi di base e gli endpoint del servizio.Il servizio fornisce queste informazioni utilizzando le classi <xref:System.ServiceModel.OperationContext>, <xref:System.ServiceModel.ServiceHost> e <xref:System.ServiceModel.Description.ServiceDescription>.  
  
 In questo esempio, il client è un'applicazione console \(.exe\) e il servizio è ospitato da Internet Information Services \(IIS\).  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine dell'argomento.  
  
 Questo esempio utilizza una versione modificata del contratto della calcolatrice chiamata `IServiceDescriptionCalculator`.Il contratto definisce un'operazione del servizio aggiuntiva denominata `GetServiceDescriptionInfo` che restituisce una stringa su più righe al client che descrive l'indirizzo o gli indirizzi di base e l'endpoint o gli endpoint del servizio.  
  
```  
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
public interface IServiceDescriptionCalculator  
{  
    [OperationContract]  
    int Add(int n1, int n2);  
    [OperationContract]  
    int Subtract(int n1, int n2);  
    [OperationContract]  
    int Multiply(int n1, int n2);  
    [OperationContract]  
    int Divide(int n1, int n2);  
    [OperationContract]  
    string GetServiceDescriptionInfo();  
}  
  
```  
  
 Il codice di implementazione per `GetServiceDescriptionInfo` utilizza la classe<xref:System.ServiceModel.Description.ServiceDescription> per elencare gli endpoint del servizio.Poiché gli endpoint del servizio possono avere indirizzi relativi, elenca per primi gli indirizzi di base del servizio.Per ottenere tutte di queste informazioni il codice recupera il contesto dell'operazione utilizzando <xref:System.ServiceModel.OperationContext.Current%2A>.La classe <xref:System.ServiceModel.ServiceHost> e l'oggetto <xref:System.ServiceModel.Description.ServiceDescription> sono recuperati dal contesto dell'operazione.Per elencare gli endpoint di base del servizio il codice scorre la raccolta <xref:System.ServiceModel.ServiceHostBase.BaseAddresses%2A> dell'host del servizio.Per elencare gli endpoint del servizio il codice scorre la raccolta degli endpoint della descrizione del servizio.  
  
```  
public string GetServiceDescriptionInfo()  
{  
    string info = "";  
    OperationContext operationContext = OperationContext.Current;  
    ServiceHost host = (ServiceHost)operationContext.Host;  
    ServiceDescription desc = host.Description;  
    // Enumerate the base addresses in the service host.  
    info += "Base addresses:\n";  
    foreach (Uri uri in host.BaseAddresses)  
    {  
        info += "    " + uri + "\n";  
    }  
    // Enumerate the service endpoints in the service description.  
    info += "Service endpoints:\n";  
    foreach (ServiceEndpoint endpoint in desc.Endpoints)  
    {  
        info += "    Address:  " + endpoint.Address + "\n";  
        info += "    Binding:  " + endpoint.Binding.Name + "\n";  
        info += "    Contract: " + endpoint.Contract.Name + "\n";  
    }  
     return info;  
}  
  
```  
  
 Quando si esegue l'esempio, le operazioni della calcolatrice, e in seguito le informazioni del servizio, vengono restituite dall'operazione `GetServiceDescriptionInfo`.Premere INVIO nella finestra del client per arrestare il client.  
  
```  
Add(15,3) = 18  
Subtract(145,76) = 69  
Multiply(9,81) = 729  
Divide(22,7) = 3  
GetServiceDescriptionInfo  
Base addresses:  
    http://<machine-name>/ServiceModelSamples/service.svc  
    https://<machine-name>/ServiceModelSamples/service.svc  
Service endpoints:  
    Address:  http://<machine-name>/ServiceModelSamples/service.svc  
    Binding:  WSHttpBinding  
    Contract: IServiceDescriptionCalculator  
    Address:  http://<machine-name>/ServiceModelSamples/service.svc/mex  
    Binding:  MetadataExchangeHttpBinding  
    Contract: IMetadataExchange  
  
Press <ENTER> to terminate client.  
```  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Assicurarsi di aver eseguito [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare l'edizione in C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Per eseguire l'esempio in una configurazione con un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Services\ServiceDescription`  
  
## Vedere anche