---
title: "First statement of this &#39;Sub New&#39; must be an explicit call to &#39;MyBase.New&#39; or &#39;MyClass.New&#39; because the &#39;&lt;constructorname&gt;&#39; in the base class &#39;&lt;baseclassname&gt;&#39; of &#39;&lt;derivedclassname&gt;&#39; is marked obsolete: &#39;&lt;errormessage&gt;&#39; | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vbc30920"
  - "bc30920"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30920"
ms.assetid: e47dc755-4294-4368-b813-2177b7677957
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# First statement of this &#39;Sub New&#39; must be an explicit call to &#39;MyBase.New&#39; or &#39;MyClass.New&#39; because the &#39;&lt;constructorname&gt;&#39; in the base class &#39;&lt;baseclassname&gt;&#39; of &#39;&lt;derivedclassname&gt;&#39; is marked obsolete: &#39;&lt;errormessage&gt;&#39;
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Un costruttore di classi non chiama in modo esplicito un costruttore di classi base, il costruttore di classi base implicito è contrassegnato con l'attributo <xref:System.ObsoleteAttribute> e l'istruzione per elaborarlo come errore.  
  
 Quando un costruttore di classi derivate non chiama un costruttore di classi base, in [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] viene generata una chiamata implicita a un costruttore di classi base senza parametri.  Se la classe base non contiene costruttori accessibili che possono essere chiamati senza argomenti, non è possibile generare alcuna chiamata implicita.  In questo caso, il costruttore richiesto è contrassegnato dall'attributo <xref:System.ObsoleteAttribute>, quindi non potrà essere chiamato da [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)].  
  
 Per contrassegnare un elemento di programmazione come non più in uso, applicare <xref:System.ObsoleteAttribute> all'elemento.  In questo caso sarà possibile impostare la proprietà <xref:System.ObsoleteAttribute.IsError%2A> dell'attributo su `True` o `False`.  Se il valore viene impostato su `True`, il compilatore considererà come errore un tentativo di utilizzare l'elemento.  Se il valore viene impostato su `False` o viene mantenuto il valore predefinito di `False`, il compilatore visualizzerà un avviso in caso di tentativo di utilizzare l'elemento.  
  
 **ID errore:** BC30920  
  
### Per correggere l'errore  
  
1.  Esaminare il messaggio di errore indicato ed eseguire le operazioni necessarie.  
  
2.  Includere una chiamata a `MyBase.New()` o a `MyClass.New()` come prima istruzione di`Sub New` nella classe derivata.  
  
## Vedere anche  
 [Attributi](../Topic/Attributes%20\(C%23%20and%20Visual%20Basic\).md)