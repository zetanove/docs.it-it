---
title: Organizzare il progetto per il supporto di .NET Framework e .NET Core
description: Indicazioni per i responsabili di progetti che desiderano compilare la propria soluzione affiancando .NET Framework e .NET Core.
keywords: ".NET, .NET Core, .NET Framework, layout di progetto, più framework"
author: conniey
ms.author: mairaw
ms.date: 04/06/2017
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: 3af62252-1dfa-4336-8d2f-5cfdb57d7724
ms.translationtype: Human Translation
ms.sourcegitcommit: 9fd4e033a5f33d4f560b12e23950abd62c7825c5
ms.openlocfilehash: d83378b094fbae16c788c04269b833a4ecae3608
ms.contentlocale: it-it
ms.lasthandoff: 04/07/2017

---

# <a name="organizing-your-project-to-support-net-framework-and-net-core"></a>Organizzare il progetto per il supporto di .NET Framework e .NET Core

Questo articolo offre indicazioni per i responsabili di progetto che intendono compilare la propria soluzione affiancando .NET Framework e .NET Core. Offre diverse opzioni per organizzare i progetti in modo da consentire agli sviluppatori di raggiungere tale obiettivo. L'elenco seguente visualizza alcuni scenari tipici da considerare per la scelta della modalità di configurazione del layout di progetto da usare con .NET Core. È possibile che l'elenco non includa tutti gli aspetti desiderati. Definire le priorità in base alle esigenze.

* [**Combinare progetti esistenti e progetti .NET Core in singoli progetti**][option-csproj]

  *Vantaggi:*
  * Semplificazione del processo di compilazione mediante la compilazione di un singolo progetto piuttosto che di progetti multipli, ciascuno destinato a una versione o a una piattaforma differente di .NET Framework.
  * Semplificazione della gestione di file di origine per progetti con più destinazioni perché è necessario gestire un unico file di progetto. Quando si aggiungono o rimuovono i file di origine, le alternative richiedono una sincronizzazione manuale di questi file con altri progetti.
  * Generazione semplificata di un pacchetto NuGet per l'utilizzo.
  * Scrittura di codice per una versione specifica di .NET Framework nelle librerie tramite l'uso di direttive del compilatore.

  *Scenari non supportati:*
  * Gli sviluppatori devono usare Visual Studio 2017 per aprire i progetti esistenti. Per supportare le versioni precedenti di Visual Studio, è opportuno [mantenere i file di progetto in cartelle diverse](#support-vs).

* <a name="support-vs"></a>[**Mantenere separati i progetti esistenti e i nuovi progetti .NET Core**][option-csproj-folder]

  *Vantaggi:*
  * Supporto per lo sviluppo di progetti esistenti, senza necessità di aggiornamento per sviluppatori/collaboratori che non dispongono di Visual Studio 2017.
  * Riduzione della possibilità di creazione di nuovi bug nei progetti esistenti in quanto non è necessaria alcuna varianza del codice nei progetti.

## <a name="example"></a>Esempio

Si consideri il repository seguente:

![Progetto esistente][example-initial-project]

[**Codice sorgente**][example-initial-project-code]

Di seguito vengono illustrati vari metodi per l'aggiunta del supporto .NET Core per il repository, a seconda dei vincoli e della complessità dei progetti esistenti.

## <a name="replace-existing-projects-with-a-multi-targeted-net-core-project"></a>Sostituire i progetti esistenti con un progetto .NET Core con più destinazioni

Riorganizzare il repository in modo che venga rimosso qualsiasi file *\*csproj* esistente e venga creato un singolo file *\*csproj* destinato a più framework. Questa è un'ottima opzione perché consente di compilare un singolo progetto per diversi framework. Include anche la possibilità di gestire diverse opzioni di compilazione e dipendenze a seconda del framework di destinazione.

![Creare un file csproj con più framework come destinazione][example-csproj]

[**Codice sorgente**][example-csproj-code]

Modifiche da notare:
* Sostituzione di *packages.config* e *\*csproj* con un nuovo [.NET Core *\*.csproj*][example-csproj-netcore]. I pacchetti NuGet vengono specificati con `<PackageReference> ItemGroup`.

## <a name="keep-existing-projects-and-create-a-net-core-project"></a>Mantenere i progetti esistenti e creare un progetto .NET Core

Se sono presenti progetti destinati a framework precedenti, è consigliabile lasciare invariati i progetti e usare un progetto .NET Core in modo che sia destinato a framework futuri.

![Progetto .NET Core con un progetto esistente in un'altra cartella][example-csproj-different-folder]

[**Codice sorgente**][example-csproj-different-code]

Modifiche da notare:
* I progetti esistenti e .NET Core vengono mantenuti in cartelle separate.
    * La gestione dei progetti in cartelle separate evita l'obbligo di avere Visual Studio 2017. È possibile creare una soluzione separata che consente di aprire solo i progetti precedenti.

## <a name="see-also"></a>Vedere anche

Per altre indicazioni relative alla migrazione a .NET Core, vedere la [documentazione relativa alla portabilità di .NET Core][porting-doc].

[porting-doc]: index.md
[example-initial-project]: media/project-structure/project.png "Progetto esistente"
[example-initial-project-code]: https://github.com/dotnet/docs/tree/master/samples/framework/libraries/migrate-library/

[example-csproj]: media/project-structure/project.csproj.png "Creare un file csproj con più framework come destinazione"
[example-csproj-code]: https://github.com/dotnet/docs/tree/master/samples/framework/libraries/migrate-library-csproj/
[example-csproj-netcore]: https://github.com/dotnet/docs/tree/master/samples/framework/libraries/migrate-library-csproj/src/Car/Car.csproj

[example-csproj-different-folder]: media/project-structure/project.csproj.different.png "Progetto .NET Core con una libreria di classi portabile esistente in un'altra cartella"
[example-csproj-different-code]: https://github.com/dotnet/docs/tree/master/samples/framework/libraries/migrate-library-csproj-keep-existing/

[option-csproj]: #replace-existing-projects-with-a-multi-targeted-net-core-project
[option-csproj-folder]: #keep-existing-projects-and-create-a-net-core-project
