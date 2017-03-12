---
title: "Expression has the type &#39;&lt;typename&gt;&#39; which is a restricted type and cannot be used to access members inherited from &#39;Object&#39; or &#39;ValueType&#39; | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc31393"
  - "vbc31393"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC31393"
ms.assetid: 2963cf3f-c527-4aa7-b67c-ee80b6d23186
caps.latest.revision: 6
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 6
---
# Expression has the type &#39;&lt;typename&gt;&#39; which is a restricted type and cannot be used to access members inherited from &#39;Object&#39; or &#39;ValueType&#39;
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Un'espressione restituisce un tipo di cui Common Language Runtime \(CLR\) non può essere il boxing ma accede a un membro che richiede tale operazione.  
  
 Il termine *Boxing* indica il processo di elaborazione necessario per la conversione di un tipo in `Object` oppure <xref:System.ValueType>.  Common Language Runtime non supporta il boxing di alcuni tipi di strutture, quali <xref:System.ArgIterator>, <xref:System.RuntimeArgumentHandle> e <xref:System.TypedReference>.  
  
 Questa espressione tenta di utilizzare il tipo limitato per chiamare un metodo ereditato dalla classe <xref:System.Object> o <xref:System.ValueType>, quali <xref:System.Object.GetHashCode%2A> o <xref:System.Object.ToString%2A>.  Per accedere a questo metodo, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] ha tentato una conversione boxing implicita che causa questo errore.  
  
 **ID errore:** BC31393  
  
### Per correggere l'errore  
  
1.  Individuare l'espressione che restituisce il tipo citato.  
  
2.  Individuare la parte di istruzione che tenta di chiamare il metodo ereditato dalla classe <xref:System.Object> o <xref:System.ValueType>.  
  
3.  Riscrivere l'istruzione in modo da impedire la chiamata al metodo.  
  
## Vedere anche  
 [Implicit and Explicit Conversions](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)