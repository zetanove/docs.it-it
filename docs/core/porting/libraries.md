---
title: "Portabilità in .NET Core - Librerie"
description: "Portabilità in .NET Core - Librerie"
keywords: .NET, .NET Core
author: cartermp
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: a0fd860d-d6b6-4659-b325-8a6e6f5fa4a1
ms.translationtype: Human Translation
ms.sourcegitcommit: 50e128137fde445f64e10cf7c2a1ee5fdecb34e6
ms.openlocfilehash: 883745ca26a9c0d4bd1db805da603aa6e2c41972
ms.contentlocale: it-it
ms.lasthandoff: 05/01/2017

---

# <a name="porting-to-net-core---libraries"></a>Portabilità in .NET Core - Librerie

Con la versione di .NET Core 1.0 è possibile trasferire il codice di libreria esistente per consentirne l'esecuzione su più piattaforme. Questo articolo descrive la libreria .NET Standard e le tecnologie non disponibili. Spiega inoltre come tener conto del minor numero possibile di API disponibili in .NET Core 1.0 e come usare gli strumenti forniti con .NET Core SDK Preview 2. Illustra infine gli approcci consigliati per il trasferimento del codice.

Il trasferimento è un'attività che può richiedere diverso tempo, in particolare se si dispone di una CodeBase di grandi dimensioni. È inoltre consigliabile essere pronti ad adattare le indicazioni fornite secondo quanto necessario per il proprio codice. Ogni CodeBase è differente, motivo per cui questo articolo tenta di spiegare i concetti in modo flessibile. È tuttavia possibile che, in base alle specifiche esigenze, sia necessario scostarsi dalle linee guida offerte.

## <a name="prerequisites"></a>Prerequisiti

Questo articolo presuppone l'uso di Visual Studio 2017 o versione successiva in Windows. I componenti necessari per la compilazione del codice .NET Core non sono disponibili nelle precedenti versioni di Visual Studio.

Questo articolo presuppone inoltre che l'utente abbia compreso il [processo di trasferimento consigliato](index.md) e che abbia risolto qualsiasi problema relativo a [dipendenze di terze parti](third-party-deps.md).

## <a name="targeting-the-net-standard-library"></a>Definizione della libreria .NET Standard come destinazione

Il modo migliore per creare una libreria multipiattaforma per .NET Core è definire la [libreria .NET Standard](../../standard/library.md) come destinazione. La libreria .NET Standard è la specifica formale delle API .NET che devono essere disponibili in tutti i runtime .NET. È supportata dal runtime di .NET Core.

Questo significa che sarà necessario trovare un compromesso tra le API che è possibile usare e le piattaforme che è possibile supportare, scegliendo la versione della piattaforma standard .NET più adatta al compromesso scelto.

Al momento sono disponibili sette differenti versioni, da .NET Standard 1.0 a .NET Standard 1.6. Se si sceglie una versione più recente, si ha accesso a un numero più alto di API, ma con la possibilità di eseguire il codice su un numero minore di destinazioni. Se invece si sceglie una versione meno recente, è possibile eseguire il codice su un numero maggiore di destinazioni, ma con conseguente riduzione del numero di API disponibili.

Per praticità, di seguito è riportata una matrice con le diverse versioni di .NET Standard e le relative aree di esecuzione:

| Nome della piattaforma | Alias |  |  |  |  |  | | |
| :---------- | :--------- |:--------- |:--------- |:--------- |:--------- |:--------- |:--------- |:--------- |
|.NET Standard | netstandard | 1.0 | 1.1 | 1.2 | 1.3 | 1.4 | 1,5 | 1.6 |
|.NET Core|netcoreapp|&rarr;|&rarr;|&rarr;|&rarr;|&rarr;|&rarr;|1.0|
|.NET Framework|net|&rarr;|4.5|4.5.1|4.6|4.6.1|4.6.2|4.6.3|
|Piattaforme Mono/Xamarin||&rarr;|&rarr;|&rarr;|&rarr;|&rarr;|&rarr;|*|
|Piattaforma UWP (Universal Windows Platform)|uap|&rarr;|&rarr;|&rarr;|&rarr;|10.0|||
|Windows|win|&rarr;|8.0|8.1|||||
|Windows Phone|wpa|&rarr;|&rarr;|8.1|||||
|Silverlight per Windows Phone|wp|8.0|||||||

Un fattore chiave da comprendere è che **un progetto che ha come destinazione una versione meno recente non può fare riferimento a un progetto che ha come destinazione una versione più recente**. Ad esempio, un progetto che ha come destinazione la piattaforma standard .NET versione 1.2 non può fare riferimento a progetti che hanno come destinazione la piattaforma standard .NET versione 1.3 o successiva. I progetti, tuttavia, **possono** fare riferimento a versioni meno recenti: un progetto che ha come destinazione la piattaforma standard .NET versione 1.3 può fare riferimento a un progetto che ha come destinazione la piattaforma standard .NET versione 1.2 o precedente.

È consigliabile scegliere la versione della piattaforma standard .NET meno recente e usarla in tutto il progetto.

Per altre informazioni, vedere [.NET Platform Standard Library](../../standard/library.md) (Libreria della piattaforma standard .NET).

## <a name="key-technologies-not-yet-available-on-the-net-standard-or-net-core"></a>Tecnologie chiave non ancora disponibili in .NET Standard o .NET Core

È possibile che gli utenti usino tecnologie disponibili per .NET Framework che però non sono attualmente disponibili per .NET Core. Ciascuna delle sottosezioni seguenti corrisponde a una di queste tecnologie. Vengono inoltre elencate opzioni alternative eventualmente adottabili.

### <a name="app-domains"></a>Domini app

È possibile usare Domini app per diverse finalità all'interno di .NET Framework. Per l'isolamento del codice, è consigliabile usare come alternativa processi e/o contenitori separati. Per il caricamento dinamico di assembly è consigliabile usare la nuova classe @System.Runtime.Loader.AssemblyLoadContext.

### <a name="remoting"></a>Servizi remoti

Per la comunicazione tra processi, è possibile usare il meccanismo IPC (Inter-Process Communication) in alterativa alla comunicazione remota, ad esempio [pipe](https://docs.microsoft.com/dotnet/core/api/system.io.pipes) o [file mappati alla memoria](https://docs.microsoft.com/dotnet/core/api/system.io.memorymappedfiles.memorymappedfile).

Per la comunicazione tra computer è possibile usare come alternativa una soluzione di rete, ad esempio un protocollo in testo normale con sovraccarico ridotto quale HTTP. [KestrelHttpServer](https://github.com/aspnet/KestrelHttpServer), il server Web usato da ASP.NET Core, rappresenta un'opzione utilizzabile. La generazione in remoto del proxy tramite [Castle.Core](https://github.com/castleproject/Core) è un'ulteriore opzione da prendere in considerazione.

### <a name="binary-serialization"></a>Serializzazione binaria

Sono disponibili diverse tecnologie di serializzazione da usare in alternativa alla serializzazione binaria. È consigliabile sceglierne una adatta alle proprie finalità in termini di formattazione e footprint. Le scelte più comuni includono quanto segue:

* [JSON.NET](http://www.newtonsoft.com/json) per JSON
* @System.Runtime.Serialization.DataContractSerializer per XML e JSON
* @System.Xml.Serialization.XmlSerializer per XML
* [protobuf-net](https://github.com/mgravell/protobuf-net) per i buffer di protocollo

Per conoscere i vantaggi offerti e scegliere le soluzioni più adatte alle specifiche esigenze, fare riferimento alle risorse collegate. Esistono molti altri formati e tecnologie di serializzazione, molti dei quali open source.

### <a name="sandboxes"></a>Sandbox

In alternativa al sandboxing, è possibile usare i limiti di sicurezza forniti dal sistema operativo, ad esempio gli account utente, per eseguire i processi con il set di privilegi più ridotto.

## <a name="overview-of-projectjson"></a>Panoramica di `project.json`

Il [modello di progetto project.json](../tools/project-json.md) viene fornito con .NET Core SDK 1.0 Preview 2. Tale modello offre i vantaggi seguenti:

* Multitargeting semplice, con la possibilità di generare assembly specifici della destinazione a partire da una singola compilazione.
* Possibilità di generare facilmente un pacchetto NuGet con una compilazione del progetto.
* Nessuna necessità di elencare file nel file di progetto.
* Unificazione delle dipendenze dei pacchetti NuGet e delle dipendenze da progetto a progetto.

> Anche se alla fine `project.json` verrà deprecato, è attualmente possibile usarlo per compilare librerie in .NET Standard.

### <a name="the-project-file-projectjson"></a>File di progetto: `project.json`

I progetti .NET Core sono definiti come una directory contenente un file `project.json`. In questo file vengono dichiarati diversi elementi del progetto, ad esempio le dipendenze del pacchetto, la configurazione del compilatore, la configurazione del runtime e molto altro.

Il comando `dotnet restore` legge questo file, ripristina tutte le dipendenze del progetto e genera un file `project.lock.json`. Questo file contiene tutte le informazioni di cui il sistema di compilazione ha bisogno per compilare il progetto.

Per altre informazioni sul file `project.json`, vedere [project.json reference](../tools/project-json.md) (Riferimenti di project.json).

### <a name="the-solution-file-globaljson"></a>File di soluzione: `global.json`

Il file `global.json` è un file opzionale da includere in una soluzione contenente più progetti. Si trova in genere nella directory radice di un set di progetti. Può essere usato per indicare al sistema di compilazione le differenti sottodirectory che possono contenere progetti. Questa affermazione vale per i sistemi di grandi dimensioni composti da diversi progetti.

Ad esempio, è possibile organizzare il codice in cartelle di livello superiore `/src` e `/test`, come mostrato di seguito:

```json
{
    "projects":[ "src", "test" ]
}
```

È quindi possibile avere più file `project.json` nelle relative sottocartelle all'interno di `/src` e `/test`.

### <a name="how-to-multitarget-with-projectjson"></a>Come definire più destinazioni con `project.json`

Diverse librerie definiscono più destinazioni per ottenere la massima copertura possibile. Con .NET Core la definizione di più destinazioni è un "oggetto di prima classe": questo significa che è possibile generare facilmente assembly specifici della piattaforma con una sola compilazione.

Il multitargeting è semplice quanto l'aggiunta del TFM (Target Framework Moniker) corretto al file `project.json`, mediante l'uso delle dipendenze corrette per ciascuna destinazione (`dependencies` per .NET Core e `frameworkAssemblies` per .NET Framework) e potenzialmente mediante l'uso delle direttive `#if` per la compilazione condizionale del codice sorgente per l'utilizzo delle API specifiche della piattaforma.

Si supponga, ad esempio, di compilare una libreria in cui si vogliono eseguire alcune operazioni di rete. Si vuole inoltre che la libreria possa essere eseguita in tutte le versioni di .NET Framework, in un profilo della libreria di classi portabile e in .NET Core. Per le destinazioni .NET Core e .NET Framework 4.5 e versione successiva, è possibile usare la libreria `System.Net.Http` e `async`/`await`. Per le precedenti versioni di .NET Framework, tuttavia, tali API non sono disponibili.

Di seguito è riportata una sezione `frameworks` di esempio per un file `project.json` che ha come destinazione le versioni 2.0, 3.5, 4.0 e 4.5 di .NET Framework, oltre a .NET Standard 1.6:

```javascript
{
    "frameworks":{
        "net20":{
            "frameworkAssemblies":{
                "System.Net":""
            }
        },
        "net35":{
            "frameworkAssemblies":{
                "System.Net":""
            }
        },
        "net40":{
            "frameworkAssemblies":{
                "System.Net":""
            }
        },
        "net45":{
            "frameworkAssemblies":{
                "System.Net.Http":"",
                "System.Threading.Tasks":""
            }
        },
        ".NETPortable,Version=v4.5,Profile=Profile259": {
            "buildOptions": {
                "define": [ "PORTABLE" ]
             },
             "frameworkAssemblies":{
                 "mscorlib":"",
                 "System":"",
                 "System.Core":"",
                 "System.Net.Http":""
             }
        },
        "netstandard16":{
            "dependencies":{
                "NETStandard.Library":"1.6.0",
                "System.Net.Http":"4.0.1",
                "System.Threading.Tasks":"4.0.11"
            }
        },
    }
}
```

Si noti che le destinazioni delle librerie di classi portabili sono speciali: richiedono infatti la specifica di una definizione di compilazione che il compilatore possa riconoscere. Richiedono inoltre la specifica di tutti gli assembly usati, incluso `mscorlib`.

Il codice sorgente può quindi usare le dipendenze, come mostrato di seguito:

```csharp
#if (NET20 || NET35 || NET40 || PORTABLE)
using System.Net;
#else
using System.Net.Http;
using System.Threading.Tasks;
#endif
```

Si noti che tutte le destinazioni .NET Framework e .NET Standard hanno nomi riconosciuti dal compilatore:

```
.NET Framework 2.0   --> NET20
.NET Framework 3.5   --> NET35
.NET Framework 4.0   --> NET40
.NET Framework 4.5   --> NET45
.NET Framework 4.5.1 --> NET451
.NET Framework 4.5.2 --> NET452
.NET Framework 4.6   --> NET46
.NET Framework 4.6.1 --> NET461
.NET Framework 4.6.2 --> NET462
.NET Standard 1.0    --> NETSTANDARD1_0
.NET Standard 1.1    --> NETSTANDARD1_1
.NET Standard 1.2    --> NETSTANDARD1_2
.NET Standard 1.3    --> NETSTANDARD1_3
.NET Standard 1.4    --> NETSTANDARD1_4
.NET Standard 1.5    --> NETSTANDARD1_5
.NET Standard 1.6    --> NETSTANDARD1_6
```

Come indicato in precedenza, se si definisce come destinazione una libreria di classi portabile, sarà necessario specificare una definizione di compilazione che il compilatore sia in grado di comprendere. Non è presente alcuna definizione predefinita che il compilatore possa usare.

### <a name="using-projectjson-in-visual-studio"></a>Uso di `project.json` in Visual Studio

Per l'uso di `project.json` in Visual Studio, sono disponibili le due opzioni seguenti:

1. Un nuovo tipo di progetto Xproj.
2. Un progetto della libreria di classi portabile predestinato che supporta .NET Standard.

Per ciascuna opzione sono presenti vantaggi e svantaggi.

#### <a name="when-to-pick-an-xproj-project"></a>Quando scegliere un progetto Xproj

Il nuovo sistema di progetto Xproj di Visual Studio usa le funzionalità del modello di progetto basate su `project.json` per offrire due vantaggi rispetto ai tipi di progetto esistenti: multitargeting semplice mediante la compilazione di più assembly e possibilità di generare direttamente un pacchetto NuGet durante la fase di compilazione.

Questa scelta, tuttavia, comporta la perdita di alcune funzionalità, ad esempio quelle riportate di seguito:

- Supporto per F# o Visual Basic
- Generazione di assembly satellite con stringhe di risorsa localizzate
- Riferimento diretto a un file `.dll` nel file system
- Possibilità di fare riferimento a un progetto basato su csproj in Gestione riferimenti (a seconda del file `.dll` direttamente supportato)

Se le esigenze del progetto sono relativamente contenute e si intende trarre vantaggio dalle nuove funzionalità di Xproj, questo sistema di progetto è la scelta migliore. Questa operazione può essere eseguita in Visual Studio nel modo seguente:

1. Verificare di usare Visual Studio 2015 o versione successiva.
2. Selezionare File | Nuovo progetto.
3. Selezionare ".NET Core" nell'area Visual C#.
4. Selezionare il modello "Libreria di classi (.NET Core)". 

#### <a name="when-to-pick-a-pcl-project"></a>Quando scegliere un progetto della libreria di classi portabile

È possibile definire come destinazione .NET Core con il tradizionale sistema di progetto in Visual Studio creando una libreria di classi portabile e selezionando ".NET Core" nella finestra di dialogo per la configurazione del progetto. È quindi necessario ridestinare il progetto in modo che sia basato su .NET Standard:

1. Fare clic con il pulsante destro del mouse sul file di progetto in Visual Studio e scegliere Proprietà.
2. Nell'area Compilazione selezionare "Convert to .NET Standard" (Converti in .NET Standard).

Se sono presenti esigenze di sistema di progetto più complesse, questa è la scelta corretta. Si noti che, se si vuole eseguire il multitargeting generando assembly specifici della piattaforma come con il sistema di progetto `xproj`, sarà necessario creare una libreria di classi portabile con la tecnica dello "specchietto per le allodole", come descritto in [How to Make Portable Class Libraries Work for You](https://blogs.msdn.microsoft.com/dsplaisted/2012/08/27/how-to-make-portable-class-libraries-work-for-you/) (Come usare le librerie di classi portabili).

## <a name="retargeting-your-net-framework-code-to-net-framework-462"></a>Ridestinazione del codice .NET Framework a .NET Framework 4.6.2

Se il codice non ha come destinazione .NET Framework 4.6.2, è consigliabile ridestinarlo. Questa operazione assicura che vengano sempre usate le più recenti alternative alle API nei casi in cui .NET Standard non supporta le API esistenti.

Per ciascuno dei progetti Visual Studio che si vuole trasferire, effettuare le operazioni seguenti:

1. Fare clic con il pulsante destro del mouse sul progetto e scegliere Proprietà.
2. Nell'elenco a discesa "Versione .NET Framework di destinazione" selezionare ".NET Framework 4.6.2".
3. Ricompilare i progetti.

L'operazione è ora completata. Poiché i progetti hanno ora come destinazione .NET Framework 4.6.2, è possibile usare tale versione come base per il trasferimento del codice.

## <a name="determining-the-portability-of-your-code"></a>Determinazione della portabilità del codice

Il passaggio successivo consiste nell'esecuzione di ApiPort (API Portability Analyzer) per generare un report sulla portabilità che è possibile iniziare ad analizzare.

Assicurarsi di comprendere lo strumento [ApiPort](https://github.com/Microsoft/dotnet-apiport/blob/master/docs/HowTo/) e di essere in grado di generare report sulla portabilità per specificare come destinazione .NET Core. La procedura dipenderà probabilmente dalle esigenze e dai gusti personali. Di seguito sono riportati alcuni approcci. A seconda della strutturazione del codice, può essere necessario usare una combinazione di tali strategie.

### <a name="dealing-primarily-with-the-compiler"></a>Gestire principalmente il compilatore

Questo approccio può rivelarsi la scelta migliore per progetti di piccole dimensioni o per progetti che non usano un numero elevato di API .NET Framework. L'approccio è molto semplice:

1. Eseguire ApiPort sul progetto (facoltativo).
2. Se è stato eseguito ApiPort, rivedere velocemente il report.
3. Copiare tutto il codice in un nuovo progetto .NET Core.
4. Risolvere gli eventuali errori durante la compilazione, se necessario facendo riferimento al report sulla portabilità.
5. Se necessario, ripetere i passaggi.

Anche se molto poco strutturato, questo approccio centrato sul codice può consentire la rapida risoluzione di eventuali problemi e può costituire la scelta migliore per i progetti o le librerie di minori dimensioni. Un progetto contenente solo modelli di dati può essere un candidato ideale per questo approccio.

### <a name="staying-on-the-net-framework-until-portability-issues-are-resolved"></a>Rimanere in .NET Framework fino alla risoluzione dei problemi di portabilità

Questo approccio può costituire la scelta migliore se si preferisce che il codice venga compilato durante l'intero processo. Di seguito viene riportata la descrizione di questo approccio:

1. Eseguire ApiPort su un progetto.
2. Risolvere i problemi usando diverse API portabili.
3. Prendere nota delle aree in cui non è possibile usare un'alternativa diretta.
4. Ripetere i passaggi da 1 a 3 per tutti i progetti in fase di trasferimento, fino a quando non si è certi che ciascuno di essi è pronto per essere copiato in un progetto .NET Core.
5. Copiare il codice in un nuovo progetto .NET Core.
6. Risolvere gli eventuali problemi di cui si è preso nota.

Questo approccio attento è più strutturato rispetto alla semplice risoluzione degli errori del compilatore, ma è ancora relativamente centrato sul codice e offre il vantaggio di consentirne sempre la compilazione. I modi in cui gli utenti correggono determinati problemi non risolvibili mediante il semplice uso di un'altra API possono variare notevolmente. È possibile che si ritenga necessario sviluppare un piano più completo per determinati progetti, approccio descritto nella sezione seguente.

### <a name="developing-a-comprehensive-plan-of-attack"></a>Sviluppare un piano di attacco completo

Questo approccio può costituire la scelta migliore per progetti più complessi e di maggiori dimensioni, in cui per supportare .NET Core può essere necessaria la ristrutturazione del codice o la riscrittura di determinate aree. Di seguito viene riportata la descrizione di questo approccio:

1. Eseguire ApiPort su un progetto.
2. Determinare i punti del codice in cui viene usato ciascun tipo non portabile e stabilire l'entità dell'impatto sulla portabilità complessiva.

   a. Comprendere la natura di tali tipi. Sono in numero limitato, ma di uso frequente? Sono numerosi, ma usati raramente? Il loro uso è concentrato o distribuito in tutto il codice?
   
   b. È possibile isolare facilmente il codice non portabile per gestirlo con maggiore semplicità?
   
   c. È necessario effettuare il refactoring del codice?
   
   d. Per i tipi non portabili, esistono API alternative che svolgono la stessa attività? Ad esempio, se si usa la classe `WebClient`, è possibile usare al suo posto la classe `HttpClient`.
   
   e. Esistono API portabili differenti che è possibile usare per eseguire un'attività, anche se non si tratta di una sostituzione vera e propria? Ad esempio, se si usa `XmlSchema` per analizzare XML ma non è necessaria l'individuazione dello schema XML, è possibile usare le API `System.Linq.Xml` e analizzare i dati manualmente.

3. Se sono presenti assembly difficili da trasferire, è opportuno lasciarli per il momento in .NET Framework? Di seguito sono riportati alcuni aspetti da prendere in considerazione:

   a. Alcune funzionalità della libreria possono non essere compatibili con .NET Core poiché sono basate in misura eccessiva su funzionalità specifiche di .NET Framework o di Windows. È opportuno trascurare momentaneamente tali funzionalità non compatibili e rilasciare una versione .NET Core della libreria con un numero minore di funzionalità?
   
   b. Un'operazione di refactoring può risultare vantaggiosa?
   
4. La scrittura di una propria implementazione di un'API .NET Framework non disponibile è una scelta ragionevole?

   Può essere invece opportuno copiare, modificare e usare codice tratto da [.NET Framework Reference Source](https://github.com/Microsoft/referencesource) (Codice sorgente di riferimento .NET Framework). Tale codice è disponibile con [Licenza MIT](https://github.com/Microsoft/referencesource/blob/master/LICENSE.txt), con conseguente significativa libertà di utilizzo per gli utenti. È sufficiente assicurarsi di attribuire la creazione del codice a Microsoft.
   
5. Ripetere questo processo in base alle esigenze per i diversi progetti.
6. Dopo aver definito un piano, passare alla fase di esecuzione.
 
A seconda delle dimensioni della CodeBase, la fase di analisi può richiedere diverso tempo. Il tempo dedicato a questa fase per comprendere appieno l'ambito delle modifiche necessarie e sviluppare un piano può assicurare un notevole risparmio di tempo durante la fase di esecuzione, in particolare se si dispone di una CodeBase più complessa.

Il piano può comportare la necessità di modifiche significative della CodeBase, mantenendo tuttavia come destinazione .NET Framework 4.6.2. Si tratta di una versione più strutturata dell'approccio precedente. La modalità di esecuzione del piano dipende dalle caratteristiche della CodeBase.

### <a name="mixing-approaches"></a>Combinazione di approcci

È probabile che, in base al tipo di progetto, sia necessario combinare gli approcci descritti in precedenza. È consigliabile effettuare le scelte più corrette per il progetto e la CodeBase.

## <a name="porting-your-tests"></a>Trasferimento dei test

Il modo migliore per verificare un codice trasferito consiste nell'eseguirne il test durante il trasferimento in .NET Core. A tale scopo è necessario usare un framework di test che compilerà ed eseguirà test per .NET Core. Attualmente sono disponibili le tre opzioni seguenti:

* [xUnit](https://xunit.github.io/)
   - [Introduzione](http://xunit.github.io/docs/getting-started-dotnet-core.html)
   - [Strumento per trasferire un progetto MSTest in xUnit](https://github.com/dotnet/codeformatter/tree/master/src/XUnitConverter)
* [NUnit](http://www.nunit.org/)
  - [Introduzione](https://github.com/nunit/docs/wiki/Installation)
  - [Post di blog sulla migrazione da MSTest a NUnit](http://www.florian-rappl.de/News/Page/275/convert-mstest-to-nunit)
* [MSTest](https://msdn.microsoft.com/library/ms243147.aspx)

## <a name="recommended-approach-to-porting"></a>Approccio consigliato per il porting

Una volta eseguite le operazioni descritte in precedenza, è possibile trasferire il codice. In definitiva, l'effettiva entità del lavoro di trasferimento dipende in larga misura dal modo in cui il codice .NET Framework è strutturato. Detto questo, di seguito è descritto un approccio consigliato che dovrebbe funzionare correttamente con la CodeBase.

Un buon metodo per trasferire il codice consiste nell'iniziare con la "base" della libreria. Può trattarsi di modelli o di altri metodi e classi fondamentali usati dagli altri elementi in modo diretto o indiretto.

1. Trasferire il progetto di test, operazione che verifica il livello della libreria attualmente in fase di trasferimento.
2. Copiare la "base" della libreria in un nuovo progetto .NET Core e selezionare la versione di .NET Standard che si vuole supportare.
3. Apportare le modifiche necessarie per consentire la compilazione del codice. Può essere necessario aggiungere le dipendenze di un pacchetto NuGet al file `project.json`.
4. Eseguire i test e apportare le modifiche eventualmente necessarie.
5. Selezionare il successivo livello di codice da trasferire e ripetere i passaggi 2 e 3.

Spostandosi metodicamente dalla base all'esterno della libreria e testando ogni livello nel modo necessario, il trasferimento risulterà un processo sistematico in cui i problemi vengono isolati in un livello di codice alla volta.

