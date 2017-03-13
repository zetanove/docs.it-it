---
title: "How to: Pass Arguments to a Procedure (Visual Basic) | Microsoft Docs"
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
  - "arguments [Visual Basic], passing to procedures"
  - "procedures, arguments"
  - "procedures, parameters"
  - "procedure arguments"
  - "Visual Basic code, procedures"
  - "procedure parameters"
  - "procedures, calling"
  - "argument passing, procedures"
ms.assetid: 08723588-3890-4ddc-8249-79e049e0f241
caps.latest.revision: 14
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 14
---
# How to: Pass Arguments to a Procedure (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Quando si effettua una chiamata a una routine, dopo il nome di quest'ultima viene inserito un elenco di argomenti tra parentesi.  Viene fornito un argomento corrispondente a ogni parametro obbligatorio definito dalla routine e facoltativamente è possibile fornire argomenti ai parametri `Optional`.  Se nella chiamata non viene fornito un parametro `Optional`, è necessario includere una virgola per contrassegnarne la posizione nell'elenco degli argomenti nel caso in cui si forniscano argomenti successivi.  
  
 Se si intende passare un argomento di un tipo di dati diverso dal relativo parametro corrispondente, ad esempio da `Byte` a `String`, è possibile impostare l'opzione per il controllo dei tipi \([Option Strict Statement](../../../../visual-basic/language-reference/statements/option-strict-statement.md)\) su `Off`.  Se l'opzione `Option Strict` è impostata su `On`, è necessario utilizzare conversioni verso un tipo di dati più grande o parole chiave di conversione esplicita.  Per ulteriori informazioni, vedere [Widening and Narrowing Conversions](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md) e [Type Conversion Functions](../../../../visual-basic/language-reference/functions/type-conversion-functions.md).  
  
 Per ulteriori informazioni, vedere [Procedure Parameters and Arguments](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md).  
  
### Per passare uno o più argomenti a una routine  
  
1.  Nell'istruzione chiamante inserire le parentesi dopo il nome della routine.  
  
2.  Inserire all'interno delle parentesi un elenco di argomenti.  Includere un argomento per ciascun parametro obbligatorio definito dalla routine e separare gli argomenti con virgole.  
  
3.  Assicurarsi che ciascun argomento sia un'espressione valida in grado di restituire un tipo di dati convertibile nel tipo definito dalla routine per il parametro corrispondente.  
  
4.  Se un parametro viene definito come [Optional](../../../../visual-basic/language-reference/modifiers/optional.md), è possibile includerlo nell'elenco degli argomenti oppure ometterlo.  Se viene omesso, la routine utilizza il valore predefinito specificato per tale parametro.  
  
5.  Se si omette un argomento per un parametro `Optional` seguito da un altro parametro nell'elenco dei parametri, è possibile contrassegnare la posizione dell'argomento omesso inserendo un'altra virgola nell'elenco degli argomenti.  
  
     Nell'esempio seguente viene chiamata la funzione <xref:Microsoft.VisualBasic.Interaction.MsgBox%2A> [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)].  
  
     [!code-vb[VbVbcnProcedures#34](./codesnippet/VisualBasic/how-to-pass-arguments-to-a-procedure_1.vb)]  
  
     Nell'esempio precedente viene fornito il primo argomento obbligatorio, che è la stringa di messaggio da visualizzare.  Viene omesso un argomento relativo al secondo parametro facoltativo, che specifica i pulsanti da visualizzare nella finestra di messaggio.  Poiché la chiamata non fornisce alcun valore, `MsgBox` utilizza il valore predefinito `MsgBoxStyle.OKOnly`, che visualizza solo un pulsante **OK**.  
  
     La seconda virgola nell'elenco degli argomenti contrassegna la posizione del secondo argomento omesso, mentre l'ultima stringa viene passata al terzo parametro facoltativo di `MsgBox`, che è il testo da visualizzare nella barra del titolo.  
  
## Vedere anche  
 [Sub Procedures](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md)   
 [Routine Function](../../../../visual-basic/programming-guide/language-features/procedures/function-procedures.md)   
 [Routine Property](../../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [Operator Procedures](../../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)   
 [How to: Define a Parameter for a Procedure](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-parameter-for-a-procedure.md)   
 [Passing Arguments by Value and by Reference](../../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)   
 [Recursive Procedures](../../../../visual-basic/programming-guide/language-features/procedures/recursive-procedures.md)   
 [Procedure Overloading](../../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)   
 [Objects and Classes](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)   
 [Programmazione orientata ad oggetti](../Topic/Object-Oriented%20Programming%20\(C%23%20and%20Visual%20Basic\).md)