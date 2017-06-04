---
title: "Exceptions in Managed Threads | Microsoft Docs"
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
  - "unhandled exceptions,in managed threads"
  - "threading [.NET Framework],unhandled exceptions"
  - "threading [.NET Framework],exceptions in managed threads"
  - "managed threading"
ms.assetid: 11294769-2e89-43cb-890e-ad4ad79cfbee
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 7
---
# Exceptions in Managed Threads
A partire da .NET Framework versione 2.0, Common Language Runtime consente alla maggior parte delle eccezioni non gestite nei thread di proseguire normalmente.  Per questo motivo, nella maggior parte dei casi l'eccezione non gestita determina l'interruzione dell'applicazione.  
  
> [!NOTE]
>  Questa è una modifica significativa rispetto a .NET Framework versioni 1.0 e 1.1, che forniscono un meccanismo di backstop per numerose eccezioni non gestite, ad esempio quelle che si verificano nei thread del pool.  Al riguardo, vedere [Modifica rispetto alle versioni precedenti](#ChangeFromPreviousVersions) più avanti in questo argomento.  
  
 Common Language Runtime fornisce un meccanismo di backstop per alcune eccezioni non gestite utilizzate per controllare il flusso di programma:  
  
-   Viene generata un'eccezione <xref:System.Threading.ThreadAbortException> in un thread per effetto di una chiamata a <xref:System.Threading.Thread.Abort%2A>.  
  
-   Viene generata un'eccezione <xref:System.AppDomainUnloadedException> in un thread perché è in corso lo scaricamento del dominio applicazione in cui il thread è in esecuzione.  
  
-   Il thread viene interrotto da Common Language Runtime o da un processo host mediante la generazione di un'eccezione interna.  
  
 Se una qualsiasi di queste eccezioni non è gestita nei thread creati da Common Language Runtime, l'eccezione determina l'interruzione del thread, ma Common Language Runtime impedisce che prosegua ulteriormente.  
  
 Se queste eccezioni non sono gestite nel thread principale o nei thread passati sotto il controllo di Common Language Runtime dal codice non gestito, proseguono normalmente e l'applicazione viene quindi interrotta.  
  
> [!NOTE]
>  Common Language Runtime può generare un'eccezione non gestita prima che qualsiasi codice gestito riesca a installare un gestore eccezioni.  Anche se il codice gestito non può gestire in alcun modo tale eccezione, a quest'ultima viene consentito di proseguire normalmente.  
  
## Esposizione dei problemi associati al threading durante le operazioni di sviluppo  
 Quando i thread possono avere automaticamente esito negativo, senza interrompere l'applicazione, è possibile che non vengano rilevati gravi problemi di programmazione.  Si tratta di un problema specifico di servizi e altre applicazioni eseguiti per periodi di tempo prolungati.  Non appena si verifica un errore nei thread, lo stato del programma inizia gradualmente a danneggiarsi.  È possibile che le prestazioni dell'applicazione diminuiscano e quest'ultima si blocchi.  
  
 Quando si consente alle eccezioni non gestite nei thread di proseguire normalmente, finché il programma non termina automaticamente, è possibile esporre tali problemi durante le fasi di sviluppo e di verifica dell'applicazione.  I report di errore relativi alle interruzioni del programma supportano il debug.  
  
<a name="ChangeFromPreviousVersions"></a>   
## Modifica rispetto alle versioni precedenti  
 La modifica più significativa apportata rispetto alle versioni precedenti riguarda i thread gestiti.  In .NET Framework versioni 1.0 e 1.1 Common Language Runtime fornisce un meccanismo di backstop per le eccezioni non gestite nelle seguenti situazioni:  
  
-   Non esiste alcuna eccezione non gestita in un thread del pool.  Se un'attività genera un'eccezione di cui non esegue la gestione, Common Language Runtime stampa la traccia dello stack dell'eccezione nella console e quindi restituisce il thread nel relativo pool.  
  
-   Non esiste alcuna eccezione non gestita in un thread creato con il metodo <xref:System.Threading.Thread.Start%2A> della classe <xref:System.Threading.Thread>.  Quando il codice in esecuzione su tale thread genera un'eccezione di cui non esegue la gestione, Common Language Runtime stampa la traccia dello stack dell'eccezione nella console e quindi interrompe correttamente il thread.  
  
-   Non esiste alcuna eccezione non gestita nel thread finalizzatore.  Se un finalizzatore genera un'eccezione di cui non esegue la gestione, Common Language Runtime stampa la traccia dello stack dell'eccezione nella console e quindi ripristina l'esecuzione dei finalizzatori.  
  
 Lo stato in background o in primo piano di un thread gestito non influisce su questo comportamento.  
  
 Per le eccezioni non gestite in thread provenienti dal codice non gestito, la differenza è più sottile.  La finestra di dialogo per l'associazione JIT di Common Language Runtime viene visualizzata prima di quella del sistema operativo per le eccezioni gestite o native nei thread passati attraverso il codice nativo.  Il processo si interrompe in ogni caso.  
  
### Migrazione del codice  
 In genere, la modifica esporrà i problemi di programmazione, che in precedenza non venivano riconosciuti, affinché possano essere risolti.  In alcuni casi è tuttavia possibile che i programmatori abbiano usufruito della funzionalità di backstop di Common Language Runtime, ad esempio per interrompere i thread.  A seconda della situazione, è opportuno che prendano in considerazione una delle seguenti strategie di migrazione:  
  
-   Ristrutturare il codice in modo che i thread si interrompano normalmente alla ricezione di un segnale.  
  
-   Utilizzare il metodo <xref:System.Threading.Thread.Abort%2A?displayProperty=fullName> per interrompere il thread.  
  
-   Se è necessario che un thread venga interrotto perché l'operazione di arresto del processo possa continuare, trasformare il thread in un thread in background, in modo che termini automaticamente all'uscita dal processo.  
  
 In ogni caso la strategia deve rispettare le indicazioni guida per la progettazione relative alle eccezioni.  Per informazioni al riguardo, vedere [Linee guida di progettazione per le eccezioni](../../../docs/standard/design-guidelines/exceptions.md).  
  
### Flag di compatibilità tra applicazioni  
 Come misura di compatibilità temporanea, gli amministratori possono inserire un flag di compatibilità nella sezione `<runtime>` del file di configurazione dell'applicazione.  In questo modo Common Language Runtime ripristinerà il comportamento previsto per le versioni 1.0 e 1.1.  
  
```  
<legacyUnhandledExceptionPolicy enabled="1"/>  
```  
  
## Override degli host  
 In .NET Framework versione 2.0 un host non gestito può utilizzare l'interfaccia [ICLRPolicyManager](../../../ocs/framework/unmanaged-api/hosting/iclrpolicymanager-interface.md) nell'API di hosting per eseguire l'override dei criteri predefiniti di Common Language Runtime relativi alle eccezioni non gestite.  Per l'impostazione dei criteri associati alle eccezioni non gestite viene utilizzata la funzione [ICLRPolicyManager::SetUnhandledExceptionPolicy](../Topic/ICLRPolicyManager::SetUnhandledExceptionPolicy%20Method.md).  
  
## Vedere anche  
 [Managed Threading Basics](../../../docs/standard/threading/managed-threading-basics.md)