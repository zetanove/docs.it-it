---
title: "&quot;&lt;typename&gt;&quot; è un tipo delegato | Documenti di Microsoft"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- bc32008
- vbc32008
dev_langs:
- VB
helpviewer_keywords:
- BC32008
ms.assetid: dc6abba0-a9ad-450f-8899-87265bc84abc
caps.latest.revision: 11
author: stevehoag
ms.author: shoag
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
ms.openlocfilehash: 3d6cc283f7e9815eb9b723a450731998f14b3424
ms.lasthandoff: 03/13/2017

---
# <a name="39lttypenamegt39-is-a-delegate-type"></a>'&lt;typename&gt;' è un tipo delegato
'\<typename >' è un tipo delegato. Creazione di delegati consente solo una singola espressione AddressOf come un elenco di argomenti. Spesso è possibile utilizzare un'espressione AddressOf anziché una costruzione di delegati.  
  
 Oggetto `New` clausola che crea un'istanza di una classe delegata fornisce un elenco di argomenti non valido al costruttore di delegato.  
  
 È possibile fornire una sola `AddressOf` espressione quando si crea una nuova istanza di delegato.  
  
 Questo errore può verificarsi se non si passano argomenti al costruttore di delegato, se si passano più argomenti, o se si passa un singolo argomento che non è valido `AddressOf` espressione.  
  
 **ID errore:** BC32008  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
-   Utilizzare una sola `AddressOf` espressione nell'elenco di argomenti per la classe delegata nella `New` clausola.  
  
## <a name="see-also"></a>Vedere anche  
 [Operatore new](../../../visual-basic/language-reference/operators/new-operator.md)   
 [AddressOf (operatore)](../../../visual-basic/language-reference/operators/addressof-operator.md)   
 [Delegati](../../../visual-basic/programming-guide/language-features/delegates/index.md)   
 [Procedura: Richiamare un metodo delegato](../../../visual-basic/programming-guide/language-features/delegates/how-to-invoke-a-delegate-method.md)
