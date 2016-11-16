---
title: Common Type System in dettaglio
description: Common Type System in dettaglio
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
manager: wpickett
ms.date: 07/20/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: b5482a1d-7bdc-40fe-aa45-10df930ceb5b
translationtype: Human Translation
ms.sourcegitcommit: b20713600d7c3ddc31be5885733a1e8910ede8c6
ms.openlocfilehash: 7d7f869b07d7cf00ffa69da117aa199d1b6e8f20

---

# <a name="common-type-system-in-depth"></a>Common Type System in dettaglio

Questo argomento contiene le sezioni seguenti che illustrano Common Type System in dettaglio:

* [Tipi in .NET](#types-in-net)

* [Definizioni dei tipi](#type-definitions)

* [Membri dei tipi](#type-members)

* [Caratteristiche dei membri dei tipi](#characteristics-of-type-members)


## <a name="types-in-net"></a>Tipi in .NET

Tutti i tipi in .NET sono tipi valore o tipi riferimento. 

I tipi di valore sono tipi di dati i cui oggetti sono rappresentati dal valore effettivo dell'oggetto. Se un'istanza di un tipo di valore viene assegnata a una variabile, a tale variabile viene fornita una copia aggiornata del valore.

I tipi di riferimento sono tipi di dati i cui oggetti sono rappresentati da un riferimento (simile a un puntatore) al valore effettivo dell'oggetto. Se un tipo di riferimento viene assegnato a una variabile, tale variabile fa riferimento (punta) al valore originale. Non viene effettuata alcuna copia. 

Common Type System in .NET supporta le cinque categorie di tipi seguenti:

* [Classi](#classes)

* [Strutture](#structures)

* [Enumerazioni](#enumerations)

* [Interfacce](#interfaces)

* [Delegati](#delegates)

### <a name="classes"></a>Classi

Una classe è un tipo riferimento che è possibile derivare direttamente da un'altra classe e che viene derivato in modo implicito da [System.Object](xref:System.Object). La classe definisce le operazioni che un oggetto (un'istanza della classe) può eseguire (metodi, eventi o proprietà) e i dati che l'oggetto contiene (campi). Sebbene una classe includa in genere sia la definizione che l'implementazione, a differenza delle interfacce che contengono, ad esempio, solo la definizione senza l'implementazione, può contenere uno o più membri privi di implementazione.

Nella tabella seguente vengono descritte alcune delle caratteristiche che una classe può avere. Ogni linguaggio che supporta il runtime fornisce un modo per indicare che una classe o membro di classe dispone di una o più di queste caratteristiche. È tuttavia possibile che i singoli linguaggi di programmazione destinati a .NET non rendano disponibili tutte queste caratteristiche.

Caratteristica | Descrizione
-------------- | -----------
sealed | Specifica che da questo tipo non è possibile derivare un'altra classe.
implementa | Indica che la classe utilizza una o più interfacce fornendo implementazioni dei membri di interfaccia.
abstract | Indica che non è possibile creare un'istanza della classe. Per utilizzarla è necessario derivare da essa un'altra classe.
eredita | Indica che le istanze della classe possono essere utilizzate ovunque la classe sia specificata. Una classe derivata che eredita da una classe di base può utilizzare l'implementazione di qualsiasi membro pubblico fornito dalla classe di base oppure la classe derivata può eseguire l'override dell'implementazione dei membri pubblici con la propria implementazione.
exported o not exported | Indica se una classe è visibile all'esterno dell'assembly in cui è definita. Questa caratteristica è applicabile unicamente alle classi di primo livello e non alle classi annidate.

> [!NOTE]
> Una classe può anche essere annidata in una struttura o una classe padre. Anche le classi annidate possiedono le caratteristiche dei membri. Per altre informazioni, vedere [Tipi annidati](#nested-types).

I membri di classe privi di implementazione sono membri astratti. Una classe con uno o più membri astratti è essa stessa astratta e non è possibile crearne nuove istanze. Con alcuni linguaggi destinati al runtime è possibile contrassegnare una classe come astratta anche se nessuno dei relativi membri è astratto. È possibile utilizzare una classe astratta quando si desidera incapsulare un set di base di funzionalità che le classi derivate possono ereditare oppure sottoporre a override nelle circostanze appropriate. Alle classi che non sono astratte viene fatto riferimento come a classi concrete.

Una classe può implementare un numero qualsiasi di interfacce, ma può ereditare solo da una classe di base, oltre che da [System.Object](xref:System.Object), da cui tutte le classi ereditano in modo implicito. Tutte le classi devono avere almeno un costruttore, per l'inizializzazione di nuove istanze della classe. Se non si definisce in modo esplicito un costruttore, la maggior parte dei compilatori fornisce automaticamente un costruttore predefinito (senza parametri).

### <a name="structures"></a>Strutture

Una struttura è un tipo valore che deriva in modo implicito da [System.ValueType](xref:System.ValueType), che a sua volta deriva da [System.Object](xref:System.Object). Una struttura è molto utile per la rappresentazione di valori con requisiti di memoria piccoli e per passare valori come parametri per valori a metodi che dispongono di parametri fortemente tipizzati. In .NET tutti i tipi di dati primitivi ([Boolean](xref:System.Boolean), [Byte](xref:System.Byte), [Char](xref:System.Char), [DateTime](xref:System.DateTime), [Decimal](xref:System.Decimal), [Double](xref:System.Double), [Int16](xref:System.Int16), [Int32](xref:System.Int32), [Int64](xref:System.Int64), [SByte](xref:System.SByte), [Single](xref:System.Single), [UInt16](xref:System.UInt16), [UInt32](xref:System.UInt32), e [UInt64](xref:System.UInt64)) sono definiti come strutture.

Analogamente alle classi, le strutture definiscono sia i dati (i campi della struttura) che le operazioni che è possibile eseguire s tali dati (i metodi della struttura). Ciò significa che è possibile chiamare metodi nelle strutture, inclusi i metodi virtuali definiti nelle classi [System.Object](xref:System.Object) e [System.ValueType](xref:System.ValueType) e qualsiasi metodo definito nel tipo valore stesso. In altre parole, le strutture possono disporre di campi, proprietà ed eventi, nonché di metodi statici e non statici. È possibile creare istanze di strutture, passarle come parametri, archiviarle come variabili locali oppure in un campo di un altro tipo di valore o tipo di riferimento. Le strutture possono inoltre implementare interfacce.

I tipi di valore differiscono dalle classi per diversi motivi. Per prima cosa, anche se ereditano in modo implicito da [System.ValueType](xref:System.ValueType), non possono ereditare direttamente da alcun tipo. Analogamente, tutti i tipi di valore sono sealed, ovvero nessun altro tipo può essere derivato da essi. Non richiedono inoltre costruttori.

Per ogni tipo di valore, Common Language Runtime fornisce un tipo sottoposto a boxing corrispondente, ovvero una classe avente lo stesso stato e lo stesso comportamento del tipo di valore. Un'istanza di un tipo valore viene sottoposta a boxing quando viene passata a un metodo che accetta un parametro di tipo [System.Object](xref:System.Object). La conversione unboxing, ovvero la conversione da un'istanza di una classe di nuovo in un'istanza di un tipo di valore, viene eseguita quando il controllo viene restituito da una chiamata al metodo che accetta un tipo di valore come parametro per riferimento. In alcuni linguaggi è richiesto l'utilizzo di una sintassi speciale quando il tipo sottoposto a boxing è obbligatorio, mentre in altri il tipo sottoposto a boxing viene utilizzato automaticamente quando è necessario. Quando si definisce un tipo di valore si sta definendo sia il tipo boxed che il tipo unboxed.

### <a name="enumerations"></a>Enumerazioni

Un'enumerazione (enum) è un tipo valore che eredita direttamente da [System.Enum](xref:System.Enum) e che specifica nomi alternativi per i valori di un tipo primitivo sottostante. Un tipo enumerazione ha un nome, un tipo sottostante che deve essere uno dei tipi intero con o senza segno predefinito, come ad esempio [Byte](xref:System.Byte), [Int32](xref:System.Int32), o [UInt64](xref:System.UInt64), e un set di campi. I campi sono campi letterali statici, ognuno dei quali rappresenta una costante. Lo stesso valore può essere assegnato a più campi. In questo caso, è necessario contrassegnare uno dei valori come valore di enumerazione primario a scopo di reflection e conversione di stringhe.

È possibile assegnare a un'enumerazione un valore del tipo sottostante e viceversa. Nel runtime non è richiesto alcun cast. È possibile creare un'istanza di un'enumerazione e chiamare i metodi di [System.Enum](xref:System.Enum), nonché qualsiasi metodo definito nel tipo sottostante dell'enumerazione. In alcuni linguaggi, tuttavia, potrebbe non essere possibile passare un'enumerazione come parametro quando un'istanza del tipo sottostante è obbligatoria (o viceversa).

Alle enumerazioni si applicano le seguenti ulteriori restrizioni: 

* La definizione dei metodi non può essere eseguita direttamente dall'enumerazione.

* Con un'enumerazione non è possibile implementare un'interfaccia.

* Con un'enumerazione non è possibile definire proprietà o eventi.

* Le enumerazioni non possono essere generiche, a meno che non siano generiche solo perché annidate all'interno di un tipo generico. In altre parole, un'enumerazione non può disporre di parametri di tipo propri. 

> [!NOTE]
> I tipi annidati, incluse le enumerazioni, creati con C# comprendono i parametri di tipo di tutti i tipi generici che li comprendono e sono pertanto generici anche se non hanno parametri di tipo propri. Per altre informazioni, vedere l'argomento di riferimento [Type.MakeGenericType](xref:System.Type.MakeGenericType(System.Type[])). 

L'attributo [FlagsAttribute](xref:System.FlagsAttribute) denota un tipo speciale di enumerazione definito campo di bit. Nel runtime non viene fatta distinzione tra enumerazioni tradizionali e campi di bit, ma è possibile che tale distinzione esista nel linguaggio utilizzato. Quando tale distinzione viene effettuata, gli operatori bit per bit possono essere utilizzati sui campi di bit, ma non sulle enumerazioni, per generare valori non denominati. Le enumerazioni sono in genere utilizzate per elenchi di elementi univoci, come giorni della settimana o nomi di paesi o province. I campi di bit sono normalmente utilizzati per elenchi di qualità o quantità che possono ricorrere in combinazioni, come `Red And Big And Fast`.

Nell'esempio che segue viene illustrato come utilizzare sia i campi di bit, sia le enumerazioni tradizionali.

```csharp
using System;
using System.Collections.Generic;

// A traditional enumeration of some root vegetables.
public enum SomeRootVegetables
{
    HorseRadish,
    Radish,
    Turnip
}

// A bit field or flag enumeration of harvesting seasons.
[Flags]
public enum Seasons
{
    None = 0,
    Summer = 1,
    Autumn = 2,
    Winter = 4,
    Spring = 8,
    All = Summer | Autumn | Winter | Spring
}

public class Example
{
   public static void Main()
   {
       // Hash table of when vegetables are available.
       Dictionary<SomeRootVegetables, Seasons> AvailableIn = new Dictionary<SomeRootVegetables, Seasons>();

       AvailableIn[SomeRootVegetables.HorseRadish] = Seasons.All;
       AvailableIn[SomeRootVegetables.Radish] = Seasons.Spring;
       AvailableIn[SomeRootVegetables.Turnip] = Seasons.Spring | 
            Seasons.Autumn;

       // Array of the seasons, using the enumeration.
       Seasons[] theSeasons = new Seasons[] { Seasons.Summer, Seasons.Autumn, 
            Seasons.Winter, Seasons.Spring };

       // Print information of what vegetables are available each season.
       foreach (Seasons season in theSeasons)
       {
          Console.Write(String.Format(
              "The following root vegetables are harvested in {0}:\n", 
              season.ToString("G")));
          foreach (KeyValuePair<SomeRootVegetables, Seasons> item in AvailableIn)
          {
             // A bitwise comparison.
             if (((Seasons)item.Value & season) > 0)
                 Console.Write(String.Format("  {0:G}\n", 
                      (SomeRootVegetables)item.Key));
          }
       }
   }
}
// The example displays the following output:
//    The following root vegetables are harvested in Summer:
//      HorseRadish
//    The following root vegetables are harvested in Autumn:
//      Turnip
//      HorseRadish
//    The following root vegetables are harvested in Winter:
//      HorseRadish
//    The following root vegetables are harvested in Spring:
//      Turnip
//      Radish
//      HorseRadish
```

```vb
Imports System.Collections.Generic

' A traditional enumeration of some root vegetables.
Public Enum SomeRootVegetables
   HorseRadish
   Radish
   Turnip
End Enum 

' A bit field or flag enumeration of harvesting seasons.
<Flags()> Public Enum Seasons
   None = 0
   Summer = 1
   Autumn = 2
   Winter = 4
   Spring = 8
   All = Summer Or Autumn Or Winter Or Spring
End Enum 

' Entry point.
Public Class Example
   Public Shared Sub Main()
      ' Hash table of when vegetables are available.
      Dim AvailableIn As New Dictionary(Of SomeRootVegetables, Seasons)()

      AvailableIn(SomeRootVegetables.HorseRadish) = Seasons.All
      AvailableIn(SomeRootVegetables.Radish) = Seasons.Spring
      AvailableIn(SomeRootVegetables.Turnip) = Seasons.Spring Or _
                                               Seasons.Autumn

      ' Array of the seasons, using the enumeration.
      Dim theSeasons() As Seasons = {Seasons.Summer, Seasons.Autumn, _
                                     Seasons.Winter, Seasons.Spring}

      ' Print information of what vegetables are available each season.
      For Each season As Seasons In theSeasons
         Console.WriteLine(String.Format( _
              "The following root vegetables are harvested in {0}:", _
              season.ToString("G")))
         For Each item As KeyValuePair(Of SomeRootVegetables, Seasons) In AvailableIn
            ' A bitwise comparison.
            If(CType(item.Value, Seasons) And season) > 0 Then
               Console.WriteLine("  " + _
                     CType(item.Key, SomeRootVegetables).ToString("G"))
            End If
         Next
      Next
   End Sub 
End Class 
' The example displays the following output:
'    The following root vegetables are harvested in Summer:
'      HorseRadish
'    The following root vegetables are harvested in Autumn:
'      Turnip
'      HorseRadish
'    The following root vegetables are harvested in Winter:
'      HorseRadish
'    The following root vegetables are harvested in Spring:
'      Turnip
'      Radish
'      HorseRadish
```

### <a name="interfaces"></a>Interfacce

Un'interfaccia definisce un contratto che specifica una relazione di tipo "può" o una relazione di tipo "ha". Le interfacce vengono spesso usate per implementare funzionalità, ad esempio il confronto e l'ordinamento (interfacce [IComparable](xref:System.IComparable) e [IComparable&lt;T&gt;](xref:System.IComparable%601)), il test di uguaglianza (interfaccia [IEquatable&lt;T&gt;](xref:System.IEquatable%601)) o l'enumerazione di elementi in una raccolta (interfacce [IEnumerable](xref:System.Collections.IEnumerable) e [IEnumerable&lt;T&gt;](xref:System.Collections.Generic.IEnumerable%601)). Le interfacce possono disporre di proprietà, metodi ed eventi, ovvero tutti membri astratti. Per questo motivo, anche se l'interfaccia definisce i membri e le relative firme, il compito di definire le funzionalità di ogni membro dell'interfaccia viene lasciato al tipo che la implementa. Ciò significa che qualsiasi classe o struttura che implementa un'interfaccia deve fornire le definizioni per i membri astratti dichiarati nell'interfaccia. Un'interfaccia può richiedere che qualsiasi classe o struttura che la implementa implementi anche una o più altre interfacce.

Alle interfacce si applicano le seguenti restrizioni: 

* Un'interfaccia può essere dichiarata con qualsiasi accessibilità ma i membri di interfaccia devono tutti avere accessibilità pubblica.

* Con un'interfaccia non è possibile definire costruttori.

* Le interfacce non possono definire campi.

* Le interfacce possono definire solo membri di istanza. Non possono definire membri statici.

Ogni linguaggio deve fornire regole per il mapping di un'implementazione all'interfaccia che richiede il membro, in quanto più interfacce possono dichiarare un membro con la stessa firma e i membri possono disporre di implementazioni separate.

### <a name="delegates"></a>Delegati

I delegati sono tipi di riferimento che assolvono a una funzione simile a quella dei puntatori a funzione in C++. Vengono usati per i gestori di eventi e le funzioni di callback in .NET. Diversamente dai puntatori a funzione, i delegati sono sicuri, verificabili e indipendenti dai tipi. Un tipo delegato può rappresentare qualsiasi metodo di istanza o metodo statico con una firma compatibile. 

Un parametro di un delegato è compatibile con il parametro di un metodo corrispondente se il tipo del parametro del delegato è più restrittivo rispetto al tipo del parametro del metodo. In questo modo si garantisce che un argomento passato al delegato possa essere passato in modo sicuro al metodo.

Analogamente, il tipo restituito di un delegato è compatibile con il tipo restituito di un metodo se il tipo restituito del metodo è più restrittivo rispetto al tipo restituito del delegato. In questo modo si garantisce la possibilità di eseguire in modo sicuro il cast del valore restituito del metodo nel tipo restituito del delegato.

Un delegato con un parametro di tipo [IEnumerable](xref:System.Collections.IEnumerable) e un tipo restituito di tipo [Object](xref:System.Object) può, ad esempio, rappresentare un metodo con un parametro di tipo [Object](xref:System.Object) e un valore restituito di tipo [IEnumerable](xref:System.Collections.IEnumerable). 

 Un delegato è associato al metodo che rappresenta. Oltre a essere associato al metodo, un delegato può essere associato a un oggetto. L'oggetto rappresenta il primo parametro del metodo e viene passato al metodo ogni volta che viene richiamato il delegato. Se il metodo è un metodo di istanza, l'oggetto associato viene passato come parametro `this` implicito (`Me` in Visual Basic). Se il metodo è statico, l'oggetto viene passato come primo parametro formale del metodo e la firma del delegato deve corrispondere ai parametri rimanenti. 
 
 Tutti i delegati ereditano da [System.MulticastDelegate](xref:System.MulticastDelegate), che eredita da [System.Delegate](xref:System.Delegate). I linguaggi C# e Visual Basic non consentono l'ereditarietà da questi tipi. Forniscono invece parole chiave per la dichiarazione di delegati.
 
 Dal momento che i delegati ereditano da [MulticastDelegate](xref:System.MulticastDelegate), hanno un elenco di chiamate, ovvero un elenco di metodi rappresentati dal delegato che vengono eseguiti quando il delegato viene chiamato. Tutti i metodi dell'elenco ricevono gli argomenti forniti quando viene chiamato il delegato.

> [!NOTE]
> Il valore restituito non è definito per un delegato il cui elenco chiamate contiene più metodi, anche se il delegato dispone di un tipo restituito.

In molti casi, ad esempio con i metodi di callback, un delegato rappresenta un solo metodo e le uniche azioni che è necessario eseguire sono la creazione e il richiamo del delegato. 

Per i delegati che rappresentano più metodi, .NET specifica metodi delle classi di delegati [Delegate](xref:System.Delegate) e [MulticastDelegate](xref:System.MulticastDelegate) per supportare operazioni quali l'aggiunta di un metodo a un elenco di chiamate di un delegato (il metodo [Delegate.Combine](xref:System.Delegate.Combine(System.Delegate,System.Delegate))), la rimozione di un metodo (il metodo [Delegate.Remove](xref:System.Delegate.Remove(System.Delegate,System.Delegate))) e il recupero dell'elenco di chiamate (il metodo [Delegate.GetInvocationList](xref:System.Delegate.GetInvocationList)).

> [!NOTE]
> Non è necessario usare questi metodi per i delegati dei gestori di eventi nei linguaggi C# o Visual Basic perché questi linguaggi specificano la sintassi per l'aggiunta e la rimozione dei gestori di eventi.

## <a name="type-definitions"></a>Definizioni di tipo

Una definizione di tipo include gli elementi seguenti: 

* Gli eventuali attributi definiti per il tipo.

* Accessibilità del tipo (visibilità)

* Il nome del tipo.

* Il tipo base del tipo.

* Le interfacce eventualmente implementate dal tipo.

* Le definizioni per ciascuno dei membri del tipo.

### <a name="attributes"></a>Attributi

Gli attributi forniscono metadati aggiuntivi definiti dall'utente. Comunemente vengono utilizzati per archiviare informazioni aggiuntive su un tipo nell'assembly o per modificare il comportamento di un membro del tipo nella fase di progettazione o nell'ambiente di runtime. 

Gli attributi stessi sono classi che ereditano da [System.Attribute](xref:System.Attribute). I linguaggi che supportano l'utilizzo di attributi forniscono ognuno la sintassi necessaria per l'applicazione degli attributi a un elemento del linguaggio. Gli attributi possono essere applicati a quasi tutti gli elementi del linguaggio. Gli elementi specifici a cui è possibile applicare un attributo sono definiti dall'oggetto [AttributeUsageAttribute](xref:System.AttributeUsageAttribute) applicato alla classe di attributi.

### <a name="type-accessibility"></a>Accessibilità dei tipi

Tutti i tipi dispongono di un modificatore che ne regola l'accessibilità da parte di altri tipi. Nella tabella che segue si descrive l'accessibilità dei tipi supportata dal runtime.

Accessibilità | Descrizione
------------- | -----------
public | Il tipo è accessibile da tutti gli assembly.
assembly | Il tipo è accessibile solo dall'interno dell'assembly.

L'accessibilità di un tipo annidato dipende dal relativo dominio di accessibilità, che è determinato sia dall'accessibilità dichiarata del membro che dal dominio di accessibilità del tipo che lo contiene direttamente. Tuttavia il dominio di accessibilità di un tipo annidato non può essere superiore a quello del tipo che lo contiene.

Il dominio di accessibilità di un membro annidato `M` dichiarato in un tipo `T` all'interno di un programma `P` viene definito come riportato di seguito (si noti che `M` potrebbe essere a sua volta un tipo): 

* Se l'accessibilità dichiarata di `M` è `public`, il dominio di accessibilità di `M` è il dominio di accessibilità di `T`.

* Se l'accessibilità dichiarata di `M` è `protected internal`, il dominio di accessibilità di `M` è l'intersezione del dominio di accessibilità di `T` con il testo di programma di `P` e il testo di programma di qualsiasi tipo derivato da `T` dichiarato esternamente a `P`.

* Se l'accessibilità dichiarata di `M` è `protected`, il dominio di accessibilità di `M` è l'intersezione del dominio di accessibilità di `T` con il testo di programma di `T` e qualsiasi tipo derivato da `T`.

* Se l'accessibilità dichiarata di `M` è `internal`, il dominio di accessibilità di `M` è l'intersezione del dominio di accessibilità di `T` con il testo di programma di `P`.

* Se l'accessibilità dichiarata di `M` è `private`, il dominio di accessibilità di `M` è il testo di programma di `T`.

### <a name="type-names"></a>Nomi dei tipi

Il sistema di tipi comuni impone solo due restrizioni sui nomi: 

* Tutti i nomi sono codificati come stringhe di caratteri Unicode, ovvero a 16 bit.

* I nomi non possono avere un valore incorporato (a 16 bit) pari a 0x0000.

La maggior parte dei linguaggi impone tuttavia restrizioni aggiuntive per i nomi dei tipi. Poiché tutti i confronti vengono effettuati byte per byte, sono indipendenti dalle impostazioni locali e fanno distinzione tra maiuscole e minuscole.

Sebbene un tipo possa fare riferimento a tipi di altri moduli e assembly, deve essere definito completamente all'interno di un modulo .NET. A seconda del supporto del compilatore, tuttavia, può essere diviso in più file di codice sorgente. I nomi dei tipi devono essere univoci solo all'interno di uno spazio dei nomi. Per identificare completamente un tipo, il relativo nome deve essere qualificato dallo spazio dei nomi che contiene l'implementazione del tipo.

### <a name="base-types-and-interfaces"></a>Tipi di base e interfacce

Un tipo può ereditare valori e comportamenti da un altro tipo. Common Type System non consente ai tipi di ereditare da più di un tipo base.

Un tipo può implementare un numero indefinito di interfacce. Per implementare un'interfaccia un tipo deve implementare tutti i membri virtuali di tale interfaccia. Un metodo virtuale può essere implementato da un tipo derivato e può essere richiamato in modo statico o dinamico.

## <a name="type-members"></a>Membri dei tipi

Il runtime consente di definire membri del tipo per specificare il comportamento e lo stato di un tipo. I membri dei tipi includono gli elementi seguenti:

* [Campi](#fields)

* [Proprietà](#properties)

* [Metodi](#methods)

* [Costruttori](#constructors)

* [Eventi](#events)

* [Tipi annidati](#nested-types)

### <a name="fields"></a>Campi

Un campo descrive e contiene parte dello stato del tipo. I campi possono essere di qualsiasi tipo supportato dal runtime. Nella maggior parte dei casi, i campi sono `private` o `protected`, in modo che siano accessibili solo dall'interno della classe o da una classe derivata. Se il valore di un campo può essere modificato dall'esterno del relativo tipo, viene in genere utilizzata una funzione di accesso set della proprietà. I campi esposti pubblicamente sono in genere di sola lettura e possono essere di due tipi: 

* Costanti, il cui valore viene assegnato durante la fase di progettazione. Si tratta di membri statici di una classe, sebbene non vengano definiti utilizzando la parola chiave `static` (`Shared` in Visual Basic).

* Variabili di sola lettura, i cui valori possono essere assegnati nel costruttore di classi.

Nell'esempio seguente vengono illustrati questi due utilizzi di campi di sola lettura.

```csharp
using System;

public class Constants
{
   public const double Pi = 3.1416;
   public readonly DateTime BirthDate;

   public Constants(DateTime birthDate)
   {
      this.BirthDate = birthDate;
   }
}

public class Example
{
   public static void Main()
   {
      Constants con = new Constants(new DateTime(1974, 8, 18));
      Console.Write(Constants.Pi + "\n");
      Console.Write(con.BirthDate.ToString("d") + "\n");
   }
}
// The example displays the following output if run on a system whose current
// culture is en-US:
//    3.1417
//    8/18/1974
```

```vb
Public Class Constants
   Public Const Pi As Double = 3.1416
   Public ReadOnly BirthDate As Date

   Public Sub New(birthDate As Date)
      Me.BirthDate = birthDate
   End Sub
End Class

Public Module Example
   Public Sub Main()
      Dim con As New Constants(#8/18/1974#)
      Console.WriteLine(Constants.Pi.ToString())
      Console.WriteLine(con.BirthDate.ToString("d"))
   End Sub
End Module
' The example displays the following output if run on a system whose current
' culture is en-US:
'    3.1417
'    8/18/1974
```

### <a name="properties"></a>Proprietà

Una proprietà consente di denominare un valore o uno stato del tipo e di definire i metodi per ottenere o impostare il valore della proprietà. Le proprietà possono essere tipi primitivi, raccolte di tipi primitivi, tipi definiti dall'utente, oppure raccolte di tipi definiti dall'utente. Sono spesso utilizzate per mantenere l'interfaccia pubblica di un tipo indipendente dalla sua effettiva rappresentazione. In questo modo le proprietà riflettono valori che non sono archiviati direttamente nella classe, ad esempio quando una proprietà restituisce un valore calcolato, oppure eseguono la convalida prima che i valori vengano assegnati a campi privati. Nell'esempio seguente viene illustrato quest'ultimo caso.

```csharp
using System;

public class Person
{
   private int m_Age;

   public int Age
   { 
      get { return m_Age; }
      set {
         if (value < 0 || value > 125)
         {
            throw new ArgumentOutOfRangeException("The value of the Age property must be between 0 and 125.");
         }
         else
         {
            m_Age = value;
         }         
      }
   }
}
```

```vb
Public Class Person
   Private m_Age As Integer

   Public Property Age As Integer
      Get
         Return m_Age
      End Get
      Set
         If value < 0 Or value > 125 Then
            Throw New ArgumentOutOfRangeException("The value of the Age property must be between 0 and 125.")
         Else
            m_Age = value
         End If
      End Set
   End Property
End Class
```

Oltre a includere la proprietà stessa, Microsoft Intermediate Language (MSIL) per un tipo contenente una proprietà leggibile include un metodo `get`*_propertyname* e per un tipo contenente una proprietà scrivibile include un metodo `set`*_propertyname*.

### <a name="methods"></a>Metodi

Un metodo descrive le operazioni disponibili sul tipo. Nella firma di un metodo sono specificati i tipi consentiti di tutti i relativi parametri e del relativo valore restituito.

Sebbene molti metodi definiscono il numero preciso di parametri necessari per le chiamate al metodo, alcuni metodi supportano un numero di parametri variabile. Il parametro finale dichiarato di questi metodi è contrassegnato con l'attributo [ParamArrayAttribute](xref:System.ParamArrayAttribute). I compilatori di linguaggio specificano in genere una parola chiave, ad esempio `params` in C# e `ParamArray` in Visual Basic, che usa esplicitamente l'attributo [ParamArrayAttribute](xref:System.ParamArrayAttribute) non necessario.

### <a name="constructors"></a>Costruttori

Un costruttore è un tipo speciale di metodo che consente di creare nuove istanze di una classe o di una struttura. Analogamente a ogni altro metodo, un costruttore può includere parametri. I costruttori, tuttavia, non restituiscono alcun valore, ovvero restituiscono `void`. 

Se il codice sorgente per una classe non definisce in modo esplicito un costruttore, il compilatore include un costruttore predefinito (senza parametri). Se tuttavia il codice sorgente per una classe definisce solo costruttori con parametri, il compilatore di C# non genera un costruttore senza parametri.

Se il codice sorgente per una struttura definisce i costruttori, essi devono essere con parametri. Una struttura non può definire un costruttore predefinito (senza parametri) e i compilatori non generano costruttori senza parametri per strutture o altri tipi di valori. Tutti i tipi di valori hanno un costruttore predefinito implicito. Questo costruttore viene implementato da Common Language Runtime e inizializza tutti i campi della struttura sui valori predefiniti. 

### <a name="events"></a>Eventi

Un evento definisce una situazione a cui è possibile fornire risposta e metodi per la sottoscrizione, l'annullamento della sottoscrizione e la generazione dell'evento. Gli eventi sono spesso utilizzati per indicare modifiche di stato a tipi diversi.

### <a name="nested-types"></a>Tipi annidati

I tipi annidati sono tipi membri di altri tipi. I tipi annidati devono essere strettamente collegati ai rispettivi tipi contenitori e non devono essere utilizzati come tipi generici. I tipi annidati risultano utili quando il tipo dichiarante utilizza e crea istanze del tipo annidato e quando il loro utilizzo non viene esposto in membri pubblici.

Per alcuni sviluppatori i tipi annidati possono generare confusione e dovrebbero essere visibili pubblicamente solo in casi di assoluta necessità. In una libreria progettata correttamente è improbabile che gli sviluppatori debbano utilizzare tipi annidati per creare istanze di oggetti o dichiarare variabili.

## <a name="characteristics-of-type-members"></a>Caratteristiche dei membri dei tipi

In Common Type System i membri dei tipi possono disporre di caratteristiche diverse, anche se non è necessario che i linguaggi le supportino tutte. Nella tabella riportata di seguito vengono descritte le caratteristiche dei membri.

Caratteristica | Si applica a | Descrizione
-------------- | ------------ | -----------
abstract | Metodi, proprietà ed eventi | Il tipo non fornisce l'implementazione del metodo. I tipi che ereditano o implementano metodi astratti devono fornire un'implementazione per il metodo. L'unica eccezione si verifica nel caso in cui il tipo derivato sia esso stesso un tipo astratto. Tutti i metodi astratti sono virtuali.
private | Tutti | Accessibile solo dall'interno dello stesso tipo del membro o di un tipo annidato.
family | Tutti | Accessibile dall'interno dello stesso tipo del membro e dai tipi derivati che ereditano da esso.
assemby | Tutti | Accessibile solo nell'assembly nel quale il tipo viene definito.
family e assembly | Tutti | Accessibile solo dai tipi che sono qualificati sia per l'accesso di gruppo che di assembly.
family o assembly | Tutti | Accessibile solo dai tipi che sono qualificati per l'accesso di gruppo o per quello di assembly.
public | Tutti | Accessibile da qualsiasi tipo.
final | Metodi, proprietà ed eventi | Il metodo virtuale non può essere sottoposto a override in un tipo derivato.
initialize-only | Campi | Il valore può essere solo inizializzato e non può essere scritto dopo l'inizializzazione.
istanza | Campi, metodi, proprietà ed eventi | Se un membro non è contrassegnato come `static` (C#), `Shared` (Visual Basic), `virtual` (C#) o `Overridable` (Visual Basic), è un membro di istanza (nessuna parola chiave di istanza). Ci saranno tante copie di tali membri in memoria quanti sono gli oggetti che li utilizzano.
valore letterale | Campi | Il valore assegnato al campo è un valore fisso, noto in fase di compilazione, di un tipo di valore incorporato. Ai campi literal viene a volte fatto riferimento come a costanti.
newslot o override | Tutti | Definisce come il membro interagisce con membri ereditati aventi la stessa firma: `newslot` nasconde i membri ereditati aventi la stessa firma; `override` sostituisce la definizione di un metodo virtuale ereditato. Il valore predefinito è newslot.
statico | Campi, metodi, proprietà ed eventi | Il membro appartiene al tipo sul quale viene definito, non a un'istanza specifica del tipo. Il membro esiste anche se non viene creata un'istanza del tipo ed è condiviso tra tutte le istanze del tipo.
virtuale | Metodi, proprietà ed eventi | Il metodo può essere implementato da un tipo derivato e può essere richiamato in modo statico o dinamico. Se viene utilizzata la chiamata dinamica, il tipo dell'istanza che effettua la chiamata in fase di esecuzione, e non il tipo noto in fase di compilazione, determina l'implementazione del metodo chiamata. Per richiamare un metodo virtuale in modo statico, potrebbe essere necessario eseguire il cast della variabile in un tipo che utilizza la versione desiderata del metodo.

### <a name="overloading"></a>Overload

Ciascun membro di tipo dispone di una firma univoca. La firma di un metodo è costituita dal nome del metodo e da un elenco di parametri, ovvero l'ordine e i tipi degli argomenti del metodo. All'interno di un tipo è possibile definire più metodi con lo stesso nome, purché la relativa firma sia diversa. Quando vengono definiti due o più metodi con lo stesso nome si dice che il metodo è stato sottoposto a overload. Ad esempio, in [System.Char](xref:System.Char) il metodo `IsDigit` è sottoposto a overload. Un metodo usa un oggetto [Char](xref:System.Char). L'altro metodo usa un oggetto [String](xref:System.String) e un oggetto [Int32](xref:System.Int32). 

> [!NOTE]
> Il tipo restituito non viene considerato parte della firma del metodo. Ciò significa che i metodi non possono essere sottoposti a overload se differiscono unicamente per il tipo restituito.

### <a name="inheriting-overriding-and-hiding-members"></a>Eredità, override e membri nascosti

Un tipo derivato eredita tutti i membri del relativo tipo di base, ovvero tali membri vengono definiti e resi disponibili nel tipo derivato. Il comportamento o le qualità dei membri ereditati possono essere modificati in due modi: 

* È possibile nascondere un membro ereditato con un tipo derivato definendo un nuovo membro con la stessa firma. Questa operazione può essere eseguita per rendere privato un membro precedentemente pubblico oppure per definire un nuovo comportamento per un metodo ereditato contrassegnato come `final`.

* Con un tipo derivato è possibile eseguire l'override di un metodo virtuale ereditato. Nel metodo con cui viene eseguito l'override si fornisce una nuova definizione del metodo che sarà richiamato in base al tipo del valore in fase di esecuzione anziché in base al tipo della variabile nota in fase di compilazione. Un metodo può sottoporre a override un metodo virtuale solo se quest'ultimo non è contrassegnato come `final` e se il nuovo metodo è accessibile almeno quanto il metodo virtuale.

## <a name="see-also"></a>Vedere anche

[Conversione di tipi in .NET Framework](type-conversion.md)


<!--HONumber=Nov16_HO1-->


