---
title: "Durata personalizzata | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 52806c07-b91c-48fe-b992-88a41924f51f
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Durata personalizzata
In questo esempio viene descritto come scrivere un'estensione [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] per fornire servizi di durata personalizzata per le istanze del servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] condivise.  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine dell'argomento.  
  
## Istanze condivise  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] offre diverse modalità di istanza per le istanze del servizio.La modalità istanze condivise analizzata in questo argomento offre un modo per condividere un'istanza del servizio tra più canali.I client possono risolvere l'indirizzo dell'endpoint dell'istanza a livello locale o possono contattare un metodo factory nel servizio per ottenere l'indirizzo dell'endpoint di un'istanza in esecuzione.Una volta ottenuto l'indirizzo dell'endpoint, possono creare un nuovo canale e avviare la comunicazione.Il frammento di codice seguente mostra la creazione di un nuovo canale in un'istanza del servizio esistente da parte di un'applicazione client.  
  
```  
// Create the first channel.  
IEchoService proxy = channelFactory.CreateChannel();  
  
// Resolve the instance.  
EndpointAddress epa = ((IClientChannel)proxy).ResolveInstance();  
  
// Create new channel factory with the endpoint address resolved by   
// previous statement.  
ChannelFactory<IEchoService> channelFactory2 =  
                new ChannelFactory<IEchoService>("echoservice",  
                epa);  
  
// Create the second channel to the same instance.  
IEchoService proxy2 = channelFactory2.CreateChannel();  
  
```  
  
 A differenza di altre modalità di istanza, la modalità istanze condivise dispone di un modo univoco di rilascio di istanze del servizio.Quando tutti i canali sono chiusi per un'istanza, il runtime del servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] avvia un timer.Se nessuna connessione viene effettuata prima della scadenza del timeout, in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] viene rilasciata l'istanza e viene effettuata la richiesta delle risorse.Come parte della routine di chiusura, in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] viene richiamato il metodo <xref:System.ServiceModel.Dispatcher.IShareableInstanceContextLifetime.IsIdle%2A> di tutte le implementazioni di <xref:System.ServiceModel.Dispatcher.IShareableInstanceContextLifetime> prima di rilasciare l'istanza.Se tutte le implementazioni restituiscono `true`, l'istanza viene rilasciata.In caso contrario, l'implementazione <xref:System.ServiceModel.Dispatcher.IShareableInstanceContextLifetime> è responsabile della notifica al `Dispatcher` dello stato inattivo tramite un metodo di callback.  
  
 Per impostazione predefinita, il valore di timeout inattivo di <xref:System.ServiceModel.InstanceContext> è un minuto.In questo esempio viene tuttavia illustrato come estendere tale valore mediante un'estensione personalizzata.  
  
## Estensione di InstanceContext  
 In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] l'oggetto <xref:System.ServiceModel.InstanceContext> è il collegamento tra l'istanza del servizio e `Dispatcher`.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] consente di estendere tale componente di runtime aggiungendo un nuovo stato o comportamento mediante il modello di oggetti estensibili.Questo modello viene utilizzato in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] per estendere le classi del runtime esistenti con nuove funzionalità oppure per aggiungere nuove funzionalità di stato a un oggetto.Nel modello di oggetti estensibili sono disponibili tre interfacce: `IExtensibleObject<T>`, `IExtension<T>` e `IExtensionCollection<T>`.  
  
 L'interfaccia `IExtensibleObject<T>` viene implementata da oggetti che consentono alle estensioni di personalizzare la funzionalità.  
  
 L'interfaccia `IExtension<T>` viene implementata da oggetti che possono essere estensioni di classi di tipo `T`.  
  
 Infine, l'interfaccia `IExtensionCollection<T>` è una raccolta di `IExtensions` che consente di recuperare `IExtensions` in base al tipo.  
  
 Per estendere <xref:System.ServiceModel.InstanceContext>, è pertanto necessario implementare l'interfaccia `IExtension`.In questo progetto di esempio la classe `CustomLeaseExtension` include tale implementazione.  
  
```  
class CustomLeaseExtension : IExtension<InstanceContext>  
{  
}  
  
```  
  
 L'interfaccia `IExtension` dispone di due metodi: `Attach` e `Detach`.Come implicano i nomi, questi due metodi vengono chiamati quando il runtime connette e disconnette l'estensione a un'istanza della classe <xref:System.ServiceModel.InstanceContext>.In questo esempio, il metodo `Attach` viene utilizzato per tenere traccia dell'oggetto <xref:System.ServiceModel.InstanceContext> appartenente all'istanza corrente dell'estensione.  
  
```  
InstanceContext owner;  
  
public void Attach(InstanceContext owner)  
{  
  this.owner = owner;   
}  
```  
  
 Inoltre, è necessario aggiungere l'implementazione necessaria all'estensione per fornire il supporto di durata estesa.L'interfaccia `ICustomLease` viene pertanto dichiarata con i metodi desiderati e viene implementata nella classe `CustomLeaseExtension`.  
  
```  
interface ICustomLease  
{  
    bool IsIdle { get; }          
    InstanceContextIdleCallback Callback { get; set; }  
}  
  
class CustomLeaseExtension : IExtension<InstanceContext>, ICustomLease  
{  
}  
  
```  
  
 Quando [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] richiama il metodo <xref:System.ServiceModel.Dispatcher.IShareableInstanceContextLifetime.IsIdle%2A> nell'implementazione <xref:System.ServiceModel.Dispatcher.IShareableInstanceContextLifetime>, tale chiamata viene indirizzata al metodo <xref:System.ServiceModel.Dispatcher.IShareableInstanceContextLifetime.IsIdle%2A> dell'estensione `CustomLeaseExtension`.`CustomLeaseExtension` controlla quindi lo stato privato per verificare se <xref:System.ServiceModel.InstanceContext> è inattivo.Se è inattivo, viene restituito `true`.In caso contrario, viene avviato un timer per un tempo specificato della durata estesa.  
  
```  
public bool IsIdle  
{  
  get  
  {  
    lock (thisLock)  
    {  
      if (isIdle)  
      {  
        return true;  
      }  
      else  
      {  
        StartTimer();  
        return false;  
      }  
    }  
  }  
}  
  
```  
  
 Nell'evento `Elapsed` del timer la funzione di callback nel dispatcher viene chiamata per avviare un altro ciclo di pulizia.  
  
```  
void idleTimer_Elapsed(object sender, ElapsedEventArgs args)  
{  
    idleTimer.Stop();  
    isIdle = true;    
    callback(owner);  
}  
  
```  
  
 Non è possibile rinnovare in alcun modo il timer in esecuzione all'arrivo di un nuovo messaggio relativo al passaggio dell'istanza nello stato inattivo.  
  
 L'esempio implementa <xref:System.ServiceModel.Dispatcher.IShareableInstanceContextLifetime> per intercettare le chiamate al metodo <xref:System.ServiceModel.Dispatcher.IShareableInstanceContextLifetime.IsIdle%2A> e indirizzarle a `CustomLeaseExtension`.L'implementazione <xref:System.ServiceModel.Dispatcher.IShareableInstanceContextLifetime> è inclusa nella classe `CustomLifetimeLease`.Il metodo <xref:System.ServiceModel.Dispatcher.IShareableInstanceContextLifetime.IsIdle%2A> viene richiamato quando [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] sta per rilasciare l'istanza del servizio.Tuttavia, esiste solo un'istanza di una specifica implementazione `ISharedSessionInstance` nella raccolta <xref:System.ServiceModel.Dispatcher.DispatchRuntime.InstanceContextLifetimes%2A> di ServiceBehavior.Ciò significa che non è possibile sapere che <xref:System.ServiceModel.InstanceContext> viene chiuso quando [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] controlla il metodo <xref:System.ServiceModel.Dispatcher.IShareableInstanceContextLifetime.IsIdle%2A>.Questo esempio utilizza pertanto blocchi di thread per serializzare le richieste al metodo <xref:System.ServiceModel.Dispatcher.IShareableInstanceContextLifetime.IsIdle%2A>.  
  
> [!IMPORTANT]
>  L'utilizzo di blocchi di thread non è un approccio consigliato perché la serializzazione può influenzare negativamente le prestazioni dell'applicazione.  
  
 Una variabile membro privato viene utilizzata nella classe `CustomLeaseExtension` per rilevare il valore `IsIdle`.Ogni volta che viene recuperato il valore di <xref:System.ServiceModel.Dispatcher.IShareableInstanceContextLifetime>, il membro privato `IsIdle` viene restituito e reimpostato su `false`.È essenziale impostare questo valore su `false` per assicurarsi che il dispatcher chiami il metodo <xref:System.ServiceModel.Dispatcher.IShareableInstanceContextLifetime.NotifyIdle%2A>.  
  
```  
public bool IsIdle  
{  
    get   
    {  
       lock (thisLock)  
       {  
           bool idleCopy = isIdle;  
           isIdle = false;  
           return idleCopy;  
       }  
    }  
}  
  
```  
  
 Se la proprietà `ISharedSessionLifetime.IsIdle` restituisce `false`, il dispatcher registra una funzione di callback tramite il metodo `NotifyIdle`.Tale metodo riceve un riferimento al <xref:System.ServiceModel.InstanceContext> rilasciato.Pertanto il codice di esempio può eseguire una query dell'estensione di tipo `ICustomLease` e archiviare la proprietà `ICustomLease.IsIdle` nello stato esteso.  
  
```  
public void NotifyIdle(InstanceContextIdleCallback callback,   
            InstanceContext instanceContext)  
{  
    lock (thisLock)  
    {  
       ICustomLease customLease =  
           instanceContext.Extensions.Find<ICustomLease>();  
       customLease.Callback = callback;   
       isIdle = customLease.IsIdle;  
       if (isIdle)  
       {  
             callback(instanceContext);  
       }  
    }   
}  
  
```  
  
 Prima che la proprietà `ICustomLease.IsIdle` venga verificata, è necessario impostare la proprietà di callback, poiché ciò è essenziale affinché `CustomLeaseExtension` notifichi al dispatcher quando diventa inattiva.Se `ICustomLease.IsIdle` restituisce `true`, il membro privato `isIdle` viene semplicemente impostato in `CustomLifetimeLease` su `true` e chiama il metodo di callback.Poiché il codice contiene un blocco, gli altri thread non possono modificare il valore del membro privato.La volta successiva che il dispatcher controlla `ISharedSessionLifetime.IsIdle`, restituisce `true` e consente al dispatcher di rilasciare l'istanza.  
  
 Una volta completato il lavoro di base per l'estensione personalizzata, quest'ultima deve essere associata al modello del servizio.Per collegare l'implementazione `CustomLeaseExtension` a <xref:System.ServiceModel.InstanceContext>, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] fornisce l'interfaccia <xref:System.ServiceModel.Dispatcher.IInstanceContextInitializer> per eseguire l'avvio di <xref:System.ServiceModel.InstanceContext>.Nell'esempio, la classe `CustomLeaseInitializer` implementa tale interfaccia e aggiunge un'istanza di `CustomLeaseExtension` alla raccolta <xref:System.ServiceModel.InstanceContext.Extensions%2A> dalla sola inizializzazione del metodo.Questo metodo viene chiamato dal dispatcher durante l'inizializzazione di <xref:System.ServiceModel.InstanceContext>.  
  
```  
public void Initialize(InstanceContext instanceContext, Message message)  
{  
  IExtension<InstanceContext> customLeaseExtension =  
    new CustomLeaseExtension(timeout);  
  instanceContext.Extensions.Add(customLeaseExtension);  
}  
```  
  
 Infine, le implementazioni di <xref:System.ServiceModel.Dispatcher.IShareableInstanceContextLifetime> e <xref:System.ServiceModel.Dispatcher.IInstanceContextInitializer> sono associate al modello del servizio tramite l'implementazione <xref:System.ServiceModel.Description.IServiceBehavior>.Tale implementazione viene posizionata nella classe `CustomLeaseTimeAttribute` e deriva dalla classe di base `Attribute` per esporre questo comportamento come attributo.Nel metodo `IServiceBehavior.ApplyBehavior`, le istanze delle implementazioni di <xref:System.ServiceModel.Dispatcher.IInstanceContextInitializer> e <xref:System.ServiceModel.Dispatcher.IShareableInstanceContextLifetime> vengono aggiunte rispettivamente alle raccolte <xref:System.ServiceModel.Dispatcher.DispatchRuntime.InstanceContextLifetimes%2A> e <xref:System.ServiceModel.Dispatcher.DispatchRuntime.InstanceContextInitializers%2A> di <xref:System.ServiceModel.Dispatcher>.  
  
```  
public void ApplyBehavior(ServiceDescription description,   
           ServiceHostBase serviceHostBase,   
           Collection<DispatchBehavior> behaviors,  
           Collection<BindingParameterCollection> parameters)  
{  
    CustomLifetimeLease customLease = new CustomLifetimeLease();  
    CustomLeaseInitializer initializer =   
                new CustomLeaseInitializer(timeout);  
  
    foreach (DispatchBehavior dispatchBehavior in behaviors)  
    {  
        dispatchBehavior.InstanceContextLifetimes.Add(customLease);  
        dispatchBehavior.InstanceContextInitializers.Add(initializer);  
    }  
}  
  
```  
  
 Questo comportamento può essere aggiunto a una classe del servizio di esempio mediante annotazione con l'attributo `CustomLeaseTime`.  
  
```  
[ServiceBehavior(InstanceContextMode=InstanceContextMode.Shareable)]  
[CustomLeaseTime(Timeout = 20000)]  
public class EchoService : IEchoService  
{  
  //…  
}  
```  
  
 Quando si esegue l'esempio, le richieste e le risposte dell'operazione vengono visualizzate nelle finestre della console client e del servizio.Premere INVIO in tutte le finestre della console per arrestare il servizio e il client.  
  
#### Per impostare, compilare ed eseguire l'esempio  
  
1.  Assicurarsi di avere eseguito [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare l'edizione in C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Per eseguire l'esempio in una configurazione con un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Extensibility\Instancing\Lifetime`  
  
## Vedere anche