---
title: 'Procedura: chiamare un gestore eventi in Visual Basic | Documenti di Microsoft'
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
- event handlers, calling
- event handlers
- procedures, event handlers
- procedures, calling
ms.assetid: 72e18ef8-144e-40df-a1f4-066a57271e28
caps.latest.revision: 19
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
ms.openlocfilehash: c5b300feca3415d1283d24179795a4ae92c61e52
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-call-an-event-handler-in-visual-basic"></a>Procedura: chiamare un gestore eventi in Visual Basic
Un *evento* è un'azione o un'occorrenza, ad esempio un mouse superato un limite di credito o fare clic su, che è riconosciuto da un componente di programma e per cui è possibile scrivere codice per rispondere. Un *gestore dell'evento* è il codice scritto in risposta a un evento.  
  
 Un gestore dell'evento [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] è un `Sub` procedura. Tuttavia, si non viene in genere chiamato lo stesso modo di altri `Sub` procedure. Al contrario, la procedura per identificare come un gestore per l'evento. È possibile eseguire questa operazione con un [gestisce](../../../../visual-basic/language-reference/statements/handles-clause.md) clausola e [WithEvents](../../../../visual-basic/language-reference/modifiers/withevents.md) variabile, o con un [AddHandler (istruzione)](../../../../visual-basic/language-reference/statements/addhandler-statement.md). Utilizzando un `Handles` clausola è la modalità predefinita per dichiarare un gestore dell'evento [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]. Questo è il modo in cui che i gestori eventi vengono scritti dalle finestre di progettazione quando si programma nell'ambiente di sviluppo integrato (IDE). Il `AddHandler` istruzione è adatta per la generazione di eventi in modo dinamico in fase di esecuzione.  
  
 Quando si verifica l'evento, [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] automaticamente chiama la routine del gestore eventi. Qualsiasi codice che dispone dell'accesso per l'evento può causare la generazione mediante l'esecuzione di un [istruzione RaiseEvent](../../../../visual-basic/language-reference/statements/raiseevent-statement.md).  
  
 È possibile associare più gestori di eventi con lo stesso evento. In alcuni casi è possibile dissociare un gestore a un evento. Per ulteriori informazioni, vedere [eventi](../../../../visual-basic/programming-guide/language-features/events/index.md).  
  
### <a name="to-call-an-event-handler-using-handles-and-withevents"></a>Per chiamare un gestore eventi mediante Handles e WithEvents  
  
1.  Assicurarsi che l'evento è dichiarato con un [istruzione Event](../../../../visual-basic/language-reference/statements/event-statement.md).  
  
2.  Dichiarare una variabile oggetto livello di modulo o classe utilizzando il [WithEvents](../../../../visual-basic/language-reference/modifiers/withevents.md) (parola chiave). Il `As` clausola per questa variabile deve specificare la classe che genera l'evento.  
  
3.  Nella dichiarazione della gestione dell'evento `Sub` procedura, aggiungere un [gestisce](../../../../visual-basic/language-reference/statements/handles-clause.md) clausola che specifica il `WithEvents` variabile e il nome dell'evento.  
  
4.  Quando si verifica l'evento, [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] chiama automaticamente il `Sub` procedura. Il codice può usare un `RaiseEvent` istruzione per generare l'evento.  
  
     Nell'esempio seguente definisce un evento e un `WithEvents` variabile che fa riferimento alla classe che genera l'evento. La gestione dell'evento `Sub` procedura vengono utilizzati un `Handles` clausola per specificare la classe gestisce l'evento.  
  
     [!code-vb[VbVbcnProcedures n.&4;](./codesnippet/VisualBasic/how-to-call-an-event-handler_1.vb)]  
  
### <a name="to-call-an-event-handler-using-addhandler"></a>Per chiamare un gestore eventi mediante AddHandler  
  
1.  Assicurarsi che l'evento è dichiarato con un `Event` istruzione.  
  
2.  Eseguire un [AddHandler (istruzione)](../../../../visual-basic/language-reference/statements/addhandler-statement.md) in grado di connettersi in modo dinamico la gestione dell'evento `Sub` procedure con l'evento.  
  
3.  Quando si verifica l'evento, [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] chiama automaticamente il `Sub` procedura. Il codice può usare un `RaiseEvent` istruzione per generare l'evento.  
  
     L'esempio seguente definisce una `Sub` procedura per gestire il <xref:System.Windows.Forms.Form.Closing>evento di un form.</xref:System.Windows.Forms.Form.Closing> Viene quindi utilizzato il [AddHandler (istruzione)](../../../../visual-basic/language-reference/statements/addhandler-statement.md) per associare il `catchClose` procedura come un gestore eventi per <xref:System.Windows.Forms.Form.Closing>.</xref:System.Windows.Forms.Form.Closing>  
  
     [!code-vb[VbVbcnProcedures n.&5;](./codesnippet/VisualBasic/how-to-call-an-event-handler_2.vb)]  
  
     È possibile dissociare un gestore eventi da un evento mediante l'esecuzione di [istruzione RemoveHandler](../../../../visual-basic/language-reference/statements/removehandler-statement.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Procedure](./index.md)   
 [Sub (routine)](./sub-procedures.md)   
 [Sub (istruzione)](../../../../visual-basic/language-reference/statements/sub-statement.md)   
 [AddressOf (operatore)](../../../../visual-basic/language-reference/operators/addressof-operator.md)   
 [Procedura: creare una stored Procedure](./how-to-create-a-procedure.md)   
 [Procedura: Chiamare una routine che non restituisce un valore](./how-to-call-a-procedure-that-does-not-return-a-value.md)
