---
title: "&lt;trasportoMsmq&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 19d89f35-76ac-49dc-832b-e8bec2d5e33b
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# &lt;trasportoMsmq&gt;
Impone a un canale di trasferire i messaggi tramite il trasporto MSMQ quando viene incluso in un'associazione personalizzata.  
  
## Sintassi  
  
```  
  
<msmqTransport>  
    customDeadLetterQueue="Uri"  
    deadLetterQueue="Custom/None/System"  
    durable="Boolean"  
    exactlyOnce="Boolean"  
    manualAddressing="Boolean"  
    maxBufferPoolSize="Integer"  
    maxImmediateRetries="Integer"  
    maxPoolSize="Integer"  
    maxReceivedMessageSize="Integer"  
    maxRetryCycles="Integer"  
....queueTransferProtocol="Native/Srmp/SrmpSecure"  
    rejectAfterLastRetry="Boolean"  
    retryCycleDelay="TimeSpan"  
    timeToLive="TimeSpan"  
    useActiveDirectory="Boolean"  
    useSourceJournal="Boolean"  
    useMsmqTracing="Boolean"  
    <msmqTransportSecurity>  
    </msmqTransportSecurity>  
</msmqIntegration>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|customDeadLetterQueue|URI che indica il percorso della coda dei messaggi non recapitabili per applicazione. In tale coda vengono collocati i messaggi scaduti o non recapitabili all'applicazione.<br /><br /> Per i messaggi che richiedono la garanzia ExactlyOnce, ovvero l'impostazione dell'attributo `exactlyOnce` su `true`, questo attributo viene impostato come valore predefinito sulla coda transazionale dei messaggi non recapitabili a livello di sistema di MSMQ.<br /><br /> Per i messaggi che non richiedono alcuna garanzia, ovvero per i messaggi il cui attributo `exactlyOnce` è impostato su `false`, l'impostazione predefinita dell'attributo è `null`.<br /><br /> Il valore deve usare lo schema net.msmq.  Il valore predefinito è `null`.<br /><br /> Se `deadLetterQueue` è impostato su `None` o su `System`, questo attributo deve essere impostato su `null`.  Se questo attributo non viene impostato su `null`, `deadLetterQueue` deve essere impostato su `Custom`.|  
|deadLetterQueue|Specifica il tipo di coda dei messaggi non recapitabili da usare.<br /><br /> I valori validi includono<br /><br /> -   Custom: viene usata una coda dei messaggi non recapitabili personalizzata.<br />-   None: non viene usata alcuna coda dei messaggi non recapitabili.<br />-   System: viene usata la coda dei messaggi non recapitabili di sistema.<br /><br /> L'attributo è di tipo DeadLetterQueue.|  
|durable|Valore booleano che specifica se i messaggi elaborati da questa associazione sono durevoli o volatili.  Il valore predefinito è `true`.<br /><br /> Un messaggio durevole sopravvive a un arresto del gestore delle code, un messaggio volatile no.  I messaggi volatili sono utili quando le applicazioni richiedono minore latenza e possono tollerare messaggi perduti occasionalmente.<br /><br /> Se `exactlyOnce` è impostato su `true`, i messaggi devono essere durevoli.|  
|exactlyOnce|Valore booleano che indica se i messaggi elaborati da questa associazione verranno ricevuti una sola volta.  Il valore predefinito è `true`.<br /><br /> Un messaggio può essere inviato con o senza garanzie.  Una garanzia consente a un'applicazione di verificare che un messaggio inviato abbia raggiunto la coda dei messaggi del destinatario. In caso contrario, l'applicazione può determinarlo leggendo la coda dei messaggi non recapitabili.<br /><br /> Quando `exactlyOnce` è impostato su `true` indica che MSMQ verificherà che un messaggio inviato sia recapitato una sola volta alla coda dei messaggi del destinatario e, se il recapito non riesce, il messaggio viene inviato alla coda dei messaggi non recapitabili.<br /><br /> I messaggi inviati con la proprietà `exactlyOnce` impostata su `true` devono essere inviati solo a una coda transazionale.|  
|manualAddressing|Valore booleano che consente all'utente di assumere il controllo dell'indirizzamento dei messaggi.  Questa proprietà viene usata in genere in scenari di router, in cui è l'applicazione a determinare a quale delle tante destinazioni inviare un messaggio.<br /><br /> Quando è impostato su `true`, il canale presuppone che il messaggio sia già stato indirizzato e non aggiunge ulteriori informazioni.  L'utente può indirizzare quindi individualmente ogni messaggio.<br /><br /> Quando è impostato su `false`, il meccanismo di indirizzamento predefinito di Windows Communication Foundation \(WCF\) crea automaticamente indirizzi per tutti i messaggi.<br /><br /> Il valore predefinito è `false`.|  
|maxBufferPoolSize|Numero intero positivo che specifica la dimensione massima del pool di buffer.  Il valore predefinito è 524288.<br /><br /> Molte parti di WCF usano buffer.  La creazione e l'eliminazione dei buffer a ogni relativo uso sono operazioni onerose, analogamente a quelle di Garbage Collection dei buffer.  Quando si usa un pool di buffer è possibile prelevare un buffer dal pool, usarlo e, al termine delle operazioni, riporlo nel pool.  In questo modo è possibile evitare il sovraccarico dovuto alla creazione e all'eliminazione dei buffer.|  
|maxImmediateRetries|Valore intero che specifica il numero massimo di tentativi immediati su un messaggio letto dalla coda dell'applicazione.  Il valore predefinito è 5.<br /><br /> Se viene raggiunto il numero massimo di tentativi senza che il messaggio venga usato dall'applicazione, il messaggio viene inviato a una coda di tentativi per essere sottoposto in seguito a nuovi tentativi di elaborazione.  Se non è specificato alcun ciclo di ripetizione, il messaggio viene inviato alla coda dei messaggi non elaborabili oppure viene inviato un riconoscimento negativo al mittente.|  
|maxPoolSize|Numero intero positivo che specifica la dimensione massima del pool.  Il valore predefinito è 524288.|  
|maxReceivedMessageSize|Numero intero positivo che specifica la dimensione massima in byte dei messaggi, comprese le intestazioni.  Il mittente di un messaggio riceve un errore SOAP se il messaggio è troppo grande per il destinatario.  Il destinatario elimina il messaggio e crea una voce dell'evento nel registro di traccia.  Il valore predefinito è 65536.|  
|maxRetryCycles|Numero intero che indica il numero massimo di cicli di ripetizione dei tentativi di recapito dei messaggi all'applicazione ricevente.  Il valore predefinito è <xref:System.Int32.MaxValue>.<br /><br /> Un singolo ciclo di ripetizione tenta di recapitare un messaggio a un'applicazione per un numero di volte specificato.  Il numero di tentativi eseguiti è impostato dall'attributo `maxImmediateRetries`.  Se l'applicazione non riesce a usare il messaggio dopo che i tentativi di recapito sono stati esauriti, il messaggio viene inviato a una coda di tentativi.  I cicli di ripetizione successivi sono costituiti dal messaggio restituito dalla coda di tentativi alla coda dell'applicazione per tentare nuovamente il recapito all'applicazione, dopo un intervallo di tempo specificato dall'attributo `retryCycleDelay`.  L'attributo `maxRetryCycles` specifica il numero di cicli di ripetizione che l'applicazione usa per tentare di recapitare il messaggio.|  
|queueTransferProtocol|Specifica il trasporto del canale delle comunicazioni in coda usato da questa associazione.  I valori validi sono:<br /><br /> -   Native: viene usato il protocollo MSMQ nativo.<br />-   Srmp: viene usato il protocollo SRMP \(Soap Reliable Messaging Protocol\).<br />-   SrmpSecure: viene usato il trasporto SRMPS \(Soap Reliable Messaging Protocol Secure\).<br /><br /> L'attributo è di tipo <xref:System.ServiceModel.QueueTransferProtocol>.<br /><br /> Poiché MSMQ non supporta l'indirizzamento di Active Directory quando si usa il protocollo SRMP, evitare di impostare questo attributo su Srmp o Srmps quando la proprietà `u``seActiveDirectory` è impostata su `true`.|  
|rejectAfterLastRetry|Valore booleano che indica l'azione da intraprendere per un messaggio non recapitato dopo il numero massimo di tentativi.<br /><br /> `true` indica che al mittente viene restituito un non riconoscimento e che il messaggio viene eliminato. `false` indica che il messaggio viene inviato alla coda dei messaggi non elaborabili.  Il valore predefinito è `false`.<br /><br /> Se il valore è `false`, l'applicazione ricevente può leggere la coda dei messaggi non elaborabili per elaborare i messaggi non elaborabili, ovvero i messaggi il cui recapito ha avuto esito negativo.<br /><br /> Poiché MSMQ 3.0 non supporta la restituzione di un non riconoscimento al mittente, questo attributo viene ignorato in MSMQ 3.0.|  
|retryCycleDelay|Valore <xref:System.TimeSpan> che specifica l'intervallo di tempo tra i cicli di ripetizione dei tentativi di recapitare un messaggio che è impossibile recapitare immediatamente.  L'impostazione predefinita è 00:10:00.<br /><br /> Un singolo ciclo di ripetizione tenta di recapitare un messaggio a un'applicazione ricevente per uno specificato numero di volte.  Il numero di tentativi eseguiti è specificato dall'attributo `maxImmediateRetries`.  Se l'applicazione non riesce a usare il messaggio dopo il numero specificato di tentativi immediati, il messaggio viene inviato a una coda di tentativi.  I cicli di ripetizione successivi sono costituiti dal messaggio restituito dalla coda di tentativi alla coda dell'applicazione per tentare nuovamente il recapito all'applicazione, dopo un intervallo di tempo specificato dall'attributo `retryCycleDelay` .  Il numero di cicli di ripetizione è specificato dall'attributo `maxRetryCycles`.|  
|timeToLive|Valore <xref:System.TimeSpan> che specifica la durata di validità dei messaggi prima che scadano e vengano inseriti nella coda dei messaggi non recapitabili.  Il valore predefinito è 1.00:00:00, che corrisponde a un giorno.<br /><br /> L'attributo è impostato per verificare che i messaggi a scadenza non risultino non aggiornati prima di essere elaborati dalle applicazioni riceventi.  Un messaggio in una coda che non viene usato dall'applicazione ricevente entro l'intervallo di tempo specificato viene considerato scaduto.  I messaggi scaduti vengono inviati a una coda speciale denominata coda dei messaggi non recapitabili.  Il percorso della coda dei messaggi non recapitabili viene impostato con l'attributo `customDeadLetterQueue` o sul valore appropriato predefinito, in base alle garanzie.|  
|UseActiveDirectory|Valore booleano che indica se convertire gli indirizzi delle code mediante Active Directory.<br /><br /> Gli indirizzi delle code MSMQ possono essere costituiti da nomi di percorso o da nomi di formato Direct.  Con un nome di formato Direct, MSMQ risolve il nome del computer usando DNS, NetBIOS o IP.  Con un nome di percorso, MSMQ risolve il nome del computer usando Active Directory.  Per impostazione predefinita, il trasporto in coda di Windows Communication Framework \(WCF\) converte l'URI di una coda di messaggi in un nome di formato Direct.  Impostando questo attributo su `true`, un'applicazione può specificare che il trasporto in coda debba risolvere il nome del computer usando Active Directory invece di DNS, NetBIOS o IP.|  
|useMsmqTracing|Valore booleano che specifica se i messaggi elaborati da questa associazione devono essere tracciati.  Il valore predefinito è `false`.<br /><br /> Quando la traccia è attivata, i messaggi di rapporto vengono creati e inviati alla coda dei rapporti ogni volta che il messaggio viene inviato o ricevuto da un computer in cui è installato il sistema di accodamento messaggi.|  
|useSourceJournal|Valore booleano che indica se le copie dei messaggi elaborati da questa associazione devono essere archiviate nella coda journal di origine.  Il valore predefinito è `false`.<br /><br /> Le applicazioni in coda che devono tenere un registro dei messaggi che hanno lasciato la coda in uscita del computer possono copiare i messaggi in una coda journal.  Quando un messaggio lascia la coda in uscita e viene ricevuto un riconoscimento che il messaggio è stato ricevuto nel computer di destinazione, una copia del messaggio viene mantenuta nella coda journal del sistema del computer di invio.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<sicurezzaTrasportoMsmq\>](../../../../../docs/framework/configure-apps/file-schema/wcf/msmqtransportsecurity.md)|Specifica le impostazioni di sicurezza del trasporto per questa associazione.  L'elemento è di tipo <xref:System.ServiceModel.Configuration.MsmqTransportSecurityElement>.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<associazione\>](../../../../../docs/framework/misc/binding.md)|Definisce tutte le funzionalità di associazione dell'associazione personalizzata.|  
  
## Note  
 L'elemento `msmqTransport` consente all'utente di impostare le proprietà per il canale delle comunicazioni in coda.  Il canale delle comunicazioni in coda usa l'accodamento dei messaggi per il trasporto.  
  
 Questo è l'elemento di associazione predefinito usato dall'associazione standard dell'accodamento dei messaggi \(`netMsmqBinding`\).  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.MsmqTransportElement>   
 <xref:System.ServiceModel.Channels.MsmqTransportBindingElement>   
 <xref:System.ServiceModel.Channels.TransportBindingElement>   
 <xref:System.ServiceModel.Channels.CustomBinding>   
 [Code in WCF](../../../../../docs/framework/wcf/feature-details/queues-in-wcf.md)   
 [Trasporti](../../../../../docs/framework/wcf/feature-details/transports.md)   
 [Scelta di un trasporto](../../../../../docs/framework/wcf/feature-details/choosing-a-transport.md)   
 [Associazioni](../../../../../docs/framework/wcf/bindings.md)   
 [Estensione delle associazioni](../../../../../docs/framework/wcf/extending/extending-bindings.md)   
 [Associazioni personalizzate](../../../../../docs/framework/wcf/extending/custom-bindings.md)   
 [\<customBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)