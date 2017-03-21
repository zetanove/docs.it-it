---
title: 'Procedura: chiamare una routine di overload (Visual Basic) | Documenti di Microsoft'
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
- Visual Basic code, procedures
- procedures, overloading
- procedures, calling
- procedures, multiple versions
- procedure calls, overloaded
ms.assetid: 3bb331fb-f6bc-406f-9ca0-9609b497014c
caps.latest.revision: 12
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
ms.openlocfilehash: 0da83aa63bf013d841f2a01a535726f3b03497a1
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-call-an-overloaded-procedure-visual-basic"></a>Procedura: chiamare una routine di overload (Visual Basic)
Il vantaggio di overload di una routine è la flessibilità della chiamata. Il codice chiamante può ottenere le informazioni che necessarie per passare alla procedura e quindi chiamare un singolo nome di routine indipendentemente dagli argomenti passaggio.  
  
### <a name="to-call-a-procedure-that-has-more-than-one-version-defined"></a>Per chiamare una routine che ha definita più di una versione  
  
1.  Nel codice chiamante, determinare i dati da passare alla procedura.  
  
2.  Scrivere la chiamata di procedura in modo normale, presentazione dei dati nell'elenco di argomenti. Assicurarsi che gli argomenti corrispondano all'elenco di parametri in una delle versioni definite per la procedura.  
  
3.  Non è necessario determinare la versione della routine da chiamare. [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]passa il controllo alla versione corrispondente all'elenco di argomenti.  
  
     Nell'esempio seguente viene chiamato il `post` routine dichiarata in [procedura: definire più versioni di una routine](./how-to-define-multiple-versions-of-a-procedure.md). Ottiene l'identificazione del cliente, determina se è un `String` o `Integer`, quindi chiama la stessa procedura in entrambi i casi.  
  
     [!code-vb[&#56; VbVbcnProcedures](./codesnippet/VisualBasic/how-to-call-an-overloaded-procedure_1.vb)]  
  
     [!code-vb[VbVbcnProcedures&#57;](./codesnippet/VisualBasic/how-to-call-an-overloaded-procedure_2.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 [Procedure](./index.md)   
 [Gli argomenti e parametri di routine](./procedure-parameters-and-arguments.md)   
 [Overload di routine](./procedure-overloading.md)   
 [Le procedure di risoluzione](./troubleshooting-procedures.md)   
 [Procedura: definire più versioni di una routine](./how-to-define-multiple-versions-of-a-procedure.md)   
 [Procedura: eseguire l'Overload di una routine che accetta parametri facoltativi](./how-to-overload-a-procedure-that-takes-optional-parameters.md)   
 [Procedura: eseguire l'Overload di una routine che accetta un numero indefinito di parametri](./how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters.md)   
 [Considerazioni sull'overload di routine](./considerations-in-overloading-procedures.md)   
 [Risoluzione dell'overload](./overload-resolution.md)   
 [Overload](../../../../visual-basic/language-reference/modifiers/overloads.md)
