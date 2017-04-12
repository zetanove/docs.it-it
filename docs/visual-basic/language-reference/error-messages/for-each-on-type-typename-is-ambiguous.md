---
title: "&quot;For Each&quot; sul tipo &quot;&lt;typename&gt;&quot; è ambiguo perché il tipo implementa più creazioni di istanze di &quot;IEnumerable (Of T)&quot; | Documenti di Microsoft"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vbc32096
- bc32096
dev_langs:
- VB
helpviewer_keywords:
- BC32096
ms.assetid: ed20d09c-913f-482e-89f8-c0a596c3ec24
caps.latest.revision: 7
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 6177b48cdc3bc4085cecb6d73c164684ef1c0bc6
ms.lasthandoff: 03/13/2017

---
# <a name="39for-each39-on-type-39lttypenamegt39-is-ambiguous-because-the-type-implements-multiple-instantiations-of-39systemcollectionsgenericienumerableof-t39"></a>'For Each' sul tipo '&lt;typename&gt;' è ambiguo perché il tipo implementa più creazioni di istanze di 'IEnumerable (Of T)'
Oggetto `For Each` istruzione specifica una variabile di iteratore che è presenti più <xref:System.Collections.IEnumerable.GetEnumerator%2A>metodo.</xref:System.Collections.IEnumerable.GetEnumerator%2A>  
  
 La variabile di iteratore deve essere di un tipo che implementa il <xref:System.Collections.IEnumerable?displayProperty=fullName>o <xref:System.Collections.Generic.IEnumerable%601?displayProperty=fullName>interfaccia in uno del `Collections` gli spazi dei nomi di [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)].</xref:System.Collections.Generic.IEnumerable%601?displayProperty=fullName> </xref:System.Collections.IEnumerable?displayProperty=fullName> È possibile che una classe implementare più interfacce generiche costruite utilizzando un argomento di tipo diverso per ogni tipo di costruzione. Se una classe che esegue questa operazione viene utilizzata per la variabile di iteratore, tale variabile è presenti più <xref:System.Collections.IEnumerable.GetEnumerator%2A>metodo.</xref:System.Collections.IEnumerable.GetEnumerator%2A> In tal caso, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] non può scegliere il metodo da chiamare.  
  
 **ID errore:** BC32096  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
-   Utilizzare [operatore DirectCast](../../../visual-basic/language-reference/operators/directcast-operator.md) o [operatore TryCast](../../../visual-basic/language-reference/operators/trycast-operator.md) per eseguire il cast del tipo di variabile di iteratore per l'interfaccia che definisce il <xref:System.Collections.IEnumerable.GetEnumerator%2A>metodo che si desidera utilizzare.</xref:System.Collections.IEnumerable.GetEnumerator%2A>  
  
## <a name="see-also"></a>Vedere anche  
 [Per ogni corso... Next (istruzione)](../../../visual-basic/language-reference/statements/for-each-next-statement.md)   
 [Interfacce](../../../visual-basic/programming-guide/language-features/interfaces/index.md)
