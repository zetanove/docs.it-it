---
title: "Error Types (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "exceptions, types"
  - "errors [Visual Basic], types"
  - "errors [Visual Basic], logic"
  - "errors [Visual Basic], syntax"
  - "logic errors, Visual Basic"
  - "run-time errors, types of errors"
  - "syntax errors, Visual Basic"
ms.assetid: 3048aabf-8c97-4e13-9150-853769cb5f6f
caps.latest.revision: 13
caps.handback.revision: 13
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Error Types (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

In [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] gli errori, detti anche *eccezioni* possono essere suddivisi in tre categorie: errori di sintassi, errori di runtime ed errori logici.  
  
## Errori di sintassi  
 Gli *errori di sintassi* vengono visualizzati durante la scrittura del codice.  [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] controlla il codice durante la digitazione nella finestra **Editor di codice** e avvisa l'utente in caso di errori, quali l'ortografia errata di parole o l'utilizzo improprio di un elemento del linguaggio.  Gli errori di sintassi costituiscono il tipo di errori più comune.  È possibile correggerli facilmente, all'interno del codice, nel momento in cui si verificano.  
  
> [!NOTE]
>  È possibile evitare gli errori di sintassi utilizzando l'istruzione `Option Explicit`.  Tale istruzione imposta la dichiarazione anticipata di tutte le variabili da utilizzare nell'applicazione.  In questo modo, quando le variabili sono utilizzate nel codice, gli errori di digitazione vengono rilevati immediatamente e possono essere corretti.  
  
## Errori di runtime  
 Gli *errori di runtime* vengono visualizzati solo dopo la compilazione e l'esecuzione del codice.  Sono relativi a un codice che sembra corretto, in quanto non contiene errori di sintassi, ma che non verrà eseguito.  È possibile, ad esempio, scrivere correttamente una riga di codice per l'apertura di un file.  Se però il file è danneggiato, l'applicazione non è in grado di eseguire la funzione `Open` e arresta l'esecuzione.  È possibile correggere la maggior parte degli errori di runtime riscrivendo il codice errato, quindi compilandolo ed eseguendolo di nuovo.  
  
## Errori logici  
 *Gli errori logici* sono visualizzati una volta che l'applicazione è in uso.  Si tratta principalmente di risultati indesiderati o imprevisti in risposta ad azioni da parte dell'utente.  È ad esempio possibile che una chiave digitata in modo non corretto o un altro tipo di errore determini l'interruzione del funzionamento dell'applicazione nei parametri previsti o del tutto.  Gli errori logici sono normalmente i più difficili da correggere, perché non è sempre chiaro il punto da cui hanno origine.  
  
## Vedere anche  
 [Try...Catch...Finally Statement](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)   
 [Nozioni di base sul debugger](/visual-studio/debugger/debugger-basics)