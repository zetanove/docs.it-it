---
title: Determinazione del tipo di oggetto (Visual Basic) | Documenti di Microsoft
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
- classes [Visual Basic], discovering which an object belongs to
- types [Visual Basic], determining Visual Basic object types
- object variables, testing values
- TypeOf...Is expression, object type at run time
- TypeName function
- objects [Visual Basic], type determining
ms.assetid: d95e7ad1-cd63-41d6-9a28-d7a1380d49c1
caps.latest.revision: 13
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
ms.openlocfilehash: 2486d989801fc4866a50747aa963b509a627994d
ms.lasthandoff: 03/13/2017

---
# <a name="determining-object-type-visual-basic"></a>Determinazione del tipo di un oggetto (Visual Basic)
Le variabili oggetto generiche (ovvero, le variabili dichiarate come `Object`) possono contenere oggetti di qualsiasi classe. Quando si utilizzano variabili di tipo `Object`, potrebbe essere necessario eseguire azioni diverse in base alla classe dell'oggetto, ad esempio, alcuni oggetti potrebbero non supportare una determinata proprietà o metodo. [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]fornisce due modi per determinare quale tipo di oggetto viene archiviato in una variabile oggetto: il `TypeName` funzione e `TypeOf...Is` operatore.  
  
## <a name="typename-and-typeofis"></a>TypeName e TypeOf... È  
 Il `TypeName` funzione restituisce una stringa ed è la scelta migliore quando è necessario archiviare o visualizzare il nome della classe di un oggetto, come illustrato nel frammento di codice seguente:  
  
 [!code-vb[VbVbalrOOP&#92;](../../../../visual-basic/misc/codesnippet/VisualBasic/determining-object-type_1.vb)]  
  
 Il `TypeOf...Is` operatore è la scelta migliore per il test di un tipo di oggetto, perché è molto più veloce rispetto a un confronto di stringa equivalente con `TypeName`. Il frammento di codice seguente utilizza `TypeOf...Is` all'interno di un `If...Then...Else` istruzione:  
  
 [!code-vb[&#93; VbVbalrOOP](../../../../visual-basic/misc/codesnippet/VisualBasic/determining-object-type_2.vb)]  
  
 Una precisazione è dovuta qui. Il `TypeOf...Is` operatore restituisce `True` se un oggetto è di un tipo specifico oppure è derivato da un tipo specifico. Quasi tutte le operazioni eseguite con [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] all'uso di oggetti, inclusi alcuni elementi che normalmente non vengono considerati come oggetti, ad esempio stringhe e numeri interi. Questi oggetti derivano da ed ereditano i metodi <xref:System.Object>.</xref:System.Object> Quando viene passato un `Integer` e valutato con `Object`, `TypeOf...Is` operatore restituisce `True`. L'esempio seguente segnala che il parametro `InParam` è sia un `Object` e `Integer`:  
  
 [!code-vb[VbVbalrOOP&#94;](../../../../visual-basic/misc/codesnippet/VisualBasic/determining-object-type_3.vb)]  
  
 Nell'esempio seguente utilizza sia `TypeOf...Is` e `TypeName` per determinare il tipo di oggetto passato nel `Ctrl` argomento. Il `TestObject` le chiamate di procedura `ShowType` con tre diversi tipi di controlli.  
  
#### <a name="to-run-the-example"></a>Per eseguire l'esempio  
  
1.  Creare un nuovo progetto applicazione Windows e aggiungere un <xref:System.Windows.Forms.Button>controllo, un <xref:System.Windows.Forms.CheckBox>, controllo e un <xref:System.Windows.Forms.RadioButton>al form.</xref:System.Windows.Forms.RadioButton> </xref:System.Windows.Forms.CheckBox> </xref:System.Windows.Forms.Button>  
  
2.  Dal pulsante sul form, chiamare il `TestObject` procedura.  
  
3.  Aggiungere il codice seguente al form:  
  
     [!code-vb[&#95; VbVbalrOOP](../../../../visual-basic/misc/codesnippet/VisualBasic/determining-object-type_4.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.Information.TypeName%2A></xref:Microsoft.VisualBasic.Information.TypeName%2A>   
 [Chiamata di una proprietà o metodo mediante un nome di stringa](../../../../visual-basic/programming-guide/language-features/early-late-binding/calling-a-property-or-method-using-a-string-name.md)   
 [Tipo di dati Object](../../../../visual-basic/language-reference/data-types/object-data-type.md)   
 [If... Quindi... Else (istruzione)](../../../../visual-basic/language-reference/statements/if-then-else-statement.md)   
 [Tipo di dati String](../../../../visual-basic/language-reference/data-types/string-data-type.md)   
 [Tipo di dati Integer](../../../../visual-basic/language-reference/data-types/integer-data-type.md)
