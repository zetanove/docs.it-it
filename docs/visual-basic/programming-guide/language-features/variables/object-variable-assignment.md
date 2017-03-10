---
title: "Object Variable Assignment (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Nothing keyword, object variable assignment"
  - "object variables, initializing"
  - "variables [Visual Basic], initializing"
  - "objects [Visual Basic], current instance"
  - "object variables, assigning"
  - "variables [Visual Basic], object variables"
  - "current instance, defined"
  - "variables [Visual Basic], assigning"
  - "assignment statements, object variable assignment"
  - "Me keyword, as object variable"
ms.assetid: 3706811d-fd40-44fe-8727-d692e8e55d6d
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# Object Variable Assignment (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Per assegnare un oggetto a una variabile oggetto si utilizza generalmente una normale istruzione di assegnazione.  È possibile assegnare un'espressione dell'oggetto o la parola chiave [Nothing](../../../../visual-basic/language-reference/nothing.md), come illustrato nell'esempio che segue.  
  
```  
Dim thisObject As Object  
' The following statement assigns an object reference.  
thisObject = Form1  
' The following statement discontinues association with any object.  
thisObject = Nothing  
```  
  
 `Nothing` indica che attualmente alla variabile non è assegnato alcun oggetto.  
  
## Inizializzazione  
 Quando il codice inizia l'esecuzione, le variabili oggetto vengono inizializzate a `Nothing`.  Le variabili, le cui dichiarazioni includono l'inizializzazione, vengono reinizializzate in base ai valori specificati al momento dell'esecuzione delle istruzioni di dichiarazione.  
  
 È possibile includere l'inizializzazione nella dichiarazione utilizzando la parola chiave [New](../../../../visual-basic/language-reference/operators/new-operator.md).  Le istruzioni di dichiarazione seguenti consentono di dichiarare le variabili oggetto `testUri` e `ver` e di assegnare a tali variabili oggetti specifici.  Ciascuna istruzione utilizza i costruttori con overload della classe appropriata per inizializzare l'oggetto.  
  
```  
Dim testUri As New System.Uri("http://www.microsoft.com")  
Dim ver As New System.Version(6, 1, 0)  
```  
  
## Dissociazione  
 L'impostazione di una variabile oggetto su `Nothing` interrompe l'associazione delle variabili con oggetti specifici.  Questo impedisce di modificare involontariamente l'oggetto modificando la variabile  e consente di controllare se la variabile oggetto punta a un oggetto valido, come nell'esempio che segue.  
  
```  
If otherObject IsNot Nothing Then  
    ' otherObject refers to a valid object, so your code can use it.  
End If  
```  
  
 Se l'oggetto cui la variabile si riferisce si trova in un'altra applicazione, questo controllo non può determinare se l'applicazione è stata chiusa o ha semplicemente invalidato l'oggetto.  
  
 Una variabile oggetto con valore `Nothing` viene definita anche *riferimento null*.  
  
## Istanza corrente  
 L'*istanza corrente* di un oggetto è l'istanza nella quale il codice è attualmente in esecuzione.  Poiché tutto il codice viene eseguito all'interno di una routine, l'istanza corrente è quella nella quale è stata richiamata la routine.  
  
 La parola chiave `Me` funge da variabile oggetto che fa riferimento all'istanza corrente.  Se una routine non è [Shared](../../../../visual-basic/language-reference/modifiers/shared.md), può utilizzare la parola chiave `Me` per ottenere un puntatore all'istanza corrente.  Le routine condivise non possono essere associate a un'istanza specifica di una classe.  
  
 L'utilizzo della parola chiave `Me` è particolarmente utile per il passaggio dell'istanza corrente a una routine in un altro modulo.  Si supponga, ad esempio, di disporre di un certo numero di documenti XML a cui si desidera aggiungere testo standard.  Nell'esempio che segue viene definita la routine che consente di eseguire tale operazione.  
  
```  
Sub addStandardText(XmlDoc As System.Xml.XmlDocument)  
    XmlDoc.CreateTextNode("This text goes into every XML document.")  
End Sub  
```  
  
 Ogni oggetto del documento XML può quindi chiamare la routine e passare la rispettiva istanza corrente come argomento.  Nell'esempio che segue viene illustrato quanto descritto.  
  
```  
addStandardText(Me)  
```  
  
## Vedere anche  
 [Object Variables](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)   
 [Object Variable Declaration](../../../../visual-basic/programming-guide/language-features/variables/object-variable-declaration.md)   
 [Object Variable Values](../../../../visual-basic/programming-guide/language-features/variables/object-variable-values.md)   
 [How to: Declare an Object Variable and Assign an Object to It in Visual Basic](../../../../visual-basic/programming-guide/language-features/variables/how-to-declare-an-object-variable-and-assign-an-object-to-it.md)   
 [How to: Make an Object Variable Not Refer to Any Instance](../../../../visual-basic/programming-guide/language-features/variables/how-to-make-an-object-variable-not-refer-to-any-instance.md)   
 [Me, My, MyBase, and MyClass](../../../../visual-basic/programming-guide/program-structure/me-my-mybase-and-myclass.md)