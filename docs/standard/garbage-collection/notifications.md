---
title: "Garbage Collection Notifications | Microsoft Docs"
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
  - "garbage collection, notifications"
ms.assetid: e12d8e74-31e3-4035-a87d-f3e66f0a9b89
caps.latest.revision: 23
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 23
---
# Garbage Collection Notifications
In alcune situazioni un'operazione completa di garbage collection \(che è una collection di seconda generazione\) eseguita da Common Language Runtime può influire negativamente sulle prestazioni.  Questo può rappresentare un problema in modo particolare con server che elaborano grandi volumi di richieste. In questo caso, un processo di Garbage Collection lungo può provocare un timeout delle richieste.  Per impedire che si verifichi un'operazione completa di Garbage Collection durante un periodo critico, è possibile ricevere una notifica quando questa operazione sta per essere eseguita e intraprendere quindi un'azione per reindirizzare il carico di lavoro a un'altra istanza del server.  È anche possibile forzare una raccolta, purché l'istanza del server corrente non richieda l'elaborazione di richieste.  
  
 Il metodo <xref:System.GC.RegisterForFullGCNotification%2A> esegue la registrazione per la generazione di una notifica quando il runtime riconosce che sta per verificarsi un'operazione completa di Garbage Collection.  Questa notifica è composta da due parti: quando sta per verificarsi l'operazione completa di Garbage Collection e quando tale operazione è stata completata.  
  
> [!WARNING]
>  Solo il blocco delle operazioni di garbage collection genera notifiche.  Quando l'elemento di configurazione [\<gcConcurrent\>](../../../docs/framework/configure-apps/file-schema/runtime/gcconcurrent-element.md) è abilitato, le operazioni di Garbage Collection in background non genereranno le notifiche.  
  
 Per determinare quando è stata generata una notifica, utilizzare i metodi <xref:System.GC.WaitForFullGCApproach%2A> e <xref:System.GC.WaitForFullGCComplete%2A>.  In genere, questi metodi vengono utilizzati in un ciclo `while` per ottenere continuamente un'enumerazione <xref:System.GCNotificationStatus> che mostra lo stato della notifica.  Se il valore è <xref:System.GCNotificationStatus>, è possibile effettuare le operazioni seguenti:  
  
-   In risposta a una notifica ottenuta con il metodo <xref:System.GC.WaitForFullGCApproach%2A>, è possibile reindirizzare il carico di lavoro e possibilmente forzare una raccolta.  
  
-   In risposta a una notifica ottenuta con il metodo <xref:System.GC.WaitForFullGCComplete%2A>, è possibile rendere disponibile l'istanza del server corrente per elaborare nuovamente le richieste.  È anche possibile raccogliere informazioni.  Ad esempio, è possibile utilizzare il metodo <xref:System.GC.CollectionCount%2A> per registrare il numero di raccolte.  
  
 I metodi <xref:System.GC.WaitForFullGCApproach%2A> e <xref:System.GC.WaitForFullGCComplete%2A> sono progettati per essere utilizzati insieme.  L'utilizzo di uno senza l'altro può produrre risultati imprevisti.  
  
## Operazione completa di Garbage Collection  
 Il runtime provoca un'operazione completa di Garbage Collection se si verifica uno degli scenari seguenti:  
  
-   Una quantità sufficiente di memoria passa nella generazione 2 per generare la successiva raccolta di generazione 2.  
  
-   Una quantità sufficiente di memoria passa nell'heap degli oggetti grandi per generare la successiva raccolta di generazione 2.  
  
-   Viene eseguita l'escalation di una raccolta di generazione 1 in una raccolta di generazione 2 a causa di altri fattori.  
  
 Le soglie specificate nel metodo <xref:System.GC.RegisterForFullGCNotification%2A> si applicano ai primi due scenari.  Tuttavia, nel primo scenario non si riceverà sempre la notifica nel momento proporzionale ai valori di soglia specificati, per due motivi:  
  
-   Il runtime non controlla ogni allocazione di oggetti piccoli \(per motivi di prestazioni\).  
  
-   Solo le raccolte di generazione 1 passano la memoria nella generazione 2.  
  
 Anche il terzo scenario contribuisce ad aumentare l'incertezza sul momento in cui si riceverà la notifica.  Anche se non è garantita, questa soluzione si dimostra utile per attenuare gli effetti di un'operazione completa di Garbage Collection inopportuna, reindirizzando le richieste durante questo periodo o forzando la raccolta in un momento più favorevole.  
  
## Parametri di soglia delle notifiche  
 Il metodo <xref:System.GC.RegisterForFullGCNotification%2A> include due parametri per specificare i valori di soglia degli oggetti di generazione 2 e dell'heap degli oggetti grandi.  Quando vengono raggiunti tali valori, dovrebbe essere generata una notifica di Garbage Collection.  Nella tabella seguente vengono descritti tali parametri.  
  
|Parametro|Descrizione|  
|---------------|-----------------|  
|`maxGenerationThreshold`|Numero compreso tra 1 e 99 che specifica quando generare la notifica in base agli oggetti passati alla generazione 2.|  
|`largeObjectHeapThreshold`|Numero compreso tra 1 e 99 che specifica quando generare la notifica in base agli oggetti allocati nell'heap degli oggetti grandi.|  
  
 Se si specifica un valore troppo alto, esiste un'elevata probabilità che si riceverà una notifica, ma il periodo di attesa potrebbe essere eccessivamente lungo prima che il runtime provochi una raccolta.  Se si forza una raccolta, è possibile che venga recuperato un numero di oggetti maggiore rispetto a quelli che verrebbero recuperati se la raccolta viene provocata dal runtime.  
  
 Se si specifica un valore eccessivamente basso, il runtime può provocare la raccolta prima che sia trascorso un periodo di tempo sufficiente per ricevere una notifica.  
  
## Esempio  
  
### Descrizione  
 Nell'esempio seguente un gruppo di server gestisce le richieste Web in ingresso.  Per simulare il carico di lavoro dell'elaborazione delle richieste, vengono aggiunte matrici di byte a una raccolta <xref:System.Collections.Generic.List%601>.  Ogni server esegue la registrazione per una notifica di Garbage Collection, quindi avvia un thread sul metodo utente `WaitForFullGCProc` per controllare continuamente l'enumerazione <xref:System.GCNotificationStatus> restituita dai metodi <xref:System.GC.WaitForFullGCApproach%2A> e <xref:System.GC.WaitForFullGCComplete%2A>.  
  
 I metodi <xref:System.GC.WaitForFullGCApproach%2A> e <xref:System.GC.WaitForFullGCComplete%2A> chiamano i rispettivi metodi utente di gestione eventi quando viene generata una notifica:  
  
-   `OnFullGCApproachNotify`  
  
     Questo metodo chiama il metodo utente `RedirectRequests` che indica al server di accodamento delle richieste di sospendere l'invio di richieste al server.  Questa situazione viene simulata impostando la variabile a livello di classe `bAllocate` su `false` in modo che non vengano più allocati oggetti.  
  
     Quindi, viene chiamato il metodo utente `FinishExistingRequests` per completare l'elaborazione delle richieste in sospeso al server.  Questa situazione viene simulata cancellando la raccolta <xref:System.Collections.Generic.List%601>.  
  
     Infine, viene forzata un'operazione di Garbage Collection perché il carico di lavoro è ridotto.  
  
-   `OnFullGCCompleteNotify`  
  
     Questo metodo chiama il metodo utente `AcceptRequests` per riprendere ad accettare richieste, perché il server non è più soggetto a un'operazione completa di Garbage Collection.  Questa azione viene simulata impostando la variabile `bAllocate` su `true` in modo che gli oggetti possano riprendere a essere aggiunti alla raccolta <xref:System.Collections.Generic.List%601>.  
  
 Il codice seguente contiene il metodo `Main` dell'esempio.  
  
 [!code-cpp[GCNotification#2](../../../samples/snippets/cpp/VS_Snippets_CLR/GCNotification/cpp/program.cpp#2)]
 [!code-csharp[GCNotification#2](../../../samples/snippets/csharp/VS_Snippets_CLR/GCNotification/cs/Program.cs#2)]
 [!code-vb[GCNotification#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GCNotification/vb/program.vb#2)]  
  
 Il codice seguente contiene il metodo utente `WaitForFullGCProc`, che contiene un ciclo while continuo per le notifiche di Garbage Collection.  
  
 [!code-cpp[GCNotification#8](../../../samples/snippets/cpp/VS_Snippets_CLR/GCNotification/cpp/program.cpp#8)]
 [!code-csharp[GCNotification#8](../../../samples/snippets/csharp/VS_Snippets_CLR/GCNotification/cs/Program.cs#8)]
 [!code-vb[GCNotification#8](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GCNotification/vb/program.vb#8)]  
  
 Il codice seguente contiene il metodo `OnFullGCApproachNotify` chiamato dal  
  
 metodo `WaitForFullGCProc`.  
  
 [!code-cpp[GCNotification#5](../../../samples/snippets/cpp/VS_Snippets_CLR/GCNotification/cpp/program.cpp#5)]
 [!code-csharp[GCNotification#5](../../../samples/snippets/csharp/VS_Snippets_CLR/GCNotification/cs/Program.cs#5)]
 [!code-vb[GCNotification#5](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GCNotification/vb/program.vb#5)]  
  
 Il codice seguente contiene il metodo `OnFullGCApproachComplete` chiamato dal  
  
 metodo `WaitForFullGCProc`.  
  
 [!code-cpp[GCNotification#6](../../../samples/snippets/cpp/VS_Snippets_CLR/GCNotification/cpp/program.cpp#6)]
 [!code-csharp[GCNotification#6](../../../samples/snippets/csharp/VS_Snippets_CLR/GCNotification/cs/Program.cs#6)]
 [!code-vb[GCNotification#6](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GCNotification/vb/program.vb#6)]  
  
 Il codice seguente contiene i metodi utente chiamati dai metodi `OnFullGCApproachNotify` e `OnFullGCCompleteNotify`.  I metodi utente reindirizzano le richieste, completano le richieste esistenti, quindi riprendono le richieste dopo che si è verificata un'operazione completa di Garbage Collection.  
  
 [!code-cpp[GCNotification#9](../../../samples/snippets/cpp/VS_Snippets_CLR/GCNotification/cpp/program.cpp#9)]
 [!code-csharp[GCNotification#9](../../../samples/snippets/csharp/VS_Snippets_CLR/GCNotification/cs/Program.cs#9)]
 [!code-vb[GCNotification#9](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GCNotification/vb/program.vb#9)]  
  
 L'esempio di codice completo è riportato di seguito:  
  
 [!code-cpp[GCNotification#1](../../../samples/snippets/cpp/VS_Snippets_CLR/GCNotification/cpp/program.cpp#1)]
 [!code-csharp[GCNotification#1](../../../samples/snippets/csharp/VS_Snippets_CLR/GCNotification/cs/Program.cs#1)]
 [!code-vb[GCNotification#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/GCNotification/vb/program.vb#1)]  
  
## Vedere anche  
 [Garbage Collection](../../../docs/standard/garbage-collection/index.md)