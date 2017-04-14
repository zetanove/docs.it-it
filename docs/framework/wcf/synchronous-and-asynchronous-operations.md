---
title: "Operazioni sincrone e asincrone | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "contratti di servizio [WCF], operazioni asincrone"
  - "contratti di servizio [WCF], operazioni sincrone"
ms.assetid: db8a51cb-67e6-411b-9035-e5821ed350c9
caps.latest.revision: 24
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 24
---
# Operazioni sincrone e asincrone
In questo argomento vengono illustrate l'implementazione e la chiamata delle operazioni del servizio asincrone.  
  
 Molte applicazioni chiamano metodi in modo asincrono, poiché ciò consente all'applicazione di continuare a eseguire operazioni utili mentre viene effettuata la chiamata al metodo.  I servizi e i client di [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] possono partecipare alle chiamate di operazioni asincrone a due livelli distinti dell'applicazione, assicurando alle applicazioni [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] più flessibilità per ottimizzare la velocità effettiva bilanciata a fronte dell'interattività.  
  
## Tipi di operazioni asincrone  
 In tutti i contratti di servizio in [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], indipendentemente dai tipi di parametri e dai valori restituiti, vengono usati attributi [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] per specificare un particolare modello di scambio dei messaggi tra client e servizio.  [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] indirizza automaticamente i messaggi in ingresso e in uscita all'operazione del servizio appropriata o al codice client in esecuzione.  
  
 Il client possiede solo il contratto di servizio, che specifica il modello di scambio dei messaggi per una particolare operazione.  I client possono offrire allo sviluppatore qualsiasi modello di programmazione desiderato, purché venga rispettato il modello di scambio dei messaggi sottostante.  Anche i servizi possono quindi implementare le operazioni in qualsiasi modo, purché venga rispettato il modello dei messaggi specificato.  
  
 L'indipendenza del contratto di servizio dall'implementazione del client o del servizio consente le forme seguenti di esecuzione asincrona nelle applicazioni [!INCLUDE[indigo2](../../../includes/indigo2-md.md)]:  
  
-   I client possono richiamare operazioni di richiesta\/risposta in modo asincrono usando uno scambio di messaggi sincrono.  
  
-   I servizi possono implementare operazioni di richiesta\/risposta in modo asincrono usando uno scambio di messaggi sincrono.  
  
-   Gli scambi di messaggi possono essere unidirezionali, indipendentemente dall'implementazione del client o del servizio.  
  
### Scenari asincroni suggeriti  
 Usare un approccio asincrono nell'implementazione di un'operazione di servizio se tale implementazione effettua una chiamata di blocco, ad esempio effettuando le operazioni di I\/O.  Quando si effettua l'implementazione di un'operazione asincrona, provare a chiamare i metodi e le operazioni asincrone per estendere il più possibile il percorso della chiamata asincrona.  Ad esempio chiamare l'opzione`BeginOperationTwo()` dall'interno di `BeginOperationOne()`.  
  
-   Usare un approccio asincrono in un'applicazione client o in un'applicazione chiamante nei seguenti casi:  
  
-   Se si richiamano operazioni da un'applicazione di livello intermedio.  \([!INCLUDE[crabout](../../../includes/crabout-md.md)] tali scenari, vedere [Applicazioni client di livello intermedio](../../../docs/framework/wcf/feature-details/middle-tier-client-applications.md).\)  
  
-   Se si richiamano operazioni all'interno di una pagina ASP.NET, usare pagine asincrone.  
  
-   Se si richiamano operazioni da applicazioni a thread singolo, ad esempio Windows Forms o [!INCLUDE[avalon1](../../../includes/avalon1-md.md)].  Se si usa il modello di chiamata asincrono basato su eventi, l'evento risultante viene generato sul thread UI, aggiungendo velocità di risposta all'applicazione senza che vi sia necessità di gestire più thread.  
  
-   Generalmente, se è possibile scegliere tra una chiamata sincrona e una asincrona, scegliere la seconda.  
  
### Implementazione di un'operazione del servizio asincrona  
 Le operazioni asincrone possono essere implementate tramite uno dei tre metodi seguenti:  
  
1.  Modello asincrono basato su attività  
  
2.  Modello asincrono basato su eventi  
  
3.  Modello asincrono IAsyncResult  
  
#### Modello asincrono basato su attività  
 Il modello asincrono basato su attività è la modalità preferita per implementare le operazioni asincrone dal momento che è il più semplice.  Per usare questo metodo, implementare semplicemente l'operazione del servizio e specificare un tipo restituito Task\<T\>, dove T è il tipo restituito dall'operazione logica.  Ad esempio:  
  
```csharp  
public class SampleService:ISampleService   
{   
   // ...  
   public async Task<string> SampleMethodTaskAsync(string msg)   
   {   
      return Task<string>.Factory.StartNew(() =>   
      {   
         return msg;   
      });   
   }  
   // ...  
}  
  
```  
  
 L'operazione SampleMethodTaskAsync restituisce Task\<string\> in quanto l'operazione logica restituisce una stringa.  Per altre informazioni sul modello asincrono basato su attività, vedere la pagina relativa al [modello asincrono basato su attività](http://go.microsoft.com/fwlink/?LinkId=232504).  
  
> [!WARNING]
>  Quando si usa il modello asincrono basato su attività, è possibile che venga generato un oggetto T: System.AggregateException se si verifica un'eccezione nell'attesa del completamento dell'operazione.  Questa eccezione può verificarsi nel client o nei servizi.  
  
#### Modello asincrono basato su eventi  
 Un servizio che supporta il modello asincrono basato su eventi disporrà di una o più operazioni denominate MethodNameAsync.  Tali metodi possono eseguire il mirroring delle versioni sincrone che eseguono la stessa operazione sul thread corrente.  La classe può anche disporre di un evento MethodNameCompleted e di un metodo MethodNameAsyncCancel \(o semplicemente CancelAsync\).  Un client che desidera chiamare l'operazione definirà un gestore eventi da chiamare al completamento dell'operazione.  
  
 Nel frammento di codice riportato di seguito viene illustrato come dichiarare le operazioni asincrone mediante il modello asincrono basato su eventi.  
  
```csharp  
public class AsyncExample  
{  
    // Synchronous methods.  
    public int Method1(string param);  
    public void Method2(double param);  
  
    // Asynchronous methods.  
    public void Method1Async(string param);  
    public void Method1Async(string param, object userState);  
    public event Method1CompletedEventHandler Method1Completed;  
  
    public void Method2Async(double param);  
    public void Method2Async(double param, object userState);  
    public event Method2CompletedEventHandler Method2Completed;  
  
    public void CancelAsync(object userState);  
  
    public bool IsBusy { get; }  
  
    // Class implementation not shown.  
}  
  
```  
  
 Per altre informazioni sul modello asincrono basato su eventi, vedere [Cenni preliminari sul modello asincrono basato su eventi](http://go.microsoft.com/fwlink/?LinkId=232515).  
  
#### Modello asincrono IAsyncResult  
 Un'operazione del servizio può essere implementata in modo asincrono usando il modello di programmazione asincrona di [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] e contrassegnando il metodo `<Begin>` con la proprietà <xref:System.ServiceModel.OperationContractAttribute.AsyncPattern%2A> impostata su `true`.  In questo caso, l'operazione asincrona viene esposta nei metadati nella stessa forma di un'operazione sincrona, ovvero come singola operazione con un messaggio di richiesta e un messaggio di risposta correlato.  I modelli di programmazione client possono quindi effettuare una scelta.  Possono rappresentare questo modello come operazione sincrona o asincrona, a condizione che, quando viene richiamato il servizio, si verifichi uno scambio di messaggi di richiesta\-risposta.  
  
 In generale, data la natura asincrona dei sistemi, non è necessario considerare una dipendenza sui thread.  Il modo più affidabile di passare dati alle varie fasi di elaborazione di distribuzione dell'operazione è rappresentato dall'uso di estensioni.  
  
 Per un esempio, vedere [Procedura: implementare un'operazione del servizio asincrona](../../../docs/framework/wcf/how-to-implement-an-asynchronous-service-operation.md).  
  
 Per definire un'operazione di contratto `X` eseguita in modo asincrono indipendentemente dalla modalità con cui viene chiamata nell'applicazione client:  
  
-   Definire due metodi usando il modello `BeginOperation` e `EndOperation`.  
  
-   Il metodo `BeginOperation` include i parametri `in` e `ref` per l'operazione e restituisce un tipo <xref:System.IAsyncResult>.  
  
-   Il metodo `EndOperation` include un parametro <xref:System.IAsyncResult>, nonché i parametri `out` e `ref`, e restituisce il tipo restituito dall'operazione.  
  
 Vedere, ad esempio, il metodo seguente.  
  
```csharp  
int DoWork(string data, ref string inout, out string outonly)  
  
```  
  
```vb  
Function DoWork(ByVal data As String, ByRef inout As String, _out outonly As out) As Integer  
  
```  
  
 Per creare un'operazione asincrona, i due metodi sarebbero:  
  
```csharp  
[OperationContract(AsyncPattern=true)]IAsyncResult BeginDoWork(string data,                           ref string inout,                           AsyncCallback callback,                           object state);int EndDoWork(ref string inout, out string outonly, IAsyncResult result);  
  
```  
  
```vb  
<OperationContract(AsyncPattern := True)>  _Function BeginDoWork(ByVal data As String, _                 ByRef inout As String, _                 ByVal callback As AsyncCallback, _                 ByVal state As Object) _As IAsyncResult Function EndDoWork(ByRef inout As String, _        ByRef outonly As String, _        ByVal result As IAsyncResult) _As Integer  
  
```  
  
> [!NOTE]
>  L'attributo <xref:System.ServiceModel.OperationContractAttribute> viene applicato solo al metodo `BeginDoWork`.  Il contratto risultante include un'operazione WSDL denominata `DoWork`.  
  
### Chiamate asincrone lato client  
 Un'applicazione client [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] può usare uno qualsiasi dei tre modelli di chiamata asincrona descritti in precedenza.  
  
 Quando si usa il modello basato su attività, chiamare semplicemente l'operazione usando la parola chiave await come illustrato nel seguente frammento di codice.  
  
```  
await simpleServiceClient.SampleMethodTaskAsync(“hello, world”);  
  
```  
  
 L'uso del modello asincrono basato su eventi richiede solamente l'aggiunta di un gestore eventi per ricevere una notifica di risposta e l'evento risultante viene automaticamente generato sul thread dell'interfaccia utente.  Per usare questo approccio, specificare le opzioni di comando **\/async** e **\/tcv:Version35** con lo [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md), come nell'esempio seguente.  
  
```  
svcutil http://localhost:8000/servicemodelsamples/service/mex /async /tcv:Version35  
```  
  
 Al termine di questa operazione, Svcutil.exe genera una classe client [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] in cui l'infrastruttura dell'evento consente all'applicazione chiamante di implementare e fare in modo che un gestore eventi riceva la risposta ed esegua le operazioni necessarie.  Per un esempio completo, vedere [Procedura: chiamare operazioni del servizio in modo asincrono](../../../docs/framework/wcf/feature-details/how-to-call-wcf-service-operations-asynchronously.md).  
  
 Il modello asincrono basato su eventi è disponibile solamente in [!INCLUDE[netfx35_long](../../../includes/netfx35-long-md.md)].  Inoltre, non è supportato anche in [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)] se viene creato un canale client [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] usando la classe <xref:System.ServiceModel.ChannelFactory%601?displayProperty=fullName>.  Con gli oggetti del canale client [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] è necessario usare gli oggetti <xref:System.IAsyncResult?displayProperty=fullName> per richiamare le operazioni in modo asincrono.  Per usare questo approccio, specificare l'opzione di comando **\/async** con lo [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md), come nell'esempio seguente.  
  
```  
svcutil http://localhost:8000/servicemodelsamples/service/mex /async   
```  
  
 In questo modo viene generato un contratto di servizio nel quale ciascuna operazione viene modellata come un metodo `<Begin>` con la proprietà <xref:System.ServiceModel.OperationContractAttribute.AsyncPattern%2A> impostata su `true` e un metodo `<End>` corrispondente.  Per un esempio completo usando una classe <xref:System.ServiceModel.ChannelFactory%601>, vedere [Procedura: chiamare le operazioni in modo asincrono tramite una channel factory](../../../docs/framework/wcf/feature-details/how-to-call-operations-asynchronously-using-a-channel-factory.md).  
  
 In ogni caso, le applicazioni possono richiamare un'operazione in modo asincrono anche se il servizio viene implementato in modo sincrono, esattamente come un'applicazione può usare lo stesso modello per richiamare in modo asincrono un metodo sincrono locale.  La modalità di implementazione dell'operazione non è importante per il client. Quando il messaggio di risposta arriva, il relativo contenuto viene inviato al metodo asincrono del client \<`End`\> e il client recupera le informazioni.  
  
### Modelli di scambio di messaggi unidirezionali  
 È inoltre possibile creare un modello di scambio di messaggi asincrono, in cui le operazioni unidirezionali \(operazioni per cui se la proprietà <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A?displayProperty=fullName> è `true` non esiste una risposta correlata\) possono essere inviate in entrambe le direzioni dal client o dal servizio in modo indipendente dall'altro lato.  A tale scopo si usa il modello di scambio di messaggi duplex con messaggi unidirezionali. In questo caso, il contratto di servizio specifica uno scambio di messaggi unidirezionale che entrambi i lati possono implementare o meno come chiamate o implementazioni asincrone, in base alle necessità.  In genere, quando il contratto è uno scambio di messaggi unidirezionali, le implementazioni possono essere prevalentemente asincrone poiché, una volta inviato un messaggio, l'applicazione non attende una risposta e può continuare a svolgere altre attività.  
  
### Contratti client e di messaggio asincroni basati su eventi  
 Le linee guida di progettazione per il modello asincrono basato su eventi indicano che, se vengono restituiti più valori, un valore viene restituito come proprietà `Result` e i restanti valori sono restituiti come proprietà nell’oggetto <xref:System.EventArgs>.  Di conseguenza, è possibile che, se un client importa metadati usando le opzioni di comando asincrone basate su eventi e l'operazione restituisce più valori, l'oggetto predefinito <xref:System.EventArgs> restituisce un valore come proprietà `Result` e i restanti valori come proprietà dell’oggetto <xref:System.EventArgs>.  
  
 Se si desidera ricevere l’oggetto del messaggio come proprietà `Result` e i valori restituiti come proprietà in quell’oggetto, usare l’opzione di comando **\/messageContract**.  Questa operazione genera una firma che restituisce il messaggio di risposta come proprietà `Result` nell’oggetto <xref:System.EventArgs>.  Pertanto, tutti i valori restituiti interni sono proprietà dell’oggetto del messaggio di risposta.  
  
## Vedere anche  
 <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A>   
 <xref:System.ServiceModel.OperationContractAttribute.AsyncPattern%2A>