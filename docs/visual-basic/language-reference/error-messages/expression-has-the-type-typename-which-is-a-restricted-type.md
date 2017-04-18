---
title: "Espressione è di tipo &quot;&lt;typename&gt;&quot; che corrisponde a un tipo limitato e non può essere utilizzato per accedere ai membri ereditati da &quot;Object&quot; o &quot;ValueType&quot; | Documenti di Microsoft"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- bc31393
- vbc31393
dev_langs:
- VB
helpviewer_keywords:
- BC31393
ms.assetid: 2963cf3f-c527-4aa7-b67c-ee80b6d23186
caps.latest.revision: 6
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
ms.openlocfilehash: aaedfd825889498159f92cbd1d615cc0064973d3
ms.lasthandoff: 03/13/2017

---
# <a name="expression-has-the-type-39lttypenamegt39-which-is-a-restricted-type-and-cannot-be-used-to-access-members-inherited-from-39object39-or-39valuetype39"></a>Espressione è di tipo '&lt;typename&gt;' che corrisponde a un tipo limitato e non può essere utilizzato per accedere ai membri ereditati da 'Object' o 'ValueType'
Un'espressione restituisce un tipo che non può essere sottoposto a boxing da common language runtime (CLR), ma accede a un membro che richiede il boxing.  
  
 *Conversione boxing* si intende l'elaborazione necessaria convertire un tipo di `Object` o, in alcuni casi, per <xref:System.ValueType>.</xref:System.ValueType> Common language runtime non supporta il boxing determinati tipi di struttura, ad esempio <xref:System.ArgIterator>, <xref:System.RuntimeArgumentHandle>e <xref:System.TypedReference>.</xref:System.TypedReference> </xref:System.RuntimeArgumentHandle> </xref:System.ArgIterator>  
  
 Questa espressione tenta di utilizzare il tipo con restrizioni per chiamare un metodo ereditato da <xref:System.Object>o <xref:System.ValueType>, ad esempio <xref:System.Object.GetHashCode%2A>o <xref:System.Object.ToString%2A>.</xref:System.Object.ToString%2A> </xref:System.Object.GetHashCode%2A> </xref:System.ValueType> </xref:System.Object> Per accedere a questo metodo, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] ha tentato una conversione boxing implicita che causa questo errore.  
  
 **ID errore:** BC31393  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
1.  Trovare l'espressione che restituisce il tipo citato.  
  
2.  Individuare la parte dell'istruzione che tenta di chiamare il metodo ereditato da <xref:System.Object>o <xref:System.ValueType>.</xref:System.ValueType> </xref:System.Object>  
  
3.  Riscrivere l'istruzione per evitare la chiamata al metodo.  
  
## <a name="see-also"></a>Vedere anche  
 [Conversioni implicite ed esplicite](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)
