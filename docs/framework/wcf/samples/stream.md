---
title: "Stream | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 58a3db81-20ab-4627-bf31-39d30b70b4fe
caps.latest.revision: 22
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 22
---
# Stream
L'esempio flusso illustra l'utilizzo della modalità di trasferimento con flusso.Il servizio espone molte operazioni che inviano e ricevono flussi.Questo esempio è indipendente.Sia il client che il servizio sono programmi console.  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine dell'argomento.  
  
 [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] può comunicare in due modalità di trasferimento, memorizzando i dati nel buffer o utilizzando il flusso.Per impostazione predefinita, il messaggio viene memorizzato nel buffer e deve essere recapitato completamente prima che un destinatario sia in grado di leggerlo.Nella modalità di trasferimento con flusso, il destinatario può iniziare a elaborare il messaggio prima che esso venga recapitato completamente.La modalità di trasmissione con flusso è utile quando le informazioni passate sono lunghe e possono essere elaborate in serie.La modalità di trasmissione con flusso è utile anche quando il messaggio è troppo grande da memorizzare completamente nel buffer.  
  
## Flusso e contratti di servizio  
 Il flusso va preso in considerazione quando si progetta un contratto di servizio.Se un'operazione riceve o restituisce grandi quantità di dati, è necessario trasmetterli per evitare un utilizzo eccessivo della memoria a causa della memorizzazione nel buffer di messaggi di input o output.Per trasmettere dati, il parametro che contiene i dati deve essere il solo parametro del messaggio.Ad esempio, se il messaggio di input è quello da trasmettere, l'operazione deve avere esattamente un parametro di input.Allo stesso modo, se deve essere trasmesso il messaggio di output, l'operazione deve avere esattamente un solo parametro di output o un solo valore restituito.In entrambi i casi, il parametro o il valore restituito devono essere `Stream`, `Message`, o `IXmlSerializable`.Segue il contratto di servizio utilizzato in questo esempio di flusso.  
  
```  
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
public interface IStreamingSample  
{  
    [OperationContract]  
    Stream GetStream(string data);  
    [OperationContract]  
    bool UploadStream(Stream stream);  
    [OperationContract]  
    Stream EchoStream(Stream stream);  
    [OperationContract]  
    Stream GetReversedStream();  
  
}  
```  
  
 L'operazione `GetStream` riceve alcuni dati di input come stringa, memorizzata nel buffer e restituisce un `Stream`, trasmesso.Viceversa, `UploadStream` accetta uno `Stream` \(trasmesso\) e restituisce un `bool` \(memorizzato nel buffer\).`EchoStream` accetta e restituisce uno `Stream` ed è un esempio di un'operazione i cui messaggi di input e output vengono entrambi trasmessi.Infine, `GetReversedStream` non prende input e restituisce un `Stream` \(trasmesso\).  
  
## Attivazione dei trasferimenti con flusso  
 La definizione di contratti dell'operazione, come descritto precedentemente, fornisce la trasmissione a livello del modello di programmazione.Se ci si ferma a questo punto, il trasporto memorizza ancora nel buffer l'intero contenuto del messaggio.Per abilitare il flusso di trasmissione, selezionare la modalità di trasferimento dall'elemento di associazione del trasporto.L'elemento di associazione presenta una proprietà `TransferMode` che può essere impostata su `Buffered`, `Streamed`, `StreamedRequest` o `StreamedResponse`.L'impostazione della modalità di trasferimento su `Streamed` consente di attivare la comunicazione con flusso bidirezionale.L'impostazione della modalità di trasferimento su `StreamedRequest` o `StreamedResponse` consente di attivare la comunicazione con flusso soltanto come richiesta o come risposta.  
  
 `basicHttpBinding` espone la proprietà `TransferMode` sull'associazione come fanno anche `NetTcpBinding` e `NetNamedPipeBinding`.Per impostare la modalità di trasferimento degli altri trasporti è necessario creare un'associazione personalizzata.  
  
 Il codice di configurazione seguente, preso dall'esempio illustra l'impostazione della proprietà `TransferMode` su trasmissione su `basicHttpBinding` e un'associazione HTTP personalizzata:  
  
```  
<!-- An example basicHttpBinding using streaming. -->  
<basicHttpBinding>  
  <binding name="HttpStreaming" maxReceivedMessageSize="67108864"  
           transferMode="Streamed"/>  
</basicHttpBinding>  
<!-- An example customBinding using HTTP and streaming.-->  
<customBinding>  
  <binding name="Soap12">  
    <textMessageEncoding messageVersion="Soap12WSAddressing10" />  
    <httpTransport transferMode="Streamed"  
                   maxReceivedMessageSize="67108864"/>  
  </binding>  
</customBinding>  
  
```  
  
 Oltre a impostare `transferMode` su `Streamed`, il codice di configurazione precedente imposta `maxReceivedMessageSize` su 64 MB.Analogo a un meccanismo di difesa, `maxReceivedMessageSize` pone un limite alla dimensione massima consentita dei messaggi in ricezione.La misura predefinita è `maxReceivedMessageSize` 64 KB che è di solito troppo bassa per gli scenari di flusso.  
  
## Elaborazione dei dati durante la trasmissione  
 Le operazioni `GetStream`, `UploadStream` e `EchoStream` riguardano entrambe l'invio diretto di dati da un file o il salvataggio diretto dei dati ricevuti in un file.C'è tuttavia, in alcuni casi, un requisito per inviare o ricevere grandi quantità di dati ed eseguire alcune elaborazioni su blocchi di dati appena essi vengono ricevuti.Una modalità per indirizzare tali scenari è scrivere un flusso personalizzato \(una classe che deriva da <xref:System.IO.Stream>\) che elabora i dati mentre vengono letti o scritti.Ne sono un esempio l'operazione `GetReversedStream` e la classe `ReverseStream`.  
  
 `GetReversedStream` crea e restituisce una nuova istanza di `ReverseStream`.L'elaborazione effettiva si verifica quando il sistema legge da quell'oggetto `ReverseStream`.L'implementazione `ReverseStream.Read` legge un blocco di byte dal file sottostante, li inverte, quindi restituisce i byte invertiti.Non inverte il contenuto del file intero; inverte uno blocco di byte alla volta.Questo è un esempio per mostrare come è possibile eseguire elaborazione del flusso mentre il contenuto viene letto o scritto da e verso il flusso.  
  
```  
class ReverseStream : Stream  
{  
  
    FileStream inStream;  
    internal ReverseStream(string filePath)  
    {  
        //Opens the file and places a StreamReader around it.  
        inStream = File.OpenRead(filePath);  
    }  
  
    // Other methods removed for brevity.  
  
    public override int Read(byte[] buffer, int offset, int count)  
    {  
        int countRead=inStream.Read(buffer, offset,count);  
        ReverseBuffer(buffer, offset, countRead);  
        return countRead;  
    }  
  
    public override void Close()  
    {  
        inStream.Close();  
        base.Close();  
    }  
    protected override void Dispose(bool disposing)  
    {  
        inStream.Dispose();  
        base.Dispose(disposing);  
    }  
    void ReverseBuffer(byte[] buffer, int offset, int count)  
    {  
        int i, j;  
        for (i = offset, j = offset + count - 1; i < j; i++, j--)  
        {  
            byte currenti = buffer[i];  
            buffer[i] = buffer[j];  
            buffer[j] = currenti;  
        }  
  
    }  
}  
```  
  
## Esecuzione dell'esempio  
 Per eseguire l'esempio, prima compilare il servizio e il client seguendo le istruzioni alla fine di questo documento.Quindi avviare il servizio e il client in due finestre della console diverse.Quando il client si avvia, aspetta la pressione del tasto INVIO quando il servizio è pronto.Il client chiama quindi prima i metodi `GetStream()`, `UploadStream()` e `GetReversedStream()` su HTTP e quindi su TCP.Ecco un esempio di output restituito dal servizio seguito da un esempio di output del client:  
  
 Output del servizio:  
  
```  
The streaming service is ready.  
Press <ENTER> to terminate service.  
  
Saving to file D:\...\uploadedfile  
......................  
File D:\...\uploadedfile saved  
Saving to file D:\...\uploadedfile  
...............  
File D:\...\uploadedfile saved  
```  
  
 Output del client:  
  
```  
Press <ENTER> when service is ready  
------ Using HTTP ------   
Calling GetStream()  
Saving to file D:\...\clientfile  
......................  
Wrote 33405 bytes to stream  
  
File D:\...\clientfile saved  
Calling UploadStream()  
Calling GetReversedStream()  
Saving to file D:\...\clientfile  
......................  
Wrote 33405 bytes to stream  
  
File D:\...\clientfile saved  
------ Using Custom HTTP ------  
Calling GetStream()  
Saving to file D:\...\clientfile  
...............  
Wrote 33405 bytes to stream  
  
File D:\...\clientfile saved  
Calling UploadStream()  
Calling GetReversedStream()  
Saving to file D:\...\clientfile  
...............  
Wrote 33405 bytes to stream  
  
File D:\...\clientfile saved  
  
Press <ENTER> to terminate client.  
```  
  
#### Per impostare, compilare ed eseguire l'esempio  
  
1.  Assicurarsi di aver eseguito [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare l'edizione in C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
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
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Contract\Service\Stream`  
  
## Vedere anche