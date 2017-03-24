---
title: "How to: Determine the String Associated with an Enumeration Value (Visual Basic) | Microsoft Docs"
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
  - "enumerations [Visual Basic]"
  - "strings [Visual Basic], enumeration values"
  - "values, enumeration members"
ms.assetid: 9253e7c8-579c-49a2-8f26-392b20ea99eb
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# How to: Determine the String Associated with an Enumeration Value (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

I metodi <xref:System.Enum.GetValues%2A> e <xref:System.Enum.GetNames%2A> consentono di determinare le stringhe e i valori associati a membri di enumerazione.  
  
### Per determinare la stringa associata a un'enumerazione  
  
-   Utilizzare il metodo <xref:System.Enum.GetNames%2A> per recuperare le stringhe associate ai membri di enumerazione.  Nell'esempio riportato di seguito viene dichiarata l'enumerazione `flavorEnum`, quindi viene utilizzato il metodo <xref:System.Enum.GetNames%2A> per visualizzare le stringhe associate a ciascun membro.  
  
     [!code-vb[VbEnumsTask#2](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/how-to-determine-the-string-associated-with-an-enumeration-value_1.vb)]  
  
## Vedere anche  
 <xref:System.Enum.GetValues%2A>   
 <xref:System.Enum.GetNames%2A>   
 <xref:System.Enum>   
 [How to: Declare an Enumeration](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-enumerations.md)   
 [How to: Refer to an Enumeration Member](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-refer-to-an-enumeration-member.md)   
 [Enumerations and Name Qualification](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md)   
 [How to: Iterate Through An Enumeration in Visual Basic](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-iterate-through-an-enumeration.md)   
 [When to Use an Enumeration](../../../../visual-basic/programming-guide/language-features/constants-enums/when-to-use-an-enumeration.md)   
 [Enum Statement](../../../../visual-basic/language-reference/statements/enum-statement.md)