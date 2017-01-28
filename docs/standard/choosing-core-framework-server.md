---
title: Scelta di .NET Core o .NET Framework per le app server
description: Guida alla scelta della tipologia di .NET da prendere in considerazione per creare un&quot;app server in .NET.
keywords: .NET, .NET Core, .NET Framework
author: cartermp
manager: wpickett
ms.author: phcart
ms.date: 11/16/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 155553e4-89a2-418d-be88-4e75f6c3cc69
translationtype: Human Translation
ms.sourcegitcommit: d6ce9e3dd3c1189f35d147d140bb45095b3d77a5
ms.openlocfilehash: a0563f7437711ddbee309803e97ab653aa160337

---

# <a name="choosing-between-net-core-and-net-framework-for-server-apps"></a>Scelta di .NET Core o .NET Framework per le app server

Per la creazione di applicazioni lato server con .NET sono supportate due opzioni di runtime: .NET Framework e .NET Core. Entrambe condividono gran parte dei componenti della piattaforma .NET e possono condividere codice. Tuttavia, esistono differenze fondamentali tra le due opzioni e la scelta dipende dall'obiettivo che si vuole conseguire.  Questo articolo fornisce materiale sussidiario per identificare i casi in cui è opportuno usare ciascuna delle due opzioni.

È consigliabile usare .NET Core per l'applicazione server nei casi seguenti:

* Si hanno esigenze multipiattaforma.
* Si scelgono microservizi.
* Si usano contenitori Docker.
* Si hanno esigenze di elevate prestazioni e scalabilità.
* È necessaria l'installazione side-by-side delle versioni di .NET in base all'applicazione.

È consigliabile usare .NET Framework per l'applicazione server nei casi seguenti:

* L'applicazione attualmente usa .NET Framework (si consiglia di optare per l'estensione anziché per la migrazione)
* È necessario usare pacchetti NuGet o librerie .NET di terze parti non disponibili per .NET Core.
* È necessario usare tecnologie .NET non disponibili per .NET Core.
* È necessario usare una piattaforma che non supporta .NET Core.

## <a name="when-to-choose-net-core"></a>Quando scegliere .NET Core

Di seguito vengono descritti in modo più dettagliato i motivi indicati in precedenza per la scelta di .NET Core.

### <a name="cross-platform-needs"></a>Esigenze multipiattaforma

Chiaramente, se l'obiettivo è disporre di un'applicazione (Web/servizio) eseguibile su più piattaforme (Windows, Linux e macOS), la scelta ottimale è usare .NET Core.

.NET Core supporta anche i sistemi operativi indicati in precedenza come workstation di sviluppo. Visual Studio fornisce un ambiente di sviluppo integrato (IDE) per Windows.  È anche possibile usare Visual Studio Code in macOS, Linux e Windows che supportano completamente .NET Core, incluse le funzionalità IntelliSense e di debug. .NET Core può essere scelto anche con quasi tutti gli editor di terze parti come Sublime, Emacs e VI e la funzionalità IntelliSense è accessibile mediante il progetto open source [Omnisharp](http://www.omnisharp.net/). È anche possibile evitare di usare gli editor di codice ricorrendo direttamente agli strumenti da riga di comando di .NET Core, disponibili per tutte le piattaforme supportate.

### <a name="microservices-architecture"></a>Architettura di microservizi

.NET Core è la scelta ottimale se si intende adottare un sistema orientato ai microservizi, costituito da più microservizi con o senza stato, indipendenti e scalabili in modo dinamico. .NET Core è leggero e la sua interfaccia API può essere ridotta in base all'ambito del microservizio. Un'architettura di microservizi permette anche di unire le tecnologie di più servizi, consentendo la graduale adozione di .NET Core per nuovi microservizi che si attivano in combinazione con altri o per servizi sviluppati con .NET Framework, Java, Ruby o altre tecnologie monolitiche.

Le piattaforme di infrastruttura che è possibile usare sono numerose. Per i sistemi di microservizi complessi e di grandi dimensioni è possibile usare [Azure Service Fabric](https://azure.microsoft.com/en-us/services/service-fabric/). Per i microservizi senza stato è possibile usare anche altri prodotti come [Servizio app di Azure](https://azure.microsoft.com/en-us/services/app-service/). Le alternative basate su Docker sono inoltre adatte a qualsiasi tipo di approccio ai microservizi, come descritto di seguito. Grazie al supporto di .NET Core, tutte queste piattaforme rappresentano soluzioni ideali per l'hosting dei microservizi.

### <a name="containers"></a>Contenitori

I contenitori vengono comunemente usati in combinazione con un'architettura di microservizi, sebbene possano essere impiegati anche per creare contenitori di servizi o app Web basati su qualsiasi modello architettonico. Sarà possibile usare i contenitori di .NET Framework per Windows, ma le caratteristiche di modularità e leggerezza rendono .NET Core la scelta ideale per i contenitori.  Quando si crea e si distribuisce un contenitore, la sua immagine risulta notevolmente più piccola con .NET Core rispetto a .NET Framework.  Trattandosi di un'opzione multipiattaforma, è ad esempio possibile distribuire le app server in contenitori Docker di Linux.

È quindi possibile ospitare i contenitori Docker nell'infrastruttura Linux o Windows in uso oppure usare un servizio cloud, ad esempio il [servizio contenitore di Azure](https://azure.microsoft.com/en-us/services/container-service/), per gestire, orchestrare e ridimensionare l'applicazione basata su contenitore nel cloud.

### <a name="a-need-for-high-performance-and-scalable-systems"></a>Esigenze di elevate prestazioni e scalabilità

Se il sistema richiede i massimi livelli di prestazioni e scalabilità, le opzioni ottimali sono rappresentate da .NET Core e ASP.NET Core. Offrendo prestazioni 10 volte superiori a quelle di ASP.NET, ASP.NET Core è in testa alla classifica delle più diffuse tecnologie di settore per microservizi, come servlet Java, Go e node.js.

Questo aspetto riguarda in particolare le architetture con centinaia di microservizi in esecuzione. Con ASP.NET Core è possibile eseguire il sistema con un numero di server/macchine virtuali sensibilmente inferiore, determinando in ultima analisi una riduzione dei costi di infrastruttura e hosting.

### <a name="a-need-for-side-by-side-of-net-versions-per-application-level"></a>Necessità di installazione side-by-side delle versioni di .NET in base al livello di applicazione

Per poter installare applicazioni con dipendenze su versioni diverse di framework in .NET, è necessario usare .NET Core per garantire una perfetta installazione side-by-side. Grazie alla facilità di installazione side-by-side di versioni diverse di .NET Core nella stessa macchina, è possibile ospitare più servizi nello stesso server, ciascuno con la rispettiva versione di .NET Core, eliminando i rischi e risparmiando sui costi degli aggiornamenti di applicazioni e delle operazioni IT.

## <a name="when-to-choose-net-framework"></a>Quando scegliere .NET Framework

Sebbene .NET Core offra vantaggi significativi per le nuove applicazioni e i nuovi modelli di applicazione, .NET Framework continua a rappresentare la scelta naturale per molti scenari esistenti e pertanto non verrà sostituito da .NET Core per tutte le applicazioni server.

### <a name="current-net-framework-applications"></a>Applicazioni .NET Framework correnti

Nella maggior parte dei casi, non è necessario eseguire la migrazione delle applicazioni esistenti a .NET Core. Al contrario, un approccio consigliato è quello di usare .NET Core per estendere un'applicazione esistente, ad esempio con la scrittura di un nuovo servizio Web in ASP.NET Core.

### <a name="a-need-to-use-third-party-net-libraries-or-nuget-packages-not-available-for-net-core"></a>Necessità di usare pacchetti NuGet o librerie .NET di terze parti non disponibili per .NET Core

Per le librerie è in corso l'adozione rapida di .NET Standard, che consente la condivisione di codice tra tutte le versioni di .NET incluso .NET Core. Con .NET Standard 2.0 sarà ancora più semplice perché l'interfaccia API di .NET Core sarà molto più grande e le applicazioni .NET Core potranno usare direttamente le librerie di .NET Framework esistenti. Questo passaggio, tuttavia, non avverrà subito, pertanto è consigliabile controllare le librerie specifiche richieste dall'applicazione prima di prendere una qualsiasi decisione.

### <a name="a-need-to-use-net-technologies-not-available-for-net-core"></a>Necessità di usare tecnologie .NET non disponibili per .NET Core

Esistono tecnologie di .NET Framework non disponibili in .NET Core. Alcune saranno disponibili in versioni future di .NET Core, mentre altre non si applicano ai nuovi modelli di applicazione basati su .NET Core ed è possibile che non vengano mai rese disponibili. Di seguito sono elencate le tecnologie più comuni non disponibili in .NET Core 1.0:

* Applicazioni Web Form ASP.NET: Web Form ASP.NET è disponibile solo in .NET Framework, pertanto non è possibile usare ASP.NET Core o .NET Core per questo scenario. Attualmente non è previsto il trasferimento di Web Form ASP.NET in .NET Core.

* Applicazioni Pagine Web ASP.NET: Pagine Web ASP.NET non è incluso in ASP.NET Core 1.0, anche se ne è prevista l'inclusione in una versione futura come indicato nella [roadmap di .NET Core](https://github.com/aspnet/Home/wiki/Roadmap).

* Implementazione di server/client ASP.NET SignalR: al momento del rilascio di .NET Core 1.0 (giugno 2016), ASP.NET SignalR non è disponibile in ASP.NET Core (né per client né per server), anche se ne è prevista l'inclusione in una versione futura come indicato nella [roadmap di .NET Core](https://github.com/aspnet/Home/wiki/Roadmap). Lo stato di anteprima è disponibile nei repository di GitHub relativi al [lato server](https://github.com/aspnet/SignalR-Server) e alla [libreria client](https://github.com/aspnet/SignalR-Client-Net).

* Implementazione di servizi WCF: anche se, da giugno 2016, è presente una [libreria WCF client](https://github.com/dotnet/wcf) per l'utilizzo di servizi WCF da .NET Core, l'implementazione di server WCF è disponibile solo in .NET Framework. Questo scenario non è attualmente previsto per .NET Core, ma verrà preso in considerazione per il futuro.

* Servizi correlati al flusso di lavoro: Windows Workflow Foundation (WF), Servizi flusso di lavoro (WCF e WF in un unico servizio) e WCF Data Services (in precedenza "ADO.NET Data Services") sono disponibili solo in .NET Framework e non è previsto alcun trasferimento a .NET Core.

* Supporto per i linguaggi: Visual Basic e F# non dispongono attualmente di strumenti per il supporto di .NET Core, ma entrambi saranno supportati in Visual Studio 2017 e versioni successive di Visual Studio.

In aggiunta a quanto indicato nella roadmap ufficiale, sono presenti altri framework da trasferire in .NET Core. Per un elenco completo, consultare i problemi di CoreFX contrassegnati come [port-to-core](https://github.com/dotnet/corefx/issues?q=is%3Aopen+is%3Aissue+label%3Aport-to-core). Si noti che questo elenco non obbliga Microsoft a trasferire i componenti indicati in .NET Core, ma rappresenta solo il desiderio della community di procedere in tal senso. Se comunque si è interessati a uno dei componenti elencati in precedenza, è consigliabile partecipare alle discussioni su GitHub per far valere la propria opinione. Inoltre, se si ritiene di dover aggiungere alcune osservazioni, è possibile [inserire un nuovo problema nel repository CoreFX](https://github.com/dotnet/corefx/issues/new).

### <a name="a-need-to-use-a-platform-that-doesnt-support-net-core"></a>Necessità di usare una piattaforma che non supporta .NET Core

Alcune piattaforme Microsoft o di terze parti non supportano .NET Core. Alcuni servizi di Azure come i servizi Reliable con stato di Service Fabric e Reliable Actors di Service Fabric, ad esempio, richiedono .NET Framework. Altri servizi forniscono un SDK non ancora disponibile per l'utilizzo in .NET Core. Questa situazione è transitoria poiché tutti i servizi di Azure usano .NET Core. Nel frattempo, è possibile usare l'API REST equivalente anziché l'SDK client.

## <a name="further-resources"></a>Altre risorse

* [Guida a .NET Core](../core/index.md)
* [Porting from .NET Framework to .NET Core](../core/porting/index.md) (Portabilità da .NET Framework a .NET Core)
* [.NET Framework on Docker Guide](../framework/index.md) (Guida a .NET Framework su Docker)
* [.NET Components Overview](components.md) (Panoramica dei componenti .NET)


<!--HONumber=Nov16_HO3-->


