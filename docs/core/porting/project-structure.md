---
title: Organizzazione del progetto per il supporto di .NET Framework e .NET Core
description: Organizzazione del progetto per il supporto di .NET Framework e .NET Core
keywords: .NET, .NET Core
author: conniey
manager: wpickett
ms.date: 07/18/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 3af62252-1dfa-4336-8d2f-5cfdb57d7724
translationtype: Human Translation
ms.sourcegitcommit: 15c55a87beb64f265a164db918c7721c7690fadf
ms.openlocfilehash: ca63b25bb5f5e98167aaa8b74a7204fcd77b3523

---

# <a name="organizing-your-project-to-support-net-framework-and-net-core"></a>Organizzazione del progetto per il supporto di .NET Framework e .NET Core

Questo articolo fornisce indicazioni ai proprietari di progetto che vogliono compilare la propria soluzione affiancando .NET Framework e .NET Core.  Offre diverse opzioni per organizzare i progetti in modo da consentire agli sviluppatori di raggiungere tale obiettivo.  Ecco alcuni scenari tipici da considerare quando si decide quale modalità di configurazione del layout di progetto usare con .NET Core.  È possibile che questi scenari non coprano tutti gli aspetti desiderati, è quindi opportuno definire delle priorità in base alle proprie esigenze.

* [**Combinare progetti esistenti e progetti .NET Core in singoli progetti**][option-xproj]
  
  *Vantaggi:*
  * Semplificazione del processo di compilazione mediante la compilazione di un singolo progetto piuttosto che di progetti multipli, ciascuno destinato a una versione o a una piattaforma differente di .NET Framework.
  * Semplificazione della gestione di file di origine per progetti con più destinazioni perché è necessario gestire un singolo file di progetto.  Quando si aggiungono o rimuovono i file di origine, le alternative richiedono una sincronizzazione manuale di questi file con altri progetti.
  * Generazione semplificata di un pacchetto NuGet per l'utilizzo.
  * Scrittura di codice per una versione specifica di .NET Framework nelle librerie tramite l'uso di direttive del compilatore.
  
  *Scenari non supportati:*
  * Non consente agli sviluppatori senza Visual Studio 2015 di aprire progetti esistenti. Per supportare le versioni precedenti di Visual Studio, è opportuno [mantenere i file di progetto in cartelle diverse](#support-vs).
  * Non consente di condividere la libreria .NET Core tra diversi tipi di progetto nello stesso file di soluzione. A tale scopo, è opportuno [creare una libreria di classi portabile](#support-pcl).
  * Non consente la compilazione del progetto o le modifiche dei caricamenti supportate da attività e destinazioni di MSBuild. A tale scopo, è opportuno [creare una libreria di classi portabile](#support-pcl).

* [**Mantenere separati i progetti esistenti e i nuovi progetti .NET Core**][option-xproj-folder]
  
  *Vantaggi:*
  * Supporto per lo sviluppo di progetti esistenti senza dover eseguire l'aggiornamento per sviluppatori/collaboratori che non dispongono di Visual Studio 2015.
  * Riduzione della possibilità di creazione di nuovi bug nei progetti esistenti in quanto non è necessaria alcuna varianza del codice nei progetti.

* [**Mantenere i progetti esistenti e creare librerie di classi portabili destinate a .NET Core**][option-pcl]

  *Vantaggi:*
  * Riferimento alle librerie .NET Core nei progetti desktop e/o Web destinati a .NET Framework completo nella stessa soluzione.
  * Supporto delle modifiche nella build del progetto o nel processo di caricamento. Queste modifiche possono riguardare l'inclusione delle attività e delle destinazioni di MSBuild nel file `*.csproj`.

  *Scenari non supportati:*
  * Non consente di scrivere codice per una versione specifica di .NET Framework, perché i [simboli predefiniti del preprocessore][how-to-multitarget] non sono supportati.

## <a name="example"></a>Esempio

Si consideri il repository seguente:

![Progetto esistente][example-initial-project]

[**Codice sorgente**][example-initial-project-code]

Sono disponibili diversi modi per aggiungere il supporto per .NET Core per il repository in base ai vincoli e alla complessità dei progetti esistenti descritti di seguito.

## <a name="replace-existing-projects-with-a-multitargeted-net-core-project-xproj"></a>Sostituire i progetti esistenti con un progetto .NET Core con più destinazioni (xproj)

Il repository può essere riorganizzato in modo che qualsiasi file `*.csproj` esistente venga rimosso e un singolo file `*.xproj` venga creato per essere destinato a più framework.  Questa è un'ottima opzione perché consente di compilare un singolo progetto per diversi framework.  Include inoltre la possibilità di gestire diverse opzioni di compilazione, dipendenze e così via per ciascun framework di destinazione.

![Creare un progetto xproj con più framework come destinazione][example-xproj]

[**Codice sorgente**][example-xproj-code]

Modifiche da notare:
* Aggiunta di `global.json`
* Sostituzione di `packages.config` e `*.csproj` con `project.json` e `*.xproj`
* Modifiche in [project.json di Car][example-xproj-projectjson] e il relativo [progetto di test][example-xproj-projectjson-test] per supportare la compilazione dell'istanza di .NET Framework esistente e di altre

## <a name="create-a-portable-class-library-pcl-to-target-net-core"></a>Creare una libreria di classi portabile come destinazione per .NET Core

Se i progetti esistenti contengono operazioni di compilazione o proprietà complesse nel file `*.csproj`, può risultare più facile creare una libreria di classi portabile.

![][example-pcl]

[**Codice sorgente**][example-pcl-code]

Modifiche da notare:
*  Ridenominazione di `project.json` in `{project-name}.project.json`
    * In questo modo, si evita un potenziale conflitto in Visual Studio quando si tenta di ripristinare i pacchetti per le librerie nella stessa directory. Per altre informazioni, vedere tra le [domande frequenti su NuGet](https://docs.nuget.org/consume/nuget-faq#working-with-packages) quella relativa alla _disponibilità di più progetti nella stessa cartella e alla possibilità di usare file packages.config o project.json separati per ogni progetto_.
    *  **Alternativa**: creare la libreria di classi portabile in un'altra cartella e fare riferimento al codice sorgente originale per evitare questo problema.  L'inserimento della libreria di classi portabile in un'altra cartella presenta un ulteriore vantaggio per gli utenti che non hanno Visual Studio 2015 in quanto possono comunque utilizzare i progetti precedenti senza caricare la nuova soluzione.
*  Per impostare come destinazione .NET Standard dopo aver creato la libreria di classi portabile, in Visual Studio aprire **Proprietà del progetto**. Nella sezione **Destinazioni** fare clic sul collegamento **"Imposta come destinazione la piattaforma standard .NET"**.  Questa modifica può essere invertita ripetendo la stessa procedura.

## <a name="keep-existing-projects-and-create-a-net-core-project"></a>Mantenere i progetti esistenti e creare un progetto -NET Core

Se sono presenti progetti destinati a framework precedenti, è consigliabile lasciare invariati i progetti e usare un progetto .NET Core in modo che sia destinato a framework futuri.

![Progetto .NET Core con una libreria di classi portabile esistente in un'altra cartella][example-xproj-different-folder]

[**Codice sorgente**][example-xproj-different-code]

Modifiche da notare:
* I progetti esistenti e .NET Core vengono mantenuti in cartelle separate.
    * Questo evita il problema di ripristino del pacchetto che è stato indicato in precedenza a causa di più file project.json/package.config nella stessa cartella.
    * La suddivisione dei progetti in cartelle separate evita di dover disporre di Visual Studio 2015 (a causa di project.json).  È possibile creare una soluzione separata che consente di aprire solo i progetti precedenti.

## <a name="see-also"></a>Vedere anche

Per altre indicazioni sullo spostamento a project.json e xproj, vedere la [documentazione di .NET Core relativa alla portabilità][porting-doc].

[porting-doc]: index.md
[example-initial-project]: media/project-structure/project.png "Progetto esistente"
[example-initial-project-code]: https://github.com/dotnet/docs/tree/master/samples/framework/libraries/migrate-library/

[example-xproj]: media/project-structure/project.xproj.png "Creare un progetto xproj con più framework come destinazione"
[example-xproj-code]: https://github.com/dotnet/docs/tree/master/samples/framework/libraries/migrate-library-xproj/
[example-xproj-projectjson]: https://github.com/dotnet/docs/tree/master/samples/framework/libraries/migrate-library-xproj/src/Car/project.json
[example-xproj-projectjson-test]: https://github.com/dotnet/docs/tree/master/samples/framework/libraries/migrate-library-xproj/tests/Car.Tests/project.json

[example-xproj-different-folder]: media/project-structure/project.xproj.different.png "Progetto .NET Core con una libreria di classi portabile esistente in un'altra cartella"
[example-xproj-different-code]: https://github.com/dotnet/docs/tree/master/samples/framework/libraries/migrate-library-xproj-keep-csproj/

[example-pcl]: media/project-structure/project.pcl.png "Libreria di classi portabile con .NET Core come destinazione"
[example-pcl-code]: https://github.com/dotnet/docs/tree/master/samples/framework/libraries/migrate-library-pcl

[option-xproj]: #replace-existing-projects-with-a-multi-targeted-net-core-project-xproj
[option-pcl]: #create-a-portable-class-library-pcl-to-target-net-core
[option-xproj-folder]: #keep-existing-projects-and-create-a-net-core-project

[how-to-multitarget]: ../tutorials/libraries.md#how-to-multitarget



<!--HONumber=Nov16_HO1-->


