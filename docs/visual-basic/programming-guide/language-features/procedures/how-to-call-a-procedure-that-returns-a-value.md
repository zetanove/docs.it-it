---
title: 'Procedura: chiamare una routine che restituisce un valore (Visual Basic) | Documenti di Microsoft'
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
- procedure calls, returning values
- Visual Basic code, procedures
- procedures, calling
- procedures, returning a value
ms.assetid: a445127b-0f5f-465a-98fb-3e514b93d115
caps.latest.revision: 15
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
ms.openlocfilehash: df6bb1ed8acf5f86a290d67fec9c053cfe5245d2
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-call-a-procedure-that-returns-a-value-visual-basic"></a>Procedura: chiamare una routine che restituisce un valore (Visual Basic)
Oggetto `Function` routine restituisce un valore al codice chiamante. Per chiamarla, inclusi il nome e gli argomenti sul lato destro di un'istruzione di assegnazione o in un'espressione.  
  
### <a name="to-call-a-function-procedure-within-an-expression"></a>Per chiamare una routine di funzione all'interno di un'espressione  
  
1.  Utilizzare la `Function` procedura nome esattamente come si utilizzerebbe una variabile. È possibile utilizzare un `Function` procedura chiamata ovunque in un'espressione, è possibile utilizzare una variabile o costante.  
  
2.  Aggiungere il nome tra parentesi per racchiudere l'elenco di argomenti. Se non sono presenti argomenti, è possibile omettere le parentesi. Tuttavia, l'utilizzo delle parentesi rende il codice più facile da leggere.  
  
3.  Inserire gli argomenti nell'elenco di argomenti all'interno delle parentesi, separati da virgole. Assicurarsi di inserire gli argomenti nello stesso ordine in cui la `Function` procedura definisce i parametri corrispondenti.  
  
     In alternativa, è possibile passare uno o più argomenti in base al nome. Per ulteriori informazioni, vedere [il passaggio di argomenti in base alla posizione e al nome](./passing-arguments-by-position-and-by-name.md).  
  
4.  Il valore restituito dalla routine fa parte dell'espressione come valore di una variabile o costante.  
  
### <a name="to-call-a-function-procedure-in-an-assignment-statement"></a>Per chiamare una routine di funzione in un'istruzione di assegnazione  
  
1.  Utilizzare il `Function` nome procedura segue uguali (`=`) segno nell'istruzione di assegnazione.  
  
2.  Aggiungere il nome tra parentesi per racchiudere l'elenco di argomenti. Se non sono presenti argomenti, è possibile omettere le parentesi. Tuttavia, l'utilizzo delle parentesi rende il codice più facile da leggere.  
  
3.  Inserire gli argomenti nell'elenco di argomenti all'interno delle parentesi, separati da virgole. Assicurarsi di inserire gli argomenti nello stesso ordine in cui la `Function` procedura definisce i parametri corrispondenti, a meno che vengano passati in base al nome.  
  
4.  Il valore restituito dalla routine è archiviato nella variabile o proprietà sul lato sinistro dell'istruzione di assegnazione.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene chiamato il [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] <xref:Microsoft.VisualBasic.Interaction.Environ%2A>per recuperare il valore di una variabile di ambiente del sistema operativo.</xref:Microsoft.VisualBasic.Interaction.Environ%2A> Il prima riga chiama `Environ` all'interno di un'espressione, mentre la seconda viene chiamata in un'istruzione di assegnazione. `Environ`accetta il nome della variabile come unico argomento. Restituisce il valore della variabile al codice chiamante.  
  
 [!code-vb[VbVbcnProcedures&#7;](./codesnippet/VisualBasic/how-to-call-a-procedure-that-returns-a-value_1.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 [Routine di funzione](./function-procedures.md)   
 [Gli argomenti e parametri di routine](./procedure-parameters-and-arguments.md)   
 [Istruzione Function](../../../../visual-basic/language-reference/statements/function-statement.md)   
 [Procedura: creare una routine che restituisce un valore](./how-to-create-a-procedure-that-returns-a-value.md)   
 [Procedura: restituire un valore da una routine](./how-to-return-a-value-from-a-procedure.md)   
 [Procedura: Chiamare una routine che non restituisce un valore](./how-to-call-a-procedure-that-does-not-return-a-value.md)
