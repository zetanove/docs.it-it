---
title: "Timers | Microsoft Docs"
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
  - "threading [.NET Framework], timers"
  - "timers, about timers"
ms.assetid: 7091500d-be18-499b-a942-95366ce185e5
caps.latest.revision: 12
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 12
---
# Timers
I timer sono oggetti lightweight che consentono di specificare un delegato da chiamare a un intervallo di tempo specificato.  Un thread nel pool di thread esegue l'operazione di attesa.  
  
 L'utilizzo della classe <xref:System.Threading.Timer?displayProperty=fullName> è abbastanza semplice.  Si crea un **Timer**, che passa un delegato <xref:System.Threading.TimerCallback> al metodo di callback, un oggetto che rappresenta lo stato che verrà passato al callback, un tempo di generazione iniziale e un tempo che rappresenta il periodo tra le chiamate di callback.  Per annullare un timer in sospeso, chiamare la funzione **Timer.Dispose**.  
  
> [!NOTE]
>  Esistono altre due classi timer.  La classe <xref:System.Windows.Forms.Timer?displayProperty=fullName>, progettata per essere utilizzata in contesti di interfaccia utente, rappresenta un controllo che funziona con le finestre di progettazione visiva e genera eventi nel thread dell'interfaccia utente.  La classe <xref:System.Timers.Timer?displayProperty=fullName> deriva da <xref:System.ComponentModel.Component> e può quindi essere utilizzata con le finestre di progettazione visiva. Anche questa classe genera eventi, ma in un thread di <xref:System.Threading.ThreadPool>.  La classe <xref:System.Threading.Timer?displayProperty=fullName> crea i callback in un thread <xref:System.Threading.ThreadPool> e non utilizza il modello basato su eventi.  A differenza di altri timer, fornisce anche un oggetto di stato al metodo di callback.  Questa classe è totalmente lightweight.  
  
 Nell'esempio di codice riportato di seguito viene avviato un timer che inizia il conteggio dopo un secondo \(1.000 millisecondi\) e scatta ogni secondo finché non si preme **INVIO**.  La variabile in cui è contenuto il riferimento al timer è un campo a livello di classe, per evitare che il timer venga sottoposto a Garbage Collection mentre è ancora in esecuzione.  Per ulteriori informazioni sulla Garbage Collection aggressiva, vedere <xref:System.GC.KeepAlive%2A>.  
  
 [!code-cpp[System.Threading.Timer#2](../../../samples/snippets/cpp/VS_Snippets_CLR_System/system.Threading.Timer/CPP/source2.cpp#2)]
 [!code-csharp[System.Threading.Timer#2](../../../samples/snippets/csharp/VS_Snippets_CLR_System/system.Threading.Timer/CS/source2.cs#2)]
 [!code-vb[System.Threading.Timer#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR_System/system.Threading.Timer/VB/source2.vb#2)]  
  
## Vedere anche  
 <xref:System.Threading.Timer>   
 [Threading Objects and Features](../../../docs/standard/threading/threading-objects-and-features.md)