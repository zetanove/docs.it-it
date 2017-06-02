---
title: "asynchronousThreadAbort MDA | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "asynchronous thread aborts"
  - "AsynchronousThreadAbort MDA"
  - "managed debugging assistants (MDAs), asynchronous thread aborts"
  - "threading [.NET Framework], managed debugging assistants"
  - "MDAs (managed debugging assistants), asynchronous thread aborts"
ms.assetid: 9ebe40b2-d703-421e-8660-984acc42bfe0
caps.latest.revision: 10
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 10
---
# asynchronousThreadAbort MDA
L'assistente al debug gestito `asynchronousThreadAbort` viene attivato quando un thread tenta di introdurre un'interruzione asincrona in un altro thread.  L'MDA `asynchronousThreadAbort` non viene invece attivato da interruzioni sincrone dei thread.  
  
## Sintomi  
 Si verifica l'arresto anomalo di un'applicazione con la generazione di una <xref:System.Threading.ThreadAbortException> non gestita quando viene interrotto il thread principale dell'applicazione.  Se l'esecuzione dell'applicazione dovesse continuare, le conseguenze potrebbero essere peggiori di un arresto anomalo. Si potrebbe infatti verificare un ulteriore danneggiamento dei dati.  
  
 Con molta probabilità operazioni che dovevano essere atomiche sono state interrotte dopo il completamento parziale, lasciando i dati dell'applicazione in uno stato imprevedibile.  È possibile che venga generata una <xref:System.Threading.ThreadAbortException> da punti apparentemente causali nell'esecuzione del codice che spesso coincidono con posizioni in cui non è prevista la generazione di un'eccezione.  Il codice può non essere in grado di gestire questo tipo di eccezioni e determinare in questo caso uno problema di danneggiamento.  
  
 I sintomi variano ampiamente a causa della casualità implicita nel problema.  
  
## Causa  
 Il codice presente in un thread ha chiamato il metodo <xref:System.Threading.Thread.Abort%2A?displayProperty=fullName> su un thread di destinazione per introdurre un'interruzione asincrona.  L'interruzione è asincrona perché il codice che effettua la chiamata a <xref:System.Threading.Thread.Abort%2A> è in esecuzione su un thread diverso da quello di destinazione dell'operazione di interruzione.  In genere, le interruzioni sincrone dei thread non causano problemi in quanto il thread che esegue il metodo <xref:System.Threading.Thread.Abort%2A> effettua tale operazione solo in un checkpoint sicuro in cui lo stato dell'applicazione è coerente.  
  
 Le interruzioni asincrone dei thread sono invece un problema in quanto vengono elaborate in punti imprevisti nell'esecuzione del thread di destinazione.  Per evitare ciò, il codice scritto per essere eseguito su un thread che potrebbe essere interrotto in questo modo deve gestire almeno una <xref:System.Threading.ThreadAbortException> per ogni riga, prestando attenzione a ripristinare lo stato di coerenza dei dati dell'applicazione.  Tuttavia, non è realistico prevedere la scrittura di codice tenendo presente questo problema o la protezione da tutti possibili rischi.  
  
 Le chiamate a codice non gestito e a blocchi `finally` non vengono interrotte in modo asincrono, ma all'uscita da una di queste categorie.  
  
 Può essere difficile stabilire la causa del problema per via della sua causalità implicita.  
  
## Risoluzione  
 Evitare la progettazione di codice che richieda l'uso di interruzioni asincrone dei thread.  Sono disponibili diversi approcci più adeguati per l'interruzione di un thread di destinazione che non richiedono una chiamata al metodo <xref:System.Threading.Thread.Abort%2A>.  L'approccio più sicuro consiste nell'introduzione di un meccanismo, ad esempio una proprietà comune, che segnali al thread di destinazione di richiedere un'interruzione.  Il thread di destinazione verificherà il segnale in determinati checkpoint sicuri  e, in caso di rilevamento di una richiesta di interruzione, potrà eseguire la chiusura correttamente.  
  
## Effetto sul runtime  
 Questo assistente al debug gestito non produce effetti su CLR.  Si limita a generare un report dei dati relativi alle interruzioni asincrone dei thread.  
  
## Output  
 L'assistente al debug gestito segnala l'ID del thread che esegue l'interruzione e l'ID del thread di destinazione dell'interruzione  che non coincideranno mai, in quanto l'utilizzo di questo assistente è limitato alle sole interruzioni asincrone.  
  
## Configurazione  
  
```  
<mdaConfig>  
  <assistants>  
    <asynchronousThreadAbort />  
  </assistants>  
</mdaConfig>  
```  
  
## Esempio  
 L'attivazione dell'assistente al debug gestito `asynchronousThreadAbort` richiede una sola chiamata al metodo <xref:System.Threading.Thread.Abort%2A> su un altro thread in esecuzione.  Considerare le conseguenze nel caso in cui il contenuto della funzione di avvio del thread corrispondesse a un insieme di operazioni più complesse che potrebbero essere interrotte in modo anomalo in un qualsiasi punto arbitrario.  
  
```  
using System.Threading;  
void FireMda()  
{  
    Thread t = new Thread(delegate() { Thread.Sleep(1000); });  
    t.Start();  
    // The following line activates the MDA.  
    t.Abort();   
    t.Join();  
}  
```  
  
## Vedere anche  
 <xref:System.Threading.Thread>   
 [Diagnosing Errors with Managed Debugging Assistants](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)