---
title: Protocollo di comunicazione dei test dell&quot;interfaccia della riga di comando di .NET Core
description: Protocollo di comunicazione dei test dell&quot;interfaccia della riga di comando di .NET Core
keywords: .NET, .NET Core
author: mairaw
manager: wpickett
ms.date: 06/20/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 88cba792-3640-41de-b55d-00f575e9d5e2
translationtype: Human Translation
ms.sourcegitcommit: 81e7604f0a646e5de9c2ed35ff3b6ef6d7fb2e71
ms.openlocfilehash: beab195d283fcfcdc454a29498d27bcd290b66c1

---

#<a name="net-core-cli-test-communication-protocol"></a>Protocollo di comunicazione dei test dell'interfaccia della riga di comando di .NET Core

## <a name="introduction"></a>Introduzione
Quando si passa una porta al test dotnet, il comando viene eseguito in fase di progettazione. Ciò significa che il test dotnet si connette alla porta tramite TCP e quindi scambia un determinato set di messaggi con qualsiasi altro componente connesso a tale porta. Quando ciò accade, il runner riceve anche una nuova porta che viene usata dal test dotnet per le comunicazioni con il runner. L'uso di TCP per le comunicazioni tra runner e test dotnet è dovuto al fatto che, in modalità di progettazione, non è sufficiente inviare i risultati alla console. Il comando deve inviare all'adapter i messaggi della struttura contenenti i risultati dell'esecuzione del test.

### <a name="communication-protocol-at-design-time"></a>Protocollo di comunicazione in fase di progettazione

1. Poiché, durante la fase di progettazione, il test dotnet si connette a una porta all'avvio, l'adapter deve essere in ascolto su tale porta, altrimenti il test dotnet avrà esito negativo. In questo modo, l'adapter può riservare tutte le porte necessarie rimanendo in ascolto su tali porte prima che il test dotnet venga eseguito e provi a ottenere le porte per il runner.
2. Una volta avviato, il test dotnet invia all'adapter un messaggio TestSession.Connected per segnalare che è pronto a ricevere messaggi.
3. È possibile inviare un messaggio facoltativo di [controllo della versione](https://github.com/dotnet/cli/blob/rel/1.0.0/src/Microsoft.Extensions.Testing.Abstractions/Messages/ProtocolVersionMessage.cs) in cui è riportata la versione del protocollo dell'adapter. In risposta a questo messaggio, il test dotnet invierà la versione del protocollo supportata.

Tutti i messaggi presentano il formato descritto qui: [Message.cs](https://github.com/dotnet/cli/blob/rel/1.0.0/src/Microsoft.Extensions.Testing.Abstractions/Messages/Message.cs). I formati del payload per ogni messaggio sono descritti nei collegamenti alle classi usate per serializzare o deserializzare le informazioni nella descrizione del protocollo.

#### <a name="test-execution"></a>Esecuzione dei test
![Esecuzione dei test](./media/test-protocol/dotnet-test-execute.png)

1. Dopo il controllo della versione facoltativo, l'adapter invia un messaggio TestExecution.GetTestRunnerProcessStartInfo, con l'indicazione dei [test](https://github.com/dotnet/cli/blob/rel/1.0.0/src/Microsoft.Extensions.Testing.Abstractions/Messages/RunTestsMessage.cs) che vuole eseguire. Il test dotnet restituisce un nome di file e gli argomenti all'interno di un payload [TestStartInfo](https://github.com/dotnet/cli/blob/rel/1.0.0/src/Microsoft.DotNet.Tools.Test/TestStartInfo.cs) che l'adapter può usare per avviare il runner. In passato, l'elenco dei test da eseguire veniva inviato come parte dell'argomento, ma per alcuni progetti di test veniva superato il limite delle dimensioni della riga di comando.
  1. Come parte degli argomenti, viene inviata una porta a cui il runner deve connettersi e, per l'esecuzione di test, un flag --wait-command, indicante che il runner deve connettersi alla porta e rimanere in attesa dei comandi, anziché procedere con l'esecuzione dei test.
2. A questo punto, l'adapter può avviare il runner ed eventualmente connettersi ad esso per il debug.
3. Una volta avviato, il runner invia al test dotnet un messaggio TestRunner.WaitCommand per segnalare che è pronto a ricevere comandi. A questo punto, il test dotnet invia un messaggio TestRunner.Execute con l'elenco di [test](https://github.com/dotnet/cli/blob/rel/1.0.0/src/Microsoft.Extensions.Testing.Abstractions/Messages/RunTestsMessage.cs) da eseguire. Ciò consente di evitare il problema descritto in precedenza riguardo al limite delle dimensioni della riga di comando.
4. Il runner invia quindi al test dotnet (e inoltra all'adapter) un messaggio TestExecution.TestStarted per ogni test avviato, con le informazioni relative ai [test](https://github.com/dotnet/cli/blob/rel/1.0.0/src/Microsoft.Extensions.Testing.Abstractions/Test.cs).
5. Il runner invia anche al test dotnet (e inoltra all'adapter) un messaggio TestExecution.TestResult per ogni test, con il [singolo risultato](https://github.com/dotnet/cli/blob/rel/1.0.0/src/Microsoft.Extensions.Testing.Abstractions/TestResult.cs) del test.
6. Al termine di tutti i test, il runner invia al test dotnet un messaggio TestRunner.Completed, che il test dotnet invia all'adapter come TestExecution.Completed.
7. Una volta completata l'operazione, l'adapter invia al test dotnet un messaggio TestSession.Terminate che determina l'arresto del test.

#### <a name="test-discovery"></a>Individuazione dei test
![Individuazione dei test](./media/test-protocol/dotnet-test-discover.png)

1. Dopo il controllo della versione facoltativo, l'adapter invia un messaggio TestDiscovery.Start. Poiché in questo caso l'adapter non deve connettersi al processo, il test dotnet avvia direttamente il runner. Inoltre, poiché non deve essere passato un lungo elenco di argomenti al runner, non è richiesto l'invio del flag --wait-command al runner. Il test dotnet passa solo un argomento --list al runner. Ciò significa che il runner non deve eseguire i test ma solo elencarli.
2. Il runner invia quindi al test dotnet (e inoltra all'adapter) un messaggio TestDiscovery.TestFound per ogni [test](https://github.com/dotnet/cli/blob/rel/1.0.0/src/Microsoft.Extensions.Testing.Abstractions/Test.cs) trovato.
3. Dopo aver individuato tutti i test, il runner invia al test dotnet un messaggio TestRunner.Completed, che il test invia all'adapter come TestDiscovery.Completed.
4. Una volta completata l'operazione, l'adapter invia al test dotnet un messaggio TestSession.Terminate che determina l'arresto del test.


<!--HONumber=Nov16_HO3-->


