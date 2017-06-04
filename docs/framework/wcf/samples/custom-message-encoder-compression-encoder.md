---
title: "Codificatore di messaggi personalizzato: codificatore di compressione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 57450b6c-89fe-4b8a-8376-3d794857bfd7
caps.latest.revision: 37
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 37
---
# Codificatore di messaggi personalizzato: codificatore di compressione
In questo esempio viene illustrato come implementare un codificatore personalizzato utilizzando la piattaforma [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Extensibility\MessageEncoder\Compression`  
  
## Dettagli dell'esempio  
 Questo esempio è costituito da un programma di console client \(con estensione exe\), da un programma di console del servizio ospitato \(.exe\) e da una libreria di codificatori di messaggi di compressione \(dll\).Il servizio implementa un contratto che definisce un modello di comunicazione request\/reply.Il contratto viene definito dall'interfaccia `ISampleServer` che espone operazioni di ripetizione di stringhe di base \(`Echo` e `BigEcho`\).Il client esegue richieste sincrone a un'operazione specificata e il servizio risponde ripetendo il messaggio al client.L'attività del client e del servizio è visibile nella finestra della console.Lo scopo di questo esempio è illustrare come scrivere un codificatore personalizzato e dimostrare l'impatto della compressione di un messaggio sulla rete.È possibile aggiungere strumenti al codificatore di messaggi di compressione per calcolare la dimensione del messaggio, il tempo di elaborazione o entrambi.  
  
> [!NOTE]
>  In .NET Framework 4 la decompressione automatica è stata abilitata in un client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] se il server invia una risposta compressa \(creata con un algoritmo quale GZip o Deflate\).Se il servizio è ospitato su Web in Internet Information Server \(IIS\), IIS è in grado di essere configurato per il servizio per inviare una risposta compressa.Questo esempio può essere utilizzato se il requisito è effettuare compressione e decompressione sia nel client che nel servizio o se il servizio è indipendente.  
  
 Nell'esempio viene illustrato come compilare e integrare un codificatore di messaggi personalizzato in un'applicazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].La libreria GZipEncoder.dll viene distribuita con il client e il servizio.In questo esempio viene inoltre illustrato l'impatto della compressione dei messaggi.Il codice in GZipEncoder.dll dimostra le operazioni seguenti:  
  
-   Compilazione di un codificatore personalizzato e di una factory del codificatore.  
  
-   Sviluppo di un elemento di associazione per un codificatore personalizzato.  
  
-   Utilizzo della configurazione dell'associazione personalizzata per l'integrazione di elementi di associazione personalizzati.  
  
-   Sviluppo di un gestore di configurazione personalizzato per consentire la configurazione del file di un elemento di associazione personalizzato.  
  
 Come indicato in precedenza, in un codificatore personalizzato vengono implementati molti livelli.Per illustrare meglio la relazione tra i singoli livelli, nell'elenco seguente è fornito un ordine semplificato di eventi per l'avvio del servizio:  
  
1.  Il server viene avviato.  
  
2.  Le informazioni di configurazione vengono lette.  
  
    1.  La configurazione del servizio registra il gestore di configurazione personalizzato.  
  
    2.  L'host del servizio viene creato e aperto.  
  
    3.  L'elemento di configurazione personalizzato crea e restituisce l'elemento di associazione personalizzato.  
  
    4.  L'elemento di associazione personalizzato crea e restituisce una factory del codificatore di messaggi.  
  
3.  Un messaggio viene ricevuto.  
  
4.  La factory del codificatore di messaggi restituisce un codificatore di messaggi per la lettura del messaggio e la scrittura della risposta.  
  
5.  Il livello del codificatore viene implementato come una class factory.Solo la class factory del codificatore deve essere esposta pubblicamente per il codificatore personalizzato.L'oggetto della factory viene restituito dall'elemento di associazione quando viene creato l'oggetto <xref:System.ServiceModel.ServiceHost> o <xref:System.ServiceModel.ChannelFactory%601>.I codificatori di messaggi possono operare in modalità di memorizzazione nel buffer o di trasmissione.In questo esempio vengono illustrate entrambe le modalità.  
  
 A ogni modalità è associato un metodo `ReadMessage` e un metodo `WriteMessage` sulla classe `MessageEncoder` astratta.La maggior parte del lavoro di codifica si verifica in questi metodi.Nell'esempio viene eseguito il wrapping dei codificatori di testo e di messaggi binari esistenti.In questo modo l'esempio può delegare la lettura e la scrittura della rappresentazione in rete dei messaggi al codificatore interno e il codificatore di compressione può comprimere o decomprimere i risultati.Poiché non è presente una pipeline per la codifica dei messaggi, questo l'unico modello per l'utilizzo di più codificatori in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].Quando il messaggio è stato decompresso, il messaggio risultante viene passato sullo stack affinché venga gestito dallo stack di canali.Durante la compressione, il messaggio compresso risultante viene scritto direttamente nel flusso fornito.  
  
 In questo esempio vengono utilizzati metodi helper \(`CompressBuffer` e `DecompressBuffer`\) per eseguire la conversione da buffer a flussi allo scopo di utilizzare la classe `GZipStream`.  
  
 Le classi `ReadMessage` e `WriteMessage` memorizzate nel buffer utilizzano la classe `BufferManager`.Il codificatore è accessibile solo tramite la factory del codificatore.La classe `MessageEncoderFactory` astratta fornisce una proprietà denominata `Encoder` per l'accesso al codificatore corrente e un metodo denominato `CreateSessionEncoder` per la creazione di un codificatore che supporta le sessioni.Tale codificatore può essere utilizzato nello scenario in cui il canale supporta le sessioni, è ordinato e affidabile.Questo scenario consente l'ottimizzazione in ogni sessione dei dati scritti in rete.Se non si desidera questo aspetto, non deve essere eseguito l'overload del metodo di base.La proprietà `Encoder` fornisce un meccanismo di accesso al codificatore senza sessione e l'implementazione predefinita del metodo `CreateSessionEncoder` restituisce il valore della proprietà.Poiché nell'esempio viene eseguito il wrapping di un codificatore esistente per fornire la compressione, l'implementazione `MessageEncoderFactory` accetta un elemento `MessageEncoderFactory` che rappresenta la factory del codificatore interna.  
  
 Dopo aver definito il codificatore e la factory del codificatore, è possibile utilizzarli con un client e un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].Tuttavia, questi codificatori devono essere aggiunti allo stack di canali.È possibile dedurre le classi dalle classi <xref:System.ServiceModel.ServiceHost> e <xref:System.ServiceModel.ChannelFactory%601> ed eseguire l'override dei metodi `OnInitialize` per aggiungere manualmente questa factory del codificatore.È inoltre possibile esporre la factory del codificatore tramite un elemento di associazione personalizzato.  
  
 Per creare un nuovo elemento di associazione personalizzato, derivare una classe dalla classe <xref:System.ServiceModel.Channels.BindingElement>.Sono tuttavia disponibili molti tipi di elementi di associazione.Per assicurare che l'elemento di associazione personalizzato venga riconosciuto come un elemento di associazione di codifica dei messaggi, è necessario implementare anche <xref:System.ServiceModel.Channels.MessageEncodingBindingElement>.<xref:System.ServiceModel.Channels.MessageEncodingBindingElement> espone un metodo per la creazione di una nuova factory del codificatore di messaggi \(`CreateMessageEncoderFactory`\), che viene implementato per restituire un'istanza della factory del codificatore di messaggi corrispondente.Inoltre, <xref:System.ServiceModel.Channels.MessageEncodingBindingElement> dispone di una proprietà per indicare la versione Addressing.Poiché in questo esempio viene eseguito il wrapping dei codificatori esistenti, l'implementazione di esempio esegue il wrapping anche degli elementi di associazione del codificatore esistente e accetta un elemento di associazione del codificatore interno come parametro del costruttore e lo espone tramite una proprietà.Nell'esempio di codice seguente viene illustrata l'implementazione della classe `GZipMessageEncodingBindingElement`.  
  
```  
public sealed class GZipMessageEncodingBindingElement   
                        : MessageEncodingBindingElement //BindingElement  
                        , IPolicyExportExtension  
{  
  
    //We use an inner binding element to store information   
    //required for the inner encoder.  
    MessageEncodingBindingElement innerBindingElement;  
  
        //By default, use the default text encoder as the inner encoder.  
        public GZipMessageEncodingBindingElement()  
            : this(new TextMessageEncodingBindingElement()) { }  
  
    public GZipMessageEncodingBindingElement(MessageEncodingBindingElement messageEncoderBindingElement)  
    {  
        this.innerBindingElement = messageEncoderBindingElement;  
    }  
  
    public MessageEncodingBindingElement InnerMessageEncodingBindingElement  
    {  
        get { return innerBindingElement; }  
        set { innerBindingElement = value; }  
    }  
  
    //Main entry point into the encoder binding element.   
    // Called by WCF to get the factory that creates the  
    //message encoder.  
    public override MessageEncoderFactory CreateMessageEncoderFactory()  
    {  
        return new   
GZipMessageEncoderFactory(innerBindingElement.CreateMessageEncoderFactory());  
    }  
  
    public override MessageVersion MessageVersion  
    {  
        get { return innerBindingElement.MessageVersion; }  
        set { innerBindingElement.MessageVersion = value; }  
    }  
  
    public override BindingElement Clone()  
    {  
        return new   
        GZipMessageEncodingBindingElement(this.innerBindingElement);  
    }  
  
    public override T GetProperty<T>(BindingContext context)  
    {  
        if (typeof(T) == typeof(XmlDictionaryReaderQuotas))  
        {  
            return innerBindingElement.GetProperty<T>(context);  
        }  
        else   
        {  
            return base.GetProperty<T>(context);  
        }  
    }  
  
    public override IChannelFactory<TChannel> BuildChannelFactory<TChannel>(BindingContext context)  
    {  
        if (context == null)  
            throw new ArgumentNullException("context");  
  
        context.BindingParameters.Add(this);  
        return context.BuildInnerChannelFactory<TChannel>();  
    }  
  
    public override IChannelListener<TChannel> BuildChannelListener<TChannel>(BindingContext context)  
    {  
        if (context == null)  
            throw new ArgumentNullException("context");  
  
        context.BindingParameters.Add(this);  
        return context.BuildInnerChannelListener<TChannel>();  
    }  
  
    public override bool CanBuildChannelListener<TChannel>(BindingContext context)  
    {  
        if (context == null)  
            throw new ArgumentNullException("context");  
  
        context.BindingParameters.Add(this);  
        return context.CanBuildInnerChannelListener<TChannel>();  
    }  
  
    void IPolicyExportExtension.ExportPolicy(MetadataExporter exporter, PolicyConversionContext policyContext)  
    {  
        if (policyContext == null)  
        {  
            throw new ArgumentNullException("policyContext");  
        }  
       XmlDocument document = new XmlDocument();  
       policyContext.GetBindingAssertions().Add(document.CreateElement(  
            GZipMessageEncodingPolicyConstants.GZipEncodingPrefix,  
            GZipMessageEncodingPolicyConstants.GZipEncodingName,  
            GZipMessageEncodingPolicyConstants.GZipEncodingNamespace));  
    }  
}  
```  
  
 Si noti che la classe `GZipMessageEncodingBindingElement` implementa l'interfaccia `IPolicyExportExtension`, in modo che questo elemento di associazione può essere esportato come un criterio nei metadati, come mostrato nell'esempio seguente.  
  
```  
<wsp:Policy wsu:Id="BufferedHttpSampleServer_ISampleServer_policy">  
    <wsp:ExactlyOne>  
      <wsp:All>  
        <gzip:text xmlns:gzip=  
        "http://schemas.microsoft.com/ws/06/2004/mspolicy/netgzip1" />   
       <wsaw:UsingAddressing />   
     </wsp:All>  
   </wsp:ExactlyOne>  
</wsp:Policy>  
  
```  
  
 La classe `GZipMessageEncodingBindingElementImporter` implementa l'interfaccia `IPolicyImportExtension` e importa i criteri per `GZipMessageEncodingBindingElement`.Lo strumento Svcutil.exe può essere utilizzato per importare criteri nel file di configurazione e, per gestire `GZipMessageEncodingBindingElement`, è necessario aggiungere quanto segue al file Svcutil.exe.config.  
  
```  
  
<configuration>  
  <system.serviceModel>  
    <extensions>  
      <bindingElementExtensions>  
        <add name="gzipMessageEncoding"   
          type=  
            "Microsoft.ServiceModel.Samples.GZipMessageEncodingElement, GZipEncoder, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />  
      </bindingElementExtensions>  
    </extensions>  
    <client>  
      <metadata>  
        <policyImporters>  
          <remove type=  
"System.ServiceModel.Channels.MessageEncodingBindingElementImporter, System.ServiceModel, Version=3.0.0.0, Culture=neutral, PublicKeyToken=b77a5c561934e089" />  
          <extension type=  
"Microsoft.ServiceModel.Samples.GZipMessageEncodingBindingElementImporter, GZipEncoder, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />  
        </policyImporters>  
      </metadata>  
    </client>  
  </system.serviceModel>  
</configuration>  
  
```  
  
 A questo punto, poiché è disponibile un elemento di associazione corrispondente per il codificatore di compressione, è possibile associarlo a livello di programmazione nel servizio o client costruendo un nuovo oggetto di associazione personalizzato e aggiungendo ad esso l'elemento di associazione personalizzato, come mostrato nel codice di esempio seguente.  
  
```  
ICollection<BindingElement> bindingElements = new List<BindingElement>();  
HttpTransportBindingElement httpBindingElement = new HttpTransportBindingElement();  
GZipMessageEncodingBindingElement compBindingElement = new GZipMessageEncodingBindingElement ();  
bindingElements.Add(compBindingElement);  
bindingElements.Add(httpBindingElement);  
CustomBinding binding = new CustomBinding(bindingElements);  
binding.Name = "SampleBinding";  
binding.Namespace = "http://tempuri.org/bindings";  
  
```  
  
 Sebbene questo possa essere sufficiente per la maggioranza degli scenari utente, se un servizio deve essere ospitato sul Web è essenziale che supporti un file di configurazione.Per supportare lo scenario ospitato sul Web, è necessario sviluppare un gestore di configurazione personalizzato per consentire a un elemento di associazione personalizzato di essere configurabile in un file.  
  
 È possibile compilare un gestore di configurazione per l'elemento di associazione nel sistema di configurazione fornito da [!INCLUDE[dnprdnlong](../../../../includes/dnprdnlong-md.md)].Il gestore di configurazione per l'elemento di associazione deve derivare dalla classe <xref:System.ServiceModel.Configuration.BindingElementExtensionElement>.La proprietà `BindingElementType` viene utilizzata per informare il sistema di configurazione del tipo di elemento di associazione da creare per questa sezione.Tutti gli aspetti di `BindingElement` che possono essere impostati devono essere esposti come proprietà nella classe derivata <xref:System.ServiceModel.Configuration.BindingElementExtensionElement>.<xref:System.Configuration.ConfigurationPropertyAttribute> viene utilizzato per assistere nell'operazione di mapping degli attributi dell'elemento di configurazione alle proprietà e nell'impostazione dei valori predefiniti se gli attributi non sono disponibili.Dopo aver caricato i valori della configurazione e averli applicati alle proprietà, viene chiamato il metodo <xref:System.ServiceModel.Configuration.BindingElementExtensionElement.CreateBindingElement%2A> che converte le proprietà in un'istanza concreta di un elemento di associazione.Il metodo <xref:System.ServiceModel.Configuration.BindingElementExtensionElement.ApplyConfiguration%2A> viene utilizzato per convertire le proprietà nella classe derivata <xref:System.ServiceModel.Configuration.BindingElementExtensionElement> nei valori da impostare sull'elemento di associazione appena creato.  
  
 Nel codice di esempio seguente viene mostrata l'implementazione di `GZipMessageEncodingElement`.  
  
```  
public class GZipMessageEncodingElement : BindingElementExtensionElement  
{  
    public GZipMessageEncodingElement()  
    {  
    }  
  
//Called by the WCF to discover the type of binding element this   
//config section enables  
    public override Type BindingElementType  
    {  
        get { return typeof(GZipMessageEncodingBindingElement); }  
    }  
  
    //The only property we need to configure for our binding element is   
    //the type of inner encoder to use. Here, we support text and  
    //binary.  
    [ConfigurationProperty("innerMessageEncoding",   
                         DefaultValue = "textMessageEncoding")]  
    public string InnerMessageEncoding  
    {  
        get { return (string)base["innerMessageEncoding"]; }  
        set { base["innerMessageEncoding"] = value; }  
    }  
  
    //Called by the WCF to apply the configuration settings (the   
    //property above) to the binding element  
    public override void ApplyConfiguration(BindingElement bindingElement)  
    {  
        GZipMessageEncodingBindingElement binding =   
                (GZipMessageEncodingBindingElement)bindingElement;  
        PropertyInformationCollection propertyInfo =   
                    this.ElementInformation.Properties;  
        if (propertyInfo["innerMessageEncoding"].ValueOrigin !=   
                                     PropertyValueOrigin.Default)  
        {  
            switch (this.InnerMessageEncoding)  
            {  
                case "textMessageEncoding":  
                    binding.InnerMessageEncodingBindingElement =   
                      new TextMessageEncodingBindingElement();  
                    break;  
                case "binaryMessageEncoding":  
                    binding.InnerMessageEncodingBindingElement =   
                         new BinaryMessageEncodingBindingElement();  
                    break;  
            }  
        }  
    }  
  
    //Called by the WCF to create the binding element  
    protected override BindingElement CreateBindingElement()  
    {  
        GZipMessageEncodingBindingElement bindingElement =   
                new GZipMessageEncodingBindingElement();  
        this.ApplyConfiguration(bindingElement);  
        return bindingElement;  
    }  
}   
```  
  
 Questo gestore di configurazione esegue il mapping alla rappresentazione seguente in App.config o Web.config per il servizio o il client.  
  
```  
<gzipMessageEncoding innerMessageEncoding="textMessageEncoding" />  
  
```  
  
 Per utilizzare questo gestore di configurazione, è necessario che sia registrato nell'elemento [\<system.serviceModel\>](../../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md), come illustrato nella configurazione di esempio seguente.  
  
```  
<extensions>  
    <bindingElementExtensions>  
       <add   
           name="gzipMessageEncoding"   
           type=  
           "Microsoft.ServiceModel.Samples.GZipMessageEncodingElement,  
           GZipEncoder, Version=1.0.0.0, Culture=neutral,   
           PublicKeyToken=null" />  
      </bindingElementExtensions>  
</extensions>  
  
```  
  
 Quando si esegue il server, le richieste e le risposte dell'operazione vengono visualizzate nella finestra della console.Premere INVIO nella finestra per arrestare il server.  
  
```  
  
Press Enter key to Exit.  
  
        Server Echo(string input) called:  
        Client message: Simple hello  
  
        Server BigEcho(string[] input) called:  
        64 client messages  
  
```  
  
 Quando si esegue il client, le richieste e le risposte dell'operazione vengono visualizzate nella finestra della console.Premere INVIO nella finestra del client per arrestare il client.  
  
```  
  
Calling Echo(string):  
Server responds: Simple hello Simple hello  
  
Calling BigEcho(string[]):  
Server responds: Hello 0  
  
Press <ENTER> to terminate client.  
  
```  
  
#### Per impostare, compilare ed eseguire l'esempio  
  
1.  Installare [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] 4.0 utilizzando il comando seguente:  
  
    ```  
    %windir%\Microsoft.NET\Framework\v4.0.XXXXX\aspnet_regiis.exe /i /enable  
  
    ```  
  
2.  Verificare di avere eseguito [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
3.  Per compilare la soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
4.  Per eseguire l'esempio in una configurazione con un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Extensibility\MessageEncoder\Compression`  
  
## Vedere anche