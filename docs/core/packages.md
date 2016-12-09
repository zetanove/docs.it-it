---
title: Pacchetti, metapacchetti e framework
description: Pacchetti, metapacchetti e framework
keywords: .NET, .NET Core
author: richlander
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: 609b0845-49e7-4864-957b-21ffe1b93bf2
translationtype: Human Translation
ms.sourcegitcommit: cb2e83b35b5a4aae14c89bcbdf26b064885a477a
ms.openlocfilehash: 6b5bb7042fdaa453966a4fc576291b3c90ee5410

---

# <a name="packages-metapackages-and-frameworks"></a>Pacchetti, metapacchetti e framework

.NET Core è una piattaforma costituita da pacchetti NuGet. Alcuni prodotti traggono vantaggio da una definizione dei pacchetti con granularità fine, mentre altri da una definizione con granularità più grossolana. Per tenere conto di questo dualismo, il prodotto viene distribuito come set di pacchetti con granularità fine e quindi viene descritto in blocchi più grossolani con un tipo di pacchetto denominato in modo informale "metapacchetto".

Ciascuno dei pacchetti .NET Core supporta l'esecuzione su più runtime .NET, rappresentati come framework. Alcuni di questi framework sono tradizionali, ad esempio `net46`, e rappresentano l'istanza .NET Framework. Un altro insieme è costituito da nuovi framework che possono essere considerati come "framework basati su pacchetti", il che stabilisce un nuovo modello di definizione dei framework stessi. Questi framework basati su pacchetti sono interamente formati e definiti come pacchetti, creando una forte relazione tra pacchetti e framework.

## <a name="packages"></a>Pacchetti

.NET Core è suddiviso in un set di pacchetti che forniscono primitive, tipi di dati di livello superiore, tipi di composizione delle app e utilità di uso comune. Ognuno di questi pacchetti rappresenta un singolo assembly con lo stesso nome. Ad esempio, [System.Runtime](https://www.nuget.org/packages/System.Runtime) contiene System.Runtime.dll. 

La definizione dei pacchetti con granularità fine presenta alcuni vantaggi:

- I pacchetti con granularità fine possono essere distribuiti in base a una specifica pianificazione, con operazioni di test di altri pacchetti relativamente limitate.
- I pacchetti con granularità fine possono fornire supporto per diversi sistemi operativi e CPU.
- I pacchetti con granularità fine possono avere dipendenze specifiche da una sola libreria.
- Le app hanno dimensioni ridotte perché i pacchetti senza riferimenti non diventano parte della distribuzione delle app stesse.

Alcuni di questi vantaggi vengono sfruttati solo in particolari circostanze. I pacchetti .NET Core, ad esempio, possono essere distribuiti in base alla stessa pianificazione con lo stesso supporto di piattaforma. Nel caso di interventi di manutenzione, le correzioni possono essere distribuite e installate come piccoli aggiornamenti di singoli pacchetti. A causa del ristretto ambito di modifica, le operazioni di convalida e il tempo necessario per rendere una correzione disponibile sono limitati a quanto necessario per una singola libreria.

Di seguito è riportato un elenco dei principali pacchetti NuGet per .NET Core:

- [System.Runtime](https://www.nuget.org/packages/System.Runtime): principale pacchetto .NET Core. Sono inclusi [Object](http://docs.microsoft.com/dotnet/core/api/System.Object), [String](http://docs.microsoft.com/dotnet/core/api/System.String), [Array](http://docs.microsoft.com/dotnet/core/api/System.Array), [Action](http://docs.microsoft.com/dotnet/core/api/System.Action) e [IList&lt;T&gt;](http://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.IList-1).
- [System.Collections](https://www.nuget.org/packages/System.Collections): set di raccolte (essenzialmente) generiche. Sono inclusi [List&lt;T&gt;](http://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.List-1) e [Dictionary&lt;K,V&gt;](http://docs.microsoft.com/dotnet/core/api/System.Collections.Generic.Dictionary-2).
- [System.Net.Http](https://www.nuget.org/packages/System.Net.Http): set di tipi per la comunicazione di rete HTTP. Sono inclusi [HttpClient](http://docs.microsoft.com/dotnet/core/api/System.Net.Http.HttpClient) e [HttpResponseMessage](http://docs.microsoft.com/dotnet/core/api/System.Net.Http.HttpResponseMessage).
- [System.IO.FileSystem](https://www.nuget.org/packages/System.IO.FileSystem): set di tipi per la lettura e la scrittura in sistemi di archiviazione basati su disco locali o di rete. Sono inclusi [File](http://docs.microsoft.com/dotnet/core/api/System.IO.File) e [Directory](http://docs.microsoft.com/dotnet/core/api/System.IO.Directory).
- [System.Linq](https://www.nuget.org/packages/System.Linq): set di tipi di oggetti di query. Sono inclusi Enumerable, [ILookup&lt;TKey e TElement&gt;](http://docs.microsoft.com/dotnet/core/api/System.Linq.ILookup-2).
- [System.Reflection](https://www.nuget.org/packages/System.Reflection): set di tipi per il caricamento, l'analisi e l'attivazione. Sono inclusi [Assembly](http://docs.microsoft.com/dotnet/core/api/System.Reflection.Assembly), [TypeInfo](http://docs.microsoft.com/dotnet/core/api/System.Reflection.TypeInfo) e [MethodInfo](http://docs.microsoft.com/dotnet/core/api/System.Reflection.MethodInfo).

Nel file project.json viene fatto riferimento ai pacchetti. Nell'esempio seguente viene fatto riferimento al pacchetto [System.Runtime](https://www.nuget.org/packages/System.Runtime/). 

```json
{
  "dependencies": {
    "System.Runtime": "4.1.0"
  },
  "frameworks": {
    "netstandard1.6": {}
  }
}
```

Nella maggior parte dei casi non viene fatto riferimento direttamente ai pacchetti .NET Core di livello più basso, perché si finirebbe con l'avere troppi pacchetti da gestire. Viene invece fatto riferimento a un metapacchetto.

## <a name="metapackages"></a>Metapacchetti

I metapacchetti sono una convenzione di NuGet per descrivere un set di pacchetti che sono significativi insieme. I metapacchetti rappresentano questo set di pacchetti trasformandoli in dipendenze. Facoltativamente, stabiliscono un framework per questo set di pacchetti specificando appunto un framework. 

Facendo riferimento a un metapacchetto, si aggiunge in effetti un riferimento a ciascuno dei suoi pacchetti dipendenti con una singola operazione. Questo significa che tutte le librerie ('ref' o 'lib') di tali pacchetti sono disponibili per IntelliSense (o esperienza simile) e per la pubblicazione dell'app (solo 'lib'). 

Nota: i termini 'lib' e 'ref' indicano cartelle dei pacchetti NuGet. Le cartelle 'ref' descrivono l'API pubblica di un pacchetto tramite metadati di assembly. Le cartelle 'lib' contengono l'implementazione di tale API pubblica per un determinato framework. 

L'uso dei metapacchetti presenta i vantaggi seguenti:

- Fornisce un'esperienza utente che consente di fare facilmente riferimento a un elevato numero di pacchetti con granularità fine. 
- Definisce un set di pacchetti (incluse versioni specifiche) che vengono testati e funzionano bene insieme.

Metapacchetto della libreria .NET Standard:

- [NETStandard.Library](https://www.nuget.org/packages/NETStandard.Library): descrive le librerie che fanno parte della "libreria .NET Standard". Si applica a tutte le implementazioni .NET, ad esempio .NET Framework, .NET Core e Mono, che supportano la libreria .NET Standard. Stabilisce il framework 'netstandard'.

I metapacchetti .NET Core chiave sono i seguenti:

- [Microsoft.NETCore.App](https://www.nuget.org/packages/Microsoft.NETCore.App): descrive le librerie che fanno parte della distribuzione .NET Core. Stabilisce il framework [`.NETCoreApp` ](https://github.com/dotnet/core-setup/blob/master/pkg/projects/Microsoft.NETCore.App/Microsoft.NETCore.App.pkgproj). Dipende dalla `NETStandard.Library` di minori dimensioni.
- [Microsoft.NETCore.Portable.Compatibility](https://www.nuget.org/packages/Microsoft.NETCore.Portable.Compatibility): set di caratteristiche di compatibilità che abilitano l'esecuzione in .NET Core di librerie di classi portabili basate su mscorlib.

Ai metapacchetti viene fatto riferimento nel file project.json come a qualsiasi altro pacchetto NuGet. 

Nell'esempio seguente viene fatto riferimento al metapacchetto `NETStandard.Library`, usato per creare librerie che possono essere trasferite tra runtime .NET.

```json
{
  "dependencies": {
    "NETStandard.Library": "1.6.0"
  },
  "frameworks": {
    "netstandard1.6": {}
  }
}
```

Nell'esempio seguente viene fatto riferimento al pacchetto `Microsoft.NETCore.App`, usato per creare app e librerie da eseguire in .NET Core sfruttandone appieno i vantaggi. Consente l'accesso a un set di librerie più grande rispetto a quello fornito dalla `NETStandard.Library`.

```json
{
  "dependencies": {
    "Microsoft.NETCore.App": "1.0.0"
  },
  "frameworks": {
    "netcoreapp1.0": {}
  }
}
```

## <a name="frameworks"></a>Framework

I pacchetti .NET Core supportano ciascuno un set di framework, dichiarati con cartelle di framework all'interno delle cartelle 'lib' e 'ref' menzionate in precedenza. I framework descrivono un set di API disponibili (e potenzialmente altre caratteristiche) che è possibile usare quando si definisce un determinato framework come destinazione. Vengono sottoposti al controllo delle versioni quando si aggiungono nuove API.

Ad esempio, [System.IO.FileSystem](https://www.nuget.org/packages/System.IO.FileSystem) supporta i framework seguenti:

- .NETFramework, versione 4.6
- .NETStandard,versione 1.3
- 6 piattaforme Xamarin, ad esempio xamarinios10

È utile confrontare i primi due di questi framework, in quanto sono esempi dei due diversi modi di definire i framework.

Il framework `.NETFramework,Version=4.6` rappresenta le API disponibili in .NET Framework 4.6. È possibile creare librerie compilate con assembly di riferimento .NET Framework 4.6 e quindi distribuirle in pacchetti NuGet in una cartella 'lib' net46. Questo procedimento verrà usato per app che hanno come destinazione .NET Framework 4.6 o che sono compatibili con esso. Quella sopra descritta è la tradizionale modalità di funzionamento dei framework.

`.NETStandard,Version=1.3` è un framework basato su pacchetti. Si basa su pacchetti che hanno come destinazione il framework per definire ed esporre le API in termini di framework.

## <a name="package-based-frameworks"></a>Framework basati su pacchetti

Tra i framework e i pacchetti è presente una relazione bidirezionale. La prima parte consiste nella definizione delle API disponibili per un determinato framework, ad esempio `netstandard1.3`. I pacchetti che hanno come destinazione `netstandard1.3` (o framework compatibili quali `netstandard1.0`) definiscono le API disponibili per `netstandard1.3`. Può sembrare una definizione circolare, ma non lo è. Poiché è basato su pacchetti, la definizione delle API per il framework deriva dai pacchetti. Il framework stesso non definisce alcuna API.

La seconda parte della relazione è la selezione delle risorse. I pacchetti possono contenere risorse per più framework. Dato un riferimento a un set di pacchetti e/o metapacchetti, il framework è necessario per determinare quale risorsa deve essere selezionata, ad esempio `net46` o `netstandard1.3`. È importante selezionare la risorsa corretta. Ad esempio, è improbabile che una risorsa `net46` sia compatibile con .NET Framework 4.0 o .NET Core 1.0.

![Composizione dei framework basati su pacchetti](./media/packages/package-framework.png)

La relazione è illustrata nella figura precedente. L'*API* identifica il *framework* come destinazione e lo definisce. Il *framework* viene usato per la *selezione delle risorse*. La *risorsa* fornisce l'API.

Dove termina la definizione di un framework basato su pacchetti e dove inizia l'utilizzo di tale definizione è una questione interessante. È possibile considerare la propria visualizzazione del framework come una funzione di un file project.json dato. Le dipendenze creano la visualizzazione del framework, indipendentemente dall'autore di tali dipendenze.

I due principali framework basati su pacchetti usati con .NET Core sono i seguenti:

- `netstandard`
- `netcoreapp`

### <a name="net-standard"></a>.NET Standard

Il framework .NET Standard (`netstandard`) rappresenta le API definite e compilate nella [libreria .NET Standard](../standard/library.md). Le librerie da eseguire su più runtime devono avere come destinazione questo framework. Tali librerie verranno supportate su qualsiasi runtime compatibile con .NET Standard, ad esempio .NET Core, .NET Framework e Mono/Xamarin. Ciascuno di questi runtime supporta un set di versioni di .NET Standard, a seconda delle API implementate. 

Il metapacchetto `NETStandard.Library` ha come destinazione il framework `netstandard`. Il modo più comune per definire `netstandard` come destinazione consiste nel fare riferimento a questo metapacchetto. Questo metapacchetto descrive e fornisce l'accesso alle circa 40 librerie .NET e alle API associate che definiscono la libreria .NET Standard. È possibile fare riferimento a pacchetti aggiuntivi che hanno `netstandard` come destinazione per ottenere accesso ad altre API.

Una determinata versione della [NETStandard.Library](versions/index.md) corrisponde alla più recente versione di `netstandard` esposta (tramite la relativa chiusura). Il riferimento al framework nel file project.json viene usato per selezionare le risorse corrette dai pacchetti sottostanti. In questo caso, sono necessarie le risorse `netstandard1.6` e non, ad esempio, le risorse `netstandard1.4` o `net46`. 

```json
{
  "dependencies": {
    "NETStandard.Library": "1.6.0"
  },
  "frameworks": {
    "netstandard1.6": {}
  }
}
```

I riferimenti al framework e al metapacchetto nel file project.json non devono necessariamente corrispondere. Ad esempio, il file project.json seguente è valido.

```json
{
  "dependencies": {
    "NETStandard.Library": "1.6.0"
  },
  "frameworks": {
    "netstandard1.3": {}
  }
}
```

Può sembrare strano definire come destinazione `netstandard1.3` ma usare la versione 1.6.0 della `NETStandard.Library`. Si tratta di un caso di uso valido, dal momento che il metapacchetto mantiene il supporto per le precedenti versioni di `netstandard`. Può trattarsi di una situazione in cui è stata definita come standard la versione 1.6.0 del pacchetto e tale versione è stata usata per tutte le librerie, che hanno come destinazione un'ampia gamma di versioni di `netstandard`. Con questo approccio, è sufficiente ripristinare `NETStandard.Library` 1.6.0 e non le versioni precedenti. 

La situazione opposta, ovvero la definizione di `netstandard1.6` come destinazione con la versione 1.3.0 della `NETStandard.Library`, non è valida. Non è possibile definire come destinazione la versione più recente di un framework con una versione precedente di un metapacchetto. La versione precedente del metapacchetto, infatti, non espone alcuna risorsa per la versione più recente del framework. Lo [schema di versionamento] per i metapacchetti impone che questi ultimi corrispondano alla versione più recente del framework che descrivono. In base a questo schema di versionamento, la prima versione della `NETStandard.Library` è la 1.6.0, dato che contiene le risorse `netstandard1.6`. La versione 1.3.0 viene usata nell'esempio precedente per simmetria, ma di fatto non esiste.

### <a name="net-core-application"></a>Applicazione .NET Core

Il framework .NET Core Application (`netcoreapp`) rappresenta i pacchetti e le API associate forniti con la distribuzione .NET Core e con il relativo modello di applicazione console offerto. Le app .NET Core devono usare questo framework poiché hanno come destinazione il modello dell'applicazione console. Devono usare questo framework anche le librerie da eseguire solo in .NET Core. L'uso di questo framework impone che le app e le librerie vengano eseguite solo in .NET Core. 

Il metapacchetto `Microsoft.NETCore.App` ha come destinazione il framework `netcoreapp`. Consente l'accesso a circa 60 librerie, circa 40 fornite dal pacchetto `NETStandard.Library` e le rimanenti 20 in aggiunta. È possibile fare riferimento a librerie aggiuntive che hanno come destinazione `netcoreapp` o framework compatibili, ad esempio `netstandard`, per ottenere l'accesso ad altre API. 

Anche la maggior parte delle librerie fornite da `Microsoft.NETCore.App` ha come destinazione `netstandard`, dato che le relative dipendenze sono soddisfatte da altre librerie `netstandard`. Questo significa che anche le librerie `netstandard` possono fare riferimento a tali pacchetti come dipendenze. 


<!--HONumber=Nov16_HO3-->


