---
title: Raccolte (C#) | Microsoft Docs
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: get-started-article
dev_langs:
- CSharp
ms.assetid: 317d7dc3-8587-4873-8b3e-556f86497939
caps.latest.revision: 6
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: Human Translation
ms.sourcegitcommit: fe32676f0e39ed109a68f39584cf41aec5f5ce90
ms.openlocfilehash: 6ce347ec50378590946c756b3adbf64fe855874d
ms.contentlocale: it-it
ms.lasthandoff: 05/10/2017

---
# <a name="collections-c"></a>Raccolte (C#)
Per molte applicazioni è utile creare e gestire gruppi di oggetti correlati. È possibile raggruppare gli oggetti in due modi: creando matrici di oggetti e creando raccolte di oggetti.  
  
 Le matrici sono estremamente utili per la creazione e l'uso di un numero fisso di oggetti fortemente tipizzati. Per altre informazioni sulle matrici, vedere [Matrici](../../../csharp/programming-guide/arrays/index.md).  
  
 Le raccolte consentono di lavorare in modo più flessibile con gruppi di oggetti. A differenza delle matrici, il gruppo di oggetti con cui si lavora può aumentare e diminuire in modo dinamico in base alle esigenze dell'applicazione. Per alcune raccolte è possibile assegnare una chiave a qualsiasi oggetto inserito nella raccolta in modo da recuperare rapidamente l'oggetto usando la chiave.  
  
 Una raccolta è una classe. Di conseguenza, prima di poter aggiungere elementi a una nuova raccolta è necessario dichiarare la raccolta.  
  
 Se la raccolta contiene elementi di un solo tipo di dati, è possibile usare una delle classi dello spazio dei nomi <xref:System.Collections.Generic?displayProperty=fullName>. In una raccolta generica viene imposta l'indipendenza dai tipi, in modo da impedire che vengano aggiunti altri tipi di dati alla raccolta. Quando si recupera un elemento da una raccolta generica, non è necessario determinarne il tipo di dati né convertirlo.  
  
> [!NOTE]
>  Per gli esempi in questo argomento, includere le direttive [using](../../../csharp/language-reference/keywords/using-directive.md) per gli spazi dei nomi `System.Collections.Generic` e `System.Linq`.  
  
 **Contenuto dell'argomento**  
  
-   [Uso di una raccolta semplice](#BKMK_SimpleCollection)  
  
-   [Tipi di raccolte](#BKMK_KindsOfCollections)  
  
    -   [Classi System.Collections.Generic](#BKMK_Generic)  
  
    -   [Classi System.Collections.Concurrent](#BKMK_Concurrent)  
  
    -   [Classi System.Collections](#BKMK_Collections)  
  
-   [Implementazione di una raccolta di coppie chiave/valore](#BKMK_KeyValuePairs)  
  
-   [Uso di LINQ per accedere a una raccolta](#BKMK_LINQ)  
  
-   [Ordinamento di una raccolta](#BKMK_Sorting)  
  
-   [Definizione di una raccolta personalizzata](#BKMK_CustomCollection)  
  
-   [Iteratori](#BKMK_Iterators)  
  
<a name="BKMK_SimpleCollection"></a>
## <a name="using-a-simple-collection"></a>Uso di una raccolta semplice  
 Gli esempi in questa sezione usano la classe generica <xref:System.Collections.Generic.List%601>, che consente di usare un elenco di oggetti fortemente tipizzato.  
  
 L'esempio seguente crea un elenco di stringhe, quindi esegue l'iterazione nelle stringhe usando un'istruzione [foreach](../../../csharp/language-reference/keywords/foreach-in.md).  
  
```csharp  
// Create a list of strings.  
var salmons = new List<string>();  
salmons.Add("chinook");  
salmons.Add("coho");  
salmons.Add("pink");  
salmons.Add("sockeye");  
  
// Iterate through the list.  
foreach (var salmon in salmons)  
{  
    Console.Write(salmon + " ");  
}  
// Output: chinook coho pink sockeye  
```  
  
 Se il contenuto di una raccolta è noto in anticipo, si può usare un *inizializzatore di raccolta* per inizializzare la raccolta. Per altre informazioni, vedere [Inizializzatori di oggetto e di raccolta](../../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md).  
  
 L'esempio seguente è identico all'esempio precedente, ma usa un inizializzatore di raccolta per aggiungere elementi alla raccolta.  
  
```csharp  
// Create a list of strings by using a  
// collection initializer.  
var salmons = new List<string> { "chinook", "coho", "pink", "sockeye" };  
  
// Iterate through the list.  
foreach (var salmon in salmons)  
{  
    Console.Write(salmon + " ");  
}  
// Output: chinook coho pink sockeye  
```  
  
 È possibile usare un'istruzione [for](../../../csharp/language-reference/keywords/for.md) anziché un'istruzione `foreach` per eseguire l'iterazione in una raccolta. Questo è possibile mediante l'accesso agli elementi della raccolta dalla posizione di indice. L'indice degli elementi inizia da 0 e termina in corrispondenza del numero di elementi meno 1.  
  
 Nell'esempio seguente l'iterazione negli elementi di una raccolta avviene mediante `for` anziché mediante `foreach`.  
  
```csharp  
// Create a list of strings by using a  
// collection initializer.  
var salmons = new List<string> { "chinook", "coho", "pink", "sockeye" };  
  
for (var index = 0; index < salmons.Count; index++)  
{  
    Console.Write(salmons[index] + " ");  
}  
// Output: chinook coho pink sockeye  
```  
  
 Nell'esempio seguente viene rimosso un elemento dalla raccolta specificando l'oggetto da rimuovere.  
  
```csharp  
// Create a list of strings by using a  
// collection initializer.  
var salmons = new List<string> { "chinook", "coho", "pink", "sockeye" };  
  
// Remove an element from the list by specifying  
// the object.  
salmons.Remove("coho");  
  
// Iterate through the list.  
foreach (var salmon in salmons)  
{  
    Console.Write(salmon + " ");  
}  
// Output: chinook pink sockeye  
```  
  
 Nell'esempio seguente vengono rimossi elementi da un elenco generico. Invece di un'istruzione `foreach` viene usata un'istruzione [for](../../../csharp/language-reference/keywords/for.md) che esegue l'iterazione in ordine decrescente. Ciò è necessario perché il metodo <xref:System.Collections.Generic.List%601.RemoveAt%2A> fa sì che gli elementi dopo un elemento rimosso abbiano un valore di indice inferiore.  
  
```csharp  
var numbers = new List<int> { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };  
  
// Remove odd numbers.  
for (var index = numbers.Count - 1; index >= 0; index--)  
{  
    if (numbers[index] % 2 == 1)  
    {  
        // Remove the element by specifying  
        // the zero-based index in the list.  
        numbers.RemoveAt(index);  
    }  
}  
  
// Iterate through the list.  
// A lambda expression is placed in the ForEach method  
// of the List(T) object.  
numbers.ForEach(  
    number => Console.Write(number + " "));  
// Output: 0 2 4 6 8  
```  
  
 Per il tipo di elementi in <xref:System.Collections.Generic.List%601>, è possibile anche definire una classe personalizzata. Nell'esempio seguente la classe `Galaxy` viene usata dall'oggetto <xref:System.Collections.Generic.List%601> definito nel codice.  
  
```csharp  
private static void IterateThroughList()  
{  
    var theGalaxies = new List<Galaxy>  
        {  
            new Galaxy() { Name="Tadpole", MegaLightYears=400},  
            new Galaxy() { Name="Pinwheel", MegaLightYears=25},  
            new Galaxy() { Name="Milky Way", MegaLightYears=0},  
            new Galaxy() { Name="Andromeda", MegaLightYears=3}  
        };  
  
    foreach (Galaxy theGalaxy in theGalaxies)  
    {  
        Console.WriteLine(theGalaxy.Name + "  " + theGalaxy.MegaLightYears);  
    }  
  
    // Output:  
    //  Tadpole  400  
    //  Pinwheel  25  
    //  Milky Way  0  
    //  Andromeda  3  
}  
  
public class Galaxy  
{  
    public string Name { get; set; }  
    public int MegaLightYears { get; set; }  
}  
```  

<a name="BKMK_KindsOfCollections"></a>
## <a name="kinds-of-collections"></a>Tipi di raccolte 
 Molte raccolte comuni vengono fornite da .NET Framework. Ogni tipo di raccolta è progettato per uno scopo specifico.  
  
 In questa sezione sono descritte alcune classi di raccolte comuni:  
  
-   Classi @System.Collections.Generic  
  
-   Classi @System.Collections.Concurrent  
  
-   Classi @System.Collections  
  
<a name="BKMK_Generic"></a>
### <a name="systemcollectionsgeneric-classes"></a>Classi System.Collections.Generic  
 È possibile creare una raccolta generica usando una delle classi dello spazio dei nomi <xref:System.Collections.Generic>. Una raccolta generica è utile quando ogni elemento al suo interno presenta lo stesso tipo di dati. Una raccolta generica applica la tipizzazione forte consentendo di aggiungere soltanto i tipi di dati desiderati.  
  
 La tabella seguente elenca alcune delle classi di uso frequente dello spazio dei nomi <xref:System.Collections.Generic?displayProperty=fullName>:  

|Classe|Descrizione| 
|---|---|  
|<xref:System.Collections.Generic.Dictionary%602>|Rappresenta una raccolta di coppie chiave/valore organizzate in base alla chiave.|  
|<xref:System.Collections.Generic.List%601>|Rappresenta un elenco di oggetti accessibile in base all'indice. Fornisce metodi per la ricerca, l'ordinamento e la modifica degli elenchi.|  
|<xref:System.Collections.Generic.Queue%601>|Rappresenta una raccolta di oggetti FIFO (First-In First-Out).|  
|<xref:System.Collections.Generic.SortedList%602>|Rappresenta una raccolta di coppie chiave/valore ordinate per chiave in base all'implementazione <xref:System.Collections.Generic.IComparer%601> associata.|  
|<xref:System.Collections.Generic.Stack%601>|Rappresenta una raccolta di oggetti LIFO (Last-In First-Out).|  
  
 Per altre informazioni, vedere [Tipi di raccolte comunemente utilizzate](../../../standard/collections/commonly-used-collection-types.md), [Selezione di una classe Collection](../../../standard/collections/selecting-a-collection-class.md) e @System.Collections.Generic.  
  
<a name="BKMK_Concurrent"></a>
### <a name="systemcollectionsconcurrent-classes"></a>Classi System.Collections.Concurrent  
 In .NET Framework 4 o versioni successive le raccolte dello spazio dei nomi <xref:System.Collections.Concurrent> garantiscono operazioni thread-safe efficienti per accedere agli elementi della raccolta da più thread.  
  
 Le classi dello spazio dei nomi <xref:System.Collections.Concurrent> devono essere usate in sostituzione dei tipi corrispondenti negli spazi dei nomi <xref:System.Collections.Generic?displayProperty=fullName> e <xref:System.Collections?displayProperty=fullName> ogni volta che più thread accedono contemporaneamente alla raccolta. Per altre informazioni, vedere [Raccolte thread-safe](../../../standard/collections/thread-safe/index.md) e <xref:System.Collections.Concurrent>.  
  
 Alcune classi incluse nello spazio dei nomi <xref:System.Collections.Concurrent> sono <xref:System.Collections.Concurrent.BlockingCollection%601>, <xref:System.Collections.Concurrent.ConcurrentDictionary%602>, <xref:System.Collections.Concurrent.ConcurrentQueue%601> e <xref:System.Collections.Concurrent.ConcurrentStack%601>.  
  
<a name="BKMK_Collections"></a>
### <a name="systemcollections-classes"></a>Classi System.Collections  
 Le classi dello spazio dei nomi <xref:System.Collections?displayProperty=fullName> non archiviano gli elementi come oggetti tipizzati in modo specifico, ma come oggetti di tipo `Object`.  
  
 Quando possibile, usare le raccolte generiche degli spazi dei nomi <xref:System.Collections.Generic?displayProperty=fullName> o <xref:System.Collections.Concurrent> al posto dei tipi legacy dello spazio dei nomi `System.Collections`.  
  
 La tabella seguente elenca alcune classi di uso frequente nello spazio dei nomi `System.Collections`:  
  
|Classe|Descrizione|  
|---|---|  
|<xref:System.Collections.ArrayList>|Rappresenta una matrice di oggetti le cui dimensioni sono incrementate in modo dinamico in base alle esigenze.|  
|<xref:System.Collections.Hashtable>|Rappresenta una raccolta di coppie chiave/valore organizzate in base al codice hash della chiave.|  
|<xref:System.Collections.Queue>|Rappresenta una raccolta di oggetti FIFO (First-In First-Out).|  
|<xref:System.Collections.Stack>|Rappresenta una raccolta di oggetti LIFO (Last-In First-Out).|  
  
 Lo spazio dei nomi <xref:System.Collections.Specialized> offre classi di raccolte fortemente tipizzate e specializzate, ad esempio raccolte di sole stringhe, dizionari ibridi e dizionari a elenchi collegati.  

<a name="BKMK_KeyValuePairs"></a>
## <a name="implementing-a-collection-of-keyvalue-pairs"></a>Implementazione di una raccolta di coppie chiave/valore  
 La raccolta generica <xref:System.Collections.Generic.Dictionary%602> consente di accedere agli elementi di una raccolta usando la chiave di ogni elemento. Ogni aggiunta al dizionario è costituita da un valore e dalla chiave associata corrispondente. Il recupero di un valore tramite la relativa chiave è un'operazione veloce, perché la classe `Dictionary` viene implementata come tabella hash.  
  
 L'esempio seguente crea una raccolta `Dictionary` ed esegue l'iterazione nel dizionario usando un'istruzione `foreach`.  
  
```csharp  
private static void IterateThruDictionary()  
{  
    Dictionary<string, Element> elements = BuildDictionary();  
  
    foreach (KeyValuePair<string, Element> kvp in elements)  
    {  
        Element theElement = kvp.Value;  
  
        Console.WriteLine("key: " + kvp.Key);  
        Console.WriteLine("values: " + theElement.Symbol + " " +  
            theElement.Name + " " + theElement.AtomicNumber);  
    }  
}  
  
private static Dictionary<string, Element> BuildDictionary()  
{  
    var elements = new Dictionary<string, Element>();  
  
    AddToDictionary(elements, "K", "Potassium", 19);  
    AddToDictionary(elements, "Ca", "Calcium", 20);  
    AddToDictionary(elements, "Sc", "Scandium", 21);  
    AddToDictionary(elements, "Ti", "Titanium", 22);  
  
    return elements;  
}  
  
private static void AddToDictionary(Dictionary<string, Element> elements,  
    string symbol, string name, int atomicNumber)  
{  
    Element theElement = new Element();  
  
    theElement.Symbol = symbol;  
    theElement.Name = name;  
    theElement.AtomicNumber = atomicNumber;  
  
    elements.Add(key: theElement.Symbol, value: theElement);  
}  
  
public class Element  
{  
    public string Symbol { get; set; }  
    public string Name { get; set; }  
    public int AtomicNumber { get; set; }  
}  
```  
  
 Per usare invece un inizializzatore di raccolta per compilare la raccolta `Dictionary`, è possibile sostituire i metodi `BuildDictionary` e `AddToDictionary` con il metodo seguente.  
  
```csharp  
private static Dictionary<string, Element> BuildDictionary2()  
{  
    return new Dictionary<string, Element>  
    {  
        {"K",  
            new Element() { Symbol="K", Name="Potassium", AtomicNumber=19}},  
        {"Ca",  
            new Element() { Symbol="Ca", Name="Calcium", AtomicNumber=20}},  
        {"Sc",  
            new Element() { Symbol="Sc", Name="Scandium", AtomicNumber=21}},  
        {"Ti",  
            new Element() { Symbol="Ti", Name="Titanium", AtomicNumber=22}}  
    };  
}  
```  
  
 L'esempio seguente usa il metodo <xref:System.Collections.Generic.Dictionary%602.ContainsKey%2A> e la proprietà <xref:System.Collections.Generic.Dictionary%602.Item%2A> di `Dictionary` per trovare rapidamente un elemento in base alla chiave. La proprietà `Item` consente di accedere a un elemento nella raccolta `elements` usando il codice `elements[symbol]` in C#.  
  
```csharp  
private static void FindInDictionary(string symbol)  
{  
    Dictionary<string, Element> elements = BuildDictionary();  
  
    if (elements.ContainsKey(symbol) == false)  
    {  
        Console.WriteLine(symbol + " not found");  
    }  
    else  
    {  
        Element theElement = elements[symbol];  
        Console.WriteLine("found: " + theElement.Name);  
    }  
}  
```  
  
 L'esempio seguente usa invece il metodo <xref:System.Collections.Generic.Dictionary%602.TryGetValue%2A> per individuare rapidamente un elemento in base alla chiave.  
  
```csharp  
private static void FindInDictionary2(string symbol)  
{  
    Dictionary<string, Element> elements = BuildDictionary();  
  
    Element theElement = null;  
    if (elements.TryGetValue(symbol, out theElement) == false)  
        Console.WriteLine(symbol + " not found");  
    else  
        Console.WriteLine("found: " + theElement.Name);  
}  
```  

<a name="BKMK_LINQ"></a>
## <a name="using-linq-to-access-a-collection"></a>Uso di LINQ per accedere a una raccolta  
 È possibile usare LINQ (Language-Integrated Query) per accedere alle raccolte. Le query LINQ forniscono funzionalità di filtro, ordinamento e raggruppamento. Per altre informazioni, vedere [Introduzione a LINQ in C#](../../../csharp/programming-guide/concepts/linq/getting-started-with-linq.md).  
  
 Nell'esempio seguente viene eseguita una query LINQ su un oggetto `List` generico. La query LINQ restituisce una raccolta diversa che contiene i risultati.  
  
```csharp  
private static void ShowLINQ()  
{  
    List<Element> elements = BuildList();  
  
    // LINQ Query.  
    var subset = from theElement in elements  
                 where theElement.AtomicNumber < 22  
                 orderby theElement.Name  
                 select theElement;  
  
    foreach (Element theElement in subset)  
    {  
        Console.WriteLine(theElement.Name + " " + theElement.AtomicNumber);  
    }  
  
    // Output:  
    //  Calcium 20  
    //  Potassium 19  
    //  Scandium 21  
}  
  
private static List<Element> BuildList()  
{  
    return new List<Element>  
    {  
        { new Element() { Symbol="K", Name="Potassium", AtomicNumber=19}},  
        { new Element() { Symbol="Ca", Name="Calcium", AtomicNumber=20}},  
        { new Element() { Symbol="Sc", Name="Scandium", AtomicNumber=21}},  
        { new Element() { Symbol="Ti", Name="Titanium", AtomicNumber=22}}  
    };  
}  
  
public class Element  
{  
    public string Symbol { get; set; }  
    public string Name { get; set; }  
    public int AtomicNumber { get; set; }  
}  
```  

<a name="BKMK_Sorting"></a>
## <a name="sorting-a-collection"></a>Ordinamento di una raccolta  
 L'esempio seguente illustra una procedura per ordinare una raccolta. Nell'esempio vengono ordinate le istanze della classe `Car` archiviate in un oggetto <xref:System.Collections.Generic.List%601>. La classe `Car` implementa l'interfaccia <xref:System.IComparable%601>, che richiede l'implementazione del metodo <xref:System.IComparable%601.CompareTo%2A>.  
  
 Ogni chiamata al metodo <xref:System.IComparable%601.CompareTo%2A> effettua un confronto unico che viene usato per l'ordinamento. Il codice scritto dall'utente presente nel metodo `CompareTo` restituisce un valore per ogni confronto dell'oggetto corrente con un altro oggetto. Il valore restituito è minore di zero se l'oggetto corrente è inferiore all'altro oggetto, maggiore di zero se l'oggetto corrente è superiore all'altro oggetto e zero se sono uguali. In questo modo è possibile definire nel codice i criteri di maggiore, minore e uguale.  
  
 Nel metodo `ListCars` l'istruzione `cars.Sort()` ordina l'elenco. Questa chiamata al metodo <xref:System.Collections.Generic.List%601.Sort%2A> di <xref:System.Collections.Generic.List%601> determina la chiamata automatica al metodo `CompareTo` per gli oggetti `Car` in `List`.  
  
```csharp  
private static void ListCars()  
{  
    var cars = new List<Car>  
    {  
        { new Car() { Name = "car1", Color = "blue", Speed = 20}},  
        { new Car() { Name = "car2", Color = "red", Speed = 50}},  
        { new Car() { Name = "car3", Color = "green", Speed = 10}},  
        { new Car() { Name = "car4", Color = "blue", Speed = 50}},  
        { new Car() { Name = "car5", Color = "blue", Speed = 30}},  
        { new Car() { Name = "car6", Color = "red", Speed = 60}},  
        { new Car() { Name = "car7", Color = "green", Speed = 50}}  
    };  
  
    // Sort the cars by color alphabetically, and then by speed  
    // in descending order.  
    cars.Sort();  
  
    // View all of the cars.  
    foreach (Car thisCar in cars)  
    {  
        Console.Write(thisCar.Color.PadRight(5) + " ");  
        Console.Write(thisCar.Speed.ToString() + " ");  
        Console.Write(thisCar.Name);  
        Console.WriteLine();  
    }  
  
    // Output:  
    //  blue  50 car4  
    //  blue  30 car5  
    //  blue  20 car1  
    //  green 50 car7  
    //  green 10 car3  
    //  red   60 car6  
    //  red   50 car2  
}  
  
public class Car : IComparable<Car>  
{  
    public string Name { get; set; }  
    public int Speed { get; set; }  
    public string Color { get; set; }  
  
    public int CompareTo(Car other)  
    {  
        // A call to this method makes a single comparison that is  
        // used for sorting.  
  
        // Determine the relative order of the objects being compared.  
        // Sort by color alphabetically, and then by speed in  
        // descending order.  
  
        // Compare the colors.  
        int compare;  
        compare = String.Compare(this.Color, other.Color, true);  
  
        // If the colors are the same, compare the speeds.  
        if (compare == 0)  
        {  
            compare = this.Speed.CompareTo(other.Speed);  
  
            // Use descending order for speed.  
            compare = -compare;  
        }  
  
        return compare;  
    }  
}  
```  
  
<a name="BKMK_CustomCollection"></a>
## <a name="defining-a-custom-collection"></a>Definizione di una raccolta personalizzata  
 È possibile definire una raccolta implementando l'interfaccia <xref:System.Collections.Generic.IEnumerable%601> o <xref:System.Collections.IEnumerable>. Per altre informazioni, vedere [Procedura: Accedere a una classe di raccolte con foreach](../../../csharp/programming-guide/classes-and-structs/how-to-access-a-collection-class-with-foreach.md).  
  
 Sebbene sia possibile definire una raccolta personalizzata, in genere è preferibile usare le raccolte incluse in .NET Framework, descritte in [Tipi di raccolte](#BKMK_KindsOfCollections) in precedenza in questo argomento.  
  
 L'esempio seguente definisce una classe di raccolte personalizzata denominata `AllColors`. Questa classe implementa l'interfaccia <xref:System.Collections.IEnumerable> che richiede l'implementazione del metodo <xref:System.Collections.IEnumerable.GetEnumerator%2A>.  
  
 Il metodo `GetEnumerator` restituisce un'istanza della classe `ColorEnumerator`. `ColorEnumerator` implementa l'interfaccia <xref:System.Collections.IEnumerator> che richiede l'implementazione della proprietà <xref:System.Collections.IEnumerator.Current%2A> e dei metodi <xref:System.Collections.IEnumerator.MoveNext%2A> e <xref:System.Collections.IEnumerator.Reset%2A>.  
  
```csharp  
private static void ListColors()  
{  
    var colors = new AllColors();  
  
    foreach (Color theColor in colors)  
    {  
        Console.Write(theColor.Name + " ");  
    }  
    Console.WriteLine();  
    // Output: red blue green  
}  
  
// Collection class.  
public class AllColors : System.Collections.IEnumerable  
{  
    Color[] _colors =  
    {  
        new Color() { Name = "red" },  
        new Color() { Name = "blue" },  
        new Color() { Name = "green" }  
    };  
  
    public System.Collections.IEnumerator GetEnumerator()  
    {  
        return new ColorEnumerator(_colors);  
  
        // Instead of creating a custom enumerator, you could  
        // use the GetEnumerator of the array.  
        //return _colors.GetEnumerator();  
    }  
  
    // Custom enumerator.  
    private class ColorEnumerator : System.Collections.IEnumerator  
    {  
        private Color[] _colors;  
        private int _position = -1;  
  
        public ColorEnumerator(Color[] colors)  
        {  
            _colors = colors;  
        }  
  
        object System.Collections.IEnumerator.Current  
        {  
            get  
            {  
                return _colors[_position];  
            }  
        }  
  
        bool System.Collections.IEnumerator.MoveNext()  
        {  
            _position++;  
            return (_position < _colors.Length);  
        }  
  
        void System.Collections.IEnumerator.Reset()  
        {  
            _position = -1;  
        }  
    }  
}  
  
// Element class.  
public class Color  
{  
    public string Name { get; set; }  
}  
```  

<a name="BKMK_Iterators"></a> 
##  <a name="iterators"></a>Iteratori  
 Un *iteratore* viene usato per eseguire un'iterazione personalizzata in una raccolta. Un iteratore può essere un metodo o una funzione di accesso `get`. Un iteratore usa un'istruzione [yield return](../../../csharp/language-reference/keywords/yield.md) per restituire ogni elemento della raccolta, uno alla volta.  
  
 Per chiamare un iteratore usare un'istruzione [foreach](../../../csharp/language-reference/keywords/foreach-in.md). Ogni iterazione del ciclo `foreach` chiama l'iteratore. Quando si raggiunge un'istruzione `yield return` nell'iteratore, viene restituita un'espressione e viene mantenuta la posizione corrente nel codice. L'esecuzione viene ripresa a partire da quella posizione la volta successiva che viene chiamato l'iteratore.  
  
 Per altre informazioni, vedere [Iteratori (C#)](../../../csharp/programming-guide/concepts/iterators.md).  
  
 Nell'esempio seguente viene usato un metodo iteratore. Il metodo iteratore dispone di un'istruzione `yield return` all'interno di un ciclo [for](../../../csharp/language-reference/keywords/for.md). Nel metodo `ListEvenNumbers` ogni iterazione del corpo dell'istruzione `foreach` crea una chiamata al metodo iteratore, che procede all'istruzione `yield return` successiva.  
  
```csharp  
private static void ListEvenNumbers()  
{  
    foreach (int number in EvenSequence(5, 18))  
    {  
        Console.Write(number.ToString() + " ");  
    }  
    Console.WriteLine();  
    // Output: 6 8 10 12 14 16 18  
}  
  
private static IEnumerable<int> EvenSequence(  
    int firstNumber, int lastNumber)  
{  
    // Yield even numbers in the range.  
    for (var number = firstNumber; number <= lastNumber; number++)  
    {  
        if (number % 2 == 0)  
        {  
            yield return number;  
        }  
    }  
}  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Inizializzatori di oggetto e di raccolta](../../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md)   
 [Nozioni di base sulla programmazione (C#)](../../../csharp/programming-guide/concepts/index.md)   
 [Istruzione Option Strict](../../../visual-basic/language-reference/statements/option-strict-statement.md)   
 [LINQ to Objects (C#)](../../../csharp/programming-guide/concepts/linq/linq-to-objects.md)   
 [Parallel LINQ (PLINQ)](../../../standard/parallel-programming/parallel-linq-plinq.md)   
 [Raccolte e strutture di dati](../../../standard/collections/index.md)   
 [Creazione e modifica delle raccolte](http://msdn.microsoft.com/en-us/2065398e-eb1a-4821-9188-75f16e42e069)   
 [Selezione di una classe Collection](../../../standard/collections/selecting-a-collection-class.md)   
 [Confronti e ordinamenti all'interno delle raccolte](../../../standard/collections/comparisons-and-sorts-within-collections.md)   
 [Quando usare raccolte generiche](../../../standard/collections/when-to-use-generic-collections.md)   
 [Procedura: Accedere a una classe Collection con foreach](../../../csharp/programming-guide/classes-and-structs/how-to-access-a-collection-class-with-foreach.md)

