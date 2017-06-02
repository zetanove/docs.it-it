---
title: "Sessioni, istanze e concorrenza | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 50797a3b-7678-44ed-8138-49ac1602f35b
caps.latest.revision: 16
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 16
---
# Sessioni, istanze e concorrenza
Una *sessione* è una correlazione di tutti i messaggi inviati tra due endpoint. La *creazione di istanze* fa riferimento al controllo della durata di oggetti servizio definiti dall'utente e di oggetti <xref:System.ServiceModel.InstanceContext> correlati. La *concorrenza* è il termine dato al controllo del numero di thread in esecuzione contemporaneamente in un <xref:System.ServiceModel.InstanceContext>.  
  
 In questo argomento vengono descritte tali impostazioni, come utilizzarle e le varie interazioni tra di esse.  
  
## Sessions  
 Quando la proprietà <xref:System.ServiceModel.ServiceContractAttribute.SessionMode%2A?displayProperty=fullName> viene impostata da un contratto di servizio su <xref:System.ServiceModel.SessionMode?displayProperty=fullName>, tutte le chiamate, ovvero gli scambi di messaggi sottostanti che supportano le chiamate, devono essere parte della stessa conversazione. Se un contratto consente sessioni ma non ne richiede, i client possono connettersi e possono stabilire o meno una sessione. Se, al termine della sessione, un messaggio viene inviato sullo stesso canale basato sulla sessione, viene generata un'eccezione.  
  
 Le principali caratteristiche delle sessioni [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] sono le seguenti:  
  
-   Vengono avviate e terminate esplicitamente dall'applicazione chiamante.  
  
-   I messaggi recapitati durante una sessione vengono elaborati nell'ordine in cui vengono ricevuti.  
  
-   Le sessioni consentono di correlare un gruppo di messaggi in una conversazione. Il significato di tale correlazione è un'astrazione. Un canale basato sulla sessione, ad esempio, è in grado di correlare messaggi basati su una connessione di rete condivisa mentre un altro canale basato sulla sessione è in grado di correlare messaggi basati su un tag condiviso nel corpo del messaggio. Le funzionalità che possono derivare dalla sessione dipendono dalla natura della correlazione.  
  
-   Non esiste alcun archivio dati generale associato a una sessione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
 Se si ha familiarità con la classe <xref:System.Web.SessionState.HttpSessionState?displayProperty=fullName> in applicazioni [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] e con la funzionalità fornita, è possibile notare le differenze seguenti tra quel tipo di sessioni e le sessioni [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]:  
  
-   Le sessioni [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] sono sempre avviate dal server.  
  
-   Le sessioni [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] sono implicitamente non ordinate.  
  
-   Le sessioni [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] forniscono un meccanismo di archiviazione dati generale tramite richieste.  
  
 Le applicazioni client e le applicazioni di servizio interagiscono con le sessioni in modi diversi. Le applicazioni client avviano sessioni e quindi ricevono ed elaborano i messaggi inviati all'interno della sessione. Le applicazioni di servizio possono utilizzare le sessioni come punto di estensibilità per aggiungere comportamenti. Ciò si ottiene utilizzando direttamente <xref:System.ServiceModel.InstanceContext> o implementando un provider di contesto dell'istanza personalizzato.  
  
## Istanze  
 Il comportamento delle istanze \(impostato tramite la proprietà <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A?displayProperty=fullName> \) consente di controllare come viene creato <xref:System.ServiceModel.InstanceContext> in risposta ai messaggi in ingresso. Per impostazione predefinita, ogni <xref:System.ServiceModel.InstanceContext> viene associato a uno oggetto servizio definito dall'utente. In questo modo l'impostazione \(nel caso predefinito\) della proprietà <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A> consente di controllare anche le istanze di oggetti servizio definiti dall'utente. L'enumerazione <xref:System.ServiceModel.InstanceContextMode> definisce le modalità di istanza.  
  
 Sono disponibili le modalità di istanza seguenti:  
  
-   <xref:System.ServiceModel.InstanceContextMode>: viene creato un nuovo <xref:System.ServiceModel.InstanceContext> \(e di conseguenza l'oggetto servizio\) per ogni richiesta client.  
  
-   <xref:System.ServiceModel.InstanceContextMode>: viene creato un nuovo <xref:System.ServiceModel.InstanceContext> \(e di conseguenza l'oggetto servizio\) per ogni sessione client nuova e viene mantenuto per la durata di quella sessione \(è necessaria un'associazione che supporti sessioni\).  
  
-   <xref:System.ServiceModel.InstanceContextMode>: un unico <xref:System.ServiceModel.InstanceContext> \(e di conseguenza l'oggetto servizio\) gestisce tutte le richieste client per la durata dell'applicazione.  
  
 Nell'esempio di codice seguente viene illustrato il valore <xref:System.ServiceModel.InstanceContextMode> predefinito, con <xref:System.ServiceModel.InstanceContextMode> impostato esplicitamente su una classe del servizio.  
  
```  
[ServiceBehavior(InstanceContextMode=InstanceContextMode.PerSession)]   
public class CalculatorService : ICalculatorInstance   
{   
    ...  
}  
```  
  
 Mentre la proprietà <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A?displayProperty=fullName> consente di controllare la frequenza di rilascio di <xref:System.ServiceModel.InstanceContext>, le proprietà <xref:System.ServiceModel.OperationBehaviorAttribute.ReleaseInstanceMode%2A?displayProperty=fullName> e <xref:System.ServiceModel.ServiceBehaviorAttribute.ReleaseServiceInstanceOnTransactionComplete%2A?displayProperty=fullName> consentono di controllare quando l'oggetto servizio viene rilasciato.  
  
### Servizi Singleton noti  
 Una variazione su oggetti servizio di una singola istanza può a volte essere utile. È infatti possibile creare un oggetto servizio e quindi creare l'host del servizio tramite quell'oggetto. A tale scopo, è necessario impostare la proprietà <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A?displayProperty=fullName> su <xref:System.ServiceModel.InstanceContextMode>, in caso contrario verrà generata un'eccezione quando l'host del servizio viene aperto.  
  
 Utilizzare il costruttore [ServiceHost.ServiceHost\(Object, Uri\<xref:System.ServiceModel.ServiceHost.%23ctor%28System.Object%2CSystem.Uri%5B%5D%29?displayProperty=fullName> per creare tale servizio. Fornisce un'alternativa all'implementazione di un'interfaccia <xref:System.ServiceModel.Dispatcher.IInstanceContextInitializer?displayProperty=fullName> personalizzata quando si desidera fornire un'istanza specifica dell'oggetto utilizzabile da un servizio singleton. Questo overload può risultare utile quando il tipo di implementazione del servizio è di difficile costruzione, ad esempio se non implementa alcun costruttore pubblico predefinito privo di parametri.  
  
 Si noti che quando un oggetto viene fornito a questo costruttore, alcune funzionalità relative al comportamento di creazione delle istanze [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] operano in modo diverso. La chiamata, ad esempio, di <xref:System.ServiceModel.InstanceContext.ReleaseServiceInstance%2A?displayProperty=fullName> non ha effetto quando viene fornita l'istanza di un oggetto Singleton. Analogamente, qualsiasi altro meccanismo di rilascio delle istanze viene ignorato. L'host <xref:System.ServiceModel.ServiceHost> si comporta sempre come se la proprietà <xref:System.ServiceModel.OperationBehaviorAttribute.ReleaseInstanceMode%2A?displayProperty=fullName> fosse impostata su <xref:System.ServiceModel.ReleaseInstanceMode?displayProperty=fullName> per tutte le operazioni.  
  
### Condivisione di oggetti InstanceContext  
 È inoltre possibile controllare l'associazione tra canali o chiamate con sessione e oggetti <xref:System.ServiceModel.InstanceContext> eseguendo quell'associazione.  
  
## Concorrenza  
 La concorrenza è il controllo del numero di thread attivi in un <xref:System.ServiceModel.InstanceContext> contemporaneamente. Viene controllato tramite <xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A?displayProperty=fullName> con l'enumerazione <xref:System.ServiceModel.ConcurrencyMode>.  
  
 Sono disponibili le tre modalità di concorrenza seguenti:  
  
-   <xref:System.ServiceModel.ConcurrencyMode>: ogni contesto dell'istanza può avere al massimo un thread alla volta per l'elaborazione dei messaggi nel contesto dell'istanza. Altri thread che devono utilizzare lo stesso contesto dell'istanza, devono restare bloccati fino alla chiusura del thread originale dal contesto dell'istanza.  
  
-   <xref:System.ServiceModel.ConcurrencyMode>: ogni istanza del servizio può avere contemporaneamente più thread per l'elaborazione messaggi. Per essere in grado di usare questa modalità di concorrenza, l'implementazione del servizio deve essere thread\-safe.  
  
-   <xref:System.ServiceModel.ConcurrencyMode>: ogni istanza del servizio elabora un messaggio alla volta ma accetta chiamate di operazioni rientranti. Il servizio accetta queste chiamate solo quando è in corso una chiamata in uscita tramite un oggetto client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
> [!NOTE]
>  Può essere difficile comprendere, scrivere correttamente e sviluppare codice che utilizza in modo sicuro più di un thread. Prima di utilizzare valori <xref:System.ServiceModel.ConcurrencyMode> o <xref:System.ServiceModel.ConcurrencyMode>, verificare che il servizio sia progettato correttamente per queste modalità.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] <xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A>.  
  
 L'uso della concorrenza è correlato alla modalità di istanza. Nelle istanze <xref:System.ServiceModel.InstanceContextMode>`` la concorrenza non è rilevante, perché ogni messaggio viene elaborato da un nuovo <xref:System.ServiceModel.InstanceContext> e, di conseguenza, non è mai attivo più di un singolo thread in <xref:System.ServiceModel.InstanceContext>.  
  
 Nell'esempio di codice seguente viene illustrata l'impostazione della proprietà <xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A> su <xref:System.ServiceModel.ConcurrencyMode>.  
  
```  
[ServiceBehavior(ConcurrencyMode=ConcurrencyMode.Multiple, InstanceContextMode = InstanceContextMode.Single)]   
public class CalculatorService : ICalculatorConcurrency   
{   
    ...  
}  
  
```  
  
## Sessioni che interagiscono con impostazioni InstanceContext  
 L'interazione di sessioni e di <xref:System.ServiceModel.InstanceContext>, che dipendono dalla combinazione tra il valore dell'enumerazione <xref:System.ServiceModel.SessionMode> in un contratto e la proprietà <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A?displayProperty=fullName> nell'implementazione del servizio, consente di controllare l'associazione tra canali e oggetti servizio specifici.  
  
 Nella tabella seguente viene mostrato il risultato di un canale in ingresso in cui le sessioni sono supportate o non supportate. Tale risultato è in funzione della combinazione dei valori delle proprietà <xref:System.ServiceModel.ServiceContractAttribute.SessionMode%2A?displayProperty=fullName> e <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A?displayProperty=fullName> del servizio.  
  
|Valore InstanceContextMode|<xref:System.ServiceModel.SessionMode>|<xref:System.ServiceModel.SessionMode>|<xref:System.ServiceModel.SessionMode>|  
|--------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------|  
|PerCall|-   Comportamento in caso di canale con sessione: una sessione e un contesto <xref:System.ServiceModel.InstanceContext> per ogni chiamata.<br />-   Comportamento in caso di canale senza sessione: viene generata un'eccezione.|-   Comportamento in caso di canale con sessione: una sessione e un contesto <xref:System.ServiceModel.InstanceContext> per ogni chiamata.<br />-   Comportamento in caso di canale senza sessione: un contesto <xref:System.ServiceModel.InstanceContext> per ogni chiamata.|-   Comportamento in caso di canale con sessione: viene generata un'eccezione.<br />-   Comportamento in caso di canale senza sessione: un contesto <xref:System.ServiceModel.InstanceContext> per ogni chiamata.|  
|PerSession|-   Comportamento in caso di canale con sessione: una sessione e un contesto <xref:System.ServiceModel.InstanceContext> per ogni canale.<br />-   Comportamento in caso di canale senza sessione: viene generata un'eccezione.|-   Comportamento in caso di canale con sessione: una sessione e un contesto <xref:System.ServiceModel.InstanceContext> per ogni canale.<br />-   Comportamento in caso di canale senza sessione: un contesto <xref:System.ServiceModel.InstanceContext> per ogni chiamata.|-   Comportamento in caso di canale con sessione: viene generata un'eccezione.<br />-   Comportamento in caso di canale senza sessione: un contesto <xref:System.ServiceModel.InstanceContext> per ogni chiamata.|  
|Single|-   Comportamento in caso di canale con sessione: un'unica sessione e un solo <xref:System.ServiceModel.InstanceContext> per tutte le chiamate.<br />-   Comportamento in caso di canale senza sessione: viene generata un'eccezione.|-   Comportamento in caso di canale con sessione: una sessione e un <xref:System.ServiceModel.InstanceContext> per il singleton creato o per il singleton specificato dall'utente.<br />-   Comportamento in caso di canale senza sessione: un <xref:System.ServiceModel.InstanceContext> per il singleton creato o per il singleton specificato dall'utente.|-   Comportamento in caso di canale con sessione: viene generata un'eccezione.<br />-   Comportamento in caso di canale senza sessione: un contesto <xref:System.ServiceModel.InstanceContext> per ogni singleton creato o per il singleton specificato dall'utente.|  
  
## Vedere anche  
 [Uso di sessioni](../../../../docs/framework/wcf/using-sessions.md)   
 [Procedura: creare un servizio che richiede sessioni](../../../../docs/framework/wcf/feature-details/how-to-create-a-service-that-requires-sessions.md)   
 [Procedura: controllare l'istanza del servizio](../../../../docs/framework/wcf/feature-details/how-to-control-service-instancing.md)   
 [Concorrenza](../../../../docs/framework/wcf/samples/concurrency.md)   
 [Istanze](../../../../docs/framework/wcf/samples/instancing.md)   
 [Sessione](../../../../docs/framework/wcf/samples/session.md)