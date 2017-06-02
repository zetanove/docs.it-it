---
title: "How to: Use SpinWait to Implement a Two-Phase Wait Operation | Microsoft Docs"
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
  - "SpinWait, how to synchronize two-phase wait"
ms.assetid: b2ac4e4a-051a-4f65-b4b9-f8e103aff195
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# How to: Use SpinWait to Implement a Two-Phase Wait Operation
Nell'esempio seguente viene illustrato come utilizzare un oggetto <xref:System.Threading.SpinWait?displayProperty=fullName> per implementare un'operazione di attesa a due fasi.  Nella prima fase l'oggetto di sincronizzazione, un oggetto `Latch`, esegue uno spin per alcuni cicli mentre verifica la disponibilità del blocco.  Nella seconda fase, se il blocco diventa disponibile, il metodo `Wait` viene restituito senza utilizzare <xref:System.Threading.ManualResetEvent?displayProperty=fullName> per eseguirne l'attesa; in caso contrario, `Wait` esegue l'attesa.  
  
## Esempio  
 In questo esempio viene illustrata un'implementazione molto semplice di una primitiva di sincronizzazione latch.  È possibile utilizzare questa struttura dei dati quando si prevedono tempi di attesa molto brevi.  Questo esempio viene riportato a scopo puramente dimostrativo.  Se è necessaria una funzionalità di tipo latch nel programma, considerare l'utilizzo di <xref:System.Threading.ManualResetEventSlim?displayProperty=fullName>.  
  
 [!code-csharp[CDS_SpinWait#03](../../../samples/snippets/csharp/VS_Snippets_Misc/cds_spinwait/cs/spinwait03.cs#03)]
 [!code-vb[CDS_SpinWait#03](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cds_spinwait/vb/spinwait2.vb#03)]  
  
 Il latch utilizza l'oggetto <xref:System.Threading.SpinWait> per eseguire uno spin sul posto soltanto finché la chiamata successiva a `SpinOnce` non fa sì che <xref:System.Threading.SpinWait> restituisca la porzione di tempo del thread.  A quel punto, il latch provoca il proprio cambio di contesto chiamando <xref:System.Threading.WaitHandle.WaitOne%2A> su <xref:System.Threading.ManualResetEvent> e passando la parte restante del valore di timeout.  
  
 L'output di registrazione mostra la frequenza con cui il latch è stato in grado di aumentare le prestazioni acquisendo il blocco senza utilizzare <xref:System.Threading.ManualResetEvent>.  
  
## Vedere anche  
 [SpinWait](../../../docs/standard/threading/spinwait.md)   
 [Threading Objects and Features](../../../docs/standard/threading/threading-objects-and-features.md)