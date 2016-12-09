---
title: Introduzione all&quot;uso di .NET Core su Windows con Visual Studio 2017
description: Introduzione all&quot;uso di .NET Core su Windows con Visual Studio 2017
keywords: .NET, .NET Core
author: bleroy
ms.author: mairaw
ms.date: 11/16/2016
ms.topic: article
ms.prod: .net-core
ms.devlang: dotnet
ms.assetid: d743134a-08a3-4ff6-aab7-49f71f0568c3
translationtype: Human Translation
ms.sourcegitcommit: 71eab6216e116b99927dfeaa8ce3cf70bcc08a5e
ms.openlocfilehash: 4437f44523bcc4e8517de5b6be42a63439f817d7

---

# <a name="getting-started-with-net-core-on-windows-using-visual-studio-2017"></a>Introduzione all'uso di .NET Core su Windows con Visual Studio 2017

di [Bertrand Le Roy](https://github.com/bleroy) e [Phillip Carter](https://github.com/cartermp)

Visual Studio 2017 offre un ambiente completo per lo sviluppo di applicazioni .NET Core. Questo documento descrive le procedure necessarie per compilare un'applicazione console molto semplice usando Visual Studio e .NET Core.

## <a name="prerequisites"></a>Prerequisiti

Seguire le istruzioni nella [pagina dei prerequisiti](../windows-prerequisites.md) per aggiornare l'ambiente.

## <a name="getting-started"></a>Introduzione

Questa procedura consente di configurare Visual Studio 2017 per lo sviluppo di applicazioni console .NET Core:

1. In Visual Studio fare clic sul menu **File** e scegliere **Nuovo**, **Progetto**.

2. Nella finestra di dialogo **Nuovo progetto**, nell'elenco **Modelli**, espandere il nodo **Visual C#** e scegliere **.NET Core**. Verranno visualizzati quattro modelli di progetto: **Applicazione console (.NET Core)**, **Progetto unit test (.NET Core)**, **Libreria di classi (.NET Core)** e **Applicabile Web ASP.NET (.NET Core)**. Scegliere **Applicazione console (.NET Core)**, digitare un nome per il progetto, selezionare un percorso e quindi fare clic su OK.

  ![Nuovo progetto: Applicazione console](media/new-project-console-app.png)

3. Il progetto risultante sarà composto da un unico file C# che scriverà "Hello World" nella console.

  ![Progetto Applicazione console](media/console-app-solution.png)

È possibile eseguire questa applicazione in modalità di debug premendo F5 o in modalità di rilascio premendo CTRL + F5. È possibile anche impostare punti di interruzione per interrompere l'esecuzione ed esaminare le variabili oppure iniziare a scrivere codice più interessante.

Buona codifica!

## <a name="what-to-do-next"></a>Operazioni successive

Dopo questa semplice introduzione è possibile passare alla compilazione di soluzioni più avanzate con test e librerie riutilizzabili. A questo scopo, vedere l'argomento [Creazione di una soluzione .NET Core completa in Windows tramite Visual Studio 2017](using-on-windows-vs-2017-full-solution.md).



<!--HONumber=Nov16_HO3-->


