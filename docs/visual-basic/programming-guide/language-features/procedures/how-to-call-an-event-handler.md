---
title: "How to: Call an Event Handler in Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Visual Basic code, procedures"
  - "event handlers, calling"
  - "event handlers"
  - "procedures, event handlers"
  - "procedures, calling"
ms.assetid: 72e18ef8-144e-40df-a1f4-066a57271e28
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# How to: Call an Event Handler in Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Un *evento* è un'operazione o un'occorrenza, come un clic del mouse o il superamento di un limite di credito, riconosciuta da un componente del programma e per la quale è possibile scrivere un codice di risposta.  Un *gestore eventi* è il codice scritto in risposta a un evento.  
  
 Un gestore eventi in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] è una routine `Sub`.  In genere, tuttavia, tale routine non viene chiamata in modo simile alle altre routine `Sub` ma viene piuttosto identificata come gestore per l'evento.  A tale scopo è possibile utilizzare una clausola [Handles](../../../../visual-basic/language-reference/statements/handles-clause.md) e una variabile [WithEvents](../../../../visual-basic/language-reference/modifiers/withevents.md) oppure un'[AddHandler Statement](../../../../visual-basic/language-reference/statements/addhandler-statement.md).  L'utilizzo di una clausola `Handles` rappresenta la modalità predefinita per dichiarare un gestore eventi in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)].  I gestori eventi vengono scritti in questo modo dagli addetti alla progettazione quando si programma nell'ambiente di sviluppo integrato \(IDE\).  L'istruzione `AddHandler` consente di generare eventi in modo dinamico in fase di esecuzione.  
  
 Quando si verifica l'evento, la routine del gestore eventi viene chiamata automaticamente.  Qualsiasi codice che disponga di accesso all'evento può causarne la generazione mediante l'esecuzione di un'[RaiseEvent Statement](../../../../visual-basic/language-reference/statements/raiseevent-statement.md).  
  
 È possibile associare più gestori eventi allo stesso evento.  In alcuni casi è possibile dissociare un gestore da un evento.  Per ulteriori informazioni, vedere [Events](../../../../visual-basic/programming-guide/language-features/events/events.md).  
  
### Per chiamare un gestore eventi mediante Handles e WithEvents  
  
1.  Verificare che l'evento venga dichiarato mediante un'[Event Statement](../../../../visual-basic/language-reference/statements/event-statement.md).  
  
2.  Dichiarare una variabile oggetto a livello di modulo o classe utilizzando la parola chiave [WithEvents](../../../../visual-basic/language-reference/modifiers/withevents.md).  La clausola `As` per questa variabile deve specificare la classe che genera l'evento.  
  
3.  Nella dichiarazione della routine di gestione degli eventi `Sub` aggiungere una clausola [Handles](../../../../visual-basic/language-reference/statements/handles-clause.md) che specifichi la variabile `WithEvents` e il nome dell'evento.  
  
4.  Quando si verifica l'evento, la routine `Sub` viene chiamata automaticamente.  Nel codice è possibile specificare un'istruzione `RaiseEvent` per generare l'evento.  
  
     Nell'esempio seguente vengono definiti un evento e una variabile `WithEvents` che fa riferimento alla classe che genera l'evento.  La routine di gestione degli eventi `Sub` utilizza una clausola `Handles` per specificare la classe e l'evento che gestisce.  
  
     [!code-vb[VbVbcnProcedures#4](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/how-to-call-an-event-han_1.vb)]  
  
### Per chiamare un gestore eventi mediante AddHandler  
  
1.  Verificare che l'evento venga dichiarato mediante un'istruzione `Event`.  
  
2.  Eseguire un'[AddHandler Statement](../../../../visual-basic/language-reference/statements/addhandler-statement.md) per collegare in modo dinamico la routine di gestione degli eventi `Sub` all'evento stesso.  
  
3.  Quando si verifica l'evento, la routine `Sub` viene chiamata automaticamente.  Nel codice è possibile specificare un'istruzione `RaiseEvent` per generare l'evento.  
  
     Nell'esempio seguente viene definita una routine `Sub` per la gestione dell'evento <xref:System.Windows.Forms.Form.Closing> di un form.  Viene quindi utilizzata l'[AddHandler Statement](../../../../visual-basic/language-reference/statements/addhandler-statement.md) per associare la routine `catchClose` come gestore eventi per <xref:System.Windows.Forms.Form.Closing>.  
  
     [!code-vb[VbVbcnProcedures#5](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/how-to-call-an-event-han_2.vb)]  
  
     È possibile dissociare un gestore eventi da un evento mediante l'esecuzione dell'[RemoveHandler Statement](../../../../visual-basic/language-reference/statements/removehandler-statement.md).  
  
## Vedere anche  
 [Procedures](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Sub Procedures](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md)   
 [Sub Statement](../../../../visual-basic/language-reference/statements/sub-statement.md)   
 [AddressOf Operator](../../../../visual-basic/language-reference/operators/addressof-operator.md)   
 [How to: Create a Procedure](../../../../visual-basic/programming-guide/language-features/procedures/how-to-create-a-procedure.md)   
 [How to: Call a Procedure that Does Not Return a Value](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-a-procedure-that-does-not-return-a-value.md)