---
title: "Destroying Threads | Microsoft Docs"
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
  - "destroying threads"
  - "threading [.NET Framework], destroying threads"
ms.assetid: df54e648-c5d1-47c9-bd29-8e4438c1db6d
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# Destroying Threads
Il metodo <xref:System.Threading.Thread.Abort%2A> viene utilizzato per interrompere definitivamente un thread gestito.  Quando si chiama <xref:System.Threading.Thread.Abort%2A>, Common Language Runtime genera un'eccezione <xref:System.Threading.ThreadAbortException> nel thread di destinazione, che può intercettare l'eccezione.  Per ulteriori informazioni, vedere <xref:System.Threading.Thread.Abort%2A?displayProperty=fullName>.  
  
> [!NOTE]
>  Se un thread sta eseguendo codice non gestito al momento della chiamata al relativo metodo <xref:System.Threading.Thread.Abort%2A>, Common Language Runtime contrassegna il thread come <xref:System.Threading.ThreadState?displayProperty=fullName>.  L'eccezione viene generata quando il thread restituisce il controllo al codice gestito.  
  
 I thread terminati non possono essere riavviati.  
  
 Il metodo <xref:System.Threading.Thread.Abort%2A> non provoca l'interruzione immediata del thread perché il thread di destinazione può intercettare l'eccezione <xref:System.Threading.ThreadAbortException> ed eseguire quantità arbitrarie di codice in un blocco `finally`.  Se necessario, è possibile rimanere in attesa finché il thread non termina chiamando <xref:System.Threading.Thread.Join%2A?displayProperty=fullName>.  <xref:System.Threading.Thread.Join%2A?displayProperty=fullName> rappresenta una chiamata di blocco che non restituisce il controllo prima che il thread abbia effettivamente interrotto l'esecuzione o sia trascorso un intervallo di timeout facoltativo.  Poiché il thread interrotto può chiamare il metodo <xref:System.Threading.Thread.ResetAbort%2A> o procedere con un'elaborazione illimitata in un blocco `finally`, non è possibile garantire che l'attesa termini senza specificare un timeout.  
  
 I thread in attesa su una chiamata al metodo <xref:System.Threading.Thread.Join%2A?displayProperty=fullName> possono essere interrotti da altri thread che chiamano <xref:System.Threading.Thread.Interrupt%2A?displayProperty=fullName>.  
  
## Gestione di ThreadAbortException  
 Se si prevede che il thread verrà interrotto per effetto di una chiamata a <xref:System.Threading.Thread.Abort%2A> dal codice o a causa dello scaricamento di un dominio applicazione in cui il thread è in esecuzione \(<xref:System.AppDomain.Unload%2A?displayProperty=fullName> utilizza <xref:System.Threading.Thread.Abort%2A?displayProperty=fullName> per interrompere i thread\), è necessario che il thread gestisca l'eccezione <xref:System.Threading.ThreadAbortException> ed esegua tutta l'elaborazione finale in una clausola `finally`, come illustrato nel codice riportato di seguito.  
  
```vb  
Try  
    ' Code that is executing when the thread is aborted.  
Catch ex As ThreadAbortException  
    ' Clean-up code can go here.  
    ' If there is no Finally clause, ThreadAbortException is  
    ' re-thrown by the system at the end of the Catch clause.   
Finally  
    ' Clean-up code can go here.  
End Try  
' Do not put clean-up code here, because the exception   
' is rethrown at the end of the Finally clause.  
```  
  
```csharp  
try   
{  
    // Code that is executing when the thread is aborted.  
}   
catch (ThreadAbortException ex)   
{  
    // Clean-up code can go here.  
    // If there is no Finally clause, ThreadAbortException is  
    // re-thrown by the system at the end of the Catch clause.   
}  
// Do not put clean-up code here, because the exception   
// is rethrown at the end of the Finally clause.  
```  
  
 Il codice di pulitura deve essere incluso nella clausola `catch` o `finally`, perché, se non esiste alcuna clausola `finally`, il sistema genera nuovamente un'eccezione <xref:System.Threading.ThreadAbortException> alla fine della clausola `finally` o `catch`.  
  
 È possibile impedire al sistema di rigenerare l'eccezione chiamando il metodo <xref:System.Threading.Thread.ResetAbort%2A?displayProperty=fullName>.  Tuttavia, questa operazione deve essere eseguita solo se la generazione di <xref:System.Threading.ThreadAbortException> è dovuta al codice.  
  
## Vedere anche  
 <xref:System.Threading.ThreadAbortException>   
 <xref:System.Threading.Thread>   
 [Using Threads and Threading](../../../docs/standard/threading/using-threads-and-threading.md)