---
title: "Codificatore di messaggi personalizzato: codificatore di testi personalizzato | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 68ff5c74-3d33-4b44-bcae-e1d2f5dea0de
caps.latest.revision: 28
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 28
---
# Codificatore di messaggi personalizzato: codificatore di testi personalizzato
Questo esempio illustra come implementare un codificatore di messaggi di testi personalizzato utilizzando [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].  
  
> [!WARNING]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Extensibility\MessageEncoder\Text`  
  
 La classe <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement> di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] supporta solo le codifiche UTF\-8, UTF\-16 e Big Endian Unicode.Il codificatore di messaggi di testi personalizzato in questo esempio supporta ogni codifica dei caratteri supportata dalla piattaforma che può essere necessaria per l'interoperabilità.L'esempio è costituito da un programma di console client \(.exe\) e da una libreria di servizi \(.dll\) ospitati su Internet Information Services \(IIS\).Il servizio implementa un contratto che definisce un modello di comunicazione request\/reply.Il contratto viene definito dall'interfaccia `ICalculator`, che espone operazioni matematiche \(somma, sottrazione, moltiplicazione e divisione\).Il client esegue richieste sincrone a un'operazione matematica specificata e il servizio risponde fornendo il risultato.Il client e il servizio utilizzano `CustomTextMessageEncoder` anziché la classe <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement> predefinita.  
  
 L'implementazione del codificatore personalizzato è costituita da una factory del codificatore di messaggi, un codificatore di messaggi, un messaggio che codifica l'elemento di associazione e un gestore di configurazione, e illustra quanto segue:  
  
-   Compilazione di un codificatore personalizzato e di una factory del codificatore.  
  
-   Creazione di un elemento di associazione per un codificatore personalizzato.  
  
-   Utilizzo della configurazione dell'associazione personalizzata per l'integrazione di elementi di associazione personalizzati.  
  
-   Sviluppo di un gestore di configurazione personalizzato per consentire la configurazione del file di un elemento di associazione personalizzato.  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Installare [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 4.0 utilizzando il comando seguente.  
  
    ```  
    %windir%\Microsoft.NET\Framework\v4.0.XXXXX\aspnet_regiis.exe /i /enable  
  
    ```  
  
2.  Verificare di avere eseguito la [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
3.  Per compilare la soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
4.  Per eseguire l'esempio su una configurazione con un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
## Factory di codificatori di messaggi e codificatori dei messaggi.  
 Quando la classe <xref:System.ServiceModel.ServiceHost> o il canale client vengono aperti, il componente della fase di progettazione `CustomTextMessageBindingElement` crea `CustomTextMessageEncoderFactory`.La factory crea `CustomTextMessageEncoder`.Il codificatore di messaggi aziona entrambi in modalità di trasmissione e in modalità di memorizzazione nel buffer.Utilizza le classi <xref:System.Xml.XmlReader> e <xref:System.Xml.XmlWriter> per leggere e scrivere i messaggi, rispettivamente.Al contrario dei lettori e writer XML ottimizzati di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], che supportano solo UTF\-8, UTF\-16 e Big Endian Unicode, questi lettori e writer supportano ogni piattaforma di codifica supportata.  
  
 Nel codice seguente viene illustrato il codificatore di messaggio personalizzato.  
  
```csharp  
  
public class CustomTextMessageEncoder : MessageEncoder  
{  
    private CustomTextMessageEncoderFactory factory;  
    private XmlWriterSettings writerSettings;  
    private string contentType;  
  
    public CustomTextMessageEncoder(CustomTextMessageEncoderFactory factory)  
    {  
        this.factory = factory;  
  
        this.writerSettings = new XmlWriterSettings();  
        this.writerSettings.Encoding = Encoding.GetEncoding(factory.CharSet);  
        this.contentType = string.Format("{0}; charset={1}",   
            this.factory.MediaType, this.writerSettings.Encoding.HeaderName);  
    }  
  
    public override string ContentType  
    {  
        get  
        {  
            return this.contentType;  
        }  
    }  
  
    public override string MediaType  
    {  
        get   
        {  
            return factory.MediaType;  
        }  
    }  
  
    public override MessageVersion MessageVersion  
    {  
        get   
        {  
            return this.factory.MessageVersion;  
        }  
    }  
  
    public override Message ReadMessage(ArraySegment<byte> buffer, BufferManager bufferManager, string contentType)  
    {     
        byte[] msgContents = new byte[buffer.Count];  
        Array.Copy(buffer.Array, buffer.Offset, msgContents, 0, msgContents.Length);  
        bufferManager.ReturnBuffer(buffer.Array);  
  
        MemoryStream stream = new MemoryStream(msgContents);  
        return ReadMessage(stream, int.MaxValue);  
    }  
  
    public override Message ReadMessage(Stream stream, int maxSizeOfHeaders, string contentType)  
    {  
        XmlReader reader = XmlReader.Create(stream);  
        return Message.CreateMessage(reader, maxSizeOfHeaders, this.MessageVersion);  
    }  
  
    public override ArraySegment<byte> WriteMessage(Message message, int maxMessageSize, BufferManager bufferManager, int messageOffset)  
    {  
        MemoryStream stream = new MemoryStream();  
        XmlWriter writer = XmlWriter.Create(stream, this.writerSettings);  
        message.WriteMessage(writer);  
        writer.Close();  
  
        byte[] messageBytes = stream.GetBuffer();  
        int messageLength = (int)stream.Position;  
        stream.Close();  
  
        int totalLength = messageLength + messageOffset;  
        byte[] totalBytes = bufferManager.TakeBuffer(totalLength);  
        Array.Copy(messageBytes, 0, totalBytes, messageOffset, messageLength);  
  
        ArraySegment<byte> byteArray = new ArraySegment<byte>(totalBytes, messageOffset, messageLength);  
        return byteArray;  
    }  
  
    public override void WriteMessage(Message message, Stream stream)  
    {  
        XmlWriter writer = XmlWriter.Create(stream, this.writerSettings);  
        message.WriteMessage(writer);  
        writer.Close();  
    }  
}  
```  
  
 Nell'esempio di codice seguente viene illustrato come compilare la factory del codificatore di messaggi.  
  
```csharp  
public class CustomTextMessageEncoderFactory : MessageEncoderFactory  
{  
    private MessageEncoder encoder;  
    private MessageVersion version;  
    private string mediaType;  
    private string charSet;  
  
    internal CustomTextMessageEncoderFactory(string mediaType, string charSet,  
        MessageVersion version)  
    {  
        this.version = version;  
        this.mediaType = mediaType;  
        this.charSet = charSet;  
        this.encoder = new CustomTextMessageEncoder(this);  
    }  
  
    public override MessageEncoder Encoder  
    {  
        get   
        {   
            return this.encoder;  
        }  
    }  
  
    public override MessageVersion MessageVersion  
    {  
        get   
        {   
            return this.version;  
        }  
    }  
  
    internal string MediaType  
    {  
        get  
        {  
            return this.mediaType;  
        }  
    }  
  
    internal string CharSet  
    {  
        get  
        {  
            return this.charSet;  
        }  
    }  
}  
```  
  
## Elemento di associazione di codifica dei messaggi  
 Gli elementi di associazione consentono la configurazione dello stack di runtime di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].Per utilizzare il codificatore di messaggi personalizzato in un'applicazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] è necessario un elemento di associazione che crea la factory del codificatore di messaggi con le impostazioni adatte al livello adatto nello stack di runtime.  
  
 La classe `CustomTextMessageBindingElement` deriva dalla classe base <xref:System.ServiceModel.Channels.BindingElement> ed eredita dalla classe <xref:System.ServiceModel.Channels.MessageEncodingBindingElement>.Ciò consente agli altri componenti di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] di riconoscere questo elemento di associazione come elemento di associazione di codifica dei messaggi.L'implementazione del metodo <xref:System.ServiceModel.Channels.MessageEncodingBindingElement.CreateMessageEncoderFactory%2A> restituisce un'istanza della factory del codificatore di messaggi corrispondente con le impostazioni appropriate.  
  
 `CustomTextMessageBindingElement` espone impostazioni per `MessageVersion`, `ContentType` e `Encoding` tramite proprietà.Il codificatore supporta le versioni Soap11Addressing e Soap12Addressing1.L'impostazione predefinita è Soap11Addressing1.Il valore predefinito della proprietà `ContentType` è "text\/xml".La proprietà `Encoding` consente di impostare il valore della codifica dei caratteri desiderata.Il client e il servizio di esempio utilizzano la codifica dei caratteri ISO\-8859\-1 \(Latin1\) che non è supportata dalla classe <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement> di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
 Nel codice seguente viene illustrato come creare l'associazione a livello di codice utilizzando il codificatore del messaggio di testo personalizzato.  
  
```  
ICollection<BindingElement> bindingElements = new List<BindingElement>();  
HttpTransportBindingElement httpBindingElement = new HttpTransportBindingElement();  
CustomTextMessageBindingElement textBindingElement = new CustomTextMessageBindingElement();  
bindingElements.Add(textBindingElement);  
bindingElements.Add(httpBindingElement);  
CustomBinding binding = new CustomBinding(bindingElements);  
```  
  
## Aggiunta del supporto dei metadati per un elemento di associazione di codifica dei messaggi  
 Qualsiasi tipo che deriva da <xref:System.ServiceModel.Channels.MessageEncodingBindingElement> deve eseguire l'aggiornamento della versione dell'associazione SOAP nel documento WSDL generato per il servizio.Ciò viene fatto implementando il metodo `ExportEndpoint` sull'interfaccia <xref:System.ServiceModel.Description.IWsdlExportExtension> e modificando quindi il WSDL generato.In questo esempio, `CustomTextMessageBindingElement` utilizza la logica di esportazione WSDL di `TextMessageEncodingBinidngElement`.  
  
 Per questo esempio, la configurazione del client è manuale.Non è possibile utilizzare Svcutil.exe per generare la configurazione del client perché `CustomTextMessageBindingElement` non esporta un'asserzione di criteri per descrivere il comportamento.Generalmente si deve implementare l'interfaccia <xref:System.ServiceModel.Description.IPolicyExportExtension> su un elemento di associazione personalizzato per esportare un'asserzione di criteri personalizzata che descrive il comportamento o la funzionalità implementata dall'elemento di associazione.Per un esempio su come esportare un'asserzione di criteri per un elemento di associazione personalizzato, vedere l'esempio [Trasporto UDP](../../../../docs/framework/wcf/samples/transport-udp.md).  
  
## Gestore di configurazione dell'associazione di codifica dei messaggi  
 La sezione precedente mostra come utilizzare il codificatore dei messaggi di testo personalizzato a livello di codice.`CustomTextMessageEncodingBindingSection` implementa un gestore di configurazione che consente di specificare l'utilizzo di un codificatore dei messaggi di testo personalizzato all'interno di un file di configurazione.La classe `CustomTextMessageEncodingBindingSection` deriva dalla classe <xref:System.ServiceModel.Configuration.BindingElementExtensionElement>.La proprietà `BindingElementType` informa il sistema di configurazione del tipo di elemento di associazione da creare per questa sezione.  
  
 Tutte le impostazioni definite da `CustomTextMessageBindingElement` sono esposte come proprietà in `CustomTextMessageEncodingBindingSection`.La classe <xref:System.Configuration.ConfigurationPropertyAttribute> assiste nell'eseguire il mapping degli attributi dell'elemento di configurazione alle proprietà e nell'impostazione dei valori predefiniti se l'attributo non è impostato.Dopo i valori della configurazione sono caricati e applicati alle proprietà del tipo, e viene chiamato il metodo <xref:System.ServiceModel.Configuration.BindingElementExtensionElement.CreateBindingElement%2A>. Esso converte le proprietà in un'istanza concreta di un elemento di associazione.  
  
 Questo gestore di configurazione esegue il mapping alla rappresentazione seguente in App.config o Web.config per il servizio o il client.  
  
```  
<customTextMessageEncoding encoding="utf-8" contentType="text/xml" messageVersion="Soap11Addressing1" />  
  
```  
  
 Nell'esempio viene utilizzata la codifica ISO\-8859\-1.  
  
 Per utilizzare questo gestore di configurazione deve essere registrato utilizzando l'elemento di configurazione seguente.  
  
```  
<extensions>  
    <bindingElementExtensions>  
        <add name="customTextMessageEncoding" type="   
Microsoft.ServiceModel.Samples.CustomTextMessageEncodingBindingSection,   
                  CustomTextMessageEncoder" />  
    </bindingElementExtensions>  
</extensions>  
  
```  
  
## Vedere anche