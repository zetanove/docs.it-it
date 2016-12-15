---
title: "&#39;&lt;elementname&gt;&#39; is obsolete (Visual Basic Warning) | Microsoft Docs"
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
  - "vbc40008"
  - "bc40008"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC40008"
ms.assetid: 729e3eb5-76ac-4c55-9fdd-78350e0de55e
caps.latest.revision: 12
caps.handback.revision: 12
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# &#39;&lt;elementname&gt;&#39; is obsolete (Visual Basic Warning)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Un'istruzione tenta di accedere a un elemento di programmazione contrassegnato con l'attributo <xref:System.ObsoleteAttribute> e la direttiva di considerarlo un avviso.  
  
 Per contrassegnare un elemento di programmazione come non più in uso, applicare <xref:System.ObsoleteAttribute> all'elemento.  In questo caso sarà possibile impostare la proprietà <xref:System.ObsoleteAttribute.IsError%2A> dell'attributo su `True` o `False`.  Se il valore viene impostato su `True`, il compilatore considererà come errore un tentativo di utilizzare l'elemento.  Se il valore viene impostato su `False` o viene mantenuto il valore predefinito di `False`, il compilatore visualizzerà un avviso in caso di tentativo di utilizzare l'elemento.  
  
 Per impostazione predefinita, questo messaggio è un avviso perché la proprietà <xref:System.ObsoleteAttribute.IsError%2A> di <xref:System.ObsoleteAttribute> è `False`.  Per ulteriori informazioni su come nascondere gli avvisi o considerarli come errori, vedere [Configurazione degli avvisi in Visual Basic](/visual-studio/ide/configuring-warnings-in-visual-basic).  
  
 **ID errore:** BC40008  
  
### Per correggere l'errore  
  
-   Assicurarsi che il riferimento al nome dell'elemento nel codice sorgente sia stato digitato correttamente.  
  
## Vedere anche  
 [Attributi](../Topic/Attributes%20\(C%23%20and%20Visual%20Basic\).md)