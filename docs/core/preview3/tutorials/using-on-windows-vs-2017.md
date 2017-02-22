---
title: Introduzione all&quot;uso di .NET Core su Windows con Visual Studio 2017 | Microsoft Docs
description: Introduzione all&quot;uso di .NET Core su Windows con Visual Studio 2017
keywords: .NET, .NET Core
author: bleroy
ms.author: mairaw
ms.date: 01/18/2016
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: 613c65d0-f773-41b8-ba0e-83f6a82a0b30
translationtype: Human Translation
ms.sourcegitcommit: 796df1549a7553aa93158598d62338c02d4df73e
ms.openlocfilehash: cc2c2853bc31e161d1fe0de4edc71d15281c6d24

---

# <a name="getting-started-with-net-core-on-windows-using-visual-studio-2017-net-core-tools-rc4"></a>Introduzione all'uso di .NET Core su Windows con Visual Studio 2017 (strumenti di .NET Core RC4)

> [!WARNING]
> Questo argomento si applica agli strumenti di .NET Core RC4. Per gli strumenti dell'anteprima 2 di .NET Core (Visual Studio 2015), vedere l'argomento [Introduzione all'uso di .NET Core su Windows con Visual Studio 2015](../../tutorials/using-on-windows.md).

Visual Studio 2017 offre un ambiente completo per lo sviluppo di applicazioni .NET Core. Questo documento descrive le procedure necessarie per compilare un'applicazione console molto semplice usando Visual Studio e .NET Core.

## <a name="prerequisites"></a>Prerequisiti

Seguire le istruzioni nella [pagina dei prerequisiti](../windows-prerequisites.md) per aggiornare l'ambiente.

## <a name="getting-started"></a>Introduzione

Questa procedura consente di configurare Visual Studio 2017 per lo sviluppo di applicazioni console .NET Core:

1. In Visual Studio fare clic sul menu **File** e scegliere **Nuovo**, **Progetto**.

2. Nella finestra di dialogo **Nuovo progetto**, nell'elenco **Modelli**, espandere il nodo **Visual C#** e scegliere **.NET Core**. Verranno visualizzati cinque modelli di progetto: **Applicazione console (.NET Core)**, **Libreria di classi (.NET Standard)**, **Progetto unit test (.NET Core)**, **Libreria di classi (.NET Core)** e **Applicazione Web ASP.NET (.NET Core)**. Scegliere **Applicazione console (.NET Core)**, digitare un nome per il progetto, selezionare un percorso e quindi fare clic su OK.

  ![Nuovo progetto: Applicazione console](media/new-project-console-app.png)

3. Il progetto risultante sarà composto da un unico file C# che scriverà "Hello World" nella console.

  ![Progetto Applicazione console](media/console-app-solution.png)

È possibile eseguire questa applicazione in modalità di debug premendo F5 o in modalità di rilascio premendo CTRL + F5. È possibile anche impostare punti di interruzione per interrompere l'esecuzione ed esaminare le variabili oppure iniziare a scrivere codice più interessante.

Buona codifica!

## <a name="next-steps"></a>Passaggi successivi

Dopo questa semplice introduzione è possibile passare alla compilazione di soluzioni più avanzate con test e librerie riutilizzabili. A questo scopo, vedere l'argomento [Creazione di una soluzione .NET Core completa in Windows tramite Visual Studio 2017](using-on-windows-vs-2017-full-solution.md).



<!--HONumber=Feb17_HO2-->


