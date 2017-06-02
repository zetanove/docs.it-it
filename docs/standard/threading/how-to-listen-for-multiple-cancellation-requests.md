---
title: "How to: Listen for Multiple Cancellation Requests | Microsoft Docs"
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
  - "cancellation tokens, joining"
  - "LinkedTokenSource, how to"
ms.assetid: 6f4f3804-2ed7-41b4-a97a-6e32b93f6e05
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# How to: Listen for Multiple Cancellation Requests
In questo esempio viene illustrato come mettersi in ascolto di due token di annullamento contemporaneamente, in modo che sia possibile annullare un'operazione se uno dei token lo richiede.  
  
> [!NOTE]
>  Quando viene abilitato "Just My Code", in alcuni casi Visual Studio si interromperà in corrispondenza della riga che genera l'eccezione e in cui viene visualizzato un messaggio di errore che indica che l'eccezione non è gestita dal codice utente. Questo errore è benigno.  È possibile premere F5 per continuare e visualizzare il comportamento di gestione delle eccezioni illustrato negli esempi riportati di seguito.  Per impedire l'interruzione di Visual Studio al primo errore, deselezionare semplicemente la casella di controllo "Just My Code" in **Strumenti, Opzioni, Debug, Generale**.  
  
## Esempio  
 Nell'esempio seguente viene utilizzato il metodo <xref:System.Threading.CancellationTokenSource.CreateLinkedTokenSource%2A> per unire due token in un unico token.  In questo modo, è possibile passare il token ai metodi che accettano un solo token di annullamento come argomento.  Nell'esempio viene illustrato un scenario comune in cui un metodo deve osservare sia un token passato dall'esterno della classe che un token generato all'interno della classe.  
  
 [!code-csharp[Cancellation#13](../../../samples/snippets/csharp/VS_Snippets_Misc/cancellation/cs/cancellationex13.cs#13)]
 [!code-vb[Cancellation#13](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cancellation/vb/cancellationex13.vb#13)]  
  
 Quando il token collegato genera un evento <xref:System.OperationCanceledException>, il token passato all'eccezione è il token collegato, non uno dei token del predecessore.  Per determinare quale dei token è stato annullato, controllare direttamente lo stato dei token del predecessore.  
  
 In questo esempio, l'eccezione <xref:System.AggregateException> non deve essere mai generata. Tuttavia tale eccezione viene intercettata in questo punto perché, negli scenari reali, per qualsiasi altra eccezione diversa da <xref:System.OperationCanceledException> generata dal delegato dell'attività viene eseguito il wrapping in un'eccezione <xref:System.OperationCanceledException>.  
  
## Vedere anche  
 [Cancellation in Managed Threads](../../../docs/standard/threading/cancellation-in-managed-threads.md)