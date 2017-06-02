---
title: "How to: Listen for Cancellation Requests That Have Wait Handles | Microsoft Docs"
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
  - "cancellation, waiting with wait handles"
ms.assetid: 6e2aa49b-fc84-4bcf-962b-17db98b7edcb
caps.latest.revision: 9
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 9
---
# How to: Listen for Cancellation Requests That Have Wait Handles
Se un metodo è bloccato mentre è in attesa che un evento venga segnalato, non può controllare il valore del token di annullamento e rispondere in modo tempestivo.  Nel primo esempio viene illustrato come risolvere questo problema quando si utilizzano eventi come <xref:System.Threading.ManualResetEvent?displayProperty=fullName> che non supportano a livello nativo il framework di annullamento unificato.  Nel secondo esempio viene illustrato un approccio più semplificato che prevede l'utilizzo di <xref:System.Threading.ManualResetEventSlim?displayProperty=fullName>, che supporta l'annullamento unificato.  
  
> [!NOTE]
>  Quando viene abilitato "Just My Code", in alcuni casi Visual Studio si interromperà in corrispondenza della riga che genera l'eccezione e in cui viene visualizzato un messaggio di errore che indica che l'eccezione non è gestita dal codice utente. Questo errore è benigno.  È possibile premere F5 per continuare e visualizzare il comportamento di gestione delle eccezioni illustrato negli esempi riportati di seguito.  Per impedire l'interruzione di Visual Studio al primo errore, deselezionare semplicemente la casella di controllo "Just My Code" in **Strumenti, Opzioni, Debug, Generale**.  
  
## Esempio  
 Nell'esempio seguente viene utilizzato un oggetto <xref:System.Threading.ManualResetEvent> per illustrare come sbloccare gli handle di attesa che non supportano l'annullamento unificato.  
  
 [!code-csharp[Cancellation#9](../../../samples/snippets/csharp/VS_Snippets_Misc/cancellation/cs/cancellationex9.cs#9)]
 [!code-vb[Cancellation#9](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cancellation/vb/cancellationex9.vb#9)]  
  
## Esempio  
 Nell'esempio riportato di seguito viene utilizzato un oggetto <xref:System.Threading.ManualResetEventSlim> per illustrare come sbloccare le primitive di coordinamento che supportano l'annullamento unificato.  Lo stesso approccio può essere utilizzato con le altre primitive di coordinamento leggere, ad esempio <xref:System.Threading.Semaphore>`Slim` e <xref:System.Threading.CountdownEvent>.  
  
 [!code-csharp[Cancellation#10](../../../samples/snippets/csharp/VS_Snippets_Misc/cancellation/cs/cancellationex10.cs#10)]
 [!code-vb[Cancellation#10](../../../samples/snippets/visualbasic/VS_Snippets_Misc/cancellation/vb/cancellationex10.vb#10)]  
  
## Vedere anche  
 [Cancellation in Managed Threads](../../../docs/standard/threading/cancellation-in-managed-threads.md)