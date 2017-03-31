---
title: Controllo delle versioni di C# | Guida a C#
description: Informazioni sul funzionamento del controllo delle versioni in C# e .NET
keywords: .NET, .NET Core, C#
author: tsolarin
manager: wpickett
ms.date: 01/08/2017
ms.topic: article
ms.prod: visual-studio-dev-14
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: aa8732d7-5cd0-46e1-994a-78017f20d861
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: bfa94e6d994f63adb13bdeea9b23f7130799b438
ms.lasthandoff: 03/13/2017

---

# <a name="versioning-in-c"></a>Controllo delle versioni in C# #

In questa esercitazione si apprenderà il significato del controllo delle versioni in .NET. Si apprenderanno anche i fattori da considerare durante il controllo delle versioni della libreria, nonché durante l'aggiornamento a una nuova versione di una libreria.

## <a name="authoring-libraries"></a>Creazione di librerie

Gli sviluppatori che hanno creato le librerie .NET per uso pubblico probabilmente si sono trovati in situazioni in cui è necessario distribuire i nuovi aggiornamenti. Le modalità di gestione di questo processo sono molto importanti poiché è necessario garantire che non si verifichino problemi durante la transizione del codice esistente alla nuova versione della libreria. Ecco alcuni aspetti da considerare quando si crea una nuova versione:

### <a name="semantic-versioning"></a>Versionamento Semantico

[Versionamento Semantico](http://semver.org/) (SemVer per brevità) è una convenzione di denominazione applicata alle versioni della libreria per indicare cardine specifici.
In teoria, le informazioni sulla versione applicate alla libreria consentono agli sviluppatori di determinare la compatibilità con i progetti che usano versioni precedenti di quella libreria.

L'approccio di base a SemVer è il formato a 3 componenti `MAJOR.MINOR.PATCH`, dove:
 
* `MAJOR` viene incrementato quando si apportano modifiche incompatibili all'API
* `MINOR` viene incrementato quando si aggiungono funzionalità compatibili con le versioni precedenti
* `PATCH` viene incrementato quando si apportano correzioni dei bug compatibili con le versioni precedenti

Esistono anche dei modi per specificare altri scenari, ad esempio le versioni non definitive, quando si applicano le informazioni sulla versione alla libreria .NET.

### <a name="backwards-compatibility"></a>Compatibilità con le versioni precedenti

Quando si rilasciano nuove versioni della libreria, la compatibilità con le versioni precedenti probabilmente è una delle principali preoccupazioni.
Una nuova versione della libreria è compatibile a livello di codice sorgente con una versione precedente se il codice che dipende dalla versione precedente, quando viene ricompilato, funziona con la nuova versione. Una nuova versione della libreria è compatibile a livello binario se un'applicazione che dipende dalla versione precedente funziona, senza ricompilazione, con la nuova versione.

Di seguito sono riportati alcuni aspetti da considerare quando si tenta di gestire la compatibilità della libreria con le versioni precedenti:

* Metodi virtuali: quando si trasforma un metodo virtuale in non virtuale nella nuova versione, sarà necessario aggiornare i progetti che eseguono l'override di tale metodo. Questa è una modifica sostanziale di grande impatto ed è fortemente sconsigliata.
* Firme del metodo: quando l'aggiornamento del comportamento di un metodo richiede anche la modifica della firma, è necessario creare un overload in modo tale che il codice che chiama il metodo continui a funzionare.
È sempre possibile modificare la firma del metodo precedente per chiamare la firma del nuovo metodo in modo che l'implementazione resti coerente.
* [Attributo Obsolete](programming-guide/concepts/attributes/common-attributes.md#Obsolete): è possibile usare questo attributo nel codice per specificare le classi o i membri di classe deprecati che potrebbero essere rimossi nelle versioni future.
Ciò consente di predisporre meglio gli sviluppatori che usano la libreria a eventuali modifiche di rilievo.
* Argomenti di metodo facoltativi: se si rendono obbligatori argomenti di metodo che in precedenza erano facoltativi o si modifica il valore predefinito degli argomenti, tutto il codice che non specifica tali argomenti dovrà essere aggiornato.
> [!NOTE]
> Rendere obbligatori gli argomenti facoltativi ha un impatto molto limitato, soprattutto se non modifica il comportamento del metodo.

Più è facile per gli utenti eseguire l'aggiornamento alla nuova versione della libreria, più rapido sarà l'aggiornamento.

### <a name="application-configuration-file"></a>File di configurazione dell'applicazione

Gli sviluppatori .NET molto probabilmente hanno trovato [il file `app.config`](https://msdn.microsoft.com/en-us/library/1fk1t1t0(v=vs.110).aspx) nella maggior parte dei tipi di progetto.
Questo semplice file di configurazione è in grado di ottimizzare la distribuzione dei nuovi aggiornamenti. In genere è consigliabile progettare le librerie in modo che le informazioni che probabilmente cambieranno regolarmente vengano memorizzate nel file `app.config`. Quando le informazioni vengono aggiornate è sufficiente sostituire il file di configurazione delle versioni precedenti con il nuovo file senza dover ricompilare la libreria.

## <a name="consuming-libraries"></a>Elaborazione delle librerie

Uno sviluppatore che elabora librerie .NET compilate da altri sviluppatori probabilmente sa che una nuova versione di una libreria potrebbe non essere completamente compatibile con il progetto e che spesso è necessario aggiornare il codice perché funzioni con le modifiche.

Sia C# che l'ecosistema .NET offrono funzionalità e tecniche che consentono di aggiornare facilmente l'applicazione in modo che funzioni con le nuove versioni delle librerie che potrebbero introdurre modifiche sostanziali.

### <a name="assembly-binding-redirection"></a>Reindirizzamento dell'associazione di assembly

È possibile usare il file `app.config` per aggiornare la versione di una libreria usata dall'applicazione. Aggiungendo il cosiddetto un [ *reindirizzamento di binding* ](https://msdn.microsoft.com/en-us/library/7wd6ex19(v=vs.110).aspx) è possibile usare la nuova versione della libreria senza dover ricompilare l'applicazione. Nell'esempio seguente viene illustrato come aggiornare il file `app.config` dell'applicazione per usare la versione di patch `1.0.1` di `ReferencedLibrary` anziché la versione `1.0.0` con cui è stata compilata in origine.

```xml
<dependentAssembly>
    <assemblyIdentity name="ReferencedLibrary" publicKeyToken="32ab4ba45e0a69a1" culture="en-us" />
    <bindingRedirect oldVersion="1.0.0" newVersion="1.0.1" />
</dependentAssembly>
```

> [!NOTE]
> Questo approccio funziona solo se la nuova versione di `ReferencedLibrary` è compatibile a livello binario con l'applicazione.
> Vedere la sezione [Compatibilità con le versioni precedenti](#backwards-compatibility) per verificare quando deve essere determinata la compatibilità.

### <a name="new"></a>new

Usare il modificatore `new` per nascondere i membri ereditati di una classe di base. In questo modo le classi derivate possono rispondere agli aggiornamenti nelle classi di base.

Vedere l'esempio seguente:

[!code-csharp[Esempio di uso del modificatore new](../../samples/csharp/versioning/new/Program.cs#sample)]

**Output**

```
A base method
A derived method
```

Nell'esempio precedente si può vedere come `DerivedClass` nasconde il metodo `MyMethod` presente in `BaseClass`.
Ciò significa che quando una classe di base nella nuova versione di una libreria aggiunge un membro già esistente nella classe derivata, è sufficiente usare il modificatore `new` per il membro della classe derivata per nascondere il membro della classe di base.

Se non si specifica alcun modificatore `new`, una classe derivata nasconderà per impostazione predefinita i membri in conflitto in una classe di base e il codice verrà comunque compilato anche se viene generato un avviso del compilatore. Ciò significa che la semplice aggiunta di nuovi membri a una classe esistente rende la nuova versione della libreria compatibile sia a livello di codice sorgente che a livello binario con il codice che dipende da essa.

### <a name="override"></a>override

Il modificatore `override` indica che un'implementazione derivata estende l'implementazione di un membro della classe di base anziché nasconderlo. È necessario che al membro della classe di base sia applicato il modificatore `virtual`.

[!code-csharp[Esempio di uso del modificatore override](../../samples/csharp/versioning/override/Program.cs#sample)]

**Output**

```
Base Method One: Method One
Derived Method One: Derived Method One
```

Il modificatore `override` viene valutato in fase di compilazione e il compilatore genera un errore se non trova un membro virtuale di cui eseguire l'override.

Conoscere le tecniche descritte e sapere in quali situazioni usarle significa semplificare notevolmente la transizione da una versione all'altra di una libreria.

