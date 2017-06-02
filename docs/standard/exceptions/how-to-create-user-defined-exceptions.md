---
title: "Procedura: creare eccezioni definite dall&#39;utente | Microsoft Docs"
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
  - "eccezioni, esempi"
  - "eccezioni, definite dall'utente"
  - "eccezioni definite dall'utente"
ms.assetid: 25819a5a-f915-4fc8-b924-a76915674e04
caps.latest.revision: 10
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: creare eccezioni definite dall&#39;utente
Se si desidera che gli utenti possano distinguere durante l'esecuzione del programma tra alcune condizioni di errore, sarà possibile creare personalmente eccezioni definite dall'utente.  In .NET Framework viene fornita una gerarchia di classi di eccezione derivate, direttamente o indirettamente, dalla classe di base <xref:System.Exception>.  Ciascuna di queste classi definisce un'eccezione specifica, pertanto in molti casi occorre unicamente intercettare l'eccezione.  È inoltre possibile creare classi di eccezione personalizzate derivandole dalla classe <xref:System.Exception>.  
  
 Quando si creano eccezioni personalizzate è buona norma, nella scrittura del codice, che il nome di classe dell'eccezione definita dall'utente termini con la parola "Exception". È inoltre opportuno implementare i tre costruttori comuni consigliati, come illustrato nell'esempio che segue.  
  
> [!NOTE]
>  Nelle situazioni in cui si fa uso di risorse remote, è necessario garantire che i metadati relativi alle eccezioni definite dall'utente siano disponibili sia al server \(il destinatario della chiamata\) che al client \(l'oggetto proxy o chiamante\).  È ad esempio necessario che il codice che consente di chiamare un metodo in un dominio applicazione separato sia in grado di individuare l'assembly contenente un'eccezione generata da una chiamata remota.  Per ulteriori informazioni, vedere [Suggerimenti per gestire le eccezioni](../../../docs/standard/exceptions/best-practices-for-exceptions.md).  
  
 Nell'esempio riportato di seguito una nuova classe di eccezioni, `EmployeeListNotFoundException`, viene derivata da <xref:System.Exception>.  Nella classe vengono definiti tre costruttori, ciascuno dei quali accetta parametri differenti.  
  
## Esempio  
 [!code-cpp[dg_exceptionDesign#14](../../../samples/snippets/cpp/VS_Snippets_CLR/dg_exceptionDesign/cpp/example2.cpp#14)]
 [!code-csharp[dg_exceptionDesign#14](../../../samples/snippets/csharp/VS_Snippets_CLR/dg_exceptionDesign/cs/example2.cs#14)]
 [!code-vb[dg_exceptionDesign#14](../../../samples/snippets/visualbasic/VS_Snippets_CLR/dg_exceptionDesign/vb/example2.vb#14)]  
  
## Vedere anche  
 [Procedura: Usare il blocco try\/catch per l'intercettazione di eccezioni](../../../docs/standard/exceptions/how-to-use-the-try-catch-block-to-catch-exceptions.md)   
 [Procedura: utilizzare eccezioni specifiche in un blocco catch](../../../docs/standard/exceptions/how-to-use-specific-exceptions-in-a-catch-block.md)   
 [Suggerimenti per le eccezioni](../../../docs/standard/exceptions/best-practices-for-exceptions.md)   
 [Nozioni fondamentali sulla gestione delle eccezioni](../../../docs/standard/exceptions/exception-handling-fundamentals.md)