---
title: "Chunking del canale | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e4d53379-b37c-4b19-8726-9cc914d5d39f
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# Chunking del canale
Quando si inviano messaggi di grandi dimensioni usando [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)], spesso è consigliabile limitare la quantità di memoria usata per memorizzare quei messaggi nel buffer.  Una possibile soluzione è di trasmettere il corpo del messaggio \(presupponendo che il grosso dei dati è contenuto nel corpo\).  Tuttavia alcuni protocolli richiedono la memorizzazione nel buffer del messaggio intero.  Due esempi sono rappresentati dai protocolli di messaggistica affidabile e di sicurezza.  Un'altra possibile soluzione è di suddividere il messaggio in messaggi più piccoli, chiamati blocchi, inviare quei blocchi uno alla volta e ricostruire il messaggio originale sul lato ricevente.  L'applicazione stessa può eseguire questa suddivisione in blocchi e ricostruzione oppure può usare un canale personalizzato per eseguire queste operazioni.  Nell'esempio relativo al canale per la suddivisione in blocchi viene illustrato come è possibile usare un protocollo personalizzato o un canale su più livelli per suddividere in blocchi e ricostruire i messaggi di grandi dimensioni.  
  
 La suddivisione in blocchi deve essere eseguita solo dopo la costruzione dell'intero messaggio da inviare.  Un canale per la suddivisione in blocchi deve sempre distribuito su più livelli al di sotto di un canale di sicurezza e di un canale di sessione affidabile.  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine di questo argomento.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.  Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].  Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Extensibility\Channels\ChunkingChannel`  
  
## Presupposti e limitazioni del canale per la suddivisione in blocchi  
  
### Struttura del messaggio  
 Il canale per la suddivisione in blocchi presuppone che il messaggio sia strutturato nel modo seguente per eseguire la suddivisione in blocchi:  
  
```  
<soap:Envelope ...>  
  <!-- headers -->  
  <soap:Body>  
    <operationElement>  
      <paramElement>data to be chunked</paramElement>  
    </operationElement>  
  </soap:Body>  
</soap:Envelope>  
```  
  
 Quando si usa ServiceModel, le operazioni del contratto che hanno 1 parametro di input si conformano con questa forma di messaggio per il messaggio di input.  In modo simile, le operazioni del contratto che hanno 1 parametro di output o valore restituito si conformano con questa forma di messaggio per il messaggio di output.  Di seguito sono elencati esempi di queste operazioni:  
  
```  
[ServiceContract]  
interface ITestService  
{  
    [OperationContract]  
    Stream EchoStream(Stream stream);  
  
    [OperationContract]  
    Stream DownloadStream();  
  
    [OperationContract(IsOneWay = true)]  
    void UploadStream(Stream stream);  
}  
```  
  
### Sessions  
 Il canale per la suddivisione in blocchi richiede che i messaggi vengano recapitati una volta sola, con recapito ordinato dei messaggi \(blocchi\).  Questo significa che lo stack di canali sottostante deve essere dotato di sessioni.  Le sessioni possono essere fornite dal trasporto \(ad esempio, trasporto TCP\) o da un canale del protocollo con sessione \(ad esempio, il canale ReliableSession\).  
  
### Invio e ricezione asincroni  
 I metodi di invio e ricezione asincroni non vengono implementati in questa versione dell'esempio relativo al canale per la suddivisione in blocchi.  
  
## Protocollo per la suddivisione in blocchi  
 Il canale per la suddivisione in blocchi definisce un protocollo che indica l'inizio e la fine di una serie di blocchi, oltre al numero di sequenza di ogni blocco.  Nei tre esempi di messaggio seguenti vengono descritti i messaggi iniziali, a blocchi e finali con i commenti che descrivono gli aspetti principali di ognuno.  
  
### Messaggio iniziale  
  
```  
<s:Envelope xmlns:a="http://www.w3.org/2005/08/addressing"   
            xmlns:s="http://www.w3.org/2003/05/soap-envelope">  
  <s:Header>  
<!—Original message action is replaced with a chunking-specific action. -->  
    <a:Action s:mustUnderstand="1">http://samples.microsoft.com/chunkingAction</a:Action>  
<!--  
Original message is assigned a unique id that is transmitted   
in a MessageId header. Note that this is different from the WS-Addressing MessageId header.  
-->  
    <MessageId s:mustUnderstand="1" xmlns="http://samples.microsoft.com/chunking">  
53f183ee-04aa-44a0-b8d3-e45224563109  
</MessageId>  
<!--  
ChunkingStart header signals the start of a chunked message.  
-->  
    <ChunkingStart s:mustUnderstand="1" i:nil="true" xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://samples.microsoft.com/chunking" />  
<!--  
Original message action is transmitted in OriginalAction.  
This is required to re-create the original message on the other side.  
-->  
    <OriginalAction xmlns="http://samples.microsoft.com/chunking">  
http://tempuri.org/ITestService/EchoStream  
    </OriginalAction>  
   <!--  
    All original message headers are included here.  
   -->  
  </s:Header>  
  <s:Body>  
<!--  
Chunking assumes this structure of Body content:  
<element>  
  <childelement>large data to be chunked<childelement>  
</element>  
The start message contains just <element> and <childelement> without  
the data to be chunked.  
-->  
    <EchoStream xmlns="http://tempuri.org/">  
      <stream />  
    </EchoStream>  
  </s:Body>  
</s:Envelope>  
```  
  
### Messaggio a blocchi  
  
```  
<s:Envelope   
  xmlns:a="http://www.w3.org/2005/08/addressing"   
  xmlns:s="http://www.w3.org/2003/05/soap-envelope">  
  <s:Header>  
   <!--  
    All chunking protocol messages have this action.  
   -->  
    <a:Action s:mustUnderstand="1">  
      http://samples.microsoft.com/chunkingAction  
    </a:Action>  
<!--  
Same as MessageId in the start message. The GUID indicates which original message this chunk belongs to.  
-->  
    <MessageId s:mustUnderstand="1"   
               xmlns="http://samples.microsoft.com/chunking">  
      53f183ee-04aa-44a0-b8d3-e45224563109  
    </MessageId>  
<!--  
The sequence number of the chunk.  
This number restarts at 1 with each new sequence of chunks.  
-->  
    <ChunkNumber s:mustUnderstand="1"   
                 xmlns="http://samples.microsoft.com/chunking">  
      1096  
    </ChunkNumber>  
  </s:Header>  
  <s:Body>  
<!--  
The chunked data is wrapped in a chunk element.  
The encoding of this data (and the entire message)   
depends on the encoder used. The chunking channel does not mandate an encoding.  
-->  
    <chunk xmlns="http://samples.microsoft.com/chunking">  
kfSr2QcBlkHTvQ==  
    </chunk>  
  </s:Body>  
</s:Envelope>  
  
```  
  
### Messaggio finale  
  
```  
<s:Envelope xmlns:a="http://www.w3.org/2005/08/addressing"   
            xmlns:s="http://www.w3.org/2003/05/soap-envelope">  
  <s:Header>  
    <a:Action s:mustUnderstand="1">  
      http://samples.microsoft.com/chunkingAction  
    </a:Action>  
<!--  
Same as MessageId in the start message. The GUID indicates which original message this chunk belongs to.  
-->  
    <MessageId s:mustUnderstand="1"   
               xmlns="http://samples.microsoft.com/chunking">  
      53f183ee-04aa-44a0-b8d3-e45224563109  
    </MessageId>  
<!--  
ChunkingEnd header signals the end of a chunk sequence.  
-->  
    <ChunkingEnd s:mustUnderstand="1" i:nil="true"   
                 xmlns:i="http://www.w3.org/2001/XMLSchema-instance"   
                 xmlns="http://samples.microsoft.com/chunking" />  
<!--  
ChunkingEnd messages have a sequence number.  
-->  
    <ChunkNumber s:mustUnderstand="1"   
                 xmlns="http://samples.microsoft.com/chunking">  
      79  
    </ChunkNumber>  
  </s:Header>  
  <s:Body>  
<!--  
The ChunkingEnd message has the same <element><childelement> structure  
as the ChunkingStart message.  
-->  
    <EchoStream xmlns="http://tempuri.org/">  
      <stream />  
    </EchoStream>  
  </s:Body>  
</s:Envelope>  
```  
  
## Architettura del canale per la suddivisione in blocchi  
 Il canale per la suddivisione in blocchi è un `IDuplexSessionChannel` che, a livello superiore, segue l'architettura del canale tipica.  C'è un `ChunkingBindingElement` che può compilare un `ChunkingChannelFactory` e un `ChunkingChannelListener`.  `ChunkingChannelFactory` crea istanze di `ChunkingChannel` quando gli viene richiesto.  `ChunkingChannelListener` crea istanze di `ChunkingChannel` quando viene accettato un nuovo canale interno.  Il `ChunkingChannel` stesso è responsabile per l'invio e la ricezione dei messaggi.  
  
 Al successivo livello inferiore, il `ChunkingChannel` si basa su molti componenti per implementare il protocollo per la suddivisione in blocchi.  Per l'invio, il canale usa un oggetto `XmlDictionaryWriter` personalizzato chiamato `ChunkingWriter` che esegue la vera e propria suddivisione in blocchi.  `ChunkingWriter` usa direttamente il canale interno per inviare i blocchi.  L'uso di un `XmlDictionaryWriter` personalizzato consente di inviare i blocchi mentre viene scritto il corpo del messaggio originale.  Questo significa che non viene memorizzato nel buffer l'intero messaggio originale.  
  
 ![Chunking del canale](../../../../docs/framework/wcf/samples/media/chunkingchannel1.gif "ChunkingChannel1")  
  
 Per la ricezione, `ChunkingChannel` esegue il pull dei messaggi dal canale interno e li consegna a un oggetto `XmlDictionaryReader` personalizzato denominato `ChunkingReader`, che ricostruisce il messaggio originale dai blocchi in arrivo.  `ChunkingChannel` esegue il wrapping di questo `ChunkingReader` in un'implementazione `Message` personalizzata denominata `ChunkingMessage` e restituisce il messaggio al livello superiore.  Questa combinazione di `ChunkingReader` e `ChunkingMessage` consente di ricostruire il corpo del messaggio originale mentre viene letto dal livello superiore, invece di dover memorizzare nel buffer l'intero corpo del messaggio originale.  `ChunkingReader` è dotato di una coda in cui memorizza nel buffer i blocchi in arrivo, fino a un numero massimo configurabile di blocchi memorizzati.  Quando questo limite massimo viene raggiunto, il lettore attende che i messaggi vengano svuotati dalla coda dal livello superiore \(operazione eseguita semplicemente leggendo il corpo del messaggio originale\) o fino a raggiungere il timeout di ricezione massimo.  
  
 ![Chunking del canale](../../../../docs/framework/wcf/samples/media/chunkingchannel2.gif "ChunkingChannel2")  
  
## Modello di programmazione per la suddivisione in blocchi  
 Gli sviluppatori del servizio possono specificare quali messaggi devono essere suddivisi in blocchi applicando l'attributo `ChunkingBehavior` alle operazioni all'interno del contratto.  L'attributo espone una proprietà `AppliesTo` che consente allo sviluppatore di specificare se la suddivisione in blocchi si applica al messaggio di input, al messaggio di output o a entrambi.  Nell'esempio seguente viene illustrato l'uso dell'attributo `ChunkingBehavior`:  
  
```  
[ServiceContract]  
interface ITestService  
{  
    [OperationContract]  
    [ChunkingBehavior(ChunkingAppliesTo.Both)]  
    Stream EchoStream(Stream stream);  
  
    [OperationContract]  
    [ChunkingBehavior(ChunkingAppliesTo.OutMessage)]  
    Stream DownloadStream();  
  
    [OperationContract(IsOneWay=true)]  
    [ChunkingBehavior(ChunkingAppliesTo.InMessage)]  
    void UploadStream(Stream stream);  
  
}  
  
```  
  
 Da questo modello di programmazione, il `ChunkingBindingElement` compila un elenco di URI dell'azione che identificano i messaggi da suddividere in blocchi.  L'azione di ogni messaggio in uscita viene confrontata con questo elenco per determinare se il messaggio deve essere suddiviso in blocchi o inviato direttamente.  
  
## Implementazione dell'operazione Send  
 A livello superiore, l'operazione Send prima controlla se il messaggio in uscita deve essere suddiviso in blocchi e altrimenti invia direttamente il messaggio usando il canale interno.  
  
 Se il messaggio deve essere suddiviso in blocchi, l'operazione Send crea un nuovo `ChunkingWriter` e chiama `WriteBodyContents` sul messaggio in uscita passandogli il `ChunkingWriter`.  Il `ChunkingWriter` esegue quindi la suddivisione in blocchi del messaggio \(copiando le intestazioni del messaggio originale nel blocco di messaggio iniziale\) e invia i blocchi usando il canale interno.  
  
 Alcuni dettagli degni di nota:  
  
-   L'operazione Send prima chiama `ThrowIfDisposedOrNotOpened` per assicurarsi che `CommunicationState` sia aperto.  
  
-   L'invio viene sincronizzato in modo che possa essere inviato solo uno messaggio alla volta per ogni sessione.  C'è un `ManualResetEvent` denominato `sendingDone` che viene reimpostato quando viene inviato un messaggio suddiviso in blocchi.  Una volta inviato il blocco di messaggio finale, l'evento viene impostato.  Il metodo Send attende che questo evento venga impostato prima che di tentare di inviare il messaggio in uscita.  
  
-   L'operazione Send blocca `CommunicationObject.ThisLock` per evitare modifiche sincronizzate dello stato durante l'invio.  Vedere la documentazione relativa a <xref:System.ServiceModel.Channels.CommunicationObject> per altre informazioni sugli stati di <xref:System.ServiceModel.Channels.CommunicationObject> e sulla macchina a stati.  
  
-   Il timeout passato a Send viene usato come timeout per l'intera operazione di invio, che comprende l'invio di tutti i blocchi.  
  
-   La progettazione `XmlDictionaryWriter` personalizzata viene scelta per evitare di memorizzare nel buffer l'intero corpo del messaggio originale.  Se si dovesse usare un `XmlDictionaryReader` sul corpo usando `message.GetReaderAtBodyContents`, l'intero corpo verrebbe memorizzato nel buffer.  Invece, si usa un `XmlDictionaryWriter` personalizzato passato a `message.WriteBodyContents`.  Quando il messaggio chiama WriteBase64 sul writer, il writer ricostruisce i blocchi in messaggi e li invia usando il canale interno.  WriteBase64 si blocca fino a che non viene inviato il blocco.  
  
## Implementazione dell'operazione Receive  
 A livello superiore, l'operazione Receive prima controlla che il messaggio in arrivo non sia `null` e che l'azione sia `ChunkingAction`.  Se non vengono soddisfatti entrambi i criteri, Receive restituisce il messaggio immutato.  In caso contrario, Receive crea un nuovo `ChunkingReader` su cui viene eseguito il wrapping di un nuovo `ChunkingMessage` \(chiamando `GetNewChunkingMessage`\).  Prima di restituire quel nuovo `ChunkingMessage`, Receive usa un che un thread del pool di thread per eseguire `ReceiveChunkLoop` che chiama `innerChannel.Receive` in un ciclo e consegna i blocchi al `ChunkingReader` fino a ricevere il blocco di messaggio finale o fino a raggiungere il timeout di ricezione.  
  
 Alcuni dettagli degni di nota:  
  
-   Come per l'operazione Send, Receive prima chiama `ThrowIfDisposedOrNotOepned` per assicurarsi che `CommunicationState` sia aperto.  
  
-   Anche l'operazione Receive viene sincronizzata in modo che si possa ricevere solo un messaggio alla volta dalla sessione.  Questo è particolarmente importante perché una volta ricevuto un blocco di messaggio iniziale, si presuppone che tutti i messaggi seguenti ricevuti siano blocchi di questa nuova sequenza di blocchi, fino alla ricezione del blocco di messaggio finale.  L'operazione Receive non è in grado di eseguire il pull dei messaggi dal canale interno finché non vengono ricevuti tutti i blocchi che appartengono al messaggio in corso di ricostruzione.  Per eseguire questa operazione, Receive usa un `ManualResetEvent` denominato `currentMessageCompleted`, impostato quando viene ricevuto il blocco di messaggio finale e reimpostato quando viene ricevuto un nuovo blocco di messaggio iniziale.  
  
-   A differenza dell'operazione Send, Receive non impedisce le transizioni sincronizzate dello stato durante la ricezione.  Ad esempio, è possibile chiamare il metodo Close durante la ricezione. Il metodo attenderà che venga completata la ricezione del messaggio originale o che venga raggiunto il valore di timeout specificato.  
  
-   Il timeout passato a Receive viene usato come timeout per l'intera operazione di ricezione, che comprende la ricezione di tutti i blocchi.  
  
-   Se il livello che usa il messaggio sta usando il corpo del messaggio a una velocità inferiore della velocità di arrivo dei blocchi dei messaggi, `ChunkingReader` memorizza nel buffer quei blocchi in arrivo fino al limite specificato da `ChunkingBindingElement.MaxBufferedChunks`.  Una volta raggiunto quel limite, non viene eseguito il pull di altri blocchi dal livello inferiore finché non viene usato un blocco memorizzato nel buffer o viene raggiunto il timeout di ricezione.  
  
## Override di CommunicationObject  
  
### OnOpen  
 `OnOpen` chiama `innerChannel.Open` per aprire il canale interno.  
  
### OnClose  
 `OnClose` prima imposta `stopReceive` su `true` per comunicare al `ReceiveChunkLoop` in sospeso di arrestarsi.  Quindi attende l'evento `receiveStopped``ManualResetEvent`, che viene impostato quando `ReceiveChunkLoop` si arresta.  Presupponendo che `ReceiveChunkLoop` si arresti entro il timeout specificato, `OnClose` chiama `innerChannel.Close` con il timeout rimanente.  
  
### OnAbort  
 `OnAbort` chiama `innerChannel.Abort` per interrompere il canale interno.  Se c'è un `ReceiveChunkLoop` in sospeso, viene generata un'eccezione dalla chiamata `innerChannel.Receive` in sospeso.  
  
### OnFaulted  
 Il `ChunkingChannel` non richiede un comportamento speciale quando il canale contiene errori, per cui non viene eseguito l'override di `OnFaulted`.  
  
## Implementazione di una channel factory  
 La `ChunkingChannelFactory` è responsabile per la creazione di istanze di `ChunkingDuplexSessionChannel` e per la sovrapposizione delle transizioni di stato nella channel factory interna.  
  
 `OnCreateChannel` usa la channel factory interna per creare un canale interno `IDuplexSessionChannel`.  Crea quindi un nuovo `ChunkingDuplexSessionChannel` passandogli questo canale interno, l'elenco di azioni del messaggio da suddividere in blocchi e il numero massimo di blocchi da memorizzare nel buffer al momento della ricezione.  L'elenco di azioni del messaggio da suddividere in blocchi e il numero massimo di blocchi da memorizzare nel buffer sono due parametri passati a `ChunkingChannelFactory` nel costruttore.  Nella sezione relativa all'elemento `ChunkingBindingElement` viene descritto da dove provengono questi valori.  
  
 `OnOpen`, `OnClose`, `OnAbort` e gli equivalenti asincroni chiamano il metodo della transizione di stato corrispondente nella channel factory interna.  
  
## Implementazione di un listener del canale  
 Il `ChunkingChannelListener` è un wrapper del listener del canale interno.  La sua funzione principale, oltre a delegare le chiamate al listener del canale interno, è di eseguire il wrapping dei nuovi `ChunkingDuplexSessionChannels` sui canali accettati dal listener del canale interno.  Questa operazione viene eseguita in `OnAcceptChannel` e `OnEndAcceptChannel`.  Il nuovo `ChunkingDuplexSessionChannel` viene passato al canale interno insieme agli altri parametri precedentemente descritti.  
  
## Implementazione degli elementi di associazione e delle associazioni  
 `ChunkingBindingElement` è responsabile della creazione di `ChunkingChannelFactory` e di `ChunkingChannelListener`.  `ChunkingBindingElement` controlla se T in `CanBuildChannelFactory`\<T\> e in `CanBuildChannelListener`\<T\> è di tipo `IDuplexSessionChannel` \(l'unico canale supportato dal canale per la suddivisione in blocchi\) e che gli altri elementi di associazione nell'associazione supportano questo tipo di canale.  
  
 `BuildChannelFactory`\<T\> controlla prima di tutto che il tipo di canale richiesto possa essere compilato, quindi ottiene un elenco delle azioni del messaggio da suddividere in blocchi  Per altre informazioni, vedere la sezione successiva.  Crea quindi un nuovo `ChunkingChannelFactory` passandogli la channel factory interna \(restituita da `context.BuildInnerChannelFactory<IDuplexSessionChannel>`\), l'elenco di azioni del messaggio e il numero massimo di blocchi da memorizzare nel buffer.  Il numero massimo di blocchi proviene da una proprietà chiamata `MaxBufferedChunks` esposta da `ChunkingBindingElement`.  
  
 L'implementazione del metodo `BuildChannelListener<T>` per creare `ChunkingChannelListener` e passare il listener del canale interno è simile.  
  
 In questo esempio viene incluso un esempio di associazione denominata `TcpChunkingBinding`.  Questa associazione è costituita da due elementi di associazione: `TcpTransportBindingElement` e `ChunkingBindingElement`.  Oltre a esporre la proprietà `MaxBufferedChunks`, l'associazione imposta anche alcune delle proprietà `TcpTransportBindingElement`, ad esempio `MaxReceivedMessageSize` \(lo imposta su `ChunkingUtils.ChunkSize` \+ 100KB byte per le intestazioni\).  
  
 `TcpChunkingBinding` implementa anche `IBindingRuntimePreferences` e restituisce true dal metodo `ReceiveSynchronously`, che indica che vengono implementate solo le chiamate Receive sincrone.  
  
### Decidere quali messaggi vanno suddivisi in blocchi  
 Il canale per la suddivisione in blocchi suddivide solo i messaggi identificati dall'attributo `ChunkingBehavior`.  La classe `ChunkingBehavior` implementa `IOperationBehavior` e viene implementata chiamando il metodo `AddBindingParameter`.  In questo metodo, `ChunkingBehavior` esamina il valore della proprietà `AppliesTo` \(`InMessage`, `OutMessage` o entrambi\) per determinare quali messaggi vanno suddivisi in blocchi.  Ottiene quindi l'azione di ognuno di quei messaggi \(dalla raccolta dei messaggi in `OperationDescription`\) e la aggiunge a una raccolta di stringhe contenuta all'interno di un'istanza di `ChunkingBindingParameter`.  Aggiunge quindi questo `ChunkingBindingParameter` alla raccolta `BindingParameterCollection` fornito  
  
 `BindingParameterCollection` viene passato all'interno di `BindingContext` a ogni elemento di associazione nell'associazione quando l'elemento di associazione compila la channel factory o il listener del canale.  L'implementazione `ChunkingBindingElement` di `BuildChannelFactory<T>` e di  `BuildChannelListener<T>` esegue il pull di questo `ChunkingBindingParameter` dalla raccolta `BindingParameterCollection` di `BindingContext’`.  La raccolta di azioni contenuta all'interno di `ChunkingBindingParameter` viene quindi passata alla `ChunkingChannelFactory` o al `ChunkingChannelListener`, che a sua volta la passa al `ChunkingDuplexSessionChannel`.  
  
## Esecuzione dell'esempio  
  
#### Per impostare, compilare ed eseguire l'esempio  
  
1.  Installare [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 4.0 usando il comando seguente.  
  
    ```  
    %windir%\Microsoft.NET\Framework\v4.0.XXXXX\aspnet_regiis.exe /i /enable  
  
    ```  
  
2.  Assicurarsi di avere eseguito la [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
3.  Per compilare la soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
4.  Per eseguire l'esempio su un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
5.  Eseguire prima Service.exe quindi Client.exe e controllare l'output di entrambe le finestre della console.  
  
 Quando si esegue l'esempio, viene visualizzato l'output seguente:  
  
 Client:  
  
```  
Press enter when service is available  
  
 > Sent chunk 1 of message 867c1fd1-d39e-4be1-bc7b-32066d7ced10  
 > Sent chunk 2 of message 867c1fd1-d39e-4be1-bc7b-32066d7ced10  
 > Sent chunk 3 of message 867c1fd1-d39e-4be1-bc7b-32066d7ced10  
 > Sent chunk 4 of message 867c1fd1-d39e-4be1-bc7b-32066d7ced10  
 > Sent chunk 5 of message 867c1fd1-d39e-4be1-bc7b-32066d7ced10  
 > Sent chunk 6 of message 867c1fd1-d39e-4be1-bc7b-32066d7ced10  
 > Sent chunk 7 of message 867c1fd1-d39e-4be1-bc7b-32066d7ced10  
 > Sent chunk 8 of message 867c1fd1-d39e-4be1-bc7b-32066d7ced10  
 > Sent chunk 9 of message 867c1fd1-d39e-4be1-bc7b-32066d7ced10  
 > Sent chunk 10 of message 867c1fd1-d39e-4be1-bc7b-32066d7ced10  
 < Received chunk 1 of message 5b226ad5-c088-4988-b737-6a565e0563dd  
 < Received chunk 2 of message 5b226ad5-c088-4988-b737-6a565e0563dd  
 < Received chunk 3 of message 5b226ad5-c088-4988-b737-6a565e0563dd  
 < Received chunk 4 of message 5b226ad5-c088-4988-b737-6a565e0563dd  
 < Received chunk 5 of message 5b226ad5-c088-4988-b737-6a565e0563dd  
 < Received chunk 6 of message 5b226ad5-c088-4988-b737-6a565e0563dd  
 < Received chunk 7 of message 5b226ad5-c088-4988-b737-6a565e0563dd  
 < Received chunk 8 of message 5b226ad5-c088-4988-b737-6a565e0563dd  
 < Received chunk 9 of message 5b226ad5-c088-4988-b737-6a565e0563dd  
 < Received chunk 10 of message 5b226ad5-c088-4988-b737-6a565e0563dd  
```  
  
 Server:  
  
```  
Service started, press enter to exit  
 < Received chunk 1 of message 867c1fd1-d39e-4be1-bc7b-32066d7ced10  
 < Received chunk 2 of message 867c1fd1-d39e-4be1-bc7b-32066d7ced10  
 < Received chunk 3 of message 867c1fd1-d39e-4be1-bc7b-32066d7ced10  
 < Received chunk 4 of message 867c1fd1-d39e-4be1-bc7b-32066d7ced10  
 < Received chunk 5 of message 867c1fd1-d39e-4be1-bc7b-32066d7ced10  
 < Received chunk 6 of message 867c1fd1-d39e-4be1-bc7b-32066d7ced10  
 < Received chunk 7 of message 867c1fd1-d39e-4be1-bc7b-32066d7ced10  
 < Received chunk 8 of message 867c1fd1-d39e-4be1-bc7b-32066d7ced10  
 < Received chunk 9 of message 867c1fd1-d39e-4be1-bc7b-32066d7ced10  
 < Received chunk 10 of message 867c1fd1-d39e-4be1-bc7b-32066d7ced10  
 > Sent chunk 1 of message 5b226ad5-c088-4988-b737-6a565e0563dd  
 > Sent chunk 2 of message 5b226ad5-c088-4988-b737-6a565e0563dd  
 > Sent chunk 3 of message 5b226ad5-c088-4988-b737-6a565e0563dd  
 > Sent chunk 4 of message 5b226ad5-c088-4988-b737-6a565e0563dd  
 > Sent chunk 5 of message 5b226ad5-c088-4988-b737-6a565e0563dd  
 > Sent chunk 6 of message 5b226ad5-c088-4988-b737-6a565e0563dd  
 > Sent chunk 7 of message 5b226ad5-c088-4988-b737-6a565e0563dd  
 > Sent chunk 8 of message 5b226ad5-c088-4988-b737-6a565e0563dd  
 > Sent chunk 9 of message 5b226ad5-c088-4988-b737-6a565e0563dd  
 > Sent chunk 10 of message 5b226ad5-c088-4988-b737-6a565e0563dd  
```  
  
## Vedere anche