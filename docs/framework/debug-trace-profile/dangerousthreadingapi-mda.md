---
title: "dangerousThreadingAPI MDA | Microsoft Docs"
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
  - "suspending threads"
  - "DangerousThreadingAPI MDA"
  - "managed debugging assistants (MDAs), dangerous threading operations"
  - "threading [.NET Framework], suspending"
  - "MDAs (managed debugging assistants), dangerous threading operations"
  - "Suspend method"
  - "threading [.NET Framework], managed debugging assistants"
ms.assetid: 3e5efbc5-92e4-4229-b31f-ce368a1adb96
caps.latest.revision: 10
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 10
---
# dangerousThreadingAPI MDA
L'assistente al debug gestito `dangerousThreadingAPI` viene attivato quando il metodo <xref:System.Threading.Thread.Suspend%2A?displayProperty=fullName> viene chiamato su un thread diverso da quello attuale.  
  
## Sintomi  
 Un'applicazione non risponde o si blocca in modo indefinito.  È possibile che i dati del sistema e dell'applicazione vengano lasciati in uno stato imprevedibile temporaneamente o anche dopo la chiusura dell'applicazione.  Alcune operazioni non vengono eseguite come previsto.  
  
 I sintomi variano ampiamente a causa della casualità implicita nel problema.  
  
## Causa  
 Un thread viene sospeso in modo asincrono da un altro thread mediante il metodo <xref:System.Threading.Thread.Suspend%2A>.  Non esiste modo di stabilire quando sia sicuro sospendere un altro thread mentre è in corso qualche relativa operazione.  La sospensione del thread può determinare il danneggiamento dei dati o l'interruzione della lingua invariabile.  Qualora un thread dovesse essere inserito in uno stato di sospensione e mai ripreso mediante il metodo <xref:System.Threading.Thread.Resume%2A>, è possibile che l'applicazione si blocchi in modo indefinito e che i relativi dati vengano danneggiati.  Questi metodi sono stati contrassegnati come obsoleti.  
  
 Se le primitive di sincronizzazione sono contenute nel thread di destinazione, rimarranno in tale posizione durante la sospensione  causando probabilmente deadlock se un altro thread, ad esempio quello che esegue il metodo <xref:System.Threading.Thread.Suspend%2A>, tenta di acquisire un blocco sulla primitiva.  In questa situazione il problema stesso si manifesta come deadlock.  
  
## Risoluzione  
 Evitare progettazioni in cui sia richiesto l'utilizzo di <xref:System.Threading.Thread.Suspend%2A> e <xref:System.Threading.Thread.Resume%2A>.  Per l'interazione tra thread, utilizzare le primitive di sincronizzazione, quali <xref:System.Threading.Monitor>, <xref:System.Threading.ReaderWriterLock>, <xref:System.Threading.Mutex> o l'istruzione C\# `lock`.  Se è necessario utilizzare questi metodi, ridurre il periodo di tempo e la quantità di codice eseguito quando il thread si trova in uno stato di sospensione.  
  
## Effetto sul runtime  
 Questo assistente al debug gestito non produce effetti su CLR.  Si limita a generare un report dei dati relativi alle operazioni di threading dannose.  
  
## Output  
 L'assistente al debug gestito identifica il metodo threading dannoso che ne ha provocato l'attivazione.  
  
## Configurazione  
  
```  
<mdaConfig>  
  <assistants>  
    <dangerousThreadingAPI />  
  </assistants>  
</mdaConfig>  
```  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene illustrata una chiamata al metodo <xref:System.Threading.Thread.Suspend%2A> che causa l'attivazione di `dangerousThreadingAPI`.  
  
```  
using System.Threading;  
void FireMda()  
{  
    Thread t = new Thread(delegate() { Thread.Sleep(1000); });  
    t.Start();  
    // The following line activates the MDA.  
    t.Suspend();   
    t.Resume();  
    t.Join();  
}  
```  
  
## Vedere anche  
 <xref:System.Threading.Thread>   
 [Diagnosing Errors with Managed Debugging Assistants](../../../docs/framework/debug-trace-profile/diagnosing-errors-with-managed-debugging-assistants.md)   
 [Istruzione lock](../Topic/lock%20Statement%20\(C%23%20Reference\).md)