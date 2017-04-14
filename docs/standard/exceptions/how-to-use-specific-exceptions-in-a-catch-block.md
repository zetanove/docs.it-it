---
title: "Procedura: utilizzare eccezioni specifiche in un blocco catch | Microsoft Docs"
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
  - "blocchi catch"
  - "eccezioni, blocchi try/catch"
  - "blocchi try/catch"
ms.assetid: 12af9ff3-8587-4f31-90cf-6c2244e0fdae
caps.latest.revision: 9
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: utilizzare eccezioni specifiche in un blocco catch
Quando si verifica un'eccezione, essa viene passata verso i livelli superiori dello stack e ciascun blocco catch ha l'opportunità di gestirla.  L'ordine delle istruzioni catch è importante.  Inserire i blocchi catch destinati a eccezioni specifiche prima di un blocco catch relativo a eccezioni generiche, poiché in caso contrario è possibile che venga generato un errore in fase di compilazione.  Nella determinazione del blocco catch adatto viene considerato il tipo dell'eccezione, che deve corrispondere al nome dell'eccezione specificata nel blocco catch.  Se non esiste alcun blocco catch specifico, l'eccezione verrà intercettata da un blocco catch generico, se ne è presente uno.  
  
 Nell'esempio di codice seguente viene utilizzato un blocco try\/catch per intercettare un'eccezione <xref:System.InvalidCastException>.  Nell'esempio viene creata una classe denominata `Employee` con una singola proprietà, relativa al livello dell'impiegato \(`Emlevel`\).  Un metodo`, PromoteEmployee`, richiede la specifica di un oggetto e incrementa il livello dell'impiegato.  Quando al metodo `PromoteEmployee` viene passata un'istanza di <xref:System.DateTime>, si verifica un'eccezione **InvalidCastException**.  
  
## Esempio  
 [!code-cpp[CatchException#2](../../../samples/snippets/cpp/VS_Snippets_CLR/CatchException/CPP/catchexception1.cpp#2)]
 [!code-csharp[CatchException#2](../../../samples/snippets/csharp/VS_Snippets_CLR/CatchException/CS/catchexception1.cs#2)]
 [!code-vb[CatchException#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CatchException/VB/catchexception1.vb#2)]  
  
 Le eccezioni che non vengono intercettate da un blocco catch vengono intercettate nel Common Language Runtime.  A seconda della configurazione del runtime viene visualizzata una finestra di dialogo di debug oppure viene interrotta l'esecuzione del programma e viene visualizzata una finestra di dialogo contenente informazioni sull'eccezione.  Per informazioni sul debug, vedere [Debug e profiling di applicazioni](../../../docs/framework/debug-trace-profile/index.md).  
  
## Vedere anche  
 [Procedura: Usare il blocco try\/catch per l'intercettazione di eccezioni](../../../docs/standard/exceptions/how-to-use-the-try-catch-block-to-catch-exceptions.md)   
 [Procedura: generare eccezioni in modo esplicito](../../../docs/standard/exceptions/how-to-explicitly-throw-exceptions.md)   
 [Procedura: creare eccezioni definite dall'utente](../../../docs/standard/exceptions/how-to-create-user-defined-exceptions.md)   
 [Procedura: utilizzare blocchi Finally](../../../docs/standard/exceptions/how-to-use-finally-blocks.md)   
 [Classe e proprietà dell'eccezione](../../../docs/standard/exceptions/exception-class-and-properties.md)   
 [Nozioni fondamentali sulla gestione delle eccezioni](../../../docs/standard/exceptions/exception-handling-fundamentals.md)