---
title: "How to: Implement a Client of the Event-based Asynchronous Pattern | Microsoft Docs"
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
  - "Event-based Asynchronous Pattern"
  - "ProgressChangedEventArgs class"
  - "BackgroundWorker component"
  - "events [.NET Framework], asynchronous"
  - "Asynchronous Pattern"
  - "AsyncOperationManager class"
  - "threading [.NET Framework], asynchronous features"
  - "components [.NET Framework], asynchronous"
  - "AsyncOperation class"
  - "threading [Windows Forms], asynchronous features"
  - "AsyncCompletedEventArgs class"
ms.assetid: 21a858c1-3c99-4904-86ee-0d17b49804fa
caps.latest.revision: 11
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 11
---
# How to: Implement a Client of the Event-based Asynchronous Pattern
Nell'esempio di codice riportato di seguito viene illustrato come utilizzare un componente conforme a [Event\-based Asynchronous Pattern Overview](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-overview.md).  Per il form relativo a questo esempio viene utilizzato il componente `PrimeNumberCalculator` descritto in [How to: Implement a Component That Supports the Event\-based Asynchronous Pattern](../../../docs/standard/asynchronous-programming-patterns/component-that-supports-the-event-based-asynchronous-pattern.md).  
  
 Quando viene eseguito un progetto in cui viene utilizzato questo esempio, verrà visualizzato un form intitolato "Prime Number Calculator" provvisto di griglia e di due pulsanti, **Start New Task** e **Cancel**.  È possibile fare clic sul pulsante **Start New Task** diverse volte in successione. Per ogni clic, un'operazione asincrona avvierà un calcolo per determinare se un numero sottoposto a test generato casualmente è un numero primo.  Nel form verranno periodicamente visualizzati lo stato di avanzamento e i risultati incrementali.  A ogni operazione viene assegnato un ID attività univoco.  Il risultato del calcolo viene visualizzato nella colonna **Result**. Se il numero sottoposto a test non è un numero primo, verrà assegnata l'etichetta **Composite** e verrà visualizzato il relativo primo divisore.  
  
 Le operazioni in sospeso possono essere annullate con il pulsante **Cancel**.  È possibile effettuare più selezioni.  
  
> [!NOTE]
>  La maggior parte dei numeri non risulterà numero primo.  Se, dopo l'esecuzione di diverse operazioni non è stato trovato un numero primo, avviare altre attività in seguito alle quali la ricerca potrebbe avere esito positivo.  
  
## Esempio  
 [!code-csharp[System.ComponentModel.AsyncOperationManager#10](../../../samples/snippets/csharp/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/CS/primenumbercalculatormain.cs#10)]
 [!code-vb[System.ComponentModel.AsyncOperationManager#10](../../../samples/snippets/visualbasic/VS_Snippets_Winforms/System.ComponentModel.AsyncOperationManager/VB/primenumbercalculatormain.vb#10)]  
  
## Vedere anche  
 <xref:System.ComponentModel.AsyncOperation>   
 <xref:System.ComponentModel.AsyncOperationManager>   
 <xref:System.Windows.Forms.WindowsFormsSynchronizationContext>