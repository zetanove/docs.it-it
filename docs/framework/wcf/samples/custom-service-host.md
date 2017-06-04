---
title: "Host di servizi personalizzati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fe16ff50-7156-4499-9c32-13d8a79dc100
caps.latest.revision: 16
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 16
---
# Host di servizi personalizzati
Questo esempio dimostra come usare un derivato personalizzato della classe <xref:System.ServiceModel.ServiceHost> per modificare il comportamento in fase di esecuzione di un servizio.  Questo approccio fornisce un'alternativa riusabile alla configurazione tradizionale di un gran numero di servizi.  In questo esempio viene inoltre illustrato come impiegare la classe <xref:System.ServiceModel.Activation.ServiceHostFactory> per usare un ServiceHost personalizzato nell'ambiente di hosting Internet Information Services \(IIS\) o nel servizio di attivazione dei processi di Windows \(WAS, Windows Process Activation Service\).  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.  Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].  Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Extensibility\Hosting\CustomServiceHost`  
  
## Informazioni sullo scenario  
 Per impedire la rivelazione non intenzionale di metadati del servizio potenzialmente riservati, la configurazione predefinita per i servizi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] disabilita la pubblicazione dei metadati.  Questo comportamento è protetto per impostazione predefinita, ma significa inoltre che non è possibile usare uno strumento di importazione di metadati \(ad esempio Svcutil.exe\) per generare il codice client necessario per chiamare il servizio, a meno che il comportamento del servizio di pubblicazione dei metadati non venga abilitato in modo esplicito in fase di configurazione.  
  
 L'abilitazione della pubblicazione dei metadati per un gran numero di servizi comporta l'aggiunta degli stessi elementi di configurazione a ciascun singolo servizio, che produce una quantità elevata di informazioni di configurazione sostanzialmente uguali.  Come alternativa alla configurazione di ogni singolo servizio, è possibile scrivere il codice imperativo che consente la pubblicazione dei metadati una volta e riusare quindi tale codice su vari servizi diversi.  Ciò viene ottenuto creando una nuova classe che viene derivata da <xref:System.ServiceModel.ServiceHost> ed esegue l'override del metodo `ApplyConfiguration`\(\) per aggiungere imperativamente il comportamento di pubblicazione di metadati.  
  
> [!IMPORTANT]
>  Per maggior chiarezza, questo esempio illustra come creare un endpoint non protetto per la configurazione di metadati.  Tali endpoint sono potenzialmente disponibili per utenti anonimi non autenticati e bisogna fare attenzione prima di distribuirli per garantire che la pubblicazione dei metadati di un servizio sia appropriata.  
  
## Implementazione di un ServiceHost personalizzato  
 La classe <xref:System.ServiceModel.ServiceHost> espone diversi metodi virtuali utili che possono essere sottoposti a override dagli eredi per modificare il comportamento di un servizio in fase di esecuzione.  Ad esempio, il metodo `ApplyConfiguration`\(\) legge informazioni di configurazione del servizio dall'archivio di configurazione e modifica di conseguenza <xref:System.ServiceModel.Description.ServiceDescription> dell'host.  L'implementazione predefinita legge la configurazione dal file di configurazione dell'applicazione.  Le implementazioni personalizzate possono eseguire l'override di `ApplyConfiguration`\(\) per alterare ulteriormente la <xref:System.ServiceModel.Description.ServiceDescription> usando codice imperativo o anche sostituire completamente l'archivio di configurazione predefinito.  Ad esempio, per leggere la configurazione dell'endpoint di un servizio da un database anziché il file di configurazione dell'applicazione.  
  
 In questo esempio si desidera compilare un ServiceHost personalizzato che aggiunge il ServiceMetadataBehavior, \(il quale consente la pubblicazione di metadati\) anche se questo comportamento non viene aggiunto in modo esplicito nel file di configurazione del servizio.  Per ottenere questo risultato, viene creata una nuova classe che eredita da <xref:System.ServiceModel.ServiceHost> ed esegue l'override di `ApplyConfiguration`\(\).  
  
```  
class SelfDescribingServiceHost : ServiceHost  
{  
    public SelfDescribingServiceHost(Type serviceType, params Uri[] baseAddresses)  
        : base(serviceType, baseAddresses) { }  
  
    //Overriding ApplyConfiguration() allows us to   
    //alter the ServiceDescription prior to opening  
    //the service host.   
    protected override void ApplyConfiguration()  
    {  
        //First, we call base.ApplyConfiguration()  
        //to read any configuration that was provided for  
        //the service we're hosting. After this call,  
        //this.Description describes the service  
        //as it was configured.  
        base.ApplyConfiguration();       
  
        //(rest of implementation elided for clarity)  
    }  
}  
```  
  
 Poiché ogni configurazione fornita nel file di configurazione dell'applicazione non va ignorata, la prima operazione di override di `ApplyConfiguration`\(\) è chiamare l'implementazione di base.  Dopo che questo metodo è stato completato, è possibile aggiungere in modo imperativo <xref:System.ServiceModel.Description.ServiceMetadataBehavior> alla descrizione usando il codice imperativo seguente.  
  
```  
ServiceMetadataBehavior mexBehavior = this.Description.Behaviors.Find<ServiceMetadataBehavior>();  
if (mexBehavior == null)  
{  
    mexBehavior = new ServiceMetadataBehavior();  
    this.Description.Behaviors.Add(mexBehavior);  
}  
else  
{  
    //Metadata behavior has already been configured,   
    //so we do not have any work to do.  
    return;  
}  
```  
  
 L'ultima operazione dell'override di `ApplyConfiguration`\(\) è aggiungere l'endpoint di metadati predefinito.  Per convenzione, viene creato uno endpoint di metadati per ciascun URI nella raccolta BaseAddresses del host del servizio.  
  
```  
//Add a metadata endpoint at each base address  
//using the "/mex" addressing convention  
foreach (Uri baseAddress in this.BaseAddresses)  
{  
    if (baseAddress.Scheme == Uri.UriSchemeHttp)  
    {  
        mexBehavior.HttpGetEnabled = true;  
        this.AddServiceEndpoint(ServiceMetadataBehavior.MexContractName,  
                                MetadataExchangeBindings.CreateMexHttpBinding(),  
                                "mex");  
    }  
    else if (baseAddress.Scheme == Uri.UriSchemeHttps)  
    {  
        mexBehavior.HttpsGetEnabled = true;  
        this.AddServiceEndpoint(ServiceMetadataBehavior.MexContractName,  
                                MetadataExchangeBindings.CreateMexHttpsBinding(),  
                                "mex");  
    }  
    else if (baseAddress.Scheme == Uri.UriSchemeNetPipe)  
    {  
        this.AddServiceEndpoint(ServiceMetadataBehavior.MexContractName,  
                                MetadataExchangeBindings.CreateMexNamedPipeBinding(),  
                                "mex");  
    }  
    else if (baseAddress.Scheme == Uri.UriSchemeNetTcp)  
    {  
        this.AddServiceEndpoint(ServiceMetadataBehavior.MexContractName,  
                                MetadataExchangeBindings.CreateMexTcpBinding(),  
                                "mex");  
    }  
}  
  
```  
  
## Uso di un ServiceHost personalizzato in host indipendente  
 Ora che è stata completata l'implementazione personalizzata di ServiceHost, è possibile usarlo per aggiungere il comportamento di pubblicazione dei metadati a qualsiasi servizio ospitando tale servizio all'interno di un'istanza di `SelfDescribingServiceHost`.  Nell'esempio di codice seguente viene illustrato come usarlo nello scenario di host indipendente.  
  
```  
SelfDescribingServiceHost host =   
         new SelfDescribingServiceHost( typeof( Calculator ) );  
host.Open();  
```  
  
 L'host personalizzato legge comunque la configurazione dell'endpoint del servizio dal file di configurazione dell'applicazione, come se fosse stata usata la classe <xref:System.ServiceModel.ServiceHost> predefinita per ospitare il servizio.  Tuttavia, poiché è stata aggiunta la logica per abilitare la pubblicazione dei metadati all'interno dell'host personalizzato, non è più necessario abilitare in modo esplicito il comportamento di pubblicazione dei metadati nella configurazione.  L'approccio offre un vantaggio evidente quando si compila un'applicazione che contiene diversi servizi e si desidera abilitare la pubblicazione dei metadati su ognuno di essi senza riscrivere ripetutamente gli stessi elementi di configurazione.  
  
## Uso di un ServiceHost personalizzato in IIS e WAS  
 L'uso di un host del servizio personalizzato in scenari di host indipendente è semplice in quanto spetta fondamentalmente al codice dell'applicazione la responsabilità di creare e aprire l'istanza dell'host del servizio.  Nell'ambiente di hosting di IIS o WAS, tuttavia, l'infrastruttura [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] crea in modo dinamico istanze dell'host del servizio in risposta ai messaggi in arrivo.  Gli host del servizio personalizzati possono essere usati anche in questo ambiente di hosting, ma richiedono del codice aggiuntivo nel modulo di un ServiceHostFactory.  Nel codice seguente è illustrato un derivato di <xref:System.ServiceModel.Activation.ServiceHostFactory> che restituisce istanze del `SelfDescribingServiceHost` personalizzato.  
  
```  
public class SelfDescribingServiceHostFactory : ServiceHostFactory  
{  
    protected override ServiceHost CreateServiceHost(Type serviceType,   
     Uri[] baseAddresses)  
    {  
        //All the custom factory does is return a new instance  
        //of our custom host class. The bulk of the custom logic should  
        //live in the custom host (as opposed to the factory)   
        //for maximum  
        //reuse value outside of the IIS/WAS hosting environment.  
        return new SelfDescribingServiceHost(serviceType,     
                                             baseAddresses);  
    }  
}  
```  
  
 Come è possibile vedere, l'implementazione di un ServiceHostFactory personalizzato è molto semplice.  Tutta la logica personalizzata risiede all'interno dell'implementazione ServiceHost; la factory restituisce un'istanza della classe derivata.  
  
 Per usare una factory personalizzata con un'implementazione del servizio, è necessario aggiungere altri metadati al file con estensione svc del servizio.  
  
```  
<%@ServiceHost Service="Microsoft.ServiceModel.Samples.CalculatorService"  
               Factory="Microsoft.ServiceModel.Samples.SelfDescribingServiceHostFactory"  
               language=c# Debug="true" %>  
```  
  
 Qui è stato aggiunto un altro attributo `Factory` alla direttiva `@ServiceHost` al quale è stato passato come valore il nome del tipo CLR della factory personalizzata.  Quando IIS o WAS riceve un messaggio per questo servizio, l'infrastruttura di hosting di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] prima crea un'istanza di ServiceHostFactory e quindi attiva un'istanza dell'host del servizio stesso chiamando `ServiceHostFactory.CreateServiceHost()`.  
  
## Esecuzione dell'esempio  
 Anche se questo esempio fornisce un'implementazione del client e del servizio completamente funzionante, l'obiettivo dell'esempio è illustrare come modificare il comportamento in fase di esecuzione di un servizio per mezzo di un host personalizzato eseguendo le operazioni seguenti:  
  
#### Per osservare l'effetto dell'host personalizzato  
  
1.  Aprire il file Web.config del servizio e osservare come non vi sia alcuna configurazione che abilita in modo esplicito i metadati per il servizio.  
  
2.  Aprire il file con estensione svc del servizio e osservare che la relativa direttiva @ServiceHost contiene un attributo Factory che specifica il nome di un ServiceHostFactory personalizzato.  
  
#### Per impostare, compilare ed eseguire l'esempio  
  
1.  Assicurarsi di avere eseguito la [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare la soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Dopo aver compilato la soluzione, eseguire Setup.bat per configurare l'applicazione ServiceModelSamples in [!INCLUDE[iisver](../../../../includes/iisver-md.md)].  La directory ServiceModelSamples verrà ora visualizzata come applicazione [!INCLUDE[iisver](../../../../includes/iisver-md.md)].  
  
4.  Per eseguire l'esempio su un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
5.  Per rimuovere l'applicazione [!INCLUDE[iisver](../../../../includes/iisver-md.md)], eseguire Cleanup.bat.  
  
## Vedere anche  
 [Procedura: ospitare un servizio WCF in IIS](../../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-iis.md)