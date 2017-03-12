---
title: "Other Control Structures (Visual Basic) | Microsoft Docs"
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
  - "statements [Visual Basic], control flow"
  - "control structures"
ms.assetid: 24b811f7-98ba-40ec-8dd3-4d528cfa4574
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# Other Control Structures (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

In [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] sono disponibili strutture di controllo che consentono di eliminare una risorsa o di ridurre il numero di volte in cui è necessario ripetere un riferimento a un oggetto.  
  
## Costruzione Using...End Using  
 La costruzione `Using...End Using` definisce un blocco di istruzioni all'interno del quale viene utilizzata una risorsa quale una connessione SQL.  È possibile eventualmente acquisire la risorsa mediante l'istruzione `Using`.  Quando si esce dal blocco `Using`, [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] elimina automaticamente la risorsa in modo da renderla disponibile per l'utilizzo in un altro codice.  La risorsa deve essere locale ed eliminabile.  Per ulteriori informazioni, vedere [Using Statement](../../../../visual-basic/language-reference/statements/using-statement.md).  
  
## Costruzione With...End With  
 La costruzione `With...End With` consente di specificare un riferimento a un oggetto una sola volta e di eseguire quindi una serie di istruzioni che accedono ai membri del riferimento.  Ciò consente di semplificare il codice e migliorare le prestazioni, poiché non è necessario che [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] definisca nuovamente il riferimento per ciascuna istruzione che accede a tale riferimento.  Per ulteriori informazioni, vedere [With...End With Statement](../../../../visual-basic/language-reference/statements/with-end-with-statement.md).  
  
## Vedere anche  
 [Control Flow](../../../../visual-basic/programming-guide/language-features/control-flow/index.md)   
 [Decision Structures](../../../../visual-basic/programming-guide/language-features/control-flow/decision-structures.md)   
 [Loop Structures](../../../../visual-basic/programming-guide/language-features/control-flow/loop-structures.md)   
 [Nested Control Structures](../../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md)   
 [Using Statement](../../../../visual-basic/language-reference/statements/using-statement.md)   
 [With...End With Statement](../../../../visual-basic/language-reference/statements/with-end-with-statement.md)