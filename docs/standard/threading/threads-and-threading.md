---
title: "Threads and Threading | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "multiple threads"
  - "threading [.NET Framework]"
  - "threading [.NET Framework], multiple threads"
ms.assetid: 5baac3aa-e603-4fa6-9f89-0f2c1084e6b1
caps.latest.revision: 14
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 14
---
# Threads and Threading
I sistemi operativi si servono dei processi per separare le diverse applicazioni eseguite.  I thread rappresentano l'unità di base a cui un sistema operativo assegna il tempo del processore ed è possibile che più di un thread esegua del codice all'interno del processo.  Ciascun thread gestisce i gestori eccezioni, una priorità di pianificazione e un insieme di strutture utilizzate per salvare nel sistema il contesto del thread fino a quando viene pianificato.  Nel contesto del thread sono presenti tutte le informazioni necessarie per riprendere senza problemi l'esecuzione nello spazio degli indirizzi del processo host del thread, incluse l'insieme di registri della CPU e lo stack.  
  
 In .NET Framework un processo di un sistema operativo viene suddiviso ulteriormente in sottoprocessi leggeri gestiti, definiti domini dell'applicazione, rappresentati da <xref:System.AppDomain?displayProperty=fullName>.  Uno o più thread gestiti, rappresentati da <xref:System.Threading.Thread?displayProperty=fullName>, possono essere eseguiti in uno o in un numero indefinito di domini dell'applicazione all'interno dello stesso processo gestito.  Sebbene ogni dominio dell'applicazione sia avviato con un singolo thread, il codice in quel dominio può creare domini dell'applicazione e thread aggiuntivi.  Il risultato è che un thread gestito può spostarsi senza problemi da un dominio dell'applicazione all'altro all'interno dello stesso processo gestito. È possibile avere un solo thread che si sposta tra diversi domini dell'applicazione.  
  
 Un sistema operativo che supporta il multitasking di tipo preemptive crea l'effetto dell'esecuzione simultanea di più thread di più processi.  Questa operazione viene eseguita dividendo il tempo del processore disponibile tra i thread che lo richiedono, allocando una porzione di tempo del processore a ogni thread, uno dopo l'altro.  Il thread in quel momento in esecuzione viene sospeso allo scadere della porzione di tempo e viene ripresa l'esecuzione di un altro thread.  Quando il sistema passa da un thread all'altro, salva il contesto del thread interrotto e ricarica il contesto del thread salvato del thread successivo nell'apposita coda.  
  
 L'entità della porzione di tempo dipende dal sistema operativo e dal processore.  Dal momento che ogni porzione di tempo è limitata, più thread sembrano in esecuzione contemporaneamente, anche in presenza di un solo processore.  Questa situazione si verifica effettivamente nei sistemi a più processori, in cui i thread eseguibili vengono distribuiti tra i vari processori disponibili.  
  
## Utilizzo di più thread  
 I programmi software che richiedono l'interazione dell'utente devono garantire tempi di risposta rapidi per offrire un'esperienza soddisfacente  ed eseguire al tempo stesso i calcoli necessari per presentare all'utente i dati il più velocemente possibile.  Se l'applicazione utilizza un solo thread di esecuzione, sarà possibile combinare la [programmazione asincrona](../../../docs/standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously.md) con [.NET Remoting](http://msdn.microsoft.com/it-it/eccb1d31-0a22-417a-97fd-f4f1f3aa4462) o i [servizi Web XML](http://msdn.microsoft.com/it-it/1e64af78-d705-4384-b08d-591a45f4379c) creati mediante ASP.NET per utilizzare il tempo di elaborazione di altri computer oltre a quello già disponibile per aumentare i tempi di risposta all'utente e diminuire il tempo di elaborazione dei dati dell'applicazione.  Se si eseguono molte operazioni di input\/output, sarà possibile anche utilizzare le porte di completamento I\/O per aumentare la velocità di risposta dell'applicazione.  
  
### Vantaggi dei thread multipli  
 L'utilizzo di più di un thread rappresenta comunque la tecnica più potente a disposizione per aumentare la velocità di risposta ed elaborare i dati necessari per completare il lavoro quasi contemporaneamente.  In un computer dotato di un solo processore, questo effetto viene ottenuto da più thread, che sfruttano i brevi periodi di tempo tra un evento utente e l'altro per l'elaborazione dei dati in background.  Un utente può modificare, ad esempio, un foglio di calcolo mentre un altro thread ne ricalcola altre parti all'interno della stessa applicazione.  
  
 Senza alcuna modifica, la stessa applicazione aumenterebbe in modo considerevole la soddisfazione del cliente se eseguita in un computer con più di un processore.  Il singolo dominio dell'applicazione potrebbe utilizzare più thread per realizzare le seguenti attività:  
  
-   Comunicare in rete con un server Web e un database.  
  
-   Eseguire operazioni che richiedono una notevole quantità di tempo.  
  
-   Operare una distinzione tra attività con diversa priorità.  Un thread ad alta priorità, ad esempio, gestisce attività in cui il tempo riveste molta importanza mentre un'attività a bassa priorità ne esegue altre.  
  
-   Consentire all'interfaccia utente di continuare ad essere veloce, allocando del tempo ad attività in background.  
  
### Svantaggi dei thread multipli  
 Si consiglia di utilizzare il minor numero di thread possibile, riducendo in questo modo al minimo l'utilizzo delle risorse del sistema operativo e migliorando le prestazioni.  Il threading presenta anche dei requisiti in termini di risorse e dei potenziali conflitti da considerare nella fase di progettazione dell'applicazione.  I requisiti in termini di risorse sono i seguenti:  
  
-   Il sistema consuma memoria per le informazioni sul contesto richieste da processi, oggetti **AppDomain** e thread.  Pertanto il numero di processi, oggetti **AppDomain** e thread che è possibile creare è limitato dalla memoria disponibile.  
  
-   Tenere traccia di un gran numero di thread determina un consumo notevole di tempo del processore.  Se sono presenti troppi thread, solo alcuni progrediranno in modo significativo.  Se la maggior parte dei thread correnti si trova in un processo, quelli contenuti in altri processi verranno pianificati meno frequentemente.  
  
-   Il controllo dell'esecuzione del codice con molti thread è un'operazione complessa e può causare numerosi bug.  
  
-   La distruzione dei thread richiede la conoscenza dei possibili effetti e la capacità di gestire i problemi creati.  
  
 L'accesso condiviso alle risorse può creare dei conflitti.  Per evitarli, è necessario sincronizzare o controllare l'accesso alle risorse condivise.  Una non corretta sincronizzazione dell'accesso, in domini dell'applicazione medesimi o diversi, può determinare problemi quali deadlock \(in cui due thread non rispondono più mentre l'uno attende il completamento dell'altro\) e race condition \(quando un risultato anomalo si verifica a causa di una dipendenza critica imprevista legata alla durata di due eventi\).  Nel sistema vengono forniti oggetti di sincronizzazione che è possibile utilizzare per coordinare la condivisione delle risorse tra più thread.  La riduzione del numero di thread rende più semplice la sincronizzazione delle risorse.  
  
 Le risorse che richiedono la sincronizzazione includono:  
  
-   Risorse di sistema, quali le porte di comunicazione.  
  
-   Risorse condivise da più processi, quali gli handle dei file.  
  
-   Risorse di un singolo dominio applicazione, ad esempio campi globali, statici e di istanza, a cui accedono più thread.  
  
### Threading e progettazione delle applicazioni  
 In generale l'utilizzo della classe <xref:System.Threading.ThreadPool> rappresenta il modo più semplice per gestire più thread per attività relativamente brevi senza bloccare altri thread e quando non si prevede una specifica pianificazione delle attività.  Esistono tuttavia diversi motivi per cui è opportuno creare dei thread personalizzati:  
  
-   Se è necessario che un'attività abbia una determinata priorità.  
  
-   Se si dispone di un'attività che potrebbe richiedere molto tempo, bloccandone quindi altre.  
  
-   Se è necessario inserire dei thread in un apartment a singolo thread. Tutti i thread **ThreadPool** sono in apartment con multithreading.  
  
-   Se è necessaria un'identità stabile associata al thread.  È opportuno ad esempio utilizzare un thread dedicato per terminarlo, sospenderlo o individuarlo in base al nome.  
  
-   Se è necessario eseguire thread in background che interagiscono con l'interfaccia utente, in .NET Framework versione 2.0 è disponibile un componente <xref:System.ComponentModel.BackgroundWorker> che comunica tramite eventi, con marshalling cross\-thread nel thread dell'interfaccia utente.  
  
### Threading ed eccezioni  
 Gestire le eccezioni nei thread.  In genere, le eccezioni non gestite nei thread, anche in background, determinano l'interruzione del processo.  Esistono tre eccezioni a questa regola:  
  
-   Viene generata un'eccezione <xref:System.Threading.ThreadAbortException> in un thread per effetto di una chiamata a <xref:System.Threading.Thread.Abort%2A>.  
  
-   Viene generata un'eccezione <xref:System.AppDomainUnloadedException> in un thread perché è in corso lo scaricamento del dominio applicazione.  
  
-   Il thread viene interrotto da Common Language Runtime o da un processo host.  
  
 Per ulteriori informazioni, vedere [Exceptions in Managed Threads](../../../docs/standard/threading/exceptions-in-managed-threads.md).  
  
> [!NOTE]
>  In .NET Framework versioni 1.0 e 1.1 Common Language Runtime intercetta automaticamente alcune eccezioni, ad esempio nei thread di un pool.  Questo comportamento può danneggiare lo stato dell'applicazione e determinare il blocco delle applicazioni, rendendo particolarmente difficile il debug.  
  
## Vedere anche  
 <xref:System.Threading.ThreadPool>   
 <xref:System.ComponentModel.BackgroundWorker>   
 [Synchronizing Data for Multithreading](../../../docs/standard/threading/synchronizing-data-for-multithreading.md)   
 [The Managed Thread Pool](../../../docs/standard/threading/the-managed-thread-pool.md)