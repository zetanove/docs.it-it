---
title: "Procedura: attivare il flusso | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6ca2cf4b-c7a1-49d8-a79b-843a90556ba4
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# Procedura: attivare il flusso
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] è in grado di inviare messaggi utilizzando trasferimenti con flusso o memorizzati nel buffer. Nella modalità predefinita, ovvero trasferimento con memorizzazione nel buffer, un messaggio deve essere recapitato completamente prima che un destinatario possa leggerlo. Nella modalità di trasferimento con flusso, il destinatario può iniziare a elaborare il messaggio prima che esso venga recapitato completamente. La modalità di trasmissione con flusso è utile quando le informazioni passate sono lunghe e possono essere elaborate in serie. La modalità di trasmissione con flusso è utile anche quando il messaggio è troppo grande da memorizzare completamente nel buffer.  
  
 Per attivare il flusso, definire correttamente `OperationContract` e attivare il flusso a livello di trasporto.  
  
### <a name="to-stream-data"></a>Per trasferire dati con flusso  
  
1.  Per trasferire dati con flusso, `OperationContract` per il servizio deve soddisfare due requisiti:  
  
    1.  Il parametro che contiene i dati da inviare in un flusso deve essere il solo parametro del metodo. Ad esempio, se il messaggio di input è quello da trasmettere, l'operazione deve avere esattamente un parametro di input. Allo stesso modo, se deve essere trasmesso il messaggio di output, l'operazione deve avere esattamente un solo parametro di output o un solo valore restituito.  
  
    2.  Almeno uno dei tipi di parametro e restituzione di valori deve essere <xref:System.IO.Stream>, <xref:System.ServiceModel.Channels.Message>, o <xref:System.Xml.Serialization.IXmlSerializable>.  
  
     Di seguito è riportato un esempio di contratto per dati trasferiti con flusso.  
  
     [!code-csharp[c_HowTo_EnableStreaming#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_enablestreaming/cs/service.cs#1)]
     [!code-vb[c_HowTo_EnableStreaming#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_enablestreaming/vb/service.vb#1)]  
  
     L'operazione `GetStream` riceve alcuni dati di input memorizzati nel buffer come `string`, che è memorizzata nel buffer, e restituisce `Stream`, trasferito con flusso. Viceversa, `UploadStream` accetta uno `Stream` (trasmesso) e restituisce un `bool` (memorizzato nel buffer). `EchoStream` accetta e restituisce uno `Stream` ed è un esempio di un'operazione i cui messaggi di input e output vengono entrambi trasmessi. Infine, `GetReversedStream` non prende input e restituisce un `Stream` (trasmesso).  
  
2.  La trasmissione deve essere attivata nell'associazione. Impostare una proprietà `TransferMode`, che può prendere uno dei valori seguenti:  
  
    1.  `Buffered`,  
  
    2.  `Streamed`, che consente di attivare la comunicazione con flusso bidirezionale.  
  
    3.  `StreamedRequest`, che consente la trasmissione della sola richiesta.  
  
    4.  `StreamedResponse`, che consente la trasmissione della sola risposta.  
  
     `BasicHttpBinding` espone la proprietà `TransferMode` sull'associazione come fanno anche `NetTcpBinding` e `NetNamedPipeBinding`. La proprietà `TransferMode` può essere impostata anche sull'elemento di associazione di trasporto e utilizzata in un'associazione personalizzata.  
  
     Negli esempi seguenti viene illustrato come impostare `TransferMode` tramite codice e modificando il file di configurazione. In entrambi gli esempi, inoltre, la proprietà `maxReceivedMessageSize` viene impostata a 64 MB, che pone un limite alla dimensione massima consentita dei messaggi in ricezione. La misura predefinita è `maxReceivedMessageSize` 64 KB che è di solito troppo bassa per gli scenari di flusso. Impostare questa quota come appropriato in base alla dimensione massima dei messaggi che l'applicazione si aspetta di ricevere. Si noti inoltre che `maxBufferSize` controlla la dimensione massima memorizzata nel buffer e l'imposta correttamente.  
  
    1.  Nel frammento seguente di configurazione, preso dall'esempio, viene illustrata l'impostazione della proprietà `TransferMode` su trasmissione in `basicHttpBinding` e un'associazione HTTP personalizzata:  
  
         <!-- TODO: review snippet reference [!code[c_HowTo_EnableStreaming#103](../../../../samples/snippets/common/VS_Snippets_CFX/c_howto_enablestreaming/common/app.config#103)]  -->  
  
    2.  Nel frammento di codice seguente viene illustrata l'impostazione della proprietà `TransferMode` su trasmissione in `basicHttpBinding` e un'associazione HTTP personalizzata.  
  
         [!code-csharp[c_HowTo_EnableStreaming_code#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_enablestreaming_code/cs/c_howto_enablestreaming_code.cs#2)]
         [!code-vb[c_HowTo_EnableStreaming_code#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_enablestreaming_code/vb/c_howto_enablestreaming_code.vb#2)]  
  
    3.  Nel frammento di codice seguente viene illustrata l'impostazione della proprietà `TransferMode` su trasmissione in un'associazione TCP personalizzata.  
  
         [!code-csharp[c_HowTo_EnableStreaming_code#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_enablestreaming_code/cs/c_howto_enablestreaming_code.cs#3)]
         [!code-vb[c_HowTo_EnableStreaming_code#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_enablestreaming_code/vb/c_howto_enablestreaming_code.vb#3)]  
  
3.  Le operazioni `GetStream`, `UploadStream` e `EchoStream` riguardano entrambe l'invio diretto di dati da un file o il salvataggio diretto dei dati ricevuti in un file. Il codice seguente riguarda `GetStream`.  
  
     [!code-csharp[c_HowTo_EnableStreaming#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_enablestreaming/cs/service.cs#4)]
     [!code-vb[c_HowTo_EnableStreaming#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_enablestreaming/vb/service.vb#4)]  
  
### <a name="writing-a-custom-stream"></a>Scrittura di un flusso personalizzato  
  
1.  Per eseguire un'elaborazione speciale su ogni blocco di un flusso di dati quando viene inviato o ricevuto, derivare una classe di flusso personalizzato da <xref:System.IO.Stream>. Come esempio di flusso personalizzato, il codice riportato di seguito contiene un metodo `GetReversedStream` e una classe `ReverseStream`.  
  
     `GetReversedStream` crea e restituisce una nuova istanza di `ReverseStream`. L'elaborazione effettiva si verifica quando il sistema legge dall'oggetto `ReverseStream`. Il metodo `ReverseStream.Read` legge un blocco di byte dal file sottostante, li inverte, quindi restituisce i byte invertiti. Questo metodo non inverte l'intero contenuto del file, ma un blocco di byte alla volta. In questo esempio viene illustrato come eseguire l'elaborazione del flusso mentre il contenuto viene letto o scritto da e verso il flusso.  
  
     [!code-csharp[c_HowTo_EnableStreaming#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_enablestreaming/cs/service.cs#2)]
     [!code-vb[c_HowTo_EnableStreaming#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_enablestreaming/vb/service.vb#2)]  
  
## <a name="see-also"></a>Vedere anche  
 [Dati di grandi dimensioni e Streaming](../../../../docs/framework/wcf/feature-details/large-data-and-streaming.md)   
 [Flusso](../../../../docs/framework/wcf/samples/stream.md)