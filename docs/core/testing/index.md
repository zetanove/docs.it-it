---
title: "Testing unità in .NET Core"
description: "Testing unità in .NET Core"
keywords: .NET, .NET Core
author: ardalis
manager: wpickett
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 815ac74c-4bd9-4a94-a87c-78288b27c0e2
translationtype: Human Translation
ms.sourcegitcommit: 149086110d7470d97e1ab3e5969269626290b523
ms.openlocfilehash: 94bae12916fd20f534916d97157605c6a9aa9202

---

# <a name="unit-testing-in-net-core"></a>Testing unità in .NET Core

Di [Steve Smith](http://ardalis.com) e [Bill Wagner](https://github.com/BillWagner)

.NET Core è stato progettato prestando particolare attenzione alla testabilità, in modo da facilitare la creazione di unit test per le applicazioni. Questo articolo include una breve introduzione agli unit test e ne descrive le differenze rispetto agli altri tipi di test.
Le risorse collegate illustrano come aggiungere un progetto di test alla soluzione sviluppata e quindi eseguire unit test usando la riga di comando o Visual Studio.

## <a name="getting-started-with-testing"></a>Introduzione al testing
 
L'uso di un gruppo di test automatizzati è uno dei modi migliori per verificare che un'applicazione software esegua le operazioni per la quale è stata sviluppata. Esistono molti tipi diversi di test per le applicazioni software, inclusi i test di integrazione, i test Web, i test di carico e molti altri. Al livello più basso si collocano gli unit test, che consentono di testare singoli metodi o componenti software. Gli unit test devono testare soltanto il codice sotto il controllo dello sviluppatore, senza verificare eventuali problemi dell'infrastruttura, come database, file system o risorse di rete. Gli unit test possono essere scritti usando [Test Driven Development (TDD)](http://deviq.com/test-driven-development/) (Sviluppo basato su test) o possono essere aggiunti al codice esistente per verificarne la correttezza. In entrambi i casi devono essere di piccole dimensioni, ben identificabili e veloci, poiché in teoria può essere necessario eseguirne centinaia prima di effettuare il push delle modifiche nel repository del codice condiviso del progetto.

> [!NOTE]
> Gli sviluppatori hanno spesso difficoltà a scegliere i nomi appropriati per i metodi e le classi di test. Come punto di partenza, è possibile fare riferimento alle [convenzioni](https://github.com/aspnet/Home/wiki/Engineering-guidelines#unit-tests-and-functional-tests) adottate dal team del prodotto ASP.NET.

Quando si scrivono unit test, fare attenzione a non introdurre accidentalmente dipendenze dall'infrastruttura. Queste dipendenze tendono a rendere i test più lenti e fragili ed è quindi consigliabile usarle solo nei test di integrazione. È possibile evitare queste dipendenze nascoste nel codice dell'applicazione seguendo il [principio delle dipendenze esplicite](http://deviq.com/explicit-dependencies-principle/) e usando la tecnica di [inserimento delle dipendenze](https://docs.asp.net/en/latest/fundamentals/dependency-injection.html) per richiedere le dipendenze dal framework. È inoltre possibile mantenere gli unit test in un progetto separato dai test di integrazione e verificare che il progetto di unit test non includa riferimenti o dipendenze relative a pacchetti dell'infrastruttura.

Altre informazioni sul testing unità sono disponibili nei progetti .NET Core:

Provare questa [procedura dettagliata per la creazione di unit test con xUnit e l'interfaccia della riga di comando .NET](unit-testing-with-dotnet-test.md).

Il team di xUnit ha scritto un'esercitazione che illustra [come usare xUnit con .NET Core e Visual Studio](http://xunit.github.io/docs/getting-started-dotnet-core.html).



<!--HONumber=Nov16_HO1-->


