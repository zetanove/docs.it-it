---
title: "Determining Object Type (Visual Basic) | Microsoft Docs"
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
  - "classes [Visual Basic], discovering which an object belongs to"
  - "types [Visual Basic], determining Visual Basic object types"
  - "object variables, testing values"
  - "TypeOf...Is expression, object type at run time"
  - "TypeName function"
  - "objects [Visual Basic], type determining"
ms.assetid: d95e7ad1-cd63-41d6-9a28-d7a1380d49c1
caps.latest.revision: 13
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 13
---
# Determining Object Type (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Le variabili oggetto generiche \(ovvero le variabili dichiarate come `Object`\) possono contenere oggetti di qualunque classe.  Quando si utilizzano variabili di tipo `Object`, le operazioni consentite dipendono dalla classe dell'oggetto. È ad esempio possibile che alcuni oggetti non supportino un metodo o una proprietà specifici.  In [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] sono disponibili due sistemi per la definizione del tipo di oggetto memorizzato nella variabile oggetto, ovvero la funzione `TypeName` e l'operatore `TypeOf...Is`.  
  
## TypeName e TypeOf…Is  
 La funzione `TypeName` restituisce una stringa e rappresenta la scelta ideale per la memorizzazione o la visualizzazione del nome della classe di un oggetto, come illustrato nel seguente frammento di codice:  
  
 [!code-vb[VbVbalrOOP#92](../../../../visual-basic/misc/codesnippet/VisualBasic/determining-object-type_1.vb)]  
  
 L'uso dell'operatore `TypeOf...Is` è invece ideale per la verifica del tipo di oggetto, in quanto è più rapido rispetto a un confronto di stringhe equivalente nel quale viene adoperata la funzione `TypeName`.  Nel frammento di codice che segue viene utilizzato l'operatore `TypeOf...Is` all'interno di un'istruzione `If...Then...Else`:  
  
 [!code-vb[VbVbalrOOP#93](../../../../visual-basic/misc/codesnippet/VisualBasic/determining-object-type_2.vb)]  
  
 A questo punto è necessaria una raccomandazione.  L'operatore `TypeOf...Is` restituisce `True` se un oggetto appartiene a o è derivato da un tipo specifico.  Quasi tutte le operazioni eseguite in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] implicano l'utilizzo di oggetti, inclusi alcuni elementi normalmente non considerati oggetti, quali stringhe e Integer.  Questi oggetti derivano da <xref:System.Object> e ne ereditano i metodi.  Quando viene passato un `Integer` e valutato con `Object`, l'operatore `TypeOf...Is` restituisce `True`.  L'esempio che segue indica che il parametro `InParam` è sia un `Object` sia un `Integer`:  
  
 [!code-vb[VbVbalrOOP#94](../../../../visual-basic/misc/codesnippet/VisualBasic/determining-object-type_3.vb)]  
  
 Nell'esempio che segue vengono utilizzati sia `TypeOf...Is` sia `TypeName` per determinare il tipo di oggetto passato nell'argomento `Ctrl`.  La routine `TestObject` chiama `ShowType` con tre diversi tipi di controlli.  
  
#### Per eseguire l'esempio  
  
1.  Creare un nuovo progetto di applicazione per Windows e aggiungere al form un controllo <xref:System.Windows.Forms.Button>, un controllo <xref:System.Windows.Forms.CheckBox> e un controllo <xref:System.Windows.Forms.RadioButton>.  
  
2.  Dal pulsante sul form, chiamare la routine `TestObject`.  
  
3.  Aggiungere il seguente codice al form:  
  
     [!code-vb[VbVbalrOOP#95](../../../../visual-basic/misc/codesnippet/VisualBasic/determining-object-type_4.vb)]  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.Information.TypeName%2A>   
 [Calling a Property or Method Using a String Name](../../../../visual-basic/programming-guide/language-features/early-late-binding/calling-a-property-or-method-using-a-string-name.md)   
 [Object Data Type](../../../../visual-basic/language-reference/data-types/object-data-type.md)   
 [If...Then...Else Statement](../../../../visual-basic/language-reference/statements/if-then-else-statement.md)   
 [String Data Type](../../../../visual-basic/language-reference/data-types/string-data-type.md)   
 [Integer Data Type](../../../../visual-basic/language-reference/data-types/integer-data-type.md)