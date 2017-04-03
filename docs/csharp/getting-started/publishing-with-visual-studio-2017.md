---
title: Pubblicazione dell&quot;applicazione Hello World con Visual Studio 2017
description: Pubblicazione dell&quot;applicazione Hello World con Visual Studio 2017
keywords: .NET, .NET Core, applicazione console .NET Core, pubblicazione (.NET Core), distribuzione (.NET Core)
author: stevehoag
ms.author: shoag
ms.date: 10/24/2016
ms.topic: article
ms.prod: .net-core
ms.technology: devlang-csharp
ms.devlang: csharp
ms.assetid: a19545d3-24af-4a32-9778-cfb5ae938287
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: f4a30d19e111d395088e38c4543c9dacee6105fd
ms.lasthandoff: 03/13/2017

---

# <a name="publishing-your-hello-world-application-with-visual-studio-2017"></a>Pubblicazione dell'applicazione Hello World con Visual Studio 2017

Nell'argomento [Creazione di un'applicazione C# Hello World con .NET Core in Visual Studio 2017](with-visual-studio-2017.md) è stata creata l'applicazione console Hello World, mentre nell'argomento [Debug dell'applicazione C# Hello World con Visual Studio 2017](debugging-with-visual-studio-2017.md) tale applicazione è stata testata usando il debugger di Visual Studio. A questo punto è sicuro che l'applicazione funziona nel modo previsto ed è possibile pubblicarla in modo che possa essere eseguita da altri utenti. Con la pubblicazione viene creato il set di file necessari per eseguire l'applicazione. È possibile distribuire tali file copiandoli in un computer di destinazione.

Per pubblicare ed eseguire l'applicazione: 

1. Verificare che Visual Studio compili la versione di rilascio dell'applicazione. Se necessario, modificare la configurazione di compilazione nella barra degli strumenti da **Debug** in **Rilascio**, come mostrato nella figura seguente.

   ![Immagine](media/release.jpg)

1. Aprire una finestra della console. Ad esempio, nella casella di testo **Chiedimi qualcosa** della barra delle applicazioni di Windows immettere `Command Prompt` e quindi scegliere l'app desktop **Prompt dei comandi** per aprire la finestra della console.

1. Fare clic con il pulsante destro del mouse sul progetto HelloWorld (non sulla soluzione HelloWorld) e scegliere **Pubblica** dal menu. È anche possibile scegliere **Pubblica HelloWorld** dal menu principale **Compila** di Visual Studio.

1. Quando viene visualizzata la finestra di dialogo **Pubblica** mostrata nella figura seguente, creare un nuovo profilo di pubblicazione selezionando **Crea nuovo profilo**.

1. Nella finestra di dialogo **Pick a publishing target** (Scegli una destinazione di pubblicazione) mostrata nella figura seguente scegliere il pulsante **OK** per pubblicare l'applicazione nel file system locale. L'applicazione si troverà nella sottodirectory bin\release\PublishOutput della directory del progetto dell'applicazione.

1. Ora che è stato creato un profilo di pubblicazione, scegliere il pulsante **Pubblica** nella finestra di dialogo **Pubblica**, mostrata nella figura seguente.

   ![Immagine](media/publish-2.jpg)

1. Come mostrato nella figura seguente, l'output pubblicato include i tre file riportati di seguto. Tali file costituiscono l'applicazione ed è possibile distribuirli copiandoli in un sistema di destinazione:

      - HelloWorld.dll
   
      - HelloWorld.deps.json

      - HelloWorld.runtimeconfig.json

   Un quarto file, HelloWorld.pdb, contiene i simboli di debug. Non è necessario distribuire tale file insieme all'applicazione, anche se è consigliabile salvarlo nel caso in cui sia necessario eseguire il debug della versione pubblicata dell'applicazione.

   ![Immagine](media/pub-files.jpg)

Il processo di pubblicazione crea una distribuzione dipendente dal framework. L'applicazione pubblicata potrà essere eseguita su qualsiasi piattaforma supportata da .NET Core, a condizione che quest'ultimo sia installato nel sistema. Gli utenti possono eseguire l'applicazione attivando il comando `dotnet.exe HelloWorld.dll` da una finestra della console.

Per altre informazioni sulla pubblicazione e la distribuzione di applicazioni .NET Core, vedere [Distribuzione di applicazioni .NET Core](../../core/deploying/index.md).
