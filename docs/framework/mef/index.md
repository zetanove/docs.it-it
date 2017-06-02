---
title: "Managed Extensibility Framework (MEF) | Microsoft Docs"
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
  - "Managed Extensibility Framework, panoramica"
  - "MEF, panoramica"
ms.assetid: 6c61b4ec-c6df-4651-80f1-4854f8b14dde
caps.latest.revision: 31
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 31
---
# Managed Extensibility Framework (MEF)
In questo argomento viene fornita una panoramica di Managed Extensibility Framework, introdotto in .NET Framework 4.  
  
<a name="what_is_mef"></a>   
## <a name="what-is-mef"></a>Che cos'è MEF?  
 Managed Extensibility Framework o MEF è una libreria per la creazione di applicazioni leggere ed estendibili. Consente agli sviluppatori di applicazioni di scoprire e usare le estensioni senza alcuna configurazione. Consente anche agli sviluppatori di estensioni di incapsulare facilmente il codice ed evitare dipendenze rigide fragili. Con MEF è possibile riutilizzare le estensioni non solo all'interno ma anche tra le applicazioni.  
  
<a name="the_problem_of_extensibility"></a>   
## <a name="the-problem-of-extensibility"></a>Il problema dell'estendibilità  
 Si immagini di essere l'architetto di un'applicazione di grandi dimensioni che deve fornire supporto per l'estendibilità. L'applicazione deve includere un numero potenzialmente grande di componenti più piccoli. Inoltre, la creazione e l'esecuzione di tali componenti deve essere gestita dall'applicazione.  
  
 L'approccio più semplice a questo problema è includere i componenti come codice sorgente nell'applicazione e chiamarli direttamente dal codice.  Tuttavia, questo approccio comporta alcuni inconvenienti ovvi.  In particolare, non è possibile aggiungere nuovi componenti senza modificare il codice sorgente. Benché ammissibile, ad esempio, in un'applicazione Web, questo limite risulta inaccettabile in un'applicazione client.  Un altro ostacolo ugualmente problematico è che in alcuni casi non si ha accesso al codice sorgente dei componenti, in quanto sviluppati da terze parti. Inoltre, per lo stesso motivo, non è possibile consentire a terze parti di accedere al codice di propria creazione.  
  
 Un approccio leggermente più sofisticato consiste nel fornire un punto o un'interfaccia di estensione, per consentire la separazione tra l'applicazione e i relativi componenti.  Se si applica questo modello è possibile fornire un'interfaccia implementabile da un componente e un'API per consentire a quest'ultima di interagire con l'applicazione.  Benché elimini l'esigenza di accedere al codice sorgente, questo approccio presenta comunque alcune difficoltà.  
  
 Poiché l'applicazione è priva di qualsiasi capacità autonoma di individuare i componenti, è comunque necessario indicarle in modo esplicito quali sono i componenti disponibili da caricare.  Questa operazione in genere viene eseguita registrando in modo esplicito i componenti disponibili in un file di configurazione. Ne consegue che garantire la correttezza dei componenti diventa un problema di manutenzione, in particolar modo se la responsabilità dell'esecuzione dell'aggiornamento viene assegnata all'utente finale e non allo sviluppatore.  
  
 Inoltre, i componenti sono incapaci di comunicare fra loro, salvo tramite i canali definiti rigidamente appartenenti all'applicazione stessa.  Se per una determinata esigenza di comunicazione l'architetto dell'applicazione non ha previsto un canale specifico, di solito tale comunicazione risulta impossibile.  
  
 Infine, gli sviluppatori dei componenti devono accettare una dipendenza rigida in merito all'assembly che contiene l'interfaccia che implementano.  Ciò ostacola l'utilizzo di un componente in più applicazioni e può inoltre far emergere dei problemi quando si crea un framework di test per i componenti.  
  
<a name="what_mef_provides"></a>   
## <a name="what-mef-provides"></a>Funzionalità offerte da MEF  
 Anziché ricorrere alla registrazione esplicita dei componenti disponibili, MEF offre un modo per individuarli in modo implicito, tramite *composizione*.  Un componente MEF, detto un *parte*, in modo dichiarativo specifica sia le proprie dipendenze (dette *Importa*) e le funzionalità (noto come *Esporta*) rende disponibile. Quando si crea una parte, il motore di composizione di MEF ne soddisfa le importazioni con le risorse disponibili nelle altre parti.  
  
 Questo approccio risolve i problemi discussi nella sezione precedente.  Poiché le parti MEF specificano in modo dichiarativo le proprie funzionalità, sono individuabili al runtime. Ne consegue che un'applicazione può usare le parti senza dover ricorrere a riferimenti hardcoded oppure a file di configurazione fragili.  MEF consente alle applicazioni di individuare ed esaminare le parti mediante i relativi metadati, senza creare un'istanza o caricare gli assembly di tali parti. Di conseguenza, non c'è alcun bisogno di specificare attentamente come e quando caricare le estensioni.  
  
 Oltre alle proprie esportazioni fornite, una parte può specificare le proprie importazioni che verranno compilate dalle altre parti.  Questo approccio rende non solo possibile ma persino facile la comunicazione fra le parti. Inoltre, consente un buon factoring del codice. Ad esempio, i servizi comuni a molti componenti possono essere organizzati in una parte distinta e quindi essere modificati o sostituiti facilmente.  
  
 Poiché non è richiesta alcuna dipendenza rigida da un determinato assembly dell'applicazione, il modello MEF consente il riutilizzo delle estensioni da un'applicazione a un'altra.  Ciò semplifica inoltre lo sviluppo di un test harness, indipendente dell'applicazione, per testare i componenti dell'estensione.  
  
 Un'applicazione estensibile scritta tramite MEF dichiara un'importazione che può essere compilata da componenti di estensione. Inoltre, può dichiarare esportazioni per esporre alle estensioni i servizi dell'applicazione.  Ogni componente di estensione dichiara un'esportazione e può anche dichiarare importazioni.  In questo modo, i componenti di estensione stessi risultano automaticamente estensibili.  
  
<a name="where_is_mef_available"></a>   
## <a name="where-is-mef-available"></a>Disponibilità di MEF  
 MEF è parte integrante di [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] ed è disponibile in tutti i contesti in cui si usa .NET Framework.  È possibile usare MEF nelle applicazioni client se usano Windows Form, WPF o qualsiasi altra tecnologia oppure nelle applicazioni server che usano ASP.NET.  
  
<a name="mef_and_maf"></a>   
## <a name="mef-and-maf"></a>MEF e MAF  
 Nelle versioni precedenti di .NET Framework è stato introdotto Managed Add-in Framework (MAF), progettato per consentire alle applicazioni di isolare e gestire le estensioni.  Rispetto a MEF, MAF si concentra su un livello leggermente più elevato, in particolare sull'isolamento delle estensioni e sul caricamento e scaricamento degli assembly. MEF si concentra invece su individuazione, estensibilità e portabilità.  I due framework interoperano agevolmente e una stessa applicazione può trarre vantaggio da entrambi.  
  
<a name="simplecalculator_an_example_application"></a>   
## <a name="simplecalculator-an-example-application"></a>SimpleCalculator: esempio di applicazione  
 Il modo più semplice per vedere le potenzialità di MEF è compilare una semplice applicazione MEF. In questo esempio viene compilata una calcolatrice molto semplice denominata SimpleCalculator. L'obiettivo di SimpleCalculator è creare un'applicazione console che accetta comandi aritmetici di base, nel formato "5+3" o "6-2", e restituisce le risposte corrette. Tramite MEF sarà possibile aggiungere nuovi operatori senza modificare il codice dell'applicazione.  
  
 Per scaricare il codice completo per questo esempio, vedere il [esempio di SimpleCalculator](http://code.msdn.microsoft.com/windowsdesktop/Simple-Calculator-MEF-1152654e).  
  
> [!NOTE]
>  Più che fornire uno scenario di uso realistico, lo scopo di SimpleCalculator è dimostrare i concetti e la sintassi di MEF. Molte delle applicazioni in grado di sfruttare al meglio la potenza di MEF sono più complesse di SimpleCalculator. Per esempi più dettagliati, vedere il [Managed Extensibility Framework](http://go.microsoft.com/fwlink/?LinkId=144282) su Codeplex.  
  
 Per iniziare, in [!INCLUDE[vs_dev10_long](../../../includes/vs-dev10-long-md.md)], creare un nuovo progetto applicazione Console denominato `SimpleCalculator`. Aggiungere un riferimento all'assembly System.ComponentModel.Composition in cui risiede MEF. Aprire Module1.vb o Program.cs e aggiungere istruzioni `Imports` o `using` per System.ComponentModel.Composition e System.ComponentModel.Composition.Hosting. Questi due spazi dei nomi contengono i tipi MEF che saranno necessari per sviluppare un'applicazione estensibile. In Visual Basic aggiungere la parola chiave `Public` alla riga in cui viene dichiarato il modulo `Module1`.  
  
<a name="composition_container_and_catalogs"></a>   
## <a name="composition-container-and-catalogs"></a>Contenitore di composizione e cataloghi  
 La base del modello di composizione MEF è il *contenitore di composizione*, che contiene tutte le parti disponibili ed esegue la composizione.  ovvero l'abbinamento tra importazioni ed esportazioni.  Il tipo più comune di contenitore di composizione è <xref:System.ComponentModel.Composition.Hosting.CompositionContainer>, e verrà utilizzato anche per SimpleCalculator.  
  
 In Visual Basic, aggiungere una classe pubblica denominata `Program` in Module1.vb. Aggiungere quindi la riga seguente alla classe `Program` in Module1.vb o Program.cs:  
  
```vb  
Dim _container As CompositionContainer  
```  
  
```csharp  
private CompositionContainer _container;  
```  
  
 Per individuare le parti disponibili, i contenitori di composizione si avvalgono di un *catalogo*. Un catalogo è un oggetto che rende disponibili le parti individuate in un'origine.  MEF fornisce cataloghi per individuare le parti disponibili in un assembly, una directory o un tipo fornito. Gli sviluppatori di applicazioni possono creare facilmente nuovi cataloghi per individuare parti disponibili in altre origini, ad esempio un servizio Web.  
  
 Aggiungere il costruttore seguente alla classe `Program`:  
  
```vb  
Public Sub New()  
    'An aggregate catalog that combines multiple catalogs  
     Dim catalog = New AggregateCatalog()  
  
    'Adds all the parts found in the same assembly as the Program class  
    catalog.Catalogs.Add(New AssemblyCatalog(GetType(Program).Assembly))  
  
    'Create the CompositionContainer with the parts in the catalog  
    _container = New CompositionContainer(catalog)  
  
    'Fill the imports of this object  
    Try  
        _container.ComposeParts(Me)  
    Catch ex As Exception  
        Console.WriteLine(ex.ToString)  
    End Try  
End Sub  
```  
  
```csharp  
private Program()  
{  
    //An aggregate catalog that combines multiple catalogs  
    var catalog = new AggregateCatalog();  
    //Adds all the parts found in the same assembly as the Program class  
    catalog.Catalogs.Add(new AssemblyCatalog(typeof(Program).Assembly));  
  
    //Create the CompositionContainer with the parts in the catalog  
    _container = new CompositionContainer(catalog);  
  
    //Fill the imports of this object  
    try  
    {  
        this._container.ComposeParts(this);  
    }  
    catch (CompositionException compositionException)  
    {  
        Console.WriteLine(compositionException.ToString());  
   }  
}  
```  
  
 La chiamata a <xref:System.ComponentModel.Composition.AttributedModelServices.ComposeParts%2A> indica al contenitore di composizione di comporre un set specifico di parti, in questo caso l'istanza corrente di `Program`. Tuttavia, a questo punto non si verificherà nulla, poiché `Program` non presenta importazioni da compilare.  
  
<a name="imports_and_exports_with_attributes"></a>   
## <a name="imports-and-exports-with-attributes"></a>Importazioni ed esportazioni con attributi  
 Prima di tutto, `Program` deve importare una calcolatrice. Ciò consente di separare le problematiche dell'interfaccia utente, ad esempio l'input e l'output della console che andrà in `Program`, dalla logica della calcolatrice.  
  
 Aggiungere il codice seguente alla classe `Program` :  
  
```vb  
<Import(GetType(ICalculator))>  
Public Property calculator As ICalculator  
```  
  
```csharp  
[Import(typeof(ICalculator))]  
public ICalculator calculator;  
```  
  
 Si noti che la dichiarazione di `calculator` oggetto non è insolito, ma è decorata con il <xref:System.ComponentModel.Composition.ImportAttribute> attributo.  Questo attributo dichiara un elemento di importazione, ovvero un elemento che verrà fornito dal motore di composizione quando l'oggetto viene composto.  
  
 Ogni importazione presenta un *contratto*, che determina le esportazioni a cui verrà abbinata. Il contratto può essere una stringa specificata in modo esplicito oppure può essere generato automaticamente da MEF a partire da un tipo specificato, in questo caso l'interfaccia `ICalculator`.  Qualsiasi esportazione dichiarata con un contratto corrispondente verrà usata per soddisfare questa importazione.  Benché il tipo dell'oggetto `calculator` sia effettivamente `ICalculator`, non si tratta di una condizione obbligatoria. Il contratto è indipendente dal tipo dell'oggetto di importazione.  In questo caso, è possibile escludere l'oggetto `typeof(ICalculator)`.  Se non specificato in modo esplicito, MEF presuppone automaticamente che il contratto si basi sul tipo di importazione.  
  
 Aggiungere questa interfaccia molto semplice al modulo o allo spazio dei nomi `SimpleCalculator`:  
  
```vb  
Public Interface ICalculator  
    Function Calculate(ByVal input As String) As String  
End Interface  
```  
  
```csharp  
public interface ICalculator  
{  
    String Calculate(String input);  
}  
```  
  
 Ora che è stato definito `ICalculator`, è necessaria una classe che lo implementi.  Aggiungere la classe seguente al modulo o allo spazio dei nomi `SimpleCalculator`:  
  
```vb  
<Export(GetType(ICalculator))>  
Public Class MySimpleCalculator  
   Implements ICalculator  
  
End Class  
```  
  
```csharp  
[Export(typeof(ICalculator))]  
class MySimpleCalculator : ICalculator  
{  
  
}  
```  
  
 Questa è l'esportazione che verrà abbinata all'importazione in `Program`. Affinché l'esportazione corrisponda all'importazione, è necessario che dispongano dello stesso contratto.  L'esportazione nel contesto di un contratto basato su `typeof(MySimpleCalculator)` darebbe luogo a una mancata corrispondenza e l'importazione non verrebbe compilata. Il contratto deve corrispondere in modo esatto.  
  
 Poiché il contenitore di composizione sarà popolato con tutte le parti disponibili in questo assembly, la parte `MySimpleCalculator` sarà disponibile.  Quando il costruttore di `Program` esegue la composizione nell'oggetto `Program`, la relativa importazione verrà compilata con un oggetto `MySimpleCalculator` che verrà creato a tale scopo.  
  
 Al livello dell'interfaccia utente (`Program`) non occorrono altre informazioni.  È quindi possibile compilare il resto della logica dell'interfaccia utente nel metodo `Main`.  
  
 Aggiungere al metodo `Main` il codice seguente:  
  
```vb  
Sub Main()  
    Dim p As New Program()  
    Dim s As String  
    Console.WriteLine("Enter Command:")  
    While (True)  
        s = Console.ReadLine()  
        Console.WriteLine(p.calculator.Calculate(s))  
    End While  
End Sub  
```  
  
```csharp  
static void Main(string[] args)  
{  
    Program p = new Program(); //Composition is performed in the constructor  
    String s;  
    Console.WriteLine("Enter Command:");  
    while (true)  
    {  
        s = Console.ReadLine();  
        Console.WriteLine(p.calculator.Calculate(s));  
    }  
}  
```  
  
 Questo codice legge semplicemente una riga di input e chiama la funzione `Calculate` di `ICalculator` nel risultato, che quindi scrive nella console. Questo è tutto il codice necessario in `Program`.  Tutte le altre operazioni avranno luogo nelle parti.  
  
<a name="further_imports_and_importmany"></a>   
## <a name="further-imports-and-importmany"></a>Altre importazioni e ImportMany  
 Per essere estensibile, SimpleCalculator deve importare un elenco di operazioni. Un normale <xref:System.ComponentModel.Composition.ImportAttribute> attributo viene riempito da una sola <xref:System.ComponentModel.Composition.ExportAttribute>.  Se ne è disponibile più di uno, il motore di composizione genera un errore.  Per creare un'importazione che può essere compilata da qualsiasi numero di esportazioni, è possibile utilizzare il <xref:System.ComponentModel.Composition.ImportManyAttribute> attributo.  
  
 Aggiungere la proprietà operations seguente per la `MySimpleCalculator` classe:  
  
```vb  
<ImportMany()>  
Public Property operations As IEnumerable(Of Lazy(Of IOperation, IOperationData))  
```  
  
```csharp  
[ImportMany]  
IEnumerable<Lazy<IOperation, IOperationData>> operations;  
```  
  
 <xref:System.Lazy%602> è un tipo fornito da MEF per contenere riferimenti indiretti alle esportazioni.</T, TMetadata>  In questo caso, oltre all'oggetto esportato stesso, si ottengono anche *esportare metadati*, ovvero informazioni che descrivono l'oggetto esportato. Ogni <xref:System.Lazy%602> contiene un `IOperation` oggetto che rappresenta un'operazione effettiva e un `IOperationData` oggetto che rappresenta i metadati.\</T, TMetadata>  
  
 Aggiungere le interfacce semplici seguenti al modulo o allo spazio dei nomi `SimpleCalculator`:  
  
```vb  
Public Interface IOperation  
    Function Operate(ByVal left As Integer, ByVal right As Integer) As Integer  
End Interface  
  
Public Interface IOperationData  
    ReadOnly Property Symbol As Char  
End Interface  
```  
  
```csharp  
public interface IOperation  
{  
     int Operate(int left, int right);  
}  
  
public interface IOperationData  
{  
    Char Symbol { get; }  
}  
```  
  
 In questo caso, i metadati di ogni operazione sono il simbolo che rappresenta l'operazione, ad esempio +, -, * e così via. Per rendere disponibile l'operazione di addizione, aggiungere la classe seguente al modulo o allo spazio dei nomi `SimpleCalculator`:  
  
```vb  
<Export(GetType(IOperation))>  
<ExportMetadata("Symbol", "+"c)>  
Public Class Add  
    Implements IOperation  
  
    Public Function Operate(ByVal left As Integer, ByVal right As Integer) As Integer Implements IOperation.Operate  
        Return left + right  
    End Function  
End Class  
```  
  
```csharp  
[Export(typeof(IOperation))]  
[ExportMetadata("Symbol", '+')]  
class Add: IOperation  
{  
    public int Operate(int left, int right)  
    {  
        return left + right;  
    }  
}  
```  
  
 Il <xref:System.ComponentModel.Composition.ExportAttribute> funzionamento dell'attributo come in precedenza.  Il <xref:System.ComponentModel.Composition.ExportMetadataAttribute> attributo Allega metadati, sotto forma di una coppia nome-valore, a tale esportazione.  Mentre la classe `Add` implementa `IOperation`, una classe che implementa `IOperationData` non viene definita in modo esplicito. Tale classe viene invece creata implicitamente da MEF con proprietà basate sui nomi dei metadati forniti.  Questo è uno dei vari modi per accedere ai metadati in MEF.  
  
 Composizione in MEF è *ricorsiva*. L'oggetto `Program` è stato composto in modo esplicito e ha importato un oggetto `ICalculator` che è risultato essere di tipo `MySimpleCalculator`.  `MySimpleCalculator`, a sua volta, importa un insieme di oggetti `IOperation` e tale importazione viene compilata quando viene creato `MySimpleCalculator`, contemporaneamente alle importazioni di `Program`. Se la classe `Add` avesse dichiarato un'altra importazione, sarebbe stato necessario compilare anch'essa e così via. Qualsiasi importazione non compilata comporta un errore di composizione.  Tuttavia, è possibile dichiarare le importazioni come facoltative oppure assegnare loro valori predefiniti.  
  
<a name="calculator_logic"></a>   
## <a name="calculator-logic"></a>Logica della calcolatrice  
 Dopo aver creato queste parti, l'unica operazione che resta da eseguire è creare la logica della calcolatrice stessa. Aggiungere il codice seguente nella classe `MySimpleCalculator` per implementare il metodo `Calculate`:  
  
```vb  
Public Function Calculate(ByVal input As String) As String Implements ICalculator.Calculate  
    Dim left, right As Integer  
    Dim operation As Char  
    Dim fn = FindFirstNonDigit(input) 'Finds the operator  
    If fn < 0 Then  
        Return "Could not parse command."  
    End If  
    operation = input(fn)  
    Try  
        left = Integer.Parse(input.Substring(0, fn))  
        right = Integer.Parse(input.Substring(fn + 1))  
    Catch ex As Exception  
        Return "Could not parse command."  
    End Try  
    For Each i As Lazy(Of IOperation, IOperationData) In operations  
        If i.Metadata.symbol = operation Then  
            Return i.Value.Operate(left, right).ToString()  
        End If  
    Next  
    Return "Operation not found!"  
End Function  
```  
  
```csharp  
public String Calculate(String input)  
{  
    int left;  
    int right;  
    Char operation;  
    int fn = FindFirstNonDigit(input); //finds the operator  
    if (fn < 0) return "Could not parse command.";  
  
    try  
    {  
        //separate out the operands  
        left = int.Parse(input.Substring(0, fn));  
        right = int.Parse(input.Substring(fn + 1));  
    }  
    catch   
    {  
        return "Could not parse command.";  
    }  
  
    operation = input[fn];  
  
    foreach (Lazy<IOperation, IOperationData> i in operations)  
    {  
        if (i.Metadata.Symbol.Equals(operation)) return i.Value.Operate(left, right).ToString();  
    }  
    return "Operation Not Found!";  
}  
```  
  
 I passaggi iniziali analizzano la stringa di input in operandi sinistro e destro e carattere dell'operatore.  Nel ciclo `foreach`, viene esaminato ogni membro della raccolta `operations`. Questi oggetti sono di tipo <xref:System.Lazy%602>, e i relativi valori di metadati e l'oggetto esportato è accessibile con la <xref:System.Lazy%602.Metadata%2A> proprietà e <xref:System.Lazy%601.Value%2A>proprietà rispettivamente.</T, TMetadata> In questo caso, se si verifica la corrispondenza della proprietà `Symbol` dell'oggetto `IOperationData`, la calcolatrice chiama il metodo `Operate` dell'oggetto `IOperation` e restituisce il risultato.  
  
 Per completare la calcolatrice è inoltre necessario il metodo helper che restituisce la posizione del primo carattere non numerico in una stringa.  Aggiungere il seguente metodo helper alla classe `MySimpleCalculator`:  
  
```vb  
Private Function FindFirstNonDigit(ByVal s As String) As Integer  
    For i = 0 To s.Length  
        If (Not (Char.IsDigit(s(i)))) Then Return i  
    Next  
    Return -1  
End Function  
```  
  
```csharp  
private int FindFirstNonDigit(String s)  
{  
    for (int i = 0; i < s.Length; i++)  
    {  
        if (!(Char.IsDigit(s[i]))) return i;  
    }  
    return -1;  
}  
```  
  
 A questo punto è possibile compilare ed eseguire il progetto. In Visual Basic, accertarsi di aver aggiunto la parola chiave `Public` a `Module1`. Digitare un'operazione di addizione nella finestra della console, ad esempio "5+3". La calcolatrice restituirà i risultati.  Se si usano altri operatori, viene visualizzato un messaggio che indica che l'operazione non è stata trovata .  
  
<a name="extending_simplecalculator_using_a_new_class"></a>   
## <a name="extending-simplecalculator-using-a-new-class"></a>Estensione di SimpleCalculator mediante una nuova classe  
 Ora che la calcolatrice funziona risulta facile aggiungere una nuova operazione. Aggiungere la classe seguente al modulo o allo spazio dei nomi `SimpleCalculator`:  
  
```vb  
<Export(GetType(IOperation))>  
<ExportMetadata("Symbol", "-"c)>  
Public Class Subtract  
    Implements IOperation  
  
    Public Function Operate(ByVal left As Integer, ByVal right As Integer) As Integer Implements IOperation.Operate  
        Return left - right  
    End Function  
End Class  
```  
  
```csharp  
[Export(typeof(IOperation))]  
[ExportMetadata("Symbol", '-')]  
class Subtract : IOperation  
{  
    public int Operate(int left, int right)  
    {  
        return left - right;  
    }  
}  
```  
  
 Compilare ed eseguire il progetto. Digitare un'operazione di sottrazione, ad esempio "5-3". Oltre all'addizione, la calcolatrice supporta ora anche la sottrazione.  
  
<a name="extending_simplecalculator_using_a_new_assembly"></a>   
## <a name="extending-simplecalculator-using-a-new-assembly"></a>Estensione di SimpleCalculator mediante un nuovo assembly  
 Benché aggiungere classi al codice sorgente sia abbastanza semplice, MEF offre la possibilità di cercare le parti all'esterno del codice sorgente di un'applicazione. Per dimostrare questo concetto, è necessario modificare SimpleCalculator per cercare una directory, nonché il proprio assembly, per le parti, aggiungendo un <xref:System.ComponentModel.Composition.Hosting.DirectoryCatalog>.  
  
 Aggiungere una nuova directory denominata `Extensions` al progetto SimpleCalculator.  Assicurarsi di aggiungerla a livello di progetto e non a livello di soluzione. Aggiungere quindi un nuovo progetto libreria di classi alla soluzione, denominata `ExtendedOperations`. Il nuovo progetto verrà compilato in un assembly separato.  
  
 Aprire la finestra di progettazione proprietà progetto per il progetto ExtendedOperations e fare clic su di **compilare** o **compilare** scheda. Modifica il **il percorso di output di compilazione** o **percorso di Output** in modo che punti alla directory Extensions nella directory del progetto SimpleCalculator (... \SimpleCalculator\Extensions\\).  
  
 In Module1.vb o Program.cs aggiungere la riga seguente al costruttore `Program`:  
  
```vb  
catalog.Catalogs.Add(New DirectoryCatalog("C:\SimpleCalculator\SimpleCalculator\Extensions"))  
```  
  
```csharp  
catalog.Catalogs.Add(new DirectoryCatalog("C:\\SimpleCalculator\\SimpleCalculator\\Extensions"));  
```  
  
 Sostituire il percorso di esempio con il percorso della directory Extensions.  Il percorso assoluto è solo a scopo di debug.  In un'applicazione di produzione si usa un percorso relativo. Il <xref:System.ComponentModel.Composition.Hosting.DirectoryCatalog> verrà ora aggiunto qualsiasi parte trovata negli assembly contenuti nella directory di estensioni per il contenitore di composizione.  
  
 Nel progetto ExtendedOperations aggiungere i riferimenti a SimpleCalculator e System.ComponentModel.Composition. Nel file di classe ExtendedOperations aggiungere un'istruzione `Imports` o `using` per System.ComponentModel.Composition. In Visual Basic aggiungere anche un'istruzione `Imports` per SimpleCalculator. Quindi, aggiungere la seguente classe al file di classe ExtendedOperations:  
  
```vb  
<Export(GetType(SimpleCalculator.IOperation))>  
<ExportMetadata("Symbol", "%"c)>  
Public Class Modulo  
    Implements IOperation  
  
    Public Function Operate(ByVal left As Integer, ByVal right As Integer) As Integer Implements IOperation.Operate  
        Return left Mod right  
    End Function  
End Class  
```  
  
```csharp  
[Export(typeof(SimpleCalculator.IOperation))]  
[ExportMetadata("Symbol", '%')]  
public class Mod : SimpleCalculator.IOperation  
{  
    public int Operate(int left, int right)  
    {  
        return left % right;  
    }  
}  
```  
  
 Si noti che, affinché il contratto per la corrispondenza, il <xref:System.ComponentModel.Composition.ExportAttribute> attributo deve avere lo stesso tipo di <xref:System.ComponentModel.Composition.ImportAttribute>.  
  
 Compilare ed eseguire il progetto. Testare il nuovo operatore Mod (%).  
  
<a name="conclusion"></a>   
## <a name="conclusion"></a>Conclusione  
 In questo argomento sono stati trattati i concetti di base di MEF.  
  
-   Parti, cataloghi e contenitore di composizione  
  
     Le parti e il contenitore di composizione sono i blocchi predefiniti di base di un'applicazione MEF. Una parte è qualsiasi oggetto che importa o esporta un valore, fino al proprio valore (incluso). Un catalogo fornisce un insieme di parti ottenute da una determinata origine.  Il contenitore di composizione usa le parti fornite da un catalogo per eseguire la composizione, ovvero il binding tra le importazioni e le esportazioni.  
  
-   Importazioni ed esportazioni  
  
     Le importazioni e le esportazioni rappresentano il canale di comunicazione fra i componenti. Con un'importazione il componente specifica la necessità di un determinato valore o oggetto, mentre con un'esportazione specifica la disponibilità di un valore. Ogni importazione viene associata a un elenco di esportazioni mediante il relativo contratto.  
  
<a name="where_do_i_go_now"></a>   
## <a name="where-do-i-go-now"></a>Argomenti correlati  
 Per scaricare il codice completo per questo esempio, vedere il [esempio di SimpleCalculator](http://code.msdn.microsoft.com/windowsdesktop/Simple-Calculator-MEF-1152654e).  
  
 Per ulteriori informazioni ed esempi di codice, vedere [Managed Extensibility Framework](http://go.microsoft.com/fwlink/?LinkId=144282). Per un elenco di tipi MEF, vedere il <xref:System.ComponentModel.Composition?displayProperty=fullName> dello spazio dei nomi.