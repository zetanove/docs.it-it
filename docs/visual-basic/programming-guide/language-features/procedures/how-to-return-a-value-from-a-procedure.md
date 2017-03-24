---
title: 'Procedura: restituire un valore da una routine (Visual Basic) | Documenti di Microsoft'
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
- procedures, returning from
- procedures, returning a value
ms.assetid: 4bcc4724-2b4e-4df8-9b4b-16054607f87d
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
ms.openlocfilehash: 98f0fb0740a021a16e87454bfaebbfad7858477c
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-return-a-value-from-a-procedure-visual-basic"></a>Procedura: restituire un valore da una routine (Visual Basic)
Oggetto `Function` routine restituisce un valore al codice chiamante tramite l'esecuzione di un `Return` istruzione o l'individuazione un `Exit Function` o `End Function` istruzione.  
  
### <a name="to-return-a-value-using-the-return-statement"></a>Per restituire un valore utilizzando l'istruzione Return  
  
1.  Inserire un `Return` istruzione nel punto in cui viene completata l'attività della routine.  
  
2.  Seguire il `Return` (parola chiave) con un'espressione che restituisce il valore da restituire al codice chiamante.  
  
3.  È possibile avere più di una `Return` istruzione nella stessa procedura.  
  
     Nell'esempio `Function` procedure calcola il lato più lungo, ovvero l'ipotenusa, di un triangolo rettangolo e lo restituisce al codice chiamante.  
  
     [!code-vb[VbVbcnProcedures n.&1;](./codesnippet/VisualBasic/how-to-return-a-value-from-a-procedure_1.vb)]  
  
     Nell'esempio seguente viene illustrata una tipica chiamata a `hypotenuse`, che memorizza il valore restituito.  
  
     [!code-vb[6 VbVbcnProcedures](./codesnippet/VisualBasic/how-to-return-a-value-from-a-procedure_2.vb)]  
  
### <a name="to-return-a-value-using-exit-function-or-end-function"></a>Per restituire un valore utilizzando Exit Function o End Function  
  
1.  In almeno un punto di `Function` procedura, assegnare un valore al nome della stored procedure.  
  
2.  Quando si esegue un `Exit Function` o `End Function` istruzione [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] restituisce l'ultimo valore assegnato al nome della stored procedure.  
  
3.  È possibile avere più di una `Exit Function` istruzione nella procedura stessa, è possibile combinare `Return` e `Exit Function` istruzioni nella procedura stessa.  
  
4.  È possibile avere solo una `End Function` istruzione in un `Function` procedura.  
  
     Per ulteriori informazioni e un esempio, vedere "Valore restituito" in [istruzione Function](../../../../visual-basic/language-reference/statements/function-statement.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Procedure](./index.md)   
 [Sub (routine)](./sub-procedures.md)   
 [Proprietà (routine)](./property-procedures.md)   
 [Routine di operatore](./operator-procedures.md)   
 [Gli argomenti e parametri di routine](./procedure-parameters-and-arguments.md)   
 [Istruzione Function](../../../../visual-basic/language-reference/statements/function-statement.md)   
 [Return (istruzione)](../../../../visual-basic/language-reference/statements/return-statement.md)   
 [Procedura: creare una routine che restituisce un valore](./how-to-create-a-procedure-that-returns-a-value.md)   
 [Procedura: Chiamare una routine che restituisce un valore](./how-to-call-a-procedure-that-returns-a-value.md)
