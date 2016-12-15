---
title: "Eventi (Guida per programmatori C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "classi [C#], eventi"
  - "C# (linguaggio), eventi"
  - "eventi [C#]"
ms.assetid: a8e51b22-d294-44fb-9539-0072f06c4cb3
caps.latest.revision: 43
caps.handback.revision: 43
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# Eventi (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Tramite gli eventi, una [classe](../../../csharp/language-reference/keywords/class.md) o un oggetto è in grado di segnalare ad altre classi o oggetti una situazione di interesse. La classe che invia \(o *genera*\) l'evento è chiamata *autore* e le classi che ricevono \(o *gestiscono*\) l'evento sono chiamate *sottoscrittori*.  
  
 In un'applicazione C\# Web o Windows Form tipica si sottoscrivono eventi generati da controlli quali pulsanti e caselle di riepilogo. È possibile usare l'ambiente di sviluppo integrato \(IDE\) di [!INCLUDE[csprcs](../../../csharp/includes/csprcs_md.md)] per cercare gli eventi pubblicati da un controllo e selezionare quelli che si vuole gestire. L'IDE aggiunge automaticamente un metodo vuoto del gestore eventi e il codice per sottoscrivere l'evento. Per altre informazioni, vedere [Procedura: eseguire e annullare la sottoscrizione a eventi](../../../csharp/programming-guide/events/how-to-subscribe-to-and-unsubscribe-from-events.md).  
  
## Cenni preliminari sugli eventi  
 Di seguito sono riportate le proprietà degli eventi:  
  
-   L'autore determina quando viene generato un evento. I sottoscrittori determinano quale azione viene eseguita in risposta all'evento.  
  
-   Un evento può avere più sottoscrittori. Un sottoscrittore può gestire più eventi da più autori.  
  
-   Gli eventi che non hanno sottoscrittore non vengono mai generati.  
  
-   Gli eventi vengono in genere usati per segnalare azioni dell'utente, ad esempio la scelta di un pulsante o di una voce di menu nell'interfaccia utente grafica.  
  
-   Quando un evento ha più sottoscrittori, i gestori eventi vengono richiamati in modo sincrono al momento della generazione dell'evento. Per richiamare gli eventi in modo asincrono, vedere [Calling Synchronous Methods Asynchronously](../Topic/Calling%20Synchronous%20Methods%20Asynchronously.md).  
  
-   Nella libreria di classi di [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] gli eventi sono basati sul delegato <xref:System.EventHandler> e sulla classe di base <xref:System.EventArgs>.  
  
## Sezioni correlate  
 Per altre informazioni, vedere:  
  
-   [Procedura: eseguire e annullare la sottoscrizione a eventi](../../../csharp/programming-guide/events/how-to-subscribe-to-and-unsubscribe-from-events.md)  
  
-   [Procedura: pubblicare eventi conformi alle linee guida di .NET Framework](../../../csharp/programming-guide/events/how-to-publish-events-that-conform-to-net-framework-guidelines.md)  
  
-   [Procedura: generare eventi di classe base nelle classi derivate](../../../csharp/programming-guide/events/how-to-raise-base-class-events-in-derived-classes.md)  
  
-   [Procedura: implementare eventi di interfaccia](../../../csharp/programming-guide/events/how-to-implement-interface-events.md)  
  
-   [Sincronizzazione di thread](../Topic/Thread%20Synchronization%20\(C%23%20and%20Visual%20Basic\).md)  
  
-   [Procedura: utilizzare un dizionario per archiviare istanze di evento](../../../csharp/programming-guide/events/how-to-use-a-dictionary-to-store-event-instances.md)  
  
-   [Procedura: implementare funzioni di accesso a eventi personalizzati](../../../csharp/programming-guide/events/how-to-implement-custom-event-accessors.md)  
  
## Specifiche del linguaggio C\#  
 [!INCLUDE[CSharplangspec](../../../csharp/language-reference/keywords/includes/csharplangspec_md.md)]  
  
## Capitoli del libro rappresentati  
 [Delegates, Events, and Lambda Expressions](http://go.microsoft.com/fwlink/?LinkId=195395) \(Delegati, eventi ed espressioni lambda\) in [C\# 3.0 Cookbook, Third Edition: More than 250 solutions for C\# 3.0 programmers](http://go.microsoft.com/fwlink/?LinkId=195369)  
  
 [Delegati ed eventi](http://go.microsoft.com/fwlink/?LinkId=195418) in [Learning C\# 3.0: Master the fundamentals of C\# 3.0](http://go.microsoft.com/fwlink/?LinkId=195412) \(Nozioni fondamentali su C\# 3.0\).  
  
## Vedere anche  
 <xref:System.EventHandler>   
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Delegati](../../../csharp/programming-guide/delegates/index.md)   
 [Creating Event Handlers in Windows Forms](../Topic/Creating%20Event%20Handlers%20in%20Windows%20Forms.md)   
 [Multithreaded Programming with the Event\-based Asynchronous Pattern](../Topic/Multithreaded%20Programming%20with%20the%20Event-based%20Asynchronous%20Pattern.md)