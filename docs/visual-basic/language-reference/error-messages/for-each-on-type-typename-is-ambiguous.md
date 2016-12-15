---
title: "&#39;For Each&#39; on type &#39;&lt;typename&gt;&#39; is ambiguous because the type implements multiple instantiations of &#39;System.Collections.Generic.IEnumerable(Of T)&#39; | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vbc32096"
  - "bc32096"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC32096"
ms.assetid: ed20d09c-913f-482e-89f8-c0a596c3ec24
caps.latest.revision: 7
caps.handback.revision: 7
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# &#39;For Each&#39; on type &#39;&lt;typename&gt;&#39; is ambiguous because the type implements multiple instantiations of &#39;System.Collections.Generic.IEnumerable(Of T)&#39;
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Un'istruzione `For Each` specifica una variabile di iteratore che dispone di più metodi <xref:System.Collections.IEnumerable.GetEnumerator%2A>.  
  
 È necessario che la variabile iteratore sia di un tipo che implementi l'interfaccia <xref:System.Collections.IEnumerable?displayProperty=fullName> o <xref:System.Collections.Generic.IEnumerable%601?displayProperty=fullName> in uno degli spazi dei nomi `Collections` di [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)].  È possibile implementare in una classe più interfacce generiche costruite utilizzando un argomento di tipo diverso per ogni costruzione.  Tuttavia, se una classe con queste implementazioni viene utilizzata per la variabile di iteratore, quest'ultima disporrà di più metodi <xref:System.Collections.IEnumerable.GetEnumerator%2A>.  In questo caso, non è possibile scegliere il metodo da chiamare.  
  
 **ID errore:** BC32096  
  
### Per correggere l'errore  
  
-   Utilizzare [DirectCast Operator](../../../visual-basic/language-reference/operators/directcast-operator.md) o [TryCast Operator](../../../visual-basic/language-reference/operators/trycast-operator.md) per eseguire il cast del tipo di variabile iteratore nell'interfaccia che definisce il metodo <xref:System.Collections.IEnumerable.GetEnumerator%2A> che si desidera utilizzare.  
  
## Vedere anche  
 [Istruzione For Each...Next](../../../visual-basic/language-reference/statements/for-each-next-statement.md)   
 [Interfaces](../../../visual-basic/programming-guide/language-features/interfaces/index.md)