---
title: "Panoramica dell&#39;architettura di trasferimento dei dati | Microsoft Docs"
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
  - "trasferimento dei dati [WCF], panoramica dell'architettura"
ms.assetid: 343c2ca2-af53-4936-a28c-c186b3524ee9
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# Panoramica dell&#39;architettura di trasferimento dei dati
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] può essere considerato un'infrastruttura di messaggistica. Può ricevere messaggi, elaborarli e inviarli a codice utente per ulteriori azioni, oppure può costruire messaggi dai dati forniti dal codice utente e recapitarli a una destinazione. In questo argomento, rivolto agli sviluppatori avanzati, viene illustrata l'architettura per la gestione dei messaggi e dei dati in essi contenuti. Per informazioni più semplici e orientate alle attività su come inviare e ricevere dati, vedere [Specifica del trasferimento di dati nei contratti di servizio](../../../../docs/framework/wcf/feature-details/specifying-data-transfer-in-service-contracts.md).  
  
> [!NOTE]
>  In questo argomento vengono illustrati i dettagli di implementazione di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] che non sono visibili esaminando il modello a oggetti di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]. In merito ai dettagli di implementazione documentati, è opportuno precisare due cose. In primo luogo, le descrizioni sono semplificate. L'implementazione effettiva potrebbe essere più complessa a causa delle ottimizzazioni o di altre ragioni. In secondo luogo, non fare mai affidamento su dettagli specifici di implementazione, nemmeno su quelli documentati, poiché possono cambiare senza preavviso da una versione all'altra o anche in una Service Release.  
  
## Architettura di base  
 Alla base delle funzionalità di gestione dei messaggi di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] vi è la classe <xref:System.ServiceModel.Channels.Message>, descritta dettagliatamente in [Utilizzo della classe Message](../../../../docs/framework/wcf/feature-details/using-the-message-class.md). I componenti runtime di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] possono essere suddivisi in due parti principali: lo stack dei canali e il framework dei servizi, il cui punto di connessione è rappresentato dalla classe <xref:System.ServiceModel.Channels.Message>.  
  
 Lo stack dei canali è responsabile della conversione tra un'istanza <xref:System.ServiceModel.Channels.Message> valida e una qualche azione che corrisponde all'invio o alla ricezione di dati del messaggio. Sul lato di invio, lo stack dei canali prende un'istanza <xref:System.ServiceModel.Channels.Message> valida e, dopo averla elaborata, esegue un'azione che corrisponde in modo logico all'invio del messaggio. L'azione potrebbe essere l'invio di pacchetti TCP o HTTP, la messa in coda del messaggio nel sistema di Accodamento messaggi, la scrittura del messaggio in un database, il suo salvataggio in una condivisione file o una qualsiasi altra azione, a seconda dell'implementazione. L'azione più comune è l'invio del messaggio su un protocollo di rete. Sul lato di ricezione, accade il contrario, ovvero viene rilevata un'azione \(che può essere l'arrivo di pacchetti TCP o HTTP o qualsiasi altra azione\) e, dopo l'elaborazione, lo stack dei canali converte questa azione in un'istanza <xref:System.ServiceModel.Channels.Message> valida.  
  
 È possibile utilizzare [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizzando direttamente la classe <xref:System.ServiceModel.Channels.Message> e lo stack dei canali. Questa procedura è tuttavia difficile e lunga. Inoltre, l'oggetto <xref:System.ServiceModel.Channels.Message> non fornisce supporto dei metadati, pertanto non è possibile generare client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] fortemente tipizzati se si utilizza [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] in questo modo.  
  
 In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] è incluso pertanto un framework del servizio che fornisce un modello di programmazione di facile utilizzo, per costruire e ricevere oggetti `Message`. Il framework del servizio esegue il mapping dei servizi ai tipi [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] attraverso la nozione dei contratti di servizio e invia messaggi a operazioni utente che sono semplicemente metodi [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] contrassegnati con l'attributo <xref:System.ServiceModel.OperationContractAttribute>. Per altre informazioni, vedere [Progettazione dei contratti di servizio](../../../../docs/framework/wcf/designing-service-contracts.md). Tali metodi possono avere parametri e valori restituiti. Sul lato del servizio, il framework del servizio converte le istanze <xref:System.ServiceModel.Channels.Message> in ingresso in parametri e i valori restituiti in istanze <xref:System.ServiceModel.Channels.Message> in uscita. Nel lato client, avviene il contrario. Si consideri ad esempio l'operazione `FindAirfare` seguente.  
  
 [!code-csharp[c_DataArchitecture#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_dataarchitecture/cs/source.cs#1)]
 [!code-vb[c_DataArchitecture#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_dataarchitecture/vb/source.vb#1)]  
  
 Si supponga che `FindAirfare` venga chiamato nel client. Il framework del servizio nel client converte i parametri `FromCity` e `ToCity` in un'istanza <xref:System.ServiceModel.Channels.Message> in uscita e la passa allo stack dei canali perché venga inviata.  
  
 Nel lato del servizio, quando un'istanza <xref:System.ServiceModel.Channels.Message> arriva dallo stack dei canali, il framework del servizio estrae i dati pertinenti dal messaggio per popolare i parametri `FromCity` e `ToCity`, quindi chiama il metodo `FindAirfare` nel lato servizio. Quando il metodo restituisce il risultato, il framework del servizio prende il valore integer restituito e il parametro di output `IsDirectFlight` e crea un'istanza dell'oggetto <xref:System.ServiceModel.Channels.Message> che contiene queste informazioni. Passa quindi l'istanza `Message` allo stack dei canali affinché venga inviata di nuovo al client.  
  
 Sul lato client, dallo stack dei canali emerge un'istanza <xref:System.ServiceModel.Channels.Message> che contiene il messaggio di risposta. Il framework del servizio estrae il valore restituito e il valore `IsDirectFlight` e li restituisce al chiamante del client.  
  
## Classe di messaggi  
 La classe <xref:System.ServiceModel.Channels.Message> è intesa per essere una rappresentazione astratta di un messaggio, ma la sua progettazione è fortemente legata al messaggio SOAP. Un <xref:System.ServiceModel.Channels.Message> contiene tre informazioni principali: il corpo, le intestazioni e le proprietà del messaggio.  
  
## Corpo del messaggio  
 Il corpo del messaggio ha lo scopo di rappresentare il payload effettivo dei dati del messaggio. Il corpo del messaggio è sempre rappresentato come un Infoset XML. Ciò non significa che tutti i messaggi creati o ricevuti in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] debbano essere in formato XML. È lo stack dei canali a decidere come interpretare il corpo del messaggio. Può emetterlo come XML, convertirlo in un altro formato o anche ometterlo completamente. Con la maggior parte dei fornitori di associazioni [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], ovviamente, il corpo del messaggio è rappresentato come contenuto XML nella sezione del corpo di una SOAP envelope.  
  
 È importante comprendere che la classe `Message` non contiene necessariamente un buffer con dati XML che rappresentano il corpo. Logicamente, `Message` contiene un Infoset XML, che può essere creato dinamicamente e può non essere mai fisicamente presente in memoria.  
  
### Inserimento di dati nel corpo del messaggio  
 Non esiste un meccanismo uniforme per inserire dati in un corpo del messaggio. La classe <xref:System.ServiceModel.Channels.Message> ha un metodo astratto, <xref:System.ServiceModel.Channels.Message.OnWriteBodyContents%28System.Xml.XmlDictionaryWriter%29>, che prende un <xref:System.Xml.XmlDictionaryWriter>. Ogni sottoclasse della classe <xref:System.ServiceModel.Channels.Message> è responsabile dell'esecuzione dell'override di questo metodo e della scrittura del suo contenuto. Il corpo del messaggio contiene logicamente l'Infoset XML prodotto da `OnWriteBodyContent`. Si consideri ad esempio la sottoclasse seguente `Message`.  
  
 [!code-csharp[c_DataArchitecture#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_dataarchitecture/cs/source.cs#2)]
 [!code-vb[c_DataArchitecture#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_dataarchitecture/vb/source.vb#2)]  
  
 Fisicamente, un'istanza `AirfareRequestMessage` contiene solo due stringhe \("fromCity" e "toCity"\). Tuttavia, il messaggio contiene logicamente l'infoset XML seguente:  
  
```  
<airfareRequest>  
    <from>Tokyo</from>  
    <to>London</to>  
</airfareRequest>  
```  
  
 In genere questo non è il metodo utilizzato per creare messaggi, perché è possibile utilizzare il framework del servizio per creare un messaggio come il precedente dai parametri del contratto dell'operazione. La classe <xref:System.ServiceModel.Channels.Message>, inoltre, ha metodi `CreateMessage` statici che è possibile utilizzare per creare messaggi con tipi di contenuto comuni: un messaggio vuoto, un messaggio che contiene un oggetto serializzato in XML con <xref:System.Runtime.Serialization.DataContractSerializer>, un messaggio che contiene un errore SOAP, un messaggio che contiene XML rappresentato da un <xref:System.Xml.XmlReader>e così via.  
  
### Ottenimento di dati da un corpo del messaggio  
 Esistono due modalità principali per estrarre i dati archiviati in un corpo del messaggio:  
  
-   È possibile ottenere l'intero corpo del messaggio chiamando il metodo <xref:System.ServiceModel.Channels.Message.WriteBodyContents%28System.Xml.XmlDictionaryWriter%29> e passando contemporaneamente un writer XML. L'intero corpo del messaggio viene scritto in questo writer. L'ottenimento contemporaneo dell'intero corpo del messaggio viene detto anche *scrittura di un messaggio*. La scrittura viene eseguita principalmente dallo stack dei canali all'invio dei messaggi. Parte dello stack dei canali di solito otterrà l'accesso all'intero corpo del messaggio, lo codificherà e l'invierà.  
  
-   Un'altra modalità per estrarre informazioni dal corpo del messaggio consiste nel chiamare <xref:System.ServiceModel.Channels.Message.GetReaderAtBodyContents> e ottenere un lettore XML. Se necessario, sarà quindi possibile accedere al corpo del messaggio in sequenza, chiamando i metodi nel lettore. L'ottenimento del corpo del messaggio un pezzo alla volta viene detto anche *lettura di un messaggio*. La lettura del messaggio è utilizzata principalmente dal framework del servizio alla ricezione dei messaggi. Quando, ad esempio, è utilizzato <xref:System.Runtime.Serialization.DataContractSerializer>, il framework del servizio otterrà un lettore XML sul corpo e lo passerà al motore di deserializzazione che avvierà la lettura del messaggio, elemento per elemento, e costruirà l'oggetto grafico corrispondente.  
  
 Un corpo del messaggio può essere recuperato solo una volta. Ciò consente di lavorare con flussi di tipo forward\-only. È ad esempio possibile scrivere un override <xref:System.ServiceModel.Channels.Message.OnWriteBodyContents%28System.Xml.XmlDictionaryWriter%29> che legge da un <xref:System.IO.FileStream> e restituisce i risultati come Infoset XML. Non sarà mai necessario tornare all'inizio del file.  
  
 I metodi `WriteBodyContents` e `GetReaderAtBodyContents` controllano semplicemente che il corpo del messaggio non sia mai stato recuperato, quindi chiamano rispettivamente `OnWriteBodyContents` o `OnGetReaderAtBodyContents`.  
  
## Utilizzo di messaggi in WCF  
 La maggior parte dei messaggi può essere classificata come *in uscita* \(quelli che vengono creati dal framework del servizio per essere inviati dallo stack dei canali\) o *in ingresso* \(quelli che arrivano dallo stack dei canali e sono interpretati dal framework del servizio\). Lo stack di canali può inoltre operare in modalità di memorizzazione nel buffer o in modalità flusso. Il framework del servizio può anche esporre un modello di programmazione con o senza invio nel flusso. Ciò porta ai casi elencati nella tabella seguente assieme ai dettagli semplificati della loro implementazione.  
  
|Tipo messaggio|Dati del corpo nel messaggio|Implementazione della scrittura \(OnWriteBodyContents\)|Implementazione della lettura \(OnGetReaderAtBodyContents\)|  
|--------------------|----------------------------------|-------------------------------------------------------------|-----------------------------------------------------------------|  
|In uscita, creato da un modello di programmazione senza invio nel flusso|I dati necessario per scrivere il messaggio \(ad esempio, un oggetto e l'istanza <xref:System.Runtime.Serialization.DataContractSerializer> necessaria per serializzarlo\)\*|Logica personalizzata per scrivere il messaggio sulla base dei dati archiviati \(ad esempio, chiamare `WriteObject` su `DataContractSerializer` se questo è il serializzatore utilizzato\)\*|Chiamare `OnWriteBodyContents`, memorizzare nel buffer i risultati, restituire un lettore XML sul buffer|  
|In uscita, creato dal modello di programmazione con invio nel flusso|`Stream` con i dati da scrivere\*|Scrivere i dati dal flusso archiviato utilizzando il meccanismo <xref:System.Xml.IStreamProvider>\*|Chiamare `OnWriteBodyContents`, memorizzare nel buffer i risultati, restituire un lettore XML sul buffer|  
|In ingresso dallo stack dei canali del flusso|Un oggetto `Stream` che rappresenta i dati che entrano sulla rete con un <xref:System.Xml.XmlReader> su di esso|Scrivere il contenuto dal `XmlReader` archiviato utilizzando `WriteNode`|Restituisce il `XmlReader` archiviato|  
|In ingresso dallo stack dei canali senza utilizzo del flusso|Un buffer che contiene dati del corpo con un `XmlReader` su di esso|Scrive il contenuto dal `XmlReader` archiviato utilizzando `WriteNode`|Restituisce il lang archiviato|  
  
 \* Questi elementi non vengono implementati direttamente nelle sottoclassi `Message`, ma in sottoclassi della classe <xref:System.ServiceModel.Channels.BodyWriter>. Per altre informazioni su <xref:System.ServiceModel.Channels.BodyWriter>, vedere [Utilizzo della classe Message](../../../../docs/framework/wcf/feature-details/using-the-message-class.md).  
  
## Intestazioni del messaggio  
 Un messaggio può contenere intestazioni. Un'intestazione è costituita in modo logico da un Infoset XML a cui sono associati un nome, uno spazio dei nomi e alcune altre proprietà. Alle intestazioni messaggio si accede utilizzando la proprietà `Headers` su <xref:System.ServiceModel.Channels.Message>. Ogni intestazione è rappresentata da una classe <xref:System.ServiceModel.Channels.MessageHeader>. Le intestazioni messaggio in genere vengono mappate su intestazioni messaggio SOAP quando si utilizza uno stack dei canali configurato per lavorare con messaggi SOAP.  
  
 L'inserimento e l'estrazione di informazioni in e da un'intestazione messaggio sono simili all'utilizzo del corpo del messaggio. Il processo è leggermente semplificato perché il flusso non è supportato. È possibile accedere al contenuto della stessa intestazione più di una volta e accedere alle intestazioni in ordine arbitrario, forzando le intestazioni a essere sempre memorizzate nel buffer. Non esiste nessun meccanismo generico disponibile per ottenere un lettore XML su un'intestazione, ma esiste una sottoclasse `MessageHeader` interna a [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] che rappresenta un'intestazione leggibile con tale funzionalità. Questo tipo di `MessageHeader` viene creato dallo stack dei canali all'arrivo di un messaggio con intestazioni dell'applicazione personalizzate. Ciò consente al framework del servizio di utilizzare un motore di deserializzazione, ad esempio <xref:System.Runtime.Serialization.DataContractSerializer>, per interpretare queste intestazioni.  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Utilizzo della classe Message](../../../../docs/framework/wcf/feature-details/using-the-message-class.md).  
  
## Proprietà del messaggio  
 Un messaggio può contenere proprietà. Una *proprietà* è qualsiasi oggetto [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] associato a un nome di stringa. Alle proprietà si accede tramite la proprietà `Properties` su `Message`.  
  
 Contrariamente al corpo del messaggio e alle intestazioni messaggio \(che in genere eseguono il mapping rispettivamente al corpo SOAP e alle intestazioni SOAP\), le proprietà normalmente non vengono inviate o ricevute insieme ai messaggi. La funzione principale delle proprietà del messaggio è quella di fungere da meccanismo di comunicazione per passare dati sul messaggio tra i vari canali nello stack dei canali e tra lo stack dei canali e il modello di servizio.  
  
 Il canale di trasporto HTTP, ad esempio, incluso come parte di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] è in grado di produrre vari codici di stato HTTP, ad esempio "404 \(Non trovato\)" e "500 \(Errore interno del server\)", quando invia risposte ai client. Prima di inviare un messaggio di risposta, viene eseguito un controllo per vedere se le `Properties` del `Message` contengono una proprietà chiamata "httpResponse" che contiene un oggetto di tipo <xref:System.ServiceModel.Channels.HttpResponseMessageProperty>. Se tale proprietà risulta presente, esaminerà la proprietà <xref:System.ServiceModel.Channels.HttpResponseMessageProperty.StatusCode%2A> e utilizzerà quel codice di stato. Se non la trova, viene utilizzato il codice predefinito "200 \(OK\)".  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Utilizzo della classe Message](../../../../docs/framework/wcf/feature-details/using-the-message-class.md).  
  
### Il messaggio nel suo insieme  
 Finora, sono stati illustrati i metodi per accedere separatamente alle varie parti del messaggio. La classe <xref:System.ServiceModel.Channels.Message> fornisce tuttavia anche dei metodi per lavorare su tutto il messaggio. Il metodo `WriteMessage`, ad esempio, scrive l'intero messaggio in un writer XML.  
  
 Affinché ciò sia possibile, è necessario definire un mapping tra l'intera istanza `Message` e un Infoset XML. Questo mapping, di fatto, esiste: [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza lo standard SOAP per definirlo. Quando un'istanza `Message` viene scritta come Infoset XML, l'Infoset risultante è la SOAP envelope valida che contiene il messaggio. Pertanto, `WriteMessage` eseguirebbe in genere i passaggi seguenti:  
  
1.  Scrivere il tag di apertura dell'elemento SOAP envelope.  
  
2.  Scrivere il tag di apertura dell'elemento intestazione SOAP, scrivere tutte le intestazioni e chiudere l'elemento intestazione.  
  
3.  Scrivere il tag di apertura dell'elemento corpo SOAP.  
  
4.  Chiamare `WriteBodyContents` o un metodo equivalente per scrivere il corpo.  
  
5.  Chiudere gli elementi corpo ed envelope.  
  
 I passaggi precedenti sono strettamente legati allo standard SOAP. Una complicazione deriva dal fatto che esistono più versioni di SOAP. È ad esempio impossibile scrivere correttamente l'elemento SOAP envelope senza sapere qual è la versione SOAP utilizzata. In alcuni casi, inoltre, potrebbe essere auspicabile disattivare completamente questo mapping complesso specifico di SOAP.  
  
 A tale scopo, in `Version` viene fornita una proprietà `Message`. Può essere impostata sulla versione SOAP da utilizzare quando si scrive il messaggio, oppure su `None` per impedire qualsiasi mapping specifico di SOAP. Se la proprietà `Version` è impostata su `None`, i metodi che lavorano con il messaggio intero operano come se il messaggio fosse costituito unicamente dal suo corpo. `WriteMessage`, ad esempio, chiamerebbe semplicemente `WriteBodyContents` invece di eseguire i diversi passaggi elencati sopra. È previsto che, sui messaggi in arrivo, `Version` verrà automaticamente rilevata e impostata correttamente.  
  
## Stack dei canali  
  
### Canali  
 Come già indicato, lo stack dei canali è responsabile della conversione di istanze <xref:System.ServiceModel.Channels.Message> in uscita in un'azione \(ad esempio l'invio di pacchetti sulla rete\) o della conversione di un'azione \(ad esempio la ricezione di pacchetti di rete\) in istanze `Message` in ingresso.  
  
 Lo stack dei canali è composto da uno o più canali ordinati in una sequenza. Un'istanza `Message` in uscita viene passata al primo canale nello stack \(chiamato anche *canale superiore*\) che lo passa al canale successivo lungo lo stack e così via. Il messaggio termina nell'ultimo canale, chiamato *canale di trasporto*. I messaggi in arrivo hanno origine nel canale di trasporto e vengono passati di canale in canale lungo lo stack. Dal canale principale, il messaggio viene in genere passato nel framework del servizio. Anche se questo è il modello abituale per i messaggi dell'applicazione, alcuni canali potrebbero funzionare in modo leggermente diverso. Potrebbero, ad esempio, inviare i messaggi della propria infrastruttura senza che venga loro passato un messaggio da un canale superiore.  
  
 I canali possono operare sul messaggio in vari modi, mentre transita nello stack. L'operazione più comune consiste nell'aggiungere un'intestazione a un messaggio in uscita e nel leggere le intestazioni in un messaggio in arrivo. Un canale può, ad esempio, calcolare la firma digitale di un messaggio e aggiungerla come intestazione. Un canale può anche controllare tale intestazione di firma digitale sui messaggi in arrivo e impedire che quelli senza una firma valida risalgano lo stack dei canali. I canali, inoltre, spesso impostano o controllano le proprietà dei messaggi. Il corpo del messaggio in genere non viene modificato, anche se ciò è consentito. Il canale di sicurezza [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], ad esempio, può crittografare il corpo del messaggio.  
  
### Canali di trasporto e codificatori di messaggi  
 Il canale inferiore nello stack è responsabile della trasformazione effettiva in un'azione di un <xref:System.ServiceModel.Channels.Message> in uscita, modificato da altri canali. Sul lato ricevente, questo è il canale che converte un'azione in un `Message` che viene elaborato dagli altri canali.  
  
 Come già indicato, le azioni possono essere diverse: invio o ricezione di pacchetti di rete su vari protocolli, lettura o scrittura del messaggio in un database, oppure messa in coda o rimozione del messaggio da una coda di Accodamento messaggi e così via. Tutte queste azioni hanno una caratteristica comune: richiedono una trasformazione tra l'istanza [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]`Message` e un gruppo effettivo di byte che possono essere inviati, ricevuti, letti, scritti, messi in coda o rimossi dalla coda. Il processo di conversione di un `Message` in un gruppo di byte è detto *codifica*, mentre il processo inverso di creazione di un `Message` da un gruppo di byte è detto *decodifica*.  
  
 La maggior parte dei canali di trasporto utilizza componenti detti *codificatori di messaggi* destinati ad eseguire la codifica e la decodifica. Un codificatore di messaggi è una sottoclasse della classe <xref:System.ServiceModel.Channels.MessageEncoder>.`MessageEncoder` include vari overload dei metodi `ReadMessage` e `WriteMessage` per eseguire la conversione tra `Message` e gruppi di byte.  
  
 Sul lato di invio, un canale di trasporto di memorizzazione nel buffer passa l'oggetto `Message` ricevuto da un canale sovrastante a `WriteMessage`. Di ritorno, riceve una matrice di byte che utilizzerà poi per eseguire l'azione \(ad esempio assemblare questi byte come pacchetti TCP validi e inviarli alla destinazione corretta\). Un canale di trasporto del flusso crea innanzitutto un `Stream` \(ad esempio, sulla connessione TCP in uscita\), quindi passa sia lo `Stream` che il `Message` da inviare all'overload `WriteMessage` appropriato che scrive il messaggio.  
  
 Sul lato ricevente, un canale di trasporto di memorizzazione nel buffer estrae i byte in ingresso \(ad esempio, dai pacchetti TCP in ingresso\) in una matrice e chiama `ReadMessage` per ottenere un oggetto `Message` che può passare più avanti nello stack dei canali. Un canale di trasporto del flusso crea un oggetto `Stream` \(ad esempio, un flusso di rete sulla connessione TCP in ingresso\) e lo passa a `ReadMessage` per ottenere un oggetto `Message`.  
  
 La separazione tra i canali di trasporto e il codificatore di messaggi non è obbligatoria. È possibile scrivere un canale di trasporto che non utilizza un codificatore di messaggi. Il vantaggio di questa separazione, tuttavia, è la facilità di composizione. Finché un canale di trasporto utilizza solo <xref:System.ServiceModel.Channels.MessageEncoder> di base,  può funzionare con qualsiasi codificatore di messaggi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] o di terze parti. Analogamente, lo stesso codificatore può essere normalmente utilizzato in qualsiasi canale di trasporto.  
  
### Operazione del codificatore messaggi  
 Per descrivere l'operazione tipica di un codificatore, è opportuno considerare i quattro casi seguenti.  
  
|Operazione|Commento|  
|----------------|--------------|  
|Codifica, memorizzata nel buffer|In modalità di memorizzazione nel buffer, il codificatore crea un buffer  di dimensioni variabili, dopo di che crea un writer XML su di esso. Chiama quindi <xref:System.ServiceModel.Channels.Message.WriteMessage%28System.Xml.XmlWriter%29> sul messaggio in fase di codifica, per scrivere le intestazioni e il corpo utilizzando <xref:System.ServiceModel.Channels.Message.WriteBodyContents%28System.Xml.XmlDictionaryWriter%29>, come spiegato nella sezione precedente di questo argomento su `Message`. Viene infine restituito il contenuto del buffer \(rappresentato come matrice di byte\) che deve essere utilizzato dal canale di trasporto.|  
|Codifica, trasmessa|In modalità con invio nel flusso, l'operazione è simile a quanto sopra, ma più semplice. Non è necessario alcun buffer. In genere viene creato un writer XML sopra il flusso e viene chiamato <xref:System.ServiceModel.Channels.Message.WriteMessage%28System.Xml.XmlWriter%29> sul `Message` per scriverlo in questo writer.|  
|Decodifica, memorizzata nel buffer|In caso di decodifica in modalità di memorizzazione nel buffer, in genere viene creata una speciale sottoclasse `Message` che contiene i dati memorizzati nel buffer. Vengono lette le intestazioni messaggio e viene creato un lettore XML posizionato sul corpo del messaggio. Si tratta del lettore che verrà restituito con <xref:System.ServiceModel.Channels.Message.GetReaderAtBodyContents>.|  
|Decodifica, trasmessa|In caso di decodifica in modalità con invio nel flusso, in genere viene creata una speciale sottoclasse messaggio. Il flusso viene fatto avanzare solo quel tanto che è sufficiente per leggere tutte le intestazioni e posizionarlo sul corpo del messaggio. Sul flusso viene quindi creato un lettore XML. Si tratta del lettore che verrà restituito con <xref:System.ServiceModel.Channels.Message.GetReaderAtBodyContents>.|  
  
 I codificatori possono eseguire anche altre funzioni. Possono, ad esempio, inserire in un pool i lettori e i writer XML. Creare un nuovo lettore o writer XML ogni volta che è richiesto, è oneroso. I codificatori, pertanto, gestiscono un pool di lettori e un pool di writer di dimensioni configurabili. Nelle descrizioni dell'operazione del codificatore illustrata in precedenza l'espressione "creare un lettore\/writer XML" in genere significa "prenderne uno dal pool oppure crearlo se non è disponibile". Il codificatore \(insieme alle sottoclassi `Message` che crea durante la decodifica\) contiene la logica necessaria per restituire lettori e scrittori ai pool quando non sono più necessari, ad esempio quando `Message` viene chiuso.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] fornisce tre codificatori di messaggi, anche se è possibile crearne tipi aggiuntivi personalizzati. I tipi forniti sono testo, binario e MTOM \(Message Transmission Optimization Mechanism\). La descrizione dettagliata è disponibile in [Scelta di un codificatore di messaggi](../../../../docs/framework/wcf/feature-details/choosing-a-message-encoder.md).  
  
### Interfaccia IStreamProvider  
 Quando si scrive in un writer XML un messaggio in uscita che contiene un corpo inviato nel flusso, <xref:System.ServiceModel.Channels.Message> utilizza una sequenza di chiamate simili alle seguenti nell'implementazione di <xref:System.ServiceModel.Channels.Message.OnWriteBodyContents%28System.Xml.XmlDictionaryWriter%29>:  
  
-   Scrivere tutte le informazioni necessarie che precedono il flusso \(ad esempio, il tag di apertura XML\).  
  
-   Scrivere il flusso.  
  
-   Scrivere tutte le informazioni dopo il flusso \(ad esempio, il tag di chiusura XML\).  
  
 Questa procedura funziona bene con codifiche simili alla codifica XML testuale. Esistono, tuttavia, alcune codifiche che non inseriscono informazioni InfoSet XML \(ad esempio, i tag di inizio e fine di elementi XML\) insieme ai dati contenuti all'interno di elementi. Nella codifica MTOM, ad esempio, il messaggio è suddiviso in più parti. Una parte contiene l'InfoSet XML, che può contenere riferimenti ad altre parti per il contenuto effettivo degli elementi. Dato che, in genere, l'InfoSet XML è di piccole dimensioni rispetto al contenuto inviato nel flusso, è consigliabile memorizzarlo nel buffer, scriverlo e quindi scrivere il contenuto in un flusso. Ciò significa che quando viene scritto il tag dell'elemento di chiusura, il flusso non dovrebbe essere stato ancora scritto.  
  
 A tale fine, viene utilizzata l'interfaccia <xref:System.Xml.IStreamProvider>. L'interfaccia ha un metodo <xref:System.Xml.IStreamProvider.GetStream> che restituisce il flusso da scrivere. La modalità corretta per scrivere il corpo di un messaggio inviato in un flusso in <xref:System.ServiceModel.Channels.Message.OnWriteBodyContents%28System.Xml.XmlDictionaryWriter%29> è la seguente:  
  
1.  Scrivere tutte le informazioni necessarie che precedono il flusso \(ad esempio, il tag di apertura XML\).  
  
2.  Chiamare l'overload `WriteValue` in <xref:System.Xml.XmlDictionaryWriter> che prende un <xref:System.Xml.IStreamProvider>, con un'implementazione `IStreamProvider` che restituisce il flusso da scrivere.  
  
3.  Scrivere tutte le informazioni dopo il flusso \(ad esempio, il tag di chiusura XML\).  
  
 Con questo approccio, il writer XML può scegliere quando chiamare <xref:System.Xml.IStreamProvider.GetStream> e scrivere i dati inviati nel flusso. I writer XML binari e testuali, ad esempio, lo chiameranno immediatamente e scriveranno il contenuto inviato nel flusso tra il tag di inizio e quello di fine. Il writer MTOM può decidere di chiamare <xref:System.Xml.IStreamProvider.GetStream> in un secondo momento, quando è pronto per scrivere la parte appropriata del messaggio.  
  
## Rappresentazione di dati in framework del servizio  
 Come dichiarato nella sezione "Architettura di base" di questo argomento, il framework del servizio è la parte di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] che, tra le altre cose, è responsabile della conversione tra un modello di programmazione di facile uso per dati del messaggio e le istanze `Message` effettive. Uno scambio di messaggi viene in genere rappresentato nel framework del servizio come metodo [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] contrassegnato con l'attributo <xref:System.ServiceModel.OperationContractAttribute>. Il metodo può prendere alcuni parametri e restituire un valore restituito o parametri out \(o entrambi\). Sul lato servizio, i parametri di input rappresentano il messaggio in arrivo, mentre il valore restituito e i parametri out rappresentano il messaggio in uscita. Sul lato client, è vero il contrario. Il modello di programmazione per descrivere i messaggi tramite parametri e il valore restituito vengono illustrati dettagliatamente in [Specifica del trasferimento di dati nei contratti di servizio](../../../../docs/framework/wcf/feature-details/specifying-data-transfer-in-service-contracts.md). Contenuto della sezione verrà fornita una breve panoramica.  
  
## Modelli di programmazione  
 Il framework del servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] supporta cinque diversi modelli di programmazione per descrivere i messaggi:  
  
### 1. Messaggio vuoto  
 Questo è il caso più semplice. Per descrivere un messaggio in arrivo vuoto, non utilizzare parametri di input.  
  
 [!code-csharp[C_DataArchitecture#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_dataarchitecture/cs/source.cs#3)]
 [!code-vb[C_DataArchitecture#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_dataarchitecture/vb/source.vb#3)]  
  
 Per descrivere un messaggio in uscita vuoto, utilizzare un valore restituito vuoto e non utilizzare nessun parametro out:  
  
 [!code-csharp[C_DataArchitecture#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_dataarchitecture/cs/source.cs#4)]
 [!code-vb[C_DataArchitecture#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_dataarchitecture/vb/source.vb#4)]  
  
 Si noti che questa procedura è diversa da un contratto dell'operazione unidirezionale:  
  
 [!code-csharp[C_DataArchitecture#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_dataarchitecture/cs/source.cs#5)]
 [!code-vb[C_DataArchitecture#5](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_dataarchitecture/vb/source.vb#5)]  
  
 Nell'esempio `SetDesiredTemperature`, viene illustrato un modello di scambio di messaggio bidirezionale. Dall'operazione viene restituito un messaggio, ma è vuoto. L'operazione può restituire un errore. Nell'esempio "Set Lightbulb", il modello di scambio di messaggi è unidirezionale, pertanto non c'è nessun messaggio in uscita da descrivere. In questo caso, il servizio non può comunicare nessuno stato al client.  
  
### 2. Utilizzo diretto della classe messaggio  
 È possibile utilizzare direttamente la classe <xref:System.ServiceModel.Channels.Message> \(o una delle sue sottoclassi\) in un contratto dell'operazione. In questo caso, il framework del servizio passa unicamente `Message` dall'operazione allo stack dei canali e viceversa, senza ulteriore elaborazione.  
  
 L'utilizzo diretto di `Message` è consigliato principalmente in due casi. È possibile utilizzarlo per scenari avanzati, quando nessuno degli altri modelli di programmazione offre flessibilità sufficiente per descrivere il messaggio. Si potrebbe, ad esempio, voler utilizzare file su disco per descrivere un messaggio, con le proprietà file che diventano intestazioni messaggio e il contenuto del file che diventa il corpo del messaggio. A questo punto, è possibile creare un codice simile al seguente.  
  
 [!code-csharp[C_DataArchitecture#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_dataarchitecture/cs/source.cs#6)]
 [!code-vb[C_DataArchitecture#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_dataarchitecture/vb/source.vb#6)]  
  
 Il secondo utilizzo comune per `Message` in un contratto dell'operazione è quando un servizio non tiene conto dello specifico contenuto del messaggio e si comporta come se fosse una black box. Potrebbe, ad esempio, esservi un servizio che inoltra i messaggi a più destinatari diversi. Il contratto può essere scritto come segue.  
  
 [!code-csharp[C_DataArchitecture#7](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_dataarchitecture/cs/source.cs#7)]
 [!code-vb[C_DataArchitecture#7](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_dataarchitecture/vb/source.vb#7)]  
  
 La riga Action\="\*" disattiva l'invio dei messaggi e assicura che tutti quelli inviati al contratto `IForwardingService` arrivino all'operazione `ForwardMessage`. In genere, il dispatcher esaminerebbe l'intestazione "Action" del messaggio per determinare a quale operazione è destinato. Action\="\*" significa "tutti i valori possibili dell'intestazione Action". La combinazione di Action\="\*" e l'utilizzo di Message come parametro è nota come "contratto universale" perché è in grado di ricevere tutti i messaggi possibili. Per poter inviare tutti i messaggi possibili, utilizzare Message come valore restituito e impostare `ReplyAction` su "\*". Ciò impedirà al framework del servizio di aggiungere la propria intestazione Action, permettendogli di controllarla utilizzando l'oggetto `Message` restituito.  
  
### 3. Contratti di messaggio  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] fornisce un modello di programmazione dichiarativa per descrivere i messaggi, chiamato *contratti di messaggio*. Questo modello viene descritto dettagliatamente in [Utilizzo dei contratti di messaggio](../../../../docs/framework/wcf/feature-details/using-message-contracts.md). Essenzialmente, tutto il messaggio è rappresentato da un singolo tipo di [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] che utilizza attributi quali <xref:System.ServiceModel.MessageBodyMemberAttribute> e <xref:System.ServiceModel.MessageHeaderAttribute> per descrivere le parti della classe del contratto di messaggio di cui eseguire il mapping su determinate parti del messaggio.  
  
 I contratti di messaggio forniscono un grande controllo sulle istanze `Message` risultanti, anche se, ovviamente, non pari a quello assicurato dall'utilizzo diretto della classe `Message`. I corpi dei messaggi, ad esempio, spesso sono composti da più informazioni, ognuna delle quali è rappresentata da un proprio elemento XML. Questi elementi possono verificarsi direttamente nel corpo \(modalità*bare*\) oppure possono essere *incapsulati* in un elemento XML. L'utilizzo del modello di programmazione di contratto di messaggio consente di decidere se utilizzare lo stile bare o quello incapsulato e controllare il nome wrapper e lo spazio dei nomi.  
  
 Nell'esempio di codice seguente di un contratto di messaggio vengono illustrate queste funzionalità.  
  
 [!code-csharp[C_DataArchitecture#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_dataarchitecture/cs/source.cs#9)]
 [!code-vb[C_DataArchitecture#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_dataarchitecture/vb/source.vb#9)]  
  
 Gli elementi contrassegnati per essere serializzati \(con <xref:System.ServiceModel.MessageBodyMemberAttribute>, <xref:System.ServiceModel.MessageHeaderAttribute> o altri attributi correlati\) devono essere serializzabili per partecipare a un contratto di messaggio.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] la sezione "Serializzazione" più avanti in questo argomento.  
  
### 4. Parametri  
 Spesso, uno sviluppatore che desidera descrivere un'operazione che influenza più blocchi di dati non ha bisogno del livello di controllo fornito dai contratti di messaggio. Quando si creano nuovi servizi, ad esempio, in genere non si desidera decidere se scegliere lo stile bare o quello incapsulato o il nome dell'elemento wrapper. Queste decisioni spesso richiedono una profonda conoscenza dei servizi Web e di SOAP.  
  
 Il framework del servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] può scegliere automaticamente la rappresentazione SOAP migliore e più interoperativa per l'invio o la ricezione di più informazioni correlate, senza imporre queste scelte sull'utente. A tale fine, è sufficiente descrivere queste informazioni come parametri o valori restituiti di un contratto dell'operazione. Si consideri ad esempio il contratto dell'operazione seguente:  
  
 [!code-csharp[C_DataArchitecture#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_dataarchitecture/cs/source.cs#11)]
 [!code-vb[C_DataArchitecture#11](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_dataarchitecture/vb/source.vb#11)]  
  
 Il framework del servizio decide automaticamente di inserire tutte e tre le informazioni \(`customerID`, `item` e `quantity`\) nel corpo del messaggio e di incapsularle in un elemento wrapper chiamato `SubmitOrderRequest`.  
  
 L'approccio consigliato è quello di descrivere le informazioni da inviare o ricevere come un semplice elenco di parametri del contratto dell'operazione, a meno che non vi siano delle ragioni speciali per passare al contratto di messaggio più complesso o a modelli di programmazione basati su `Message`.  
  
### 5. Flusso  
 L'utilizzo di `Stream` o di una delle sue sottoclassi in un contratto dell'operazione o come parte unica del corpo del messaggio in un contratto di messaggio può essere considerato un modello di programmazione separato da quelli descritti sopra. Utilizzare `Stream` in questo modo è l'unica possibilità per garantire che il contratto sia utilizzabile in un flusso, a meno che non si scriva una sottoclasse `Message` compatibile con il flusso.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Dati di grandi dimensioni e flussi](../../../../docs/framework/wcf/feature-details/large-data-and-streaming.md).  
  
 Quando `Stream` o una delle sottoclassi vengono utilizzati in questo modo, il serializzatore non viene richiamato. Per i messaggi in uscita, viene creata una sottoclasse `Message` speciale di flusso e il flusso viene scritto come descritto nella sezione sull'interfaccia <xref:System.Xml.IStreamProvider>. Per i messaggi in arrivo, il framework del servizio crea una sottoclasse `Stream` sul messaggio in arrivo e la fornisce all'operazione.  
  
## Restrizioni relative al modello di programmazione  
 I modelli di programmazione descritti sopra non possono essere combinati arbitrariamente. Se, ad esempio, un'operazione accetta un tipo di contratto di messaggio, il contratto di messaggio deve essere il suo unico parametro di input. L'operazione, inoltre, deve restituire un messaggio vuoto \(il tipo restituito deve essere void\) o un altro contratto di messaggio. Queste restrizioni del modello di programmazione vengono descritte negli argomenti per ogni modello di programmazione specifico: [Utilizzo dei contratti di messaggio](../../../../docs/framework/wcf/feature-details/using-message-contracts.md), [Utilizzo della classe Message](../../../../docs/framework/wcf/feature-details/using-the-message-class.md) e [Dati di grandi dimensioni e flussi](../../../../docs/framework/wcf/feature-details/large-data-and-streaming.md).  
  
## Formattatori dei messaggi  
 I modelli di programmazione descritti sopra sono supportati inserendo nel framework del servizio componenti denominati *formattatori dei messaggi*. I formattatori dei messaggi sono tipi che implementano l'interfaccia <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter> o <xref:System.ServiceModel.Dispatcher.IDispatchMessageFormatter> o entrambe, da utilizzare rispettivamente in client e client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] del servizio.  
  
 I formattatori dei messaggi normalmente sono inseriti da comportamenti.<xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior>, ad esempio, inserisce il formattatore dei messaggi di contratto dati. Questa operazione viene eseguita sul lato servizio impostando <xref:System.ServiceModel.Dispatcher.DispatchOperation.Formatter%2A> sul formattatore corretto nel metodo <xref:System.ServiceModel.Description.IOperationBehavior.ApplyDispatchBehavior%28System.ServiceModel.Description.OperationDescription%2CSystem.ServiceModel.Dispatcher.DispatchOperation%29> oppure sul lato client impostando <xref:System.ServiceModel.Dispatcher.ClientOperation.Formatter%2A> sul formattatore corretto nel metodo <xref:System.ServiceModel.Description.IOperationBehavior.ApplyClientBehavior%28System.ServiceModel.Description.OperationDescription%2CSystem.ServiceModel.Dispatcher.ClientOperation%29>.  
  
 Nelle tabelle seguenti sono elencati i metodi che possono essere implementati da un formattatore dei messaggi.  
  
|Interfaccia|Metodo|Operazione|  
|-----------------|------------|----------------|  
|<xref:System.ServiceModel.Dispatcher.IDispatchMessageFormatter>|[DeserializeRequest\(Message, Object\<xref:System.ServiceModel.Dispatcher.IDispatchMessageFormatter.DeserializeRequest%28System.ServiceModel.Channels.Message%2CSystem.Object%5B%5D%29>|Converte un `Message` in ingresso in parametri dell'operazione|  
|<xref:System.ServiceModel.Dispatcher.IDispatchMessageFormatter>|[SerializeReply\(MessageVersion, Object\<xref:System.ServiceModel.Dispatcher.IDispatchMessageFormatter.SerializeReply%28System.ServiceModel.Channels.MessageVersion%2CSystem.Object%5B%5D%2CSystem.Object%29>|Crea un `Message` in uscita dal valore restituito\/parametri out dell'operazione|  
|<xref:System.ServiceModel.Dispatcher.IClientMessageFormatter>|[SerializeRequest\(MessageVersion, Object\<xref:System.ServiceModel.Dispatcher.IClientMessageFormatter.SerializeRequest%28System.ServiceModel.Channels.MessageVersion%2CSystem.Object%5B%5D%29>|Crea un `Message` in uscita dai parametri dell'operazione|  
|<xref:System.ServiceModel.Dispatcher.IClientMessageFormatter>|[DeserializeReply\(Message, Object\<xref:System.ServiceModel.Dispatcher.IClientMessageFormatter.DeserializeReply%28System.ServiceModel.Channels.Message%2CSystem.Object%5B%5D%29>|Converte un `Message` in ingresso in un valore restituito\/parametri out|  
  
## Serializzazione  
 Ogni volta che si utilizzano contratti di messaggi o parametri per descrivere il contenuto del messaggio, è necessario utilizzare la serializzazione per la conversione tra i tipi [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] e la rappresentazione di Infoset XML. La serializzazione è utilizzata in altre posizioni in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], ad esempio, <xref:System.ServiceModel.Channels.Message> ha un metodo <xref:System.ServiceModel.Channels.Message.GetBody%2A> generico che è possibile utilizzare per leggere l'intero corpo del messaggio deserializzato in un oggetto.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] supporta due tecnologie di serializzazione "automatica" per serializzare e deserializzare parametri e parti dei messaggi: <xref:System.Runtime.Serialization.DataContractSerializer> e `XmlSerializer`. È inoltre possibile scrivere serializzatori personalizzati. È tuttavia possibile far sì che altre parti di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] \(ad esempio il metodo `GetBody` generico o la serializzazione di errori SOAP\) utilizzino solo le sottoclassi \(<xref:System.Runtime.Serialization.XmlObjectSerializer> e <xref:System.Runtime.Serialization.DataContractSerializer>, ma non <xref:System.Runtime.Serialization.NetDataContractSerializer>\) <xref:System.Xml.Serialization.XmlSerializer> o specificarle a livello di codice affinché utilizzono solo <xref:System.Runtime.Serialization.DataContractSerializer>.  
  
 `XmlSerializer` è il motore di serializzazione utilizzato nei servizi Web [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)].`DataContractSerializer` è il nuovo motore di serializzazione che riconosce il nuovo modello di programmazione del contratto dati.`DataContractSerializer` è la scelta predefinita e la scelta di utilizzare `XmlSerializer` può essere fatta in base a ogni singola operazione utilizzando l'attributo <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior.DataContractFormatAttribute%2A>.  
  
 <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior> e <xref:System.ServiceModel.Description.XmlSerializerOperationBehavior> sono i comportamenti dell'operazione responsabili del collegamento dei formattatori dei messaggi rispettivamente per `DataContractSerializer` e `XmlSerializer`. Il comportamento <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior> può di fatto operare con qualsiasi serializzatore che deriva da <xref:System.Runtime.Serialization.XmlObjectSerializer>, compreso <xref:System.Runtime.Serialization.NetDataContractSerializer> \(descritto in dettaglio nella sezione sull'utilizzo della serializzazione autonoma\). Il comportamento chiama uno degli overload del metodo virtuale `CreateSerializer` per ottenere il serializzatore. Per collegare un serializzatore diverso, creare una nuova sottoclasse <xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior> ed eseguire l'override di entrambi gli overload `CreateSerializer`.  
  
## Vedere anche  
 [Specifica del trasferimento di dati nei contratti di servizio](../../../../docs/framework/wcf/feature-details/specifying-data-transfer-in-service-contracts.md)