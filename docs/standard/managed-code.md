---
title: Informazioni sul codice gestito
description: Informazioni sul codice gestito
keywords: .NET, .NET Core
author: blackdwarf
manager: wpickett
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 20bb7ea8-192e-4a96-8ef3-e10e1950fd3d
translationtype: Human Translation
ms.sourcegitcommit: 0013cf5604bfd1e8a16e5ca15577ac81fce49612
ms.openlocfilehash: f05bd2e2344b4dd61d038278ad02e9c8f357b3a8

---

# <a name="what-is-managed-code"></a>Informazioni sul codice gestito

Quando si lavora con .NET Framework, viene spesso utilizzato il termine "codice gestito". Questo documento illustra il significato di questo termine e fornisce informazioni aggiuntive.

Detto in parole povere, il codice gestito è un codice la cui esecuzione è gestita da un runtime. In questo caso il runtime in questione è denominato **CLR (Common Language Runtime)** indipendentemente dall'implementazione ([Mono](http://www.mono-project.com/), .NET Framework o .NET Core). Il CLR è responsabile dell'acquisizione del codice gestito, della compilazione dello stesso in codice macchina e quindi della sua esecuzione. Aspetto ancora più importante, il runtime offre diversi servizi importanti, ad esempio la gestione automatica della memoria, i limiti di sicurezza, l'indipendenza dai tipi e così via.

Il modo in cui viene eseguito un programma C/C++, denominato anche "codice non gestito", è opposto a quanto sopra esposto. Nel "mondo non gestito", il programmatore è responsabile di tutte le attività relative al codice. Il programma effettivo è essenzialmente un file binario che il sistema operativo carica in memoria e avvia. Tutti gli altri aspetti, dalla gestione della memoria alle considerazioni sulla sicurezza, sono a carico del programmatore.

Il codice gestito è scritto in uno dei linguaggi di alto livello eseguibili nella piattaforma .NET, ad esempio C#, Visual Basic, F# e altri. Quando si compila codice scritto in uno di questi linguaggi con il relativo compilatore, non si ottiene codice macchina. Si ottiene invece codice in **linguaggio intermedio ** che il runtime provvede a compilare ed eseguire. C++ è l'unica eccezione a questa regola, poiché può generare alche file binari nativi non gestiti eseguibili in Windows.

## <a name="intermediate-language-execution"></a>Linguaggio intermedio ed esecuzione

Cosa si intende con il termine "linguaggio intermedio"? Il linguaggio intermedio è un prodotto della compilazione di codice scritto in linguaggi .NET di alto livello. Dopo la compilazione del codice scritto in uno di questi linguaggi, si ottiene un file binario in linguaggio intermedio. È importante notare che il linguaggio intermedio è indipendente da qualsiasi linguaggio specifico eseguito a un livello superiore rispetto al runtime. Esiste una specifica separata che è possibile consultare per maggiori informazioni.

Una volta generato il linguaggio intermedio dal codice di alto livello, è probabile che si voglia eseguirlo. A questo punto il CLR assume il controllo e avvia il processo di compilazione **Just-In-Time**, o **JIT**, del codice dal linguaggio intermedio al codice macchina che può essere effettivamente eseguito su una CPU. In questo modo, il CLR conosce esattamente le finalità del codice e può _gestirlo_.

Talvolta il linguaggio intermedio viene chiamato anche CIL (Common Intermediate Language) o MSIL (Microsoft Intermediate Language).

## <a name="unmanaged-code-interoperability"></a>Interoperabilità con codice non gestito

Il CLR consente naturalmente il superamento dei confini tra "mondo gestito" e "mondo non gestito". È disponibile molto codice in grado di eseguire tale operazione, anche nelle [librerie di classi base](framework-libraries.md). Questa attività è denominata **interoperabilità**, abbreviata in **interop**. Queste condizioni consentono, ad esempio, di eseguire il wrapping di una libreria non gestita e di chiamarla. È tuttavia importante notare che, una volta eseguita questa operazione, quando il codice oltrepassa i confini del runtime, la gestione effettiva dell'esecuzione è di nuovo responsabilità del codice non gestito e di conseguenza è soggetta alle stesse limitazioni.

Analogamente a quanto sopra esposto, C# è un linguaggio che consente di usare costrutti non gestiti, ad esempio i puntatori, direttamente nel codice usando il cosiddetto **contesto non sicuro**. Questo termine indica una porzione di codice la cui esecuzione non è gestita dal CLR.

## <a name="more-resources"></a>Altre risorse

*   [Cenni preliminari su .NET Framework](https://msdn.microsoft.com/library/zw4w595w.aspx)
*   [Codice unsafe e puntatori](https://msdn.microsoft.com/library/t2yzs44b.aspx)
*   [Interoperabilità (Guida per programmatori C#)](https://msdn.microsoft.com/library/ms173184.aspx)



<!--HONumber=Nov16_HO1-->


