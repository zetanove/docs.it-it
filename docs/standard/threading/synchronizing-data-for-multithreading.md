---
title: "Synchronizing Data for Multithreading | Microsoft Docs"
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
  - "synchronization, threads"
  - "threading [.NET Framework], synchronizing threads"
  - "managed threading"
ms.assetid: b980eb4c-71d5-4860-864a-6dfe3692430a
caps.latest.revision: 16
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 16
---
# Synchronizing Data for Multithreading
Quando più thread consentono di effettuare chiamate alle proprietà e ai metodi di un singolo oggetto, è indispensabile che tali chiamate siano sincronizzate.  In caso contrario, un thread potrebbe interrompere le operazioni di un altro thread e lo stato dell'oggetto potrebbe risultare non valido.  Una classe i cui membri sono protetti da tali interruzioni è detta thread\-safe.  
  
 Common Language Infrastructure offre diverse strategie per sincronizzare l'accesso a membri di istanza e statici:  
  
-   Aree del codice sincronizzate.  È possibile utilizzare la classe <xref:System.Threading.Monitor> o il supporto del compilatore per questa classe per sincronizzare solo il blocco di codice necessario, migliorando le prestazioni.  
  
-   Sincronizzazione manuale.  È possibile utilizzare gli oggetti di sincronizzazione forniti dalla libreria delle classi .NET.  Per informazioni, vedere [Overview of Synchronization Primitives](../../../docs/standard/threading/overview-of-synchronization-primitives.md), in cui è inclusa una descrizione della classe <xref:System.Threading.Monitor>.  
  
-   Contesti sincronizzati.  È possibile utilizzare la classe <xref:System.Runtime.Remoting.Contexts.SynchronizationAttribute> per attivare la sincronizzazione semplice e automatica per gli oggetti <xref:System.ContextBoundObject>.  
  
-   Classi Collection nello spazio dei nomi <xref:System.Collections.Concurrent?displayProperty=fullName>.  Queste classi forniscono operazioni di aggiunta e rimozione sincronizzate incorporate.  Per ulteriori informazioni, vedere [Raccolte thread\-safe](../../../docs/standard/collections/thread-safe/index.md).  
  
 Common Language Runtime fornisce un modello di thread in cui le classi rientrano in diverse categorie che è possibile sincronizzare in vari modi a seconda dei requisiti.  Nella tabella che segue viene indicato il tipo di supporto alla sincronizzazione fornito per campi e metodi con una determinata categoria di sincronizzazione.  
  
|Categoria|Campi globali|Campi statici|Metodi statici|Campi di istanza|Metodi di istanza|Blocchi di codice specifici|  
|---------------|-------------------|-------------------|--------------------|----------------------|-----------------------|---------------------------------|  
|Nessuna sincronizzazione|No|No|No|No|No|No|  
|Contesto di sincronizzazione|No|No|No|Sì|Sì|No|  
|Aree del codice sincronizzate|No|No|Solo se contrassegnato|No|Solo se contrassegnato|Solo se contrassegnato|  
|Sincronizzazione manuale|Manual|Manual|Manual|Manual|Manual|Manual|  
  
## Nessuna sincronizzazione  
 Si tratta dell'impostazione predefinita per gli oggetti.  Ogni thread può accedere a qualsiasi metodo o campo in qualsiasi momento.  Solo un thread alla volta deve poter accedere a questi oggetti.  
  
## Sincronizzazione manuale  
 La libreria delle classi .NET Framework fornisce una serie di classi per la sincronizzazione dei thread.  Per informazioni al riguardo, vedere [Overview of Synchronization Primitives](../../../docs/standard/threading/overview-of-synchronization-primitives.md).  
  
## Aree del codice sincronizzate  
 È possibile utilizzare la classe <xref:System.Threading.Monitor> o una parola chiave del compilatore per sincronizzare blocchi di codice, metodi di istanza e metodi statici.  Non è disponibile alcun supporto per i campi statici sincronizzati.  
  
 Sia con Visual Basic che con C\# è possibile contrassegnare blocchi di codice con una particolare parola chiave del linguaggio, l'istruzione `lock` in C\# o `SyncLock` in Visual Basic.  Quando il codice viene eseguito da un thread, viene effettuato un tentativo di acquisire il blocco.  Se il blocco è già stato acquisito da un altro thread, il thread corrente si blocca finché il blocco non diventa disponibile.  Quando il thread esce dal blocco di codice sincronizzato, il blocco viene rilasciato, indipendentemente dalla modalità di uscita del thread dal blocco di codice.  
  
> [!NOTE]
>  Le istruzioni `lock` e `SyncLock` vengono implementate tramite <xref:System.Threading.Monitor.Enter%2A?displayProperty=fullName> e <xref:System.Threading.Monitor.Exit%2A?displayProperty=fullName>, pertanto è possibile utilizzare insieme altri metodi di <xref:System.Threading.Monitor> all'interno dell'area sincronizzata.  
  
 È anche possibile decorare un metodo con **MethodImplAttribute** e **MethodImplOptions.Synchronized**, in modo da avere lo stesso effetto di quando si utilizza **Monitor** o una delle parole chiave del compilatore per bloccare l'intero corpo del metodo.  
  
 <xref:System.Threading.Thread.Interrupt%2A?displayProperty=fullName> può essere utilizzato per interrompere le operazioni di blocco di un thread, quali l'attesa di accesso a un'area sincronizzata di codice.  **Thread.Interrupt** viene utilizzato anche per interrompere operazioni del thread quali <xref:System.Threading.Thread.Sleep%2A?displayProperty=fullName>.  
  
> [!IMPORTANT]
>  Non bloccare il tipo, ovvero `typeof(MyType)` in C\#, `GetType(MyType)` in Visual Basic o `MyType::typeid` in C\+\+, per proteggere i metodi `static` \(i metodi `Shared` in Visual Basic\).  Utilizzare invece un oggetto statico privato.  Analogamente, non utilizzare `this` in C\# \(`Me` in Visual Basic\) per bloccare i metodi di istanza.  Utilizzare invece un oggetto privato.  Una classe o istanza può venire bloccata da codice diverso da quello che si sta sviluppando, con conseguenti possibili deadlock o problemi di prestazioni.  
  
### Supporto del compilatore  
 Sia Visual Basic che C\# supportano una parola chiave del linguaggio che utilizza <xref:System.Threading.Monitor.Enter%2A?displayProperty=fullName> e <xref:System.Threading.Monitor.Exit%2A?displayProperty=fullName> per bloccare l'oggetto.  Visual Basic supporta l'istruzione [SyncLock](../../../ocs/visual-basic/language-reference/statements/synclock-statement.md), mentre C\# supporta l'istruzione [lock](../Topic/lock%20Statement%20\(C%23%20Reference\).md).  
  
 In entrambi i casi, se viene generata un'eccezione nel blocco di codice, il blocco acquisito da **lock** o da **SyncLock** viene rilasciato automaticamente.  I compilatori C\# e Visual Basic creano un costrutto **try**\/**finally** con **Monitor.Enter** all'inizio e **Monitor.Exit** nel costrutto **finally**.  Se un'eccezione viene generata all'interno del blocco **lock** o **SyncLock**, il gestore **finally** viene eseguito per consentire l'esecuzione di eventuale lavoro di pulizia.  
  
## Contesto di sincronizzazione  
 È possibile utilizzare **SynchronizationAttribute** su qualsiasi **ContextBoundObject** per sincronizzare tutti i metodi e i campi di istanza.  Tutti gli oggetti nello stesso dominio del contesto condividono lo stesso blocco.  I thread multipli possono accedere a metodi e campi, ma è consentito solo ad un singolo thread alla volta.  
  
## Vedere anche  
 <xref:System.Runtime.Remoting.Contexts.SynchronizationAttribute>   
 [Threads and Threading](../../../docs/standard/threading/threads-and-threading.md)   
 [Overview of Synchronization Primitives](../../../docs/standard/threading/overview-of-synchronization-primitives.md)   
 [SyncLock Statement](../../../ocs/visual-basic/language-reference/statements/synclock-statement.md)   
 [Istruzione lock](../Topic/lock%20Statement%20\(C%23%20Reference\).md)