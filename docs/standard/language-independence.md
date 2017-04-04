---
title: Indipendenza del linguaggio e componenti indipendenti dal linguaggio
description: Indipendenza del linguaggio e componenti indipendenti dal linguaggio
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 07/22/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 2dbed1bc-86f5-43cd-9a57-adbb1c5efba4
translationtype: Human Translation
ms.sourcegitcommit: b967d8e55347f44a012e4ad8e916440ae228c8ec
ms.openlocfilehash: 815d9c24c139ef738b256c7bee791756a2fdb3b3
ms.lasthandoff: 03/10/2017

---

# <a name="language-independence-and-language-independent-components"></a>Indipendenza del linguaggio e componenti indipendenti dal linguaggio

La piattaforma .NET è indipendente dal linguaggio. Questo significa che gli sviluppatori possono lavorare in uno dei diversi linguaggi che hanno come destinazione la piattaforma .NET, ad esempio C#, F# e Visual Basic. È possibile accedere a tipi e membri di librerie di classi sviluppate per la piattaforma .NET senza dover conoscere il linguaggio in cui sono stati originariamente scritti e senza dover seguire nessuna delle convenzioni del linguaggio originale. Se si è uno sviluppatore di componenti, è possibile accedere al componente da qualsiasi applicazione .NET, indipendentemente dal linguaggio.

> [!NOTE]
> La prima parte di questo articolo illustra la creazione di componenti indipendenti dal linguaggio, vale a dire componenti che possono essere usati da applicazioni scritte in qualsiasi linguaggio. È anche possibile creare un singolo componente o applicazione dal codice sorgente scritto in più linguaggi. Vedere [Interoperabilità tra linguaggi diversi](#cross-language-interoperability) nella seconda parte di questo articolo. 

È necessario che gli oggetti espongano ai chiamanti solo le funzionalità comuni a tutti i linguaggi, affinché sia garantita un'interazione completa con altri oggetti scritti in uno qualsiasi dei linguaggi. Questo set comune di funzionalità è definito dalle specifiche CLS (Common Language Specification), un set di regole che si applicano agli assembly generati. Le specifiche CLS (Common Language Specification) sono definite nella partizione I, clausole da 7 a 11 dello [standard ECMA-335 di Common Language Infrastructure](http://www.ecma-international.org/publications/standards/Ecma-335.htm). 

Se il componente è conforme alle specifiche CLS (Common Language Specification), ne è garantita la conformità a CLS ed è possibile accedervi dal codice negli assembly scritti in qualsiasi linguaggio di programmazione che supporti CLS. È possibile determinare se il componente è conforme alle specifiche CLS (Common Language Specification) in fase di compilazione applicando l'attributo [CLSCompliantAttribute](xref:System.CLSCompliantAttribute) al codice sorgente. Per altre informazioni, vedere [Attributo CLSCompliantAttribute](#the-clscompliantattribute-attribute).

Contenuto dell'articolo:

* [Regole di conformità a CLS](#cls-compliance-rules)

    * [Tipi e firme dei membri di tipo](#types-and-type-member-signatures)

    * [Convenzioni di denominazione](#naming-conventions)
    
    * [Conversione di tipi](#type-conversion)
    
    * [Array](#arrays)
    
    * [Interfacce](#interfaces)
    
    * [Enumerazioni](#enumerations)
    
    * [Membri dei tipi di in generale](#type-members-in-general)
    
    * [Accessibilità del membro](#member-accessibility)
    
    * [Tipi e membri generici](#generic-types-and-members)
    
    * [Costruttori](#constructors)
    
    * [Proprietà](#properties)
    
    * [Eventi](#events)
    
    * [Overload](#overloads)
    
    * [Eccezioni](#exceptions)
    
    * [Attributi](#attributes)
    
* [Attributo CLSCompliantAttribute](#the-clscompliantattribute-attribute)

* [Interoperabilità tra linguaggi diversi](#cross-language-interoperability)

## <a name="cls-compliance-rules"></a>Regole di conformità a CLS

In questa sezione vengono illustrate le regole per creare un componente conforme a CLS. Per un elenco completo delle regole, vedere la partizione I, clausola 11 dello [standard ECMA-335 di Common Language Infrastructure](http://www.ecma-international.org/publications/standards/Ecma-335.htm).

> [!NOTE]
> Nelle specifiche CLS (Common Language Specification) viene illustrata ciascuna regola per la conformità a CLS applicata ai consumer (sviluppatori che accedono a livello di codice a un componente conforme a CLS), ai framework (sviluppatori che usano un compilatore di linguaggio per creare librerie conformi a CLS) e alle estensioni (sviluppatori che creano uno strumento quale un compilatore di linguaggio o un parser di codice per la creazione di componenti conformi a CLS). Questo articolo è incentrato sulle regole che si applicano ai framework. Si noti, tuttavia, che alcune delle regole applicate alle estensioni possono essere applicate anche agli assembly creati usando [Reflection.Emit](xref:System.Reflection.Emit). 

Per progettare un componente indipendente dal linguaggio, è necessario applicare le regole per la conformità a CLS solo all'interfaccia pubblica del componente. L'implementazione privata non deve essere conforme alla specifica. 

> [!IMPORTANT]
> Le regole per la conformità a CLS si applicano solo all'interfaccia pubblica di un componente, non alla relativa implementazione privata. 

Ad esempio, Unsigned Integer diversi da [Byte](xref:System.Byte) non sono conformi a CLS. Poiché la classe `Person` dell'esempio seguente espone una proprietà `Age` di tipo [UInt16](xref:System.UInt16), il codice riportato di seguito visualizza un avviso del compilatore.

```csharp
using System;

[assembly: CLSCompliant(true)]

public class Person
{
   private UInt16 personAge = 0;

   public UInt16 Age 
   { get { return personAge; } }
}
// The attempt to compile the example displays the following compiler warning:
//    Public1.cs(10,18): warning CS3003: Type of 'Person.Age' is not CLS-compliant
```

```vb
<Assembly: CLSCompliant(True)> 

Public Class Person
   Private personAge As UInt16

   Public ReadOnly Property Age As UInt16
      Get
         Return personAge      
      End Get   
   End Property
End Class
' The attempt to compile the example displays the following compiler warning:
'    Public1.vb(9) : warning BC40027: Return type of function 'Age' is not CLS-compliant.
'    
'       Public ReadOnly Property Age As UInt16
'                                ~~~
```

È possibile rendere la classe Person conforme a CLS modificando il tipo di proprietà `Age` da `UInt16` a [Int16](xref:System.Int16), vale a dire un Signed Integer a 16 bit conforme a CLS. Non è necessario modificare il tipo del campo `personAge` privato. 

```csharp
using System;

[assembly: CLSCompliant(true)]

public class Person
{
   private Int16 personAge = 0;

   public Int16 Age 
   { get { return personAge; } }
}
```

```vb
<Assembly: CLSCompliant(True)> 

Public Class Person
   Private personAge As UInt16

   Public ReadOnly Property Age As Int16
      Get
         Return CType(personAge, Int16)      
      End Get   
   End Property
End Class
```

L'interfaccia pubblica di una libreria è costituita dagli elementi seguenti:

* Definizioni di classi pubbliche.

* Definizioni dei membri pubblici di classi pubbliche e definizioni di membri accessibili alle classi derivate, cioè membri protetti. 

* Parametri e tipi restituiti di metodi pubblici di classi pubbliche e parametri e tipi restituiti di metodi accessibili alle classi derivate. 

Le regole per la conformità a CLS sono elencate nella tabella riportata di seguito. Il testo delle regole è stato copiato alla lettera dallo [standard ECMA-335 di Common Language Infrastructure](http://www.ecma-international.org/publications/standards/Ecma-335.htm), Copyright 2012 di Ecma International. Nelle sezioni seguenti sono disponibili informazioni più dettagliate su queste regole. 

Categoria | Vedere | Regola | Numero regola
-------- | --- | ---- | -----------
Accessibilità | [Accessibilità del membro](#member-accessibility) | L'accessibilità non sarà modificata quando si esegue l'override di metodi ereditati, tranne nel caso in cui si esegue l'override di un metodo ereditato da un assembly diverso con accessibilità `family-or-assembly`. In questo caso, l'override disporrà dell'accessibilità `family`. | 10
Accessibilità | [Accessibilità del membro](#member-accessibility) | La visibilità e l'accessibilità di tipi e membri saranno tali che i tipi nella firma di qualsiasi membro saranno visibili e accessibili ogni volta che il membro stesso è visibile e accessibile. Ad esempio, in un metodo pubblico che è visibile all'esterno del relativo assembly non deve essere presente un argomento il cui tipo è visibile solo nell'assembly. La visibilità e l'accessibilità di tipi che compongono un tipo generico con istanze usato nella firma di qualsiasi membro saranno visibili e accessibili ogni volta che il membro stesso è visibile e accessibile. Ad esempio, in un tipo generico con istanze presente nella firma di un membro visibile all'esterno del relativo assembly non deve essere disponibile un argomento generico il cui tipo è visibile solo nell'assembly. | 12
Array | [Array](#arrays) | Le matrici devono disporre di elementi con un tipo conforme a CLS e i limiti inferiori di tutte le dimensioni della matrice devono essere pari a zero. Solo per il fatto che un elemento sia una matrice, il tipo di elemento della matrice sarà richiesto per eseguire una distinzione tra gli overload. Quando l'overload è basato su due o più i tipi di matrice, i tipi di elemento vengono denominati tipi. | 16
Attributi | [Attributi](#attributes) | Gli attributi devono essere di tipo [System.Attribute](xref:System.Attribute) o derivati da questo tipo. | 41
Attributi | [Attributi](#attributes) | La specifica CLS consente solo un subset delle codifiche di attributi personalizzati. Gli unici tipi che verranno visualizzati in queste codifiche sono (vedere la partizione IV): [System.Type](xref:System.Type), [System.String](xref:System.String), [System.Char](xref:System.Char), [System.Boolean](xref:System.Boolean), [System.Byte](xref:System.Byte), [System.Int16](xref:System.Int16), [System.Int32](xref:System.Int32), [System.Int64](xref:System.Int64), [System.Single](xref:System.Single), [System.Double](xref:System.Double) e qualsiasi tipo di enumerazione basato su un tipo Integer di base conforme a CLS. | 34
Attributi | [Attributi](#attributes) | La specifica CLS non consente i modificatori necessari visibili pubblicamente (`modreq`, vedere la partizione II), ma consente i modificatori facoltativi (`modopt`, vedere la partizione II) che non riconosce. | 35
Costruttori | [Costruttori](#constructors) | Prima di un eventuale accesso ai dati di istanza ereditati, tramite un costruttore di oggetti deve essere effettuata una chiamata a un costruttore di istanze della relativa classe di base. Ciò non si applica ai tipi di valore, che non devono disporre di costruttori.  | 21
Costruttori | [Costruttori](#constructors) | Un costruttore di oggetti non deve essere chiamato se non come parte della creazione di un oggetto e un oggetto non deve essere inizializzato due volte. | 22
Enumerazioni | [Enumerazioni](#enumerations) | Il tipo sottostante di un'enumerazione deve essere un tipo Integer CLS incorporato, il nome del campo deve essere "value__" e il campo deve essere contrassegnato come `RTSpecialName`. |  7
Enumerazioni | [Enumerazioni](#enumerations) | Sono disponibili due tipi distinti di enumerazioni, indicati dalla presenza o dall'assenza dell'attributo personalizzato [System.FlagsAttribute](xref:System.FlagsAttribute) (vedere la libreria nella partizione IV). Una rappresenta Integer denominati, l'altra flag di bit denominati che possono essere combinati per generare un valore senza nome. Il valore di un oggetto `enum` non è limitato ai valori specifici. |  8
Enumerazioni | [Enumerazioni](#enumerations) | Il tipo dei campi statici con valori letterali di un'enumerazione deve essere uguale a quello dell'enumerazione stessa. |  9
eventi | [Eventi](#events) | I metodi che implementano un evento devono essere contrassegnati come `SpecialName` nei metadati. |29
eventi | [Eventi](#events) | L'accessibilità di un evento e le relative funzioni di accesso devono essere identiche. |30
eventi | [Eventi](#events) | I metodi `add` e `remove` per un evento devono essere entrambi presenti o entrambi assenti. |31
eventi | [Eventi](#events) | I metodi `add` e `remove` per un evento devono entrambi accettare un parametro il cui tipo definisce il tipo dell'evento e che deve essere derivato da [System.Delegate](xref:System.Delegate). |32
eventi | [Eventi](#events) | Gli eventi devono essere conformi a un pattern di nome specifico. L'attributo SpecialName indicato nella regola CLS 29 deve essere ignorato nei confronti tra nomi appropriati e deve essere conforme alle regole dell'identificatore.  |33
Eccezioni | [Eccezioni](#exceptions) | Gli oggetti generati devono essere di tipo [System.Exception](xref:System.Exception) o di un tipo che eredita da esso. Ciononostante, i metodi conformi a CLS non sono necessari per bloccare la propagazione di altri tipi di eccezioni. | 40
Generale | [Regole di conformità a CLS](#cls-compliance-rules) | Le regole CLS sono valide solo per quelle parti di un tipo che sono accessibili o visibili all'esterno dell'assembly di definizione. | 1
Generale | [Regole di conformità a CLS](#cls-compliance-rules) | I membri di tipi non conformi a CLS non saranno contrassegnati come conformi a CLS. | 2
Generics | [Tipi e membri generici](#generic-types-and-members) | I tipi annidati disporranno di un numero di parametri generici almeno pari a quelli del tipo di inclusione. I parametri generici di un tipo annidato corrispondono per posizione ai parametri generici del rispettivo tipo di inclusione.  | 42
Generics | [Tipi e membri generici](#generic-types-and-members) | Con il nome di un tipo generico verrà codificato il numero di parametri di tipo dichiarati nel tipo non annidato o appena introdotti nel tipo se annidato, in base alle regole definite sopra. | 43
Generics | [Tipi e membri generici](#generic-types-and-members) | Tramite un tipo generico deve essere dichiarato nuovamente un numero di vincoli sufficiente a garantire che qualsiasi vincolo delle interfacce o del tipo base venga soddisfatto dai vincoli del tipo generico. | 44
Generics | [Tipi e membri generici](#generic-types-and-members) | I tipi usati come vincoli sui parametri generici dovranno essere essi stessi conformi a CLS. | 45
Generics | [Tipi e membri generici](#generic-types-and-members) | La visibilità e l'accessibilità di membri (compresi i tipi annidati) in un tipo generico con istanze devono essere considerate come limitate all'ambito della creazione di un'istanza specifica, anziché come dichiarazione del tipo generico nel suo complesso. Partendo da questo presupposto, valgono ancora le regole di visibilità e accessibilità della regola CLS 12. | 46
Generics | [Tipi e membri generici](#generic-types-and-members) | Per ogni metodo generico astratto o virtuale sarà necessaria un'implementazione concreta (non astratta) predefinita | 47
Interfacce | [Interfacce](#interfaces) | Per l'implementazione delle interfacce conformi a CLS non sarà necessaria la definizione di metodi non conformi a CLS. | 18
Interfacce | [Interfacce](#interfaces) | Tramite le interfacce conformi a CLS non verranno definiti i metodi statici, né verranno definiti i campi. | 19
Membri | [Membri dei tipi di in generale](#type-members-in-general) | I metodi e i campi static globali non sono conformi a CLS. | 36
Membri | -- | Il valore di un valore statico letterale viene specificato attraverso l'uso dei metadati di inizializzazione del campo. Un valore letterale conforme a CLS deve disporre di un valore specificato nei metadati di inizializzazione del campo che sia esattamente dello stesso tipo del valore letterale, o del tipo sottostante, se questo valore letterale è un oggetto `enum`. | 13
Membri | [Membri dei tipi di in generale](#type-members-in-general) | Il vincolo vararg non fa parte delle specifiche CLS e l'unica convenzione di chiamata supportata da CLS è la convenzione di chiamata gestita standard. | 15
Convenzioni di denominazione | [Convenzioni di denominazione](#naming-conventions) | Gli assembly seguiranno l'allegato 7 del rapporto tecnico 15 di Unicode Standard 3.0 con cui viene controllato il set di caratteri che possono essere usati all'inizio e all'interno degli identificatori, disponibili online nella pagina [Unicode Normalization Forms](http://www.unicode.org/unicode/reports/tr15/tr15-18.html) (Formati di normalizzazione Unicode). Gli identificatori dovranno essere nel formato canonico definito dal formato di normalizzazione Unicode C. Per fini CLS, due identificatori sono identici se i relativi mapping di minuscole (come specificato dai mapping di minuscole di tipo uno a uno, senza distinzione tra le impostazioni internazionali Unicode) sono uguali. Vale a dire, affinché due identificatori vengano considerati differenti nella specifica CLS, devono presentare differenze che vanno oltre la semplice distinzione tra maiuscole e minuscole. Tuttavia, per eseguire l'override di una definizione non ereditata, CLI richiede l'uso della codifica precisa della dichiarazione originale. | 4
Overload | [Convenzioni di denominazione](#naming-conventions) | Tutti i nomi introdotti in un ambito conforme a CLS devono essere di tipo indipendente e distinto, fatta eccezione per i casi in cui i nomi sono identici e vengono risolti tramite l'overload. Ad esempio, mentre CTS consente a un unico tipo di usare lo stesso nome per un metodo e per un campo, CLS non lo consente. | 5
Overload | [Convenzioni di denominazione](#naming-conventions) | I campi e i tipi annidati devono risultare distinti in base al solo confronto tra identificatori, anche se CTS consente la distinzione di firme distinte. I metodi, le proprietà e gli eventi che hanno lo stesso nome (in base al confronto degli identificatori) dovranno presentare differenze che vanno oltre il tipo restituito, ad eccezione di quanto specificato nella regola CLS 39. | 6
Overload | [Overload](#overloads) | È possibile eseguire l'overload solo di proprietà e metodi. | 37
Overload | [Overload](#overloads) |Le proprietà e i metodi possono essere sottoposti a overload solo in base al numero e ai tipi dei relativi parametri, a eccezione degli operatori di conversione denominati `op_Implicit` e `op_Explicit`, i quali possono essere anche sottoposti a overload in base al relativo tipo restituito. | 38
Overload | -- | Se due o più metodi conformi a CLS dichiarati in un tipo hanno lo stesso nome e, per un set specifico di creazioni di istanze del tipo, dispongono dello stesso parametro e dei tipi restituiti, tutti questi metodi saranno semanticamente equivalenti alle creazioni di istanze del tipo. | 48
Proprietà | [Proprietà](#properties) | I metodi che implementano i metodi Get e Set di una proprietà devono essere contrassegnati come `SpecialName` nei metadati. | 24
Proprietà | [Proprietà](#properties) | Le funzioni di accesso di una proprietà devono essere tutte statiche, tutte virtuali o tutte istanze. | 26
Proprietà | [Proprietà](#properties) | Il tipo di una proprietà deve essere il tipo restituito del metodo Get e il tipo dell'ultimo argomento del metodo Set. I tipi dei parametri della proprietà devono essere i tipi dei parametri per il metodo Get e i tipi di tutti i parametri del metodo Set tranne l'ultimo. Tutti questi tipi devono essere conformi a CLS e non devono essere puntatori gestiti, ossia non devono essere passati per riferimento. | 27
Proprietà | [Proprietà](#properties) | Le proprietà devono essere conformi a un pattern di nome specifico. L'attributo `SpecialName` indicato nella regola CLS 24 deve essere ignorato nei confronti tra nomi appropriati e deve essere conforme alle regole dell'identificatore. Una proprietà deve disporre di un metodo Get, un metodo Set o di entrambi. | 28
Conversione di tipi | [Conversione di tipi](#type-conversion) | Se viene specificato op_Implicit oppure op_Explicit, sarà necessario fornire un metodo alternativo di coercizione. | 39
Tipi | [Tipi e firme dei membri di tipo](#types-and-type-member-signatures) | I tipi di valore boxed non sono conformi a CLS. | 3
Tipi | [Tipi e firme dei membri di tipo](#types-and-type-member-signatures) | Tutti i tipi visualizzati in una firma devono essere conformi a CLS. Tutti i tipi che costituiscono un tipo generico con istanze devono essere conformi a CLS. | 11
Tipi | [Tipi e firme dei membri di tipo](#types-and-type-member-signatures) | I riferimenti tipizzati non sono conformi a CLS. | 14
Tipi | [Tipi e firme dei membri di tipo](#types-and-type-member-signatures) | I tipi di puntatore non gestiti non sono conformi a CLS. | 17
Tipi | [Tipi e firme dei membri di tipo](#types-and-type-member-signatures) | Per le classi, i tipi di valore e le interfacce conformi a CLS non è necessaria l'implementazione di membri non conformi a CLS | 20
Tipi | [Tipi e firme dei membri di tipo](#types-and-type-member-signatures) | [System.Object](xref:System.Object) è conforme a CLS. Qualsiasi altra classe conforme a CLS deve ereditare da una classe conforme a CLS. | 23

### <a name="types-and-type-member-signatures"></a>Tipi e firme dei membri di tipo

Il tipo [System.Object](xref:System.Object) è conforme a CLS ed è il tipo di base di tutti i tipi di oggetto nel sistema di tipo .NET Framework. L'ereditarietà in .NET Framework è implicita (ad esempio la classe [String](xref:System.String) eredita in modo implicito dalla classe `Object`) o esplicita (ad esempio la classe [CultureNotFoundException](xref:System.Globalization.CultureNotFoundException) eredita in modo esplicito dalla classe [ArgumentException](xref:System.ArgumentException), che eredita in modo esplicito dalla classe [Exception](xref:System.Exception). Affinché un tipo derivato sia conforme a CLS, anche il tipo di base deve essere conforme a CLS. 

Nell'esempio seguente viene illustrato un tipo derivato il cui tipo di base non è conforme a CLS. Viene definita una classe `Counter` base tramite in cui viene usato un Unsigned Integer a 32 bit come contatore. Poiché la classe fornisce la funzionalità contatore eseguendo il wrapping di un Unsigned Integer, la classe viene contrassegnata come non conforme a CLS. Di conseguenza, anche una classe derivata, `NonZeroCounter`, non è conforme a CLS. 

```csharp
using System;

[assembly: CLSCompliant(true)]

[CLSCompliant(false)] 
public class Counter
{
   UInt32 ctr;

   public Counter()
   {
      ctr = 0;
   }

   protected Counter(UInt32 ctr)
   {
      this.ctr = ctr;
   }

   public override string ToString()
   {
      return String.Format("{0}). ", ctr);
   }

   public UInt32 Value
   {
      get { return ctr; }
   }

   public void Increment() 
   {
      ctr += (uint) 1;
   }
}

public class NonZeroCounter : Counter
{
   public NonZeroCounter(int startIndex) : this((uint) startIndex)
   {
   }

   private NonZeroCounter(UInt32 startIndex) : base(startIndex)
   {
   }
}
// Compilation produces a compiler warning like the following:
//    Type3.cs(37,14): warning CS3009: 'NonZeroCounter': base type 'Counter' is not
//            CLS-compliant
//    Type3.cs(7,14): (Location of symbol related to previous warning)
```

```vb
<Assembly: CLSCompliant(True)>

<CLSCompliant(False)> _ 
Public Class Counter
   Dim ctr As UInt32

   Public Sub New
      ctr = 0
   End Sub

   Protected Sub New(ctr As UInt32)
      ctr = ctr
   End Sub

   Public Overrides Function ToString() As String
      Return String.Format("{0}). ", ctr)
   End Function

   Public ReadOnly Property Value As UInt32
      Get
         Return ctr
      End Get
   End Property

   Public Sub Increment()
      ctr += CType(1, UInt32)
   End Sub
End Class

Public Class NonZeroCounter : Inherits Counter
   Public Sub New(startIndex As Integer)
      MyClass.New(CType(startIndex, UInt32))
   End Sub

   Private Sub New(startIndex As UInt32)
      MyBase.New(CType(startIndex, UInt32))
   End Sub
End Class
' Compilation produces a compiler warning like the following:
'    Type3.vb(34) : warning BC40026: 'NonZeroCounter' is not CLS-compliant 
'    because it derives from 'Counter', which is not CLS-compliant.
'    
'    Public Class NonZeroCounter : Inherits Counter
'                 ~~~~~~~~~~~~~~
```

Tutti i tipi visualizzati nelle firme dei membri, incluso il tipo restituito di un metodo o un tipo di proprietà, devono essere conformi a CLS. Inoltre, per i tipi generici: 

* Tutti i tipi che costituiscono un tipo generico con istanze devono essere conformi a CLS.

* Tutti i tipi usati come vincoli sui parametri generici devono essere conformi a CLS. 

In [common type system](common-type-system.md) di .NET Framework è incluso un numero di tipi incorporati supportati direttamente da Common Language Runtime, codificati in particolare nei metadati di un assembly. Di questi tipi intrinseci, i tipi elencati nella tabella seguente sono conformi a CLS. 


Tipo conforme a CLS | Descrizione
------------------ | -----------
[Byte](xref:System.Byte) | Unsigned Integer a 8 bit 
[Int16](xref:System.Int16) | Signed Integer a 16 bit 
[Int32](xref:System.Int32) | Intero con segno a 32 bit 
[Int64](xref:System.Int64) | Intero con segno a 64 bit
[Single](xref:System.Single) | Valore a virgola mobile e precisione singola
[Double](xref:System.Double) | Valore a virgola mobile e precisione doppia
[Boolean](xref:System.Boolean) | tipo di valore true o false 
[Char](xref:System.Char) | Unità di codice codificata UTF-16
[Decimal](xref:System.Decimal) | Numero decimale non a virgola mobile
[IntPtr](xref:System.IntPtr) | Puntatore o handle di una dimensione definita dalla piattaforma
[String](xref:System.String) | Raccolta di zero, uno o più oggetti Char 
 
I tipi intrinseci elencati nella tabella seguente non sono conformi a CLS.


Tipo non conforme | Descrizione | Alternativa alla conformità a CLS
------------------ | ----------- | -------------------------
[SByte](xref:System.SByte) | Tipo di dati Signed Integer a 8 bit | [Int16](xref:System.Int16)
[UInt16](xref:System.UInt16) | Intero senza segno a 16 bit | [Int32](xref:System.Int32)
[UInt32](xref:System.UInt32) | Intero senza segno a 32 bit | [Int64](xref:System.Int64)
[UInt64](xref:System.UInt64) | Intero senza segno a 64 bit | [Int64](xref:System.Int64) (possibile overflow), [BigInteger](xref:System.Numerics.BigInteger) o [Double](xref:System.Double)
[UIntPtr](xref:System.UIntPtr) | Puntatore o handle senza segno | [IntPtr](xref:System.IntPtr)
 
 Nella libreria di classi .NET Framework o in qualsiasi altra libreria di classi possono essere inclusi altri tipi non conformi a CLS; ad esempio: 
 
 * Tipi di valore boxed. Nell'esempio C# seguente viene creata una classe con una proprietà pubblica di tipo `int`*denominata `Value`. Poiché `int`* è un tipo di valore boxed, il compilatore lo contrassegna come non conforme a CLS.

  ```csharp
  using System;

  [assembly:CLSCompliant(true)]

  public unsafe class TestClass
  {
     private int* val;

     public TestClass(int number)
     {
        val = (int*) number;
     }

     public int* Value {
        get { return val; }        
     }
  }
  // The compiler generates the following output when compiling this example:
  //        warning CS3003: Type of 'TestClass.Value' is not CLS-compliant
  ```

* Riferimenti tipizzati, che sono costrutti speciali contenenti un riferimento a un oggetto e un riferimento a un tipo.

Se un tipo non è conforme a CLS, è necessario applicarvi l'attributo [CLSCompliantAttribute](xref:System.CLSCompliantAttribute) con un parametro *isCompliant* con valore `false`. Per altre informazioni, vedere la sezione [Attributo CLSCompliantAttribute](#the-clscompliantattribute-attribute).  

Nell'esempio seguente viene illustrato il problema della conformità a CLS in una firma di metodo e nella creazione di un'istanza di tipo generico. Viene definita una classe `InvoiceItem` con una proprietà di tipo [UInt32](xref:System.UInt32), una proprietà di tipo [Nullable(Of UInt32)](xref:System.Nullable%601) e un costruttore con parametri di tipo `UInt32` e `Nullable(Of UInt32)`. Vengono visualizzati quattro avvisi del compilatore quando si tenta di compilare l'esempio.

```csharp
using System;

[assembly: CLSCompliant(true)]

public class InvoiceItem
{
   private uint invId = 0;
   private uint itemId = 0;
   private Nullable<uint> qty;

   public InvoiceItem(uint sku, Nullable<uint> quantity)
   {
      itemId = sku;
      qty = quantity;
   }

   public Nullable<uint> Quantity
   {
      get { return qty; }
      set { qty = value; }
   }

   public uint InvoiceId
   {
      get { return invId; }
      set { invId = value; }
   }
}
// The attempt to compile the example displays the following output:
//    Type1.cs(13,23): warning CS3001: Argument type 'uint' is not CLS-compliant
//    Type1.cs(13,33): warning CS3001: Argument type 'uint?' is not CLS-compliant
//    Type1.cs(19,26): warning CS3003: Type of 'InvoiceItem.Quantity' is not CLS-compliant
//    Type1.cs(25,16): warning CS3003: Type of 'InvoiceItem.InvoiceId' is not CLS-compliant
```

```vb
<Assembly: CLSCompliant(True)>

Public Class InvoiceItem

   Private invId As UInteger = 0
   Private itemId As UInteger = 0
   Private qty AS Nullable(Of UInteger)

   Public Sub New(sku As UInteger, quantity As Nullable(Of UInteger))
      itemId = sku
      qty = quantity
   End Sub

   Public Property Quantity As Nullable(Of UInteger)
      Get
         Return qty
      End Get   
      Set 
         qty = value
      End Set   
   End Property

   Public Property InvoiceId As UInteger
      Get   
         Return invId
      End Get
      Set 
         invId = value
      End Set   
   End Property
End Class
' The attempt to compile the example displays output similar to the following:
'    Type1.vb(13) : warning BC40028: Type of parameter 'sku' is not CLS-compliant.
'    
'       Public Sub New(sku As UInteger, quantity As Nullable(Of UInteger))
'                      ~~~
'    Type1.vb(13) : warning BC40041: Type 'UInteger' is not CLS-compliant.
'    
'       Public Sub New(sku As UInteger, quantity As Nullable(Of UInteger))
'                                                               ~~~~~~~~
'    Type1.vb(18) : warning BC40041: Type 'UInteger' is not CLS-compliant.
'    
'       Public Property Quantity As Nullable(Of UInteger)
'                                               ~~~~~~~~
'    Type1.vb(27) : warning BC40027: Return type of function 'InvoiceId' is not CLS-compliant.
'    
'       Public Property InvoiceId As UInteger
```

Per eliminare gli avvisi del compilatore, sostituire i tipi non conformi a CLS nell'interfaccia pubblica `InvoiceItem` con tipi conformi:

```csharp
using System;

[assembly: CLSCompliant(true)]

public class InvoiceItem
{
   private uint invId = 0;
   private uint itemId = 0;
   private Nullable<int> qty;

   public InvoiceItem(int sku, Nullable<int> quantity)
   {
      if (sku <= 0)
         throw new ArgumentOutOfRangeException("The item number is zero or negative.");
      itemId = (uint) sku;

      qty = quantity;
   }

   public Nullable<int> Quantity
   {
      get { return qty; }
      set { qty = value; }
   }

   public int InvoiceId
   {
      get { return (int) invId; }
      set { 
         if (value <= 0)
            throw new ArgumentOutOfRangeException("The invoice number is zero or negative.");
         invId = (uint) value; }
   }
}
```

```vb
Assembly: CLSCompliant(True)>

Public Class InvoiceItem

   Private invId As UInteger = 0
   Private itemId As UInteger = 0
   Private qty AS Nullable(Of Integer)

   Public Sub New(sku As Integer, quantity As Nullable(Of Integer))
      If sku <= 0 Then
         Throw New ArgumentOutOfRangeException("The item number is zero or negative.")
      End If
      itemId = CUInt(sku)
      qty = quantity
   End Sub

   Public Property Quantity As Nullable(Of Integer)
      Get
         Return qty
      End Get   
      Set 
         qty = value
      End Set   
   End Property

   Public Property InvoiceId As Integer
      Get   
         Return CInt(invId)
      End Get
      Set 
         invId = CUInt(value)
      End Set   
   End Property
End Class
```

Oltre ai tipi specifici elencati, alcune categorie di tipi non sono conformi a CLS, tra cui, tipi di puntatore non gestiti e tipi di puntatore a funzione. Nell'esempio seguente viene generato un avviso del compilatore perché viene usato un puntatore a un Integer per creare una matrice di Integer. 

```csharp
using System;

[assembly: CLSCompliant(true)]

public class ArrayHelper
{
   unsafe public static Array CreateInstance(Type type, int* ptr, int items)
   {
      Array arr = Array.CreateInstance(type, items);
      int* addr = ptr;
      for (int ctr = 0; ctr < items; ctr++) {
          int value = *addr;
          arr.SetValue(value, ctr);
          addr++;
      }
      return arr;
   }
}   
// The attempt to compile this example displays the following output:
//    UnmanagedPtr1.cs(8,57): warning CS3001: Argument type 'int*' is not CLS-compliant
```

```vb
using System;

[assembly: CLSCompliant(true)]

public class ArrayHelper
{
   unsafe public static Array CreateInstance(Type type, int* ptr, int items)
   {
      Array arr = Array.CreateInstance(type, items);
      int* addr = ptr;
      for (int ctr = 0; ctr < items; ctr++) {
          int value = *addr;
          arr.SetValue(value, ctr);
          addr++;
      }
      return arr;
   }
}   
// The attempt to compile this example displays the following output:
//    UnmanagedPtr1.cs(8,57): warning CS3001: Argument type 'int*' is not CLS-compliant
```

Per le classi astratte conformi a CLS (cioè quelle contrassegnate come `abstract` in C#), anche tutti i membri della classe devono essere conformi a CLS. 

### <a name="naming-conventions"></a>Convenzioni di denominazione

Poiché per alcuni linguaggi di programmazione non viene fatta distinzione tra maiuscole e minuscole, gli identificatori, ad esempio i nomi degli spazi dei nomi, i tipi e i membri, occorre che non differiscano solo per la combinazione di caratteri maiuscoli o minuscoli. Due identificatori sono considerati equivalenti se i relativi mapping di minuscole sono uguali. Nell'esempio di C# seguente vengono definite due classi pubbliche, `Person` e `person`. Poiché si differenziano solo per le maiuscole e le minuscole, dal compilatore C# vengono contrassegnate come non conformi a CLS. 

```csharp
using System;

[assembly: CLSCompliant(true)]

public class Person : person
{

}

public class person
{

}
// Compilation produces a compiler warning like the following:
//    Naming1.cs(11,14): warning CS3005: Identifier 'person' differing 
//                       only in case is not CLS-compliant
//    Naming1.cs(6,14): (Location of symbol related to previous warning)
```

Gli identificatori del linguaggio di programmazione, ad esempio i nomi degli spazi dei nomi, i tipi e i membri, devono essere conformi allo [standard Unicode 3.0, rapporto tecnico 15, allegato 7](http://www.unicode.org/reports/tr15/tr15-18.html). Vale a dire che:

* Il primo carattere di un identificatore può essere qualsiasi carattere Unicode, una lettera maiuscola, una lettera minuscola, tutte iniziali maiuscole, una lettera di modificatore, un'altra lettera o un numero rappresentato dalla lettera. Per informazioni sulle categorie di caratteri Unicode, vedere l'enumerazione [System.Globalization.UnicodeCategory](xref:System.Globalization.UnicodeCategory). 

* I caratteri successivi possono provenire da una qualsiasi delle categorie come primo carattere e in essi possono anche essere inclusi contrassegni senza spaziatura, contrassegni di combinazioni di spazi, numeri decimali, punteggiature del connettore e codici di formattazione. 

Prima di confrontare gli identificatori, è necessario filtrare i codici di formattazione e convertire gli identificatori nel formato di normalizzazione Unicode C, poiché un singolo carattere può essere rappresentato da più unità di codice codificate UTF-16. Le sequenze di caratteri che producono le stesse unità di codice nel formato di normalizzazione Unicode C non sono conformi a CLS. L'esempio seguente definisce una proprietà denominata `Å`, costituita dal carattere SEGNO di ANGSTROM (U+212B) e una seconda proprietà denominata `Å`, costituita dal carattere LETTERA LATINA A MAIUSCOLA CON UN CERCHIO SOPRA (U+00C5). Il compilatore C# contrassegna il codice sorgente come non conforme a CLS.

```csharp
public class Size
{
   private double a1;
   private double a2;

   public double Å
   {
       get { return a1; }
       set { a1 = value; }
   }         

   public double Å
   {
       get { return a2; }
       set { a2 = value; }
   }
}
// Compilation produces a compiler warning like the following:
//    Naming2a.cs(16,18): warning CS3005: Identifier 'Size.Å' differing only in case is not
//            CLS-compliant
//    Naming2a.cs(10,18): (Location of symbol related to previous warning)
//    Naming2a.cs(18,8): warning CS3005: Identifier 'Size.Å.get' differing only in case is not
//            CLS-compliant
//    Naming2a.cs(12,8): (Location of symbol related to previous warning)
//    Naming2a.cs(19,8): warning CS3005: Identifier 'Size.Å.set' differing only in case is not
//            CLS-compliant
//    Naming2a.cs(13,8): (Location of symbol related to previous warning)
```

```vb
<Assembly: CLSCompliant(True)>
Public Class Size
   Private a1 As Double
   Private a2 As Double

   Public Property Å As Double
       Get
          Return a1
       End Get
       Set 
          a1 = value
       End Set
   End Property         

   Public Property Å As Double
       Get
          Return a2
       End Get
       Set
          a2 = value
       End Set   
   End Property
End Class
' Compilation produces a compiler warning like the following:
'    Naming1.vb(9) : error BC30269: 'Public Property Å As Double' has multiple definitions
'     with identical signatures.
'    
'       Public Property Å As Double
'                       ~
```

I nomi dei membri all'interno di un ambito specifico (ad esempio gli spazi dei nomi in un assembly, i tipi in uno spazio dei nomi o i membri in un tipo) devono essere univoci ad eccezione dei nomi che vengono risolti tramite l'overload. Questo requisito è più rigido di quello di Common Type System, che consente a più membri all'interno di un ambito di disporre di nomi identici purché siano tipi diversi di membri (ad esempio, uno è un metodo e uno è un campo). In particolare, per i membri di tipo: 

* I campi e i tipi annidati vengono distinti solo in base al nome. 

* I metodi, le proprietà e gli eventi che hanno lo stesso nome devono presentare differenze che vanno oltre il solo tipo restituito. 

Nell'esempio seguente viene illustrato il requisito in base al quale i nomi dei membri devono essere univoci all'interno del relativo ambito. Viene definita una classe denominata `Converter` in cui sono inclusi quattro membri denominati `Conversion`. Tre sono metodi e uno è una proprietà. Il metodo che prevede un parametro `Int64` è denominato in modo univoco, ma i due metodi con un parametro `Int32` non lo sono, poiché il valore restituito non è considerato parte della firma di un membro. Questo requisito viene violato anche dalla proprietà `Conversion`, poiché le proprietà non possono disporre dello stesso nome dei metodi di overload. 

```csharp
using System;

[assembly: CLSCompliant(true)]

public class Converter
{
   public double Conversion(int number)
   {
      return (double) number;
   }

   public float Conversion(int number)
   {
      return (float) number;
   }

   public double Conversion(long number)
   {
      return (double) number;
   }

   public bool Conversion
   {
      get { return true; }
   }     
}  
// Compilation produces a compiler error like the following:
//    Naming3.cs(13,17): error CS0111: Type 'Converter' already defines a member called
//            'Conversion' with the same parameter types
//    Naming3.cs(8,18): (Location of symbol related to previous error)
//    Naming3.cs(23,16): error CS0102: The type 'Converter' already contains a definition for
//            'Conversion'
//    Naming3.cs(8,18): (Location of symbol related to previous error)
```

```vb
<Assembly: CLSCompliant(True)>

Public Class Converter
   Public Function Conversion(number As Integer) As Double
      Return CDbl(number)
   End Function

   Public Function Conversion(number As Integer) As Single
      Return CSng(number)
   End Function

   Public Function Conversion(number As Long) As Double
      Return CDbl(number)
   End Function

   Public ReadOnly Property Conversion As Boolean
      Get
         Return True
      End Get   
   End Property     
End Class
' Compilation produces a compiler error like the following:
'    Naming3.vb(8) : error BC30301: 'Public Function Conversion(number As Integer) As Double' 
'                    and 'Public Function Conversion(number As Integer) As Single' cannot 
'                    overload each other because they differ only by return types.
'    
'       Public Function Conversion(number As Integer) As Double
'                       ~~~~~~~~~~
'    Naming3.vb(20) : error BC30260: 'Conversion' is already declared as 'Public Function 
'                     Conversion(number As Integer) As Single' in this class.
'    
'       Public ReadOnly Property Conversion As Boolean
'                                ~~~~~~~~~~
```

Nei singoli linguaggi sono incluse parole chiave univoche, pertanto i linguaggi destinati a Common Language Runtime devono fornire anche un meccanismo di riferimento agli identificatori (ad esempio nomi di tipi) che coincidono con le parole chiave. Ad esempio, `case` è una parola chiave sia in C# sia in Visual Basic. Tuttavia, nell'esempio di Visual Basic seguente è possibile evitare ambiguità relative a una classe denominata `case` dalla parola chiave `case` usando le parentesi graffe di apertura e chiusura. In caso contrario, nell'esempio verrà generato il messaggio di errore "Parola chiave non valida come identificatore" e la compilazione non verrà completata. 

```vb
Public Class [case]
   Private _id As Guid
   Private name As String  

   Public Sub New(name As String)
      _id = Guid.NewGuid()
      Me.name = name 
   End Sub   

   Public ReadOnly Property ClientName As String
      Get
         Return name
      End Get
   End Property
End Class
```

Nell'esempio C# seguente viene creata un'istanza della classe `case` usando il simbolo @ per distinguere l'identificatore dalla parola chiave del linguaggio. Senza, tramite il compilatore C# verrebbero visualizzati due messaggi di errore, "È previsto un tipo" e "'case' è un termine non valido nell'espressione". 

```csharp
using System;

public class Example
{
   public static void Main()
   {
      @case c = new @case("John");
      Console.WriteLine(c.ClientName);
   }
}
```

### <a name="type-conversion"></a>Conversione di tipi

Tramite le specifiche CLS (Common Language Specification) vengono definiti due operatori di conversione:

* `op_Implicit`, che viene usato per le conversioni verso un tipo di dati più grande che non comportano la perdita di dati o di precisione. Ad esempio, nella struttura [Decimal](xref:System.Decimal) è incluso un operatore `op_Implicit` di overload per convertire i valori di tipi integrali e i valori [Char](xref:System.Char) in valori `Decimal`. 

* `op_Explicit`, che viene usato per le conversioni verso un tipo di dati più piccolo che possono comportare la perdita di grandezza (un valore viene convertito in un altro a cui è associato un intervallo inferiore) o di precisione. Ad esempio, nella struttura `Decimal` è incluso un operatore `op_Explicit` di overload per convertire i valori [Double](xref:System.Double) e [Single](xref:System.Single) in `Decimal` e per convertire i valori `Decimal` in valori integrali `Double`, `Single` e `Char`. 

Tuttavia, non tutti i linguaggi supportano l'overload degli operatori o la definizione di operatori personalizzati. Se si sceglie di implementare questi operatori di conversione, è necessario fornire anche un modo alternativo per eseguire la conversione. È consigliabile fornire i metodi `From`Xxx e `To`Xxx. 

Nell'esempio seguente vengono definite le convenzioni esplicite e implicite conformi a CLS. Viene creata una classe `UDouble` che rappresenta un numero a virgola mobile e precisione doppia con segno. Viene usato per le conversioni implicite da `UDouble` a `Double` e per le conversioni esplicite da `UDouble` a `Single`, da `Double` a `UDouble` e da `Single` a `UDouble`. Vengono anche definiti un metodo `ToDouble` come alternativa all'operatore di conversione implicito e i metodi `ToSingle`, `FromDouble` e `FromSingle` come alternative agli operatori di conversione espliciti. 

```csharp
using System;

public struct UDouble
{
   private double number;

   public UDouble(double value)
   {
      if (value < 0)
         throw new InvalidCastException("A negative value cannot be converted to a UDouble.");

      number = value;
   }

   public UDouble(float value)
   {
      if (value < 0)
         throw new InvalidCastException("A negative value cannot be converted to a UDouble.");

      number = value;
   }

   public static readonly UDouble MinValue = (UDouble) 0.0;
   public static readonly UDouble MaxValue = (UDouble) Double.MaxValue;

   public static explicit operator Double(UDouble value)
   {
      return value.number;
   }

   public static implicit operator Single(UDouble value)
   {
      if (value.number > (double) Single.MaxValue) 
         throw new InvalidCastException("A UDouble value is out of range of the Single type.");

      return (float) value.number;         
   }

   public static explicit operator UDouble(double value)
   {
      if (value < 0)
         throw new InvalidCastException("A negative value cannot be converted to a UDouble.");

      return new UDouble(value);
   } 

   public static implicit operator UDouble(float value)
   {
      if (value < 0)
         throw new InvalidCastException("A negative value cannot be converted to a UDouble.");

      return new UDouble(value);
   } 

   public static Double ToDouble(UDouble value)
   {
      return (Double) value;
   }   

   public static float ToSingle(UDouble value)
   {
      return (float) value;
   }   

   public static UDouble FromDouble(double value)
   {
      return new UDouble(value);
   }

   public static UDouble FromSingle(float value)
   {
      return new UDouble(value);
   }   
}
```

```vb
Public Structure UDouble
   Private number As Double

   Public Sub New(value As Double)
      If value < 0 Then
         Throw New InvalidCastException("A negative value cannot be converted to a UDouble.")
      End If
      number = value
   End Sub

   Public Sub New(value As Single)
      If value < 0 Then
         Throw New InvalidCastException("A negative value cannot be converted to a UDouble.")
      End If
      number = value
   End Sub

   Public Shared ReadOnly MinValue As UDouble = CType(0.0, UDouble)
   Public Shared ReadOnly MaxValue As UDouble = Double.MaxValue

   Public Shared Widening Operator CType(value As UDouble) As Double
      Return value.number
   End Operator

   Public Shared Narrowing Operator CType(value As UDouble) As Single
      If value.number > CDbl(Single.MaxValue) Then
         Throw New InvalidCastException("A UDouble value is out of range of the Single type.")
      End If
      Return CSng(value.number)         
   End Operator

   Public Shared Narrowing Operator CType(value As Double) As UDouble
      If value < 0 Then
         Throw New InvalidCastException("A negative value cannot be converted to a UDouble.")
      End If
      Return New UDouble(value)
   End Operator 

   Public Shared Narrowing Operator CType(value As Single) As UDouble
      If value < 0 Then
         Throw New InvalidCastException("A negative value cannot be converted to a UDouble.")
      End If
      Return New UDouble(value)
   End Operator 

   Public Shared Function ToDouble(value As UDouble) As Double
      Return CType(value, Double)
   End Function   

   Public Shared Function ToSingle(value As UDouble) As Single
      Return CType(value, Single)
   End Function   

   Public Shared Function FromDouble(value As Double) As UDouble
      Return New UDouble(value)
   End Function

   Public Shared Function FromSingle(value As Single) As UDouble
      Return New UDouble(value)
   End Function   
End Structure
```

### <a name="arrays"></a>Matrici

Le matrici conformi a CLS sono conformi alle regole seguenti: 

* Il limite inferiore di tutte le dimensioni di una matrice deve essere uguale a zero. Nell'esempio seguente viene creata una matrice non conforme a CLS con un limite inferiore pari a uno. Si noti che, nonostante la presenza dell'attributo [CLSCompliantAttribute](xref:System.CLSCompliantAttribute), il compilatore non rileva che la matrice restituita dal metodo `Numbers.GetTenPrimes` non è conforme a CLS. 

  ```csharp
  [assembly: CLSCompliant(true)]

  public class Numbers
  {
    public static Array GetTenPrimes()
    {
        Array arr = Array.CreateInstance(typeof(Int32), new int[] {10}, new int[] {1});
        arr.SetValue(1, 1);
        arr.SetValue(2, 2);
        arr.SetValue(3, 3);
        arr.SetValue(5, 4);
        arr.SetValue(7, 5);
        arr.SetValue(11, 6); 
        arr.SetValue(13, 7);
        arr.SetValue(17, 8);
        arr.SetValue(19, 9);
        arr.SetValue(23, 10);

        return arr; 
    }
  }
  ```

  ```vb
  <Assembly: CLSCompliant(True)>

  Public Class Numbers
     Public Shared Function GetTenPrimes() As Array
        Dim arr As Array = Array.CreateInstance(GetType(Int32), {10}, {1})
        arr.SetValue(1, 1)
        arr.SetValue(2, 2)
        arr.SetValue(3, 3)
        arr.SetValue(5, 4)
        arr.SetValue(7, 5)
        arr.SetValue(11, 6)
        arr.SetValue(13, 7)
        arr.SetValue(17, 8)
        arr.SetValue(19, 9)
        arr.SetValue(23, 10)
        Return arr
     End Function
  End Class
  ```

* Tutti gli elementi delle matrici devono essere costituiti da tipi conformi a CLS. Nell'esempio seguente vengono definiti due metodi tramite cui vengono restituite matrici non conformi a CLS. Il primo restituisce una matrice di valori [UInt32](xref:System.UInt32). Il secondo restituisce una matrice [Object](xref:System.Object) che include valori [Int32](xref:System.Int32) e `UInt32`. Anche se il compilatore consente di identificare la prima matrice come non conforme a causa del relativo tipo `UInt32`, non è in grado di riconoscere che nella seconda matrice sono inclusi elementi non conformi a CLS. 

  ```csharp
  using System;

  [assembly: CLSCompliant(true)]

  public class Numbers
  {
    public static UInt32[] GetTenPrimes()
    {
        uint[] arr = { 1u, 2u, 3u, 5u, 7u, 11u, 13u, 17u, 19u };
        return arr;
    }

    public static Object[] GetFivePrimes()
    {
        Object[] arr = { 1, 2, 3, 5u, 7u };
        return arr;
    }
  }
  // Compilation produces a compiler warning like the following:
  //    Array2.cs(8,27): warning CS3002: Return type of 'Numbers.GetTenPrimes()' is not
  //            CLS-compliant
  ```

  ```vb
  <Assembly: CLSCompliant(True)>

  Public Class Numbers
     Public Shared Function GetTenPrimes() As UInt32()
        Return { 1ui, 2ui, 3ui, 5ui, 7ui, 11ui, 13ui, 17ui, 19ui }
     End Function
     Public Shared Function GetFivePrimes() As Object()
        Dim arr() As Object = { 1, 2, 3, 5ui, 7ui }
        Return arr
     End Function
  End Class
  ' Compilation produces a compiler warning like the following:
  '    warning BC40027: Return type of function 'GetTenPrimes' is not CLS-compliant.
  ```                             

* La risoluzione dell'overload per i metodi a cui sono associati parametri di matrice è basata sul fatto che si tratta di matrici e sul relativo tipo di elemento. Per questo motivo, la seguente definizione di un metodo `GetSquares` di overload è conforme a CLS. 

  ```csharp
  using System;
  using System.Numerics;

  [assembly: CLSCompliant(true)]

  public class Numbers
  {
    public static byte[] GetSquares(byte[] numbers)
    {
        byte[] numbersOut = new byte[numbers.Length];
        for (int ctr = 0; ctr < numbers.Length; ctr++) {
            int square = ((int) numbers[ctr]) * ((int) numbers[ctr]); 
            if (square <= Byte.MaxValue)
                numbersOut[ctr] = (byte) square;
            // If there's an overflow, assign MaxValue to the corresponding 
            // element.
            else
                numbersOut[ctr] = Byte.MaxValue;

        }
        return numbersOut;
    }

    public static BigInteger[] GetSquares(BigInteger[] numbers)
  {
        BigInteger[] numbersOut = new BigInteger[numbers.Length];
        for (int ctr = 0; ctr < numbers.Length; ctr++)
            numbersOut[ctr] = numbers[ctr] * numbers[ctr]; 

       return numbersOut;
    }
  }
  ```

  ```vb
  Imports System.Numerics

  <Assembly: CLSCompliant(True)>

  Public Module Numbers
     Public Function GetSquares(numbers As Byte()) As Byte()
        Dim numbersOut(numbers.Length - 1) As Byte
        For ctr As Integer = 0 To numbers.Length - 1
           Dim square As Integer = (CInt(numbers(ctr)) * CInt(numbers(ctr))) 
           If square <= Byte.MaxValue Then
              numbersOut(ctr) = CByte(square)
           ' If there's an overflow, assign MaxValue to the corresponding 
           ' element.
           Else
              numbersOut(ctr) = Byte.MaxValue
           End If   
        Next
        Return numbersOut
     End Function

     Public Function GetSquares(numbers As BigInteger()) As BigInteger()
         Dim numbersOut(numbers.Length - 1) As BigInteger
         For ctr As Integer = 0 To numbers.Length - 1
            numbersOut(ctr) = numbers(ctr) * numbers(ctr) 
         Next
         Return numbersOut
     End Function
  End Module
```

### <a name="interfaces"></a>Interfacce

Tramite interfacce conformi a CLS è possibile definire proprietà, eventi e metodi virtuali (metodi senza l'implementazione). Un'interfaccia conforme a CLS non può disporre di uno dei seguenti valori: 

* Metodi o campi statici. Se si definisce un membro statico in un'interfaccia, il compilatore C# genera errori del compilatore. 

* Campi. Se si definisce un campo in un'interfaccia, il compilatore C# genera errori del compilatore.

* Metodi non conformi a CLS. Ad esempio, nella definizione dell'interfaccia seguente è incluso un metodo, `INumber.GetUnsigned`, che è contrassegnato come non conforme a CLS. In questo esempio verrà generato un avviso del compilatore. 

  ```csharp
  using System;

  [assembly:CLSCompliant(true)]

  public interface INumber
  {
      int Length();
      [CLSCompliant(false)] ulong GetUnsigned();
  }
  // Attempting to compile the example displays output like the following:
  //    Interface2.cs(8,32): warning CS3010: 'INumber.GetUnsigned()': CLS-compliant interfaces
  //            must have only CLS-compliant members
  ```

  ```vb
  <Assembly: CLSCompliant(True)>

  Public Interface INumber
    Function Length As Integer
      <CLSCompliant(False)> Function GetUnsigned As ULong   
    End Interface
    ' Attempting to compile the example displays output like the following:
    '    Interface2.vb(9) : warning BC40033: Non CLS-compliant 'function' is not allowed in a 
    '    CLS-compliant interface.
    '    
    '       <CLSCompliant(False)> Function GetUnsigned As ULong
    '                                      ~~~~~~~~~~~
  ```

  A causa di questa regola, i tipi conformi a CLS non sono necessari per l'implementazione di membri non conformi a CLS. Se tramite un framework conforme a CLS viene esposta una classe mediante la quale viene implementata un'interfaccia non conforme a CLS, è anche consigliabile fornire implementazioni concrete di tutti i membri non conformi a CLS. 

I compilatori di linguaggi conformi a CLS devono anche consentire a una classe di fornire implementazioni separate di membri con lo stesso nome e la stessa firma in più interfacce. C# supporta implementazioni di interfacce esplicite per fornire diverse implementazioni di metodi denominati in modo identico. Nell'esempio seguente viene illustrato questo scenario definendo una classe `Temperature` mediante la quale vengono implementate le interfacce `ICelsius` e `IFahrenheit` come implementazioni di interfacce esplicite. 

```csharp
using System;

[assembly: CLSCompliant(true)]

public interface IFahrenheit
{
   decimal GetTemperature();
}

public interface ICelsius
{
   decimal GetTemperature();
}

public class Temperature : ICelsius, IFahrenheit
{
   private decimal _value;

   public Temperature(decimal value)
   {
      // We assume that this is the Celsius value.
      _value = value;
   } 

   decimal IFahrenheit.GetTemperature()
   {
      return _value * 9 / 5 + 32;
   }

   decimal ICelsius.GetTemperature()
   {
      return _value;
   } 
}
public class Example
{
   public static void Main()
   {
      Temperature temp = new Temperature(100.0m);
      ICelsius cTemp = temp;
      IFahrenheit fTemp = temp;
      Console.WriteLine("Temperature in Celsius: {0} degrees", 
                        cTemp.GetTemperature());
      Console.WriteLine("Temperature in Fahrenheit: {0} degrees", 
                        fTemp.GetTemperature());
   }
}
// The example displays the following output:
//       Temperature in Celsius: 100.0 degrees
//       Temperature in Fahrenheit: 212.0 degrees
```

```vb
Assembly: CLSCompliant(True)>

Public Interface IFahrenheit
   Function GetTemperature() As Decimal
End Interface

Public Interface ICelsius
   Function GetTemperature() As Decimal
End Interface

Public Class Temperature : Implements ICelsius, IFahrenheit
   Private _value As Decimal

   Public Sub New(value As Decimal)
      ' We assume that this is the Celsius value.
      _value = value
   End Sub 

   Public Function GetFahrenheit() As Decimal _
          Implements IFahrenheit.GetTemperature
      Return _value * 9 / 5 + 32
   End Function

   Public Function GetCelsius() As Decimal _
          Implements ICelsius.GetTemperature
      Return _value
   End Function 
End Class

Module Example
   Public Sub Main()
      Dim temp As New Temperature(100.0d)
      Console.WriteLine("Temperature in Celsius: {0} degrees", 
                        temp.GetCelsius())
      Console.WriteLine("Temperature in Fahrenheit: {0} degrees", 
                        temp.GetFahrenheit())
   End Sub
End Module
' The example displays the following output:
'       Temperature in Celsius: 100.0 degrees
'       Temperature in Fahrenheit: 212.0 degrees
```

### <a name="enumerations"></a>Enumerazioni

Le enumerazioni conformi a CLS devono rispettare queste regole: 

* Il tipo sottostante dell'enumerazione deve essere un Integer intrinseco conforme a CLS ([Byte](xref:System.Byte), [Int16](xref:System.Int16), [Int32](xref:System.Int32) o [Int64](xref:System.Int64)). Ad esempio, il codice seguente tenta di definire un'enumerazione il cui tipo sottostante è [UInt32](xref:System.UInt32) e genera un avviso del compilatore. 

    ```csharp
    using System;

    [assembly: CLSCompliant(true)]

    public enum Size : uint { 
        Unspecified = 0, 
        XSmall = 1, 
        Small = 2, 
        Medium = 3, 
        Large = 4, 
        XLarge = 5 
    };

    public class Clothing
    {
        public string Name; 
        public string Type;
        public string Size;
    }
    // The attempt to compile the example displays a compiler warning like the following:
    //    Enum3.cs(6,13): warning CS3009: 'Size': base type 'uint' is not CLS-compliant
    ```

    ```vb
    <Assembly: CLSCompliant(True)>

    Public Enum Size As UInt32
       Unspecified = 0
       XSmall = 1
       Small = 2
       Medium = 3
       Large = 4
       XLarge = 5
    End Enum

    Public Class Clothing
       Public Name As String
       Public Type As String
       Public Size As Size
    End Class
    ' The attempt to compile the example displays a compiler warning like the following:
    '    Enum3.vb(6) : warning BC40032: Underlying type 'UInt32' of Enum is not CLS-compliant.
    '    
    '    Public Enum Size As UInt32
    '                ~~~~
    ```

* Un tipo di enumerazione deve avere un singolo campo di istanza denominato `Value__` contrassegnato con l'attributo `FieldAttributes.RTSpecialName`. Ciò consente di fare riferimento al valore del campo in modo implicito. 

* Un'enumerazione prevede campi statici con valori letterali i cui tipi corrispondono al tipo dell'enumerazione stessa. Ad esempio, se si definisce un'enumerazione `State` con valori `State.On` e `State.Off`, `State.On` e `State.Off` sono entrambi campi statici con valori letterali il cui tipo è `State`. 

* Vi sono due tipi di enumerazioni: 
    
    * Enumerazione che rappresenta un set di Integer denominati che si escludono a vicenda. Questo tipo di enumerazione è indicato dall'assenza dell'attributo personalizzato [System.FlagsAttribute](xref:System.FlagsAttribute).
    
    * Enumerazione che rappresenta un set di flag di bit che possono essere combinati per generare un valore senza nome. Questo tipo di enumerazione è indicato dalla presenza dell'attributo personalizzato [System.FlagsAttribute](xref:System.FlagsAttribute).
    
 Per altre informazioni, vedere la documentazione relativa alla struttura [Enum](xref:System.Enum). 

* Il valore di un'enumerazione non è limitato all'intervallo dei relativi valori specificati. In altre parole, l'intervallo di valori in una enumerazione è l'intervallo del relativo valore sottostante. È possibile usare il metodo `Enum.IsDefined` per determinare se un valore specificato è un membro di un'enumerazione. 

### <a name="type-members-in-general"></a>Membri dei tipi in generale

In base alle specifiche CLS (Common Language Specification), l'accesso a tutti i campi e metodi deve essere effettuato come membri di una classe particolare. Pertanto, i metodi e i campi statici globali, vale a dire metodi o campi statici definiti oltre a un tipo, non sono conformi a CLS. Se si tenta di includere un campo o un metodo globale nel codice sorgente, il compilatore C# genera un errore del compilatore. 

Le specifiche CLS (Common Language Specification) supportano solo la convenzione di chiamata gestita standard. Non supportano le convenzioni di chiamata non gestite né i metodi con elenchi di argomenti variabili contrassegnati con la parola chiave `varargs`. Per gli elenchi di argomenti variabili compatibili con la convenzione di chiamata gestita standard, usare l'attributo [ParamArrayAttribute](xref:System.ParamArrayAttribute) o l'implementazione del singolo linguaggio, ad esempio la parola chiave `params` in C# e la parola chiave `ParamArray` in Visual Basic. 

### <a name="member-accessibility"></a>Accessibilità del membro

Tramite l'override di un membro ereditato non è possibile modificare l'accessibilità del membro in questione. Ad esempio, un metodo pubblico in una classe di base non può essere sottoposto a override da un metodo privato in una classe derivata. Vi è un'eccezione: un membro `protected internal` (in C#) o `Protected Friend` (in Visual Basic) in un assembly sottoposto a override da un tipo in un assembly diverso.  In questo caso, l'accessibilità dell'override è `Protected`. 

L'esempio seguente mostra l'errore generato quando l'attributo [CLSCompliantAttribute](xref:System.CLSCompliantAttribute) è impostato su `true` e `Person`, cioè una classe derivata da `Animal`, tenta di modificare l'accessibilità della proprietà `Species` da pubblica a privata. L'esempio viene compilato correttamente se la relativa accessibilità è stata modificata in pubblica. 

```csharp
using System;

[assembly: CLSCompliant(true)]

public class Animal
{
   private string _species;

   public Animal(string species)
   {
      _species = species;
   }

   public virtual string Species 
   {    
      get { return _species; }
   }

   public override string ToString()
   {
      return _species;   
   } 
}

public class Human : Animal
{
   private string _name;

   public Human(string name) : base("Homo Sapiens")
   {
      _name = name;
   }

   public string Name
   {
      get { return _name; }
   }

   private override string Species 
   {
      get { return base.Species; }
   }

   public override string ToString() 
   {
      return _name;
   }
}

public class Example
{
   public static void Main()
   {
      Human p = new Human("John");
      Console.WriteLine(p.Species);
      Console.WriteLine(p.ToString());
   }
}
// The example displays the following output:
//    error CS0621: 'Human.Species': virtual or abstract members cannot be private
```

```vb
<Assembly: CLSCompliant(True)>

Public Class Animal
   Private _species As String

   Public Sub New(species As String)
      _species = species
   End Sub

   Public Overridable ReadOnly Property Species As String
      Get
         Return _species
      End Get
   End Property

   Public Overrides Function ToString() As String
      Return _species   
   End Function 
End Class

Public Class Human : Inherits Animal
   Private _name As String

   Public Sub New(name As String)
      MyBase.New("Homo Sapiens")
      _name = name
   End Sub

   Public ReadOnly Property Name As String
      Get
         Return _name
      End Get
   End Property

   Private Overrides ReadOnly Property Species As String
      Get
         Return MyBase.Species
      End Get   
   End Property

   Public Overrides Function ToString() As String
      Return _name
   End Function
End Class

Public Module Example
   Public Sub Main()
      Dim p As New Human("John")
      Console.WriteLine(p.Species)
      Console.WriteLine(p.ToString())
   End Sub
End Module
' The example displays the following output:
'     'Private Overrides ReadOnly Property Species As String' cannot override 
'     'Public Overridable ReadOnly Property Species As String' because
'      they have different access levels.
' 
'         Private Overrides ReadOnly Property Species As String
```

I tipi nella firma di un membro devono essere accessibili ogni volta che il membro è accessibile. Questo significa, ad esempio, che un membro pubblico non può includere un parametro il cui tipo è privato, protetto o interno. Nell'esempio seguente viene illustrato l'errore del compilatore generato quando tramite un costruttore di classe `StringWrapper` viene esposto un valore di enumerazione `StringOperationType` interno con cui si determina la modalità di esecuzione del wrapping di un valore stringa. 

```csharp
using System;
using System.Text;

public class StringWrapper
{
   string internalString;
   StringBuilder internalSB = null;
   bool useSB = false;

   public StringWrapper(StringOperationType type)
   {   
      if (type == StringOperationType.Normal) {
         useSB = false;
      }   
      else {
         useSB = true;
         internalSB = new StringBuilder();
      }    
   }

   // The remaining source code...
}

internal enum StringOperationType { Normal, Dynamic }
// The attempt to compile the example displays the following output:
//    error CS0051: Inconsistent accessibility: parameter type
//            'StringOperationType' is less accessible than method
//            'StringWrapper.StringWrapper(StringOperationType)'
```

```vb
Imports System.Text

<Assembly:CLSCompliant(True)>

Public Class StringWrapper

   Dim internalString As String
   Dim internalSB As StringBuilder = Nothing
   Dim useSB As Boolean = False

   Public Sub New(type As StringOperationType)   
      If type = StringOperationType.Normal Then
         useSB = False
      Else
         internalSB = New StringBuilder() 
         useSB = True
      End If    
   End Sub

   ' The remaining source code...
End Class

Friend Enum StringOperationType As Integer
   Normal = 0
   Dynamic = 1
End Enum
' The attempt to compile the example displays the following output:
'    error BC30909: 'type' cannot expose type 'StringOperationType'
'     outside the project through class 'StringWrapper'.
'    
'       Public Sub New(type As StringOperationType)
'                              ~~~~~~~~~~~~~~~~~~~
```

### <a name="generic-types-and-members"></a>Tipi e membri generici

I tipi annidati dispongono sempre di un numero di parametri generici almeno pari a quelli del relativo tipo di inclusione. Questi corrispondono per posizione ai parametri generici del tipo di inclusione. Il tipo generico può anche prevedere nuovi parametri generici. 

La relazione tra i parametri di tipo generico di un tipo contenitore e i relativi tipi annidati può essere nascosta dalla sintassi dei singoli linguaggi. Nell'esempio seguente in un tipo generico `Outer<T>` sono contenute due classi annidate, `Inner1A` e `Inner1B<U>`. Le chiamate al metodo `ToString`, che ogni classe eredita da `Object.ToString`, mostrano che in ogni classe annidata sono inclusi i parametri di tipo della relativa classe che li contiene. 

```csharp
using System;

[assembly:CLSCompliant(true)]

public class Outer<T>
{
   T value;

   public Outer(T value)
   {
      this.value = value;
   }

   public class Inner1A : Outer<T>
   {
      public Inner1A(T value) : base(value)
      {  }
   }

   public class Inner1B<U> : Outer<T>
   {
      U value2;

      public Inner1B(T value1, U value2) : base(value1)
      {
         this.value2 = value2;
      }
   }
}

public class Example
{
   public static void Main()
   {
      var inst1 = new Outer<String>("This");
      Console.WriteLine(inst1);

      var inst2 = new Outer<String>.Inner1A("Another");
      Console.WriteLine(inst2);

      var inst3 = new Outer<String>.Inner1B<int>("That", 2);
      Console.WriteLine(inst3);
   }
}
// The example displays the following output:
//       Outer`1[System.String]
//       Outer`1+Inner1A[System.String]
//       Outer`1+Inner1B`1[System.String,System.Int32]
```

```vb
<Assembly:CLSCompliant(True)>

Public Class Outer(Of T)
   Dim value As T

   Public Sub New(value As T)
      Me.value = value
   End Sub

   Public Class Inner1A : Inherits Outer(Of T)
      Public Sub New(value As T)
         MyBase.New(value)
      End Sub
   End Class

   Public Class Inner1B(Of U) : Inherits Outer(Of T)
      Dim value2 As U

      Public Sub New(value1 As T, value2 As U)
         MyBase.New(value1)
         Me.value2 = value2
      End Sub
   End Class
End Class

Public Module Example
   Public Sub Main()
      Dim inst1 As New Outer(Of String)("This")
      Console.WriteLine(inst1)

      Dim inst2 As New Outer(Of String).Inner1A("Another")
      Console.WriteLine(inst2)

      Dim inst3 As New Outer(Of String).Inner1B(Of Integer)("That", 2)
      Console.WriteLine(inst3)
   End Sub
End Module
' The example displays the following output:
'       Outer`1[System.String]
'       Outer`1+Inner1A[System.String]
'       Outer`1+Inner1B`1[System.String,System.Int32]
```

I nomi di tipo generico sono codificati nel formato *name*'*n*, dove *name* è il nome del tipo, *`* è un valore letterale del carattere e *n* è il numero di parametri dichiarati nel tipo oppure, per i tipi generici annidati, il numero di parametri di tipo appena introdotti. Questa codifica dei nomi di tipo generico è principalmente di interesse per gli sviluppatori che usano la reflection per accedere ai tipi generici conformi a CLS in una libreria. 

Se i vincoli vengono applicati a un tipo generico, anche tutti i tipi usati come vincoli devono essere conformi a CLS. Nell'esempio seguente viene definita una classe denominata `BaseClass` che non è conforme a CLS e una classe generica denominata `BaseCollection` il cui parametro di tipo deve derivare da `BaseClass`. Tuttavia, poiché `BaseClass` non è conforme a CLS, il compilatore genera un avviso. 

```csharp
using System;

[assembly:CLSCompliant(true)]

[CLSCompliant(false)] public class BaseClass
{}


public class BaseCollection<T> where T : BaseClass
{}
// Attempting to compile the example displays the following output:
//    warning CS3024: Constraint type 'BaseClass' is not CLS-compliant
```

```vb
Assembly: CLSCompliant(True)>

<CLSCompliant(False)> Public Class BaseClass
End Class


Public Class BaseCollection(Of T As BaseClass)
End Class
' Attempting to compile the example displays the following output:
'    warning BC40040: Generic parameter constraint type 'BaseClass' is not 
'    CLS-compliant.
'    
'    Public Class BaseCollection(Of T As BaseClass)
'                                        ~~~~~~~~~

```

Se un tipo generico è derivato da un tipo base generico, è necessario dichiarare nuovamente tutti i vincoli in modo che sia possibile garantire che vengano soddisfatti anche i vincoli sul tipo base. Nell'esempio riportato di seguito viene definito un oggetto `Number<T>` che può rappresentare qualsiasi tipo numerico. Viene anche definita una classe `FloatingPoint<T>` che rappresenta un valore a virgola mobile. Tuttavia, il codice sorgente non viene compilato, perché non viene applicato il vincolo su `Number<T>` (che T deve essere un tipo di valore) a `FloatingPoint<T>`.

```csharp
using System;

[assembly:CLSCompliant(true)]

public class Number<T> where T : struct
{
   // use Double as the underlying type, since its range is a superset of
   // the ranges of all numeric types except BigInteger.
   protected double number;

   public Number(T value)
   {
      try {
         this.number = Convert.ToDouble(value);
      }  
      catch (OverflowException e) {
         throw new ArgumentException("value is too large.", e);
      }
      catch (InvalidCastException e) {
         throw new ArgumentException("The value parameter is not numeric.", e);
      }
   }

   public T Add(T value)
   {
      return (T) Convert.ChangeType(number + Convert.ToDouble(value), typeof(T));
   }

   public T Subtract(T value)
   {
      return (T) Convert.ChangeType(number - Convert.ToDouble(value), typeof(T));
   }
}

public class FloatingPoint<T> : Number<T> 
{
   public FloatingPoint(T number) : base(number) 
   {
      if (typeof(float) == number.GetType() ||
          typeof(double) == number.GetType() || 
          typeof(decimal) == number.GetType())
         this.number = Convert.ToDouble(number);
      else   
         throw new ArgumentException("The number parameter is not a floating-point number.");
   }       
}           
// The attempt to comple the example displays the following output:
//       error CS0453: The type 'T' must be a non-nullable value type in
//               order to use it as parameter 'T' in the generic type or method 'Number<T>'
```

```vb
<Assembly:CLSCompliant(True)>

Public Class Number(Of T As Structure)
   ' Use Double as the underlying type, since its range is a superset of
   ' the ranges of all numeric types except BigInteger.
   Protected number As Double

   Public Sub New(value As T)
      Try
         Me.number = Convert.ToDouble(value)
      Catch e As OverflowException
         Throw New ArgumentException("value is too large.", e)
      Catch e As InvalidCastException
         Throw New ArgumentException("The value parameter is not numeric.", e)
      End Try
   End Sub

   Public Function Add(value As T) As T
      Return CType(Convert.ChangeType(number + Convert.ToDouble(value), GetType(T)), T)
   End Function

   Public Function Subtract(value As T) As T
      Return CType(Convert.ChangeType(number - Convert.ToDouble(value), GetType(T)), T)
   End Function
End Class

Public Class FloatingPoint(Of T) : Inherits Number(Of T) 
   Public Sub New(number As T)
      MyBase.New(number) 
      If TypeOf number Is Single Or
               TypeOf number Is Double Or
               TypeOf number Is Decimal Then 
         Me.number = Convert.ToDouble(number)
      Else   
         throw new ArgumentException("The number parameter is not a floating-point number.")
      End If   
   End Sub       
End Class           
' The attempt to comple the example displays the following output:
'    error BC32105: Type argument 'T' does not satisfy the 'Structure'
'    constraint for type parameter 'T'.
'    
'    Public Class FloatingPoint(Of T) : Inherits Number(Of T)
'                                                          ~
```

L'esempio viene compilato correttamente se il vincolo viene aggiunto alla classe `FloatingPoint<T>`.

```csharp
using System;

[assembly:CLSCompliant(true)]


public class Number<T> where T : struct
{
   // use Double as the underlying type, since its range is a superset of
   // the ranges of all numeric types except BigInteger.
   protected double number;

   public Number(T value)
   {
      try {
         this.number = Convert.ToDouble(value);
      }  
      catch (OverflowException e) {
         throw new ArgumentException("value is too large.", e);
      }
      catch (InvalidCastException e) {
         throw new ArgumentException("The value parameter is not numeric.", e);
      }
   }

   public T Add(T value)
   {
      return (T) Convert.ChangeType(number + Convert.ToDouble(value), typeof(T));
   }

   public T Subtract(T value)
   {
      return (T) Convert.ChangeType(number - Convert.ToDouble(value), typeof(T));
   }
}

public class FloatingPoint<T> : Number<T> where T : struct 
{
   public FloatingPoint(T number) : base(number) 
   {
      if (typeof(float) == number.GetType() ||
          typeof(double) == number.GetType() || 
          typeof(decimal) == number.GetType())
         this.number = Convert.ToDouble(number);
      else   
         throw new ArgumentException("The number parameter is not a floating-point number.");
   }       
}      
```

```vb
<Assembly:CLSCompliant(True)>

Public Class Number(Of T As Structure)
   ' Use Double as the underlying type, since its range is a superset of
   ' the ranges of all numeric types except BigInteger.
   Protected number As Double

   Public Sub New(value As T)
      Try
         Me.number = Convert.ToDouble(value)
      Catch e As OverflowException
         Throw New ArgumentException("value is too large.", e)
      Catch e As InvalidCastException
         Throw New ArgumentException("The value parameter is not numeric.", e)
      End Try
   End Sub

   Public Function Add(value As T) As T
      Return CType(Convert.ChangeType(number + Convert.ToDouble(value), GetType(T)), T)
   End Function

   Public Function Subtract(value As T) As T
      Return CType(Convert.ChangeType(number - Convert.ToDouble(value), GetType(T)), T)
   End Function
End Class

Public Class FloatingPoint(Of T As Structure) : Inherits Number(Of T) 
   Public Sub New(number As T)
      MyBase.New(number) 
      If TypeOf number Is Single Or
               TypeOf number Is Double Or
               TypeOf number Is Decimal Then 
         Me.number = Convert.ToDouble(number)
      Else   
         throw new ArgumentException("The number parameter is not a floating-point number.")
      End If   
   End Sub       
End Class
```

Le specifiche CLS (Common Language Specification) impongono un modello conservativo per creazione di istanze per tipi annidati e membri protetti. Tramite i tipi generici aperti non è possibile esporre campi o membri con firme contenenti la creazione di un'istanza specifica di un tipo generico annidato e protetto. Tramite i tipi non generici, mediante i quali viene estesa la creazione di un'istanza specifica di un'interfaccia o di una classe di base generica, non è possibile esporre i campi o i membri con firme contenenti la creazione di un'istanza differente di un tipo generico annidato e protetto.

Nell'esempio seguente vengono definiti un tipo generico, `C1<T>`, e una classe protetta `C1<T>.N`. L'oggetto `C1<T>` dispone di due metodi: `M1` e `M2`. Tuttavia, `M1` non è conforme a CLS poiché tenta di restituire un oggetto `C1<int>.N` da `C1<T>`. Una seconda classe, `C2`, viene derivata da `C1<long>`. Dispone di due metodi, `M3` e `M4`. `M3` non è conforme a CLS perché prova a restituire un oggetto `C1<int>.N` da una sottoclasse di `C1<long>`. Si noti che i compilatori di linguaggio possono essere anche più restrittivi. In questo esempio in Visual Basic viene visualizzato un errore quando viene eseguito un tentativo di compilazione di `M4`. 

```csharp
using System;

[assembly:CLSCompliant(true)]

public class C1<T> 
{
   protected class N { }

   protected void M1(C1<int>.N n) { } // Not CLS-compliant - C1<int>.N not
                                      // accessible from within C1<T> in all
                                      // languages
   protected void M2(C1<T>.N n) { }   // CLS-compliant – C1<T>.N accessible
                                      // inside C1<T>
}

public class C2 : C1<long> 
{
   protected void M3(C1<int>.N n) { }  // Not CLS-compliant – C1<int>.N is not
                                       // accessible in C2 (extends C1<long>)

   protected void M4(C1<long>.N n) { } // CLS-compliant, C1<long>.N is
                                       // accessible in C2 (extends C1<long>)
}
// Attempting to compile the example displays output like the following:
//       Generics4.cs(9,22): warning CS3001: Argument type 'C1<int>.N' is not CLS-compliant
//       Generics4.cs(18,22): warning CS3001: Argument type 'C1<int>.N' is not CLS-compliant
```

```vb
<Assembly:CLSCompliant(True)>

Public Class C1(Of T) 
   Protected Class N
   End Class

   Protected Sub M1(n As C1(Of Integer).N)   ' Not CLS-compliant - C1<int>.N not
                                             ' accessible from within C1(Of T) in all
   End Sub                                   ' languages


   Protected Sub M2(n As C1(Of T).N)     ' CLS-compliant – C1(Of T).N accessible
   End Sub                               ' inside C1(Of T)
End Class

Public Class C2 : Inherits C1(Of Long) 
   Protected Sub M3(n As C1(Of Integer).N)   ' Not CLS-compliant – C1(Of Integer).N is not
   End Sub                                   ' accessible in C2 (extends C1(Of Long))

   Protected Sub M4(n As C1(Of Long).N)   
   End Sub                                
End Class
' Attempting to compile the example displays output like the following:
'    error BC30508: 'n' cannot expose type 'C1(Of Integer).N' in namespace 
'    '<Default>' through class 'C1'.
'    
'       Protected Sub M1(n As C1(Of Integer).N)   ' Not CLS-compliant - C1<int>.N not
'                             ~~~~~~~~~~~~~~~~
'    error BC30389: 'C1(Of T).N' is not accessible in this context because 
'    it is 'Protected'.
'    
'       Protected Sub M3(n As C1(Of Integer).N)   ' Not CLS-compliant - C1(Of Integer).N is not
'    
'                             ~~~~~~~~~~~~~~~~
'    
'    error BC30389: 'C1(Of T).N' is not accessible in this context because it is 'Protected'.
'    
'       Protected Sub M4(n As C1(Of Long).N)  
'                             ~~~~~~~~~~~~~
```

### <a name="constructors"></a>Costruttori

I costruttori nelle classi e strutture conformi a CLS devono rispettare queste regole: 

* Prima di accedere ai dati di istanza ereditati, un costruttore di una classe derivata deve chiamare il costruttore di istanze della relativa classe di base. Questo requisito è dovuto al fatto che i costruttori della classe di base non vengono ereditati dalle classi derivate. Questa regola non si applica alle strutture, che non supportano l'ereditarietà diretta. 

  In genere, questa regola viene applicata dai compilatori indipendentemente dalla conformità a CLS, come illustrato dall'esempio riportato di seguito. Viene creata una classe `Doctor` derivata da una classe `Person`, ma la classe `Doctor` non riesce a chiamare il costruttore della classe `Person` per inizializzare i campi di istanza ereditati. 

    ```csharp
    using System;

    [assembly: CLSCompliant(true)]

    public class Person
    {
    private string fName, lName, _id;

    public Person(string firstName, string lastName, string id)
    {
        if (String.IsNullOrEmpty(firstName + lastName))
            throw new ArgumentNullException("Either a first name or a last name must be provided.");    

        fName = firstName;
        lName = lastName;
        _id = id;
    }

    public string FirstName 
    {
        get { return fName; }
    }

    public string LastName 
    {
        get { return lName; }
    }

    public string Id 
    {
        get { return _id; }
    }

    public override string ToString()
    {
        return String.Format("{0}{1}{2}", fName, 
                            String.IsNullOrEmpty(fName) ?  "" : " ",
                            lName);
    }
    }

    public class Doctor : Person
    {
    public Doctor(string firstName, string lastName, string id)
    {
    }

    public override string ToString()
    {
        return "Dr. " + base.ToString();
    }
    }
    // Attempting to compile the example displays output like the following:
    //    ctor1.cs(45,11): error CS1729: 'Person' does not contain a constructor that takes 0
    //            arguments
    //    ctor1.cs(10,11): (Location of symbol related to previous error)
    ```

    ```vb
    <Assembly: CLSCompliant(True)> 

    Public Class Person
       Private fName, lName, _id As String

       Public Sub New(firstName As String, lastName As String, id As String)
          If String.IsNullOrEmpty(firstName + lastName) Then
             Throw New ArgumentNullException("Either a first name or a last name must be provided.")    
          End If

          fName = firstName
          lName = lastName
          _id = id
       End Sub

       Public ReadOnly Property FirstName As String
          Get
             Return fName
          End Get
       End Property

       Public ReadOnly Property LastName As String
          Get
             Return lName
          End Get
       End Property

       Public ReadOnly Property Id As String
          Get
             Return _id
          End Get
       End Property

       Public Overrides Function ToString() As String
          Return String.Format("{0}{1}{2}", fName, 
                               If(String.IsNullOrEmpty(fName), "", " "),
                               lName)
       End Function
    End Class

    Public Class Doctor : Inherits Person
       Public Sub New(firstName As String, lastName As String, id As String)
       End Sub

       Public Overrides Function ToString() As String
          Return "Dr. " + MyBase.ToString()
       End Function
    End Class
    ' Attempting to compile the example displays output like the following:
    '    Ctor1.vb(46) : error BC30148: First statement of this 'Sub New' must be a call 
    '    to 'MyBase.New' or 'MyClass.New' because base class 'Person' of 'Doctor' does 
    '    not have an accessible 'Sub New' that can be called with no arguments.
    '    
    '       Public Sub New()
    '                  ~~~
    ````
    
* Il costruttore di un oggetto non può essere chiamato tranne che per creare un oggetto. Inoltre, un oggetto non può essere inizializzato due volte. Ad esempio, questo significa che `Object.MemberwiseClone` non deve chiamare i costruttori.  

### <a name="properties"></a>Proprietà

Le proprietà nei tipi conformi a CLS devono rispettare queste regole:

* Una proprietà deve disporre di un metodo Set, un metodo Get o di entrambi. In un assembly questi vengono implementati come metodi speciali, ovvero vengono visualizzati come metodi separati: getter è denominato `get`\_*propertyname* e setter è `set*\_*propertyname*) marked as `SpecialName` nei metadati dell'assembly. Il compilatore C# applica questa regola automaticamente, senza la necessità di usare l'attributo [CLSCompliantAttribute](xref:System.CLSCompliantAttribute). 

* Un tipo di proprietà è il tipo restituito del metodo Get della proprietà e l'ultimo argomento del metodo Set. È necessario che questi tipi siano conformi a CLS e gli argomenti non possono essere assegnati alla proprietà per riferimento, cioè non possono essere puntatori gestiti. 

* Se una proprietà dispone dei metodi Get e Set, essi devono essere entrambi virtuali, statici o istanze. Il compilatore C# applica automaticamente questa regola tramite la relativa sintassi di definizione della proprietà. 

### <a name="events"></a>Eventi

Un evento viene definito in base al nome e al relativo tipo. Il tipo di evento è un delegato che viene usato per indicare l'evento. Ad esempio, l'evento `DbConnection.StateChange` è di tipo `StateChangeEventHandler`. Oltre all'evento stesso, vi sono tre metodi con nomi basati sul nome di evento che forniscono l'implementazione dell'evento e sono contrassegnati come `SpecialName` nei metadati dell'assembly: 

* Un metodo per l'aggiunta di un gestore eventi, denominato `add`_*EventName*. Ad esempio, il metodo di sottoscrizione evento per l'evento `DbConnection.StateChange` è denominato `add_StateChange`. 

* Un metodo per la rimozione di un gestore eventi, denominato `remove`_*EventName*. Ad esempio, il metodo di rimozione per l'evento `DbConnection.StateChange` è denominato `remove_StateChange`.

* Un metodo per indicare che si è verificato l'evento, denominato `raise`_*EventName*. 

> [!NOTE]
> La maggior parte delle regole di Common Language Specification relative agli eventi viene implementata dai compilatori di linguaggi e risulta trasparente agli sviluppatori di componenti. 

I metodi per l'aggiunta, la rimozione e la generazione di eventi devono avere la stessa accessibilità. Devono anche essere tutti statici, istanze o virtuali. I metodi per l'aggiunta e la rimozione di un evento dispongono di un parametro il cui tipo è il tipo delegato di evento. I metodi di aggiunta e rimozione devono essere entrambi presenti o entrambi assenti. 

Nell'esempio seguente viene definita una classe conforme a CLS denominata `Temperature` tramite cui viene generato un evento `TemperatureChanged` se la modifica nella temperatura tra due letture è uguale o maggiore di un valore soglia. Tramite la classe `Temperature` viene definito in modo esplicito un metodo `raise_TemperatureChanged` in modo che tramite esso sia possibile eseguire selettivamente i gestori eventi.

```csharp
using System;
using System.Collections;
using System.Collections.Generic;

[assembly: CLSCompliant(true)]

public class TemperatureChangedEventArgs : EventArgs
{
   private Decimal originalTemp;
   private Decimal newTemp; 
   private DateTimeOffset when;

   public TemperatureChangedEventArgs(Decimal original, Decimal @new, DateTimeOffset time)
   {
      originalTemp = original;
      newTemp = @new;
      when = time;
   }   

   public Decimal OldTemperature
   {
      get { return originalTemp; }
   } 

   public Decimal CurrentTemperature
   {
      get { return newTemp; }
   } 

   public DateTimeOffset Time
   {
      get { return when; }
   }
}

public delegate void TemperatureChanged(Object sender, TemperatureChangedEventArgs e);

public class Temperature
{
   private struct TemperatureInfo
   {
      public Decimal Temperature;
      public DateTimeOffset Recorded;
   }

   public event TemperatureChanged TemperatureChanged;

   private Decimal previous;
   private Decimal current;
   private Decimal tolerance;
   private List<TemperatureInfo> tis = new List<TemperatureInfo>();

   public Temperature(Decimal temperature, Decimal tolerance)
   {
      current = temperature;
      TemperatureInfo ti = new TemperatureInfo();
      ti.Temperature = temperature;
      tis.Add(ti);
      ti.Recorded = DateTimeOffset.UtcNow;
      this.tolerance = tolerance;
   }

   public Decimal CurrentTemperature
   {
      get { return current; }
      set {
         TemperatureInfo ti = new TemperatureInfo();
         ti.Temperature = value;
         ti.Recorded = DateTimeOffset.UtcNow;
         previous = current;
         current = value;
         if (Math.Abs(current - previous) >= tolerance) 
            raise_TemperatureChanged(new TemperatureChangedEventArgs(previous, current, ti.Recorded));
      }
   }

   public void raise_TemperatureChanged(TemperatureChangedEventArgs eventArgs)
   {
      if (TemperatureChanged == null)
         return; 

      foreach (TemperatureChanged d in TemperatureChanged.GetInvocationList()) {
         if (d.Method.Name.Contains("Duplicate"))
            Console.WriteLine("Duplicate event handler; event handler not executed.");
         else
            d.Invoke(this, eventArgs);
      }
   }
}

public class Example
{
   public Temperature temp;

   public static void Main()
   {
      Example ex = new Example();
   }

   public Example()
   {
      temp = new Temperature(65, 3);
      temp.TemperatureChanged += this.TemperatureNotification;
      RecordTemperatures();
      Example ex = new Example(temp);
      ex.RecordTemperatures();
   }

   public Example(Temperature t)
   {
      temp = t;
      RecordTemperatures();
   }

   public void RecordTemperatures()
   {
      temp.TemperatureChanged += this.DuplicateTemperatureNotification;
      temp.CurrentTemperature = 66;
      temp.CurrentTemperature = 63;
   }

   internal void TemperatureNotification(Object sender, TemperatureChangedEventArgs e) 
   {
      Console.WriteLine("Notification 1: The temperature changed from {0} to {1}", e.OldTemperature, e.CurrentTemperature);   
   }

   public void DuplicateTemperatureNotification(Object sender, TemperatureChangedEventArgs e)
   { 
      Console.WriteLine("Notification 2: The temperature changed from {0} to {1}", e.OldTemperature, e.CurrentTemperature);   
   }
}
```

```vb
Imports System.Collections
Imports System.Collections.Generic

<Assembly: CLSCompliant(True)>

Public Class TemperatureChangedEventArgs   : Inherits EventArgs
   Private originalTemp As Decimal
   Private newTemp As Decimal 
   Private [when] As DateTimeOffset

   Public Sub New(original As Decimal, [new] As Decimal, [time] As DateTimeOffset)
      originalTemp = original
      newTemp = [new]
      [when] = [time]
   End Sub   

   Public ReadOnly Property OldTemperature As Decimal
      Get
         Return originalTemp
      End Get
   End Property 

   Public ReadOnly Property CurrentTemperature As Decimal
      Get
         Return newTemp
      End Get
   End Property 

   Public ReadOnly Property [Time] As DateTimeOffset
      Get
         Return [when]
      End Get
   End Property
End Class

Public Delegate Sub TemperatureChanged(sender As Object, e As TemperatureChangedEventArgs)

Public Class Temperature
   Private Structure TemperatureInfo
      Dim Temperature As Decimal
      Dim Recorded As DateTimeOffset
   End Structure

   Public Event TemperatureChanged As TemperatureChanged

   Private previous As Decimal
   Private current As Decimal
   Private tolerance As Decimal
   Private tis As New List(Of TemperatureInfo)

   Public Sub New(temperature As Decimal, tolerance As Decimal)
      current = temperature
      Dim ti As New TemperatureInfo()
      ti.Temperature = temperature
      ti.Recorded = DateTimeOffset.UtcNow
      tis.Add(ti)
      Me.tolerance = tolerance
   End Sub

   Public Property CurrentTemperature As Decimal
      Get
         Return current
      End Get
      Set
         Dim ti As New TemperatureInfo
         ti.Temperature = value
         ti.Recorded = DateTimeOffset.UtcNow
         previous = current
         current = value
         If Math.Abs(current - previous) >= tolerance Then
            raise_TemperatureChanged(New TemperatureChangedEventArgs(previous, current, ti.Recorded))
         End If
      End Set
   End Property

   Public Sub raise_TemperatureChanged(eventArgs As TemperatureChangedEventArgs)
      If TemperatureChangedEvent Is Nothing Then Exit Sub

      Dim ListenerList() As System.Delegate = TemperatureChangedEvent.GetInvocationList()
      For Each d As TemperatureChanged In TemperatureChangedEvent.GetInvocationList()
         If d.Method.Name.Contains("Duplicate") Then
            Console.WriteLine("Duplicate event handler; event handler not executed.")
         Else
            d.Invoke(Me, eventArgs)
         End If
      Next
   End Sub
End Class

Public Class Example
   Public WithEvents temp As Temperature

   Public Shared Sub Main()
      Dim ex As New Example()
   End Sub

   Public Sub New()
      temp = New Temperature(65, 3)
      RecordTemperatures()
      Dim ex As New Example(temp)
      ex.RecordTemperatures()
   End Sub

   Public Sub New(t As Temperature)
      temp = t
      RecordTemperatures()
   End Sub

   Public Sub RecordTemperatures()
      temp.CurrentTemperature = 66
      temp.CurrentTemperature = 63

   End Sub

   Friend Shared Sub TemperatureNotification(sender As Object, e As TemperatureChangedEventArgs) _
          Handles temp.TemperatureChanged
      Console.WriteLine("Notification 1: The temperature changed from {0} to {1}", e.OldTemperature, e.CurrentTemperature)   
   End Sub

   Friend Shared Sub DuplicateTemperatureNotification(sender As Object, e As TemperatureChangedEventArgs) _
          Handles temp.TemperatureChanged
      Console.WriteLine("Notification 2: The temperature changed from {0} to {1}", e.OldTemperature, e.CurrentTemperature)   
   End Sub
End Class
```

### <a name="overloads"></a>Overloads

Le specifiche CLS (Common Language Specification) impongono i requisiti seguenti sui membri di overload: 

* I membri possono essere sottoposti a overload in base al numero di parametri e al tipo di qualsiasi parametro. La convenzione di chiamata, il tipo restituito, i modificatori personalizzati applicati al metodo o al relativo parametro e se i parametri vengono passati per valore o per riferimento vengono ignorati quando viene fatta distinzione tra gli overload. Per un esempio, vedere il codice relativo al requisito in cui viene richiesto che i nomi siano univoci all'interno di un ambito nella sezione [Convenzioni di denominazione](#naming-conventions). 

* È possibile eseguire l'overload solo di proprietà e metodi. Non è possibile eseguire l'overload di campi ed eventi. 

* I metodi generici possono essere sottoposti a overload in base al numero dei relativi parametri generici. 

> [!NOTE]
>Gli operatori `op_Explicit` e `op_Implicit` sono eccezioni alla regola che il valore restituito non viene considerato parte di una firma del metodo per risoluzione dell'overload. Questi due operatori possono essere sottoposti a overload in base ai relativi parametri e al relativo valore restituito. 

### <a name="exceptions"></a>Eccezioni

Gli oggetti eccezione devono derivare da [System.Exception](xref:System.Exception) o da un altro tipo derivato da `System.Exception`. Nell'esempio seguente viene illustrato l'errore del compilatore generato quando una classe personalizzata denominata `ErrorClass` viene usata per la gestione delle eccezioni.

```csharp
using System;

[assembly: CLSCompliant(true)]

public class ErrorClass
{ 
   string msg;

   public ErrorClass(string errorMessage)
   {
      msg = errorMessage;
   }

   public string Message
   {
      get { return msg; }
   }
}

public static class StringUtilities
{
   public static string[] SplitString(this string value, int index)
   {
      if (index < 0 | index > value.Length) {
         ErrorClass badIndex = new ErrorClass("The index is not within the string.");
         throw badIndex;
      }
      string[] retVal = { value.Substring(0, index - 1), 
                          value.Substring(index) };
      return retVal;
   }
}
// Compilation produces a compiler error like the following:
//    Exceptions1.cs(26,16): error CS0155: The type caught or thrown must be derived from
//            System.Exception
```

```vb
Imports System.Runtime.CompilerServices

<Assembly: CLSCompliant(True)>

Public Class ErrorClass 
   Dim msg As String

   Public Sub New(errorMessage As String)
      msg = errorMessage
   End Sub

   Public ReadOnly Property Message As String
      Get
         Return msg
      End Get   
   End Property
End Class

Public Module StringUtilities
   <Extension()> Public Function SplitString(value As String, index As Integer) As String()
      If index < 0 Or index > value.Length Then
         Dim BadIndex As New ErrorClass("The index is not within the string.")
         Throw BadIndex
      End If
      Dim retVal() As String = { value.Substring(0, index - 1), 
                                 value.Substring(index) }
      Return retVal
   End Function
End Module
' Compilation produces a compiler error like the following:
'    Exceptions1.vb(27) : error BC30665: 'Throw' operand must derive from 'System.Exception'.
'    
'             Throw BadIndex
'             ~~~~~~~~~~~~~~
```

Per correggere questo errore, la classe `ErrorClass` deve ereditare da `System.Exception`. Inoltre, la proprietà Message deve essere sottoposta a override. Nell'esempio riportato di seguito questi errori vengono corretti per definire una classe `ErrorClass` che è conforme a CLS.  

```csharp
using System;

[assembly: CLSCompliant(true)]

public class ErrorClass : Exception
{ 
   string msg;

   public ErrorClass(string errorMessage)
   {
      msg = errorMessage;
   }

   public override string Message
   {
      get { return msg; }
   }
}

public static class StringUtilities
{
   public static string[] SplitString(this string value, int index)
   {
      if (index < 0 | index > value.Length) {
         ErrorClass badIndex = new ErrorClass("The index is not within the string.");
         throw badIndex;
      }
      string[] retVal = { value.Substring(0, index - 1), 
                          value.Substring(index) };
      return retVal;
   }
}
```

```vb
Imports System.Runtime.CompilerServices

<Assembly: CLSCompliant(True)>

Public Class ErrorClass : Inherits Exception
   Dim msg As String

   Public Sub New(errorMessage As String)
      msg = errorMessage
   End Sub

   Public Overrides ReadOnly Property Message As String
      Get
         Return msg
      End Get   
   End Property
End Class

Public Module StringUtilities
   <Extension()> Public Function SplitString(value As String, index As Integer) As String()
      If index < 0 Or index > value.Length Then
         Dim BadIndex As New ErrorClass("The index is not within the string.")
         Throw BadIndex
      End If
      Dim retVal() As String = { value.Substring(0, index - 1), 
                                 value.Substring(index) }
      Return retVal
   End Function
End Module
```

### <a name="attributes"></a>Attributi

Negli assembly .NET Framework, gli attributi personalizzati forniscono un meccanismo estensibile per archiviare gli attributi personalizzati e recuperare i metadati sugli oggetti di programmazione, ad esempio assembly, tipi, membri e parametri di metodo. Gli attributi personalizzati devono derivare da [System.Attribute](xref:System.Attribute) o da un tipo derivato da `System.Attribute`.

Nell'esempio riportato di seguito viene violata questa regola. Viene definita una classe `NumericAttribute` che non deriva da `System.Attribute`. Si noti che un errore del compilatore viene visualizzato solo quando viene applicato l'attributo non conforme a CLS, non quando la classe è definita. 

```csharp
using System;

[assembly: CLSCompliant(true)]

[AttributeUsageAttribute(AttributeTargets.Class | AttributeTargets.Struct)] 
public class NumericAttribute
{
   private bool _isNumeric;

   public NumericAttribute(bool isNumeric)
   {
      _isNumeric = isNumeric;
   }

   public bool IsNumeric 
   {
      get { return _isNumeric; }
   }
}

[Numeric(true)] public struct UDouble
{
   double Value;
}
// Compilation produces a compiler error like the following:
//    Attribute1.cs(22,2): error CS0616: 'NumericAttribute' is not an attribute class
//    Attribute1.cs(7,14): (Location of symbol related to previous error)
```

```vb
<Assembly: CLSCompliant(True)>

<AttributeUsageAttribute(AttributeTargets.Class Or AttributeTargets.Struct)> _
Public Class NumericAttribute
   Private _isNumeric As Boolean

   Public Sub New(isNumeric As Boolean)
      _isNumeric = isNumeric
   End Sub

   Public ReadOnly Property IsNumeric As Boolean
      Get
         Return _isNumeric
      End Get
   End Property
End Class

<Numeric(True)> Public Structure UDouble
   Dim Value As Double
End Structure
' Compilation produces a compiler error like the following:
'    error BC31504: 'NumericAttribute' cannot be used as an attribute because it 
'    does not inherit from 'System.Attribute'.
'    
'    <Numeric(True)> Public Structure UDouble
'     ~~~~~~~~~~~~~
```

Tramite il costruttore o le proprietà di un attributo conforme a CLS possono essere esposti solo i tipi seguenti:

* [Boolean](xref:System.Boolean)

* [Byte](xref:System.Byte)

* [Char](xref:System.Char)

* [Double](xref:System.Double)

* [Int16](xref:System.Int16)

* [Int32](xref:System.Int32)

* [Int64](xref:System.Int64)

* [Single](xref:System.Single)

* [String](xref:System.String)

* [Type](xref:System.Type)

* Qualsiasi tipo di enumerazione il cui tipo sottostante è `Byte`, `Int16`, `Int32` o `Int64`. 

Nell'esempio seguente viene definita una classe `DescriptionAttribute` che deriva da [Attribute](xref:System.Attribute). Il costruttore di classe dispone di un parametro di tipo `Descriptor`, pertanto la classe non è conforme a CLS. Si noti che il compilatore C# genera un avviso, ma la compilazione viene eseguita correttamente. 

```csharp
using System;

[assembly:CLSCompliantAttribute(true)]

public enum DescriptorType { type, member };

public class Descriptor
{
   public DescriptorType Type;
   public String Description; 
}

[AttributeUsage(AttributeTargets.All)]
public class DescriptionAttribute : Attribute
{
   private Descriptor desc;

   public DescriptionAttribute(Descriptor d)
   {
      desc = d; 
   }

   public Descriptor Descriptor
   { get { return desc; } } 
}
// Attempting to compile the example displays output like the following:
//       warning CS3015: 'DescriptionAttribute' has no accessible
//               constructors which use only CLS-compliant types
```

```vb
<Assembly:CLSCompliantAttribute(True)>

Public Enum DescriptorType As Integer
   Type = 0
   Member = 1
End Enum

Public Class Descriptor
   Public Type As DescriptorType 
   Public Description As String 
End Class

<AttributeUsage(AttributeTargets.All)> _
Public Class DescriptionAttribute : Inherits Attribute
   Private desc As Descriptor

   Public Sub New(d As Descriptor)
      desc = d 
   End Sub

   Public ReadOnly Property Descriptor As Descriptor
      Get 
         Return desc
      End Get    
   End Property
End Class
```

## <a name="the-clscompliantattribute-attribute"></a>Attributo CLSCompliantAttribute

L'attributo [CLSCompliantAttribute](xref:System.CLSCompliantAttribute) è usato per indicare se un elemento del programma è conforme a CLS (Common Language Specification). Il costruttore `CLSCompliantAttribute.CLSCompliantAttribute(Boolean)` include un solo parametro obbligatorio, *isCompliant*, che indica se l'elemento del programma è conforme a CLS. 

In fase di compilazione, tramite il compilatore vengono rilevati gli elementi non conformi che si presuppone siano conformi a CLS e viene generato un avviso. Tramite il compilatore non vengono generati avvisi per i tipi o i membri che vengono dichiarati esplicitamente come non conformi. 

Gli sviluppatori di componenti possono usare l'attributo `CLSCompliantAttribute` in due modi: 

* Per definire le parti dell'interfaccia pubblica esposte da un componente che sono conformi a CLS e le parti che non sono conformi a CLS. Quando l'attributo viene usato per contrassegnare determinati elementi del programma come conformi a CLS, il relativo uso garantisce che gli elementi sono accessibili da tutti i linguaggi e strumenti destinati a .NET Framework. 

* Per assicurarsi che tramite l'interfaccia pubblica della libreria componenti vengano esposti solo elementi del programma che sono conformi a CLS. Se gli elementi non sono conformi a CLS, tramite i compilatori viene di solito generato un avviso.

> [!WARNING]
> In alcuni casi, dai compilatori di linguaggio vengono applicate regole conformi a CLS indipendentemente dal fatto che l'attributo `CLSCompliantAttribute` venga usato. Ad esempio, con la definizione di un membro `*static` in un'interfaccia viene violata una regola CLS. Tuttavia, se si definisce un membro `*static` in un'interfaccia, il compilatore C# visualizza un messaggio di errore e l'app non viene compilata.

L'attributo `CLSCompliantAttribute` è contrassegnato con un attributo [AttributeUsageAttribute](xref:System.AttributeUsageAttribute) con un valore pari a `AttributeTargets.All`. Con questo valore è possibile applicare l'attributo `CLSCompliantAttribute` a qualsiasi elemento del programma, tra cui assembly, moduli, tipi (classi, strutture, enumerazioni, interfacce e delegati), membri di tipo (costruttori, metodi, proprietà, campi ed eventi), parametri, parametri generici e valori restituiti. Tuttavia, in pratica, è consigliabile applicare l'attributo solo agli assembly, ai tipi e ai membri di tipo. In caso contrario, tramite i compilatori viene ignorato l'attributo e viene continuata la generazione di avvisi del compilatore ogni volta che viene rilevato un parametro non conforme, un parametro generico o un valore restituito nell'interfaccia pubblica della libreria.  

Il valore dell'attributo `CLSCompliantAttribute` viene ereditato dagli elementi del programma contenuti. Ad esempio, se un assembly è contrassegnato come conforme a CLS, anche i relativi tipi sono conformi a CLS. Se un tipo è contrassegnato come conforme a CLS, anche i relativi membri e tipi annidati sono conformi a CLS. 

È possibile eseguire l'override in modo esplicito della conformità ereditata applicando l'attributo `CLSCompliantAttribute` a un elemento del programma contenuto. Ad esempio, è possibile usare l'attributo `CLSCompliantAttribute` con un valore *isCompliant* `false` per definire un tipo non conforme in un assembly conforme e l'attributo con un valore *isComplian* `true` per definire un tipo conforme in un assembly non conforme. È anche possibile definire i membri non conformi in un tipo conforme. Tuttavia, in un tipo non conforme non possono essere inclusi membri conformi. Di conseguenza, non è possibile usare l'attributo con un valore *isCompliant* `true` per eseguire l'override dell'ereditarietà da un tipo non conforme. 

Quando si sviluppano componenti, è sempre consigliabile usare l'attributo `CLSCompliantAttribute` per indicare se l'assembly e i relativi tipi e membri sono conformi a CLS. 

Per creare componenti conformi a CLS: 

1. Usare l'oggetto `CLSCompliantAttribute` per contrassegnare l'assembly come conforme a CLS.

2. Contrassegnare tutti i tipi esposti pubblicamente nell'assembly che non sono conformi a CLS come non conformi. 

3. Contrassegnare tutti i membri esposti pubblicamente in tipi conformi a CLS come non conformi. 

4. Fornire un'alternativa conforme a CLS per i membri non conformi a CLS. 

Se sono stati contrassegnati correttamente tutti i tipi e i membri non conformi, tramite il compilatore non vengono generati avvisi di mancata conformità. Tuttavia, è consigliabile indicare i membri che non sono conformi a CLS ed elencare le alternative conformi a CLS nella documentazione del prodotto. 

Nell'esempio seguente viene usato l'attributo `CLSCompliantAttribute` per definire un assembly conforme a CLS e un tipo, `CharacterUtilities`, contenente due membri non conformi a CLS. Poiché entrambi i membri sono contrassegnati con l'attributo `CLSCompliant(false)`, non vengono generati avvisi dal compilatore. La classe fornisce anche un'alternativa conforme a CLS per entrambi i metodi. In genere, si aggiungono solo due overload al metodo `ToUTF16` per fornire alternative conformi a CLS. Tuttavia, poiché i metodi non possono essere sottoposti a overload in base al valore restituito, i nomi dei metodi conformi a CLS sono diversi da quelli dei metodi non conformi.  

```csharp
using System;
using System.Text;

[assembly:CLSCompliant(true)]

public class CharacterUtilities
{
   [CLSCompliant(false)] public static ushort ToUTF16(String s)
   {
      s = s.Normalize(NormalizationForm.FormC);
      return Convert.ToUInt16(s[0]);
   }

   [CLSCompliant(false)] public static ushort ToUTF16(Char ch)
   {
      return Convert.ToUInt16(ch); 
   }

   // CLS-compliant alternative for ToUTF16(String).
   public static int ToUTF16CodeUnit(String s)
   {
      s = s.Normalize(NormalizationForm.FormC);
      return (int) Convert.ToUInt16(s[0]);
   }

   // CLS-compliant alternative for ToUTF16(Char).
   public static int ToUTF16CodeUnit(Char ch)
   {
      return Convert.ToInt32(ch);
   }

   public bool HasMultipleRepresentations(String s)
   {
      String s1 = s.Normalize(NormalizationForm.FormC);
      return s.Equals(s1);   
   }

   public int GetUnicodeCodePoint(Char ch)
   {
      if (Char.IsSurrogate(ch))
         throw new ArgumentException("ch cannot be a high or low surrogate.");

      return Char.ConvertToUtf32(ch.ToString(), 0);   
   }

   public int GetUnicodeCodePoint(Char[] chars)
   {
      if (chars.Length > 2)
         throw new ArgumentException("The array has too many characters.");

      if (chars.Length == 2) {
         if (! Char.IsSurrogatePair(chars[0], chars[1]))
            throw new ArgumentException("The array must contain a low and a high surrogate.");
         else
            return Char.ConvertToUtf32(chars[0], chars[1]);
      }
      else {
         return Char.ConvertToUtf32(chars.ToString(), 0);
      } 
   }
}
```

```vb
Imports System.Text

<Assembly:CLSCompliant(True)>

Public Class CharacterUtilities
   <CLSCompliant(False)> Public Shared Function ToUTF16(s As String) As UShort
      s = s.Normalize(NormalizationForm.FormC)
      Return Convert.ToUInt16(s(0))
   End Function

   <CLSCompliant(False)> Public Shared Function ToUTF16(ch As Char) As UShort
      Return Convert.ToUInt16(ch) 
   End Function

   ' CLS-compliant alternative for ToUTF16(String).
   Public Shared Function ToUTF16CodeUnit(s As String) As Integer
      s = s.Normalize(NormalizationForm.FormC)
      Return CInt(Convert.ToInt16(s(0)))
   End Function

   ' CLS-compliant alternative for ToUTF16(Char).
   Public Shared Function ToUTF16CodeUnit(ch As Char) As Integer
      Return Convert.ToInt32(ch)
   End Function

   Public Function HasMultipleRepresentations(s As String) As Boolean
      Dim s1 As String = s.Normalize(NormalizationForm.FormC)
      Return s.Equals(s1)   
   End Function

   Public Function GetUnicodeCodePoint(ch As Char) As Integer
      If Char.IsSurrogate(ch) Then
         Throw New ArgumentException("ch cannot be a high or low surrogate.")
      End If
      Return Char.ConvertToUtf32(ch.ToString(), 0)   
   End Function

   Public Function GetUnicodeCodePoint(chars() As Char) As Integer
      If chars.Length > 2 Then
         Throw New ArgumentException("The array has too many characters.")
      End If
      If chars.Length = 2 Then
         If Not Char.IsSurrogatePair(chars(0), chars(1)) Then
            Throw New ArgumentException("The array must contain a low and a high surrogate.")
         Else
            Return Char.ConvertToUtf32(chars(0), chars(1))
         End If
      Else
         Return Char.ConvertToUtf32(chars.ToString(), 0)
      End If 
   End Function            
End Class
```

Se si sta sviluppando un'applicazione anziché una libreria (cioè se non si stanno esponendo tipi o membri che possono essere usati da altri sviluppatori dell'applicazione), la conformità a CLS degli elementi del programma usati dall'applicazione è importante solo se il linguaggio non li supporta. In questo caso, tramite il compilatore di linguaggio verrà generato un errore quando si tenta di usare un elemento non conforme a CLS. 

## <a name="cross-language-interoperability"></a>Interoperabilità tra linguaggi diversi

L'indipendenza del linguaggio ha numerosi significati possibili. Un significato riguarda l'utilizzo semplice dei tipi scritti in un linguaggio da parte di un'applicazione scritta in un linguaggio diverso. Un secondo significato, che è il fulcro di questo articolo, riguarda la combinazione di codice scritto in più linguaggi in un unico assembly .NET Framework. 

L'esempio seguente illustra l'interoperabilità tra linguaggi mediante la creazione di una libreria di classi denominata Utilities.dll che comprende due classi, `NumericLib` e `StringLib`. La classe `NumericLib` è scritta in C# e la classe `StringLib` in Visual Basic. Di seguito è riportato il codice sorgente per `StringUtil.vb`, in cui è incluso un singolo membro, `ToTitleCase`, nella classe `StringLib`.

```vb
Imports System.Collections.Generic
Imports System.Runtime.CompilerServices

Public Module StringLib
   Private exclusions As List(Of String) 

   Sub New()
      Dim words() As String = { "a", "an", "and", "of", "the" }
      exclusions = New List(Of String)
      exclusions.AddRange(words)
   End Sub

   <Extension()> _
   Public Function ToTitleCase(title As String) As String
      Dim words() As String = title.Split() 
      Dim result As String = String.Empty

      For ctr As Integer = 0 To words.Length - 1
         Dim word As String = words(ctr)
         If ctr = 0 OrElse Not exclusions.Contains(word.ToLower()) Then
            result += word.Substring(0, 1).ToUpper() + _
                      word.Substring(1).ToLower()
         Else
            result += word.ToLower()
         End If
         If ctr <= words.Length - 1 Then
            result += " "             
         End If   
      Next 
      Return result 
   End Function
End Module
```

Di seguito è riportato il codice sorgente per NumberUtil.cs tramite cui viene definita una classe `NumericLib` in cui sono contenuti due membri, `IsEven` e `NearZero`.

```csharp
using System;

public static class NumericLib 
{
   public static bool IsEven(this IConvertible number)
   {
      if (number is Byte ||
          number is SByte ||
          number is Int16 ||
          number is UInt16 || 
          number is Int32 || 
          number is UInt32 ||
          number is Int64)
         return ((long) number) % 2 == 0;
      else if (number is UInt64)
         return ((ulong) number) %2 == 0;
      else
         throw new NotSupportedException("IsEven called for a non-integer value.");
   }

   public static bool NearZero(double number)
   {
      return number < .00001; 
   }
}
```

Per includere le due classi in un singolo assembly, è necessario compilarle in moduli. Per compilare il file di codice sorgente di Visual Basic in un modulo, usare il comando seguente: 

```
vbc /t:module StringUtil.vb 
```

Per compilare il file di codice sorgente di C# in un modulo, usare il comando seguente:

```
csc /t:module NumberUtil.cs
```

Usare quindi lo strumento Link (Link.exe) per compilare i due moduli in un assembly: 

```
link numberutil.netmodule stringutil.netmodule /out:UtilityLib.dll /dll
```

L'esempio seguente chiama quindi i metodi `NumericLib.NearZero` e `StringLib.ToTitleCase`. Sia il codice Visual Basic che il codice C# sono in grado di accedere ai metodi in entrambe le classi.

```csharp
using System;

public class Example
{
   public static void Main()
   {
      Double dbl = 0.0 - Double.Epsilon;
      Console.WriteLine(NumericLib.NearZero(dbl));

      string s = "war and peace";
      Console.WriteLine(s.ToTitleCase());
   }
}
// The example displays the following output:
//       True
//       War and Peace
```

```vb
Module Example
   Public Sub Main()
      Dim dbl As Double = 0.0 - Double.Epsilon
      Console.WriteLine(NumericLib.NearZero(dbl))

      Dim s As String = "war and peace"
      Console.WriteLine(s.ToTitleCase())
   End Sub
End Module
' The example displays the following output:
'       True
'       War and Peace
```

Per compilare il codice Visual Basic, usare il comando seguente:

```
vbc example.vb /r:UtilityLib.dll
```

Per eseguire la compilazione con C#, modificare il nome del compilatore da vbc a csc e modificare l'estensione del file da vb a cs:

```
csc example.cs /r:UtilityLib.dll
```


