---
title: Architettura degli strumenti della riga di comando di .NET Core nell&quot;anteprima 3
description: L&quot;anteprima 3 introduce alcune modifiche all&quot;organizzazione complessiva degli strumenti .NET Core.
keywords: "interfaccia della riga di comando, estendibilità, comandi personalizzati, .NET Core"
author: blackdwarf
manager: wpickett
ms.date: 11/12/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
translationtype: Human Translation
ms.sourcegitcommit: 1a84c694945fe0c77468eb77274ab46618bccae6
ms.openlocfilehash: 233d365b582c274cd3a1f078846a6e854c7a6c95

---

<a name="high-level-overview-of-changes-in-cli-preview-3"></a>Panoramica di livello generale delle modifiche apportate all'interfaccia della riga di comando nell'anteprima 3
-----------------------------------------------

# <a name="overview"></a>Panoramica
Questo documento offre una descrizione di alto livello dei cambiamenti derivanti dal passaggio da `project.json` a MSBuild e al sistema di progetto `csproj`. Viene illustrata la nuova organizzazione su più livelli degli strumenti, vengono descritti i nuovi elementi disponibili e la loro collocazione nella struttura complessiva. Dopo la lettura di questo articolo gli utenti avranno una migliore comprensione degli elementi che compongono il set di strumenti .NET Core dopo il passaggio a MSBuild e `csproj`. 

> **Nota:** la lettura di questo articolo **non è necessaria** per l'uso degli strumenti della riga di comando dell'anteprima 3 di .NET Core. È possibile continuare a usare gli strumenti nel modo consueto. Scopo di questo articolo è illustrare il modo in cui il passaggio a MSBuild modifica l'organizzazione su più livelli e l'architettura complessiva degli strumenti della riga di comando. 

# <a name="moving-away-from-projectjson"></a>Abbandono di project.json
Il cambiamento più significativo negli strumenti dell'anteprima 3 di .NET Core è certamente l'[abbandono di project.json e il passaggio a csproj](https://blogs.msdn.microsoft.com/dotnet/2016/05/23/changes-to-project-json/) come sistema di progetto. La versione di anteprima 3 degli strumenti della riga di comando di .NET Core è la prima a non contenere alcun supporto per project.json. Questo significa che non può essere usata per creare, eseguire o pubblicare applicazioni e librerie basate su project.json. Per usare questa versione degli strumenti, è necessario eseguire la migrazione dei progetti esistenti o avviarne di nuovi. 

Come parte di questo passaggio, il motore di compilazione personalizzato sviluppato per i progetti project.json è stato sostituito da un motore di compilazione maturo e dotato di funzionalità complete denominato [MSBuild](https://github.com/Microsoft/msbuild). MSBuild è un motore noto nella community .NET: è stato infatti una tecnologia fondamentale fin dalla prima versione della piattaforma. Naturalmente, poiché è necessario per la compilazione di applicazioni .NET Core, MSBuild è stato portato in .NET Core e può essere usato su qualsiasi piattaforma in cui viene eseguito .NET Core. Una delle promesse principali di .NET Core è la realizzazione di uno stack di sviluppo multipiattaforma, e Microsoft ha mantenuto tale promessa.

> **Nota:** se non si ha familiarità con MSBuild e si vogliono acquisire maggiori informazioni al riguardo, è possibile iniziare leggendo la [documentazione esistente](https://msdn.microsoft.com/en-us/library/dd637714.aspx). 

# <a name="the-tooling-layers"></a>Livelli degli strumenti
Con l'abbandono del sistema di progetto esistente e dei commutatori del motore di compilazione, la domanda da porsi è la seguente: uno qualsiasi di questi cambiamenti modificherà i livelli complessivi dell'ecosistema degli strumenti .NET Core? Esistono nuovi elementi e componenti?

Nella figura seguente viene fornito un breve riepilogo dei livelli dell'anteprima 2:

![Architettura di alto livello degli strumenti dell'anteprima 2](media/p2-arch.png)

L'organizzazione su più livelli degli strumenti è piuttosto semplice. Al livello più basso, come base, si trovano gli strumenti della riga di comando di .NET Core. Tutti gli altri strumenti di livello più alto, ad esempio Visual Studio o VS Code, dipendono e si basano sull'interfaccia della riga di comando per la compilazione dei progetti, il ripristino delle dipendenze e così via. Ad esempio, questo significa che, se Visual Studio voleva eseguire un'operazione di ripristino, doveva chiamare il comando `dotnet restore` nell'interfaccia della riga di comando. 

Con il passaggio al nuovo sistema di progetto, il diagramma precedente risulta modificato nel modo illustrato di seguito: 

![Architettura di alto livello degli strumenti dell'anteprima 3](media/p3-arch.png)

La differenza principale è che l'interfaccia della riga di comando non è più il livello di base. Tale ruolo viene ora svolto dal "componente SDK condiviso". Questo componente SDK condiviso è un set di destinazioni e attività associate responsabili della compilazione e della pubblicazione del codice, della creazione di pacchetti nuget e così via. L'SDK stesso è open source ed è disponibile in GitHub nel [repository SDK](https://github.com/dotnet/sdk). 

> **Nota:** "destinazione" è un termine di MSBuild indicante un'operazione denominata che MSBuild può richiamare. La destinazione è in genere associata a una o più attività che eseguono la logica dell'operazione. MSBuild supporta diverse destinazioni predefinite, ad esempio `Copy` o `Execute`. Consente inoltre agli utenti di scrivere le proprie attività usando codice gestito e definire destinazioni per eseguire tali attività. Altre informazioni su MSBuild sono disponibili in [MSDN](https://msdn.microsoft.com/en-us/library/ms171466.aspx). 

Tutti i set di strumenti, inclusa l'interfaccia della riga di comando, utilizzano ora il componente SDK condiviso e le relative destinazioni. Ad esempio, la prossima versione di Visual Studio non chiamerà il comando `dotnet restore` per ripristinare le dipendenze per i progetti .NET Core, ma userà direttamente la destinazione "Restore". Poiché si tratta di destinazioni MSBuild, è anche possibile usare direttamente MSBuild per eseguirle mediante il comando [dotnet-msbuild](dotnet-msbuild.md). 

## <a name="preview-3-cli-commands"></a>Comandi dell'anteprima 3 della riga di comando
Con l'introduzione del componente SDK condiviso, la maggior parte dei comandi dell'interfaccia della riga di comando esistenti sono stati reimplementati come attività e destinazioni MSBuild. Cosa significa questo per i comandi dell'interfaccia della riga di comando e per l'utilizzo del set di strumenti? 

La modalità di utilizzo dell'interfaccia della riga di comando non viene modificata. Nell'interfaccia della riga di comando sono infatti ancora disponibili i comandi base presenti nell'anteprima 2:

* `new`
* `restore`
* `run` 
* `build`
* `publish`
* `test`
* `pack` 

Questi comandi consentono di eseguire le stesse operazioni di prima, ad esempio creare un progetto, compilarlo, pubblicarlo, crearne un pacchetto e così via. La maggior parte delle opzioni non è stata modificata. Per acquisire familiarità con le modifiche, è possibile consultare le schermate della Guida dei comandi (usando `dotent <command> --help`) o la documentazione dell'anteprima 3. 

Dal punto di vista dell'esecuzione, i comandi dell'interfaccia della riga di comando accetteranno i parametri e invieranno una chiamata diretta a MSBuild. Quest'ultimo imposterà le proprietà necessarie ed eseguirà la destinazione desiderata. Per comprendere meglio quanto esposto sopra, prendere in considerazione il comando seguente: 

    `dotnet publish -o pub -c Release`. 
    
Questo comando pubblica un'applicazione in una cartella `pub` usando la configurazione "Release". A livello interno, il comando viene tradotto nella chiamata a MSBuild seguente: 

    `dotnet msbuild /t:Publish /p:OutputPath=pub /p:Configuration`

La principale eccezione a questa regola sono i comandi `new` e `run`, che non sono stati implementati come destinazioni MSBuild. 

# <a name="conclusion"></a>Conclusione 
Questo documento ha illustrato le modifiche ad alto livello apportate all'architettura e al funzionamento complessivi degli strumenti dell'interfaccia della riga di comando nell'anteprima 3. È stato introdotto il concetto di componente SDK condiviso ed è stato descritto, da un punto di vista tecnico, il funzionamento dei comandi dell'interfaccia della riga di comando nell'anteprima 3. 




<!--HONumber=Nov16_HO3-->


