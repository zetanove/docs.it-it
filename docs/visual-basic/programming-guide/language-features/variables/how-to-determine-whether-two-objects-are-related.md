---
title: "How to: Determine Whether Two Objects Are Related (Visual Basic) | Microsoft Docs"
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
  - "inheritance, Visual Basic objects"
  - "objects [Visual Basic], inheritance"
  - "object variables, determining relation"
ms.assetid: da002e3f-6616-4bad-a229-f842d06652bb
caps.latest.revision: 7
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 7
---
# How to: Determine Whether Two Objects Are Related (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

È possibile confrontare due oggetti per determinare l'eventuale relazione tra le classi da cui vengono creati.  Il metodo <xref:System.Type.IsInstanceOfType%2A> della classe <xref:System.Type?displayProperty=fullName> restituisce `True` se la classe specificata eredita da quella corrente o se il tipo corrente è un'interfaccia supportata dalla classe specificata.  
  
### Per determinare se un oggetto eredita dalla classe o dall'interfaccia di un altro oggetto  
  
1.  Richiamare il metodo <xref:System.Object.GetType%2A> sull'oggetto che può essere considerato del tipo base.  
  
2.  Richiamare il metodo <xref:System.Type.IsInstanceOfType%2A> sull'oggetto <xref:System.Type?displayProperty=fullName> restituito da <xref:System.Object.GetType%2A>,  
  
3.  Specificare l'oggetto che può essere del tipo derivato nell'elenco degli argomenti di <xref:System.Type.IsInstanceOfType%2A>.  
  
     <xref:System.Type.IsInstanceOfType%2A> restituisce `True` se il relativo tipo di argomento eredita dal tipo di oggetto <xref:System.Type?displayProperty=fullName>.  
  
## Esempio  
 Nell'esempio che segue viene determinato se un oggetto rappresenta una classe derivata dalla classe di un altro oggetto.  
  
```  
Public Class baseClass  
End Class  
Public Class derivedClass : Inherits baseClass  
End Class  
Public Class testTheseClasses  
    Public Sub seeIfRelated()  
        Dim baseObj As Object = New baseClass()  
        Dim derivedObj As Object = New derivedClass()  
        Dim related As Boolean  
        related = baseObj.GetType().IsInstanceOfType(derivedObj)  
        MsgBox(CStr(related))  
    End Sub  
End Class  
```  
  
 Si osservi la posizione imprevista delle due variabili oggetto nella chiamata a <xref:System.Type.IsInstanceOfType%2A>.  Il tipo base previsto viene utilizzato per generare la classe <xref:System.Type?displayProperty=fullName> e il tipo derivato previsto viene passato come argomento al metodo <xref:System.Type.IsInstanceOfType%2A>.  
  
## Vedere anche  
 <xref:System.Object.GetType%2A>   
 <xref:System.Type?displayProperty=fullName>   
 <xref:System.Type.IsInstanceOfType%2A>   
 [Object Data Type](../../../../visual-basic/language-reference/data-types/object-data-type.md)   
 [Object Variables](../../../../visual-basic/programming-guide/language-features/variables/object-variables.md)   
 [Object Variable Values](../../../../visual-basic/programming-guide/language-features/variables/object-variable-values.md)   
 [How to: Determine Whether Two Objects Are Identical](../../../../visual-basic/programming-guide/language-features/variables/how-to-determine-whether-two-objects-are-identical.md)