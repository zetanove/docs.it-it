---
title: "Constrained Execution Regions | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "constrained execution regions"
  - "CERs"
ms.assetid: 99354547-39c1-4b0b-8553-938e8f8d1808
caps.latest.revision: 9
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 9
---
# Constrained Execution Regions
Un'area a esecuzione vincolata \(CER, Constrained Execution Region\) fa parte di un meccanismo per la creazione di codice gestito affidabile.  Definisce un'area in cui Common Language Runtime \(CLR\) è vincolato in modo da non generare eccezioni fuori banda che impedirebbero l'esecuzione completa del codice incluso nell'area,  nella quale sono previsti vincoli per il codice utente che non consentono l'esecuzione del codice da cui è possibile che vengano generate eccezioni fuori banda.  Il metodo <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareConstrainedRegions%2A>, che deve trovarsi immediatamente prima di un blocco `try`, contrassegna i blocchi `catch`, `finally` e `fault` come aree a esecuzione vincolata.  Una volta contrassegnato come area vincolata, il codice deve solamente chiamare altro codice con contratti di affidabilità elevata ed evitare di allocare o effettuare chiamate virtuali a metodi non preparati o non affidabili, a meno che non sia predisposto per la gestione degli errori.  CLR posticipa le interruzioni dei thread per il codice in esecuzione in un'area CER.  
  
 Oltre che in un blocco `try` con annotazione, le aree a esecuzione vincolata vengono utilizzate in altri elementi di Common Language Runtime, in particolare nei finalizzatori critici in esecuzione all'interno di classi derivate da <xref:System.Runtime.ConstrainedExecution.CriticalFinalizerObject> e nel codice eseguito tramite il metodo <xref:System.Runtime.CompilerServices.RuntimeHelpers.ExecuteCodeWithGuaranteedCleanup%2A>.  
  
## Preparazione anticipata delle aree CER  
 Per evitare condizioni di memoria insufficiente, CLR prepara le aree CER in anticipo.  La preparazione anticipata è necessaria affinché CLR non determini condizioni di memoria insufficiente durante la compilazione JIT o il caricamento dei tipi.  
  
 Lo sviluppatore deve necessariamente indicare se un'area di codice è di tipo CER:  
  
-   Il livello superiore dell'area CER e i metodi nel grafico delle chiamate completo a cui è stato applicato l'attributo <xref:System.Runtime.ConstrainedExecution.ReliabilityContractAttribute> devono venire preparati in anticipo.  L'attributo <xref:System.Runtime.ConstrainedExecution.ReliabilityContractAttribute> fornisce solamente garanzie di <xref:System.Runtime.ConstrainedExecution.Cer> o <xref:System.Runtime.ConstrainedExecution.Cer>.  
  
-   La preparazione anticipata non può essere eseguita per chiamate non determinabili statisticamente, quale l'invio virtuale.  In questi casi, è necessario utilizzare il metodo <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareMethod%2A>.  Quando si utilizza il metodo <xref:System.Runtime.CompilerServices.RuntimeHelpers.ExecuteCodeWithGuaranteedCleanup%2A>, è necessario applicare l'attributo <xref:System.Runtime.ConstrainedExecution.PrePrepareMethodAttribute> al codice di pulitura.  
  
## Vincoli  
 Gli utenti devono sottostare ai vincoli previsti per il tipo di codice che è possibile scrivere in un'area CER.  Il codice non può generare eccezioni fuori banda, al contrario di quanto potrebbe verificarsi a causa delle seguenti operazioni:  
  
-   Allocazione esplicita.  
  
-   Boxing.  
  
-   Acquisizione di un blocco.  
  
-   Chiamate virtuali a metodi non preparati.  
  
-   Chiamate a metodi privi di contratto di affidabilità o con contratto di affidabilità debole.  
  
 In .NET Framework versione 2.0 questi vincoli rappresentano delle indicazioni guida.  La diagnostica viene fornita tramite strumenti di analisi del codice.  
  
## Contratti di affidabilità  
 L'attributo personalizzato <xref:System.Runtime.ConstrainedExecution.ReliabilityContractAttribute> indica le garanzie di affidabilità e lo stato di danneggiamento di un determinato metodo.  
  
### Garanzie di affidabilità  
 Le garanzie di affidabilità, rappresentate da valori dell'enumerazione <xref:System.Runtime.ConstrainedExecution.Cer> indicano il livello di affidabilità di un determinato metodo.  
  
-   <xref:System.Runtime.ConstrainedExecution.Cer>.  In condizioni eccezionali il metodo può avere esito negativo.  In tal caso, il metodo segnalerà al metodo chiamante l'esito positivo o negativo.  Affinché possa fornire il valore restituito, il metodo deve essere contenuto in un'area CER.  
  
-   <xref:System.Runtime.ConstrainedExecution.Cer>.  Il metodo, tipo o assembly non dispone di alcun concetto di area CER e, in genere, non è sicuro effettuare chiamate in un'area CER senza limitare in misura sostanziale il danneggiamento dello stato.  Il metodo non usufruisce dei vantaggi offerti dalle garanzie CER.  Se ne deduce che:  
  
    1.  In condizioni eccezionali il metodo può avere esito negativo  
  
    2.  Non è possibile stabilire se il metodo segnalerà o meno l'esito negativo.  
  
    3.  Il metodo non è scritto per l'utilizzo di un'area CER \(scenario più probabile\).  
  
    4.  Se non ne viene indicato l'esito positivo in modo esplicito, un metodo, un tipo o un assembly viene identificato implicitamente come <xref:System.Runtime.ConstrainedExecution.Cer>.  
  
-   <xref:System.Runtime.ConstrainedExecution.Cer>.  In condizioni eccezionali è garantito l'esito positivo del metodo.  Per ottenere questo livello di affidabilità, è sempre necessario costruire un'area CER attorno al metodo chiamato, anche se la chiamata viene eseguita dall'interno di un'area non CER.  Anche se la riuscita del metodo può essere considerata da un punto di vista soggettivo, un metodo ha esito positivo se esegue le operazioni previste.  Se ad esempio si contrassegna Count con `ReliabilityContractAttribute(Cer.Success)`, il metodo, quando viene eseguito in un'area CER, restituirà sempre il conteggio del numero di elementi presenti nell'oggetto <xref:System.Collections.ArrayList> e non potrà mai lasciare i campi interni in uno stato indeterminato.  Tuttavia, verrà contrassegnato come riuscito anche il metodo <xref:System.Threading.Interlocked.CompareExchange%2A>, fatto salvo che l'esito positivo può sempre significare che, a causa di una race condition, il valore esistente non è stato sostituito dal nuovo.  Fondamentalmente, è necessario che il metodo si comporti nel modo documentato al riguardo e che il codice CER non debba essere scritto in modo da prevedere comportamenti insoliti, oltre a quelli che possono verificarsi in caso di codice corretto ma non affidabile.  
  
### Livelli di danneggiamento  
 I livelli di danneggiamento, rappresentati da valori dell'enumerazione <xref:System.Runtime.ConstrainedExecution.Consistency>, indicano il grado di danneggiamento a cui è soggetto lo stato in un determinato ambiente.  
  
-   <xref:System.Runtime.ConstrainedExecution.Consistency>.  In condizioni eccezionali Common Language Runtime non offre alcuna garanzia sulla coerenza dello stato nel dominio applicazione corrente.  
  
-   <xref:System.Runtime.ConstrainedExecution.Consistency>.  In condizioni eccezionali è garantito che il metodo limiterà il danneggiamento dello stato all'istanza corrente.  
  
-   <xref:System.Runtime.ConstrainedExecution.Consistency>. In condizioni eccezionali, CLR non offre alcuna garanzia sulla coerenza dello stato. In altri termini, è possibile che la condizione danneggi il processo.  
  
-   <xref:System.Runtime.ConstrainedExecution.Consistency>.  In condizioni eccezionali è garantito che il metodo non danneggerà il processo.  
  
## Istruzione try\/catch\/finally di affidabilità  
 L'istruzione `try/catch/finally` di affidabilità rappresenta un meccanismo di gestione delle eccezioni che offre lo stesso livello di garanzie di prevedibilità della versione non gestita.  Il blocco `catch/finally` è l'area CER.  I metodi contenuti in questo blocco devono essere preparati in anticipo e non devono poter essere interrotti.  
  
 In .NET Framework versione 2.0 il codice segnala l'affidabilità di un blocco try a Common Language Runtime chiamando il metodo <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareConstrainedRegions%2A> che precede immediatamente il blocco try.  Il metodo <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareConstrainedRegions%2A> è membro di <xref:System.Runtime.CompilerServices.RuntimeHelpers>, una classe di supporto del compilatore.  Chiamare <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareConstrainedRegions%2A> direttamente sospendendone la disponibilità nei compilatori.  
  
## Aree non sottoponibili a interruzioni  
 Un'area che non può essere interrotta raggruppa un insieme di istruzioni all'interno di un'area CER.  
  
 In .NET Framework versione 2.0 la sospensione della disponibilità nel supporto del compilatore fa sì che dal codice utente vengano create aree che non possono essere interrotte con un'istruzione try\/catch\/finally affidabile, che contiene un blocco try\/catch vuoto preceduto da una chiamata al metodo <xref:System.Runtime.CompilerServices.RuntimeHelpers.PrepareConstrainedRegions%2A>.  
  
## Oggetto finalizzatore critico  
 Un oggetto <xref:System.Runtime.ConstrainedExecution.CriticalFinalizerObject> garantisce che il finalizzatore verrà eseguito dalla Garbage Collection.  All'allocazione, il finalizzatore e il relativo grafico delle chiamate vengono preparati in anticipo.  Il metodo del finalizzatore viene eseguito in un'area CER e deve rispettare tutti i vincoli associati alle aree CER e ai finalizzatori.  
  
 È garantito che i finalizzatori di ciascun tipo che eredita da <xref:System.Runtime.InteropServices.SafeHandle> e <xref:System.Runtime.InteropServices.CriticalHandle> verranno eseguiti all'interno di un'area CER.  Implementare il metodo <xref:System.Runtime.InteropServices.SafeHandle.ReleaseHandle%2A> nella classe derivata <xref:System.Runtime.InteropServices.SafeHandle> per eseguire tutto il codice necessario per il rilascio dell'handle.  
  
## Codice non consentito nelle aree CER  
 Nelle aree CER non è consentito effettuare le seguenti operazioni:  
  
-   Allocazioni esplicite.  
  
-   Acquisizione di un blocco.  
  
-   Boxing.  
  
-   Accesso a matrici multidimensionali.  
  
-   Chiamate di metodi tramite la reflection.  
  
-   <xref:System.Threading.Monitor.Enter%2A> o <xref:System.IO.FileStream.Lock%2A>.  
  
-   Controlli di sicurezza.  Non eseguire le richieste, limitarsi a collegarle.  
  
-   <xref:System.Reflection.Emit.OpCodes.Isinst> e <xref:System.Reflection.Emit.OpCodes.Castclass> per proxy e oggetti COM.  
  
-   Recupero o impostazione di campi su un proxy trasparente.  
  
-   Serializzazione.  
  
-   Delegati e puntatori a funzione.  
  
## Vedere anche  
 [Reliability Best Practices](../../../docs/framework/performance/reliability-best-practices.md)