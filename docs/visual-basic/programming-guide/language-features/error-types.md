---
title: Tipi di errore (Visual Basic) | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
helpviewer_keywords:
- exceptions, types
- errors [Visual Basic], types
- errors [Visual Basic], logic
- errors [Visual Basic], syntax
- logic errors, Visual Basic
- run-time errors, types of errors
- syntax errors, Visual Basic
ms.assetid: 3048aabf-8c97-4e13-9150-853769cb5f6f
caps.latest.revision: 13
author: stevehoag
ms.author: shoag
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: d48756b74baf757f043e68124d8b65c2f613e595
ms.lasthandoff: 03/13/2017

---
# <a name="error-types-visual-basic"></a>Tipi di errore (Visual Basic)
In [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)], gli errori (detto anche *eccezioni*) rientrano in una delle tre categorie: errori di sintassi, errori di run-time e gli errori logici.  
  
## <a name="syntax-errors"></a>Errori di sintassi  
 *Errori di sintassi* vengono visualizzati durante la scrittura di codice. [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]Controlla il codice durante la digitazione nel **Editor di codice** finestra e genera avvisi se si commette un errore, ad esempio ortografia errata di parole o utilizzo improprio di un elemento di linguaggio. Errori di sintassi sono il tipo più comune di errori. È possibile correggerli facilmente nell'ambiente di codifica, non appena si verificano.  
  
> [!NOTE]
>  Il `Option Explicit` istruzione è un mezzo per evitare errori di sintassi. Impone la dichiarazione in anticipo, tutte le variabili da utilizzare nell'applicazione. Pertanto, quando tali variabili vengono utilizzate nel codice, gli errori di digitazione vengono rilevati immediatamente e possono essere risolto.  
  
## <a name="run-time-errors"></a>Errori di Run-Time  
 *Errori di run-time* vengono visualizzati solo dopo la compilazione e l'esecuzione del codice. Queste comprendono il codice che sembra essere corretto in quanto non si verificano errori di sintassi, ma che non verrà eseguito. Ad esempio, è possibile scrivere correttamente una riga di codice per aprire un file. Ma se il file è danneggiato, l'applicazione non può eseguire il `Open` funzione e si arresta. Per risolvere la maggior parte degli errori di runtime, riscrivere il codice non corretto, quindi ricompilare ed eseguirla nuovamente.  
  
## <a name="logic-errors"></a>Errori di logica  
 *Errori di logica* vengono visualizzati una volta che l'applicazione è in uso. Si tratta la maggior parte dei risultati indesiderati o imprevisti in risposta alle azioni dell'utente. Ad esempio, una chiave errata o altri determini, si potrebbero smettere di funzionare nei parametri previsti, l'applicazione o del tutto. Gli errori logici sono in genere il tipo più difficile da correggere, perché non è sempre chiaro dove provengono.  
  
## <a name="see-also"></a>Vedere anche  
 [Istruzione Try...Catch...Finally](../../../visual-basic/language-reference/statements/try-catch-finally-statement.md)   
 [Nozioni di base sul debugger](https://docs.microsoft.com/visualstudio/debugger/debugger-basics)
