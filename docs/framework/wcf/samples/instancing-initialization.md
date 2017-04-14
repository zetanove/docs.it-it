---
title: "Inizializzazione della creazione di istanze | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 154d049f-2140-4696-b494-c7e53f6775ef
caps.latest.revision: 31
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 31
---
# Inizializzazione della creazione di istanze
Questo esempio estende l'esempio [Pooling](../../../../docs/framework/wcf/samples/pooling.md) definendo un'interfaccia, `IObjectControl`, che personalizza l'inizializzazione di un oggetto attivandolo e disattivandolo.Il client richiama metodi che restituiscono l'oggetto al pool e che non restituiscono l'oggetto al pool.  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine dell'argomento.  
  
## Punti di estensibilità  
 Il primo passaggio per creare un'estensione di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] è decidere il punto di estensibilità da utilizzare.In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] il termine *EndpointDispatcher* fa riferimento a un componente runtime responsabile della conversione dei messaggi in arrivo in chiamate al metodo sul servizio dell'utente e della conversione di valori restituiti da quel metodo in un messaggio in uscita.Un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] crea un EndpointDispatcher per ogni endpoint.  
  
 L'EndpointDispatcher offre l'estensibilità dell'ambito dell'endpoint \(per tutti i messaggi ricevuti o inviati dal servizio\) utilizzando la classe <xref:System.ServiceModel.Dispatcher.EndpointDispatcher>.Questa classe consente di personalizzare le varie proprietà che controllano il comportamento dell'EndpointDispatcher.Questo esempio si concentra sulla proprietà <xref:System.ServiceModel.Dispatcher.DispatchRuntime.InstanceProvider%2A> che punta all'oggetto che fornisce le istanze della classe del servizio.  
  
## IInstanceProvider  
 In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], l'EndpointDispatcher crea istanze di una classe di servizio utilizzando un provider di istanze che implementa l'interfaccia <xref:System.ServiceModel.Dispatcher.IInstanceProvider>.Questa interfaccia dispone solo di due metodi:  
  
-   <xref:System.ServiceModel.Dispatcher.IInstanceProvider.GetInstance%2A>: quando un messaggio arriva, il dispatcher chiama il metodo <xref:System.ServiceModel.Dispatcher.IInstanceProvider.GetInstance%2A> per creare un'istanza della classe di servizio al fine di elaborare il messaggio.La frequenza delle chiamate a questo metodo è determinata dalla proprietà <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A>.Ad esempio, se la proprietà <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A> è impostata su <xref:System.ServiceModel.InstanceContextMode?displayProperty=fullName> viene creata una nuova istanza della classe di servizio per elaborare ogni messaggio che arriva, pertanto il metodo <xref:System.ServiceModel.Dispatcher.IInstanceProvider.GetInstance%2A> viene chiamato ogni qualvolta arriva un messaggio.  
  
-   <xref:System.ServiceModel.Dispatcher.IInstanceProvider.ReleaseInstance%2A>: quando l'istanza del servizio finisce l'elaborazione del messaggio, l'EndpointDispatcher chiama il metodo <xref:System.ServiceModel.Dispatcher.IInstanceProvider.ReleaseInstance%2A>.Come per il metodo <xref:System.ServiceModel.Dispatcher.IInstanceProvider.GetInstance%2A>, la frequenza delle chiamate a questo metodo è determinata dalla proprietà <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A>.  
  
## Pool di oggetti  
 La classe `ObjectPoolInstanceProvider` contiene l'implementazione per il pool di oggetti.Questa classe implementa l'interfaccia <xref:System.ServiceModel.Dispatcher.IInstanceProvider> per interagire con il livello del modello di servizio.Quando l'EndpointDispatcher chiama il metodo <xref:System.ServiceModel.Dispatcher.IInstanceProvider.GetInstance%2A>, anziché creare una nuova istanza, l'implementazione personalizzata cerca un oggetto esistente in un pool in memoria.che viene restituito se disponibile.In caso contrario, `ObjectPoolInstanceProvider` controlla se la proprietà `ActiveObjectsCount` \(numero di oggetti restituito dal pool\) ha raggiunto la dimensione massima del pool.In caso contrario, una nuova istanza viene creata e restituita al chiamante, quindi `ActiveObjectsCount` viene incrementato.Diversamente, una richiesta di creazione di un oggetto viene accodata per un periodo di tempo configurato.Nell'esempio di codice seguente viene illustrata l'implementazione di `GetObjectFromThePool`.  
  
```  
  
private object GetObjectFromThePool()  
{  
    bool didNotTimeout =   
       availableCount.WaitOne(creationTimeout, true);  
    if(didNotTimeout)  
    {  
         object obj = null;  
         lock (poolLock)  
        {  
             if (pool.Count != 0)  
             {  
                   obj = pool.Pop();  
                   activeObjectsCount++;  
             }  
             else if (pool.Count == 0)  
             {  
                   if (activeObjectsCount < maxPoolSize)  
                   {  
                        obj = CreateNewPoolObject();  
                        activeObjectsCount++;  
  
                        #if (DEBUG)  
                        WritePoolMessage(  
                             ResourceHelper.GetString("MsgNewObject"));  
                       #endif  
                   }                          
            }  
           idleTimer.Stop();  
      }  
     // Call the Activate method if possible.  
    if (obj is IObjectControl)  
   {  
         ((IObjectControl)obj).Activate();  
   }  
   return obj;  
}  
throw new TimeoutException(  
ResourceHelper.GetString("ExObjectCreationTimeout"));  
}  
```  
  
 L'implementazione personalizzata di `ReleaseInstance` aggiunge l'istanza rilasciata nuovamente al pool e decrementa il valore di `ActiveObjectsCount`.L'EndpointDispatcher può chiamare questi metodi da thread diversi e pertanto è necessario l'accesso sincronizzato ai membri del livello della classe nella classe `ObjectPoolInstanceProvider`.  
  
```  
public void ReleaseInstance(InstanceContext instanceContext, object instance)  
{  
    lock (poolLock)  
    {  
        // Check whether the object can be pooled.   
        // Call the Deactivate method if possible.  
        if (instance is IObjectControl)  
        {  
            IObjectControl objectControl = (IObjectControl)instance;  
            objectControl.Deactivate();  
  
            if (objectControl.CanBePooled)  
            {  
                pool.Push(instance);  
  
                #if(DEBUG)  
                WritePoolMessage(  
                    ResourceHelper.GetString("MsgObjectPooled"));  
                #endif                          
            }  
            else  
            {  
                #if(DEBUG)  
                WritePoolMessage(  
                    ResourceHelper.GetString("MsgObjectWasNotPooled"));  
                #endif  
            }  
        }  
        else  
        {  
            pool.Push(instance);  
  
            #if(DEBUG)  
            WritePoolMessage(  
                ResourceHelper.GetString("MsgObjectPooled"));  
            #endif   
        }  
  
        activeObjectsCount--;  
  
        if (activeObjectsCount == 0)  
        {  
            idleTimer.Start();                       
        }  
    }  
  
    availableCount.Release(1);  
}  
  
```  
  
 Il metodo `ReleaseInstance` fornisce una funzionalità di *inizializzazione di pulizia*.Normalmente il pool gestisce un numero minimo di oggetti per la durata del pool.Ci possono essere, tuttavia, periodi di utilizzo eccessivo che richiedono la creazione di oggetti aggiuntivi nel pool per raggiungere il limite massimo specificato nella configurazione.Successivamente, quando il pool diviene meno attivo, gli oggetti in eccesso possono divenire un sovraccarico aggiuntivo.Pertanto, quando il conteggio `activeObjectsCount` si azzera, viene avviato un timer, precedentemente inattivo, che inizia ed esegue un ciclo di pulizia.  
  
```  
if (activeObjectsCount == 0)  
{  
    idleTimer.Start();   
}  
  
```  
  
 Le estensioni del livello ServiceModel vengono collegate utilizzando i comportamenti seguenti:  
  
-   Comportamenti del servizio: consentono la personalizzazione del runtime dell'intero servizio.  
  
-   Comportamenti dell'endpoint: consentono la personalizzazione di un particolare endpoint del servizio, incluso EndpointDispatcher.  
  
-   Comportamenti del contratto: consentono la personalizzazione delle classi <xref:System.ServiceModel.Dispatcher.ClientRuntime> o <xref:System.ServiceModel.Dispatcher.DispatchRuntime> rispettivamente sul client o sul servizio.  
  
-   Comportamenti dell'operazione: consentono la personalizzazione delle classi <xref:System.ServiceModel.Dispatcher.ClientOperation> o <xref:System.ServiceModel.Dispatcher.DispatchOperation> rispettivamente sul client o sul servizio.  
  
 Allo scopo di estendere il pool di oggetti, è possibile creare un comportamento dell'endpoint o del servizio.In questo esempio viene utilizzato un comportamento del servizio che applica la possibilità di creare pool di oggetti a ogni endpoint del servizio.I comportamenti del servizio vengono creati implementando l'interfaccia <xref:System.ServiceModel.Description.IServiceBehavior>.Ci sono molti modi per indicare a ServiceModel i comportamenti personalizzati:  
  
-   Utilizzo di un attributo personalizzato.  
  
-   Aggiunto imperativamente alla raccolta di comportamenti della descrizione del servizio.  
  
-   Estensione dei file di configurazione  
  
 Questo esempio utilizza un attributo personalizzato.Quando la classe <xref:System.ServiceModel.ServiceHost> viene costruita, essa esamina gli attributi utilizzati nella definizione del tipo del servizio e aggiunge i comportamenti disponibili alla raccolta di comportamenti della descrizione del servizio.  
  
 L'interfaccia <xref:System.ServiceModel.Description.IServiceBehavior> dispone di tre metodi: <xref:System.ServiceModel.Description.IServiceBehavior.Validate%2A>`,` <xref:System.ServiceModel.Description.IServiceBehavior.AddBindingParameters%2A>`,` e <xref:System.ServiceModel.Description.IServiceBehavior.ApplyDispatchBehavior%2A>.Questi metodi vengono chiamati da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] quando l'oggetto <xref:System.ServiceModel.ServiceHost> viene inizializzato.Viene chiamato prima <xref:System.ServiceModel.Description.IServiceBehavior.Validate%2A?displayProperty=fullName>, che consente di controllare il servizio per eventuali incoerenze.Successivamente viene chiamato <xref:System.ServiceModel.Description.IServiceBehavior.AddBindingParameters%2A?displayProperty=fullName>, che è necessario solo in scenari molto avanzati.<xref:System.ServiceModel.Description.IServiceBehavior.ApplyDispatchBehavior%2A?displayProperty=fullName> viene chiamato per ultimo ed è responsabile per la configurazione del runtime.I parametri seguenti vengono passati in <xref:System.ServiceModel.Description.IServiceBehavior.ApplyDispatchBehavior%2A?displayProperty=fullName>:  
  
-   `Description`: questo parametro fornisce la descrizione del servizio per l'intero servizio.Può essere utilizzato per controllare dati della descrizione sugli endpoint del servizio, contratti, associazioni e altri dati associati al servizio.  
  
-   `ServiceHostBase`: questo parametro fornisce la classe <xref:System.ServiceModel.ServiceHostBase> che si sta attualmente inizializzando.  
  
 Nell'implementazione personalizzata <xref:System.ServiceModel.Description.IServiceBehavior> viene creata una nuova istanza di `ObjectPoolInstanceProvider` e viene assegnata alla proprietà <xref:System.ServiceModel.Dispatcher.DispatchRuntime.InstanceProvider%2A> in ogni <xref:System.ServiceModel.Dispatcher.EndpointDispatcher> associato a <xref:System.ServiceModel.ServiceHostBase>.  
  
```  
public void ApplyDispatchBehavior(ServiceDescription description, ServiceHostBase serviceHostBase)  
{  
    if (enabled)  
    {  
        // Create an instance of the ObjectPoolInstanceProvider.  
        instanceProvider = new ObjectPoolInstanceProvider(description.ServiceType,  
        maxPoolSize, minPoolSize, creationTimeout);  
  
        // Assign our instance provider to Dispatch behavior in each   
        // endpoint.  
        foreach (ChannelDispatcherBase cdb in serviceHostBase.ChannelDispatchers)  
        {  
             ChannelDispatcher cd = cdb as ChannelDispatcher;  
             if (cd != null)  
             {  
                 foreach (EndpointDispatcher ed in cd.Endpoints)  
                 {  
                        ed.DispatchRuntime.InstanceProvider = instanceProvider;  
                 }  
             }  
         }  
     }  
}   
```  
  
 Oltre a un'implementazione della classe <xref:System.ServiceModel.Description.IServiceBehavior>, la classe `ObjectPoolingAttribute` ha molti membri per personalizzare il pool di oggetti utilizzando gli argomenti dell'attributo.Questi membri includono `MaxSize`, `MinSize`, `Enabled` e `CreationTimeout`, per corrispondere al set di funzionalità del pool di oggetti fornito da .NET Enterprise Services.  
  
 Il comportamento del pool di oggetti può ora essere aggiunto a un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] annotando l'implementazione del servizio con l'attributo `ObjectPooling` personalizzato appena creato.  
  
```  
[ObjectPooling(MaxSize=1024, MinSize=10, CreationTimeout=30000]      
public class PoolService : IPoolService  
{  
  // …  
}  
```  
  
## Attivazione e disattivazione del collegamento  
 L'obiettivo principale del pool di oggetti è ottimizzare gli oggetti di breve durata con operazioni di creazione e inizializzazione relativamente dispendiose.Se utilizzato correttamente, può pertanto migliorare notevolmente le prestazioni di un'applicazione.Poiché l'oggetto viene restituito dal pool, il costruttore viene chiamato una sola volta.Tuttavia, alcune applicazioni richiedono un certo livello di controllo in modo da poter inizializzare e pulire le risorse utilizzate durante un solo contesto.Ad esempio, un oggetto utilizzato per una serie di calcoli può reimpostare i relativi campi privati prima di elaborare il calcolo successivo.Enterprise Services abilita questo tipo di inizializzazione specifica del contesto consentendo allo sviluppatore degli oggetti di eseguire l'override dei metodi `Activate` e `Deactivate` dalla classe di base <xref:System.EnterpriseServices.ServicedComponent>.  
  
 Il pool di oggetti chiama il metodo `Activate` poco prima di restituire l'oggetto dal pool.`Deactivate` viene chiamato quando l'oggetto viene restituito di nuovo al pool.La classe di base <xref:System.EnterpriseServices.ServicedComponent> dispone anche di una proprietà `boolean` denominata `CanBePooled`, che può essere utilizzata per notificare al pool se l'oggetto può essere ulteriormente inserito nel pool.  
  
 Per riprodurre questa funzionalità, nell'esempio viene dichiarata un'interfaccia pubblica \(`IObjectControl`\) che dispone dei membri menzionati.Questa interfaccia viene quindi implementata dalle classi del servizio destinate a fornire l'inizializzazione specifica del contesto.L'implementazione <xref:System.ServiceModel.Dispatcher.IInstanceProvider> deve essere modificata per soddisfare questi requisiti.Ogni volta che si ottiene un oggetto chiamando il metodo `GetInstance`, è necessario controllare se l'oggetto implementa `IObjectControl.` In tal caso, è necessario chiamare il metodo `Activate`.  
  
```  
if (obj is IObjectControl)  
{  
    ((IObjectControl)obj).Activate();  
}  
  
```  
  
 Quando si restituisce un oggetto al pool, è necessario controllare la proprietà `CanBePooled` prima di aggiungere di nuovo l'oggetto al pool.  
  
```  
if (instance is IObjectControl)  
{  
    IObjectControl objectControl = (IObjectControl)instance;  
    objectControl.Deactivate();  
    if (objectControl.CanBePooled)  
    {  
       pool.Push(instance);  
    }  
}  
  
```  
  
 Poiché lo sviluppatore del servizio può decidere se un oggetto può essere inserito in un pool, il conteggio degli oggetti nel pool in un determinato momento può essere inferiore alla dimensione minima.È pertanto necessario controllare se il conteggio degli oggetti è inferiore al livello minimo ed eseguire l'inizializzazione necessaria nella procedura di pulizia.  
  
```  
// Remove the surplus objects.  
if (pool.Count > minPoolSize)  
{  
  // Clean the surplus objects.  
}                      
else if (pool.Count < minPoolSize)  
{  
  // Reinitialize the missing objects.  
  while(pool.Count != minPoolSize)  
  {  
    pool.Push(CreateNewPoolObject());  
  }  
}  
```  
  
 Quando si esegue l'esempio, le richieste e le risposte dell'operazione vengono visualizzate nelle finestre della console client e del servizio.Premere INVIO in tutte le finestre della console per arrestare il servizio e il client.  
  
#### Per impostare, compilare ed eseguire l'esempio  
  
1.  Verificare di avere eseguito [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare la soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Per eseguire l'esempio in una configurazione con un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Extensibility\Instancing\Initialization`  
  
## Vedere anche