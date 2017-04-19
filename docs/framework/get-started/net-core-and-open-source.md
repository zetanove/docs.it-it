---
title: Componenti di base e open-source di .NET | Microsoft Docs
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: e6bd4655-ce37-4003-8462-468a6fe2c40f
caps.latest.revision: 8
author: mairaw
ms.author: mairaw
manager: wpickett
translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 54bade1b6e310db37537102a1625a76e11e136a7
ms.lasthandoff: 04/18/2017

---
# <a name="net-core-and-open-source"></a>Componenti di base e open-source di .NET
Questo argomento fornisce una breve descrizione di .NET Core e illustra come trovare altre informazioni. Per trovare l'elenco completo degli argomenti relativi a .NET Core, visitare il [sito della documentazione di .NET Core](https://docs.microsoft.com/en-us/dotnet/articles/core/index).  
  
<a name="BKMK_WhatisNETCore"></a>   
## <a name="what-is-net-core"></a>Informazioni su .NET Core  
 .NET Core è un'implementazione generica, modulare, multi-piattaforma e open source di .NET Platform. Contiene molte delle stesse API di .NET Framework (ma .NET Core è un set più piccolo) e include componenti di runtime, del framework, del compilatore e degli strumenti in grado di supportare un'ampia gamma di sistemi operativi e chip di destinazione. L'implementazione di .NET Core è basata principalmente sui carichi di lavoro di ASP.NET Core, ma anche sulla necessità e la volontà di avere un runtime più moderno. Può essere usata in scenari di dispositivi, cloud e IoT/incorporati.  
  
 Per iniziare a usare .NET Core, visitare la [home page di .NET Core](https://www.microsoft.com/net/core).  
  
 Di seguito sono riportate le caratteristiche principali di .NET Core:  
  
-   **Multi-piattaforma:** NET Core offre gli strumenti essenziali per implementare le funzioni dell'app necessarie e riusare il codice indipendentemente dalla piattaforma di destinazione. Supporta attualmente tre sistemi operativi principali: Windows, Linux e macOS. È possibile scrivere app e librerie in modo che vengano eseguite senza modifiche nei sistemi operativi supportati. Per visualizzare l'elenco dei sistemi operativi supportati, visitare [.NET Core roadmap](https://github.com/dotnet/core/blob/master/roadmap.md) (Roadmap di .NET Core).  
  
-   **Open source:** .NET Core è uno dei molti progetti sotto il controllo di [.NET Foundation](http://www.dotnetfoundation.org/) ed è disponibile in [GitHub](https://github.com/).  La disponibilità di .NET Core come progetto open source favorisce un processo di sviluppo più trasparente e promuove una community più attiva e impegnata.  
  
-   **Distribuzione flessibile:** esistono principalmente due modi per distribuire l'app, ovvero la distribuzione dipendente dal framework e la distribuzione autonoma. Con la distribuzione dipendente dal framework vengono installate solo l'app e le dipendenze di terze parti e l'app richiede che sia presente una versione a livello di sistema di .NET Core.  Con la distribuzione completa, insieme all'app e alle dipendenze di terze parti viene distribuita anche la versione di .NET Core usata per compilare l'applicazione. Questa distribuzione può essere eseguita side-by-side con altre versioni.    Per altre informazioni, vedere [Distribuzione di applicazioni .NET Core](https://docs.microsoft.com/en-us/dotnet/articles/core/deploying/index).  
  
-   **Modulare:** .NET Core è modulare perché viene rilasciato tramite NuGet in pacchetti di assembly di dimensioni ridotte. Invece di un unico assembly grande contenente la maggior parte delle funzionalità di base, .NET Core è disponibile sotto forma di pacchetti più piccoli incentrati sulle funzionalità. Questa struttura consente un modello di sviluppo più agile e offre agli utenti l'opportunità di ottimizzare le app includendo solo i pacchetti NuGet effettivamente necessari. Una riduzione della superficie occupata dall'app offre anche diversi vantaggi, tra cui una maggiore sicurezza, una riduzione delle esigenze di assistenza, un miglioramento delle prestazioni e una diminuzione dei costi in un modello di pagamento basato sul consumo effettivo.  
  
## <a name="the-net-core-platform"></a>La piattaforma .NET Core  
 La piattaforma .NET Core è costituita da vari componenti, tra cui i compilatori gestiti, il runtime, le librerie di classi base e numerosi modelli applicativi come ASP.NET Core. Per informazioni sui vari componenti disponibili è possibile visitare i seguenti repository [GitHub](https://github.com/):  
  
-   [.NET Core](https://github.com/dotnet/core)  
  
-   [CoreFX - .NET Core foundational libraries](https://github.com/dotnet/corefx) (CoreFX - Librerie di base di .NET Core)  
  
-   [CoreCLR - .NET Core runtime](https://github.com/dotnet/coreclr) (CoreCLR - Runtime di .NET Core)  
  
-   [CLI - .NET Core command-line tools](https://github.com/dotnet/cli) (CLI - Strumenti della riga di comando di .NET Core)  
  
-   [Roslyn - .NET Compiler Platform](https://github.com/dotnet/roslyn) (Roslyn - Piattaforma del compilatore .NET)  
  
-   [ASP.NET Core](https://github.com/aspnet/home)  
  
## <a name="see-also"></a>Vedere anche  
 [Home page di .NET core](https://www.microsoft.com/net/core)   
 [Sito della documentazione di .NET Core](https://docs.microsoft.com/en-us/dotnet/articles/core/index)   
 [Documentazione di ASP.NET Core](https://docs.asp.net/)
