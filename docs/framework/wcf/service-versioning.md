---
title: "Controllo delle versioni del servizio | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 37575ead-d820-4a67-8059-da11a2ab48e2
caps.latest.revision: 19
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 19
---
# Controllo delle versioni del servizio
Dopo la distribuzione iniziale e, potenzialmente, più volte durante il loro ciclo di vita, potrebbe essere necessario cambiare i servizi \(e gli endpoint che espongono\) per molteplici ragioni, ad esempio perché cambiano le esigenze aziendali, i requisiti IT o per risolvere altri problemi.Ogni modifica introduce una nuova versione del servizio.In questo argomento viene illustrato come controllare la versione in [!INCLUDE[indigo1](../../../includes/indigo1-md.md)].  
  
## Quattro categorie di modifiche del servizio  
 Le modifiche richieste ai servizi possono essere classificate in quattro categorie:  
  
-   Modifiche del contratto: ad esempio, potrebbe venire aggiunta un'operazione, oppure potrebbe venire aggiunto o modificato un elemento dati in un messaggio.  
  
-   Modifiche dell'indirizzo: ad esempio, un servizio viene spostato in un percorso diverso in cui gli endpoint hanno nuovi indirizzi.  
  
-   Modifiche dell'associazione: ad esempio, cambia un meccanismo di sicurezza, oppure cambiano le sue impostazioni.  
  
-   Modifiche dell'implementazione: ad esempio, cambia l'implementazione del metodo interno.  
  
 Alcune di queste modifiche sono chiamate di "interruzione" e altre di "non di interruzione". Una modifica è di *non di interruzione* se tutti i messaggi che sarebbero stati elaborati correttamente nella versione precedente lo sono anche nella versione nuova.Qualsiasi modifica che non soddisfa questo criterio è di *interruzione*.  
  
## Orientamento del servizio e controllo delle versioni  
 Uno dei principi dell'orientamento del servizio è che servizi e client sono autonomi \(o indipendenti\).Tra le altre cose, ciò implica che gli sviluppatori del servizio non possono presupporre di controllare né conoscere tutti i client del servizio.In tal modo non si dovrà ricreare e ridistribuire tutti i client quando un servizio cambia versione.In questo argomento si presume che il servizio aderisca a questo principio e che pertanto debba essere modificato o sottoposto al controllo della versione indipendentemente dai propri client.  
  
 Nei casi in cui non sia possibile evitare una modifica imprevista che può determinare interruzioni, un'applicazione può scegliere di ignorare questo principio e richiedere che i client vengano ricreati e ridistribuiti con una nuova versione del servizio.  
  
## Controllo delle versioni dei contratti  
 I contratti utilizzati da un client non devono necessariamente essere uguali a quelli utilizzati dal servizio. È sufficiente che siano compatibili.  
  
 Per i contratti di servizio, compatibilità significa che è possibile aggiungere nuove operazioni esposte dal servizio, ma non rimuovere o modificare semanticamente le operazioni esistenti.  
  
 Per i contratti dati, compatibilità significa che è possibile aggiungere nuove definizioni del tipo di schema, ma non modificare quelle esistenti in modo tale da causare interruzioni.Le modifiche che possono determinare interruzioni potrebbero includere la rimozione di membri dati o la modifica del loro tipo di dati in modo incompatibile.Questa funzionalità consente al servizio una certa libertà di modifica della versione dei propri contratti senza interrompere i client.Nelle prossime due sezioni vengono illustrate le modifiche che non determinano interruzioni e quelle che determinano interruzioni, che è possibile apportare a contratti di servizio e a contratti dati di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].  
  
## Controllo delle versioni dei contratti dati  
 In questa sezione viene illustrato il controllo delle versioni dei dati quando si utilizzano le classi <xref:System.Runtime.Serialization.DataContractSerializer> e <xref:System.Runtime.Serialization.DataContractAttribute>.  
  
### Controllo delle versioni rigoroso  
 In numerosi scenari in cui la modifica delle versioni rappresenta un problema, lo sviluppatore del servizio non ha il controllo dei client e pertanto non può fare ipotesi su come reagirebbero alle modifiche nell'XML del messaggio o nello schema.In questi casi, è necessario garantire che i nuovi messaggi vengano convalidati rispetto al vecchio schema, per due ragioni:  
  
-   I vecchi client sono stati sviluppati presupponendo che lo schema non sarebbe cambiato.Potrebbero non riuscire a elaborare messaggi per i quali non sono mai stati progettati.  
  
-   I vecchi client potrebbero eseguire la convalida effettiva dello schema rispetto al vecchio schema ancora prima di tentare di elaborare i messaggi.  
  
 L'approccio consigliato in questi scenari è trattare i contratti dati esistenti come immutabili e creare quelli nuovi con nomi completi XML univoci.Lo sviluppatore del servizio aggiungerebbe quindi i nuovi metodi a un contratto di servizio esistente oppure creerebbe un nuovo contratto di servizio con metodi che utilizzano il nuovo contratto dati.  
  
 Spesso accade che uno sviluppatore del servizio abbia la necessità di scrivere una logica di business che deve essere eseguita in tutte le versioni di un contratto dati oltre a un codice business specifico per ogni versione del contratto dati.Nell'appendice alla fine dell'argomento viene illustrato come utilizzare le interfacce per soddisfare questa esigenza.  
  
### Controllo delle versioni Lax  
 In molti altri scenari, lo sviluppatore del servizio può presumere che l'aggiunta di un nuovo membro facoltativo al contratto dati non causerà l'interruzione dei client esistenti.A tale fine, deve controllare se i client esistenti non stanno eseguendo la convalida dello schema e ignorano i membri dati sconosciuti.In questi scenari, è possibile sfruttare le funzionalità del contratto dati per aggiungere nuovi membri in modo da non causare interruzioni.Lo sviluppatore del servizio può fare tranquillamente questa ipotesi se le funzionalità del contratto dati per il controllo delle versioni sono già state utilizzate per la prima versione del servizio.  
  
 [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], i servizi Web ASP.NET e numerosi altri stack del servizio Web supportano il *controllo delle versioni lax*, ovvero non generano eccezioni per i nuovi membri dati sconosciuti nei dati ricevuti.  
  
 Accade di credere erroneamente che l'aggiunta di un nuovo membro non interromperà i client esistenti.Se non si è certi che tutti i client possano gestire il controllo delle versioni lax, è consigliabile utilizzare le indicazioni sul controllo delle versioni strict e trattare i contratti dati come immutabili.  
  
 Per indicazioni dettagliate sul controllo delle versioni dei contratti dati lax e strict, vedere [Procedure consigliate: controllo delle versioni del contratto dati](../../../docs/framework/wcf/best-practices-data-contract-versioning.md).  
  
### Distinzione tra contratto dati e tipi .NET  
 È possibile progettare una struttura o una classe .NET come contratto dati applicando l'attributo <xref:System.Runtime.Serialization.DataContractAttribute> alla classe.Il tipo .NET e le sue proiezioni del contratto dati sono due argomenti distinti.È possibile avere più tipi .NET con la stessa proiezione del contratto dati.Questa distinzione è particolarmente utile per consentire di modificare il tipo .NET mantenendo il contratto dati progettato e quindi mantenendo la compatibilità con i client esistenti anche nel senso più rigoroso del termine.Per mantenere questa distinzione tra il tipo .NET e il contratto dati è necessario eseguire sempre due operazioni:  
  
-   Specificare un <xref:System.Runtime.Serialization.DataContractAttribute.Name%2A> e un <xref:System.Runtime.Serialization.DataContractAttribute.Namespace%2A>.È necessario specificare sempre il nome e lo spazio dei nomi del contratto dati per impedire che il nome del tipo .NET e lo spazio dei nomi vengano esposti nel contratto.In questo modo, se in seguito si decide di modificare lo spazio dei nomi .NET o il nome del tipo, il contratto dati rimarrà invariato.  
  
-   Specificare <xref:System.Runtime.Serialization.DataMemberAttribute.Name%2A>.È necessario specificare sempre il nome dei propri membri dati per impedire che il nome del proprio membro .NET venga esposto nel contratto.In tal modo, se in seguito si decide di modificare il nome .NET del membro, il contratto dati rimarrà invariato.  
  
### Modifica o rimozione di membri  
 La modifica del nome o del tipo di dati di un membro o la rimozione di membri dati è un'operazione che può determinare interruzioni anche se è consentito il controllo lax delle versioni.Se tali operazioni sono necessarie, creare un nuovo contratto dati.  
  
 Se la compatibilità del servizio è molto importante, è possibile ignorare i membri dati inutilizzati nel codice e lasciarli dove sono.Se si suddivide un membro dati in più membri, si potrebbe lasciare il membro esistente nel punto in cui si trova come proprietà in grado di eseguire la separazione e la riaggregazione richieste per i client di livello inferiore \(i client che non vengono aggiornati alla versione più recente\).  
  
 Analogamente, le modifiche al nome del contratto dati o allo spazio dei nomi determinano interruzioni.  
  
### Sequenze di andata e ritorno di dati sconosciuti  
 In alcuni scenari, è necessario far compiere una sequenza di "andata e ritorno" ai dati sconosciuti provenienti dai membri aggiunti in una nuova versione.Un servizio "versionNew", ad esempio, invia i dati con alcuni membri appena aggiunti a un client "versionOld".Il client ignora i membri appena aggiunti durante l'elaborazione del messaggio, ma invia nuovamente gli stessi dati, compresi i membri appena aggiunti, al servizio versionNew.Uno scenario tipico è rappresentato da aggiornamenti dei dati in cui i dati vengono recuperati dal servizio, modificati e restituiti.  
  
 Per consentire sequenze di andata e ritorno per un particolare tipo, quest'ultimo deve implementare l'interfaccia <xref:System.Runtime.Serialization.IExtensibleDataObject>.L'interfaccia contiene una proprietà, <xref:System.Runtime.Serialization.IExtensibleDataObject.ExtensionData%2A>, che restituisce il tipo <xref:System.Runtime.Serialization.ExtensionDataObject>.La proprietà viene utilizzata per archiviare qualsiasi dato da versioni future del contratto dati che è sconosciuto alla versione corrente.Questi dati sono opachi al client, ma quando l'istanza viene serializzata, il contenuto della proprietà <xref:System.Runtime.Serialization.IExtensibleDataObject.ExtensionData%2A> viene scritto assieme al resto dei dati dei membri del contratto dati.  
  
 È consigliabile che tutti i tipi implementino questa interfaccia per accogliere i membri futuri sconosciuti e nuovi.  
  
### Librerie di contratti dati  
 Possono esistere librerie di contratti dati in cui un contratto viene pubblicato in un repository centrale e gli implementatori del servizio e del tipo implementano ed espongono i contratti dati da quel repository.In questo caso, quando si pubblica un contratto dati nel repository, non si ha alcun controllo su chi crea i tipi che l'implementano.Non è pertanto possibile modificare il contratto dopo che è stato pubblicato, che sarà quindi di fatto immutabile.  
  
### Utilizzo di XmlSerializer  
 Gli stessi principi di controllo delle versioni si applicano quando si utilizza la classe <xref:System.Xml.Serialization.XmlSerializer>.Quando è richiesto un controllo rigoroso delle versioni, trattare i contratti dati come immutabili e creare i nuovi contratti dati con nomi completi univoci per le nuove versioni.Quando si è certi che è possibile utilizzare il controllo lax delle versioni, è possibile aggiungere nuovi membri serializzabili nelle nuove versioni ma non modificare o rimuovere i membri esistenti.  
  
> [!NOTE]
>  <xref:System.Xml.Serialization.XmlSerializer> utilizza gli attributi <xref:System.Xml.Serialization.XmlAnyElementAttribute> e <xref:System.Xml.Serialization.XmlAnyAttributeAttribute> per supportare sequenze di andata e ritorno di dati sconosciuti.  
  
## Controllo delle versioni dei contratti di messaggio  
 Le linee guida per il controllo delle versioni dei contratti di messaggio sono molto simili al controllo delle versioni dei contratti dati.Se è richiesto il controllo rigoroso delle versioni, non modificare il corpo del messaggio, ma creare un nuovo contratto di messaggio con un nome completo univoco.Se si sa che è possibile utilizzare il controllo lax delle versioni, è possibile aggiungere nuove parti al corpo del messaggio ma non modificare o rimuove quelle esistenti.Questa indicazione si applica sia ai contratti di messaggio bare che a quelli wrapped.  
  
 È sempre possibile aggiungere intestazioni messaggio, anche se è utilizzato il controllo strict delle versioni.Il flag MustUnderstand può influire sul controllo delle versioni.In genere, il modello di controllo delle versioni per le intestazioni in [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] è quello descritto nella specifica SOAP.  
  
## Controllo delle versioni dei contratti di servizio  
 Anche il controllo delle versioni dei contratti di servizio implica operazioni di aggiunta, modifica e rimozione, in modo analogo a quello dei contratti dati.  
  
### Specifica di nome, spazio dei nomi e azione  
 Per impostazione predefinita, il nome di un contratto di servizio è il nome dell'interfaccia.Il suo spazio dei nomi predefinito è "http:\/\/tempuri.org" e l'azione di ogni operazione è "http:\/\/tempuri.org\/contractname\/methodname".È consigliabile specificare in modo esplicito un nome e un spazio dei nomi per il contratto di servizio e un'azione per ogni operazione per evitare di utilizzare "http:\/\/tempuri.org" e impedire che i nomi del metodo e dell'interfaccia vengano esposti nel contratto di servizio.  
  
### Aggiunta di parametri e operazioni  
 L'aggiunta di operazioni del servizio esposte dal servizio è una modifica che non provoca interruzioni perché non è necessario che i client esistenti si occupino delle nuove operazioni.  
  
> [!NOTE]
>  L'aggiunta di operazioni a un contratto di callback duplex è una modifica che può provocare interruzioni.  
  
### Modifica del parametro dell'operazione o tipi restituiti  
 La modifica del parametro o dei tipi restituiti in genere determina interruzioni a meno che il nuovo tipo non implementi lo stesso contratto dati implementato dal vecchio tipo.Per apportare questa modifica, aggiungere una nuova operazione al contratto di servizio o definire un nuovo contratto di servizio.  
  
### Rimozione di operazioni  
 Anche la rimozione di operazioni è una modifica che determina interruzioni.Per apportare tale modifica, definire un nuovo contratto di servizio ed esporlo su un nuovo endpoint.  
  
### Contratti di errore  
 L'attributo <xref:System.ServiceModel.FaultContractAttribute> consente a un sviluppatore di contratti di servizio di specificare informazioni sugli errori che possono essere restituiti dalle operazioni del contratto.  
  
 L'elenco degli errori descritti nel contratto di un servizio non è considerato completo.In qualsiasi momento, un'operazione può restituire errori che non sono descritti nel suo contratto.La modifica de set di errori descritti nel contratto non è pertanto considerata una modifica che determina interruzioni.Questo è il caso, ad esempio, dell'aggiunta di un nuovo errore al contratto utilizzando <xref:System.ServiceModel.FaultContractAttribute> o della rimozione di un errore esistente dal contratto.  
  
### Librerie di contratti di servizio  
 Le organizzazioni possono avere librerie di contratti in cui un contratto viene pubblicato in un repository centrale e il servizio implementa i contratti da quel repository.In questo caso, quando si pubblica un contratto di servizio nel repository, non si ha alcun controllo su chi crea i servizi che l'implementano.Non è pertanto possibile modificare il contratto del servizio dopo che è stato pubblicato, rendendolo di fatto immutabile.[!INCLUDE[indigo2](../../../includes/indigo2-md.md)] supporta l'ereditarietà dei contratti, che può essere utilizzata per creare un nuovo contratto che estende i contratti esistenti.Per utilizzare questa funzionalità, definire una nuova interfaccia del contratto di servizio che eredita dalla vecchia interfaccia del contratto di servizio, quindi aggiungere metodi alla nuova interfaccia.Modificare quindi il servizio che implementa il vecchio contratto per implementare quello nuovo e modificare la definizione dell'endpoint "versionOld" per utilizzare il nuovo contratto.Ai client "versionOld", l'endpoint continuerà a sembrare come se esponesse il contratto "versionOld"; ai client "versionNew", l'endpoint sembrerà esporre il contratto "versionNew".  
  
## Controllo delle versioni di associazioni e indirizzi  
 Le modifiche all'indirizzo endpoint e all'associazione sono modifiche che possono determinare interruzioni a meno che i client non siano in grado di scoprire dinamicamente il nuovo indirizzo endpoint o la nuova associazione.Per implementare questa funzionalità è possibile utilizzare un Registro di sistema UDDI \(Universal Discovery Description and Integration\) e il modello di chiamata UDDI in cui un client tenta di comunicare con un endpoint e, in caso di errore, esegue una query nel registro di sistema UDDI noto, per cercare i metadati dell'endpoint corrente.Il client utilizza quindi l'indirizzo e l'associazione da questi metadati per comunicare con l'endpoint.Se la comunicazione riesce, il client memorizza nella cache le informazioni sull'indirizzo e sull'associazione per utilizzarle in seguito.  
  
## Servizio di routing e controllo delle versioni  
 Se le modifiche apportate a un servizio sono in grado di determinare interruzioni e sono necessarie due o più versioni diverse di un servizio in esecuzione contemporanea, è possibile utilizzare il servizio di routing WCF per indirizzare messaggi all'istanza del servizio appropriata.Il servizio di routing WCF utilizza routing basato sul contenuto, ovvero informazioni contenute nel messaggio, per determinare il punto in cui indirizzare il messaggio stesso.[!INCLUDE[crabout](../../../includes/crabout-md.md)] servizio di routing WCF, vedere [Servizio di routing](../../../docs/framework/wcf/feature-details/routing-service.md).Per un esempio di utilizzo del servizio di routing WCF per il controllo delle versioni del servizio, vedere [Procedura: controllo delle versioni dei servizi](../../../docs/framework/wcf/feature-details/how-to-service-versioning.md).  
  
## Appendice  
 Quando è richiesto un controllo rigoroso delle versioni dei contratti dati, trattare questi ultimi come immutabili e creare nuovi contratti dati quando è necessario apportare modifiche.È necessario creare una nuova classe per ogni nuovo contratto dati, pertanto è richiesto un meccanismo che eviti di prendere il codice esistente scritto secondo la vecchia classe del contratto dati e riscriverli secondo quella nuova del contratto dati.  
  
 Questo meccanismo consiste nell'utilizzare le interfacce per definire i membri di ogni contratto dati e scrivere il codice di implementazione interno in termini di interfacce piuttosto che classi del contratto dati che implementano le interfacce.Nel codice seguente per la versione 1 di un servizio vengono illustrati un'interfaccia `IPurchaseOrderV1` e un oggetto `PurchaseOrderV1`:  
  
```  
public interface IPurchaseOrderV1  
{  
    string OrderId { get; set; }  
    string CustomerId { get; set; }  
}  
  
[DataContract(  
Name = "PurchaseOrder",  
Namespace = "http://examples.microsoft.com/WCF/2005/10/PurchaseOrder")]  
public class PurchaseOrderV1 : IPurchaseOrderV1  
{  
    [DataMember(...)]  
    public string OrderId {...}  
    [DataMember(...)]  
    public string CustomerId {...}  
}  
```  
  
 Mentre le operazioni del contratto di servizio verrebbero scritte come `PurchaseOrderV1`, la logica di business effettiva sarebbe `IPurchaseOrderV1`.Quindi, nella versione 2, ci sarebbero una nuova interfaccia `IPurchaseOrderV2` e una nuova classe `PurchaseOrderV2`, come illustrato nel codice seguente:  
  
```  
public interface IPurchaseOrderV2  
{  
    DateTime OrderDate { get; set; }  
}  
[DataContract(   
Name = "PurchaseOrder ",  
Namespace = "http://examples.microsoft.com/WCF/2006/02/PurchaseOrder")]  
public class PurchaseOrderV2 : IPurchaseOrderV1, IPurchaseOrderV2  
{  
    [DataMember(...)]  
    public DateTime OrderId {...}  
    [DataMember(...)]  
    public string CustomerId {...}  
    [DataMember(...)]  
    public DateTime OrderDate { ... }  
}  
```  
  
 Il contratto di servizio verrebbe aggiornato per includere le nuove operazioni che sono scritte come `PurchaseOrderV2`.La logica di business esistente scritta in termini di `IPurchaseOrderV1` continuerebbe a funzionare per `PurchaseOrderV2` e la nuova logica di business che richiede la proprietà `OrderDate` verrebbe scritta come `IPurchaseOrderV2`.  
  
## Vedere anche  
 <xref:System.Runtime.Serialization.DataContractSerializer>   
 <xref:System.Runtime.Serialization.DataContractAttribute>   
 <xref:System.Runtime.Serialization.DataContractAttribute.Name%2A>   
 <xref:System.Runtime.Serialization.DataContractAttribute.Namespace%2A>   
 <xref:System.Runtime.Serialization.DataMemberAttribute.Order%2A>   
 <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A>   
 <xref:System.Runtime.Serialization.IExtensibleDataObject>   
 <xref:System.Runtime.Serialization.ExtensionDataObject>   
 <xref:System.Runtime.Serialization.IExtensibleDataObject.ExtensionData%2A>   
 <xref:System.Xml.Serialization.XmlSerializer>   
 [Equivalenza dei contratti dati](../../../docs/framework/wcf/feature-details/data-contract-equivalence.md)   
 [Callback di serializzazione a tolleranza di versione](../../../docs/framework/wcf/feature-details/version-tolerant-serialization-callbacks.md)