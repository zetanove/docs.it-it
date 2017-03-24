---
title: Raccolte (Visual Basic) | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: get-started-article
dev_langs:
- VB
ms.assetid: 5f7749f3-aaf2-4319-b63c-bfa72e1e2b7a
caps.latest.revision: 6
author: stevehoag
ms.author: shoag
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: b3c8de3e22075d576f86bcd4eb599946740ebe16
ms.lasthandoff: 03/13/2017

---
# <a name="collections-visual-basic"></a>Raccolte (Visual Basic)
Per molte applicazioni è utile creare e gestire gruppi di oggetti correlati. È possibile raggruppare gli oggetti in due modi: creando matrici di oggetti e creando raccolte di oggetti.  
  
 Le matrici sono estremamente utili per la creazione e l'uso di un numero fisso di oggetti fortemente tipizzati. Per informazioni sulle matrici, vedere [matrici](../../../visual-basic/programming-guide/language-features/arrays/index.md).  
  
 Le raccolte consentono di lavorare in modo più flessibile con gruppi di oggetti. A differenza delle matrici, il gruppo di oggetti con cui si lavora può aumentare e diminuire in modo dinamico in base alle esigenze dell'applicazione. Per alcune raccolte è possibile assegnare una chiave a qualsiasi oggetto inserito nella raccolta in modo da recuperare rapidamente l'oggetto usando la chiave.  
  
 Una Collection è una classe. Di conseguenza, prima di poter aggiungere elementi a una nuova raccolta è necessario dichiarare la Collection.  
  
 Se la raccolta contiene elementi di un solo tipo di dati, è possibile utilizzare una delle classi di <xref:System.Collections.Generic?displayProperty=fullName>dello spazio dei nomi.</xref:System.Collections.Generic?displayProperty=fullName> In una raccolta generica viene imposta l'indipendenza dai tipi, in modo da impedire che vengano aggiunti altri tipi di dati alla raccolta. Quando si recupera un elemento da una raccolta generica, non è necessario determinarne il tipo di dati né convertirlo.  
  
> [!NOTE]
>  Per gli esempi in questo argomento, includere [importazioni](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md) le istruzioni per la `System.Collections.Generic` e `System.Linq` gli spazi dei nomi.  
  
 **Contenuto dell'argomento**  
  
-   [Utilizzando una semplice raccolta](#BKMK_SimpleCollection)  
  
-   [Tipi di raccolte](#BKMK_KindsOfCollections)  
  
    -   [Classi System.Collections.Generic](#BKMK_Generic)  
  
    -   [Classi System.Collections.Concurrent](#BKMK_Concurrent)  
  
    -   [Classi System. Collections](#BKMK_Collections)  
  
    -   [Classe di raccolta di Visual Basic](#BKMK_VisualBasic)  
  
-   [Implementazione di una raccolta di coppie chiave/valore](#BKMK_KeyValuePairs)  
  
-   [Utilizzo di LINQ per accedere a una raccolta](#BKMK_LINQ)  
  
-   [Ordinamento di una raccolta](#BKMK_Sorting)  
  
-   [Definizione di una raccolta personalizzata](#BKMK_CustomCollection)  
  
-   [Iteratori](#BKMK_Iterators)  
  
<a name="BKMK_SimpleCollection"></a>
## <a name="using-a-simple-collection"></a>Uso di una raccolta semplice  
 Negli esempi inclusi in questa sezione utilizzano gli elementi generici <xref:System.Collections.Generic.List%601>classe, che consente di lavorare con un elenco di oggetti fortemente tipizzato.</xref:System.Collections.Generic.List%601>  
  
 Nell'esempio seguente viene creato un elenco di stringhe e quindi scorre le stringhe mediante un [For Each... Avanti](../../../visual-basic/language-reference/statements/for-each-next-statement.md) istruzione.  
  
```vb  
' Create a list of strings.  
Dim salmons As New List(Of String)  
salmons.Add("chinook")  
salmons.Add("coho")  
salmons.Add("pink")  
salmons.Add("sockeye")  
  
' Iterate through the list.  
For Each salmon As String In salmons  
    Console.Write(salmon & " ")  
Next  
'Output: chinook coho pink sockeye  
```  
  
 Se il contenuto di una raccolta è noti in anticipo, è possibile utilizzare un *inizializzatore di raccolta* per inizializzare la raccolta. Per ulteriori informazioni, vedere [gli inizializzatori di insieme](../../../visual-basic/programming-guide/language-features/collection-initializers/index.md).  
  
 L'esempio seguente è identico all'esempio precedente, ma usa un inizializzatore di raccolta per aggiungere elementi alla raccolta.  
  
```vb  
' Create a list of strings by using a  
' collection initializer.  
Dim salmons As New List(Of String) From  
    {"chinook", "coho", "pink", "sockeye"}  
  
For Each salmon As String In salmons  
    Console.Write(salmon & " ")  
Next  
'Output: chinook coho pink sockeye  
```  
  
 È possibile utilizzare un [per... Avanti](../../../visual-basic/language-reference/statements/for-next-statement.md) istruzione anziché un `For Each` istruzione per scorrere una raccolta. Questo è possibile mediante l'accesso agli elementi della raccolta dalla posizione di indice. L'indice degli elementi inizia da 0 e termina in corrispondenza del numero di elementi meno 1.  
  
 Nell'esempio seguente scorre gli elementi di una raccolta tramite `For…Next` anziché `For Each`.  
  
```vb  
Dim salmons As New List(Of String) From  
    {"chinook", "coho", "pink", "sockeye"}  
  
For index = 0 To salmons.Count - 1  
    Console.Write(salmons(index) & " ")  
Next  
'Output: chinook coho pink sockeye  
```  
  
 Nell'esempio seguente viene rimosso un elemento dalla raccolta specificando l'oggetto da rimuovere.  
  
```vb  
' Create a list of strings by using a  
' collection initializer.  
Dim salmons As New List(Of String) From  
    {"chinook", "coho", "pink", "sockeye"}  
  
' Remove an element in the list by specifying  
' the object.  
salmons.Remove("coho")  
  
For Each salmon As String In salmons  
    Console.Write(salmon & " ")  
Next  
'Output: chinook pink sockeye  
```  
  
 Nell'esempio seguente vengono rimossi elementi da un elenco generico. Invece di un `For Each` istruzione, una [per... Avanti](../../../visual-basic/language-reference/statements/for-next-statement.md) viene utilizzata l'istruzione che esegue l'iterazione in ordine decrescente. In questo modo il <xref:System.Collections.Generic.List%601.RemoveAt%2A>(metodo), gli elementi dopo un elemento rimosso un valore di indice più basso.</xref:System.Collections.Generic.List%601.RemoveAt%2A>  
  
```vb  
Dim numbers As New List(Of Integer) From  
    {0, 1, 2, 3, 4, 5, 6, 7, 8, 9}  
  
' Remove odd numbers.  
For index As Integer = numbers.Count - 1 To 0 Step -1  
    If numbers(index) Mod 2 = 1 Then  
        ' Remove the element by specifying  
        ' the zero-based index in the list.  
        numbers.RemoveAt(index)  
    End If  
Next  
  
' Iterate through the list.  
' A lambda expression is placed in the ForEach method  
' of the List(T) object.  
numbers.ForEach(  
    Sub(number) Console.Write(number & " "))  
' Output: 0 2 4 6 8  
```  
  
 Per il tipo di elementi <xref:System.Collections.Generic.List%601>è inoltre possibile definire la propria classe.</xref:System.Collections.Generic.List%601> Nell'esempio seguente, il `Galaxy` classe che viene utilizzato il <xref:System.Collections.Generic.List%601>è definito nel codice.</xref:System.Collections.Generic.List%601>  
  
```vb  
Private Sub IterateThroughList()  
    Dim theGalaxies As New List(Of Galaxy) From  
        {  
            New Galaxy With {.Name = "Tadpole", .MegaLightYears = 400},  
            New Galaxy With {.Name = "Pinwheel", .MegaLightYears = 25},  
            New Galaxy With {.Name = "Milky Way", .MegaLightYears = 0},  
            New Galaxy With {.Name = "Andromeda", .MegaLightYears = 3}  
        }  
  
    For Each theGalaxy In theGalaxies  
        With theGalaxy  
            Console.WriteLine(.Name & "  " & .MegaLightYears)  
        End With  
    Next  
  
    ' Output:  
    '  Tadpole  400  
    '  Pinwheel  25  
    '  Milky Way  0  
    '  Andromeda  3  
End Sub  
  
Public Class Galaxy  
    Public Property Name As String  
    Public Property MegaLightYears As Integer  
End Class  
```  
  
<a name="BKMK_KindsOfCollections"></a>
## <a name="kinds-of-collections"></a>Tipi di raccolte   
 Molte raccolte comuni vengono fornite da .NET Framework. Ogni tipo di raccolta è progettato per uno scopo specifico.  
  
 In questa sezione sono descritte alcune classi di raccolte comuni:  
  
-   @System.Collections.Genericclassi  
  
-   @System.Collections.Concurrentclassi  
  
-   @System.Collectionsclassi  
  
-   Visual Basic `Collection` (classe)  
  
<a name="BKMK_Generic"></a>
### <a name="systemcollectionsgeneric-classes"></a>Classi System.Collections.Generic  

 È possibile creare una raccolta generica utilizzando una delle classi di <xref:System.Collections.Generic>dello spazio dei nomi.</xref:System.Collections.Generic> Una raccolta generica è utile quando ogni elemento al suo interno presenta lo stesso tipo di dati. Una raccolta generica applica la tipizzazione forte consentendo di aggiungere soltanto i tipi di dati desiderati.  
  
 Nella tabella seguente sono elencate alcune delle classi di frequente il <xref:System.Collections.Generic?displayProperty=fullName>dello spazio dei nomi:</xref:System.Collections.Generic?displayProperty=fullName>  
  
|Classe|Descrizione|  
|---|---|  
|<xref:System.Collections.Generic.Dictionary%602></xref:System.Collections.Generic.Dictionary%602>|Rappresenta una raccolta di coppie chiave/valore organizzate in base alla chiave.|  
|<xref:System.Collections.Generic.List%601></xref:System.Collections.Generic.List%601>|Rappresenta un elenco di oggetti accessibile in base all'indice. Fornisce metodi per la ricerca, l'ordinamento e la modifica degli elenchi.|  
|<xref:System.Collections.Generic.Queue%601></xref:System.Collections.Generic.Queue%601>|Rappresenta una raccolta di oggetti FIFO (First-In First-Out).|  
|<xref:System.Collections.Generic.SortedList%602></xref:System.Collections.Generic.SortedList%602>|Rappresenta una raccolta di coppie chiave/valore ordinate per chiave in base alle associato <xref:System.Collections.Generic.IComparer%601>implementazione.</xref:System.Collections.Generic.IComparer%601>|  
|<xref:System.Collections.Generic.Stack%601></xref:System.Collections.Generic.Stack%601>|Rappresenta una raccolta di oggetti LIFO (Last-In First-Out).|  
  
 Per ulteriori informazioni, vedere [utilizzati tipi di raccolte comunemente](http://msdn.microsoft.com/library/f5d4c6a4-0d7b-4944-a9fb-3b12d9ebfd55), [selezione di una classe di raccolta](../../../standard/collections/selecting-a-collection-class.md)e <xref:System.Collections.Generic?displayProperty=fullName>.</xref:System.Collections.Generic?displayProperty=fullName>  
  
<a name="BKMK_Concurrent"></a>
### <a name="systemcollectionsconcurrent-classes"></a>Classi System.Collections.Concurrent   
 In .NET Framework 4 o successive, gli insiemi di <xref:System.Collections.Concurrent>dello spazio dei nomi forniscono operazioni thread-safe efficienti per accedere agli elementi della raccolta da più thread.</xref:System.Collections.Concurrent>  
  
 Le classi di <xref:System.Collections.Concurrent>è necessario utilizzare lo spazio dei nomi anziché i tipi corrispondenti nel <xref:System.Collections.Generic?displayProperty=fullName>e <xref:System.Collections?displayProperty=fullName>gli spazi dei nomi ogni volta che più thread accedono contemporaneamente alla raccolta.</xref:System.Collections?displayProperty=fullName> </xref:System.Collections.Generic?displayProperty=fullName> </xref:System.Collections.Concurrent> Per ulteriori informazioni, vedere [raccolte Thread-Safe](../../../standard/collections/threadsafe/index.md) e <xref:System.Collections.Concurrent>.</xref:System.Collections.Concurrent>  
  
 Alcune classi incluse nel <xref:System.Collections.Concurrent>dello spazio dei nomi sono <xref:System.Collections.Concurrent.BlockingCollection%601>, <xref:System.Collections.Concurrent.ConcurrentDictionary%602>, <xref:System.Collections.Concurrent.ConcurrentQueue%601>e <xref:System.Collections.Concurrent.ConcurrentStack%601>.</xref:System.Collections.Concurrent.ConcurrentStack%601> </xref:System.Collections.Concurrent.ConcurrentQueue%601> </xref:System.Collections.Concurrent.ConcurrentDictionary%602> </xref:System.Collections.Concurrent.BlockingCollection%601> </xref:System.Collections.Concurrent>  
  
<a name="BKMK_Collections"></a>
### <a name="systemcollections-classes"></a>Classi System.Collections    
 Le classi di <xref:System.Collections?displayProperty=fullName>dello spazio dei nomi non archiviare elementi come oggetti tipizzati in modo specifico, ma come oggetti di tipo `Object`.</xref:System.Collections?displayProperty=fullName>  
  
 Quando possibile, utilizzare le raccolte generiche nel <xref:System.Collections.Generic?displayProperty=fullName>dello spazio dei nomi o <xref:System.Collections.Concurrent>dello spazio dei nomi anziché i tipi legacy nel `System.Collections` dello spazio dei nomi.</xref:System.Collections.Concurrent> </xref:System.Collections.Generic?displayProperty=fullName>  
  
 Nella tabella seguente sono elencate alcune delle classi utilizzate di frequente il `System.Collections` dello spazio dei nomi:  
  
|Classe|Descrizione|  
|---|---|  
|<xref:System.Collections.ArrayList></xref:System.Collections.ArrayList>|Rappresenta una matrice di oggetti le cui dimensioni sono incrementate in modo dinamico in base alle esigenze.|  
|<xref:System.Collections.Hashtable></xref:System.Collections.Hashtable>|Rappresenta una raccolta di coppie chiave/valore organizzate in base al codice hash della chiave.|  
|<xref:System.Collections.Queue></xref:System.Collections.Queue>|Rappresenta una raccolta di oggetti FIFO (First-In First-Out).|  
|<xref:System.Collections.Stack></xref:System.Collections.Stack>|Rappresenta una raccolta di oggetti LIFO (Last-In First-Out).|  
  
 Il <xref:System.Collections.Specialized>dello spazio dei nomi fornisce classi di raccolte specializzate e fortemente tipizzate, ad esempio elenchi collegati e ibridi dizionari e raccolte di stringa.</xref:System.Collections.Specialized>  

<a name="BKMK_VisualBasic"></a> 
###  <a name="visual-basic-collection-class"></a>Classe Collection di Visual Basic  
 È possibile utilizzare Visual Basic <xref:Microsoft.VisualBasic.Collection>di accedere a una raccolta di elementi utilizzando entrambi un indice numerico o una classe `String` chiave.</xref:Microsoft.VisualBasic.Collection> Per aggiungere elementi a un oggetto raccolta, è possibile specificare o non specificare una chiave. Se si aggiunge un elemento senza una chiave, è necessario usare il relativo indice numerico per accedervi.  
  
 Visual Basic `Collection` classe archivia tutti i relativi elementi come tipo `Object`, pertanto è possibile aggiungere un elemento di qualsiasi tipo di dati. Non esiste alcuna misura per impedire l'aggiunta di tipi di dati non appropriati.  
  
 Quando si utilizza Visual Basic `Collection` (classe), il primo elemento in una raccolta include un indice di 1. Questo comportamento è diverso rispetto alle classi Collection di .NET Framework, per cui l'indice iniziale è 0.  
  
 Quando possibile, utilizzare le raccolte generiche nel <xref:System.Collections.Generic?displayProperty=fullName>dello spazio dei nomi o <xref:System.Collections.Concurrent>dello spazio dei nomi anziché Visual Basic `Collection` classe</xref:System.Collections.Concurrent> </xref:System.Collections.Generic?displayProperty=fullName>  
  
 Per ulteriori informazioni, vedere <xref:Microsoft.VisualBasic.Collection>.</xref:Microsoft.VisualBasic.Collection>  
  
<a name="BKMK_KeyValuePairs"></a>
## <a name="implementing-a-collection-of-keyvalue-pairs"></a>Implementazione di una raccolta di coppie chiave/valore   
 Il <xref:System.Collections.Generic.Dictionary%602>insieme generico consente di accedere agli elementi in una raccolta utilizzando la chiave di ogni elemento.</xref:System.Collections.Generic.Dictionary%602> Ogni aggiunta al dizionario è costituita da un valore e dalla chiave associata corrispondente. Il recupero di un valore tramite la relativa chiave è veloci perché la `Dictionary` classe viene implementata come una tabella hash.  
  
 Nell'esempio seguente viene creato un `Dictionary` insieme e scorrere il dizionario con un `For Each` istruzione.  
  
```vb  
Private Sub IterateThroughDictionary()  
    Dim elements As Dictionary(Of String, Element) = BuildDictionary()  
  
    For Each kvp As KeyValuePair(Of String, Element) In elements  
        Dim theElement As Element = kvp.Value  
  
        Console.WriteLine("key: " & kvp.Key)  
        With theElement  
            Console.WriteLine("values: " & .Symbol & " " &  
                .Name & " " & .AtomicNumber)  
        End With  
    Next  
End Sub  
  
Private Function BuildDictionary() As Dictionary(Of String, Element)  
    Dim elements As New Dictionary(Of String, Element)  
  
    AddToDictionary(elements, "K", "Potassium", 19)  
    AddToDictionary(elements, "Ca", "Calcium", 20)  
    AddToDictionary(elements, "Sc", "Scandium", 21)  
    AddToDictionary(elements, "Ti", "Titanium", 22)  
  
    Return elements  
End Function  
  
Private Sub AddToDictionary(ByVal elements As Dictionary(Of String, Element),  
ByVal symbol As String, ByVal name As String, ByVal atomicNumber As Integer)  
    Dim theElement As New Element  
  
    theElement.Symbol = symbol  
    theElement.Name = name  
    theElement.AtomicNumber = atomicNumber  
  
    elements.Add(Key:=theElement.Symbol, value:=theElement)  
End Sub  
  
Public Class Element  
    Public Property Symbol As String  
    Public Property Name As String  
    Public Property AtomicNumber As Integer  
End Class  
```  
  
 Utilizzare invece un inizializzatore di raccolta per creare il `Dictionary` raccolta, è possibile sostituire il `BuildDictionary` e `AddToDictionary` metodi con il metodo seguente.  
  
```vb  
Private Function BuildDictionary2() As Dictionary(Of String, Element)  
    Return New Dictionary(Of String, Element) From  
        {  
            {"K", New Element With  
                {.Symbol = "K", .Name = "Potassium", .AtomicNumber = 19}},  
            {"Ca", New Element With  
                {.Symbol = "Ca", .Name = "Calcium", .AtomicNumber = 20}},  
            {"Sc", New Element With  
                {.Symbol = "Sc", .Name = "Scandium", .AtomicNumber = 21}},  
            {"Ti", New Element With  
                {.Symbol = "Ti", .Name = "Titanium", .AtomicNumber = 22}}  
        }  
End Function  
```  
  
 Nell'esempio seguente viene utilizzato il <xref:System.Collections.Generic.Dictionary%602.ContainsKey%2A>(metodo) e <xref:System.Collections.Generic.Dictionary%602.Item%2A>proprietà di `Dictionary` per trovare rapidamente un elemento dalla chiave.</xref:System.Collections.Generic.Dictionary%602.Item%2A> </xref:System.Collections.Generic.Dictionary%602.ContainsKey%2A> Il `Item` proprietà consente di accedere a un elemento di `elements` raccolta utilizzando il `elements(symbol)` codice in Visual Basic.  
  
```vb  
Private Sub FindInDictionary(ByVal symbol As String)  
    Dim elements As Dictionary(Of String, Element) = BuildDictionary()  
  
    If elements.ContainsKey(symbol) = False Then  
        Console.WriteLine(symbol & " not found")  
    Else  
        Dim theElement = elements(symbol)  
        Console.WriteLine("found: " & theElement.Name)  
    End If  
End Sub  
```  
  
 Nell'esempio seguente utilizza invece il <xref:System.Collections.Generic.Dictionary%602.TryGetValue%2A>metodo per trovare rapidamente un elemento chiave.</xref:System.Collections.Generic.Dictionary%602.TryGetValue%2A>  
  
```vb  
Private Sub FindInDictionary2(ByVal symbol As String)  
    Dim elements As Dictionary(Of String, Element) = BuildDictionary()  
  
    Dim theElement As Element = Nothing  
    If elements.TryGetValue(symbol, theElement) = False Then  
        Console.WriteLine(symbol & " not found")  
    Else  
        Console.WriteLine("found: " & theElement.Name)  
    End If  
End Sub  
```  
  
<a name="BKMK_LINQ"></a> 
##  <a name="using-linq-to-access-a-collection"></a>Uso di LINQ per accedere a una raccolta  
 È possibile usare LINQ (Language-Integrated Query) per accedere alle raccolte. Le query LINQ forniscono funzionalità di filtro, ordinamento e raggruppamento. Per ulteriori informazioni, vedere [Introduzione a LINQ in Visual Basic](../../../visual-basic/programming-guide/concepts/linq/getting-started-with-linq.md).  
  
 Nell'esempio seguente esegue una query LINQ rispetto generico `List`. La query LINQ restituisce una raccolta diversa che contiene i risultati.  
  
```vb  
Private Sub ShowLINQ()  
    Dim elements As List(Of Element) = BuildList()  
  
    ' LINQ Query.  
    Dim subset = From theElement In elements  
                  Where theElement.AtomicNumber < 22  
                  Order By theElement.Name  
  
    For Each theElement In subset  
        Console.WriteLine(theElement.Name & " " & theElement.AtomicNumber)  
    Next  
  
    ' Output:  
    '  Calcium 20  
    '  Potassium 19  
    '  Scandium 21  
End Sub  
  
Private Function BuildList() As List(Of Element)  
    Return New List(Of Element) From  
        {  
            {New Element With  
                {.Symbol = "K", .Name = "Potassium", .AtomicNumber = 19}},  
            {New Element With  
                {.Symbol = "Ca", .Name = "Calcium", .AtomicNumber = 20}},  
            {New Element With  
                {.Symbol = "Sc", .Name = "Scandium", .AtomicNumber = 21}},  
            {New Element With  
                {.Symbol = "Ti", .Name = "Titanium", .AtomicNumber = 22}}  
        }  
End Function  
  
Public Class Element  
    Public Property Symbol As String  
    Public Property Name As String  
    Public Property AtomicNumber As Integer  
End Class  
```  
  
 <a name="BKMK_Sorting"></a> 
## <a name="sorting-a-collection"></a>Ordinamento di una raccolta  
 L'esempio seguente illustra una procedura per ordinare una raccolta. Nell'esempio consente di ordinare le istanze di `Car` (classe) che vengono archiviati in un <xref:System.Collections.Generic.List%601>.</xref:System.Collections.Generic.List%601> Il `Car` implementa il <xref:System.IComparable%601>interfaccia, che è necessario che il <xref:System.IComparable%601.CompareTo%2A>metodo essere implementato.</xref:System.IComparable%601.CompareTo%2A> </xref:System.IComparable%601>  
  
 Ogni chiamata al <xref:System.IComparable%601.CompareTo%2A>metodo effettua un confronto singolo che viene utilizzato per l'ordinamento.</xref:System.IComparable%601.CompareTo%2A> Codice scritto dall'utente di `CompareTo` metodo restituisce un valore per ogni confronto dell'oggetto corrente con un altro oggetto. Il valore restituito è minore di zero se l'oggetto corrente è inferiore all'altro oggetto, maggiore di zero se l'oggetto corrente è superiore all'altro oggetto e zero se sono uguali. In questo modo è possibile definire nel codice i criteri di maggiore, minore e uguale.  
  
 Nel `ListCars` (metodo), il `cars.Sort()` istruzione Ordina l'elenco. Questa chiamata al <xref:System.Collections.Generic.List%601.Sort%2A>metodo il <xref:System.Collections.Generic.List%601>fa sì che il `CompareTo` metodo da chiamare automaticamente per il `Car` gli oggetti il `List`.</xref:System.Collections.Generic.List%601> </xref:System.Collections.Generic.List%601.Sort%2A>  
  
```vb  
Public Sub ListCars()  
  
    ' Create some new cars.  
    Dim cars As New List(Of Car) From  
    {  
        New Car With {.Name = "car1", .Color = "blue", .Speed = 20},  
        New Car With {.Name = "car2", .Color = "red", .Speed = 50},  
        New Car With {.Name = "car3", .Color = "green", .Speed = 10},  
        New Car With {.Name = "car4", .Color = "blue", .Speed = 50},  
        New Car With {.Name = "car5", .Color = "blue", .Speed = 30},  
        New Car With {.Name = "car6", .Color = "red", .Speed = 60},  
        New Car With {.Name = "car7", .Color = "green", .Speed = 50}  
    }  
  
    ' Sort the cars by color alphabetically, and then by speed  
    ' in descending order.  
    cars.Sort()  
  
    ' View all of the cars.  
    For Each thisCar As Car In cars  
        Console.Write(thisCar.Color.PadRight(5) & " ")  
        Console.Write(thisCar.Speed.ToString & " ")  
        Console.Write(thisCar.Name)  
        Console.WriteLine()  
    Next  
  
    ' Output:  
    '  blue  50 car4  
    '  blue  30 car5  
    '  blue  20 car1  
    '  green 50 car7  
    '  green 10 car3  
    '  red   60 car6  
    '  red   50 car2  
End Sub  
  
Public Class Car  
    Implements IComparable(Of Car)  
  
    Public Property Name As String  
    Public Property Speed As Integer  
    Public Property Color As String  
  
    Public Function CompareTo(ByVal other As Car) As Integer _  
        Implements System.IComparable(Of Car).CompareTo  
        ' A call to this method makes a single comparison that is  
        ' used for sorting.  
  
        ' Determine the relative order of the objects being compared.  
        ' Sort by color alphabetically, and then by speed in  
        ' descending order.  
  
        ' Compare the colors.  
        Dim compare As Integer  
        compare = String.Compare(Me.Color, other.Color, True)  
  
        ' If the colors are the same, compare the speeds.  
        If compare = 0 Then  
            compare = Me.Speed.CompareTo(other.Speed)  
  
            ' Use descending order for speed.  
            compare = -compare  
        End If  
  
        Return compare  
    End Function  
End Class  
```  
  
<a name="BKMK_CustomCollection"></a> 
## <a name="defining-a-custom-collection"></a>Definizione di una raccolta personalizzata  
 È possibile definire una raccolta mediante l'implementazione di <xref:System.Collections.Generic.IEnumerable%601>o <xref:System.Collections.IEnumerable>interfaccia.</xref:System.Collections.IEnumerable> </xref:System.Collections.Generic.IEnumerable%601> Per ulteriori informazioni, vedere [enumerando una raccolta di](http://msdn.microsoft.com/en-us/71807ea7-9180-48a6-916f-35a5251d477f).  
  
 Sebbene sia possibile definire un insieme personalizzato, è preferibile utilizzare invece le raccolte che vengono inclusi in .NET Framework, che sono descritti in [tipi di raccolte](http://msdn.microsoft.com/library/e76533a9-5033-4a0b-b003-9c2be60d185b) precedentemente in questo argomento.  
  
 Nell'esempio seguente viene definita una classe di raccolta personalizzato denominata `AllColors`. Questa classe implementa il <xref:System.Collections.IEnumerable>interfaccia, che è necessario che il <xref:System.Collections.IEnumerable.GetEnumerator%2A>metodo essere implementato.</xref:System.Collections.IEnumerable.GetEnumerator%2A> </xref:System.Collections.IEnumerable>  
  
 Il `GetEnumerator` metodo restituisce un'istanza di `ColorEnumerator` (classe). `ColorEnumerator`implementa il <xref:System.Collections.IEnumerator>interfaccia, che è necessario che il <xref:System.Collections.IEnumerator.Current%2A>proprietà <xref:System.Collections.IEnumerator.MoveNext%2A>(metodo), e <xref:System.Collections.IEnumerator.Reset%2A>metodo essere implementato.</xref:System.Collections.IEnumerator.Reset%2A> </xref:System.Collections.IEnumerator.MoveNext%2A> </xref:System.Collections.IEnumerator.Current%2A> </xref:System.Collections.IEnumerator>  
  
```vb  
Public Sub ListColors()  
    Dim colors As New AllColors()  
  
    For Each theColor As Color In colors  
        Console.Write(theColor.Name & " ")  
    Next  
    Console.WriteLine()  
    ' Output: red blue green  
End Sub  
  
' Collection class.  
Public Class AllColors  
    Implements System.Collections.IEnumerable  
  
    Private _colors() As Color =  
    {  
        New Color With {.Name = "red"},  
        New Color With {.Name = "blue"},  
        New Color With {.Name = "green"}  
    }  
  
    Public Function GetEnumerator() As System.Collections.IEnumerator _  
        Implements System.Collections.IEnumerable.GetEnumerator  
  
        Return New ColorEnumerator(_colors)  
  
        ' Instead of creating a custom enumerator, you could  
        ' use the GetEnumerator of the array.  
        'Return _colors.GetEnumerator  
    End Function  
  
    ' Custom enumerator.  
    Private Class ColorEnumerator  
        Implements System.Collections.IEnumerator  
  
        Private _colors() As Color  
        Private _position As Integer = -1  
  
        Public Sub New(ByVal colors() As Color)  
            _colors = colors  
        End Sub  
  
        Public ReadOnly Property Current() As Object _  
            Implements System.Collections.IEnumerator.Current  
            Get  
                Return _colors(_position)  
            End Get  
        End Property  
  
        Public Function MoveNext() As Boolean _  
            Implements System.Collections.IEnumerator.MoveNext  
            _position += 1  
            Return (_position < _colors.Length)  
        End Function  
  
        Public Sub Reset() Implements System.Collections.IEnumerator.Reset  
            _position = -1  
        End Sub  
    End Class  
End Class  
  
' Element class.  
Public Class Color  
    Public Property Name As String  
End Class  
```  
  
<a name="BKMK_Iterators"></a>
##  <a name="iterators"></a>Iteratori  
 Un *iteratore* viene utilizzato per eseguire un'iterazione personalizzata su una raccolta. Un iteratore può essere un metodo o un `get` della funzione di accesso. Un iteratore utilizza un [Yield](../../../visual-basic/language-reference/statements/yield-statement.md) istruzione per la restituzione di ogni elemento della raccolta uno alla volta.  
  
 Viene chiamato un iteratore utilizzando un [For Each... Avanti](../../../visual-basic/language-reference/statements/for-each-next-statement.md) istruzione. Ogni iterazione del `For Each` ciclo chiama l'iteratore. Quando un `Yield` viene raggiunta l'istruzione nell'iteratore, viene restituita un'espressione e viene mantenuta la posizione corrente nel codice. L'esecuzione viene ripresa a partire da quella posizione la volta successiva che viene chiamato l'iteratore.  
  
 Per ulteriori informazioni, vedere [iteratori (Visual Basic)](../../../visual-basic/programming-guide/concepts/iterators.md).  
  
 Nell'esempio seguente viene usato un metodo iteratore. Il metodo iteratore è un `Yield` istruzione all'interno di un [per... Avanti](../../../visual-basic/language-reference/statements/for-next-statement.md) ciclo. Nel `ListEvenNumbers` (metodo), ogni iterazione del `For Each` corpo dell'istruzione crea una chiamata al metodo iteratore, che consente di passare alla successiva `Yield` istruzione.  
  
```vb  
Public Sub ListEvenNumbers()  
    For Each number As Integer In EvenSequence(5, 18)  
        Console.Write(number & " ")  
    Next  
    Console.WriteLine()  
    ' Output: 6 8 10 12 14 16 18  
End Sub  
  
Private Iterator Function EvenSequence(  
ByVal firstNumber As Integer, ByVal lastNumber As Integer) _  
As IEnumerable(Of Integer)  
  
' Yield even numbers in the range.  
    For number = firstNumber To lastNumber  
        If number Mod 2 = 0 Then  
            Yield number  
        End If  
    Next  
End Function  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Inizializzatori di insieme](../../../visual-basic/programming-guide/language-features/collection-initializers/index.md)   
 [Concetti di programmazione (Visual Basic)](../../../visual-basic/programming-guide/concepts/index.md)   
 [Istruzione Option Strict](../../../visual-basic/language-reference/statements/option-strict-statement.md)   
 [LINQ to Objects (Visual Basic)](../../../visual-basic/programming-guide/concepts/linq/linq-to-objects.md)   
 [Parallel LINQ (PLINQ)](http://msdn.microsoft.com/library/3d4d0cd3-bde4-490b-99e7-f4e41be96455)   
 [Raccolte e strutture di dati](../../../standard/collections/index.md)   
 [Creazione e modifica delle raccolte](http://msdn.microsoft.com/en-us/2065398e-eb1a-4821-9188-75f16e42e069)   
 [Selezione di una classe di raccolta](../../../standard/collections/selecting-a-collection-class.md)   
 [Confronti e ordinamenti all'interno delle raccolte](../../../standard/collections/comparisons-and-sorts-within-collections.md)   
 [Quando utilizzare raccolte generiche](../../../standard/collections/when-to-use-generic-collections.md)
