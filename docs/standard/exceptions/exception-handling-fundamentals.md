---
title: "Nozioni fondamentali sulla gestione delle eccezioni | Microsoft Docs"
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
  - "Common Language Runtime, eccezioni"
  - "eccezioni, esempi"
  - "runtime, eccezioni"
ms.assetid: e865d48c-b862-4448-833e-09fcd48adf6b
caps.latest.revision: 11
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 9
---
# Nozioni fondamentali sulla gestione delle eccezioni
Nel Common Language Runtime è supportato un modello di gestione delle eccezioni basato sui concetti di oggetti eccezione e blocchi di codice protetti.  Quando si verifica un'eccezione nel runtime viene creato un oggetto che la rappresenta.  È inoltre possibile creare classi di eccezione personalizzate mediante la derivazione dall'eccezione di base appropriata.  
  
 In tutti i linguaggi che utilizzano il runtime le eccezioni vengono gestite in modo simile.  In ciascun linguaggio viene utilizzata una gestione delle eccezioni strutturata di tipo try\/catch\/finally.  In questa sezione verranno forniti vari esempi di gestione di eccezioni di base.  
  
## In questa sezione  
 [Procedura: utilizzare il blocco try\/catch per l'intercettazione di eccezioni](../../../docs/standard/exceptions/how-to-use-the-try-catch-block-to-catch-exceptions.md)  
 Viene descritto come utilizzare il blocco try\/catch per gestire le eccezioni.  
  
 [Procedura: utilizzare eccezioni specifiche in un blocco catch](../../../docs/standard/exceptions/how-to-use-specific-exceptions-in-a-catch-block.md)  
 Viene descritto come intercettare eccezioni specifiche.  
  
 [Procedura: generare eccezioni in modo esplicito](../../../docs/standard/exceptions/how-to-explicitly-throw-exceptions.md)  
 Viene descritto come generare eccezioni e come intercettare eccezioni e quindi generarle nuovamente.  
  
 [Procedura: creare eccezioni definite dall'utente](../../../docs/standard/exceptions/how-to-create-user-defined-exceptions.md)  
 Viene descritto come creare classi di eccezione personalizzate.  
  
 [Utilizzo di gestori filtrati dall'utente](../../../docs/standard/exceptions/using-user-filtered-exception-handlers.md)  
 Viene descritto come definire il filtro di eccezioni.  
  
 [Procedura: utilizzare un blocco finally](../../../docs/standard/exceptions/how-to-use-finally-blocks.md)  
 Viene illustrato come utilizzare l'istruzione finally in un blocco di eccezioni.  
  
## Sezioni correlate  
 [Eccezioni](../../../docs/standard/exceptions/index.md)  
 Una panoramica sulle eccezioni di Common Language Runtime.  
  
 [Classe e proprietà dell'eccezione](../../../docs/standard/exceptions/exception-class-and-properties.md)  
 Vengono descritti gli elementi di un oggetto eccezione.