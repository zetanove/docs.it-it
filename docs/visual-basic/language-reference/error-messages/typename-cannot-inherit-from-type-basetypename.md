---
title: "&#39;&lt;typename&gt;&#39; cannot inherit from &lt;type&gt; &#39;&lt;basetypename&gt;&#39; because it expands the access of the base &lt;type&gt; outside the assembly | Microsoft Docs"
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
  - "vbc30910"
  - "bc30910"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30910"
ms.assetid: 68fc05c5-5d55-4742-9a3b-ea04312594f4
caps.latest.revision: 8
caps.handback.revision: 8
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# &#39;&lt;typename&gt;&#39; cannot inherit from &lt;type&gt; &#39;&lt;basetypename&gt;&#39; because it expands the access of the base &lt;type&gt; outside the assembly
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Una classe o un'intefaccia eredita da una classe o un'interfaccia base, ma ha un livello di accesso meno restrittivo.  
  
 Ad esempio, un'interfaccia `Public` eredita da un'interfaccia `Friend` oppure una classe `Protected` eredita da una classe `Private`.  In questo modo la classe o l'interfaccia base viene esposta a un accesso superiore al livello previsto.  
  
 **ID errore:** BC30910  
  
### Per correggere l'errore  
  
-   Cambiare il livello di accesso della classe o dell'interfaccia derivata rendendolo restrittivo almeno quanto quello della classe o dell'interfaccia base.  
  
     In alternativa  
  
-   Se il livello di accesso meno restrittivo è necessario, rimuovere l'istruzione `Inherits`.  Non è possibile ereditare da una classe o un'interfaccia base più restrittiva.  
  
## Vedere anche  
 [Class Statement](../../../visual-basic/language-reference/statements/class-statement.md)   
 [Interface Statement](../../../visual-basic/language-reference/statements/interface-statement.md)   
 [Inherits Statement](../../../visual-basic/language-reference/statements/inherits-statement.md)   
 [Access Levels in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)