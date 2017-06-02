---
title: "Procedura: utilizzare blocchi Finally | Microsoft Docs"
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
  - "ArgumentOutOfRangeException (classe)"
  - "eccezioni, finally (blocchi)"
  - "eccezioni, blocchi try/catch"
  - "finally (blocchi)"
  - "blocchi try/catch"
ms.assetid: 4b9c0137-04af-4468-91d1-b9014df8ddd2
caps.latest.revision: 9
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 7
---
# Procedura: utilizzare blocchi Finally
Quando si verifica un'eccezione, l'esecuzione si interrompe e il controllo passa al più vicino gestore eccezioni.  Questo comporta spesso la mancata esecuzione di righe di codice che si prevede invece vengano sempre chiamate.  È necessario che una certa pulitura delle risorse, quale la chiusura di un file, venga sempre eseguita, anche quando viene generata un'eccezione.  A tale scopo è possibile utilizzare un blocco finally.  I blocchi finally vengono sempre eseguiti, indipendentemente dal verificarsi di eventuali eccezioni.  
  
 Nell'esempio di codice seguente viene utilizzato un blocco try\/catch per intercettare un'eccezione <xref:System.ArgumentOutOfRangeException>.  Il metodo `Main` crea due matrici e tenta di copiarne una nell'altra.  In seguito a questa operazione viene generata un'eccezione **ArgumentOutOfRangeException** e l'errore viene scritto nella console.  Il blocco finally viene eseguito indipendentemente dall'esito dell'operazione di copia.  
  
## Esempio  
 [!code-cpp[CodeTryCatchFinallyExample#3](../../../samples/snippets/cpp/VS_Snippets_CLR/CodeTryCatchFinallyExample/CPP/source2.cpp#3)]
 [!code-csharp[CodeTryCatchFinallyExample#3](../../../samples/snippets/csharp/VS_Snippets_CLR/CodeTryCatchFinallyExample/CS/source2.cs#3)]
 [!code-vb[CodeTryCatchFinallyExample#3](../../../samples/snippets/visualbasic/VS_Snippets_CLR/CodeTryCatchFinallyExample/VB/source2.vb#3)]  
  
## Vedere anche  
 [Procedura: Usare il blocco try\/catch per l'intercettazione di eccezioni](../../../docs/standard/exceptions/how-to-use-the-try-catch-block-to-catch-exceptions.md)   
 [Procedura: generare eccezioni in modo esplicito](../../../docs/standard/exceptions/how-to-explicitly-throw-exceptions.md)   
 [Procedura: creare eccezioni definite dall'utente](../../../docs/standard/exceptions/how-to-create-user-defined-exceptions.md)   
 [Nozioni fondamentali sulla gestione delle eccezioni](../../../docs/standard/exceptions/exception-handling-fundamentals.md)