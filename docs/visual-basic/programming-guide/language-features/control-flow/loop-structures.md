---
title: Cicli (strutture (Visual Basic)) | Documenti di Microsoft
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
- control flow, loops
- For keyword [Visual Basic], loop structures
- loops
- loop structures
- statements [Visual Basic], loop
- Do statement, Do loops
- conditional statements, loop structures
ms.assetid: ecacb09b-a4c9-42be-98b2-a15d368b5db8
caps.latest.revision: 18
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
ms.openlocfilehash: c2835b9d9d22196447fb1863f6e4fa9bd11ecf0a
ms.lasthandoff: 03/13/2017

---
# <a name="loop-structures-visual-basic"></a>Strutture di ciclo (Visual Basic)
[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]cicli (strutture) consentono di eseguire ripetutamente una o più righe di codice. È possibile ripetere le istruzioni in una struttura di ciclo fino a quando non è una condizione `True`, fino a quando una condizione è `False`, un numero di volte o una volta per ogni elemento specificato in una raccolta.  
  
 Nella figura seguente viene mostrata una struttura di ciclo che esegue una serie di istruzioni finché una condizione non diventa true.  
  
 ![Diagramma di flusso di un ciclo Do... Fino al ciclo](../../../../visual-basic/programming-guide/language-features/control-flow/media/dountilloop.gif "DoUntilLoop")  
Esecuzione di un set di istruzioni finché una condizione non diventa true  
  
## <a name="while-loops"></a>Cicli while  
 The `While`... `End While` esegue un set di istruzioni finché la condizione specificata nel `While` istruzione `True`. Per ulteriori informazioni, vedere [mentre... Fine istruzione While](../../../../visual-basic/language-reference/statements/while-end-while-statement.md).  
  
## <a name="do-loops"></a>Cicli Do  
 The `Do`... `Loop` costruzione consente di verificare una condizione all'inizio o fine di una struttura di ciclo. È anche possibile specificare se ripetere il ciclo mentre la condizione rimane `True` o fino a quando non diventa `True`. Per ulteriori informazioni, vedere [si... Istruzione di ciclo](../../../../visual-basic/language-reference/statements/do-loop-statement.md).  
  
## <a name="for-loops"></a>Per i cicli  
 The `For`... `Next` esegue il ciclo di un determinato numero di volte per. Viene utilizzata una variabile di controllo del ciclo, detta anche un *contatore*, per tenere traccia delle ripetizioni. Specificare i valori iniziale e finale per questo contatore e, facoltativamente, è possibile specificare la quantità di cui aumenta da una ripetizione alla successiva. Per ulteriori informazioni, vedere [per... Istruzione successiva](../../../../visual-basic/language-reference/statements/for-next-statement.md).  
  
## <a name="for-each-loops"></a>Cicli For Each  
 The `For Each`... `Next` esegue un set di istruzioni una volta per ogni elemento in una raccolta. Specificare la variabile di controllo, ma non è necessario determinare i valori iniziale e finale per esso. Per ulteriori informazioni, vedere [For Each... Istruzione successiva](../../../../visual-basic/language-reference/statements/for-each-next-statement.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Flusso di controllo](../../../../visual-basic/programming-guide/language-features/control-flow/index.md)   
 [Strutture decisionali](../../../../visual-basic/programming-guide/language-features/control-flow/decision-structures.md)   
 [Altre strutture di controllo](../../../../visual-basic/programming-guide/language-features/control-flow/other-control-structures.md)   
 [Strutture di controllo annidate](../../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md)
