---
title: "Implementazione del modello asincrono basato su eventi | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "modello asincrono basato su eventi"
  - "ProgressChangedEventArgs (classe)"
  - "BackgroundWorker (componente)"
  - "eventi [.NET Framework], asincroni"
  - "Modello asincrono"
  - "AsyncOperationManager (classe)"
  - "threading [.NET Framework], funzionalità asincrone"
  - "componenti [.NET Framework] asincroni"
  - "AsyncOperation (classe)"
  - "AsyncCompletedEventArgs (classe)"
ms.assetid: 43402d19-8d30-426d-8785-1a4478233bfa
caps.latest.revision: 20
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 20
---
# Implementazione del modello asincrono basato su eventi
Se si sta scrivendo una classe con alcune operazioni che possono causare ritardi notevoli, è consigliabile assegnandogli funzionalità asincrona implementando [Panoramica del modello asincrono basato su eventi](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md).  
  
 Il modello asincrono basato su eventi offre un modo standardizzato per una classe con funzionalità asincrone del pacchetto. Se implementata con le classi di supporto come <xref:System.ComponentModel.AsyncOperationManager>, la classe funziona con qualsiasi modello di applicazione, tra cui [!INCLUDE[vstecasp](../../../includes/vstecasp-md.md)], applicazioni Console e applicazioni Windows Form.  
  
 Per un esempio che implementa il modello asincrono basato su eventi, vedere [procedura: implementare un componente che supporta il modello asincrono basato su eventi](../../../docs/standard/asynchronous-programming-patterns/component-that-supports-the-event-based-asynchronous-pattern.md).  
  
 Per operazioni asincrone semplici può risultare utile il <xref:System.ComponentModel.BackgroundWorker> componente appropriato. Per ulteriori informazioni su <xref:System.ComponentModel.BackgroundWorker>, vedere [procedura: eseguire un'operazione in Background](../../../docs/framework/winforms/controls/how-to-run-an-operation-in-the-background.md).  
  
 Nell'elenco seguente vengono descritte le funzionalità del modello asincrono basato su eventi descritti in questo argomento.  
  
-   Opportunità per implementare il modello asincrono basato su eventi  
  
-   Denominazione di metodi asincroni  
  
-   Facoltativamente, supportano l'annullamento  
  
-   Se lo si desidera supportare la proprietà IsBusy  
  
-   Supporto facoltativo per report di stato  
  
-   Supporto facoltativo per la restituzione di risultati incrementali  
  
-   Gestione Out e Ref i parametri dei metodi  
  
## <a name="opportunities-for-implementing-the-event-based-asynchronous-pattern"></a>Opportunità per implementare il modello asincrono basato su eventi  
 Si consiglia di implementare il modello asincrono basato su eventi quando:  
  
-   I client della classe non è necessitino <xref:System.Threading.WaitHandle> e <xref:System.IAsyncResult> gli oggetti disponibili per le operazioni asincrone, vale a dire il polling e <xref:System.Threading.WaitHandle.WaitAll%2A> o <xref:System.Threading.WaitHandle.WaitAny%2A> dovrà essere creata dal client.  
  
-   Si desidera essere gestito dal client con il modello di evento/delegato noto delle operazioni asincrone.  
  
 Qualsiasi operazione è un candidato per un'implementazione asincrona, ma quelli che si prevede di lunghe latenze deve essere considerati. Operazioni in cui i client chiama un metodo e vengono visualizzata una notifica al completamento, senza alcun ulteriore intervento sono particolarmente adatte. Inoltre appropriate sono operazioni con esecuzione continua, periodicamente la notifica client di stato di avanzamento, sui risultati incrementali o modifiche di stato.  
  
 Per ulteriori informazioni sui casi in cui supportare il modello asincrono basato su eventi, vedere [prima di decidere quando implementare il modello asincrono basato su eventi](../../../docs/standard/asynchronous-programming-patterns/deciding-when-to-implement-the-event-based-asynchronous-pattern.md).  
  
## <a name="naming-asynchronous-methods"></a>Denominazione di metodi asincroni  
 Per ogni metodo sincrono *MethodName* per il quale si desidera specificare una controparte asincrona:  
  
 Definire un *MethodName* `Async` metodo che:  
  
-   Restituisce `void`.  
  
-   Accetta gli stessi parametri di *MethodName* metodo.  
  
-   Accetta più chiamate.  
  
 Facoltativamente è possibile definire un *MethodName* `Async` overload, identico a *MethodName*`Async`, ma con un parametro con valori di oggetto chiamato `userState`. Se è in grado di gestire più richiami concorrenti del metodo, nel qual caso il `userState` valore verrà recapitato nuovamente a tutti i gestori eventi per distinguere le chiamate del metodo. È inoltre possibile scegliere di eseguire questa operazione semplicemente la posizione in cui archiviare lo stato utente per un successivo recupero.  
  
 Per ogni *MethodName* `Async` firma del metodo:  
  
1.  Definire i seguenti eventi nella stessa classe del metodo:  
  
    ```vb  
    Public Event MethodNameCompleted As MethodNameCompletedEventHandler  
    ```  
  
    ```csharp  
    public event MethodNameCompletedEventHandler MethodNameCompleted;  
    ```  
  
2.  Definire il seguente delegato e <xref:System.ComponentModel.AsyncCompletedEventArgs>. Questi verranno probabilmente definiti all'esterno della classe stessa, ma nello spazio dei nomi stesso.  
  
    ```vb  
    Public Delegate Sub MethodNameCompletedEventHandler( _  
        ByVal sender As Object, _  
        ByVal e As MethodNameCompletedEventArgs)  
  
    Public Class MethodNameCompletedEventArgs  
        Inherits System.ComponentModel.AsyncCompletedEventArgs  
    Public ReadOnly Property Result() As MyReturnType  
    End Property  
    ```  
  
    ```csharp  
    public delegate void MethodNameCompletedEventHandler(object sender,   
        MethodNameCompletedEventArgs e);  
  
    public class MethodNameCompletedEventArgs : System.ComponentModel.AsyncCompletedEventArgs  
    {  
        public MyReturnType Result { get; }  
    }  
    ```  
  
    -   Assicurarsi che il *MethodName* `CompletedEventArgs` classe espone i relativi membri come proprietà di sola lettura e non da campi, come impediscono l'associazione dati.  
  
    -   Non viene definita una <xref:System.ComponentModel.AsyncCompletedEventArgs>-per i metodi che non producono risultati delle classi derivate. È sufficiente utilizzare un'istanza di <xref:System.ComponentModel.AsyncCompletedEventArgs> stesso.  
  
        > [!NOTE]
        >  È perfettamente accettabile, quando possibile e appropriato, riutilizzare il delegato e <xref:System.ComponentModel.AsyncCompletedEventArgs> tipi. In questo caso, la denominazione non sarà coerenza con il nome del metodo, poiché un determinato delegato e <xref:System.ComponentModel.AsyncCompletedEventArgs> non saranno collegati a un singolo metodo.  
  
## <a name="optionally-support-cancellation"></a>Facoltativamente, supportano l'annullamento  
 Se la classe supporta l'annullamento delle operazioni asincrone, annullamento dovrebbe essere esposto al client come descritto di seguito. Si noti che esistono due punti di decisione che devono essere raggiunta prima di definire il supporto dell'annullamento:  
  
-   La classe, inclusi eventuali future aggiunte previste, ha solo un'operazione asincrona che supporta l'annullamento?  
  
-   Per le operazioni asincrone che supportano l'annullamento più operazioni in sospeso? Che consente di *MethodName* `Async` metodo take un `userState` parametro, e consente più richiami prima dell'attesa di uno di essi?  
  
 Utilizzare le risposte a queste due domande nella tabella seguente per determinare quale deve essere la firma del metodo di annullamento.  
  
### <a name="visual-basic"></a>Visual Basic  
  
||Più operazioni simultanee supportate|Una sola operazione alla volta|  
|------|------------------------------------------------|----------------------------------|  
|Una sola operazione asincrona nell'intera classe|`Sub MethodNameAsyncCancel(ByVal userState As Object)`|`Sub MethodNameAsyncCancel()`|  
|Più operazioni asincrone in classe|`Sub CancelAsync(ByVal userState As Object)`|`Sub CancelAsync()`|  
  
### <a name="c"></a>C#  
  
||Più operazioni simultanee supportate|Una sola operazione alla volta|  
|------|------------------------------------------------|----------------------------------|  
|Una sola operazione asincrona nell'intera classe|`void MethodNameAsyncCancel(object userState);`|`void MethodNameAsyncCancel();`|  
|Più operazioni asincrone in classe|`void CancelAsync(object userState);`|`void CancelAsync();`|  
  
 Se si definisce il `CancelAsync(object userState)` (metodo), i client devono essere attenzione nella scelta dei relativi valori di stato in grado di distinguere tra tutti i metodi asincroni richiamati sull'oggetto e non solo tra tutte le chiamate di un singolo metodo asincrono.  
  
 La decisione di denominare la versione della singola operazione asincrona *MethodName* `AsyncCancel` si basa sulla possibilità di individuare più facilmente il metodo in un ambiente di progettazione come IntelliSense di Visual Studio. Questo gruppi di membri correlati e distinti dagli altri membri che non hanno niente a che fare con funzionalità asincrone. Se si prevede che potrebbero esserci altre operazioni asincrone aggiunte nelle versioni successive, è preferibile definire `CancelAsync`.  
  
 Non definire più metodi della tabella precedente nella stessa classe. Non sarà più senso o confusione per l'interfaccia della classe con un numero eccessivo di metodi.  
  
 Questi metodi restituiscono in genere verranno immediatamente e l'operazione può o non può annullare effettivamente. Nel gestore eventi per il *MethodName* `Completed` evento, il *MethodName* `CompletedEventArgs` oggetto contiene un `Cancelled` campo, i client possono utilizzare per determinare se si è verificato l'annullamento.  
  
 Rispettare la semantica di annullamento descritto in [procedure consigliate per implementare il modello asincrono basato su eventi](../../../docs/standard/asynchronous-programming-patterns/best-practices-for-implementing-the-event-based-asynchronous-pattern.md).  
  
## <a name="optionally-support-the-isbusy-property"></a>Se lo si desidera supportare la proprietà IsBusy  
 Se la classe non supporta più richiami concorrenti, è consigliabile esporre un `IsBusy` proprietà. Ciò consente agli sviluppatori determinare se un *MethodName* `Async` metodo è in esecuzione senza intercettare un'eccezione di *MethodName* `Async` (metodo).  
  
 Rispettare il `IsBusy` semantica descritto in [procedure consigliate per implementare il modello asincrono basato su eventi](../../../docs/standard/asynchronous-programming-patterns/best-practices-for-implementing-the-event-based-asynchronous-pattern.md).  
  
## <a name="optionally-provide-support-for-progress-reporting"></a>Supporto facoltativo per report di stato  
 È spesso utile per un'operazione asincrona di segnalare lo stato durante l'operazione. Il modello asincrono basato su eventi offre linee guida per questa operazione.  
  
-   Se lo si desidera definire un evento generato dall'operazione asincrona e richiamato sul thread appropriato. Il <xref:System.ComponentModel.ProgressChangedEventArgs> oggetto supporta un indicatore di stato con valori integer che deve essere compreso tra 0 e 100.  
  
-   Denominare l'evento come indicato di seguito:  
  
    -   `ProgressChanged`Se la classe dispone di più operazioni asincrone (o è prevista una crescita per includere più operazioni asincrone nelle versioni successive);  
  
    -   *MethodName* `ProgressChanged` se la classe dispone di una singola operazione asincrona.  
  
     Questa scelta di denominazione è paragonabile a quella eseguita per il metodo di annullamento, come descritto nella sezione Supporto facoltativo dell'annullamento.  
  
 Questo evento deve utilizzare il <xref:System.ComponentModel.ProgressChangedEventHandler> firma del delegato e <xref:System.ComponentModel.ProgressChangedEventArgs> (classe). In alternativa, se è possibile fornire un indicatore di stato più specifico di dominio (per istanza, byte letti e byte totali per un'operazione di download), è necessario definire una classe derivata di <xref:System.ComponentModel.ProgressChangedEventArgs>.  
  
 Si noti che è presente un solo `ProgressChanged` o *MethodName* `ProgressChanged` evento per la classe, indipendentemente dal numero di metodi asincroni supportati. I client è previsto l'utilizzo di `userState` oggetto passato al *MethodName* `Async` metodi per distinguere tra gli aggiornamenti sull'avanzamento in più operazioni simultanee.  
  
 Potrebbero verificarsi situazioni in cui lo stato di avanzamento di supportare più operazioni e ognuno restituisce un indicatore diversi per lo stato di avanzamento. In questo caso, un unico `ProgressChanged` evento non è appropriato, e si può scegliere di supportare più `ProgressChanged` eventi. In questo caso utilizzare il modello di denominazione *MethodName* `ProgressChanged` per ogni *MethodName* `Async` metodo.  
  
 Rispettare la semantica di report di stato descritta [procedure consigliate per implementare il modello asincrono basato su eventi](../../../docs/standard/asynchronous-programming-patterns/best-practices-for-implementing-the-event-based-asynchronous-pattern.md).  
  
## <a name="optionally-provide-support-for-returning-incremental-results"></a>Supporto facoltativo per la restituzione di risultati incrementali  
 A volte un'operazione asincrona può restituire risultati incrementali prima del completamento. Sono disponibili numerose opzioni che possono essere utilizzate per supportare questo scenario. Alcuni esempi.  
  
### <a name="single-operation-class"></a>Classe con singola operazione  
 Se la classe supporta solo una singola operazione asincrona e tale operazione è in grado di restituire risultati incrementali, quindi:  
  
-   Estendere la <xref:System.ComponentModel.ProgressChangedEventArgs> digitare per il trasporto di dati dei risultati incrementali e definire un *MethodName* `ProgressChanged` evento con dati estesi.  
  
-   Generare il *MethodName* `ProgressChanged` evento si verifica un risultato incrementale al report.  
  
 Questa soluzione si applica in particolare a una classe singola operazione asincrona in quanto non determina alcun problema con lo stesso evento si ripete per restituire risultati incrementali su "tutte le operazioni", come il *MethodName* `ProgressChanged` evento.  
  
### <a name="multiple-operation-class-with-homogeneous-incremental-results"></a>Classe di più operazioni con risultati incrementali omogenei  
 In questo caso, la classe supporta più metodi asincroni, in grado di restituire risultati incrementali e questi risultati incrementali tutti hanno lo stesso tipo di dati.  
  
 Seguire il modello descritto in precedenza per le classi di singola operazione, come lo stesso <xref:System.EventArgs> struttura funzionerà per tutti i risultati incrementali. Definire un `ProgressChanged` evento anziché un *MethodName* `ProgressChanged` evento, poiché viene applicato a più metodi asincroni.  
  
### <a name="multiple-operation-class-with-heterogeneous-incremental-results"></a>Classe di più operazioni con risultati incrementali eterogenei  
 Se la classe supporta più metodi asincroni, ognuno dei quali restituisce un tipo diverso di dati, è necessario:  
  
-   Separare i report dal report di stato del risultato incrementale.  
  
-   Definire un oggetto separato *MethodName* `ProgressChanged` evento con appropriati <xref:System.EventArgs> per ogni metodo gestire i dati dei risultati incrementali del metodo asincrono.  
  
 Richiamare il gestore eventi sul thread appropriato, come descritto in [procedure consigliate per implementare il modello asincrono basato su eventi](../../../docs/standard/asynchronous-programming-patterns/best-practices-for-implementing-the-event-based-asynchronous-pattern.md).  
  
## <a name="handling-out-and-ref-parameters-in-methods"></a>Gestione Out e Ref i parametri dei metodi  
 Sebbene l'utilizzo di `out` e `ref` è, in generale, è sconsigliato in .NET Framework, ecco le regole da seguire quando sono presenti:  
  
 Dato un metodo sincrono *MethodName*:  
  
-   `out`i parametri *MethodName* non devono far parte di *MethodName*`Async`. Al contrario, dovrebbero far parte di *MethodName* `CompletedEventArgs` con lo stesso nome come relativo parametro equivalente in *MethodName* (a meno che non vi è un nome più appropriato).  
  
-   `ref`i parametri *MethodName* dovrebbe essere visualizzato come parte di *MethodName*`Async`e come parte di *MethodName* `CompletedEventArgs` con lo stesso nome come relativo parametro equivalente in *MethodName* (a meno che non vi è un nome più appropriato).  
  
 Ad esempio, data:  
  
```vb  
Public Function MethodName(ByVal arg1 As String, ByRef arg2 As String, ByRef arg3 As String) As Integer  
```  
  
```csharp  
public int MethodName(string arg1, ref string arg2, out string arg3);  
```  
  
 Il metodo asincrono e il relativo <xref:System.ComponentModel.AsyncCompletedEventArgs> classe avrà un aspetto simile al seguente:  
  
```vb  
Public Sub MethodNameAsync(ByVal arg1 As String, ByVal arg2 As String)  
  
Public Class MethodNameCompletedEventArgs  
    Inherits System.ComponentModel.AsyncCompletedEventArgs  
    Public ReadOnly Property Result() As Integer   
    End Property  
    Public ReadOnly Property Arg2() As String   
    End Property  
    Public ReadOnly Property Arg3() As String   
    End Property  
End Class  
```  
  
```csharp  
public void MethodNameAsync(string arg1, string arg2);  
  
public class MethodNameCompletedEventArgs : System.ComponentModel.AsyncCompletedEventArgs  
{  
    public int Result { get; };  
    public string Arg2 { get; };  
    public string Arg3 { get; };  
}  
```  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.ComponentModel.ProgressChangedEventArgs>   
 <xref:System.ComponentModel.AsyncCompletedEventArgs>   
 [Procedura: implementare un componente che supporta il modello asincrono basato su eventi](../../../docs/standard/asynchronous-programming-patterns/component-that-supports-the-event-based-asynchronous-pattern.md)   
 [Procedura: eseguire un'operazione in Background](../../../docs/framework/winforms/controls/how-to-run-an-operation-in-the-background.md)   
 [Procedura: implementare un Form che utilizza un'operazione in Background](../../../docs/framework/winforms/controls/how-to-implement-a-form-that-uses-a-background-operation.md)   
 [Quando implementare il modello asincrono basato su eventi](../../../docs/standard/asynchronous-programming-patterns/deciding-when-to-implement-the-event-based-asynchronous-pattern.md)   
 [Programmazione multithreading con il modello asincrono basato su eventi](../../../docs/standard/asynchronous-programming-patterns/multithreaded-programming-with-the-event-based-asynchronous-pattern.md)   
 [Procedure consigliate per implementare il modello asincrono basato su eventi](../../../docs/standard/asynchronous-programming-patterns/best-practices-for-implementing-the-event-based-asynchronous-pattern.md)