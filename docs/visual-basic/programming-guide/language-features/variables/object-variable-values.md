---
title: "Object Variable Values (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "object variables, values"
  - "values, of object variables"
  - "data types [Visual Basic], object variable"
  - "variables [Visual Basic], object"
ms.assetid: 31555704-58a3-49f1-9a0a-6421f605664f
caps.latest.revision: 18
caps.handback.revision: 18
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Object Variable Values (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Una variabile del [Object Data Type](../../../../visual-basic/language-reference/data-types/object-data-type.md) può fare riferimento a dati di qualsiasi tipo.  Il valore memorizzato in una variabile `Object` viene conservato in un'altra posizione all'interno della memoria, mentre la variabile contiene un puntatore ai dati.  
  
## Funzioni di classificazione degli oggetti  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] fornisce funzioni che restituiscono informazioni relative agli elementi a cui una variabile `Object` si riferisce, come illustrato nella tabella seguente.  
  
|Funzione|Restituisce True se la variabile oggetto fa riferimento a|  
|--------------|---------------------------------------------------------------|  
|<xref:Microsoft.VisualBasic.Information.IsArray%2A>|Una matrice di valori invece di un singolo valore|  
|<xref:Microsoft.VisualBasic.Information.IsDate%2A>|Un valore [Date Data Type](../../../../visual-basic/language-reference/data-types/date-data-type.md) o una stringa che può essere interpretata come valore di data e ora|  
|<xref:Microsoft.VisualBasic.Information.IsDBNull%2A>|Un oggetto di tipo <xref:System.DBNull> che rappresenta dati mancanti o non esistenti|  
|<xref:Microsoft.VisualBasic.Information.IsError%2A>|Un oggetto eccezione che deriva da <xref:System.Exception>|  
|<xref:Microsoft.VisualBasic.Information.IsNothing%2A>|[Nothing](../../../../visual-basic/language-reference/nothing.md), ovvero attualmente alla variabile non è assegnato alcun oggetto|  
|<xref:Microsoft.VisualBasic.Information.IsNumeric%2A>|Un numero o una stringa che può essere interpretata come un numero|  
|<xref:Microsoft.VisualBasic.Information.IsReference%2A>|Un tipo di riferimento, quale una stringa, una matrice, un delegato o un tipo di classe|  
  
 È possibile utilizzare queste funzioni per evitare di sottoporre un valore non valido a un'operazione o a una routine.  
  
## Operatore TypeOf  
 È inoltre possibile utilizzare l'[TypeOf Operator](../../../../visual-basic/language-reference/operators/typeof-operator.md) per determinare se una variabile oggetto fa attualmente riferimento a un tipo di dati specifico.  L'espressione `TypeOf`...`Is` restituisce `True` se il tipo in fase di esecuzione dell'operando è derivato da o implementa il tipo specificato.  
  
 L'esempio che segue utilizza `TypeOf` su variabili oggetto che fanno riferimento al valore e ai tipi di riferimento.  
  
```  
' The following statement puts a value type (Integer) in an Object variable.  
Dim num As Object = 10  
' The following statement puts a reference type (Form) in an Object variable.  
Dim frm As Object = New Form()  
If TypeOf num Is Long Then Debug.WriteLine("num is Long")  
If TypeOf num Is Integer Then Debug.WriteLine("num is Integer")  
If TypeOf num Is Short Then Debug.WriteLine("num is Short")  
If TypeOf num Is Object Then Debug.WriteLine("num is Object")  
If TypeOf frm Is Form Then Debug.WriteLine("frm is Form")  
If TypeOf frm Is Label Then Debug.WriteLine("frm is Label")  
If TypeOf frm Is Object Then Debug.WriteLine("frm is Object")  
```  
  
 L'esempio precedente consente di scrivere le righe che seguono nella finestra **Debug**:  
  
 `num is Integer`  
  
 `num is Object`  
  
 `frm is Form`  
  
 `frm is Object`  
  
 La variabile oggetto `num` fa riferimento a dati di tipo `Integer`, mentre `frm` fa riferimento a un oggetto della classe <xref:System.Windows.Forms.Form>.  
  
## Matrici Object  
 È possibile dichiarare e utilizzare una matrice di variabili `Object`.  Tale matrice risulta utile quando è necessario gestire una varietà di tipi di dati e di classi di oggetti.  È necessario che tutti gli elementi in una matrice abbiano lo stesso tipo di dati dichiarato.  La dichiarazione di questo tipo di dati come `Object` consente di archiviare istanze di classe e di oggetto accanto ad altri tipi di dati nella matrice.  
  
## Vedere anche  
 [Object Variables](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)   
 [Object Variable Declaration](../../../../visual-basic/programming-guide/language-features/variables/object-variable-declaration.md)   
 [Object Variable Assignment](../../../../visual-basic/programming-guide/language-features/variables/object-variable-assignment.md)   
 [How to: Refer to the Current Instance of an Object](../../../../visual-basic/programming-guide/language-features/variables/how-to-refer-to-the-current-instance-of-an-object.md)   
 [How to: Determine What Type an Object Variable Refers To](../../../../visual-basic/programming-guide/language-features/variables/how-to-determine-what-type-an-object-variable-refers-to.md)   
 [How to: Determine Whether Two Objects Are Related](../../../../visual-basic/programming-guide/language-features/variables/how-to-determine-whether-two-objects-are-related.md)   
 [How to: Determine Whether Two Objects Are Identical](../../../../visual-basic/programming-guide/language-features/variables/how-to-determine-whether-two-objects-are-identical.md)   
 [Riepilogo dei tipi di dati](../../../../visual-basic/programming-guide/language-features/data-types/index.md)