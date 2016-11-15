---
title: .NET Portability Analyzer | .NET
description: "Informazioni su come usare lo strumento .NET Portability Analyzer per valutare la portabilità del codice tra le diverse piattaforme .NET."
keywords: .NET, .NET Core
author: blackdwarf
ms.author: mairaw
manager: wpickett
ms.date: 07/05/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 0375250f-5704-4993-a6d5-e21c499cea1e
translationtype: Human Translation
ms.sourcegitcommit: 8599be1eadcd6f005ef344bf173e8c06fce80725
ms.openlocfilehash: 479b141159de95c6a7e466220f935f9371b353db

---

# <a name="the-net-portability-analyzer"></a>.NET Portability Analyzer

È possibile fare in modo che le librerie in uso siano multi-piattaforma e vedere quanto lavoro è necessario per rendere l'applicazione compatibile con altre piattaforme .NET. [.NET Portability Analyzer](http://go.microsoft.com/fwlink/?LinkID=507467) è uno strumento che crea un report dettagliato sulla flessibilità del programma in tutte le piattaforme .NET analizzando gli assembly. Portability Analyzer è offerto come estensione di Visual Studio e come applicazione della console.

## <a name="new-targets"></a>Nuove destinazioni

*   [.NET Core](https://www.dotnetfoundation.org/netcore): ha una struttura modulare, con assembly affiancato ed è destinato a scenari multi-piattaforma. La modalità affiancata consente di adottare le nuove versioni di .NET Core senza interrompere le altre applicazioni.
*   [ASP.NET Core](https://www.dotnetfoundation.org/aspnet-core): è un framework Web moderno basato su .NET Core che offre agli sviluppatori gli stessi vantaggi.
*   [.NET Native](https://blogs.msdn.microsoft.com/dotnet/2014/04/24/net-native-performance): offre una compilazione statica che consente di migliorare le prestazioni delle applicazioni Windows Store eseguite su computer ARM e x64.

## <a name="how-to-use-portability-analyzer"></a>Come usare Portability Analyzer

Per iniziare a usare .NET Portability Analyzer, scaricare l'estensione da [Visual Studio Gallery](http://go.microsoft.com/fwlink/?LinkID=507467) e installarla. È possibile configurare l'estensione in Visual Studio da **Strumenti** > **Opzioni** > **.NET Portability Analyzer** e selezionare le piattaforme di destinazione. Per ora, usare ASP.NET Core come proxy per tutte le piattaforme basate su .NET Core, ad esempio [app UAP .NET di Windows 10](http://blogs.windows.com/buildingapps/2015/03/02/a-first-look-at-the-windows-10-universal-app-platform/).

![Schermata della portabilità](./media/portability-analyzer/portability-screenshot.png)

Per analizzare l'intero progetto, fare clic con il pulsante destro del mouse sul progetto in **Esplora soluzioni** e selezionare **Analizza** > ** > Analyze Assembly Portability (Analizza portabilità assembly)**. In caso contrario, accedere al menu **Analizza** e selezionare **Analyze Assembly Portability** (Analizza portabilità assembly). Da qui selezionare il file eseguibile o DLL del progetto.

![Esplora soluzioni per la portabilità](./media/portability-analyzer/portability-solution-explorer.png)

Dopo aver eseguito l'analisi, verrà visualizzato il report sulla portabilità di .NET. Solo i tipi non supportati da una piattaforma di destinazione verranno visualizzati nell'elenco ed è possibile esaminare i suggerimenti nella scheda **Messaggi** dell'**elenco degli errori**. È anche possibile passare alle aree problematiche direttamente dalla scheda **Messaggi**.

![Report sulla portabilità](./media/portability-analyzer/portability-report.png)

Si vuole evitare di usare Visual Studio? È possibile usare Portability Analyzer anche dal prompt dei comandi. Scaricare solo [API Portability Analyzer](http://www.microsoft.com/download/details.aspx?id=42678).

*   Digitare il comando seguente per analizzare la directory corrente: `\...\ApiPort.exe .`
*   Per analizzare un elenco specifico di file con estensione dll, digitare il comando seguente: `\...\ApiPort.exe first.dll second.dll third.dll`

Il report sulla portabilità di .NET verrà salvato come file di Excel con *estensione xlsx* nella directory corrente. Altre informazioni saranno disponibili nella scheda **Dettagli** della cartella di lavoro di Excel.

Per altre informazioni su .NET Portability Analyzer, vedere l'articolo sull'[uso di codice esistente nelle piattaforme .NET](https://blogs.msdn.microsoft.com/dotnet/2014/08/06/leveraging-existing-code-across-net-platforms/) del blog di .NET.



<!--HONumber=Nov16_HO1-->


