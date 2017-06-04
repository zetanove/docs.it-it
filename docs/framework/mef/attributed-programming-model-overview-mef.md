---
title: "Panoramica sul modello di programmazione con attributi (MEF) | Microsoft Docs"
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
  - "modello di programmazione con attributi [MEF]"
  - "MEF, modello di programmazione con attributi"
ms.assetid: 49b787ff-2741-4836-ad51-c3017dc592d4
caps.latest.revision: 24
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 24
---
# Panoramica sul modello di programmazione con attributi (MEF)
In Managed Extensibility Framework \(MEF\) un *modello di programmazione* è un metodo particolare per definire l'insieme di oggetti concettuali su cui opera MEF, incluse le parti, le importazioni e le esportazioni. MEF usa questi oggetti, ma non specifica il modo in cui devono essere rappresentati. È quindi possibile usare una vasta gamma di modelli di programmazione, inclusi i modelli di programmazione personalizzati.  
  
 Il modello di programmazione predefinito usato in MEF è il *modello di programmazione con attributi*. Nel modello di programmazione con attributi le parti, le importazioni, le esportazioni e gli altri oggetti sono definiti con attributi che decorano le classi normali di .NET Framework. Questo argomento illustra come usare gli attributi forniti dal modello di programmazione con attributi per creare un'applicazione MEF.  
  
<a name="import_and_export_basics"></a>   
## Nozioni fondamentali su importazione ed esportazione  
 Un'*esportazione* è un valore fornito da una parte ad altre parti di un contenitore e un'*importazione* è un requisito espresso da una parte al contenitore, da soddisfare con le esportazioni disponibili. Nel modello di programmazione con attributi le importazioni e le esportazioni sono dichiarate tramite la decorazione di classi o membri con gli attributi `Import` e `Export`. L'attributo `Export` può decorare una classe, un campo, una proprietà o un metodo, mentre l'attributo `Import` può decorare un campo, una proprietà o un parametro di costruttore.  
  
 Per associare un'importazione a un'esportazione, è necessario che l'importazione e l'esportazione abbiano lo stesso *contratto*. Il contratto è costituito da una stringa, definita *nome contratto*, e dal tipo dell'oggetto esportato o importato, definito *tipo di contratto*. Un'esportazione è in grado di soddisfare un'importazione specifica solo se il nome e il tipo di contratto corrispondono.  
  
 Uno o entrambi i parametri del contratto possono essere impliciti o espliciti. Il codice seguente mostra una classe che dichiara un'importazione di base.  
  
```vb  
Public Class MyClass1 <Import()> Public Property MyAddin As IMyAddin End Class  
```  
  
```csharp  
public class MyClass { [Import] public IMyAddin MyAddin { get; set; } }  
```  
  
 In questa importazione all'attributo `Import` non è associato alcun parametro nome contratto o tipo di contratto. Entrambi i parametri saranno quindi dedotti dalla proprietà decorata. In questo caso il tipo di contratto sarà `IMyAddin` e il nome del contratto sarà una stringa univoca creata dal tipo di contratto. In altri termini, il nome del contratto corrisponderà solo alle esportazioni i cui nomi sono stati dedotti dal tipo `IMyAddin`.  
  
 Di seguito è illustrata un'esportazione corrispondente all'importazione precedente.  
  
```vb  
<Export(GetType(IMyAddin))> Public Class MyLogger Implements IMyAddin End Class  
```  
  
```csharp  
[Export(typeof(IMyAddin))] public class MyLogger : IMyAddin { }  
```  
  
 In questa esportazione il tipo di contratto è `IMyAddin` poiché è specificato come parametro dell'attributo `Export`. Il tipo esportato deve essere uguale al tipo di contratto, deve derivare dal tipo di contratto o deve implementare il tipo di contratto come se fosse un'interfaccia. In questa esportazione il tipo effettivo `MyLogger` implementa l'interfaccia `IMyAddin`. Il nome del contratto è dedotto dal tipo di contratto. Questa esportazione corrisponderà quindi all'importazione precedente.  
  
> [!NOTE]
>  Le esportazioni e le importazioni devono essere in genere dichiarate nelle classi o nei membri pubblici. Sono supportate altre dichiarazioni, ma l'esportazione o l'importazione di un membro privato, protetto o interno influisce negativamente sul modello di isolamento per la parte e non è quindi consigliata.  
  
 Per fare in modo che l'esportazione e l'importazione siano considerate corrispondenti, il tipo di contratto deve corrispondere esattamente. Esaminare l'esportazione seguente.  
  
```vb  
<Export()> 'WILL NOT match the previous import! Public Class MyLogger Implements IMyAddin End Class  
```  
  
```csharp  
[Export] //WILL NOT match the previous import! public class MyLogger : IMyAddin { }  
```  
  
 In questa esportazione il tipo di contratto è `MyLogger` invece di `IMyAddin`. Anche se `MyLogger` implementa `IMyAddin` ed è quindi possibile eseguirne il casting in un oggetto `IMyAddin` , questa esportazione non corrisponderà all'importazione precedente perché i tipi di contratto non sono uguali.  
  
 In genere, non è necessario specificare il nome del contratto e la maggior parte dei contratti dovrebbe essere definita in termini di tipo di contratto e metadati. In alcune circostanze, tuttavia, è importante specificare direttamente il nome del contratto. Il caso più comune consiste nell'esportazione di alcuni valori che condividono un tipo comune, ad esempio le primitive, da parte di una classe. Il nome del contratto può essere specificato come primo parametro dell'attributo `Import` o `Export`. Il codice seguente mostra un'importazione e un'esportazione con un nome contratto specificato `MajorRevision`.  
  
```vb  
Public Class MyExportClass 'This one will match <Export("MajorRevision")> Public ReadOnly Property MajorRevision As Integer Get Return 4 End Get End Property <Export("MinorRevision")> Public ReadOnly Property MinorRevision As Integer Get Return 16 End Get End Property End Class  
```  
  
```csharp  
public class MyClass { [Import("MajorRevision")] public int MajorRevision { get; set; } } public class MyExportClass { [Export("MajorRevision")] //This one will match. public int MajorRevision = 4; [Export("MinorRevision")] public int MinorRevision = 16; }  
```  
  
 Se il tipo di contratto non è specificato, sarà comunque dedotto dal tipo di importazione o esportazione. Anche se il nome del contratto è specificato in modo esplicito, tuttavia, anche il tipo di contratto deve corrispondere esattamente per fare in modo che l'importazione e l'esportazione siano considerate corrispondenti. Ad esempio, se il campo `MajorRevision` fosse una stringa, i tipi di contratto dedotti non corrisponderebbero e l'esportazione non corrisponderebbe all'importazione, nonostante entrambe abbiano lo stesso nome di contratto.  
  
### Importazione ed esportazione di un metodo  
 L'attributo `Export` può anche decorare un metodo, in modo analogo a una classe, una proprietà o una funzione. Le esportazioni di metodi devono specificare un tipo o un nome di contratto, poiché il tipo non può essere dedotto. Il tipo specificato può essere un delegato personalizzato o un tipo generico, ad esempio `Func`. La classe seguente esporta un metodo denominato `DoSomething`.  
  
```vb  
Public Class MyAddin 'Explicitly specifying a generic type <Export(GetType(Func(Of Integer, String)))> Public Function DoSomething(ByVal TheParam As Integer) As String Return Nothing 'Function body goes here End Function End Class  
```  
  
```csharp  
public class MyAddin { //Explicitly specifying a generic type. [Export(typeof(Func<int, string>)] public string DoSomething(int TheParam); }  
```  
  
 In questa classe il metodo `DoSomething` accetta un singolo parametro `int` e restituisce un oggetto `string`. Per corrispondere a questa esportazione, la parte che esegue l'importazione deve dichiarare un membro appropriato. La classe seguente importa il metodo `DoSomething`.  
  
```vb  
Public Class MyClass1 'Contract name must match! <Import()> Public Property MajorRevision As Func(Of Integer, String) End Class  
```  
  
```csharp  
public class MyClass { [Import] //Contract name must match! public Func<int, string> DoSomething { get; set; } }  
```  
  
 Per altre informazioni su come usare l'oggetto `Func<T, T>`, vedere <xref:System.Func%602>.  
  
<a name="types_of_imports"></a>   
## Tipi di importazioni  
 MEF supporta diversi tipi di importazione, tra cui l'importazione dinamica, differita, essenziale o facoltativa.  
  
### Importazioni dinamiche  
 In alcuni casi è possibile che la classe che esegue l'importazione voglia corrispondere a esportazioni di qualsiasi tipo con un nome di contratto specifico. In questo scenario la classe può dichiarare una *importazione dinamica*. L'importazione seguente corrisponde a qualsiasi esportazione con nome contratto "TheString".  
  
```vb  
Public Class MyClass1 <Import("TheString")> Public Property MyAddin End Class  
```  
  
```csharp  
public class MyClass { [Import("TheString")] public dynamic MyAddin { get; set; } }  
```  
  
 Quando il tipo di contratto è dedotto dalla parola chiave `dynamic`, corrisponderà a qualsiasi tipo di contratto. In questo caso un'importazione deve **sempre** specificare un nome di contratto a cui corrispondere. Se non è stato specificato alcun nome di contratto, l'importazione sarà considerata come non corrispondente ad alcuna esportazione. Entrambe le esportazioni seguenti corrispondono all'importazione precedente.  
  
```vb  
<Export("TheString", GetType(IMyAddin))> Public Class MyLogger Implements IMyAddin End Class <Export("TheString")> Public Class MyToolbar End Class  
```  
  
```csharp  
[Export("TheString", typeof(IMyAddin))] public class MyLogger : IMyAddin { } [Export("TheString")] public class MyToolbar { }  
```  
  
 La classe che esegue l'importazione deve essere ovviamente preparata per la gestione di un oggetto di tipo arbitrario.  
  
### Importazioni differite  
 In alcuni casi è possibile che la classe che esegue l'importazione necessiti di un riferimento indiretto all'oggetto importato, in modo che non siano create immediatamente istanze dell'oggetto. In questo scenario la classe può dichiarare un'*importazione differita* usando un tipo di contratto `Lazy<T>`. La proprietà di importazione seguente dichiara un'importazione differita.  
  
```vb  
Public Class MyClass1 <Import()> Public Property MyAddin As Lazy(Of IMyAddin) End Class  
```  
  
```csharp  
public class MyClass { [Import] public Lazy<IMyAddin> MyAddin { get; set; } }  
```  
  
 Dal punto di vista del motore della composizione, un tipo di contratto `Lazy<T>` è considerato identico al tipo di contratto `T`. L'importazione precedente, quindi, corrisponderebbe all'esportazione seguente.  
  
```vb  
<Export(GetType(IMyAddin))> Public Class MyLogger Implements IMyAddin End Class  
```  
  
```csharp  
[Export(typeof(IMyAddin))] public class MyLogger : IMyAddin { }  
```  
  
 Il nome e il tipo di contratto possono essere specificati nell'attributo `Import` per un'importazione differita, come illustrato in precedenza nella sezione "Nozioni fondamentali su importazione ed esportazione".  
  
### Importazioni essenziali  
 Le parti MEF esportate sono in genere create dal motore della composizione, in risposta a una richiesta diretta o alla necessità di soddisfare un'importazione corrispondente. Per impostazione predefinita, quando si crea una parte, il motore della composizione usa il costruttore senza parametri. Per fare in modo che il motore usi un costruttore diverso, è possibile contrassegnarlo con l'attributo `ImportingConstructor`.  
  
 Ogni parte può avere solo un costruttore per l'uso da parte del motore della composizione. Se non si specifica alcun costruttore predefinito e alcun attributo `ImportingConstructor` o se si specifica più di un attributo `ImportingConstructor`, si verificherà un errore.  
  
 Per compilare i parametri di un costruttore contrassegnato con l'attributo `ImportingConstructor`, tutti questi parametri sono dichiarati automaticamente come importazioni. Si tratta di una soluzione utile per dichiarare importazioni usate durante l'inizializzazione delle parti. La classe seguente usa `ImportingConstructor` per dichiarare un'importazione.  
  
```vb  
Public Class MyClass1 Private _theAddin As IMyAddin 'Default constructor will NOT be used 'because the ImportingConstructor 'attribute is present. Public Sub New() End Sub 'This constructor will be used. 'An import with contract type IMyAddin 'is declared automatically. <ImportingConstructor()> Public Sub New(ByVal MyAddin As IMyAddin) _theAddin = MyAddin End Sub End Class  
```  
  
```csharp  
public class MyClass { private IMyAddin _theAddin; //Default constructor will NOT be //used because the ImportingConstructor //attribute is present. public MyClass() { } //This constructor will be used. //An import with contract type IMyAddin is //declared automatically. [ImportingConstructor] public MyClass(IMyAddin MyAddin) { _theAddin = MyAddin; } }  
```  
  
 Per impostazione predefinita, l'attributo `ImportingConstructor` usa i tipi e nomi di contratto dedotti per tutte le importazioni di parametri. È possibile eseguire l'override di questa procedura dichiarando i parametri con gli attributi `Import`, che possono quindi definire in modo esplicito il tipo e il nome del contratto. Il codice seguente illustra un costruttore che usa questa sintassi per importare una classe derivata invece di una classe padre.  
  
```vb  
<ImportingConstructor()> Public Sub New(<Import(GetType(IMySubAddin))> ByVal MyAddin As IMyAddin) End Sub  
```  
  
```csharp  
[ImportingConstructor] public MyClass([Import(typeof(IMySubAddin))]IMyAddin MyAddin) { _theAddin = MyAddin; }  
```  
  
 In particolare, occorre prestare attenzione ai parametri di raccolta. Se, ad esempio, si specifica `ImportingConstructor` su un costruttore con parametro di tipo `IEnumerable<int>`, l'importazione corrisponderà a una esportazione di tipo `IEnumerable<int>`, invece che a un insieme di esportazioni di tipo `int`. Per ottenere la corrispondenza a un insieme di esportazioni di tipo `int`, è necessario decorare il parametro con l'attributo `ImportMany`.  
  
 I parametri dichiarati come importazioni dall'attributo `ImportingConstructor` sono contrassegnati anche come *importazioni essenziali*. MEF permette in genere a esportazioni e importazioni di formare un *ciclo*. Ad esempio, un ciclo è rappresentato dall'oggetto A che importa l'oggetto B, che a sua volta importa l'oggetto A. In circostanze normali un ciclo non rappresenta un problema e il contenitore di composizione costruisce normalmente entrambi gli oggetti.  
  
 Se il costruttore di una parte necessita di un valore importato, tale oggetto non può essere incluso in un ciclo. Se per la costruzione dell'oggetto A è necessaria prima di tutto la costruzione dell'oggetto B e l'oggetto B importa l'oggetto A, il ciclo non potrà essere risolto e si verificherà un errore di composizione. Le importazioni dichiarate nei parametri del costruttore sono quindi importazioni essenziali, che devono essere completate prima che sia possibile usare qualsiasi esportazione dall'oggetto che le richiede.  
  
### Importazioni facoltative  
 L'attributo `Import` specifica un requisito necessario per il funzionamento della parte. Se non è possibile soddisfare un'importazione, la composizione della parte avrà esito negativo e la parte non sarà disponibile.  
  
 È possibile specificare che un'importazione è *facoltativa* usando la proprietà `AllowDefault`. In questo caso, la composizione avrà esito positivo, anche se l'importazione non corrisponde ad alcuna esportazione disponibile, e la proprietà che esegue l'importazione sarà impostata sul valore predefinito per il tipo di proprietà specifico \(`null` per proprietà degli oggetti, `false` per proprietà booleane oppure zero per proprietà numeriche\). La classe seguente usa un'importazione facoltativa.  
  
```vb  
Public Class MyClass1 <Import(AllowDefault:=True)> Public Property thePlugin As Plugin 'If no matching export is available, 'thePlugin will be set to null. End Class  
```  
  
```csharp  
public class MyClass { [Import(AllowDefault = true)] public Plugin thePlugin { get; set; } //If no matching export is avaliable, //thePlugin will be set to null. }  
```  
  
### Importazione di più oggetti  
 La composizione dell'attributo `Import` avrà esito positivo solo se corrisponde a una sola esportazione. Gli altri casi provocheranno un errore di composizione. Per importare più di un'esportazione che corrisponde allo stesso contratto, usare l'attributo `ImportMany`. Le importazioni contrassegnate con questo attributo sono sempre facoltative. Ad esempio, la composizione avrà esito positivo se non sono presenti esportazioni corrispondenti. La classe seguente importa qualsiasi numero di esportazioni di tipo `IMyAddin`.  
  
```vb  
Public Class MyClass1 <ImportMany()> Public Property MyAddin As IEnumerable(Of IMyAddin) End Class  
```  
  
```csharp  
public class MyClass { [ImportMany] public IEnumerable<IMyAddin> MyAddin { get; set; } }  
```  
  
 È possibile accedere alla matrice importata usando la normale sintassi e i normali metodi di `IEnumerable<T>`. È anche possibile usare invece una matrice normale \(`IMyAddin[]`\).  
  
 Questo modello può risultare molto importante se lo si usa insieme alla sintassi `Lazy<T>`. Ad esempio, se si usa `ImportMany`, `IEnumerable<T>` e `Lazy<T>`, sarà possibile importare riferimenti indiretti a qualsiasi numero di oggetti e creare istanze solo degli oggetti che diventano necessari. Questo modello è illustrato dalla classe seguente.  
  
```vb  
Public Class MyClass1 <ImportMany()> Public Property MyAddin As IEnumerable(Of Lazy(Of IMyAddin)) End Class  
```  
  
```csharp  
public class MyClass { [ImportMany] public IEnumerable<Lazy<IMyAddin>> MyAddin { get; set; } }  
```  
  
<a name="avoiding_discovery"></a>   
## Evitare l'individuazione  
 In alcuni casi è possibile che si voglia evitare l'individuazione di una parte come parte di un catalogo. Ad esempio, è possibile che la parte sia una classe di base da cui ereditare, ma da non usare. È possibile ottenere questo risultato in due modi. Si può prima di tutto usare la parola chiave `abstract` nella classe della parte. Le classi astratte non forniscono mai esportazioni, anche se possono fornire esportazioni ereditate alle classi da esse derivate.  
  
 Se non è possibile rendere astratta la classe, sarà possibile decorarla con l'attributo `PartNotDiscoverable`. Una parte decorata con questo attributo non sarà inclusa in alcun catalogo. L'esempio seguente illustra questi modelli.`DataOne` sarà individuata dal catalogo. Poiché `DataTwo` è astratta, non sarà individuata. Poiché `DataThree` ha usato l'attributo `PartNotDiscoverable`, non sarà individuata.  
  
```vb  
<Export()> Public Class DataOne 'This part will be discovered 'as normal by the catalog. End Class <Export()> Public MustInherit Class DataTwo 'This part will not be discovered 'by the catalog. End Class <PartNotDiscoverable()> <Export()> Public Class DataThree 'This part will also not be discovered 'by the catalog. End Class  
```  
  
```csharp  
[Export] public class DataOne { //This part will be discovered //as normal by the catalog. } [Export] public abstract class DataTwo { //This part will not be discovered //by the catalog. } [PartNotDiscoverable] [Export] public class DataThree { //This part will also not be discovered //by the catalog. }  
```  
  
<a name="metadata_and_metadata_views"></a>   
## Metadati e viste dei metadati  
 Le esportazioni possono fornire informazioni aggiuntive su se stesse, definite *metadati*. I metadati possono essere usati per trasmettere le proprietà dell'oggetto esportato alla parte che esegue l'importazione. La parte che esegue l'importazione può usare questi dati per decidere quali esportazioni usare oppure per ottenere informazioni su un'esportazione senza doverla costruire. Per questo motivo, un'importazione deve essere differita per usare i metadati.  
  
 Per usare i metadati si dichiara in genere un'interfaccia definita *vista dei metadati*, in cui sono dichiarati i metadati che saranno disponibili. L'interfaccia della vista dei metadati deve includere solo proprietà e queste proprietà devono avere `get` funzioni di accesso. L'interfaccia seguente è un esempio di vista dei metadati.  
  
```vb  
Public Interface IPluginMetadata ReadOnly Property Name As String <DefaultValue(1)> ReadOnly Property Version As Integer End Interface  
```  
  
```csharp  
public interface IPluginMetadata { string Name { get; } [DefaultValue(1)] int Version { get; } }  
```  
  
 È anche possibile usare una raccolta generica, `IDictionary<string, object>`, come vista dei metadati, ma in questo modo non saranno disponibili i vantaggi correlati alla verifica dei tipi e questa procedura è quindi sconsigliata.  
  
 In genere, tutte le proprietà indicate nella vista dei metadati sono necessarie ed eventuali esportazioni che non le forniscono non saranno considerate come corrispondenze. L'attributo `DefaultValue` specifica che una proprietà è facoltativa. Se non è inclusa, alla proprietà sarà assegnato il valore predefinito specificato come parametro di `DefaultValue`. Di seguito sono riportate due classi diverse decorate con metadati. Entrambe le classi corrisponderebbero alla vista dei metadati precedente.  
  
```vb  
<Export(GetType(IPlugin))> <ExportMetadata("Name", "Logger")> <ExportMetadata("Version", 4)> Public Class MyLogger Implements IPlugin End Class 'Version is not required because of the DefaultValue <Export(GetType(IPlugin))> <ExportMetadata("Name", "Disk Writer")> Public Class DWriter Implements IPlugin End Class  
```  
  
```csharp  
[Export(typeof(IPlugin)), ExportMetadata("Name", "Logger"), ExportMetadata("Version", 4)] public class Logger : IPlugin { } [Export(typeof(IPlugin)), ExportMetadata("Name", "Disk Writer")] //Version is not required because of the DefaultValue public class DWriter : IPlugin { }  
```  
  
 I metadati sono espressi dopo l'attributo `Export` tramite l'attributo `ExportMetadata`. Ogni elemento di metadati è costituito da una coppia nome\/valore. La parte relativa al nome dei metadati deve corrispondere al nome della proprietà appropriata nella vista dei metadati e il valore sarà assegnato a tale proprietà.  
  
 L'utilità di importazione specifica l'eventuale vista dei metadati che sarà usata. Un'importazione con metadati è dichiarata come importazione differita, con l'interfaccia dei metadati come parametro di secondo tipo per `Lazy<T,T>`. La classe seguente importa la parte precedente con i metadati.  
  
```vb  
Public Class Addin <Import()> Public Property plugin As Lazy(Of IPlugin, IPluginMetadata) End Class  
```  
  
```csharp  
public class Addin { [Import] public Lazy<IPlugin, IPluginMetadata> plugin; }  
```  
  
 In molti casi è consigliabile combinare i metadati con l'attributo `ImportMany`, in modo da analizzare le importazioni disponibili e scegliere e creare istanze di una sola importazione oppure per filtrare una raccolta in modo che corrisponda a una determinata condizione. La classe seguente crea istanze dei soli oggetti `IPlugin` con valore `Name` impostato su "Logger".  
  
```vb  
Public Class User <ImportMany()> Public Property plugins As IEnumerable(Of Lazy(Of IPlugin, IPluginMetadata)) Public Function InstantiateLogger() As IPlugin Dim logger As IPlugin logger = Nothing For Each Plugin As Lazy(Of IPlugin, IPluginMetadata) In plugins If (Plugin.Metadata.Name = "Logger") Then logger = Plugin.Value End If Next Return logger End Function End Class  
```  
  
```csharp  
public class User { [ImportMany] public IEnumerable<Lazy<IPlugin, IPluginMetadata>> plugins; public IPlugin InstantiateLogger () { IPlugin logger = null; foreach (Lazy<IPlugin, IPluginMetadata> plugin in plugins) { if (plugin.Metadata.Name = "Logger") logger = plugin.Value; } return logger; } }  
```  
  
<a name="import_and_export_inheritance"></a>   
## Eredità di importazione ed esportazione  
 Se una classe eredita da una parte, anche tale classe può diventare una parte. Le importazioni sono sempre ereditate dalle sottoclassi. Una sottoclasse di una parte, quindi, sarà sempre una parte, con le stesse importazioni come classe padre.  
  
 Le esportazioni dichiarate usando l'attributo `Export` non sono ereditate dalle sottoclassi. Una parte, tuttavia, può esportare se stessa usando l'attributo `InheritedExport`. Le sottoclassi della parte erediteranno e forniranno la stessa esportazione, inclusi nome e tipo di contratto. A differenza di un attributo `Export`, `InheritedExport` può essere applicato solo a livello di classe, non a livello di membro. Le esportazioni a livello di membri non possono quindi essere mai ereditate.  
  
 Le quattro classi seguenti illustrano i principi dell'ereditarietà di importazione ed esportazione.`NumTwo` eredita da `NumOne`, quindi `NumTwo` importerà `IMyData`. Le esportazioni normali non sono ereditate, quindi `NumTwo` non esporterà nulla.`NumFour` eredita da `NumThree`. Poiché `NumThree` ha usato `InheritedExport`, `NumFour` ha un'esportazione con tipo di contratto `NumThree`. Le esportazioni a livello di membri non sono mai ereditate, quindi `IMyData` non viene esportato.  
  
```vb  
<Export()> Public Class NumOne <Import()> Public Property MyData As IMyData End Class Public Class NumTwo Inherits NumOne 'Imports are always inherited, so NumTwo will 'Import IMyData 'Ordinary exports are not inherited, so 'NumTwo will NOT export anything.  As a result it 'will not be discovered by the catalog! End Class <InheritedExport()> Public Class NumThree <Export()> Public Property MyData As IMyData 'This part provides two exports, one of 'contract type NumThree, and one of 'contract type IMyData. End Class Public Class NumFour Inherits NumThree 'Because NumThree used InheritedExport, 'this part has one export with contract 'type NumThree. 'Member-level exports are never inherited, 'so IMyData is not exported. End Class  
```  
  
```csharp  
[Export] public class NumOne { [Import] public IMyData MyData { get; set; } } public class NumTwo : NumOne { //Imports are always inherited, so NumTwo will //import IMyData. //Ordinary exports are not inherited, so //NumTwo will NOT export anything. As a result it //will not be discovered by the catalog! } [InheritedExport] public class NumThree { [Export] Public IMyData MyData { get; set; } //This part provides two exports, one of //contract type NumThree, and one of //contract type IMyData. } public class NumFour : NumThree { //Because NumThree used InheritedExport, //this part has one export with contract //type NumThree. //Member-level exports are never inherited, //so IMyData is not exported. }  
```  
  
 Se a un attributo `InheritedExport` sono associati metadati, anche i metadati saranno ereditati. Per altre informazioni, vedere la sezione precedente "Metadati e viste dei metadati". I metadati ereditati non possono essere modificati dalla sottoclasse. Dichiarando di nuovo l'attributo `InheritedExport` con lo stesso nome e tipo di contratto ma con nuovi metadati, tuttavia, la sottoclasse potrà sostituire i metadati ereditati con nuovi metadati. La classe seguente illustra questo principio. La parte `MegaLogger` eredita da `Logger` e include l'attributo `InheritedExport`. Poiché `MegaLogger` ripete la dichiarazione di nuovi metadati con nome Status, non erediterà i metadati Name e Version da `Logger`.  
  
```vb  
<InheritedExport(GetType(IPlugin))> <ExportMetadata("Name", "Logger")> <ExportMetadata("Version", 4)> Public Class Logger Implements IPlugin 'Exports with contract type IPlugin 'and metadata "Name" and "Version". End Class Public Class SuperLogger Inherits Logger 'Exports with contract type IPlugin and 'metadata "Name" and "Version", exactly the same 'as the Logger class. End Class <InheritedExport(GetType(IPlugin))> <ExportMetadata("Status", "Green")> Public Class MegaLogger Inherits Logger 'Exports with contract type IPlugin and 'metadata "Status" only. Re-declaring 'the attribute replaces all metadata. End Class  
```  
  
```csharp  
[InheritedExport(typeof(IPlugin)), ExportMetadata("Name", "Logger"), ExportMetadata("Version", 4)] public class Logger : IPlugin { //Exports with contract type IPlugin and //metadata "Name" and "Version". } public class SuperLogger : Logger { //Exports with contract type IPlugin and //metadata "Name" and "Version", exactly the same //as the Logger class. } [InheritedExport(typeof(IPlugin)), ExportMetadata("Status", "Green")] public class MegaLogger : Logger        { //Exports with contract type IPlugin and //metadata "Status" only. Re-declaring //the attribute replaces all metadata. }  
```  
  
 Quando si dichiara di nuovo l'attributo `InheritedExport` per eseguire l'override dei metadati, occorre assicurarsi che i tipi di contratto siano uguali. Nell'esempio precedente, `IPlugin` è il tipo di contratto In caso di differenza, invece di eseguire l'override, il secondo attributo creerà una seconda esportazione indipendente dalla parte. In genere, ciò significa che sarà necessario specificare in modo esplicito il tipo di contratto quando si esegue l'override di un attributo `InheritedExport`, come illustrato nell'esempio precedente.  
  
 Poiché non è possibile creare direttamente istanze delle interfacce, non è in genere possibile decorarle con attributi `Export` o `Import`. Un'interfaccia può essere tuttavia decorata con l'attributo `InheritedExport` a livello di interfaccia e tale esportazione, insieme a eventuali metadati associati, sarà ereditata da qualsiasi classe che esegue l'implementazione. L'interfaccia stessa, tuttavia, non sarà disponibile come parte.  
  
<a name="custom_export_attributes"></a>   
## Attributi di esportazione personalizzati  
 Gli attributi di esportazione di base, `Export` e `InheritedExport`, possono essere estesi in modo da includere metadati come proprietà degli attributi. Questa tecnica è utile per l'applicazione di metadati simili a molte parti oppure per creare un albero di eredità di attributi di metadati.  
  
 Un attributo personalizzato può specificare il tipo di contratto, il nome del contratto o altri metadati. Per definire un attributo personalizzato, una classe che eredita da `ExportAttribute` \(o `InheritedExportAttribute`\) deve essere decorata con l'attributo `MetadataAttribute`. La classe seguente definisce un attributo personalizzato.  
  
```vb  
<MetadataAttribute()> <AttributeUsage(AttributeTargets.Class, AllowMultiple:=false)> Public Class MyAttribute Inherits ExportAttribute Public Property MyMetadata As String Public Sub New(ByVal myMetadata As String) MyBase.New(GetType(IMyAddin)) myMetadata = myMetadata End Sub End Class  
```  
  
```csharp  
[MetadataAttribute] [AttributeUsage(AttributeTargets.Class, AllowMultiple=false)] public class MyAttribute : ExportAttribute { public MyAttribute(string myMetadata) : base(typeof(IMyAddin)) { MyMetadata = myMetadata; } public string MyMetadata { get; private set; } }  
```  
  
 Questa classe definisce un attributo personalizzato denominato `MyAttribute` con tipo di contratto `IMyData` e alcuni metadati con nome `MyMetadata`. Tutte le proprietà in una classe contrassegnata con l'attributo `MetadataAttribute` sono considerate come metadati definiti nell'attributo personalizzato. Le due dichiarazioni seguenti sono equivalenti.  
  
```vb  
<Export(GetType(IMyAddin))> <ExportMetadata("MyMetadata", "theData")> Public Property myAddin As MyAddin <MyAttribute("theData")> Public Property myAddin As MyAddin  
```  
  
```csharp  
[Export(typeof(IMyAddin)), ExportMetadata("MyMetadata", "theData")] public MyAddin myAddin { get; set; }  
```  
  
```  
[MyAttribute("theData")] public MyAddin myAddin { get; set; }  
```  
  
 Nella prima dichiarazione il tipo di contratto e i metadati sono definiti in modo esplicito. Nella seconda dichiarazione il tipo di contratto e i metadati sono impliciti nell'attributo personalizzato. In particolare nei casi in cui è necessario applicare una quantità elevata di metadati identici a molte parti, ad esempio informazioni su autore o copyright, l'uso di un attributo personalizzato può permettere un notevole risparmio di tempo e di duplicazione. Gli alberi di eredità degli attributi personalizzati, inoltre, possono essere creati in modo da permettere variazioni.  
  
 Per creare metadati facoltativi in un attributo personalizzato, è possibile usare l'attributo `DefaultValue`. Quando questo attributo è applicato a una proprietà in una classe di attributi personalizzata, specifica che la proprietà decorata è facoltativa e non deve essere fornita da un'utilità di esportazione. Se un valore per la proprietà non è stato fornito, sarà assegnato il valore predefinito per questo tipo di proprietà, in genere `null`, `false` o 0.  
  
<a name="creation_policies"></a>   
## Criteri di creazione  
 Quando una parte specifica un'importazione e si esegue una composizione, il contenitore di composizione tenta di trovare un'esportazione corrispondente. In caso di corretta corrispondenza tra importazione ed esportazione, il membro che esegue l'importazione è impostato su un'istanza dell'oggetto esportato. La provenienza di questa istanza è controllata dai *criteri di creazione* della parte che esegue l'esportazione.  
  
 I due criteri di creazione consentiti sono *condivisi* e *non condivisi*. Una parte con criteri di creazione condivisi sarà condivisa tra tutte le importazioni nel contenuto per una parte con tale contratto. Quando il motore della composizione rileva una corrispondenza e deve impostare una proprietà che esegue l'importazione, crea un'istanza di una nuova copia della parte solo se non esiste già. In caso contrario, fornisce la copia esistente. Ciò significa che molti oggetti potrebbero includere riferimenti alla stessa parte. È quindi consigliabile che queste parti non si basino su uno stato interno che potrebbe subire modifiche da molte posizioni. Questi criteri sono appropriati per parti statiche, parti che offrono servizi e parti che usano una quantità elevata di memoria o di risorse di altro tipo.  
  
 Una parte con criteri di creazione non condivisi sarà creata ogni volta che è rilevata un'importazione corrispondente per una delle esportazioni della parte. Sarà quindi creata un'istanza della nuova copia per ogni importazione nel contenitore corrispondente a uno dei contratti esportati della parte. Lo stato interno di queste copie non sarà condiviso. Questi criteri sono appropriati per parti in cui ogni importazione necessita del proprio stato interno.  
  
 Sia l'importazione che l'esportazione possono specificare i criteri di creazione di una parte, scegliendo tra i valori `Shared`, `NonShared` o `Any`. Il valore predefinito è `Any` sia per le importazioni che per le esportazioni. Un'esportazione che specifica `Shared` o `NonShared` corrisponderà solo a un'importazione che specifica lo stesso valore o che specifica `Any`. Analogamente, un'importazione che specifica `Shared` o `NonShared` corrisponderà solo a un'esportazione che specifica lo stesso valore o che specifica `Any`. Le importazioni e le esportazioni con criteri di creazione non compatibili non saranno considerate come corrispondenti, esattamente come non lo sono un'importazione e un'esportazione con tipo o nome di contratto non corrispondenti. Se sia l'importazione che l'esportazione specificano `Any` o non specificano alcun criterio di creazione e usano il valore predefinito `Any`, i criteri di creazione saranno condivisi per impostazione predefinita.  
  
 L'esempio seguente mostra sia le importazioni che le esportazioni che specificano criteri di creazione.`PartOne` non specifica alcun criterio di creazione, quindi l'impostazione predefinita è `Any`.`PartTwo` non specifica alcun criterio di creazione, quindi l'impostazione predefinita è `Any`. Poiché sia per l'importazione che per l'esportazione sarà usato il valore predefinito `Any`, `PartOne` sarà condivisa.`PartThree` specifica un criterio di creazione `Shared`, quindi `PartTwo` e `PartThree` condivideranno la stessa copia di `PartOne`.`PartFour` specifica un criterio di creazione `NonShared`, quindi `PartFour` non saranno condivisi in `PartFive`.`PartSix` specifica un criterio di creazione `NonShared`.`PartFive` e `PartSix` riceveranno copie distinte di `PartFour`.`PartSeven` specifica un criterio di creazione `Shared`. Poiché non è disponibile alcuna `PartFour` esportata con un criterio di creazione `Shared`, l'importazione `PartSeven` non corrisponde a nessun elemento e non sarà completata.  
  
```vb  
<Export()> Public Class PartOne 'The default creation policy for an export is Any. End Class Public Class PartTwo <Import()> Public Property partOne As PartOne 'The default creation policy for an import is Any. 'If both policies are Any, the part will be shared. End Class Public Class PartThree <Import(RequiredCreationPolicy:=CreationPolicy.Shared)> Public Property partOne As PartOne 'The Shared creation policy is explicitly specified. 'PartTwo and PartThree will receive references to the 'SAME copy of PartOne. End Class <Export()> <PartCreationPolicy(CreationPolicy.NonShared)> Public Class PartFour 'The NonShared creation policy is explicitly specified. End Class Public Class PartFive <Import()> Public Property partFour As PartFour 'The default creation policy for an import is Any. 'Since the export's creation policy was explictly 'defined, the creation policy for this property will 'be non-shared. End Class Public Class PartSix <Import(RequiredCreationPolicy:=CreationPolicy.NonShared)> Public Property partFour As PartFour 'Both import and export specify matching creation 'policies.  PartFive and PartSix will each receive 'SEPARATE copies of PartFour, each with its own 'internal state. End Class Public Class PartSeven <Import(RequiredCreationPolicy:=CreationPolicy.Shared)> Public Property partFour As PartFour 'A creation policy mismatch.  Because there is no 'exported PartFour with a creation policy of Shared, 'this import does not match anything and will not be 'filled. End Class  
```  
  
```csharp  
[Export] public class PartOne { //The default creation policy for an export is Any. } public class PartTwo { [Import] public PartOne partOne { get; set; } //The default creation policy for an import is Any. //If both policies are Any, the part will be shared. } public class PartThree { [Import(RequiredCreationPolicy = CreationPolicy.Shared)] public PartOne partOne { get; set; } //The Shared creation policy is explicitly specified. //PartTwo and PartThree will receive references to the //SAME copy of PartOne. } [Export] [PartCreationPolicy(CreationPolicy.NonShared)] public class PartFour { //The NonShared creation policy is explicitly specified. } public class PartFive { [Import] public PartFour partFour { get; set; } //The default creation policy for an import is Any. //Since the export's creation policy was explictly //defined, the creation policy for this property will //be non-shared. } public class PartSix { [Import(RequiredCreationPolicy = CreationPolicy.NonShared)] public PartFour partFour { get; set; } //Both import and export specify matching creation //policies.  PartFive and PartSix will each receive //SEPARATE copies of PartFour, each with its own //internal state. } public class PartSeven { [Import(RequiredCreationPolicy = CreationPolicy.Shared)] public PartFour partFour { get; set; } //A creation policy mismatch.  Because there is no //exported PartFour with a creation policy of Shared, //this import does not match anything and will not be //filled. }  
```  
  
<a name="life_cycle_and_disposing"></a>   
## Ciclo di vita ed eliminazione  
 Poiché le parti sono ospitate nel contenitore di composizione, il relativo ciclo di vita può essere più complesso rispetto a quello degli oggetti normali. Le parti possono implementare due interfacce importanti correlate al ciclo di vita, ovvero `IDisposable` e `IPartImportsSatisfiedNotification`.  
  
 Le parti che necessitano dell'esecuzione di operazioni in fase di arresto o del rilascio di risorse devono implementare `IDisposable`, come di consueto per oggetti .NET Framework. Poiché tuttavia il contenitore crea e gestisce riferimenti alle parti, solo il contenitore proprietario di una parte dovrebbe chiamare il metodo `Dispose` per tale parte. Il contenitore stesso implementa `IDisposable` e come parte della pulizia in `Dispose` chiamerà `Dispose` per tutte le parti di sua proprietà. Per questo motivo, è sempre consigliabile eliminare il contenitore di composizione quando il contenitore ed eventuali parti di sua proprietà non sono più necessari.  
  
 Per i contenitori di composizione di lunga durata, il consumo di memoria da parte delle parti con criteri di creazione non condivisi può rappresentare un problema. Le parti non condivise possono essere create più volte e saranno eliminate solo quando si elimina il contenitore stesso. Per risolvere questo problema, il contenitore fornisce il metodo `ReleaseExport`. Se si chiama questo metodo in un'esportazione non condivisa, tale esportazione sarà rimossa dal contenitore di composizione e sarà eliminata. Saranno rimosse ed eliminate anche le parti usate solo dall'esportazione rimossa e così via lungo l'albero. In questo modo sarà possibile recuperare le risorse senza eliminare il contenitore di composizione.  
  
 `IPartImportsSatisfiedNotification` include un metodo con nome `OnImportsSatisfied`. Questo metodo è chiamato dal contenitore di composizione per qualsiasi parte che implementa l'interfaccia quando la composizione è stata completata e le importazioni della parte sono pronte per l'uso. Le parti sono create dal motore di composizione per completare le importazioni di altre parti. Prima dell'impostazione delle importazioni di una parte, sarà possibile eseguire inizializzazioni che si basano su o che modificano valori importati nel costruttore della parte solo se tali valori sono stati specificati come prerequisiti usando l'attributo `ImportingConstructor`. Questo è in genere il metodo preferito, ma in alcuni casi è possibile che l'aggiunta di costruttori non sia disponibile. In questi casi l'inizializzazione può essere eseguita in `OnImportsSatisfied` e la parte deve implementare `IPartImportsSatisfiedNotification`.  
  
## Vedere anche  
 [Video Channel 9: Aprire le applicazioni con Managed Extensibility Framework](http://channel9.msdn.com/events/TechEd/NorthAmerica/2009/DTL328)   
 [Video Channel 9: Managed Extensibility Framework \(MEF\) 2.0](http://channel9.msdn.com/posts/NET-45-Oleg-Lvovitch-and-Kevin-Ransom-Managed-Extensibility-Framework-MEF-20)