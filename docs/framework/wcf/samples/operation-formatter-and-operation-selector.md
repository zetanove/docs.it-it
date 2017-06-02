---
title: "Formattatore e selettore dell&#39;operazione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1c27e9fe-11f8-4377-8140-828207b98a0e
caps.latest.revision: 19
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 19
---
# Formattatore e selettore dell&#39;operazione
In questo esempio viene illustrato come utilizzare i punti di estensibilità di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] per consentire l'uso di dati del messaggio in un formato diverso da quello previsto da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].Per impostazione predefinita, i formattatori [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] prevedono che i parametri del metodo siano inclusi nell'elemento `soap:body`.In realtà, nell'esempio viene illustrato come implementare un formattatore dell'operazione personalizzato che analizza i dati dei parametri da una stringa di query HTTP GET e richiama i metodi utilizzando tali dati.  
  
 L'esempio si basa su [Guida introduttiva](../../../../docs/framework/wcf/samples/getting-started-sample.md), che implementa il contratto di servizio  `ICalculator`.Viene mostrato come i messaggi Add, Subtract, Multiply e Divide possono essere modificati per utilizzare HTTP GET per le richieste client\-server e HTTP POST con i messaggi POX per le risposte server\-client.  
  
 Per questo scopo, nell'esempio vengono forniti gli elementi seguenti:  
  
-   `QueryStringFormatter`, che implementa <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter> e <xref:System.ServiceModel.Dispatcher.IDispatchMessageFormatter> per il client e server, rispettivamente, ed elabora i dati nella stringa di query.  
  
-   `UriOperationSelector`, che implementa <xref:System.ServiceModel.Dispatcher.IDispatchOperationSelector> nel server per eseguire l'operazione di distribuzione in base al nome dell'operazione nella richiesta GET.  
  
-   Comportamento dell'endpoint `EnableHttpGetRequestsBehavior` \(e configurazione corrispondente\), che aggiunge il selettore dell'operazione necessario al runtime.  
  
-   Viene illustrato come inserire un nuovo formattatore dell'operazione nel runtime.  
  
-   In questo esempio sia il client che il servizio sono applicazioni console \(con estensione exe\).  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine dell'argomento.  
  
## Concetti chiave  
 `QueryStringFormatter`. Il formattatore dell'operazione è il componente di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] responsabile per la conversione di un messaggio in una matrice di oggetti parametro e di una matrice di oggetti parametro in un messaggio.Questa operazione viene eseguita nel client utilizzando l'interfaccia <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter> e nel server con l'interfaccia <xref:System.ServiceModel.Dispatcher.IDispatchMessageFormatter>.Queste interfacce consentono agli utenti di ottenere i messaggi di richiesta e risposta dai metodi `Serialize` e `Deserialize`.  
  
 In questo esempio, `QueryStringFormatter` implementa entrambe le interfacce e viene implementato nel client e nel server.  
  
 Richiesta:  
  
-   Nell'esempio viene utilizzata la classe <xref:System.ComponentModel.TypeConverter> per convertire i dati dei parametri nel messaggio di richiesta da e verso le stringhe.Se non è disponibile una classe <xref:System.ComponentModel.TypeConverter> per un tipo specifico, il formattatore di esempio genera un'eccezione.  
  
-   Nel metodo `IClientMessageFormatter.SerializeRequest` sul client, il formattatore crea un URI con l'indirizzo A appropriato e aggiunge il nome dell'operazione come suffisso.Tale nome viene utilizzato per distribuire l'operazione appropriata sul server.Il formattatore prende quindi la matrice di oggetti parametro e serializza i dati dei parametri nella stringa di query dell'URI utilizzando i nomi di parametro e i valori convertiti dalla classe <xref:System.ComponentModel.TypeConverter>.Le proprietà <xref:System.ServiceModel.Channels.MessageHeaders.To%2A> e <xref:System.ServiceModel.Channels.MessageProperties.Via%2A> vengono quindi impostate su questo URI.È possibile accedere all'oggetto <xref:System.ServiceModel.Channels.MessageProperties> attraverso la proprietà <xref:System.ServiceModel.Channels.Message.Properties%2A>.  
  
-   Nel metodo `IDispatchMessageFormatter.DeserializeRequest` sul server, il formattatore recupera l'URI `Via` nelle proprietà del messaggio di richiesta in ingresso.Analizza le coppie nome\-valore nella stringa di query dell'URI nei nomi e valori di parametro e utilizza i nomi e valori di parametro per popolare la matrice di parametri passata nel metodo.Si noti che l'operazione di distribuzione è già stata eseguita, pertanto il suffisso del nome dell'operazione viene ignorato in questo metodo.  
  
 Risposta:  
  
-   In questo esempio, HTTP GET viene utilizzato solo per la richiesta.Il formattatore delega l'invio della risposta al formattatore originale che sarebbe stato utilizzato per generare un messaggio XML.Uno degli obiettivi di questo esempio è mostrare come implementare tale formattatore delegato.  
  
### Classe UriPathSuffixOperationSelector  
 L'interfaccia <xref:System.ServiceModel.Dispatcher.IDispatchOperationSelector> consente agli utenti di implementare una logica personalizzata che richiede l'invio di un messaggio particolare.  
  
 In questo esempio, `UriPathSuffixOperationSelector` deve essere implementato nel server per selezionare l'operazione appropriata poiché il nome dell'operazione è incluso nell'URI HTTP GET anziché in un'intestazione dell'azione nel messaggio.L'esempio è configurato per consentire solo i nomi dell'operazione senza distinzione tra maiuscole e minuscole.  
  
 Il metodo `SelectOperation` accetta il messaggio in arrivo e cerca l'URI `Via` nelle proprietà del messaggio.Estrae il suffisso del nome dell'operazione dall'URI, cerca una tabella interna per ottenere il nome dell'operazione al quale il messaggio deve essere inviato e restituisce tale nome dell'operazione.  
  
### Classe EnableHttpGetRequestsBehavior  
 Il componente `UriPathSuffixOperationSelector` può essere impostato a livello di codice o tramite un comportamento dell'endpoint.Nell'esempio viene implementato il comportamento `EnableHttpGetRequestsBehavior`, specificato nel file di configurazione dell'applicazione del servizio.  
  
 Nel server:  
  
 La proprietà <xref:System.ServiceModel.Dispatcher.DispatchRuntime.OperationSelector%2A> è impostata sull'implementazione di <xref:System.ServiceModel.Dispatcher.IDispatchOperationSelector>.  
  
 Per impostazione predefinita, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza un filtro dell'indirizzo Corrispondenza esatta.L'URI del messaggio in ingresso contiene un suffisso del nome dell'operazione seguito da una stringa di query che contiene i dati dei parametri, pertanto il comportamento dell'endpoint modifica anche il filtro dell'indirizzo in modo da renderlo un filtro Prefisso corrispondente.Utilizza [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]<xref:System.ServiceModel.Dispatcher.PrefixEndpointAddressMessageFilter> per questo scopo.  
  
### Installazione di formattatori dell'operazione  
 I comportamenti dell'operazione che specificano i formattatori sono univoci.Un comportamento di questo tipo viene sempre implementato per impostazione predefinita per ogni operazione allo scopo di creare il formattatore dell'operazione necessario.Tuttavia, questi comportamenti hanno lo stesso aspetto degli altri comportamenti dell'operazione e non possono essere identificati da qualsiasi altro attributo.Per installare un comportamento sostitutivo, l'implementazione deve cercare specifici comportamenti del formattatore installati dal caricatore dei tipi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] per impostazione predefinita e sostituirli o aggiungere un comportamento compatibile da eseguire dopo il comportamento predefinito.  
  
 Questi comportamenti dei formattatori dell'operazione possono essere impostati a livello di codice prima di chiamare <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A?displayProperty=fullName> o specificando un comportamento dell'operazione da eseguire dopo quello predefinito.Tuttavia, non può essere configurato facilmente da un comportamento dell'endpoint \(e pertanto mediante la configurazione\) perché il modello di comportamento non consente la sostituzione di un comportamento con un altro o la modifica della struttura di descrizione.  
  
 Nel client:  
  
 L'implementazione <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter> deve essere implementata in modo che possa convertire le richieste in richieste HTTP GET e delegare le risposte al formattatore originale.Questo processo viene eseguito chiamando il metodo helper `EnableHttpGetRequestsBehavior.ReplaceFormatterBehavior`.  
  
 È necessario effettuare questo passaggio prima di chiamare `CreateChannel`.  
  
```  
void ReplaceFormatterBehavior(OperationDescription operationDescription, EndpointAddress address)  
{  
    // Remove the DataContract behavior if it is present.  
    IOperationBehavior formatterBehavior = operationDescription.Behaviors.Remove<DataContractSerializerOperationBehavior>();  
    if (formatterBehavior == null)  
    {  
        // Remove the XmlSerializer behavior if it is present.  
        formatterBehavior = operationDescription.Behaviors.Remove<XmlSerializerOperationBehavior>();  
        ...  
    }  
  
    // Remember what the innerFormatterBehavior was.  
    DelegatingFormatterBehavior delegatingFormatterBehavior = new DelegatingFormatterBehavior(address);  
    delegatingFormatterBehavior.InnerFormatterBehavior = formatterBehavior;  
   operationDescription.Behaviors.Add(delegatingFormatterBehavior);  
}  
```  
  
 Nel server:  
  
-   L'interfaccia <xref:System.ServiceModel.Dispatcher.IDispatchMessageFormatter> deve essere implementata in modo che possa leggere le richieste in richieste HTTP GET e delegare la scrittura delle risposte al formattatore originale.Questo processo viene eseguito chiamando lo stesso metodo helper `EnableHttpGetRequestsBehavior.ReplaceFormatterBehavior` del client \(vedere l'esempio di codice precedente\).  
  
-   È necessario effettuare questo passaggio prima di chiamare <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A>.In questo esempio viene illustrato come il formattatore viene modificato manualmente prima di chiamare <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A>.Un altro modo per ottenere lo stesso risultato consiste nel derivare una classe da <xref:System.ServiceModel.ServiceHost> che effettua le chiamate a `EnableHttpGetRequestsBehavior.ReplaceFormatterBehavior` prima dell'apertura \(vedere documentazione di hosting e gli esempi\).  
  
### Attività dell'utente  
 Nel server:  
  
-   Non è necessario modificare l'implementazione `ICalculator` del server.  
  
-   Il file App.config per il servizio deve utilizzare un'associazione POX personalizzata che imposta l'attributo `messageVersion` dell'elemento `textMessageEncoding` su `None`.  
  
    ```  
    <bindings>  
      <customBinding>  
        <binding name="poxBinding">  
          <textMessageEncoding messageVersion="None" />  
          <httpTransport />  
        </binding>  
      </customBinding>  
    </bindings>  
    ```  
  
-   Tale file deve inoltre specificare anche il comportamento `EnableHttpGetRequestsBehavior` personalizzato aggiungendolo alla sezione delle estensioni di comportamento e utilizzandolo.  
  
    ```  
    <behaviors>  
      <endpointBehaviors>  
        <behavior name="enableHttpGetRequestsBehavior">  
          <enableHttpGetRequests />  
        </behavior>  
      </endpointBehaviors>  
    </behaviors>  
  
    <extensions>  
      <behaviorExtensions>  
        <!-- Enabling HTTP GET requests: Behavior Extension -->  
        <add   
          name="enableHttpGetRequests"           type="Microsoft.ServiceModel.Samples.EnableHttpGetRequestsBehaviorElement, QueryStringFormatter, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />  
      </behaviorExtensions>  
    </extensions>  
    ```  
  
-   Aggiungere i formattatori dell'operazione prima di chiamare <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A>.  
  
 Nel client:  
  
-   Non è necessario modificare l'implementazione client.  
  
-   Il file App.config per il client deve utilizzare un'associazione POX personalizzata che imposta l'attributo `messageVersion` dell'elemento `textMessageEncoding` su `None`.Una differenza rispetto al servizio è che il client deve abilitare l'indirizzamento manuale in modo da poter modificare gli indirizzi A in uscita.  
  
    ```  
    <bindings>  
      <customBinding>  
        <binding name="poxBinding">  
          <textMessageEncoding messageVersion="None" />  
          <httpTransport manualAddressing="True" />  
        </binding>  
      </customBinding>  
    </bindings>  
    ```  
  
-   Il file App.config per il client deve specificare lo stesso comportamento `EnableHttpGetRequestsBehavior` personalizzato del server.  
  
-   Aggiungere i formattatori dell'operazione prima di chiamare <xref:System.ServiceModel.ChannelFactory%601.CreateChannel>.  
  
 Quando si esegue l'esempio, le richieste e le risposte dell'operazione vengono visualizzate nella finestra della console client.Tutte le operazioni \(Add, Subtract, Multiply e Divide\) devono essere completate.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Extensibility\Formatters\QuieryStringFormatter`  
  
##### Per impostare, compilare ed eseguire l'esempio  
  
1.  Verificare di avere eseguito [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare la soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Per eseguire l'esempio in una configurazione con un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
## Vedere anche