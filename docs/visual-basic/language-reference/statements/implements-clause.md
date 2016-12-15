---
title: "Implements Clause (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.ImplementsClause"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "interface implementation, reimplementation"
  - "interface members, reimplementation"
  - "interface members, Implements keyword"
  - "interface members"
  - "members, reimplementation"
  - "interface implementation, Implements keyword"
  - "interface members, implementing"
  - "Implements keyword"
  - "Implements statement, about Implements"
  - "members, implementing"
  - "members, Implements keyword"
  - "reimplementation"
ms.assetid: 5252cdf9-964d-4fc6-af0f-0449b7126b5a
caps.latest.revision: 15
caps.handback.revision: 15
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Implements Clause (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Indica che un membro di classe o di struttura fornisce l'implementazione per un membro definito in un'interfaccia.  
  
## Note  
 La parola chiave `Implements` non corrisponde all'[Implements Statement](../../../visual-basic/language-reference/statements/implements-statement.md).  L'istruzione `Implements` consente di specificare che una classe o una struttura implementa una o più interfacce e pertanto per ciascun membro si utilizza la parola chiave `Implements` per specificare l'interfaccia e il membro da implementare.  
  
 Se una classe o una struttura implementa un'interfaccia, l'istruzione `Implements` deve essere inclusa subito dopo l'[Class Statement](../../../visual-basic/language-reference/statements/class-statement.md) o l'[Structure Statement](../../../visual-basic/language-reference/statements/structure-statement.md). Tutti i membri definiti dall'interfaccia, inoltre, devono essere implementati.  
  
## Reimplementazione  
 In una classe derivata è possibile reimplementare un membro di interfaccia già implementato dalla classe base.  Questa operazione è diversa dall'override del membro della classe base per quanto riguarda i seguenti aspetti:  
  
-   Non è necessario che il membro della classe base sia [Overridable](../../../visual-basic/language-reference/modifiers/overridable.md) per essere reimplementato.  
  
-   È possibile reimplementare il membro con un nome diverso.  
  
 È possibile utilizzare la parola chiave `Implements` nei seguenti contesti:  
  
 [Event Statement](../../../visual-basic/language-reference/statements/event-statement.md)  
  
 [Function Statement](../../../visual-basic/language-reference/statements/function-statement.md)  
  
 [Property Statement](../../../visual-basic/language-reference/statements/property-statement.md)  
  
 [Sub Statement](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## Vedere anche  
 [Implements Statement](../../../visual-basic/language-reference/statements/implements-statement.md)   
 [Interface Statement](../../../visual-basic/language-reference/statements/interface-statement.md)   
 [Class Statement](../../../visual-basic/language-reference/statements/class-statement.md)   
 [Structure Statement](../../../visual-basic/language-reference/statements/structure-statement.md)