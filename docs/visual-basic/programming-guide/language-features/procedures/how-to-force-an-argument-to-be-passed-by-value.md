---
title: 'Procedura: forzare un argomento sia passati per valore (Visual Basic) | Documenti di Microsoft'
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
- procedures, arguments
- procedures, parameters
- procedure arguments
- Visual Basic code, procedures
- arguments [Visual Basic], ByVal
- arguments [Visual Basic], passing by value
- procedure parameters
- procedures, calling
- arguments [Visual Basic], in parentheses
- procedure arguments, in parentheses
- arguments [Visual Basic], changing value
ms.assetid: 77b4f2d2-1055-4c2f-a521-874d1db86946
caps.latest.revision: 16
author: dotnet-bot
ms.author: dotnetcontent
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
ms.openlocfilehash: eea3466534f1797170ae4bc72afbcba899929911
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-force-an-argument-to-be-passed-by-value-visual-basic"></a>Procedura: forzare il passaggio di un argomento per valore (Visual Basic)
La dichiarazione della routine determina il meccanismo di passaggio. Se un parametro dichiarato [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md), [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] prevede di passare all'argomento corrispondente per riferimento. In questo modo la procedura modificare il valore dell'elemento di programmazione sottostante all'argomento nel codice chiamante. Se si desidera proteggere l'elemento sottostante da tale modifica, è possibile eseguire l'override di `ByRef` meccanismo di passaggio della procedura chiamata racchiudendo il nome dell'argomento tra parentesi. Tali parentesi vengono aggiunte le parentesi che racchiudono l'elenco di argomenti nella chiamata.  
  
 Il codice chiamante non può ignorare un [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md) meccanismo.  
  
### <a name="to-force-an-argument-to-be-passed-by-value"></a>Per forzare un argomento sia passati per valore  
  
-   Se viene dichiarato il parametro corrispondente `ByVal` nella procedura, non è necessario eseguire passaggi aggiuntivi. [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]già prevede di passare l'argomento per valore.  
  
-   Se viene dichiarato il parametro corrispondente `ByRef` nella routine, racchiudere l'argomento tra parentesi nella chiamata di procedura.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente esegue l'override di un `ByRef` dichiarazione del parametro. Nella chiamata che forza `ByVal`, notare i due livelli di parentesi.  
  
 [!code-vb[VbVbcnProcedures&#39;](./codesnippet/VisualBasic/how-to-force-an-argument-to-be-passed-by-value_1.vb)]  
  
 [!code-vb[&#40; VbVbcnProcedures](./codesnippet/VisualBasic/how-to-force-an-argument-to-be-passed-by-value_2.vb)]  
  
 Quando `str` è racchiuso tra parentesi aggiuntive nell'elenco degli argomenti, il `setNewString` routine non può modificare il valore del codice chiamante e `MsgBox` Visualizza "Non può essere sostituito se passato ByVal". Quando `str` non viene racchiusa tra parentesi aggiuntive, la routine può modificare, e `MsgBox` Visualizza "È un nuovo valore per l'argomento inString".  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
 Quando si passa una variabile per riferimento, è necessario utilizzare il `ByRef` (parola chiave) per specificare tale meccanismo.  
  
 Il valore predefinito in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] gli argomenti vengono passati per valore. Tuttavia, è buona norma includere una programmazione di [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md) o [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md) (parola chiave) con ogni parametro dichiarato. In questo modo il codice più facile da leggere.  
  
## <a name="robust-programming"></a>Programmazione efficiente  
 Se una routine dichiara un parametro [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md), la corretta esecuzione del codice potrebbe dipendere la possibilità di modificare l'elemento sottostante nel codice chiamante. Se il codice chiamante esegue l'override di questo meccanismo di chiamata racchiudendo l'argomento tra parentesi, o se viene passato un argomento non modificabile, la routine non può modificare l'elemento sottostante. Ciò potrebbe produrre risultati imprevisti nel codice chiamante.  
  
## <a name="net-framework-security"></a>Sicurezza di .NET Framework  
 È sempre presente un potenziale rischio per consentire a una procedura per modificare il valore sottostante a un argomento nel codice chiamante. Assicurarsi che si prevede che il valore modificato e in grado di verificare la validità prima di utilizzarlo.  
  
## <a name="see-also"></a>Vedere anche  
 [Procedure](./index.md)   
 [Gli argomenti e parametri di routine](./procedure-parameters-and-arguments.md)   
 [Procedura: passare argomenti a una routine](./how-to-pass-arguments-to-a-procedure.md)   
 [Passaggio di argomenti per valore e per riferimento](./passing-arguments-by-value-and-by-reference.md)   
 [Differenze tra argomenti modificabili e](./differences-between-modifiable-and-nonmodifiable-arguments.md)   
 [Differenze tra il passaggio di un argomento per valore e per riferimento](./differences-between-passing-an-argument-by-value-and-by-reference.md)   
 [Procedura: modificare il valore di un argomento di routine](./how-to-change-the-value-of-a-procedure-argument.md)   
 [Procedura: proteggere un argomento di routine modifica del valore](./how-to-protect-a-procedure-argument-against-value-changes.md)   
 [Passaggio di argomenti in base alla posizione e in base al nome](./passing-arguments-by-position-and-by-name.md)   
 [Tipi valore e tipi di riferimento](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)
