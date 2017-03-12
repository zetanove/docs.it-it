---
title: "&lt;type1&gt;&#39;&lt;typename&gt;&#39; must implement &#39;&lt;methodname&gt;&#39; for interface &#39;&lt;interfacename&gt;&#39; | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc30149"
  - "bc30149"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30149"
ms.assetid: 29d1b7f4-dca7-478c-bbe7-c657f342c183
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# &lt;type1&gt;&#39;&lt;typename&gt;&#39; must implement &#39;&lt;methodname&gt;&#39; for interface &#39;&lt;interfacename&gt;&#39;
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Una classe o una struttura asserisce di implementare un'interfaccia ma non implementa una routine definita dall'interfaccia.  È necessario che tutti i membri dell'interfaccia siano implementati.  
  
 **ID errore:** BC30149  
  
### Per correggere l'errore  
  
1.  Dichiarare una routine con lo stesso nome e la stessa firma definite nell'interfaccia.  Accertarsi che sia inclusa almeno l'istruzione `End Function` o `End Sub`.  
  
2.  Aggiungere una clausola `Implements` alla fine dell'istruzione `Function` o `Sub`.  Di seguito è riportato un esempio:  
  
    ```  
    Public Sub DoSomething() Implements IBaseInterface.DoSomething  
    ```  
  
## Vedere anche  
 [Implements Statement](../../../visual-basic/language-reference/statements/implements-statement.md)   
 [Interfaces](../../../visual-basic/programming-guide/language-features/interfaces/index.md)