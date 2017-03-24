---
title: 'Procedura: chiamare una routine che non restituisce un valore (Visual Basic) | Documenti di Microsoft'
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
ms.assetid: 259b49a3-a3c1-4254-ba8c-73cdc4127703
caps.latest.revision: 17
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
ms.openlocfilehash: 17b2b902f3ee6ab79b2614b7742aa08fefab2420
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-call-a-procedure-that-does-not-return-a-value-visual-basic"></a>Procedura: chiamare una routine che non restituisce un valore (Visual Basic)
Oggetto `Sub` procedure non restituisce un valore al codice chiamante. Si chiama in modo esplicito con un'istruzione di chiamata autonoma. È possibile effettuare la chiamata utilizzando semplicemente il nome all'interno di un'espressione.  
  
### <a name="to-call-a-sub-procedure"></a>Per chiamare una routine Sub  
  
1.  Nome del file di `Sub` procedura.  
  
2.  Aggiungere il nome tra parentesi per racchiudere l'elenco di argomenti. Se non sono presenti argomenti, è possibile omettere le parentesi. Tuttavia, l'utilizzo delle parentesi rende il codice più facile da leggere.  
  
3.  Inserire gli argomenti nell'elenco di argomenti all'interno delle parentesi, separati da virgole. Assicurarsi di inserire gli argomenti nello stesso ordine in cui la `Sub` procedura definisce i parametri corrispondenti.  
  
     Nell'esempio seguente viene chiamato il [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] <xref:Microsoft.VisualBasic.Interaction.AppActivate%2A>funzione per attivare una finestra dell'applicazione.</xref:Microsoft.VisualBasic.Interaction.AppActivate%2A> <xref:Microsoft.VisualBasic.Interaction.AppActivate%2A>accetta il titolo della finestra come unico argomento.</xref:Microsoft.VisualBasic.Interaction.AppActivate%2A> Non restituire un valore al codice chiamante. Se non viene eseguito un processo Blocco note, viene generata una <xref:System.ArgumentException>.</xref:System.ArgumentException> Il `Shell` procedura presuppone che le applicazioni siano nei percorsi specificati.  
  
     [!code-vb[VbVbalrCatRef&#11;](./codesnippet/VisualBasic/how-to-call-a-procedure-that-does-not-return-a-value_1.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.Interaction.Shell%2A></xref:Microsoft.VisualBasic.Interaction.Shell%2A>   
 <xref:System.ArgumentException></xref:System.ArgumentException>   
 [Procedure](./index.md)   
 [Sub (routine)](./sub-procedures.md)   
 [Gli argomenti e parametri di routine](./procedure-parameters-and-arguments.md)   
 [Sub (istruzione)](../../../../visual-basic/language-reference/statements/sub-statement.md)   
 [Procedura: creare una stored Procedure](./how-to-create-a-procedure.md)   
 [Procedura: chiamare una routine che restituisce un valore](./how-to-call-a-procedure-that-returns-a-value.md)   
 [Procedura: chiamare un gestore eventi in Visual Basic](./how-to-call-an-event-handler.md)
