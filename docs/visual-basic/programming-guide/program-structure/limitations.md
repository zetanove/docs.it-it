---
title: Limitazioni di Visual Basic | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- limits
- limitations, Visual Basic
- limitations
- limits, Visual Basic code
- Visual Basic code, limitations
ms.assetid: cf1646b7-5d24-48c6-9616-bda8a4849d91
caps.latest.revision: 14
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
ms.openlocfilehash: d556b045b4ebae6ba24c0571a6cb7e5337c6a8f2
ms.lasthandoff: 03/13/2017

---
# <a name="visual-basic-limitations"></a>Limitazioni di Visual Basic
Le versioni precedenti di [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] applicati limiti nel codice, ad esempio la lunghezza dei nomi di variabili, il numero di variabili consentite nei moduli e le dimensioni del modulo. In [!INCLUDE[vbprvblong](../../../visual-basic/developing-apps/customizing-extending-my/includes/vbprvblong_md.md)], ridotti queste restrizioni, fornendo una maggiore libertà nella scrittura e il codice.  
  
 I limiti fisici sono dipendenti più memoria in fase di esecuzione su considerazioni relative alla fase di compilazione. Se si utilizzano le procedure di programmazione prudenti e dividono applicazioni di grandi dimensioni in più classi e moduli, è presente poche probabilità di incontrare interna [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] limitazione.  
  
 Di seguito sono alcune limitazioni che potrebbero verificarsi in casi estremi.  
  
-   **Lunghezza del nome.** Esiste un numero massimo di caratteri per il nome di ogni elemento di programmazione dichiarato. Questo limite si applica a un'intera stringa di qualificazione se il nome dell'elemento è qualificato. Vedere [dichiarati i nomi degli elementi](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md).  
  
-   **Lunghezza della riga.** Esiste un massimo di 65535 caratteri in una riga fisica del codice sorgente. La riga di codice sorgente logico può essere superiore se si utilizzano caratteri di continuazione di riga. Vedere [procedura: interrompere e combinare istruzioni nel codice](../../../visual-basic/programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md).  
  
-   **Dimensioni della matrice.** Esiste un numero massimo di dimensioni che è possibile dichiarare una matrice. Questo limita il numero degli indici è possibile utilizzare per specificare un elemento di matrice. Vedere [matrice dimensioni in Visual Basic](../../../visual-basic/programming-guide/language-features/arrays/array-dimensions.md).  
  
-   **Lunghezza della stringa.** Esiste un numero massimo di caratteri Unicode, che è possibile archiviare in una singola stringa. Vedere [tipo di dati stringa](../../../visual-basic/language-reference/data-types/string-data-type.md).  
  
-   **Lunghezza della stringa di ambiente.** Esiste un massimo di 32768 caratteri per qualsiasi stringa di ambiente utilizzato come argomento della riga di comando. Si tratta di una limitazione in tutte le piattaforme.  
  
## <a name="see-also"></a>Vedere anche  
 [Struttura del programma e convenzioni del codice](../../../visual-basic/programming-guide/program-structure/program-structure-and-code-conventions.md)   
 [Convenzioni di denominazione di Visual Basic](../../../visual-basic/programming-guide/program-structure/naming-conventions.md)
