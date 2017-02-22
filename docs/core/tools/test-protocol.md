---
title: Protocollo di comunicazione dei test dell&quot;interfaccia della riga di comando di .NET Core | Microsoft Docs
description: Protocollo di comunicazione dei test dell&quot;interfaccia della riga di comando di .NET Core
keywords: .NET, .NET Core
author: blackdwarf
ms.author: mairaw
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.technology: dotnet-cli
ms.devlang: dotnet
ms.assetid: 88cba792-3640-41de-b55d-00f575e9d5e2
translationtype: Human Translation
ms.sourcegitcommit: 796df1549a7553aa93158598d62338c02d4df73e
ms.openlocfilehash: 83555650a5a3ce9ed28d329aa82f5ead75e2d9cb

---

#<a name="net-core-cli-test-communication-protocol"></a>Protocollo di comunicazione dei test dell'interfaccia della riga di comando di .NET Core

> [!WARNING]
> Questo argomento si applica agli strumenti dell'anteprima 2 di .NET Core. Per la documentazione relativa agli strumenti di .NET Core versione RC4, vedere la sezione [Strumenti dell'interfaccia della riga di comando di .NET Core (strumenti di .NET Core RC4)](../preview3/tools/index.md).

## <a name="introduction"></a>Introduzione
Quando si passa una porta al test dotnet, il comando viene eseguito in fase di progettazione. Ciò significa che `dotnet test` si connette alla porta tramite TCP e quindi scambia un determinato set di messaggi con qualsiasi altro componente connesso a tale porta. Quando ciò accade, il runner riceve anche una nuova porta che viene usata da `dotnet test` per le comunicazioni con il runner. L'uso di TCP per le comunicazioni tra runner e `dotnet test` è dovuto al fatto che, in modalità di progettazione, non è sufficiente inviare i risultati alla console. Il comando deve inviare all'adapter i messaggi della struttura contenenti i risultati dell'esecuzione del test.

### <a name="communication-protocol-at-design-time"></a>Protocollo di comunicazione in fase di progettazione

1. Poiché, durante la fase di progettazione, `dotnet test` si connette a una porta all'avvio, l'adapter deve essere in ascolto su tale porta, altrimenti `dotnet test` avrà esito negativo. In questo modo, l'adapter può riservare tutte le porte necessarie rimanendo in ascolto su tali porte prima che `dotnet test` venga eseguito e provi a ottenere le porte per il runner.
2. Una volta avviato, `dotnet test` invia all'adapter un messaggio TestSession.Connected per segnalare che è pronto a ricevere messaggi.
3. È possibile inviare un messaggio facoltativo di [controllo della versione](https://github.com/dotnet/cli/blob/rel/1.0.0-preview2/src/Microsoft.Extensions.Testing.Abstractions/Messages/ProtocolVersionMessage.cs) in cui è riportata la versione del protocollo dell'adapter. In risposta a questo messaggio, `dotnet test` invierà la versione del protocollo supportata.

Tutti i messaggi presentano il formato descritto qui: [Message.cs](https://github.com/dotnet/cli/blob/rel/1.0.0-preview2/src/Microsoft.Extensions.Testing.Abstractions/Messages/Message.cs). I formati del payload per ogni messaggio sono descritti nei collegamenti alle classi usate per serializzare o deserializzare le informazioni nella descrizione del protocollo.

#### <a name="test-execution"></a>Esecuzione dei test
![Esecuzione dei test](./media/test-protocol/dotnet-test-execute.png)

1. Dopo il controllo della versione facoltativo, l'adapter invia un messaggio TestExecution.GetTestRunnerProcessStartInfo, con l'indicazione dei [test](https://github.com/dotnet/cli/blob/rel/1.0.0-preview2/src/Microsoft.Extensions.Testing.Abstractions/Messages/RunTestsMessage.cs) che vuole eseguire. `dotnet test` restituisce un nome di file e gli argomenti all'interno di un payload [TestStartInfo](https://github.com/dotnet/cli/blob/rel/1.0.0-preview2/src/dotnet/commands/dotnet-test/TestStartInfo.cs) che l'adapter può usare per avviare il runner. In passato, l'elenco dei test da eseguire veniva inviato come parte dell'argomento, ma per alcuni progetti di test veniva superato il limite delle dimensioni della riga di comando.
  1. Come parte degli argomenti, viene inviata una porta a cui il runner deve connettersi e, per l'esecuzione di test, un flag --wait-command, indicante che il runner deve connettersi alla porta e rimanere in attesa dei comandi, anziché procedere con l'esecuzione dei test.
2. A questo punto, l'adapter può avviare il runner ed eventualmente connettersi ad esso per il debug.
3. Una volta avviato, il runner invia a `dotnet test` un messaggio TestRunner.WaitCommand per segnalare che è pronto a ricevere comandi. A questo punto, `dotnet test` invia un messaggio TestRunner.Execute con l'elenco di [test](https://github.com/dotnet/cli/blob/rel/1.0.0-preview2/src/Microsoft.Extensions.Testing.Abstractions/Messages/RunTestsMessage.cs) da eseguire. Ciò consente di evitare il problema descritto in precedenza riguardo al limite delle dimensioni della riga di comando.
4. Il runner invia quindi a `dotnet test` (e inoltra all'adapter) un messaggio TestExecution.TestStarted per ogni test avviato, con le informazioni relative ai [test](https://github.com/dotnet/cli/blob/rel/1.0.0-preview2/src/Microsoft.Extensions.Testing.Abstractions/Test.cs).
5. Il runner invia anche a `dotnet test` (e inoltra all'adapter) un messaggio TestExecution.TestResult per ogni test, con il [singolo risultato](https://github.com/dotnet/cli/blob/rel/1.0.0-preview2/src/Microsoft.Extensions.Testing.Abstractions/TestResult.cs) del test.
6. Al termine di tutti i test, il runner invia a dotnet test un messaggio TestRunner.Completed, che `dotnet test` invia all'adapter come TestExecution.Completed.
7. Al termine, l'adapter invia a `dotnet test` un messaggio TestSession.Terminate che determina l'arresto di `dotnet test`.

#### <a name="test-discovery"></a>Individuazione dei test
![Individuazione dei test](./media/test-protocol/dotnet-test-discover.png)

1. Dopo il controllo della versione facoltativo, l'adapter invia un messaggio TestDiscovery.Start. Poiché in questo caso l'adapter non deve connettersi al processo, `dotnet test` avvia direttamente il runner. Inoltre, poiché non deve essere passato un lungo elenco di argomenti al runner, non è richiesto l'invio del flag --wait-command al runner. `dotnet test` passa solo un argomento --list al runner. Ciò significa che il runner non deve eseguire i test ma solo elencarli.
2. Il runner invia quindi a `dotnet test` (e inoltra all'adapter) un messaggio TestDiscovery.TestFound per ogni [test](https://github.com/dotnet/cli/blob/rel/1.0.0-preview2/src/Microsoft.Extensions.Testing.Abstractions/Test.cs) trovato.
3. Dopo aver individuato tutti i test, il runner invia a dotnet test un messaggio TestRunner.Completed che `dotnet test` invia all'adapter come TestDiscovery.Completed.
4. Al termine, l'adapter invia a `dotnet test` un messaggio TestSession.Terminate che determina l'arresto di `dotnet test`.



<!--HONumber=Feb17_HO2-->


