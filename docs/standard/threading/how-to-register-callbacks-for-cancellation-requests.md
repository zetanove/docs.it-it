---
title: "How to: Register Callbacks for Cancellation Requests | Microsoft Docs"
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
  - "cancellation, how to register callbacks"
ms.assetid: 8838dd75-18ed-4b8b-b322-cd4531faac64
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# How to: Register Callbacks for Cancellation Requests
L'esempio seguente mostra come registrare un delegato che verrà richiamato quando una proprietà <xref:System.Threading.CancellationToken.IsCancellationRequested%2A> diventerà true in seguito a una chiamata a <xref:System.Threading.CancellationTokenSource.Cancel%2A> sull'oggetto che ha creato il token.  Usare questa tecnica per annullare le operazioni asincrone che non supportano in modo nativo il framework di annullamento unificato e per sbloccare i metodi che potrebbero essere in attesa del completamento di un'operazione asincrona.  
  
> [!NOTE]
>  Quando "Just My Code" è abilitato, Visual Studio in alcuni casi si interromperà in corrispondenza della riga che genera l'eccezione e visualizzerà un messaggio di errore simile a "Eccezione non gestita dal codice utente". Questo errore non è grave.  È possibile premere F5 per continuare e osservare il comportamento di gestione delle eccezioni illustrato negli esempi seguenti.  Per impedire l'interruzione di Visual Studio al primo errore, deselezionare semplicemente la casella di controllo "Just My Code" in **Strumenti, Opzioni, Debug, Generale**.  
  
## Esempio  
 Nell'esempio seguente, il metodo <xref:System.Net.WebClient.CancelAsync%2A> viene registrato come metodo da richiamare quando viene richiesto l'annullamento tramite il token di annullamento.  
  
 [!code-csharp[Conceptual.Cancellation.Callback#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.cancellation.callback/cs/howtoexample1.cs#1)]
 [!code-vb[Conceptual.Cancellation.Callback#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.cancellation.callback/vb/howtoexample1.vb#1)]  
  
 Se l'annullamento è già stato richiesto quando il callback viene registrato, è tuttavia garantito che il callback verrà chiamato.  In questo caso particolare, il metodo <xref:System.Net.WebClient.CancelAsync%2A> non eseguirà alcuna operazione se nessuna operazione asincrona è in corso, quindi la chiamata al metodo è sempre sicura.  
  
## Vedere anche  
 [Cancellation in Managed Threads](../../../docs/standard/threading/cancellation-in-managed-threads.md)