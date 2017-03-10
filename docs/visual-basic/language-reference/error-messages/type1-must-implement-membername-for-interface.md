---
title: "&lt;type1&gt;&#39;&lt;typename&gt;&#39; must implement &#39;&lt;membername&gt;&#39; for interface &#39;&lt;interfacename&gt;&#39; | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc30154"
  - "bc30154"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30154"
ms.assetid: 259afdfa-3608-4760-adcb-88ec0da5020d
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# &lt;type1&gt;&#39;&lt;typename&gt;&#39; must implement &#39;&lt;membername&gt;&#39; for interface &#39;&lt;interfacename&gt;&#39;
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

'\<nometipo\>' deve implementare '\<nomemembro\>' per l'interfaccia '\<nomeinterfaccia\>'.La proprietà che esegue l'implementazione deve avere identificatori 'ReadOnly'\/'WriteOnly' corrispondenti.  
  
 Una classe o una struttura asserisce di implementare un'interfaccia ma non implementa una routine, una proprietà o un evento definito dall'interfaccia.  È necessario che tutti i membri dell'interfaccia siano implementati.  
  
 **ID errore:** BC30154  
  
### Per correggere l'errore  
  
1.  Dichiarare un membro con lo stesso nome e la stessa firma definite nell'interfaccia.  Assicurarsi che sia inclusa almeno l'istruzione `End Function`, `End Sub` o `End Property`.  
  
2.  Aggiungere una clausola `Implements` alla fine dell'istruzione `Function`, `Sub`, `Property` o `Event`.  Di seguito è riportato un esempio:  
  
    ```  
    Public Event ItHappened() Implements IBaseInterface.ItHappened  
    ```  
  
3.  Al momento di implementare una proprietà, controllare che `ReadOnly` o `WriteOnly` sia utilizzata come nella definizione dell'interfaccia.  
  
4.  Al momento di implementare una proprietà, dichiarare le routine `Get` e `Set` nel modo appropriato.  
  
## Vedere anche  
 [Implements Statement](../../../visual-basic/language-reference/statements/implements-statement.md)   
 [Interfaces](../../../visual-basic/programming-guide/language-features/interfaces/index.md)