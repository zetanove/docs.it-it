---
title: "Of Clause (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "Of"
  - "vb.Of"
  - "vb.of"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Of keyword"
  - "arguments [Visual Basic], data types"
  - "constraints, Visual Basic generic types"
  - "generic parameters"
  - "generics [Visual Basic], constraints"
  - "parameters, type"
  - "types [Visual Basic], generic"
  - "parameters, generic"
  - "type parameters"
  - "data type arguments"
ms.assetid: 0db8f65c-65af-4089-ab7f-6fcfecb60444
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# Of Clause (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Introduce una clausola `Of` che identifica un *parametro di tipo* su una classe, una struttura, un'interfaccia, una routine o un delegato *generico*.  Per informazioni sui tipi generici, vedere [Tipi generici in Visual Basic](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md).  
  
## Utilizzo della parola chiave Of  
 Nell'esempio di codice riportato di seguito la parola chiave `Of` viene utilizzata per definire la struttura di una classe che accetta due parametri di tipo.  Tale parola chiave *vincola* il parametro `keyType` tramite l'interfaccia <xref:System.IComparable> e pertanto il codice utilizzato deve fornire un argomento di tipo per l'implementazione di <xref:System.IComparable>.  Questa operazione è necessaria per consentire alla routine `add` di effettuare una chiamata al metodo <xref:System.IComparable.CompareTo%2A?displayProperty=fullName>.  Per ulteriori informazioni sui vincoli, vedere [Type List](../../../visual-basic/language-reference/statements/type-list.md).  
  
```  
Public Class Dictionary(Of entryType, keyType As IComparable)  
    Public Sub add(ByVal e As entryType, ByVal k As keyType)  
        Dim dk As keyType  
        If k.CompareTo(dk) = 0 Then  
        End If  
    End Sub  
    Public Function find(ByVal k As keyType) As entryType  
    End Function  
End Class  
```  
  
 Dopo aver completato la precedente definizione di classe, è possibile costruire a partire da quest'ultima una serie di classi `dictionary`.  I tipi forniti a `entryType` e `keyType` determinano il tipo di voce contenuto nella classe, nonché il tipo di chiave associato a ciascuna voce.  A causa del vincolo, è necessario fornire a `keyType` un tipo per l'implementazione dell'interfaccia <xref:System.IComparable>.  
  
 Nell'esempio di codice riportato di seguito viene creato un oggetto contenente voci `String` che associa a ciascuna voce una chiave `Integer`.  `Integer` implementa <xref:System.IComparable> e in tal modo soddisfa il vincolo definito su `keyType`.  
  
```  
Dim d As New dictionary(Of String, Integer)  
```  
  
 È possibile utilizzare la parola chiave `Of` nei seguenti contesti:  
  
 [Istruzione Class](../../../visual-basic/language-reference/statements/class-statement.md)  
  
 [Istruzione Delegate](../../../visual-basic/language-reference/statements/delegate-statement.md)  
  
 [Istruzione Function](../../../visual-basic/language-reference/statements/function-statement.md)  
  
 [Istruzione Interface](../../../visual-basic/language-reference/statements/interface-statement.md)  
  
 [Istruzione Structure](../../../visual-basic/language-reference/statements/structure-statement.md)  
  
 [Istruzione Sub](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## Vedere anche  
 <xref:System.IComparable>   
 [Type List](../../../visual-basic/language-reference/statements/type-list.md)   
 [Tipi generici in Visual Basic](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [In](../../../visual-basic/language-reference/modifiers/in-generic-modifier.md)   
 [Out](../../../visual-basic/language-reference/modifiers/out-generic-modifier.md)