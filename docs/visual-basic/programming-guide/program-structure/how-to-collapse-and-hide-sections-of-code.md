---
title: 'Procedura: comprimere e nascondere sezioni di codice (Visual Basic) | Documenti di Microsoft'
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- Visual Basic, code collapsing
- Visual Basic, code hiding
- Visual Basic code, collapsing and hiding
ms.assetid: b770e8f5-e07d-491a-ab4b-a977980f9ba2
caps.latest.revision: 11
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
ms.openlocfilehash: 200a90b6983277d46b6e5c7b27ee4a90ecf88c40
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-collapse-and-hide-sections-of-code-visual-basic"></a>Procedura: comprimere e nascondere sezioni di codice (Visual Basic)
Il `#Region` (direttiva) consente di comprimere e nascondere sezioni di codice in [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] file. Il `#Region` direttiva consente di specificare un blocco di codice che è possibile espandere o comprimere tramite la [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs_md.md)] editor di codice. La possibilità di nascondere il codice in modo selettivo rende i file più gestibile e più facile da leggere. Per altre informazioni, vedere [Struttura](https://docs.microsoft.com/visualstudio/ide/outlining).  
  
 `#Region`direttive supportano la semantica dei blocchi di codice, ad esempio `#If...#End If`. Ciò significa che non possono iniziare in un blocco e terminare con un altro. l'inizio e fine deve essere nello stesso blocco. `#Region`le direttive non sono supportate all'interno delle funzioni.  
  
### <a name="to-collapse-and-hide-a-section-of-code"></a>Per comprimere e nascondere una sezione di codice  
  
-   Inserire la sezione di codice tra le `#Region` e `#End Region` istruzioni, come nell'esempio seguente:  
  
     [!code-vb[6 VbVbalrConditionalComp](../../../visual-basic/language-reference/directives/codesnippet/VisualBasic/how-to-collapse-and-hide-sections-of-code_1.vb)]  
  
     Il `#Region` blocco può essere utilizzato più volte in un file di codice, di conseguenza, gli utenti possono definire i propri blocchi di routine e le classi che possono, a sua volta, essere compressi. `#Region`possono anche essere nidificati all'interno di altri `#Region` blocchi.  
  
    > [!NOTE]
    >  Nascondere il codice non impedisce che venga compilato e non influisce sulla `#If...#End If` istruzioni.  
  
## <a name="see-also"></a>Vedere anche  
 [Compilazione condizionale](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)   
 [#Region (direttiva)](../../../visual-basic/language-reference/directives/region-directive.md)   
 [#If... Then... #Else direttive](../../../visual-basic/language-reference/directives/if-then-else-directives.md)   
 [Struttura](https://docs.microsoft.com/visualstudio/ide/outlining)
