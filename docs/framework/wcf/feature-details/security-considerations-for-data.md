---
title: "Considerazioni sulla protezione per i dati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a7eb98da-4a93-4692-8b59-9d670c79ffb2
caps.latest.revision: 23
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 23
---
# Considerazioni sulla protezione per i dati
Quando si utilizzano dati in [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] è necessario considerare varie di categorie di minacce. Nella tabella seguente sono elencate le più importanti categorie di minacce correlate all'elaborazione dati. In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] vengono forniti gli strumenti per mitigare queste minacce.  
  
 Denial of Service \(Negazione del servizio\)  
 Quando si ricevono dati non attendibili, tali dati possono fare in modo che il lato ricevente acceda a una quantità sproporzionata di risorse varie, ad esempio memoria, thread, connessioni disponibili o cicli del processore, causando un prolungamento eccessivo dei tempi di calcolo. Un attacco Denial of Service contro un server può causarne l'arresto anomalo e l'incapacità di elaborare messaggi provenienti da altri client legittimi.  
  
 Esecuzione di codice dannoso  
 Dati non attendibili in arrivo fanno in modo che il lato ricevente esegua codice non previsto.  
  
 Information Disclosure \(Rivelazione di informazioni\)  
 L'autore dell'attacco remoto forza il ricevente a rispondere alle richieste rivelando più informazioni di quante non ne avrebbe fornite intenzionalmente.  
  
## Protezione da codice fornito dall'utente e dall'accesso di codice  
 Da varie posizioni nell'infrastruttura di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] viene eseguito codice fornito dall'utente. Ad esempio, il motore di serializzazione <xref:System.Runtime.Serialization.DataContractSerializer> può chiamare funzioni di accesso fornite dall'utente `set` e funzioni di accesso `get`. L'infrastruttura di canale di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] può inoltre eseguire chiamate in classi derivate della classe <xref:System.ServiceModel.Channels.Message> fornite dall'utente.  
  
 L'autore del codice ha la responsabilità di assicurare che non esistano punti vulnerabili. Se si crea, ad esempio, un tipo di contratto dati con una proprietà del membro dati di tipo integer e nell'implementazione della funzione di accesso `set` si alloca una matrice in base al valore della proprietà, è possibile che si verifichi un attacco Denial of Service se un messaggio dannoso contiene un valore estremamente grande per questo membro dati. In generale evitare le allocazioni basate su dati in arrivo o lunghe elaborazioni in codice fornito dall'utente, soprattutto se il prolungamento dei tempi di elaborazione può essere causato da una piccola quantità di dati in arrivo. Quando si esegue l'analisi di sicurezza di codice fornito dall'utente, assicurarsi di considerare anche tutti i casi di errore, ovvero tutti i branch del codice in cui vengono generate eccezioni.  
  
 L'esempio più estremo di codice fornito dall'utente è il codice interno all'implementazione del servizio per ogni operazione. È responsabilità dello sviluppatore proteggere l'implementazione del servizio. È facile creare inavvertitamente implementazioni dell'operazione non protette che possono indurre vulnerabilità agli attacchi Denial of Service. Ad esempio, un'operazione che utilizza una stringa e restituisce l'elenco dei clienti da un database il cui nome inizia con quella stringa. Se il database è di grandi dimensioni e la stringa passata è di una sola lettera, il codice potrebbe tentare di creare un messaggio di dimensioni maggiori della memoria disponibile, paralizzando l'intero servizio. L'eccezione <xref:System.OutOfMemoryException> non è reversibile e in [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] causa sempre la chiusura dell'applicazione.  
  
 È necessario assicurarsi che non vi sia codice dannoso collegato ai vari punti di estendibilità. Soprattutto in caso di esecuzione con attendibilità parziale, nella gestione di tipi provenienti da assembly parzialmente attendibili o nella creazione di componenti utilizzati da codici parzialmente attendibili. Per ulteriori informazioni, vedere "Minacce legate all'attendibilità parziale" in una sezione successiva .  
  
 Si noti che in caso di esecuzione con attendibilità parziale, l'infrastruttura di serializzazione del contratto dati supporta solo un sottoinsieme limitato del modello di programmazione del contratto dati \- ad esempio, tipi o membri dati privati che utilizzano l'attributo <xref:System.SerializableAttribute> non sono supportati.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Attendibilità parziale](../../../../docs/framework/wcf/feature-details/partial-trust.md).  
  
## Come evitare l'Information Disclosure \(Rivelazione di informazioni\) non intenzionale  
 Quando si progettano tipi serializzabili tenendo conto della protezione, l'Information Disclosure può costituire un problema.  
  
 Si considerino i punti seguenti:  
  
-   Il modello di programmazione <xref:System.Runtime.Serialization.DataContractSerializer> consente l'esposizione all'esterno del tipo o dell'assembly di dati riservati e interni durante la serializzazione. Durante l'esportazione dello schema è inoltre possibile che venga esposta la forma di un tipo. È essenziale sapere come sarà la proiezione della serializzazione del tipo. Se non si desidera che vengano esposti elementi, disattivarne la serializzazione, ad esempio non applicando l'attributo <xref:System.Runtime.Serialization.DataMemberAttribute> nel caso di un contratto dati.  
  
-   Si osservi che possono esistere diverse proiezioni di serializzazione per lo stesso tipo, a seconda del serializzatore utilizzato. Lo stesso tipo può esporre un set di dati quando viene utilizzato con il serializzatore <xref:System.Runtime.Serialization.DataContractSerializer> e un set di dati diverso quando viene utilizzato con il serializzatore <xref:System.Xml.Serialization.XmlSerializer>. L'utilizzo accidentale di un serializzatore errato può condurre all'Information Disclosure.  
  
-   Utilizzando il serializzatore <xref:System.Xml.Serialization.XmlSerializer> in una chiamata a una procedura remota \(RPC\) in ambiente legacy\/in modalità codificata è possibile esporre in maniera non intenzionale al lato ricevente la forma dell'oggetto grafico contenuto nel lato che invia.  
  
## Prevenzione degli attacchi Denial of Service  
  
### Quote  
 Fare in modo che il lato ricevente allochi un quantità di memoria significativa potenzialmente costituisce un attacco Denial of Service. Sebbene questa sezione verta essenzialmente sui problemi di utilizzo della memoria derivanti dai messaggi di grandi dimensioni, possono verificarsi altri attacchi. Ad esempio, i tempi di elaborazione dei messaggi possono prolungarsi intollerabilmente.  
  
 Gli attacchi Denial of Service vengono in genere mitigati utilizzando le quote. Al superamento di una quota viene di solito generata un'eccezione <xref:System.ServiceModel.QuotaExceededException>. In assenza di quote, un messaggio dannoso potrebbe causare l'utilizzo di tutta la memoria disponibile, provocando la generazione di un'eccezione <xref:System.OutOfMemoryException> o l'utilizzo di tutti gli stack disponibili, con la conseguente generazione di un'eccezione <xref:System.StackOverflowException>.  
  
 Il superamento di una quota è reversibile; se si verifica in un servizio in esecuzione, il messaggio al momento in fase di elaborazione viene ignorato e il servizio rimane in esecuzione e continua a elaborare messaggi. I casi di memoria insufficiente e di overflow dello stack non sono tuttavia reversibili in [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)], pertanto il servizio termina se incontra tali eccezioni.  
  
 In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] le quote non comportano preallocazioni. Se, ad esempio, la quota <xref:System.ServiceModel.Channels.TransportBindingElement.MaxReceivedMessageSize%2A> \(presente in varie classi\) è impostata su 128 KB, non significa che vengano automaticamente allocati 128 KB per ogni messaggio. La quantità realmente allocata dipende dalla dimensione effettiva del messaggio in arrivo.  
  
 Molte quote sono disponibili a livello di trasporto. Queste quote vengono applicate dal canale di trasporto specifico utilizzato \(HTTP, TCP e così via\). Benché alcune di queste quote siano descritte in questo argomento, per una descrizione dettagliata delle quote vedere [Quote dei trasporti](../../../../docs/framework/wcf/feature-details/transport-quotas.md).  
  
### Vulnerabilità delle tabelle hash  
 Una vulnerabilità si verifica quando i contratti dati contengono tabelle hash o raccolte. Il problema si verifica se un numero elevato di valori viene inserito in una tabella hash in cui gran parte di questi valori genera lo stesso valore hash. Questa situazione può essere utilizzata come attacco di tipo Denial of Service \(DoS\).  Questa vulnerabilità può essere contrastata impostando la quota di associazione MaxReceivedMessageSize. Prestare attenzione durante l'impostazione di questa quota per evitare tali attacchi. La quota definisce un limite superiore per la dimensione del messaggio WCF. Inoltre, evitare di utilizzare tabelle hash o raccolte nei contratti dati.  
  
## Limitazione dell'utilizzo di memoria senza flusso  
 Il modello di sicurezza da adottare per i messaggi di grandi dimensioni dipende dall'utilizzo del flusso. Nel caso più semplice, quando il flusso non viene utilizzato, i messaggi vengono memorizzati nel buffer. In questo caso, utilizzare la quota <xref:System.ServiceModel.Channels.TransportBindingElement.MaxReceivedMessageSize%2A> per l'elemento <xref:System.ServiceModel.Channels.TransportBindingElement> o le associazioni fornite dal sistema per la protezione dai messaggi di grandi dimensioni limitando la dimensione massima utilizzabile per i messaggi. Si noti che un servizio può elaborare più messaggi contemporaneamente, nel qual caso sono inclusi tutti in memoria. Utilizzare la funzionalità di limitazione per mitigare questa minaccia.  
  
 Si osservi inoltre che `MaxReceivedMessageSize` non impone un limite superiore per l'utilizzo di memoria per messaggio, ma lo forza a rientrare un fattore costante. Ad esempio, se `MaxReceivedMessageSize` è 1 MB e si riceve un messaggio da 1 MB che viene deserializzato, è necessaria memoria aggiuntiva per contenere l'oggetto grafico deserializzato, comportando un utilizzo totale della memoria ben oltre 1 MB. Per questa ragione evitare di creare tipi serializzabili che potrebbero causare un utilizzo di memoria significativo pur in assenza di grandi quantità di dati in arrivo. Ad esempio, per il contratto dati "MyContract" con 50 campi di membri dati facoltativi e ulteriori 100 campi privati potrebbe essere creata un'istanza con il costrutto XML "\<MyContract\/\>". Tale costrutto XML comporta un utilizzo della memoria per 150 campi. Si noti che i membri dati sono facoltativi per impostazione predefinita. Il problema è maggiore quando il tipo fa parte di una matrice.  
  
 La quota `MaxReceivedMessageSize` da sola non è sufficiente per impedire tutti gli attacchi Denial of Service. È ad esempio possibile forzare il deserializzatore a deserializzare un oggetto grafico profondamente annidato \(ovvero un oggetto contenente un altro oggetto che a sua volta ne contiene un altro ancora e così via\) da un messaggio in arrivo. Per deserializzare tali oggetti grafici, i serializzatori <xref:System.Runtime.Serialization.DataContractSerializer> e <xref:System.Xml.Serialization.XmlSerializer> chiamano entrambi metodi in base a una modalità annidata. L'annidamento profondo di chiamate ai metodi può causare la generazione di un'eccezione <xref:System.StackOverflowException> irreversibile. Questa minaccia viene mitigata impostando la quota <xref:System.ServiceModel.Configuration.XmlDictionaryReaderQuotasElement.MaxDepth%2A> per limitare il livello di annidamento XML, come descritto nella sezione "Utilizzo sicuro di XML" riportata più avanti in questo argomento.  
  
 È particolarmente importante impostare quote aggiuntive su `MaxReceivedMessageSize` se si utilizza la codifica XML binaria. L'utilizzo della codifica binaria è per qualche aspetto equivalente alla compressione: un piccolo gruppo di byte nel messaggio in arrivo può rappresentare molti dati. Un messaggio che rientra nel limite stabilito da `MaxReceivedMessageSize` in formato completamente espanso può pertanto utilizzare più memoria. Per mitigare queste minacce specifiche del codice XML tutte le quote di lettori XML devono essere impostate correttamente, come descritto nella sezione "Utilizzo sicuro di XML" più avanti in questo argomento.  
  
## Limitazione dell'utilizzo di memoria con flusso  
 Quando si utilizza il flusso è possibile utilizzare un numero basso come impostazione di `MaxReceivedMessageSize` per proteggersi da attacchi Denial of Service. Utilizzando il flusso si possono tuttavia creare scenari più complessi. Si supponga, come esempio, che un servizio di caricamento di file accetti file con dimensioni maggiori di tutta la memoria disponibile. In questo caso, la quota `MaxReceivedMessageSize` viene impostata su un valore molto grande, prevedendo che non vengono pressoché memorizzati dati nel buffer e che quindi il messaggio viene convogliato direttamente su disco dal flusso. Se un messaggio dannoso dovesse in qualche modo riuscire a fare sì che in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] i dati vengano memorizzati nel buffer anziché utilizzare il flusso, `MaxReceivedMessageSize` non risulta più efficace come protezione per evitare che il messaggio utilizzi tutta la memoria disponibile.  
  
 Per mitigare questa minaccia esistono impostazioni di quota specifiche nei vari componenti di elaborazione dati di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] per limitare la memorizzazione nel buffer. La più importante fra queste è la proprietà `MaxBufferSize` in vari elementi di associazione del trasporto e associazioni standard. Quando si utilizza il flusso questa quota deve essere impostata tenendo conto dalla quantità massima di memoria che si è disposti ad allocare per messaggio. Come avviene con `MaxReceivedMessageSize`, questa impostazione non impone un limite massimo assoluto all'utilizzo della memoria ma lo forza esclusivamente a rientrare in fattore costante. Con `MaxReceivedMessageSize` è inoltre necessario essere consapevoli della possibilità che più messaggi vengano elaborati contemporaneamente.  
  
### Informazioni dettagliate su MaxBufferSize  
 La proprietà `MaxBufferSize`  limita le memorizzazioni in massa nel buffer eseguite da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]. In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], ad esempio, vengono sempre memorizzati nel buffer intestazioni ed errori SOAP, così come parti MIME che non si trovano nell'ordine naturale di lettura in un messaggio MTOM \(Message Transmission Optimization Mechanism\). Questa impostazione limita la quantità di dati memorizzati nel buffer in tutti i casi descritti.  
  
 In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] questa operazione viene svolta passando il valore `MaxBufferSize` ai vari componenti che possono eseguire la memorizzazione nel buffer. Ad esempio, alcuni overload <xref:System.ServiceModel.Channels.Message.CreateMessage%2A> della classe <xref:System.ServiceModel.Channels.Message> accettano un parametro `maxSizeOfHeaders`.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] passa il valore `MaxBufferSize` a questo parametro per limitare la quantità di dati dell'intestazione SOAP memorizzati nel buffer. È importante impostare questo parametro quando si utilizza direttamente la classe <xref:System.ServiceModel.Channels.Message>. In generale, quando in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] si utilizza un componente che accetta parametri di quota, è importante essere consapevoli che questi parametri influiscono sulla protezione e impostarli correttamente.  
  
 Anche il codificatore dei messaggi MTOM dispone di un'impostazione `MaxBufferSize`. Quando si utilizzano associazioni standard, questo elemento viene impostato automaticamente sul valore `MaxBufferSize` a livello di trasporto. Quando tuttavia si utilizza l'elemento di associazione del codificatore dei messaggi MTOM per costruire un'associazione personalizzata, è importante impostare la proprietà `MaxBufferSize` su un valore sicuro quando viene utilizzato il flusso.  
  
## Attacchi al flusso basati su XML  
 La proprietà `MaxBufferSize` da sola non è sufficiente per assicurare che in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non possa essere forzatamente eseguita la memorizzazione nel buffer quando è previsto il flusso. Ad esempio, i lettori XML di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] memorizzano sempre nel buffer il tag iniziale dell'elemento XML intero quando inizia la lettura di un nuovo elemento. Questo avviene per fare in modo che spazi dei nomi e attributi vengano elaborati correttamente. Se la proprietà `MaxReceivedMessageSize` è impostata su un valore grande \(ad esempio, in uno scenario caratterizzato dal flusso diretto di file di grandi dimensioni al disco\), potrebbe essere costruito un messaggio dannoso il cui corpo intero sia costituito da un tag iniziale dell'elemento XML di grandi dimensioni. Il tentativo di leggerlo comporterebbe la generazione di un'eccezione <xref:System.OutOfMemoryException>. Questo non è che uno dei molti attacchi Denial of Service basati su XML possibili, tutti mitigabili utilizzando le quote di lettore XML descritte nella sezione "Utilizzo sicuro di XML" riportata in seguito in questo argomento. Quando si utilizza il flusso, è particolarmente importante impostare tutte queste quote.  
  
### Utilizzo congiunto del modello di programmazione basato sul flusso e del modello di programmazione basato sulla memorizzazione nel buffer  
 Molti potenziali attacchi derivano dall'utilizzo congiunto di modelli di programmazione basati e non basati sul flusso all'interno dello stesso servizio. Si prenda in considerazione ad esempio un contratto di servizio con due operazioni: una che utilizza la classe <xref:System.IO.Stream> e l'altra che utilizza una matrice di un tipo personalizzato. Si supponga inoltre che la proprietà `MaxReceivedMessageSize` sia impostata su un valore grande per consentire alla prima operazione di elaborare grandi flussi. Purtroppo ciò significa che sarà possibile inviare messaggi di grandi dimensioni anche alla seconda operazione e il deserializzatore memorizza i dati nel buffer come matrice prima che venga chiamata l'operazione. Si tratta di un attacco Denial of Service potenziale: la quota `MaxBufferSize` non limita la dimensione del corpo del messaggio che è l'elemento sul quale agisce il deserializzatore.  
  
 Per questa ragione, evitare di utilizzare congiuntamente operazioni basate sul flusso e operazioni non basate sul flusso nello stesso contratto. Se è assolutamente necessario utilizzare entrambi i modelli di programmazione contemporaneamente, osservare le precauzioni seguenti:  
  
-   Disattivare la funzione <xref:System.Runtime.Serialization.IExtensibleDataObject> impostando la proprietà <xref:System.ServiceModel.ServiceBehaviorAttribute.IgnoreExtensionDataObject%2A> di <xref:System.ServiceModel.ServiceBehaviorAttribute> su `true`. Così facendo si ha la certezza che vengano deserializzati solo i membri che fanno parte del contratto.  
  
-   Impostare la proprietà <xref:System.Runtime.Serialization.DataContractSerializer.MaxItemsInObjectGraph%2A>di <xref:System.Runtime.Serialization.DataContractSerializer> su un valore sicuro. Questa quota è disponibile anche per l'attributo <xref:System.ServiceModel.ServiceBehaviorAttribute> o tramite la configurazione. Limita il numero di oggetti che vengono deserializzati in un episodio di deserializzazione. Normalmente ogni parametro dell'operazione o parte del corpo del messaggio in un contratto di messaggio viene deserializzato in un episodio. In caso di deserializzazione di matrici, ogni voce della matrice viene considerata come un oggetto separato.  
  
-   Impostare tutte le quote di lettore XML su valori sicuri. Prestare attenzione a <xref:System.Xml.XmlDictionaryReaderQuotas.MaxDepth%2A>, <xref:System.Xml.XmlDictionaryReaderQuotas.MaxStringContentLength%2A> e <xref:System.Xml.XmlDictionaryReaderQuotas.MaxArrayLength%2A> ed evitare stringhe in operazioni non basate sul flusso.  
  
-   Rivedere l'elenco dei tipi noti, ricordando che è possibile creare in ogni momento istanze di un tipo qualsiasi \(vedere la sezione "Come impedire il caricamento di tipi non previsti" più avanti in questo argomento\).  
  
-   Non utilizzare tipi che implementano l'interfaccia <xref:System.Xml.Serialization.IXmlSerializable> e memorizzano molti dati nel buffer. Non aggiungere tali tipi all'elenco dei tipi noti.  
  
-   Non utilizzare matrici <xref:System.Xml.XmlElement>, <xref:System.Xml.XmlNode>, <xref:System.Byte> o tipi che implementano l'interfaccia <xref:System.Runtime.Serialization.ISerializable> in un contratto.  
  
-   Non utilizzare matrici <xref:System.Xml.XmlElement>, <xref:System.Xml.XmlNode>, <xref:System.Byte> o tipi che implementano l'interfaccia <xref:System.Runtime.Serialization.ISerializable> nell'elenco dei tipi noti.  
  
 Le precauzioni riportate in precedenza si applicano quando l'operazione non basata sul flusso utilizza <xref:System.Runtime.Serialization.DataContractSerializer>. Non utilizzare mai congiuntamente modelli di programmazione basati e non basati sul flusso nello stesso servizio se si utilizza la classe<xref:System.Xml.Serialization.XmlSerializer>, perché non si avvale della protezione data dalla quota <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior.MaxItemsInObjectGraph%2A>.  
  
### Attacchi che rallentano il flusso  
 Una categoria di attacchi Denial of Service basati sul flusso non comporta l'utilizzo di memoria, bensì un rallentamento del mittente o del destinatario dei dati. In attesa dell'invio o della ricezione dei dati si esauriscono risorse quali thread e connessioni disponibili. Questa situazione può verificarsi in seguito a un attacco dannoso o per effetto di un mittente\/destinatario legittimo su una connessione di rete lenta.  
  
 Per mitigare questi attacchi, impostare correttamente i timeout di trasporto.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Quote dei trasporti](../../../../docs/framework/wcf/feature-details/transport-quotas.md). In secondo luogo non utilizzare mai operazioni `Read` o `Write` sincrone quando si utilizzano i flussi in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
## Utilizzo sicuro di XML  
  
> [!NOTE]
>  Sebbene questa sezione riguardi XML, le informazioni si riferiscono anche ai documenti JavaScript Object Notation \(JSON\). Le quote funzionano in modo simile, usando [Mapping tra JSON e XML](../../../../docs/framework/wcf/feature-details/mapping-between-json-and-xml.md).  
  
### Lettori XML sicuri  
 L'Infoset XML costituisce la base di ogni messaggio che viene elaborato in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]. Quando si accettano dati XML da un'origine non attendibile, esistono varie possibilità di attacco di tipo Denial of Service \(DoS\) da contrastare.[!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] fornisce speciali lettori XML sicuri. che vengono creati automaticamente quando si utilizza una delle codifiche standard di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] \(testo, binaria o MTOM\).  
  
 Alcune delle funzionalità di sicurezza per questi lettori sono sempre attive. Ad esempio, i lettori non elaborano mai definizioni del tipo di documento \(DTD\) che sono un'origine potenziale di attacchi Denial of Service e non devono essere mai presenti nei messaggi SOAP legittimi. Fra le altre funzionalità di sicurezza sono incluse quote di lettore da configurare, descritte nella sezione seguente.  
  
 Quando si lavora direttamente con i lettori XML, ad esempio quando si scrive un codificatore personalizzato o quando si utilizza direttamente la classe <xref:System.ServiceModel.Channels.Message>, utilizzare sempre i lettori sicuri di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] se si prevede la possibilità di utilizzare dati non attendibili. Creare i lettori sicuri chiamando uno degli overload del metodo factory statici di <xref:System.Xml.XmlDictionaryReader.CreateTextReader%2A>, <xref:System.Xml.XmlDictionaryReader.CreateBinaryReader%2A> o <xref:System.Xml.XmlDictionaryReader.CreateMtomReader%2A> per la classe <xref:System.Xml.XmlDictionaryReader>. Quando si crea un lettore, passare valori di quota sicuri. Non chiamare gli overload del metodo `Create`. Così facendo non viene creato un lettore di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], Al contrario, viene creato un lettore non protetto dalle funzionalità descritte in questa sezione.  
  
### Quote di lettore  
 I lettori XML sicuri dispongono di cinque quote configurabili. Di norma vengono configurate utilizzando la proprietà `ReaderQuotas` negli elementi di associazione della codifica o nelle associazioni standard oppure utilizzando un oggetto <xref:System.Xml.XmlDictionaryReaderQuotas> passato quando si crea un lettore.  
  
#### MaxBytesPerRead  
 Questa quota limita il numero di byte letti in una sola operazione `Read` durante la lettura del tag iniziale dell'elemento e dei relativi attributi. Nei casi in cui non viene usato il flusso, il nome dell'elemento stesso non viene conteggiato ai fini della quota.<xref:System.Xml.XmlDictionaryReaderQuotas.MaxBytesPerRead%2A> è importante per i motivi seguenti:  
  
-   Il nome dell'elemento e i relativi attributi vengono sempre memorizzati nel buffer quando vengono letti, pertanto è importante impostare correttamente questa quota in modalità di flusso per impedire la memorizzazione di un'eccessiva quantità di dati nel buffer quando è previsto il flusso. Vedere la sezione quota `MaxDepth` per informazioni sulla quantità effettiva di dati che vengono memorizzati nel buffer.  
  
-   La presenza di troppi attributi XML può causare un prolungamento eccessivo dei tempi di elaborazione perché è necessario controllare che i nomi degli attributi siano univoci. Utilizzando la proprietà `MaxBytesPerRead` la minaccia viene mitigata.  
  
#### MaxDepth  
 Questa quota limita la profondità massima di annidamento degli elementi XML. Il documento "\<A\>\<B\>\<C\/\>\<\/B\>\<\/A\>", ad esempio, ha una profondità di annidamento di tre livelli.<xref:System.Xml.XmlDictionaryReaderQuotas.MaxDepth%2A> è importante per i motivi seguenti:  
  
-   `MaxDepth` interagisce con `MaxBytesPerRead`: il lettore mantiene sempre i dati in memoria per l'elemento corrente e tutti i suoi predecessori, pertanto l'utilizzo massimo di memoria da parte del lettore è proporzionale al prodotto di queste due impostazioni.  
  
-   Quando un oggetto grafico profondamente annidato viene deserializzato, il deserializzatore deve utilizzare l'intero stack e generare un'eccezione <xref:System.StackOverflowException> irreversibile. Esiste una correlazione diretta tra l'annidamento XML e l'annidamento di oggetti sia per la classe<xref:System.Runtime.Serialization.DataContractSerializer> sia per la classe <xref:System.Xml.Serialization.XmlSerializer>. Utilizzare `MaxDepth` per mitigare questa minaccia.  
  
#### MaxNameTableCharCount  
 Questa quota limita la dimensione della tabella *NameTable*del lettore. La tabella NameTable contiene alcune stringhe \(ad esempio spazi dei nomi e prefissi\) incontrate durante l'elaborazione di un documento XML. Poiché tali stringhe vengono memorizzate nel buffer, impostare questa quota per impedire la memorizzazione di un'eccessiva quantità di dati nel buffer quando si prevede un flusso.  
  
#### MaxStringContentLength  
 Questa quota limita la dimensione massima della stringa restituita dal lettore XML e non l'utilizzo di memoria nel lettore XML stesso, bensì nel componente che utilizza il lettore. Ad esempio, quando la classe <xref:System.Runtime.Serialization.DataContractSerializer> utilizza un lettore protetto con <xref:System.Xml.XmlDictionaryReaderQuotas.MaxStringContentLength%2A>, non deserializza stringhe che superano questa quota. Quando si utilizza direttamente la classe <xref:System.Xml.XmlDictionaryReader>, la quota non viene rispettata da tutti i metodi, ma solo da quelli specificamente progettati per leggere stringhe, ad esempio il metodo <xref:System.Xml.XmlDictionaryReader.ReadContentAsString%2A>. La quota non influisce sulla proprietà <xref:System.Xml.XmlReader.Value%2A> nel lettore e pertanto non deve essere utilizzata quando la protezione che questa fornisce è strettamente necessaria.  
  
#### MaxArrayLength  
 Questa quota limita la dimensione massima di una matrice di primitive che viene restituita dal lettore XML, incluse matrici di byte. La quota non limita l'utilizzo di memoria nel lettore XML stesso, bensì in un qualsiasi componente che utilizza il lettore. Ad esempio, quando la classe <xref:System.Runtime.Serialization.DataContractSerializer> utilizza un lettore protetto con <xref:System.Xml.XmlDictionaryReaderQuotas.MaxArrayLength%2A>, non deserializza matrici di byte che superano questa quota. È importante impostarla quando si tenta di utilizzare contemporaneamente modelli di programmazione basati sul flusso e sulla memorizzazione nel buffer nello stesso contratto. Si tenga presente che, utilizzando direttamente la classe <xref:System.Xml.XmlDictionaryReader>, la quota viene rispettata solo dai metodi specificamente progettati per leggere matrici di dimensioni arbitrarie di alcuni tipi di primitive, ad esempio <xref:System.Xml.XmlDictionaryReader.ReadInt32Array%2A>.  
  
## Minacce specifiche della codifica binaria  
 La codifica XML binaria supportata da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] include una funzionalità per le *stringhe di dizionario*. È possibile codificare una stringa di grandi dimensioni utilizzando solo pochi byte, con vantaggi significativi a livello di prestazioni, ma così facendo vengono introdotte nuove minacce Denial of Service che devono essere mitigate.  
  
 Sono disponibili due tipi di dizionari: *statico* e *dinamico*. Il dizionario statico è un elenco incorporato di stringhe lunghe che possono essere rappresentate utilizzando un codice breve nella codifica binaria. L'elenco di stringhe viene consolidato al momento della creazione del lettore e non può essere modificato. Nessuna delle stringhe del dizionario statico utilizzato da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] come impostazione predefinita è sufficientemente grande da costituire una grave minaccia Denial of Service, sebbene sia comunque possibile utilizzare tali stringhe in un attacco di espansione del dizionario. In scenari avanzati in cui si fornisce un proprio dizionario statico, prestare attenzione nell'inserire grandi stringhe.  
  
 La funzionalità dinamica dei dizionari consente ai messaggi di definire stringhe proprie e di associarle a codici brevi. Questi mapping da stringa a codice sono mantenuti in memoria durante l'intera sessione di comunicazione, in modo che i messaggi successivi non debbano inviare nuovamente le stringhe e possano utilizzare i codici già definiti. Queste stringhe possono essere di lunghezza arbitraria e quindi costituire una minaccia più grave di quelle contenute nel dizionario statico.  
  
 La prima minaccia che deve essere mitigata è la possibilità che il dizionario dinamico \(tabella di mapping da stringa a codice\) assuma dimensioni troppo grandi. Il dizionario può espandersi nel corso di molti messaggi, per cui la quota `MaxReceivedMessageSize` non offre protezione perché si applica separatamente a ogni singolo messaggio. È pertanto disponibile una proprietà distinta, <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement.MaxSessionSize%2A> per l'elemento <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement> che limita la dimensione del dizionario.  
  
 A differenza di altre quote, questa si applica anche alla scrittura dei messaggi. Se viene superata durante la lettura di un messaggio, come al solito viene generata l'eccezione `QuotaExceededException`. Se viene superata durante la scrittura di un messaggio, le stringhe che causano il superamento della quota vengono scritte così come sono, senza utilizzare la funzionalità dinamica dei dizionari.  
  
### Minacce di espansione del dizionario  
 Una categoria significativa di attacchi specifici del codice binario riguarda l'espansione del dizionario. Un piccolo messaggio in formato binario può trasformarsi in un messaggio di dimensioni molto grandi quando viene espanso completamente in forma testuale se si avvale diffusamente della funzionalità dei dizionari di stringhe. Il fattore di espansione per le stringhe del dizionario dinamiche è limitato dalla quota <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement.MaxSessionSize%2A>, perché nessuna stringa di dizionario dinamica supera la dimensione massima del dizionario intero.  
  
 Le proprietà <xref:System.Xml.XmlDictionaryReaderQuotas.MaxNameTableCharCount%2A>, `MaxStringContentLength`, e `MaxArrayLength` limitano esclusivamente l'utilizzo della memoria. Di solito non sono necessarie per mitigare eventuali minacce in scenari non basati sul flusso in quanto l'utilizzo della memoria è già limitato da `MaxReceivedMessageSize`.`MaxReceivedMessageSize`  tuttavia conteggia i byte prima dell'espansione. Quando viene utilizzata la codifica binaria, l'utilizzo della memoria potrebbe superare la quota `MaxReceivedMessageSize`, essendo limitato solo da un fattore di <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement.MaxSessionSize%2A>. Per questa ragione, è importante impostare sempre tutte le quote del lettore \(specialmente <xref:System.Xml.XmlDictionaryReaderQuotas.MaxStringContentLength%2A>\) quando si utilizza la codifica binaria.  
  
 Se la codifica binaria viene utilizzata con <xref:System.Runtime.Serialization.DataContractSerializer>, è possibile abusare dell'interfaccia `IExtensibleDataObject` per sferrare un attacco di espansione del dizionario. Questa interfaccia essenzialmente fornisce un'archiviazione illimitata per i dati arbitrari che non fanno parte del contratto. Se non è possibile impostare quote sufficientemente basse perché `MaxSessionSize` moltiplicato per `MaxReceivedMessageSize` non crei problemi, disattivare la funzione `IExtensibleDataObject` se si utilizza la codifica binaria. Impostare la proprietà `IgnoreExtensionDataObject`  su `true` nell'attributo `ServiceBehaviorAttribute`. In alternativa, non implementare l'interfaccia `IExtensibleDataObject`.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Contratti dati compatibili con versioni successive](../../../../docs/framework/wcf/feature-details/forward-compatible-data-contracts.md).  
  
### Riepilogo delle quote  
 La tabella seguente contiene un riepilogo delle linee guida per le quote.  
  
|Condizione|Quote importanti da impostare|  
|----------------|-----------------------------------|  
|Niente flusso o flusso di messaggi di piccole dimensioni, testo o codifica MTOM|`MaxReceivedMessageSize`, `MaxBytesPerRead` e `MaxDepth`|  
|Niente flusso o flusso di messaggi di piccole dimensioni, codifica binaria|`MaxReceivedMessageSize`, `MaxSessionSize` e tutte le `ReaderQuotas`|  
|Flusso di messaggi di grandi dimensioni, testo o codifica MTOM|`MaxBufferSize` e tutte le `ReaderQuotas`|  
|Flusso di messaggi di grandi dimensioni, codifica binaria|`MaxBufferSize`, `MaxSessionSize` e tutte le `ReaderQuotas`|  
  
-   I timeout a livello di trasporto devono sempre essere impostati e non utilizzare mai letture\/scritture sincrone quando si utilizza il flusso, indipendentemente dalle dimensioni dei messaggi.  
  
-   Quando si è incerti su una quota, impostarla su un valore sicuro anziché lasciarla aperta.  
  
## Prevenzione dell'esecuzione di codice dannoso  
 Le seguenti categorie generali di minacce possono eseguire codice e avere effetti imprevisti:  
  
-   Il deserializzatore carica un tipo dannoso, non sicuro o dipendente dalla protezione.  
  
-   Un messaggio in arrivo fa in modo che il deserializzatore costruisca un'istanza di un tipo normalmente sicuro in modo da produrre conseguenze impreviste.  
  
 Nelle sezioni seguenti vengono ulteriormente descritte queste categorie di minacce.  
  
## DataContractSerializer  
 \(Per informazioni sulla protezione della classe <xref:System.Xml.Serialization.XmlSerializer> vedere la relativa documentazione\). Il modello di sicurezza di <xref:System.Xml.Serialization.XmlSerializer> è simile a quello della classe  <xref:System.Runtime.Serialization.DataContractSerializer> e differisce soprattutto per i dettagli. L'attributo <xref:System.Xml.Serialization.XmlIncludeAttribute>, ad esempio, viene utilizzato per l'inclusione del tipo in luogo dell'attributo <xref:System.Runtime.Serialization.KnownTypeAttribute>. Alcune minacce univoche della classe <xref:System.Xml.Serialization.XmlSerializer> verranno tuttavia discusse più avanti in questo argomento.  
  
### Prevenzione del caricamento di tipi imprevisti  
 Il caricamento di tipi imprevisti può avere conseguenze significative, sia che il tipo sia dannoso sia che abbia solo effetti secondari dipendenti dalla protezione. Un tipo può contenere vulnerabilità di sicurezza sfruttabili, eseguire azioni dipendenti dalla protezione nel relativo costruttore o costruttore della classe, disporre di un footprint di memoria di grandi dimensioni che facilita gli attacchi Denial of Service o generare eccezioni irreversibili. I tipi possono disporre di costruttori della classe che vengono eseguiti appena viene caricato il tipo e prima che vengano create istanze. Per queste ragioni, è importante controllare il set dei tipi caricabili dal deserializzatore.  
  
 La classe <xref:System.Runtime.Serialization.DataContractSerializer> esegue la deserializzazione in una modalità ad accoppiamento debole \(loose coupling\). Non legge mai il tipo e i nomi degli assembly CLR \(Common Language Runtime\) dai dati in arrivo. Il relativo funzionamento è simile al comportamento delle a classe <xref:System.Xml.Serialization.XmlSerializer>, ma differisce da quello di <xref:System.Runtime.Serialization.NetDataContractSerializer>, <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> e di <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter>. L'accoppiamento debole introduce un certo grado di sicurezza, in quanto l'autore dell'attacco remoto non è in grado di indicare un tipo arbitrario da caricare semplicemente denominandolo nel messaggio.  
  
 <xref:System.Runtime.Serialization.DataContractSerializer> può sempre caricare un tipo attualmente previsto in base al contratto. Ad esempio, se un contratto dati dispone di un membro dati di tipo `Customer`, <xref:System.Runtime.Serialization.DataContractSerializer> è autorizzato a caricare il tipo `Customer` quando deserializza tale membro dati.  
  
 <xref:System.Runtime.Serialization.DataContractSerializer> inoltre supporta il polimorfismo. Un membro dati può essere dichiarato come <xref:System.Object>, ma i dati in arrivo possono contenere un'istanza `Customer`. Ciò è possibile solo se il tipo `Customer` è stato reso "noto" al deserializzatore tramite uno di questi meccanismi:  
  
-   Attributo <xref:System.Runtime.Serialization.KnownTypeAttribute> applicato a un tipo.  
  
-   Attributo `KnownTypeAttribute` che specifica un metodo che restituisce un elenco di tipi.  
  
-   Attributo `ServiceKnownTypeAttribute`.  
  
-   Sezione di configurazione `KnownTypes`.  
  
-   Un elenco di tipi noti passato in modo esplicito a <xref:System.Runtime.Serialization.DataContractSerializer> durante la costruzione, se il serializzatore viene utilizzato direttamente.  
  
 Ognuno di questi meccanismi aumenta la superficie di attacco introducendo più tipi di quanti non ne possa caricare il serializzatore. Controllare tutti questi meccanismi per assicurarsi che non vengano aggiunti tipi dannosi o imprevisti all'elenco dei tipi noti.  
  
 Una volta che un tipo noto è nell'ambito, può essere caricato in qualsiasi momento e potranno esserne create istanze anche se di fatto il contratto impedisce di utilizzarlo. Si supponga, ad esempio, che il tipo "MyDangerousType" venga aggiunto all'elenco dei tipi noti utilizzando uno dei meccanismi sopra descritti. Vale a dire che:  
  
-   `MyDangerousType` viene caricato e viene eseguito il relativo costruttore di classe.  
  
-   Anche in caso di deserializzazione di un contratto dati con un membro dati in formato di stringa, un messaggio dannoso può indurre la creazione di un'istanza di `MyDangerousType`. Può essere eseguito codice contenuto in `MyDangerousType`, ad esempio codice per i metodi Setter sulla proprietà. Successivamente il deserializzatore tenta di assegnare questa istanza al membro dati in formato di stringa e non verrà completato correttamente generando un'eccezione.  
  
 Quando si scrive un metodo che restituisce un elenco di tipi noti o si passa direttamente un elenco al costruttore <xref:System.Runtime.Serialization.DataContractSerializer>, assicurarsi che il codice preposto alla creazione dell'elenco sia sicuro e agisca solo su dati attendibili.  
  
 Se in questa configurazione si specificano tipi noti, assicurarsi che il file di configurazione sia sicuro. Utilizzare sempre nomi sicuri nella configurazione, specificando la chiave pubblica dell'assembly firmato dove risiede il tipo, senza specificare la versione del tipo da caricare. Il caricatore del tipo sceglie automaticamente la versione più recente, se possibile. Se si specifica una particolare versione nella configurazione si corre il rischio seguente: in un tipo può essere contenuta una vulnerabilità di sicurezza che verrà corretta in una versione futura, ma la versione con la vulnerabilità continua a essere caricata perché specificata in modo esplicito nella configurazione.  
  
 La presenza di troppi tipi noti produce un'altra conseguenza: <xref:System.Runtime.Serialization.DataContractSerializer> crea una cache del codice di serializzazione\/deserializzazione nel dominio dell'applicazione, con una voce per ogni tipo da serializzare e deserializzare. Il contenuto della cache non viene eliminato finché è in esecuzione il dominio dell'applicazione. Un pirata informatico consapevole del fatto che un'applicazione utilizza molti tipi noti può causare la deserializzazione di tutti questi tipi, facendo in modo che la cache utilizzi una quantità di memoria estremamente grande.  
  
### Come impedire che i tipi abbiano uno stato imprevisto  
 Per un tipo possono sussistere vincoli di coerenza interni da applicare necessariamente. Si deve prestare attenzione per evitare di infrangerli durante la deserializzazione.  
  
 L'esempio seguente di un tipo rappresenta lo stato di una sacca d'aria su un'astronave e applica il vincolo che le porte interne ed esterne non possano essere aperte contemporaneamente.  
  
 [!code-csharp[DataContractAttribute#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/datacontractattribute/cs/overview.cs#3)]
 [!code-vb[DataContractAttribute#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/datacontractattribute/vb/overview.vb#3)]  
  
 Il possibile autore di un attacco potrebbe inviare un messaggio dannoso come questo, aggirando i vincoli e portando l'oggetto in uno stato non valido che può avere conseguenze impreviste e imprevedibili.  
  
```  
<SpaceStationAirlock>  
    <innerDoorOpen>true</innerDoorOpen>  
    <outerDoorOpen>true</outerDoorOpen>  
</SpaceStationAirlock>  
```  
  
 È possibile evitare questa situazione essendo a conoscenza dei punti seguenti:  
  
-   Quando <xref:System.Runtime.Serialization.DataContractSerializer> deserializza gran parte delle classi, i costruttori non sono in esecuzione. Non basarsi pertanto su una gestione dello stato eseguita nel costruttore.  
  
-   Utilizzare richiamate per assicurare che l'oggetto sia in uno stato valido. La richiamata contrassegnata con l'attributo <xref:System.Runtime.Serialization.OnDeserializedAttribute> è particolarmente utile in quanto viene eseguita dopo che la deserializzazione è stata completata e ha quindi la possibilità di esaminare e correggere lo stato complessivo.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Callback di serializzazione a tolleranza di versione](../../../../docs/framework/wcf/feature-details/version-tolerant-serialization-callbacks.md).  
  
-   Non progettare tipi di contratto dati che si affidano a un ordine particolare per la chiamata dei metodi Setter sulla proprietà.  
  
-   Fare attenzione quando si utilizzano tipi legacy contrassegnati con l'attributo <xref:System.SerializableAttribute>. Molti di essi sono progettati per essere utilizzati con la comunicazione remota di [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] per l'utilizzo esclusivamente con dati attendibili. I tipi esistenti contrassegnati con questo attributo possono non essere stati progettati tenendo presente la sicurezza dello stato.  
  
-   Non affidarsi alla proprietà <xref:System.Runtime.Serialization.DataMemberAttribute.IsRequired%2A> dell'attributo `DataMemberAttribute` per garantire la presenza di dati per quanto riguarda la sicurezza dello stato. I dati potrebbero sempre essere `null`, `zero` o `invalid`.  
  
-   Non considerare mai attendibile un oggetto grafico deserializzato da un'origine dati non attendibile senza prima convalidarlo. Ogni singolo oggetto può essere in uno stato coerente, ma l'oggetto grafico nell'insieme potrebbe non esserlo, inoltre, anche se la modalità di mantenimento è disattivata, se l'oggetto grafico viene deserializzato può contenere più riferimenti allo stesso oggetto o riferimenti circolari.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Serializzazione e deserializzazione](../../../../docs/framework/wcf/feature-details/serialization-and-deserialization.md).  
  
### Utilizzo sicuro di NetDataContractSerializer  
 <xref:System.Runtime.Serialization.NetDataContractSerializer> è un motore di serializzazione che utilizza l'accoppiamento stretto ai tipi. È simile a <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter> e a <xref:System.Runtime.Serialization.Formatters.Soap.SoapFormatter>. Vale a dire che determina quale sia il tipo di cui creare un'istanza leggendo l'assembly [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] e il nome del tipo dai dati in arrivo. Sebbene faccia parte di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], non è possibile inserire questo motore di serializzazione come plug\-in, per farlo è necessario scrivere codice personalizzato.`NetDataContractSerializer` viene fornito soprattutto per agevolare la migrazione dalla comunicazione remota di [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] a [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] la sezione pertinente in [Serializzazione e deserializzazione](../../../../docs/framework/wcf/feature-details/serialization-and-deserialization.md).  
  
 Poiché il messaggio stesso può indicare che è possibile caricare qualsiasi tipo, il meccanismo <xref:System.Runtime.Serialization.NetDataContractSerializer> non è protetto intrinsecamente e deve essere utilizzato solo con dati attendibili. È possibile renderlo sicuro scrivendo un gestore di associazione con limitazione del tipo \(utilizzando la proprietà <xref:System.Runtime.Serialization.NetDataContractSerializer.Binder%2A>\) che consenta di caricare esclusivamente tipi sicuri.  
  
 Anche se si utilizzano dati attendibili, i dati in arrivo possono non contenere una definizione sufficiente del tipo da caricare, specialmente se la proprietà <xref:System.Runtime.Serialization.NetDataContractSerializer.AssemblyFormat%2A> è impostata su <xref:System.Runtime.Serialization.Formatters.FormatterAssemblyStyle>. Chiunque abbia accesso alla directory dell'applicazione o alla Global Assembly Cache può sostituire con un tipo dannoso il tipo che si prevede di caricare. Garantire sempre la protezione della directory dell'applicazione e della Global Assembly Cache impostando correttamente le autorizzazioni.  
  
 In generale, se si consente a codice parzialmente attendibile di accedere all'istanza `NetDataContractSerializer` o in caso contrario controllare il selettore di surrogati \(<xref:System.Runtime.Serialization.ISurrogateSelector>\) o il gestore di associazione della serializzazione \(<xref:System.Runtime.Serialization.SerializationBinder>\), il codice può controllare completamente il processo di serializzazione\/deserializzazione. Ad esempio, può inserire tipi arbitrari, portare alla diffusione di informazioni, manomettere  l'oggetto grafico risultante o i dati serializzati, oppure provocare l'overflow del conseguente flusso serializzato.  
  
 Un altro problema di sicurezza relativo a `NetDataContractSerializer` riguarda una possibile minaccia Denial of Service, non l'esecuzione di codice dannoso. Quando si utilizza `NetDataContractSerializer`, impostare sempre la quota <xref:System.Runtime.Serialization.NetDataContractSerializer.MaxItemsInObjectGraph%2A> su un valore sicuro. È semplice costruire un piccolo messaggio dannoso che alloca una matrice di oggetti la cui dimensione è limitata solo da questa quota.  
  
### Minacce specifiche di XmlSerializer  
 Il modello di sicurezza di <xref:System.Xml.Serialization.XmlSerializer> è simile a quello di <xref:System.Runtime.Serialization.DataContractSerializer>. Alcune minacce sono tuttavia specifiche di <xref:System.Xml.Serialization.XmlSerializer>.  
  
 <xref:System.Xml.Serialization.XmlSerializer> in fase di esecuzione genera *assembly di serializzazione* contenenti codice che di fatto esegue la serializzazione e la deserializzazione; tali assembly vengono creati in una directory di file temporanei. Se un altro processo o utente dispone delle autorizzazioni di accesso a tale directory, potrà sovrascrivere il codice di serializzazione\/deserializzazione con codice arbitrario.<xref:System.Xml.Serialization.XmlSerializer> esegue quindi questo codice utilizzando il relativo contesto di sicurezza anziché il codice di serializzazione\/deserializzazione. Verificare che le autorizzazioni siano impostate correttamente nella directory di file temporanei per impedire che ciò si verifichi.  
  
 <xref:System.Xml.Serialization.XmlSerializer> dispone inoltre di una modalità nella quale utilizza assembly di serializzazione generati in precedenza anziché generarli in fase di esecuzione. Questa modalità si attiva ogni volta che <xref:System.Xml.Serialization.XmlSerializer> trova un assembly di serializzazione adatto.<xref:System.Xml.Serialization.XmlSerializer> controlla se l'assembly di serializzazione è firmato dalla stessa chiave utilizzata per firmare l'assembly che contiene i tipi serializzati. Si ottiene in tal modo la protezione da assembly dannosi mistificati come assembly di serializzazione. Se l'assembly che contiene i tipi serializzabili non è tuttavia firmato, <xref:System.Xml.Serialization.XmlSerializer> non può eseguire questo controllo e utilizza qualsiasi assembly con il nome corretto. Ciò rende possibile l'esecuzione di codice dannoso. Firmare sempre gli assembly che contengono tipi serializzabili o controllare strettamente l'accesso alla directory dell'applicazione e la Global Assembly Cache per impedire l'introduzione di assembly dannosi.  
  
 <xref:System.Xml.Serialization.XmlSerializer> può essere soggetto ad attacchi Denial of Service. La classe <xref:System.Xml.Serialization.XmlSerializer> non dispone di una quota `MaxItemsInObjectGraph` \(come avviene invece per <xref:System.Runtime.Serialization.DataContractSerializer>\). Deserializza quindi un quantità arbitraria di oggetti, con la sola limitazione della dimensione del messaggio.  
  
### Minacce legate all'attendibilità parziale  
 Notare i seguenti problemi riguardanti minacce correlate a codice in esecuzione con attendibilità parziale. Queste minacce includono codice parzialmente attendibile dannoso da solo e in combinazione con gli altri scenari di attacco, ad esempio, codice parzialmente attendibile che costruisce una stringa specifica e quindi la deserializza.  
  
-   Quando si utilizzano componenti di serializzazione, non dichiarare mai autorizzazioni prima di tale sintassi, anche se l'intero scenario di serializzazione rientra nell'ambito dell'asserzione e non si trattano dati o oggetti non attendibili. Questo utilizzo può condurre a problemi di sicurezza.  
  
-   Nei casi in cui un codice parzialmente attendibile prenda il controllo del processo di serializzazione tramite punti di estendibilità \(surrogati\), tipi serializzati o in altri modi, può fare in modo che il serializzatore restituisca una grande quantità di dati nel flusso serializzato. Ciò potrebbe causare attacchi di tipo Denial of Service \(DoS\) al destinatario di questo flusso. Se si sta serializzando dati soggetti a minacce DoS, non bisogna serializzare tipi parzialmente attendibili o al contrario permettere che codice parzialmente attendibile controlli il processo di serializzazione.  
  
-   Se si permette a codice parzialmente attendibile di accedere all'istanza <xref:System.Runtime.Serialization.DataContractSerializer> o in caso contrario di controllare [Surrogati del contratto dati](../../../../docs/framework/wcf/extending/data-contract-surrogates.md), il codice può controllare significativamente il processo di serializzazione\/deserializzazione. Ad esempio, può inserire tipi arbitrari, portare alla diffusione di informazioni, manomettere  l'oggetto grafico risultante o i dati serializzati, oppure provocare l'overflow del conseguente flusso serializzato. Una minaccia equivalente <xref:System.Runtime.Serialization.NetDataContractSerializer> viene descritta nella sezione "Utilizzo sicuro di NetDataContractSerializer".  
  
-   Se l'attributo <xref:System.Runtime.Serialization.DataContractAttribute> viene applicato a un tipo \(o al tipo contrassegnato come `[Serializable]` ma che non è `ISerializable`\) il deserializzatore può creare un'istanza di tale tipo anche se tutti i costruttori non sono pubblici o sono protetti dalle richieste.  
  
-   Non fidarsi mai del risultato della deserializzazione, a meno che i dati da deserializzare siano attendibili e si sia certi che tutti i tipi noti risultino essere tipi attendibili . Si noti che, in caso di esecuzione in condizioni di attendibilità parziale, i tipi noti non vengono caricati dal file di configurazione dell'applicazione, ma vengono caricati dal file di configurazione del computer.  
  
-   Se si passa un'istanza di `DataContractSerializer` con l'aggiunta di un surrogato al codice parzialmente attendibile, il codice può cambiare impostazioni modificabili nel surrogato.  
  
-   Per un oggetto deserializzato, se il lettore XML \(o i dati inclusi\) proviene da codice parzialmente attendibile, trattare l'oggetto deserializzato risultante come dati non attendibili,  
  
-   Il fatto che il tipo <xref:System.Runtime.Serialization.ExtensionDataObject> non abbia membri pubblici non significa che i dati al suo interno siano sicuri. Se, ad esempio, si esegue la deserializzazione da un'origine dati privilegiata in un oggetto nel quale risiedono dati e quindi si passa tale oggetto a codice parzialmente attendibile, quest'ultimo potrà leggere i dati contenuti in `ExtensionDataObject` serializzando l'oggetto. Impostare <xref:System.Runtime.Serialization.DataContractSerializer.IgnoreExtensionDataObject%2A> su `true` quando la deserializzazione viene eseguita da un'origine dati privilegiata in un oggetto che in seguito viene passato a codice parzialmente attendibile.  
  
-   <xref:System.Runtime.Serialization.DataContractSerializer> e <xref:System.Runtime.Serialization.DataContractJsonSerializer> supportano la serializzazione di membri privati, protetti, interni e pubblici in condizioni di attendibilità totale. In condizioni di attendibilità parziale, tuttavia, solo i membri pubblici possono essere serializzati. Se un'applicazione tenta di serializzare un membro non pubblico, viene generata un'eccezione `SecurityException`.  
  
     Per consentire che i membri interni o protetti possano essere serializzati in condizioni di attendibilità parziale, utilizzare l'attributo dell'assembly `System.Runtime.CompilerServices.InternalsVisibleTo`. Questo attributo consente a un assembly di dichiarare che i propri membri interni sono visibili ad altri assembly. In questo caso, un assembly per cui i membri interni devono essere serializzati dichiara che tali membri sono visibili a System.Runtime.Serialization.dll.  
  
     Il vantaggio di questo approccio è rappresentato dal fatto che non è necessario un percorso di generazione di codice con privilegi elevati.  
  
     Sono tuttavia presenti due svantaggi principali.  
  
     Il primo svantaggio è costituito dal fatto che la proprietà di scelta esplicita dell'attributo `InternalsVisibleTo` è a livello di assembly. Questo significa che non è possibile specificare che solo una determinata classe può disporre di membri interni serializzati. Chiaramente, è comunque possibile scegliere di non serializzare un membro interno specifico aggiungendo semplicemente un attributo `DataMember` a tale membro. In modo analogo, uno sviluppatore può scegliere di rendere interno un membro anziché privato o protetto, con problemi di visibilità non significativi.  
  
     Il secondo svantaggio è rappresentato dal fatto che non sono ancora supportati membri privati o protetti.  
  
     Per illustrare l'utilizzo dell'attributo `InternalsVisibleTo` in condizioni di attendibilità parziale, considerare il programma seguente:  
  
     [!code-csharp[CDF_WCF_SecurityConsiderationsForData#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/cdf_wcf_securityconsiderationsfordata/cs/program.cs#1)]  
  
     Nell'esempio precedente `PermissionsHelper.InternetZone` corrisponde a `PermissionSet` in condizioni di attendibilità parziale. Attualmente, senza `InternalsVisibleToAttribute`, non sarà possibile eseguire l'applicazione e verrà generata un'eccezione `SecurityException` che indica che membri non pubblici non possono essere serializzati in condizioni di attendibilità parziale.  
  
     Se al file di origine si aggiunge tuttavia la riga seguente, il programma viene eseguito correttamente.  
  
     [!code-csharp[CDF_WCF_SecurityConsiderationsForData#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/cdf_wcf_securityconsiderationsfordata/cs/program.cs#2)]  
  
## Altri problemi di gestione dello stato  
 È utile citare alcuni altri problemi riguardanti la gestione dello stato dell'oggetto:  
  
-   Quando si utilizza il modello di programmazione basato sul flusso con un trasporto di flusso, l'elaborazione del messaggio avviene immediatamente come arriva il messaggio. Il mittente può interrompere l'operazione di invio a metà del flusso, lasciando il codice in uno stato imprevedibile se è atteso altro contenuto. In generale è bene non dare per scontato che il flusso sia completo e non intervenire su operazioni basate sul flusso delle quali non è possibile eseguire il rollback nel caso il flusso venga interrotto. Quanto sopra si applica anche nel caso un messaggio sia in formato non valido dopo il corpo nel flusso, ad esempio, se il tag finale della busta SOAP è mancante o se è presente un secondo corpo del messaggio.  
  
-   L'utilizzo della funzione `IExtensibleDataObject` può causare l'emissione di dati sensibili. Se si accettano dati da un'origine non attendibile in contratti dati con `IExtensibleObjectData` che in seguito verranno riemessi in un canale sicuro in cui i messaggi sono firmati, potenzialmente si giustificano dati di cui non si hanno informazioni. Lo stato complessivo che si sta inviando potrebbe inoltre non essere valido se si tengono in considerazione sia le parti note sia quelle non note. Evitare questa situazione impostando selettivamente la proprietà dei dati di estensione su `null` o disattivando selettivamente la funzionalità `IExtensibleObjectData`.  
  
## Importazione di schemi  
 In genere, il processo di importazione dello schema per la generazione dei tipi avviene solo in fase di progettazione, quando si usa lo [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) in un servizio Web per generare una classe client. In scenari più avanzati è tuttavia possibile elaborare gli schemi in fase di esecuzione. È necessario essere consapevoli del fatto che così facendo ci si espone al rischio di attacchi Denial of Service. Per l'importazione di alcuni schemi può essere necessario molto tempo. Non utilizzare mai il componente per l'importazione di schemi <xref:System.Xml.Serialization.XmlSerializer> in tali scenari se gli schemi provengono da un'origine non attendibile.  
  
## Minacce specifiche dell'integrazione AJAX ASP.NET  
 Quando si implementa <xref:System.ServiceModel.Description.WebScriptEnablingBehavior> o <xref:System.ServiceModel.Description.WebHttpBehavior>, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] viene esposto un endpoint che può accettare sia i messaggi XML che quelli di tipo JSON. In ogni caso, esiste un unico set di quote di reader utilizzate da entrambi i lettori XML e JSON. Alcune quote di reader possono risultare appropriate per un lettore ma troppo grandi per l'altro.  
  
 Se si implementa `WebScriptEnablingBehavior`, si ha la possibilità di esporre un proxy JavaScript all'endpoint. È necessario considerare i seguenti problemi di sicurezza:  
  
-   Si possono ottenere informazioni sul servizio \(nomi di operazione, nomi di parametri e così via\), esaminando il proxy JavaScript.  
  
-   Se si utilizza l'endpoint JavaScript, si possono mantenere informazioni riservate nella cache del browser Web del client.  
  
## Nota sui componenti  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] è un sistema flessibile e personalizzabile. La maggior parte del contenuto di questo argomento verte sugli scenari di utilizzo più comuni in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]. È tuttavia possibile combinare i componenti disponibili in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] in molti modi diversi. È importante essere a conoscenza delle implicazioni per la protezione derivanti dall'utilizzo di ogni componente. In particolare:  
  
-   Quando è necessario utilizzare lettori XML, utilizzare i lettori forniti dalla classe <xref:System.Xml.XmlDictionaryReader> anziché qualsiasi altro lettore. Si creano lettori sicuri utilizzando <xref:System.Xml.XmlDictionaryReader.CreateTextReader%2A>, <xref:System.Xml.XmlDictionaryReader.CreateBinaryReader%2A> o metodi <xref:System.Xml.XmlDictionaryReader.CreateMtomReader%2A>. Non utilizzare il metodo <xref:System.Xml.XmlReader.Create%2A>. Configurare sempre i lettori con quote sicure. I motori di serializzazione di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] sono sicuri solo se utilizzati con lettori XML sicuri da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
-   Quando si utilizza la classe <xref:System.Runtime.Serialization.DataContractSerializer> per deserializzare dati potenzialmente non attendibili, impostare sempre la proprietà <xref:System.Runtime.Serialization.DataContractSerializer.MaxItemsInObjectGraph%2A>.  
  
-   Quando si crea un messaggio, impostare il parametro `maxSizeOfHeaders`  se `MaxReceivedMessageSize` non offre una protezione sufficiente.  
  
-   Quando si crea un codificatore, configurare sempre le relative quote, ad esempio `MaxSessionSize` e `MaxBufferSize`.  
  
-   Quando si utilizza un filtro XPath per i messaggi, impostare <xref:System.ServiceModel.Dispatcher.XPathMessageFilter.NodeQuota%2A> per limitare la quantità di nodi XML visitati dal filtro. Non utilizzare espressioni XPath che richiedono lunghi tempi di calcolo anche senza visitare molti nodi.  
  
-   In generale, quando si utilizza un componente che accetta quote, è necessario comprenderne le implicazioni a livello di sicurezza e impostarle su valori sicuri.  
  
## Vedere anche  
 <xref:System.Runtime.Serialization.DataContractSerializer>   
 <xref:System.Xml.XmlDictionaryReader>   
 <xref:System.Xml.Serialization.XmlSerializer>   
 [Tipi conosciuti di contratto dati](../../../../docs/framework/wcf/feature-details/data-contract-known-types.md)