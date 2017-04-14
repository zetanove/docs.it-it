---
title: "streamWriterBufferedDataLost MDA | Microsoft Docs"
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
  - "StreamWriter class, data buffering problems"
  - "managed debugging assistants (MDAs), StreamWriter data buffering"
  - "buffers, StreamWriter problems"
  - "MDAs (managed debugging assistants), StreamWriter data buffering"
  - "StreamWriter buffered data lost"
  - "data buffering problems"
  - "streamWriterBufferedDataLost MDA"
ms.assetid: 6e5c07be-bc5b-437a-8398-8779e23126ab
caps.latest.revision: 8
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 8
---
# streamWriterBufferedDataLost MDA
L'assistente al debug gestito `streamWriterBufferedDataLost` viene attivato quando si scrive in un oggetto <xref:System.IO.StreamWriter> senza che venga successivamente chiamato il metodo <xref:System.IO.StreamWriter.Flush%2A> o <xref:System.IO.StreamWriter.Close%2A> prima dell'eliminazione dell'istanza di <xref:System.IO.StreamWriter>.  Se questo assistente al debug gestito è abilitato, Common Language Runtime determina se sono ancora presenti dati nel buffer di <xref:System.IO.StreamWriter>.  In caso affermativo, l'assistente al debug gestito viene attivato.  La chiamata ai metodi <xref:System.GC.Collect%2A> e <xref:System.GC.WaitForPendingFinalizers%2A> può imporre l'esecuzione dei finalizzatori.  In caso contrario, i finalizzatori verranno eseguiti in momenti apparentemente arbitrari ed è anche possibile che non vengano eseguiti affatto alla chiusura di un processo.  L'esecuzione esplicita dei finalizzatori mediante questo assistente al debug gestito consentirà di riprodurre in modo più affidabile questo tipo di problema.  
  
## Sintomi  
 Un oggetto <xref:System.IO.StreamWriter> non scrive gli ultimi 1\-4 KB di dati in un file.  
  
## Causa  
 <xref:System.IO.StreamWriter> memorizza i dati nel buffer interno, richiedendo quindi la chiamata al metodo <xref:System.IO.StreamWriter.Close%2A> o <xref:System.IO.StreamWriter.Flush%2A> per la scrittura dei dati del buffer nell'archivio dati sottostante.  Se il metodo <xref:System.IO.StreamWriter.Close%2A> o <xref:System.IO.StreamWriter.Flush%2A> non viene chiamato in modo appropriato, è possibile che i dati contenuti nel buffer dell'istanza di <xref:System.IO.StreamWriter> non vengano scritti nel modo previsto.  
  
 Di seguito è riportato un esempio di codice non corretto che dovrebbe essere rilevato da questo assistente al debug gestito.  
  
```  
// Poorly written code.  
void Write()   
{  
    StreamWriter sw = new StreamWriter("file.txt");  
    sw.WriteLine("Data");  
    // Problem: forgot to close the StreamWriter.  
}  
```  
  
 Il codice precedente attiverà questo assistente al debug gestito in modo più affidabile se la Garbage Collection viene avviata e quindi sospesa finché non termina l'esecuzione dei finalizzatori.  Per individuare questo tipo di problema, è possibile aggiungere il codice riportato di seguito alla fine del metodo precedente in una build di debug.  In questo modo l'assistente al debug gestito verrà attivato correttamente, ma non verrà ovviamente corretta la causa del problema.  
  
```  
GC.Collect();  
GC.WaitForPendingFinalizers();  
```  
  
## Risoluzione  
 Prima di chiudere un'applicazione o un blocco di codice contenente un'istanza di <xref:System.IO.StreamWriter>, assicurarsi di chiamare <xref:System.IO.StreamWriter.Close%2A> o <xref:System.IO.StreamWriter.Flush%2A> sull'oggetto <xref:System.IO.StreamWriter>.  Una delle migliori soluzioni consiste nel creare l'istanza con un blocco `using` di C\# \(`Using` in Visual Basic\), in modo da assicurare la chiamata al metodo <xref:System.IO.StreamWriter.Dispose%2A> per il writer e quindi la chiusura corretta dell'istanza.  
  
```  
using(StreamWriter sw = new StreamWriter("file.txt"))   
{  
    sw.WriteLine("Data");  
}  
```  
  
 Nel codice riportato di seguito viene illustrata la stessa soluzione, in questo caso utilizzando `try/finally` anziché `using`.  
  
```  
StreamWriter sw;  
try   
{  
    sw = new StreamWriter("file.txt"));  
    sw.WriteLine("Data");  
}  
finally   
{  
    if (sw != null)  
        sw.Close();  
}  
```  
  
 Se queste soluzioni non possono essere utilizzate, ad esempio quando un oggetto <xref:System.IO.StreamWriter> è memorizzato in una variabile statica e non è possibile eseguire facilmente il codice alla fine della durata della variabile, per evitare questo problema è possibile chiamare il metodo <xref:System.IO.StreamWriter.Flush%2A> sull'oggetto <xref:System.IO.StreamWriter> dopo l'ultimo utilizzo oppure impostare la proprietà <xref:System.IO.StreamWriter.AutoFlush%2A> su `true` prima del primo utilizzo.  
  
```  
private static StreamWriter log;  
// static class constructor.  
static WriteToFile()   
{  
    StreamWriter sw = new StreamWriter("log.txt");  
    sw.AutoFlush = true;  
  
    // Publish the StreamWriter for other threads.  
    log = sw;  
}  
```  
  
## Effetto sul runtime  
 Questo assistente al debug gestito non ha alcun effetto su Common Language Runtime \(CLR\).  
  
## Output  
 Un messaggio indicante che si è verificata questa violazione.  
  
## Configurazione  
  
```  
<mdaConfig>  
  <assistants>  
    <streamWriterBufferedDataLost />  
  </assistants>  
</mdaConfig>  
```  
  
## Vedere anche  
 <xref:System.IO.StreamWriter>   
 [Diagnosing Errors with Managed Debugging Assistants](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)