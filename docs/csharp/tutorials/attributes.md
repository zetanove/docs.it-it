---
title: Attributi | C#
description: Informazioni sull&quot;uso degli attributi in C#.
keywords: .NET, .NET Core, C#, attributi
author: mgroves
ms.author: wiwagn
ms.date: 03/06/2017
ms.topic: article
ms.prod: .net
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: b152cf36-76e4-43a5-b805-1a1952e53b79
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: f03e8ac38bc0f3b0d527c0cdcb5f01b40bbb9682
ms.lasthandoff: 03/13/2017

---

# <a name="using-attributes-in-c"></a>Uso degli attributi in C# #

Gli attributi consentono di associare informazioni al codice in modo dichiarativo. Offrono anche un elemento riutilizzabile che può essere applicato a vari tipi di destinazioni.

L'attributo `[Obsolete]`, ad esempio, può essere applicato a classi, struct, metodi, costruttori e altri elementi. _Dichiara_ che l'elemento è obsoleto. Spetta quindi al compilatore C# cercare l'attributo ed eseguire di conseguenza le azioni appropriate.

In questa esercitazione si illustreranno le procedure necessarie per aggiungere attributi al codice, creare e usare attributi personalizzati e usare alcuni attributi incorporati in .NET Core.

## <a name="prerequisites"></a>Prerequisiti
È necessario configurare il computer per l'esecuzione di .NET Core. Le istruzioni di installazione sono disponibili nella pagina [.NET Core](https://www.microsoft.com/net/core).
Questa applicazione può essere eseguita in Windows, Ubuntu Linux, macOS o in un contenitore Docker. È necessario installare l'editor di codice preferito. Nelle descrizioni seguenti viene usato [Visual Studio Code](https://code.visualstudio.com/), un editor open source multipiattaforma, ma è possibile usare gli strumenti con cui si ha maggiore familiarità.

## <a name="create-the-application"></a>Creare l'applicazione

Dopo avere installato tutti gli strumenti, creare una nuova applicazione .NET Core. Per usare il generatore da riga di comando, eseguire il comando seguente nella shell preferita:

`dotnet new console`

Questo comando crea file di progetto .NET Core per sistemi barebone. Sarà necessario eseguire `dotnet restore` per ripristinare le dipendenze richieste per la compilazione del progetto.

Per eseguire il programma, usare `dotnet run`. Nella console viene visualizzato "Hello, World".

## <a name="how-to-add-attributes-to-code"></a>Come aggiungere attributi al codice

In C# gli attributi sono classi che ereditano dalla classe di base `Attribute`. Qualsiasi classe che eredita da `Attribute` può essere usata come una sorta di "tag" in altre parti del codice.
Si consideri, ad esempio, l'attributo denominato `ObsoleteAttribute`, usato per segnalare che il codice è obsoleto e non deve più essere usato. È possibile inserire questo attributo in una classe usando, ad esempio, parentesi quadre.

[!code-csharp[Esempio attributo obsoleto](../../../samples/snippets/csharp/tutorials/attributes/Program.cs#ObsoleteExample1)]  

Anche se la classe è chiamata `ObsoleteAttribute`, nel codice è necessario usare solo `[Obsolete]`. Questa è una convenzione seguita da C#.
Se si preferisce, è possibile usare il nome completo `[ObsoleteAttribute]`.

Quando si contrassegna una classe come obsoleta, è opportuno fornire alcune informazioni sul *motivo* per cui è obsoleta e/o sull'*oggetto* da usare in alternativa. A questo scopo, passare un parametro stringa all'attributo Obsolete.

[!code-csharp[Esempio di attributo obsoleto con parametri](../../../samples/snippets/csharp/tutorials/attributes/Program.cs#ObsoleteExample2)]

La stringa viene trasmessa come argomento a un costruttore `ObsoleteAttribute`, come se si scrivesse `var attr = new ObsoleteAttribute("some string")`.

I parametri che è possibile passare a un costruttore di attributo sono limitati a tipi o valori letterali semplici: `bool, int, double, string, Type, enums, etc` e matrici di questi tipi.
Non è possibile usare un'espressione o una variabile, ma è possibile usare parametri posizionali o denominati.

## <a name="how-to-create-your-own-attribute"></a>Come creare un attributo personalizzato

Creare un attributo è semplice come ereditarlo dalla classe di base `Attribute`.

[!code-csharp[Creare un attributo personalizzato](../../../samples/snippets/csharp/tutorials/attributes/Program.cs#CreateAttributeExample1)]

Con quanto creato in precedenza, è possibile ora usare `[MySpecial]` (o `[MySpecialAttribute]`) come attributo in un'altra posizione della codebase.

[!code-csharp[Uso di un attributo personalizzato](../../../samples/snippets/csharp/tutorials/attributes/Program.cs#CreateAttributeExample2)]

Alcuni attributi presenti nella libreria di classi base .NET, come `ObsoleteAttribute`, attivano determinati comportamenti nel compilatore. Qualsiasi attributo creato, tuttavia, svolge solo la funzione di metadato e non genera alcun codice nella classe di attributo in esecuzione. È compito dell'utente intervenire sui metadati in un'altra parte del codice. Informazioni più dettagliate sono disponibili più avanti nell'esercitazione.

A questo punto è necessario prestare attenzione a un piccolo problema. Come specificato in precedenza, è possibile passare come argomenti solo determinati tipi di attributi. Quando si crea un tipo di attributo, tuttavia, il compilatore C# non impedisce la creazione di questi parametri. Nell'esempio seguente è stato creato un attributo con un costruttore compilato correttamente.

[!code-csharp[Costruttore valido usato in un attributo](../../../samples/snippets/csharp/tutorials/attributes/Program.cs#AttributeGothca1)]

Non sarà tuttavia possibile usare questo costruttore con la sintassi di attributo.

[!code-csharp[Tentativo non valido di usare il costruttore di attributi](../../../samples/snippets/csharp/tutorials/attributes/Program.cs#AttributeGotcha2)]

Il codice precedente genererà un errore del compilatore come `Attribute constructor parameter 'myClass' has type 'Foo', which is not a valid attribute parameter type`

## <a name="how-to-restrict-attribute-usage"></a>Come limitare l'uso degli attributi

Gli attributi possono essere usati su diversi tipi di "destinatari". Gli esempi precedenti ne illustrano l'uso all'interno di classi, ma possono anche essere usati in:

* Assembly
* Classe
* Costruttore
* Delegato
* Enum
* Evento
* Campo
* GenericParameter
* Interfaccia
* Metodo
* Modulo
* Parametro
* Proprietà
* ReturnValue
* Struct

Quando si crea una classe di attributo, per impostazione predefinita C# consente di usare l'attributo in una qualsiasi delle destinazioni possibili. Se si vuole limitare l'attributo ad alcune destinazioni, è possibile usare `AttributeUsageAttribute` nella classe di attributo, ovvero un attributo in un attributo.

[!code-csharp[Uso di un attributo personalizzato](../../../samples/snippets/csharp/tutorials/attributes/Program.cs#AttributeUsageExample1)]

Se si prova a inserire l'attributo precedente in un elemento diverso da una classe o da un tipo struct, si otterrà un errore del compilatore simile al seguente: `Attribute 'MyAttributeForClassAndStructOnly' is not valid on this declaration type. It is only valid on 'class, struct' declarations`

[!code-csharp[Uso di un attributo personalizzato](../../../samples/snippets/csharp/tutorials/attributes/Program.cs#AttributeUsageExample2)]

## <a name="how-to-use-attributes-attached-to-a-code-element"></a>Come usare attributi associati a un elemento di codice

Gli attributi agiscono come metadati. Senza una forza verso l'esterno, non hanno alcuna funzione.

Per trovare e intervenire sugli attributi, è in genere necessario usare la [reflection](../programming-guide/concepts/reflection.md). Il concetto di reflection non verrà approfondito in questa esercitazione ma, in termini generali, la reflection consente di scrivere codice C# che esamina altro codice.

È possibile, ad esempio, usare la reflection per ottenere informazioni su una classe: 

[!code-csharp[Acquisizione di informazioni sui tipi con la reflection](../../../samples/snippets/csharp/tutorials/attributes/Program.cs#ReflectionExample1)]

Verrà generato un output simile al seguente: `The assembly qualified name of MyClass is ConsoleApplication.MyClass, attributes, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null`

Dopo aver creato un oggetto `TypeInfo` (o `MemberInfo`, `FieldInfo` e così via), è possibile usare il metodo `GetCustomAttributes`. Verrà restituita una raccolta di oggetti `Attribute`.
È possibile anche usare `GetCustomAttribute` e specificare un tipo di attributo.

Di seguito è riportato un esempio d'uso di `GetCustomAttributes` in un'istanza di `MemberInfo` per `MyClass` (che, come specificato in precedenza, include un attributo `[Obsolete]`).

[!code-csharp[Acquisizione di informazioni sui tipi con la reflection](../../../samples/snippets/csharp/tutorials/attributes/Program.cs#ReflectionExample2)]

Nella console verrà visualizzato l'output seguente: `Attribute on MyClass: ObsoleteAttribute`. Provare ad aggiungere altri attributi a `MyClass`.

È importante sottolineare che le istanze di questi oggetti `Attribute` vengono create in modo differito, ovvero non vengono create finché non si usa `GetCustomAttribute` o `GetCustomAttributes`.
L'istanza, inoltre, viene creata ogni volta. Se si chiama `GetCustomAttributes` due volte in una riga, verranno restituite due istanze diverse di `ObsoleteAttribute`.

## <a name="common-attributes-in-the-base-class-library-bcl"></a>Attributi comuni nella libreria di classi base

Gli attributi vengono usati da molti tipi di strumenti e framework. NUnit si avvale di attributi come `[Test]` e `[TestFixture]`, usati dal test runner NUnit. ASP.NET MVC usa attributi come `[Authorize]` e fornisce un framework di filtri di azione per applicare questioni trasversali su azioni MVC. [PostSharp](https://www.postsharp.net) usa la sintassi di attributo per consentire la programmazione orientata agli aspetti in C#.

Di seguito sono illustrati alcuni attributi importanti incorporati nelle librerie di classi base di .NET Core:

* `[Obsolete]`. Questo attributo è stato usato negli esempi precedenti e si trova nello spazio dei nomi `System`. È utile per fornire documentazione dichiarativa su una codebase in fase di modifica. È possibile specificare un messaggio sotto forma di stringa e usare un altro parametro booleano per convertire un avviso del compilatore in un errore del compilatore.

* `[Conditional]`. Questo attributo si trova nello spazio dei nomi `System.Diagnostics` e può essere applicato a metodi (o a classi di attributo). È necessario passare una stringa al costruttore.
Se la stringa corrisponde a una direttiva `#define`, qualsiasi chiamata al metodo (ma non il metodo stesso) verrà rimossa dal compilatore C#. Questo attributo viene in genere usato per attività di debug (diagnostica).

* `[CallerMemberName]`. Questo attributo può essere usato nei parametri e si trova nello spazio dei nomi `System.Runtime.CompilerServices`. Consente di inserire il nome del metodo che chiama un altro metodo. Viene in genere usato per eliminare "stringhe magiche" quando si implementa INotifyPropertyChanged in vari framework di interfaccia utente. Ad esempio:

[!code-csharp[Uso di CallerMemberName quando si implementa INotifyPropertyChanged](../../../samples/snippets/csharp/tutorials/attributes/Program.cs#CallerMemberName1)]

Nel codice precedente non è necessario che sia inclusa una stringa `"Name"` letterale. In questo modo, infatti, si evitano bug correlati a errori di digitazione e si semplificano eventuali operazioni di refactoring/ridenominazione.

## <a name="summary"></a>Riepilogo

Gli attributi integrano funzioni dichiarative in C#. Rappresentano tuttavia elementi di codice simili ai metadati e da soli non hanno alcuna funzione.

