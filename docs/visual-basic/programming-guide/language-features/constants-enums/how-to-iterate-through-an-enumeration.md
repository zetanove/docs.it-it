---
title: "How to: Iterate Through An Enumeration in Visual Basic | Microsoft Docs"
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
  - "arrays [Visual Basic], iterating"
  - "enumerations [Visual Basic], iterating"
  - "ListBox control [Windows Forms], populating from an enumeration"
ms.assetid: e5aa10eb-cfcd-4a3b-8e76-f06b8f2002be
caps.latest.revision: 20
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 20
---
# How to: Iterate Through An Enumeration in Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Le enumerazioni costituiscono un comodo mezzo per utilizzare set di costanti correlate e di associare i valori costanti a nomi.  Per scorrere un'enumerazione, è possibile spostarla in una matrice mediante il metodo <xref:System.Enum.GetValues%2A> oppure utilizzare un'istruzione `For...Each` servendosi del metodo <xref:System.Enum.GetNames%2A> o <xref:System.Enum.GetValues%2A> per estrarre il valore stringa o numerico.  
  
### Per scorrere un'enumerazione  
  
-   Dichiarare una matrice in cui convertire l'enumerazione con il metodo <xref:System.Enum.GetValues%2A> prima di passare la matrice come con qualsiasi altra variabile.  Nell'esempio riportato di seguito viene visualizzato ogni membro dell'enumerazione <xref:Microsoft.VisualBasic.FirstDayOfWeek> mentre si scorre l'enumerazione.  
  
     [!code-vb[VbEnumsTask#7](../../../../visual-basic/language-reference/statements/codesnippet/visualbasic/WindowsApplication1/Class2.vb#7)]  
  
## Vedere anche  
 [Enumerations Overview](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-overview.md)   
 [How to: Declare an Enumeration](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-enumerations.md)   
 [When to Use an Enumeration](../../../../visual-basic/programming-guide/language-features/constants-enums/when-to-use-an-enumeration.md)   
 [How to: Determine the String Associated with an Enumeration Value](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-determine-the-string-associated-with-an-enumeration-value.md)   
 [How to: Refer to an Enumeration Member](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-refer-to-an-enumeration-member.md)   
 [Enumerations and Name Qualification](../../../../visual-basic/programming-guide/language-features/constants-enums/enumerations-and-name-qualification.md)   
 [Matrici](../../../../visual-basic/programming-guide/language-features/arrays/index.md)