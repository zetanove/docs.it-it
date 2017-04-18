---
title: Valutazione della funzione disabilitata a causa del timeout di una valutazione della funzione precedente | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- bc30957
- vbc30957
dev_langs:
- VB
helpviewer_keywords:
- BC30957
ms.assetid: 561e593a-f50a-4b72-a708-4cab60ec7b28
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
ms.openlocfilehash: b861b5c6c151c5d3aeec2810c7f2a228f22fdf6e
ms.lasthandoff: 03/13/2017

---
# <a name="function-evaluation-is-disabled-because-a-previous-function-evaluation-timed-out"></a>Valutazione della funzione disabilitata a causa del timeout di una valutazione di funzione precedente
Valutazione della funzione disabilitata a causa del timeout di una valutazione della funzione precedente. Per abilitare nuovamente la valutazione della funzione, ripetere l'operazione o riavviare il debug.  
  
 Nel debugger di Visual Studio, un'espressione specifica una chiamata di procedura, ma un altro di valutazione è scaduta.  
  
 Possibili cause per una chiamata di procedura timeout includono un ciclo infinito o *ciclo infinito*. Per ulteriori informazioni, vedere [per... Istruzione successiva](../../../visual-basic/language-reference/statements/for-next-statement.md).  
  
 Un caso speciale di ciclo infinito è *ricorsione*. Per ulteriori informazioni, vedere [routine ricorsive](../../../visual-basic/programming-guide/language-features/procedures/recursive-procedures.md).  
  
 **ID errore:** BC30957  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
1.  Se possibile, stabilire qual è la valutazione della funzione precedente e la relativa causa il timeout. In caso contrario, questo errore potrebbe verificarsi nuovamente.  
  
2.  Eseguire nuovamente il debugger o terminare e riavviare il debug.  
  
## <a name="see-also"></a>Vedere anche  
 [Debugging in Visual Studio](https://docs.microsoft.com/visualstudio/debugger/debugging-in-visual-studio)  (Debug in Visual Studio)  
 [Spostarsi nel codice con il Debugger](https://docs.microsoft.com/visualstudio/debugger/navigating-through-code-with-the-debugger)
