---
title: "Pooling | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 688dfb30-b79a-4cad-a687-8302f8a9ad6a
caps.latest.revision: 29
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 29
---
# Pooling
In questo esempio viene illustrato come estendere [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] per supportare i pool di oggetti.L'esempio illustra come creare un attributo sintatticamente e semanticamente simile alla funzionalità dell'attributo `ObjectPoolingAttribute` di Enterprise Services.Il pool degli oggetti può fornire una spinta notevole alle prestazioni di un'applicazione.Tuttavia, può avere l'effetto contrario se non utilizzato correttamente.Il pool degli oggetti consente di ridurre il sovraccarico dovuto alla creazione continua di oggetti frequentemente utilizzati che richiedono un'inizializzazione estesa.Tuttavia, se una chiamata a un metodo su un oggetto del pool richiede una quantità considerevole di tempo, il pool degli oggetti mette in coda richieste aggiuntive appena viene raggiunta la dimensione del pool massima.Pertanto può non riuscire a soddisfare richieste di creazione di oggetti generando un'eccezione di timeout.  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine dell'argomento.  
  
 Il primo passaggio nel creare un'estensione di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] è decidere il punto di estensibilità da utilizzare.  
  
 In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] il termine *dispatcher* fa riferimento a un componente runtime responsabile della conversione dei messaggi in arrivo in chiamate al metodo sul servizio dell'utente e della conversione di valori restituiti da quel metodo in un messaggio in uscita.Un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] crea un dispatcher per ogni endpoint.Un client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] deve utilizzare un dispatcher se il contratto associato a quel client è un contratto duplex.  
  
 I dispatcher del canale e dell'endpoint offrono estensibilità sul canale e sul contratto esponendo le varie proprietà che controllano il comportamento del dispatcher.La proprietà <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.DispatchRuntime%2A> consente inoltre di ispezionare, modificare e personalizzare la modalità di autenticazione dei certificati.Questo esempio si concentra sulla proprietà <xref:System.ServiceModel.Dispatcher.DispatchRuntime.InstanceProvider%2A> che punta all'oggetto che fornisce le istanze della classe del servizio.  
  
## Provider di istanze  
 In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], il dispatcher crea istanze della classe del servizio utilizzando una proprietà <xref:System.ServiceModel.Dispatcher.DispatchRuntime.InstanceProvider%2A>, che implementa l'interfaccia <xref:System.ServiceModel.Dispatcher.IInstanceProvider>.Questa interfaccia ha tre metodi:  
  
-   <xref:System.ServiceModel.Dispatcher.IInstanceProvider.GetInstance%28System.ServiceModel.InstanceContext%2CSystem.ServiceModel.Channels.Message%29>: quando un messaggio arriva il dispatcher chiama il metodo <xref:System.ServiceModel.Dispatcher.IInstanceProvider.GetInstance%28System.ServiceModel.InstanceContext%2CSystem.ServiceModel.Channels.Message%29> per creare un'istanza della classe del servizio al fine di elaborare il messaggio.La frequenza delle chiamate a questo metodo è determinata dalla proprietà <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A>.Ad esempio, se la proprietà <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A> è impostata su <xref:System.ServiceModel.InstanceContextMode> viene creata una nuova istanza della classe del servizio per elaborare ogni messaggio che arriva, pertanto il metodo <xref:System.ServiceModel.Dispatcher.IInstanceProvider.GetInstance%28System.ServiceModel.InstanceContext%2CSystem.ServiceModel.Channels.Message%29> viene chiamato ogni qualvolta arriva un messaggio.  
  
-   <xref:System.ServiceModel.Dispatcher.IInstanceProvider.GetInstance%28System.ServiceModel.InstanceContext%29>: questo metodo è identico a quello precedente, salvo che viene richiamato quando non c'è nessun argomento di messaggio.  
  
-   <xref:System.ServiceModel.Dispatcher.IInstanceProvider.ReleaseInstance%28System.ServiceModel.InstanceContext%2CSystem.Object%29>: Quando la durata di un'istanza del servizio è scaduta, il dispatcher chiama il metodo <xref:System.ServiceModel.Dispatcher.IInstanceProvider.ReleaseInstance%28System.ServiceModel.InstanceContext%2CSystem.Object%29>.Solo per il metodo <xref:System.ServiceModel.Dispatcher.IInstanceProvider.GetInstance%28System.ServiceModel.InstanceContext%2CSystem.ServiceModel.Channels.Message%29>, la frequenza delle chiamate a questo metodo è determinata dalla proprietà <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A>.  
  
## Pool di oggetti  
 Un'implementazione personalizzata della classe <xref:System.ServiceModel.Dispatcher.IInstanceProvider> fornisce la semantica del pool di oggetti necessaria per un servizio.Pertanto, questo esempio ha un tipo `ObjectPoolingInstanceProvider` che fornisce un'implementazione personalizzata della classe <xref:System.ServiceModel.Dispatcher.IInstanceProvider> per il pool.Quando `Dispatcher` chiama il metodo <xref:System.ServiceModel.Dispatcher.IInstanceProvider.GetInstance%28System.ServiceModel.InstanceContext%2CSystem.ServiceModel.Channels.Message%29>, anziché creare una nuova istanza, l'implementazione personalizzata cerca un oggetto esistente in un pool in memoriache viene restituito se disponibile.In caso contrario, viene creato un nuovo oggetto.Nell'esempio di codice seguente viene illustrata l'implementazione di `GetInstance`.  
  
```  
object IInstanceProvider.GetInstance(InstanceContext instanceContext, Message message)  
{  
    object obj = null;  
  
    lock (poolLock)  
    {  
        if (pool.Count > 0)  
        {  
            obj = pool.Pop();  
        }  
        else  
        {  
            obj = CreateNewPoolObject();  
        }  
        activeObjectsCount++;  
    }  
  
    WritePoolMessage(ResourceHelper.GetString("MsgNewObject"));  
  
    idleTimer.Stop();  
  
    return obj;            
}  
  
```  
  
 L'implementazione personalizzata di `ReleaseInstance` aggiunge l'istanza rilasciata nuovamente al pool e decrementa il valore di `ActiveObjectsCount`.Il `Dispatcher` può chiamare questi metodi da thread diversi e pertanto sincronizzare l'accesso ai membri del livello della classe, nella classe `ObjectPoolingInstanceProvider` obbligatoria.  
  
```  
void IInstanceProvider.ReleaseInstance(InstanceContext instanceContext, object instance)  
{  
    lock (poolLock)  
    {  
        pool.Push(instance);  
        activeObjectsCount--;  
  
        WritePoolMessage(  
        ResourceHelper.GetString("MsgObjectPooled"));  
  
        // When the service goes completely idle (no requests   
        // are being processed), the idle timer is started  
        if (activeObjectsCount == 0)  
            idleTimer.Start();                       
    }  
}  
  
```  
  
 Il metodo `ReleaseInstance` fornisce una funzionalità di "inizializzazione di pulizia".Normalmente il pool gestisce un numero minimo di oggetti per la durata del pool.Ci possono essere, tuttavia, periodi di utilizzo eccessivo che richiedono la creazione di oggetti aggiuntivi nel pool per raggiungere il limite massimo specificato nella configurazione.Successivamente, quando il pool diviene meno attivo, quegli oggetti in surplus possono divenire un sovraccarico aggiuntivo.Pertanto, quando il conteggio `activeObjectsCount` si azzera, viene avviato un timer, precedentemente inattivo, che inizia ed esegue un ciclo di pulizia.  
  
## Aggiunta del comportamento.  
 Le estensioni del livello del dispatcher vengono collegate utilizzando i comportamenti seguenti:  
  
-   Comportamenti del servizio.Essi consentono la personalizzazione del runtime dell'intero servizio.  
  
-   Comportamenti dell'endpoint.Essi consentono la personalizzazione degli endpoint del servizio, in particolare un canale e un dispatcher dell'endpoint.  
  
-   Comportamenti del contratto.Essi consentono la personalizzazione di entrambe le classi <xref:System.ServiceModel.Dispatcher.ClientRuntime> e <xref:System.ServiceModel.Dispatcher.DispatchRuntime> rispettivamente sul client e sui servizi.  
  
 Allo scopo di un'estensione del pool di oggetti deve essere creato un comportamento del servizio.I comportamenti del servizio vengono creati implementando l'interfaccia <xref:System.ServiceModel.Description.IServiceBehavior>.Ci sono molti modi per rendere consapevole il modello dei servizi dei comportamenti personalizzati:  
  
-   Utilizzo di un attributo personalizzato.  
  
-   Aggiunto imperativamente alla raccolta di comportamenti della descrizione del servizio.  
  
-   Estensione dei file di configurazione  
  
 Questo esempio utilizza un attributo personalizzato.Quando la classe <xref:System.ServiceModel.ServiceHost> viene costruita esamina gli attributi utilizzati nella definizione del tipo del servizio e aggiunge i comportamenti disponibili alla raccolta di comportamenti della descrizione del servizio.  
  
 L'interfaccia <xref:System.ServiceModel.Description.IServiceBehavior> contiene tre metodi: <xref:System.ServiceModel.Description.IServiceBehavior.Validate%2A>, <xref:System.ServiceModel.Description.IServiceBehavior.AddBindingParameters%2A> e <xref:System.ServiceModel.Description.IServiceBehavior.ApplyDispatchBehavior%2A>.Il metodo <xref:System.ServiceModel.Description.IServiceBehavior.Validate%2A> viene utilizzato per assicurare che il comportamento possa essere applicato al servizio.In questo esempio, l'implementazione assicura che il servizio non sia configurato con <xref:System.ServiceModel.InstanceContextMode>.Il metodo <xref:System.ServiceModel.Description.IServiceBehavior.AddBindingParameters%2A> viene utilizzato per configurare le associazioni del servizio.Non è obbligatorio in questo scenario.Il metodo <xref:System.ServiceModel.Description.IServiceBehavior.ApplyDispatchBehavior%2A> viene utilizzato per configurare i dispatcher del servizio.Questo metodo viene chiamato [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] quando viene inizializzata la classe <xref:System.ServiceModel.ServiceHost>.I parametri seguenti vengono passati in questo metodo:  
  
-   `Description`: questo argomento fornisce la descrizione del servizio per l'intero servizio.Può essere utilizzato per controllare dati della descrizione sugli endpoint del servizio, contratti, associazioni e altri dati.  
  
-   `ServiceHostBase`: questo argomento fornisce la classe <xref:System.ServiceModel.ServiceHostBase> attualmente in fase di inizializzazione.  
  
 Nell'implementazione personalizzata della classe <xref:System.ServiceModel.Description.IServiceBehavior> viene creata una nuova istanza di `ObjectPoolingInstanceProvider` e viene assegnata alla proprietà <xref:System.ServiceModel.Dispatcher.DispatchRuntime.InstanceProvider%2A> in ogni <xref:System.ServiceModel.Dispatcher.DispatchRuntime> in ServiceHostBase.  
  
```  
void IServiceBehavior.ApplyDispatchBehavior(ServiceDescription description, ServiceHostBase serviceHostBase)  
{  
    // Create an instance of the ObjectPoolInstanceProvider.  
    ObjectPoolingInstanceProvider instanceProvider = new  
           ObjectPoolingInstanceProvider(description.ServiceType,   
                                                    minPoolSize);  
  
    // Forward the call if we created a ServiceThrottlingBehavior.  
    if (this.throttlingBehavior != null)  
    {  
        ((IServiceBehavior)this.throttlingBehavior).ApplyDispatchBehavior(description, serviceHostBase);  
    }  
  
    // In case there was already a ServiceThrottlingBehavior   
    // (this.throttlingBehavior==null), it should have initialized   
    // a single ServiceThrottle on all ChannelDispatchers.    
    // As we loop through the ChannelDispatchers, we verify that   
    // and modify the ServiceThrottle to guard MaxPoolSize.  
    ServiceThrottle throttle = null;  
  
    foreach (ChannelDispatcherBase cdb in   
            serviceHostBase.ChannelDispatchers)  
    {  
        ChannelDispatcher cd = cdb as ChannelDispatcher;  
        if (cd != null)  
        {  
            // Make sure there is exactly one throttle used by all   
            // endpoints. If there were others, we could not enforce   
            // MaxPoolSize.  
            if ((this.throttlingBehavior == null) &&   
                        (this.maxPoolSize != Int32.MaxValue))  
            {  
                if (throttle == null)  
                {  
                    throttle = cd.ServiceThrottle;  
                }  
                if (cd.ServiceThrottle == null)  
                {  
                    throw new   
InvalidOperationException(ResourceHelper.GetString("ExNullThrottle"));  
                }  
                if (throttle != cd.ServiceThrottle)  
                {  
                    throw new InvalidOperationException(ResourceHelper.GetString("ExDifferentThrottle"));  
                }  
             }  
  
             foreach (EndpointDispatcher ed in cd.Endpoints)  
             {  
                 // Assign it to DispatchBehavior in each endpoint.  
                 ed.DispatchRuntime.InstanceProvider =   
                                      instanceProvider;  
             }  
         }  
     }  
  
     // Set the MaxConcurrentInstances to limit the number of items   
     // that will ever be requested from the pool.  
     if ((throttle != null) && (throttle.MaxConcurrentInstances >   
                                      this.maxPoolSize))  
     {  
         throttle.MaxConcurrentInstances = this.maxPoolSize;  
     }  
}  
```  
  
 Oltre a un'implementazione della classe <xref:System.ServiceModel.Description.IServiceBehavior>, la classe <xref:System.EnterpriseServices.ObjectPoolingAttribute> ha molti membri per personalizzare il pool di oggetti utilizzando gli argomenti dell'attributo.Questi membri includono <xref:System.EnterpriseServices.ObjectPoolingAttribute.MaxPoolSize%2A>, <xref:System.EnterpriseServices.ObjectPoolingAttribute.MinPoolSize%2A> e <xref:System.EnterpriseServices.ObjectPoolingAttribute.CreationTimeout%2A>, per corrispondere al set di funzionalità del pool di oggetti fornito da Enterprise Services .NET.  
  
 Il comportamento del pool di oggetti può ora essere aggiunto a un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] annotando l'implementazione del servizio con l'attributo `ObjectPooling` personalizzato appena creato.  
  
```  
[ObjectPooling(MaxPoolSize=1024, MinPoolSize=10, CreationTimeout=30000)]      
public class PoolService : IPoolService  
{  
  // …  
}  
```  
  
## Esecuzione dell'esempio  
 L'esempio illustra i vantaggi a livello di prestazioni che possono essere raggiunti utilizzando i pool di oggetti in alcuni scenari.  
  
 L'applicazione di servizio implementa due servizi: `WorkService` e `ObjectPooledWorkService`.Entrambi i servizi condividono la stessa implementazione. Richiedono entrambi una lunga inizializzazione e quindi espongono un metodo `DoWork()` che è relativamente conveniente.La sola differenza è che `ObjectPooledWorkService` ha un pool di oggetti configurato:  
  
```  
[ObjectPooling(MinPoolSize = 0, MaxPoolSize = 5)]  
public class ObjectPooledWorkService : IDoWork  
{  
    public ObjectPooledWorkService()  
    {  
        Thread.Sleep(5000);  
        ColorConsole.WriteLine(ConsoleColor.Blue, "ObjectPooledWorkService instance created.");  
    }  
  
    public void DoWork()  
    {  
        ColorConsole.WriteLine(ConsoleColor.Blue, "ObjectPooledWorkService.GetData() completed.");  
    }          
}  
```  
  
 Quando si esegue il client, effettua la chiamata a `WorkService` 5 volte.Quindi effettua la chiamata a `ObjectPooledWorkService` 5 volte.Viene infine visualizzata la differenza:  
  
```  
Press <ENTER> to start the client.  
  
Calling WorkService:  
1 - DoWork() Done  
2 - DoWork() Done  
3 - DoWork() Done  
4 - DoWork() Done  
5 - DoWork() Done  
Calling WorkService took: 26722 ms.  
Calling ObjectPooledWorkService:  
1 - DoWork() Done  
2 - DoWork() Done  
3 - DoWork() Done  
4 - DoWork() Done  
5 - DoWork() Done  
Calling ObjectPooledWorkService took: 5323 ms.  
Press <ENTER> to exit.  
```  
  
> [!NOTE]
>  La prima volta che il client viene eseguito, entrambi i servizi sembrano avere la stessa durata.Se si esegue nuovamente l'esempio, è possibile vedere che `ObjectPooledWorkService` restituisce molto più rapidamente perché un'istanza di quell'oggetto già esiste nel pool.  
  
#### Per impostare, compilare ed eseguire l'esempio  
  
1.  Assicurarsi di avere eseguito [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare la soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Per eseguire l'esempio su una configurazione con un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
> [!NOTE]
>  Se si utilizza Svcutil.exe per rigenerare la configurazione di questo esempio, verificare di modificare il nome dell'endpoint nella configurazione client in modo che corrisponda al codice client.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Extensibility\Instancing\Pooling`  
  
## Vedere anche