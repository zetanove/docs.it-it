---
title: "Enumerations and Name Qualification (Visual Basic) | Microsoft Docs"
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
  - "declarations, enumerations"
  - "Imports statement, namespace declarations"
  - "declaring namespaces, enumerations"
  - "name collisions"
  - "ambiguous names, enumerations"
  - "enumerations [Visual Basic], name qualification"
  - "names, avoiding conflicts"
  - "namespaces, declaring"
  - "naming conflicts, enumerations"
  - "naming conflicts, qualifying names"
  - "declaring enumerations"
  - "references, enumeration members"
  - "naming conventions, naming conflicts"
  - "declarations, namespaces"
ms.assetid: 08ba2738-df52-4140-bc55-f57c871c9b73
caps.latest.revision: 20
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 20
---
# Enumerations and Name Qualification (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Quando si fa riferimento a un membro di un'enumerazione, è in genere necessario qualificare il nome del membro con il nome dell'enumerazione.  Per fare riferimento al membro `Sunday` dell'enumerazione `Days`, ad esempio, è necessario utilizzare la seguente sintassi:  
  
 [!code-vb[VbEnumsTask#18](../../../../visual-basic/language-reference/statements/codesnippet/visualbasic/WindowsApplication1/Class2.vb#18)]  
  
## Utilizzo dell'istruzione Imports  
 È possibile evitare l'utilizzo dei nomi completi mediante l'aggiunta dell'istruzione `Imports` nella sezione dichiarazioni dello spazio dei nomi del codice, come illustrato nell'esempio seguente:  
  
 [!code-vb[VbEnumsTask#22](../../../../visual-basic/language-reference/statements/codesnippet/visualbasic/WindowsApplication1/Class1.vb#22)]  
  
 L'istruzione `Imports` consente di importare i nomi dello spazio dei nomi da progetti e assembly a cui si fa riferimento e dall'interno dello stesso progetto del modulo in cui si trova l'istruzione.  Una volta aggiunta questa istruzione, sarà possibile fare riferimento ai membri dell'enumerazione tralasciando la qualificazione, come illustrato nell'esempio seguente:  
  
 [!code-vb[VbEnumsTask#24](../../../../visual-basic/language-reference/statements/codesnippet/visualbasic/WindowsApplication1/Class1.vb#24)]  
  
 L'organizzazione di set di costanti correlate in enumerazioni consente di utilizzare gli stessi nomi di costanti in contesti diversi.  È possibile, ad esempio, utilizzare gli stessi nomi per le costanti dei giorni della settimana nelle enumerazioni `Days` e `WorkDays`.  Quando si utilizza l'istruzione `Imports` con le enumerazioni, tuttavia, è necessario fare attenzione a evitare riferimenti ambigui.  Si consideri l'esempio seguente:  
  
 [!code-vb[VbEnumsTask#22](../../../../visual-basic/language-reference/statements/codesnippet/visualbasic/WindowsApplication1/Class1.vb#22)]  
  
 [!code-vb[VbEnumsTask#25](../../../../visual-basic/language-reference/statements/codesnippet/visualbasic/WindowsApplication1/Class1.vb#25)]  
  
 Se si suppone che `Monday` sia membro sia dell'enumerazione `Days` che dell'enumerazione `Workdays`, il codice riportato di seguito genererebbe un errore di compilazione.  Per evitare riferimenti ambigui quando si fa riferimento a una singola costante, qualificare il nome della costante indicandone l'enumerazione.  Nel codice riportato di seguito si fa riferimento alle costanti `Saturday` delle enumerazioni `Days` e `WorkDays`.  
  
 [!code-vb[VbEnumsTask#32](../../../../visual-basic/language-reference/statements/codesnippet/visualbasic/WindowsApplication1/Class2.vb#32)]  
  
## Vedere anche  
 [Constants and Enumerations](../../../../visual-basic/language-reference/constants-and-enumerations.md)   
 [How to: Declare an Enumeration](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-declare-enumerations.md)   
 [How to: Refer to an Enumeration Member](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-refer-to-an-enumeration-member.md)   
 [How to: Iterate Through An Enumeration in Visual Basic](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-iterate-through-an-enumeration.md)   
 [How to: Determine the String Associated with an Enumeration Value](../../../../visual-basic/programming-guide/language-features/constants-enums/how-to-determine-the-string-associated-with-an-enumeration-value.md)   
 [When to Use an Enumeration](../../../../visual-basic/programming-guide/language-features/constants-enums/when-to-use-an-enumeration.md)   
 [Constant and Literal Data Types](../../../../visual-basic/programming-guide/language-features/constants-enums/constant-and-literal-data-types.md)   
 [Enum Statement](../../../../visual-basic/language-reference/statements/enum-statement.md)   
 [Imports Statement \(.NET Namespace and Type\)](../../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)   
 [Data Types](../../../../visual-basic/language-reference/data-types/data-type-summary.md)