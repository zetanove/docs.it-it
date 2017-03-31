---
title: "Ereditarietà in C#"
description: "Informazioni su come usare l&quot;ereditarietà nelle applicazioni e nelle librerie C#."
keywords: "ereditarietà (C#), classi di base, classi derivate, classi di base astratte"
author: rpetrusha
manager: wpickett
ms.author: ronpet
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: aeb68c74-0ea0-406f-9fbe-2ce02d47ef31
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: c14a2ecfa4b9c9522278098d54aad258b5feb1dc
ms.lasthandoff: 03/13/2017

---
# <a name="inheritance-in-c-and-net"></a>Ereditarietà in C# e .NET #

## <a name="introduction"></a>Introduzione ##

Questa esercitazione presenta l'ereditarietà in C#. L'ereditarietà è una caratteristica dei linguaggi di programmazione orientati a oggetti che consente di definire una classe di base con funzionalità specifiche (relative a dati e comportamento) e classi derivate che ereditano o eseguono l'override di tali funzionalità.

## <a name="prerequisites"></a>Prerequisiti ##

In questa esercitazione si presuppone che sia stato installato .NET Core. Per le istruzioni di installazione, vedere [.NET Core installation guide](https://www.microsoft.com/net/core) (Guida all'installazione di .NET Core). È necessario anche un editor di codice. In questa esercitazione viene usato [Visual Studio Code](https://code.visualstudio.com), ma è possibile usare qualsiasi editor di codice desiderato.

## <a name="running-the-examples"></a>Esecuzione degli esempi ##

Per creare ed eseguire gli esempi in questa esercitazione, viene usata l'utilità [dotnet](../../core/tools/dotnet.md) dalla riga di comando. Eseguire questi passaggi per ogni esempio:

1. Creare una directory per archiviare l'esempio.

1. Per creare un nuovo progetto.NET Core, immettere il comando [dotnet new console](../../core/tools/dotnet-new.md) al prompt dei comandi.

1. Copiare e incollare il codice dell'esempio nell'editor di codice.

1. Per caricare o ripristinare le dipendenze del progetto, eseguire il comando [dotnet restore](../../core/tools/dotnet-restore.md) dalla riga di comando.

1. Per compilare ed eseguire l'esempio, immettere il comando [dotnet run](../../core/tools/dotnet-run.md).

## <a name="background-what-is-inheritance"></a>Informazioni generali: che cos'è l'ereditarietà? ##

Il concetto di *ereditarietà* è uno degli attributi fondamentali della programmazione orientata a oggetti. L'ereditarietà consente di definire una classe figlio che riutilizza (eredita), estende o modifica il comportamento di una classe padre. La classe i cui membri vengono ereditati è denominata *classe di base*. Quella che eredita i membri della classe di base è denominata *classe derivata*.

C# e .NET supportano solo l'*ereditarietà singola*. Ciò significa che una classe può solo ereditare da una singola classe. L'ereditarietà tuttavia è transitiva, pertanto è possibile definire una gerarchia di ereditarietà per un set di tipi. In altre parole, il tipo `D` può ereditare dal tipo `C`, che eredita dal tipo `B`, il quale eredita a sua volta dal tipo della classe di base `A`. Poiché l'ereditarietà è transitiva, i membri del tipo `A` sono disponibili per il tipo `D`.

Non tutti i membri di una classe di base vengono ereditati dalle classi derivate. I membri seguenti non vengono ereditati:

- [Costruttori statici](../programming-guide/classes-and-structs/static-constructors.md), che inizializzano i dati statici di una classe.

- [Costruttori di istanze](../programming-guide/classes-and-structs/constructors.md), che vengono chiamati per creare una nuova istanza della classe. Ogni classe deve definire propri costruttori.

- [Distruttori](../programming-guide/classes-and-structs/destructors.md), che vengono chiamati dal Garbage Collector di runtime per distruggere le istanze di una classe.

Tutti gli altri membri di una classe di base vengono ereditati dalle classi derivate, ma la loro visibilità dipende dall'accessibilità. L'accessibilità di un membro ne determina la visibilità per le classi derivate, come indicato di seguito:

- I membri [privati](../language-reference/keywords/private.md) sono visibili solo nelle classi derivate che sono annidate nella relativa classe di base. In caso contrario, non sono visibili nelle classi derivate. Nell'esempio seguente `A.B` è una classe annidata che deriva da `A` e `C` deriva da `A`. Il campo privato `A.value` è visibile in A.B. Se tuttavia si rimuovono i commenti dal metodo `C.GetValue` e si tenta di compilare l'esempio, verrà generato l'errore del compilatore CS0122: "'A.value' non è accessibile a causa del livello di protezione impostato".

   [!CODE [Inheritance](../../../samples/snippets/csharp/tutorials/inheritance/private.cs#1)]

- I membri [protetti](../language-reference/keywords/protected.md) sono visibili solo nelle classi derivate.

- I membri [interni](../language-reference/keywords/protected.md) sono visibili solo nelle classi derivate che si trovano nello stesso assembly della classe di base. Non sono visibili nelle classi derivate che si trovano in un assembly diverso dalla classe di base.

- I membri [pubblici] (../language-reference/keywords/protected.md) sono visibili nelle classi derivate e fanno parte dell'interfaccia pubblica della classe derivata. I membri pubblici ereditati possono essere chiamati come se fossero definiti nella classe derivata. Nell'esempio seguente la classe `A` definisce un metodo denominato `Method1` e la classe `B` eredita dalla classe `A`. Nell'esempio viene quindi chiamato `Method1` come se fosse un metodo di istanza in `B`.

[!CODE [Inheritance](../../../samples/snippets/csharp/tutorials/inheritance/basics.cs#1)]

Le classi derivate possono anche eseguire l'*override* dei membri ereditati fornendo un'implementazione alternativa. Per poter eseguire l'override di un membro, il membro nella classe di base deve essere contrassegnato con la parola chiave [virtual](../language-reference/keywords/virtual.md). Per impostazione predefinita, i membri della classe di base non sono contrassegnati come `virtual` e non possono essere sottoposti a override. Se si prova a eseguire l'override di un membro non virtuale, viene generato l'errore del compilatore CS0506: "<member> non può eseguire l'override del membro ereditato <member> perché non è contrassegnato come virtual, abstract o override".

   ```csharp
   public class A
   {
      public void Method1()
      {
         // Do something.
      }
   }

   public class B : A
   {
      public override void Method1()  // Generates CS0506.
      {
         // Do something else.
      }
   }
   ```

In alcuni casi una classe derivata *deve* eseguire l'override dell'implementazione della classe di base. I membri della classe di base contrassegnati con la parola chiave [abstract](../language-reference/keywords/abstract.md) richiedono di essere sottoposti a override dalle classi derivate. Se si prova a compilare l'esempio seguente, verrà generato l'errore del compilatore CS0534, "<class> non implementa il membro astratto ereditato <member>", perché la classe `B` non fornisce alcuna implementazione per `A.Method1`.

   ```csharp
   public abstract class A
   {
      public abstract void Method1();
   }

   public class B : A                  // Generates CS0534.
   {
      public void Method3()
      {
         // Do something.
      }
   }
   ```

L'ereditarietà si applica solo alle classi e alle interfacce. Le altre categorie di tipi (struct, delegati ed enumerazioni) non supportano l'ereditarietà. Per questo motivo, se si prova a compilare il codice come nell'esempio seguente, verrà generato l'errore del compilatore CS0527: "Il tipo 'ValueType' nell'elenco delle interfacce non è un'interfaccia". Il messaggio di errore indica che, sebbene sia possibile definire le interfacce implementate da un tipo struct, l'ereditarietà non è supportata.

   ```csharp
   using System;

   public struct ValueStructure : ValueType       // Generates CS0527.
   {
   }
   ```

## <a name="implicit-inheritance"></a>Ereditarietà implicita ##

Oltre ai tipi da cui possono ereditare tramite l'ereditarietà singola, tutti i tipi nel sistema di tipi .NET ereditano in modo implicito da @System.Object o da un tipo derivato. In questo modo le funzionalità comuni saranno disponibili per qualsiasi tipo.

Per comprendere il significato dell'ereditarietà implicita, si definirà una nuova classe, `SimpleClass`, che è semplicemente una definizione di classe vuota:

[!CODE [Inheritance](../../../samples/snippets/csharp/tutorials/inheritance/simpleclass.cs#1)]

È quindi possibile usare la reflection, che consente di esaminare i metadati del tipo per ottenere informazioni su di esso, per generare un elenco dei membri che appartengono al tipo `SimpleClass`. Anche se non è stato definito alcun membro nella classe `SimpleClass`, l'output dell'esempio indica che ha effettivamente nove membri. Uno di questi membri è un costruttore senza parametri (o predefinito) fornito automaticamente per il tipo `SimpleClass` dal compilatore C#. Gli altri otto sono membri di @System.Object, il tipo da cui tutte le classi e le interfacce nel sistema di tipi .NET ereditano in modo implicito.

[!CODE [Inheritance](../../../samples/snippets/csharp/tutorials/inheritance/simpleclass.cs#2)]

L'ereditarietà implicita dalla classe @System.Object rende disponibili questi metodi per la classe `SimpleClass`:

- Il metodo pubblico `ToString`, che converte un oggetto `SimpleClass` nella relativa rappresentazione stringa, ovvero il nome di tipo completo. In questo caso il metodo `ToString` restituisce la stringa "SimpleClass".

- Tre metodi che verificano l'uguaglianza di due oggetti: il metodo pubblico di istanza `Equals(Object)`, il metodo statico pubblico `Equals(Object, Object)` e il metodo statico pubblico `ReferenceEquals(Object, Object)`. Per impostazione predefinita, questi metodi verificano l'uguaglianza dei riferimenti. Ciò significa che, per essere uguali, due variabili di oggetto devono fare riferimento allo stesso oggetto.

- Il metodo pubblico `GetHashCode`, che calcola un valore che consente di usare un'istanza del tipo nelle raccolte con hash.

- Il metodo pubblico `GetType`, che restituisce un oggetto @System.Type che rappresenta il tipo `SimpleClass`.

- Il metodo protetto @System.Object.Finalize, che è progettato per rilasciare le risorse non gestite prima che la memoria di un oggetto venga recuperata dal Garbage Collector.

- Il metodo protetto @System.Object.MemberwiseClone, che crea un clone superficiale dell'oggetto corrente.

Grazie all'ereditarietà implicita, è possibile chiamare qualsiasi membro ereditato da un oggetto `SimpleClass` come se fosse effettivamente un membro definito nella classe `SimpleClass`. Nell'esempio seguente viene chiamato il metodo `SimpleClass.ToString` che `SimpleClass` eredita da @System.Object.

[!CODE [Inheritance](../../../samples/snippets/csharp/tutorials/inheritance/simpleclass2.cs#1)]

Nella tabella seguente sono elencate le categorie di tipi che è possibile creare in C# e i tipi da cui ereditano in modo implicito. Tramite l'ereditarietà ciascun tipo di base rende disponibile un set di membri diverso per i tipi derivati in modo implicito.

| Categoria di tipi | Eredita in modo implicito da... |
| :--- | :---: | ---: |
| classe | @System.Object |
| struct | @System.ValueType, @System.Object |
| enum | @System.Enum, System.ValueType, @System.Object |
| delegato | @System.MulticastDelegate, @System.Delegate, @System.Object |

## <a name="inheritance-and-an-is-a-relationship"></a>Ereditarietà e relazione "è un" ##

In genere l'ereditarietà consente di esprimere una relazione "è un" tra una classe di base e una o più classi derivate, in cui le classi derivate sono versioni specializzate della classe di base. La classe derivata è un tipo della classe di base. La classe `Publication` rappresenta ad esempio una pubblicazione di qualsiasi tipo e le classi `Book` e `Magazine` rappresentano tipi specifici di pubblicazioni.

   [!NOTE] Una classe o un tipo struct può implementare una o più interfacce. Anche se l'implementazione dell'interfaccia è spesso presentata come una soluzione alternativa all'ereditarietà singola o come modo per usare l'ereditarietà con struct, è stata ideata per esprimere una relazione diversa (una relazione "può fare") tra un'interfaccia e il relativo tipo di implementazione rispetto all'ereditarietà. Un'interfaccia definisce un subset di funzionalità che rende disponibili per i tipi di implementazione, ad esempio le funzionalità per verificare l'uguaglianza, confrontare o ordinare gli oggetti, nonché supportare la formattazione e l'analisi in base alle impostazioni cultura.

Si noti che "è un" esprime anche la relazione tra un tipo e un'istanza specifica di quel tipo. Nell'esempio seguente `Automobile` è una classe che ha tre proprietà univoche di sola lettura: `Moke`, il produttore dell'automobile, `Model`, il tipo di automobile e `Year`, l'anno di produzione. La classe `Automobile` include anche un costruttore i cui argomenti vengono assegnati ai valori delle proprietà ed esegue l'override del metodo @System.Object.ToString per generare una stringa che identifica in modo univoco l'istanza `Automobile` anziché la classe `Automobile`.

[!CODE [Inheritance](../../../samples/snippets/csharp/tutorials/inheritance/is-a.cs#1)]

In questo caso è opportuno non fare affidamento sull'ereditarietà per rappresentare marche e modelli specifici di automobili. Non è ad esempio necessario definire un tipo `Packard` che rappresenta automobili prodotte dalla casa automobilistica Packard. È invece possibile rappresentarle creando un oggetto `Automobile` con i valori appropriati passati al costruttore della classe, come illustrato nell'esempio seguente.

[!CODE [Inheritance](../../../samples/snippets/csharp/tutorials/inheritance/is-a.cs#2)]

È preferibile applicare una relazione "è un" basata sull'ereditarietà a una classe di base e a classi derivate che aggiungono altri membri alla classe di base o che richiedono funzionalità aggiuntive non presenti nella classe di base.

## <a name="designing-the-base-class-and-derived-classes"></a>Progettazione della classe di base e delle classi derivate ##

Si esaminerà ora il processo di progettazione della classe di base e delle relative classi derivate. In questa sezione si definirà una classe di base, `Publication`, che rappresenta una pubblicazione di qualsiasi tipo, ad esempio un libro, una rivista, un giornale, un diario, un articolo e così via. Si definirà anche una classe `Book` che deriva da `Publication`. L'esempio può essere facilmente esteso alla definizione di altre classi derivate, ad esempio `Magazine`, `Journal`, `Newspaper` e `Article`.

### <a name="the-base-publication-class"></a>La classe di base `Publication` ###

Per progettare la classe `Publication`, è necessario prendere alcune decisioni di progettazione:

- Quali membri includere nella classe di base `Publication` e se i membri `Publication` forniscono le implementazioni del metodo o se `Publication` è una classe di base astratta che funge da modello per le relative classi derivate.

   In questo caso la classe `Publication` fornirà le implementazioni del metodo. La sezione [Progettazione di classi di base astratte e delle relative classi derivate](#abstract) contiene un esempio in cui viene usata una classe di base astratta per definire i metodi di cui le classi derivate devono eseguire l'override. Le classi derivate possono fornire qualsiasi implementazione adatta al tipo derivato.

   La possibilità di riutilizzare il codice, ovvero il fatto che più classi derivate condividano la dichiarazione e l'implementazione dei metodi della classe di base e non ne richiedano l'override, è un vantaggio delle classi di base non astratte. È quindi necessario aggiungere membri a `Publication` se è probabile che il relativo codice venga condiviso da alcuni o dalla maggior parte dei tipi specializzati `Publication`. Se questa operazione non viene eseguita in modo efficiente, sarà necessario fornire implementazioni di membri pressoché identiche nelle classi derivate anziché una singola implementazione nella classe di base. La necessità di mantenere il codice duplicato in più posizioni è una potenziale fonte di bug.

   Per ottimizzare il riutilizzo del codice e per creare una gerarchia di ereditarietà logica e intuitiva, è opportuno assicurarsi che nella classe `Publication` vengano inclusi solo i dati e le funzionalità comuni a tutte le pubblicazioni o alla maggior parte di esse. Le classi derivate implementano quindi i membri che sono univoci per i tipi di pubblicazione specifici che rappresentano.

- Fino a che punto estendere la gerarchia di classi. È necessario decidere se si vuole sviluppare una gerarchia di tre o più classi, anziché semplicemente una classe di base e una o più classi derivate. `Publication` può ad esempio essere una classe di base di `Periodical`, che a sua volta è una classe di base di `Magazine`, `Journal` e `Newspaper`.

   Per questo esempio si userà la gerarchia semplice di una classe `Publication` e di una singola classe derivata `Book`. L'esempio può essere facilmente esteso alla creazione di una serie di classi aggiuntive che derivano da `Publication`, ad esempio `Magazine` e `Article`.

- Se è opportuno creare un'istanza della classe di base. In caso contrario, è necessario applicare alla classe la parola chiave [abstract](../language-reference/keywords/abstract.md). Se si prova a creare un'istanza di una classe contrassegnata con la parola chiave `abstract` da una chiamata diretta al costruttore della classe, il compilatore C# genera l'errore CS0144, "Non è possibile creare un'istanza della classe o dell'interfaccia astratta". Se si prova a creare un'istanza della classe usando la reflection, il metodo di reflection genera un'eccezione @System.MemberAccessException. In caso contrario, è possibile creare un'istanza della classe `Publication` chiamando il relativo costruttore di classe.

   Per impostazione predefinita, è possibile creare un'istanza della classe di base chiamando il relativo costruttore di classe. Si noti che non è necessario definire in modo esplicito un costruttore di classe. Se non è presente un costruttore nel codice sorgente della classe di base, il compilatore C# ne fornisce automaticamente uno predefinito (senza parametri).

   Per questo esempio, la classe `Publication` verrà contrassegnata come [abstract](../language-reference/keywords/abstract.md) in modo che non sia possibile crearne un'istanza.

- Se le classi derivate devono ereditare l'implementazione della classe di base di un membro specifico o se possono eseguire l'override dell'implementazione della classe di base. È necessario usare la parola chiave [virtual](../language-reference/keywords/virtual.md) per consentire alle classi derivate di eseguire l'override di un metodo della classe di base. Per impostazione predefinita, *non* è possibile eseguire l'override dei metodi definiti nella classe di base.

- Se una classe derivata rappresenta la classe finale nella gerarchia di ereditarietà e non può essere usata come classe di base per altre classi derivate. Per impostazione predefinita, qualsiasi classe può essere usata come classe di base. È possibile applicare la parola chiave [sealed](../language-reference/keywords/sealed.md) per indicare che una classe non può essere usata come classe di base per altre classi. Se si prova a stabilire una relazione di derivazione da una classe sealed, viene generato l'errore del compilatore CS0509, "non può derivare dal tipo sealed <typeName>".

   Per questo esempio, la classe derivata verrà contrassegnata come `sealed`.

L'esempio seguente illustra il codice sorgente della classe `Publication`, nonché un'enumerazione `PublicationType` restituita dalla proprietà `Publication.PublicationType`. Oltre ai membri che eredita da @System.Object, la classe `Publication` definisce i membri univoci e gli override dei membri seguenti:

[!CODE [Inheritance](../../../samples/snippets/csharp/tutorials/inheritance/base-and-derived.cs#1)]

- Un costruttore

  Poiché la classe `Publication` è `abstract`, non è possibile crearne un'istanza direttamente dal codice, come nell'esempio seguente:

  ```csharp
  var publication = new Publication("Tiddlywinks for Experts", "Fun and Games",
                                    PublicationType.Book);
  ```

  Il relativo costruttore di istanze può essere tuttavia chiamato direttamente dai costruttori delle classi derivate, come illustrato dal codice sorgente della classe `Book`.

- Due proprietà relative alla pubblicazione

  `Title` è una proprietà @System.String di sola lettura il cui valore viene fornito chiamando il costruttore `Publication`, che archivia il valore in un campo privato denominato `pubTitle`.

  `Pages` è una proprietà @System.Int32 di lettura/scrittura che indica il numero totale di pagine contenute nella pubblicazione. Il valore viene archiviato in un campo privato denominato `totalPages`. Deve essere un numero positivo, altrimenti viene generata un'eccezione @System.ArgumentOutOfRangeException.

- Membri relativi all'editore

  Due proprietà di sola lettura, `Publisher` e `Type`, restituiscono il valore dei campi privati `pubName` e `pubType`. I valori sono forniti in origine tramite la chiamata al costruttore di classe `Publication`.

- Membri relativi alla pubblicazione

  Due metodi, `Publish` e `GetPublicationDate`, impostano e restituiscono la data di pubblicazione. Il metodo `Publish` imposta un flag privato `published` su `true` quando viene chiamato e assegna la data passata come argomento al campo privato `datePublished`. Il metodo `GetPublicationDate` restituisce la stringa "NYP" se il flag `published` è `false` e il valore del campo `datePublished` se è `true`.

- Membri relativi al copyright

  Il metodo `Copyright` accetta come argomenti il nome del titolare del copyright e l'anno del copyright e li assegna ai campi privati `copyrName` e `copyrDate`. I valori possono essere recuperati dalle proprietà `CopyrightName` e `CopyrightDate`.

- Override del metodo `ToString`

  Se un tipo non esegue l'override del metodo @System.Object.ToString, restituisce il nome completo del tipo, che è pressoché inutile per distinguere un'istanza da un'altra. La classe `Publication` esegue l'override di @System.Object.ToString per restituire il valore della proprietà `Title`.

La figura seguente illustra la relazione tra la classe di base `Publication` e la relativa classe @System.Object ereditata in modo implicito.

![Classi Object e Publication](media/publication-class.jpg)

### <a name="the-book-class"></a>Classe `Book` ###

La classe `Book` rappresenta un libro come tipo specializzato di pubblicazione. L'esempio seguente illustra il codice sorgente della classe `Book`.

[!CODE [Inheritance](../../../samples/snippets/csharp/tutorials/inheritance/base-and-derived.cs#2)]

Oltre ai membri che eredita da `Publication`, la classe `Book` definisce i membri univoci e gli override dei membri seguenti:

- Due costruttori

  I due costruttori `Book` condividono tre parametri comuni. Due, *title* e *publisher*, corrispondono ai parametri del costruttore `Publication`. Il terzo è *author*, che viene archiviato in un campo privato `authorName`. Un costruttore include un parametro *isbn*, che viene archiviato in un campo privato `id`.

  Il primo costruttore usa la parola chiave [this](../language-reference/keywords/this.md) per chiamare l'altro costruttore. Si tratta di un modello comune per la definizione dei costruttori. I costruttori con meno parametri forniscono i valori predefiniti quando chiamano il costruttore con il maggior numero di parametri.

  Il secondo costruttore usa la parola chiave [base](../language-reference/keywords/base.md) per passare il titolo e il nome dell'editore al costruttore della classe di base. Se non si esegue una chiamata esplicita a un costruttore della classe di base nel codice sorgente, il compilatore C# effettua automaticamente una chiamata al costruttore della classe di base predefinito o senza parametri.

- Una proprietà `ISBN` di sola lettura, che restituisce il numero ISBN (International Standard Book Number) dell'oggetto `Book`, un numero univoco a 10 o 13 cifre. Il numero ISBN viene fornito come argomento a uno dei costruttori `Book` e viene archiviato nel campo privato `id`.

- Una proprietà `Author` di sola lettura. Il nome dell'autore viene fornito come argomento a entrambi i costruttori `Book` e viene archiviato nel campo privato `authorName`.

- Due proprietà di sola lettura relative ai prezzi, `Price` e `Currency`. I relativi valori vengono forniti come argomenti in una chiamata al metodo `SetPrice`. Il prezzo viene archiviato in un campo privato, `bookPrice`. La proprietà `Currency` è il simbolo di valuta ISO a tre cifre, ad esempio USD per il dollaro statunitense, e viene archiviata nel campo privato `ISOCurrencySymbol`. I simboli di valuta ISO possono essere recuperati dalla proprietà @System.Globalization.RegionInfo.ISOCurrencySymbol.

- Un metodo `SetPrice`, che imposta i valori dei campi `bookPrice` e `ISOCurrencySymbol`. Si tratta dei valori restituiti dalle proprietà `Price` e `Currency`.

- Esegue l'override del metodo `ToString` ereditato da `Publication` e dei metodi @System.Object.Equals(System.Object) e @System.Object.GetHashCode ereditati da @System.Object.

  A meno che non venga sottoposto a override, il metodo @System.Object.Equals(System.Object) verifica l'uguaglianza dei riferimenti. Ciò significa che due variabili di oggetto sono considerate uguali se fanno riferimento allo stesso oggetto. Nel caso della classe `Book`, d'altra parte, due oggetti `Book` sono considerati uguali se hanno lo stesso ISBN.

  Quando si esegue l'override del metodo @System.Object.Equals(System.Object), è necessario eseguire l'override anche del metodo @System.Object.GetHashCode, che restituisce un valore che verrà usato dal runtime per archiviare elementi in raccolte con hash e facilitarne così il recupero. Il codice hash deve restituire un valore coerente con il test di uguaglianza. Poiché @System.Object.Equals(System.Object) è stato sottoposto a override per restituire `true` se le proprietà ISBN di due oggetti `Book` sono uguali, si restituisce il codice hash calcolato chiamando il metodo @System.String.GetHashCode della stringa restituita dalla proprietà `ISBN`.

La figura seguente illustra la relazione tra la classe `Book` e la relativa classe di base `Publication`.

![Classi Publication e Book](media/book-class.jpg)

È ora possibile creare un'istanza di un oggetto `Book`, richiamarne i membri univoci ed ereditati e passarla come argomento a un metodo che prevede un parametro di tipo `Publication` o `Book`, come illustrato nell'esempio seguente.

[!CODE [Inheritance](../../../samples/snippets/csharp/tutorials/inheritance/use-publication.cs#1)]

## <a name="abstract"></a> Progettazione di classi di base astratte e delle relative classi derivate ##

Nell'esempio precedente si è definita una classe di base che fornisce un'implementazione per una serie di metodi per consentire alle classi derivate di condividere il codice. In molti casi, tuttavia, la classe di base non deve fornire un'implementazione. Al contrario, è una *classe astratta* e funge da modello che definisce i membri che ogni classe derivata deve implementare. Nel caso di una classe di base astratta l'implementazione di ogni tipo derivato è in genere univoca per quel tipo.

Ogni forma geometrica bidimensionale chiusa include ad esempio due proprietà: l'area, l'estensione interna della forma e il perimetro, ovvero la lunghezza totale dei bordi della forma. La modalità di calcolo di queste proprietà dipende tuttavia completamente dalla forma specifica. La formula per calcolare il perimetro (o circonferenza) di un cerchio è ad esempio molto diversa da quella usata per un triangolo.

L'esempio seguente definisce una classe di base astratta denominata `Shape` che definisce due proprietà: `Area` e `Perimeter`. Si noti che, oltre a contrassegnare la classe con la parola chiave [abstract](../language-reference/keywords/abstract.md), si contrassegna con la parola chiave [abstract](../language-reference/keywords/abstract.md) anche ogni membro dell'istanza. In questo caso `Shape` esegue anche l'override del metodo @System.Object.ToString per restituire il nome del tipo, anziché il nome completo. Definisce inoltre due membri statici, `GetArea` e `GetPerimeter`, che consentono ai chiamanti di recuperare facilmente l'area e il perimetro di un'istanza di qualsiasi classe derivata. Quando si passa un'istanza di una classe derivata a uno di questi metodi, il runtime chiama l'override del metodo della classe derivata.

[!CODE [Inheritance](../../../samples/snippets/csharp/tutorials/inheritance/shape.cs#1)]

È quindi possibile derivare da `Shape` alcune classi che rappresentano forme specifiche. Nell'esempio seguente vengono definite tre classi, `Triangle`, `Rectangle` e `Circle`. Ogni classe usa una formula univoca per calcolare l'area e il perimetro della forma specifica. Alcune classi derivate definiscono anche le proprietà, ad esempio `Rectangle.Diagonal` e `Circle.Diameter`, che sono univoche per la forma che rappresentano.

[!CODE [Inheritance](../../../samples/snippets/csharp/tutorials/inheritance/shape.cs#2)]

Nell'esempio seguente vengono usati gli oggetti derivati da `Shape`. Viene creata un'istanza di una matrice di oggetti derivati da `Shape` e vengono chiamati i metodi statici della classe `Shape`, che esegue il wrapping dei valori restituiti della proprietà `Shape`. Si noti che il runtime recupera i valori dalle proprietà dei tipi derivati sottoposte a override. Nell'esempio viene anche eseguito il cast di ogni oggetto `Shape` nella matrice al relativo tipo derivato e, se il cast ha esito positivo, vengono recuperate le proprietà di quella sottoclasse specifica di `Shape`. 

[!CODE [Inheritance](../../../samples/snippets/csharp/tutorials/inheritance/shape.cs#3)]

## <a name="see-also"></a>Vedere anche ##

[Classi e oggetti](../tour-of-csharp/classes-and-objects.md)</br>
[Ereditarietà (Guida per programmatori C#)](../programming-guide/classes-and-structs/inheritance.md)

