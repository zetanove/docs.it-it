---
title: "Procedura: generare eccezioni in modo esplicito | Microsoft Docs"
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
  - "eccezioni, generazione"
  - "eccezioni, blocchi try/catch"
  - "FileNotFoundException (classe)"
  - "generazione implicita di eccezioni"
  - "blocchi try/catch"
ms.assetid: 72bdd157-caa9-4478-9ee3-cb4500b84528
caps.latest.revision: 10
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 8
---
# Procedura: generare eccezioni in modo esplicito
È possibile generare in modo esplicito un'eccezione mediante l'istruzione `throw`.  Tale istruzione consente inoltre di generare nuovamente usando lo statement `throw`.  Nella scrittura del codice è buona norma aggiungere informazioni alle eccezioni che vengono generate nuovamente, in modo da fornire ulteriori informazioni in sede di debug.  
  
 Nell'esempio di codice seguente viene utilizzato un blocco try\/catch per intercettare una possibile eccezione <xref:System.IO.FileNotFoundException>.  Il blocco try è seguito da un blocco catch che intercetta l'eccezione <xref:System.IO.FileNotFoundException>e scrive un messaggio nella console se il file di dati non viene trovato.  L'istruzione successiva rappresenta l'istruzione throw che genera una nuova eccezione <xref:System.IO.FileNotFoundException> aggiungendovi del testo informativo.  
  
## Esempio  
 [!code-csharp[Exception.Throwing#1](../../../samples/snippets/csharp/VS_Snippets_CLR/Exception.Throwing/CS/throw.cs#1)]
 [!code-vb[Exception.Throwing#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/Exception.Throwing/VB/throw.vb#1)]  
  
## Vedere anche  
 [Procedura: Usare il blocco try\/catch per l'intercettazione di eccezioni](../../../docs/standard/exceptions/how-to-use-the-try-catch-block-to-catch-exceptions.md)   
 [Procedura: utilizzare eccezioni specifiche in un blocco catch](../../../docs/standard/exceptions/how-to-use-specific-exceptions-in-a-catch-block.md)   
 [Procedura: utilizzare blocchi Finally](../../../docs/standard/exceptions/how-to-use-finally-blocks.md)   
 [Nozioni fondamentali sulla gestione delle eccezioni](../../../docs/standard/exceptions/exception-handling-fundamentals.md)