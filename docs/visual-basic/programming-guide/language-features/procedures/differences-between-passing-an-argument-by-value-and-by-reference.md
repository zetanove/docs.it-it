---
title: Differenze tra il passaggio di un argomento per valore e per riferimento (Visual Basic) | Documenti di Microsoft
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
- ByRef keyword, passing arguments by reference
- Visual Basic code, procedures
- procedures, passing arguments
- ByVal keyword, passing arguments by value
- arguments [Visual Basic], passing by value or by reference
ms.assetid: 5f5c38fe-3e2d-494c-8fff-f4025b55ec93
caps.latest.revision: 14
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
ms.openlocfilehash: 93c515dd8524cde85555a27879baee00185f78e3
ms.lasthandoff: 03/13/2017

---
# <a name="differences-between-passing-an-argument-by-value-and-by-reference-visual-basic"></a>Differenze tra il passaggio di un argomento per valore e per riferimento (Visual Basic)
Quando si passano uno o più argomenti a una routine, ciascun argomento corrisponde a un elemento di programmazione sottostante nel codice chiamante. È possibile passare il valore di questo elemento sottostante oppure un riferimento a esso. Ciò è noto come il *meccanismo di trasferimento*.  
  
## <a name="passing-by-value"></a>passaggio per valore  
 Si passa un argomento *dal valore* specificando il [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md) (parola chiave) per il parametro corrispondente nella definizione della routine. Quando si utilizza questo meccanismo di passaggio, [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] copia il valore dell'elemento di programmazione sottostante in una variabile locale nella procedura. Il codice della routine non dispone di accesso per l'elemento sottostante nel codice chiamante.  
  
## <a name="passing-by-reference"></a>Il passaggio per riferimento  
 Si passa un argomento *per riferimento* specificando il [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md) (parola chiave) per il parametro corrispondente nella definizione della routine. Quando si utilizza questo meccanismo di passaggio, [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] assegna alla routine un riferimento diretto all'elemento di programmazione sottostante nel codice chiamante.  
  
## <a name="passing-mechanism-and-element-type"></a>Meccanismo di passaggio e il tipo di elemento  
 La scelta del meccanismo di trasferimento non è quello utilizzato per la classificazione del tipo dell'elemento sottostante. Il passaggio per valore o per riferimento si riferisce a quanto [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] fornisce al codice della routine. Tipo di valore o tipo di riferimento fa riferimento a come un elemento di programmazione viene archiviato in memoria.  
  
 Tuttavia, il meccanismo di passaggio e il tipo di elemento sono correlati. Il valore di un tipo di riferimento è un puntatore ai dati in un' posizione in memoria. Ciò significa che quando si passa un tipo di riferimento per valore, il codice della routine è un puntatore ai dati dell'elemento sottostante, anche se non può accedere l'elemento sottostante. Ad esempio, se l'elemento è una variabile di matrice, il codice della routine non dispone dell'accesso alla variabile stessa, ma può accedere i membri della matrice.  
  
## <a name="ability-to-modify"></a>Possibilità di modificare  
 Quando si passa un elemento non è modificabile come argomento, la procedura mai modificarlo nel codice chiamante, se viene passato `ByVal` o `ByRef`.  
  
 Per un elemento modificabile, nella tabella seguente viene riepilogata l'interazione tra il tipo di elemento e il meccanismo di passaggio.  
  
|Tipo di elemento|Passato`ByVal`|Passato`ByRef`|  
|------------------|--------------------|--------------------|  
|Tipo di valore (contiene un solo valore)|La routine non può modificare la variabile o i relativi membri.|La procedura è possibile modificare la variabile e i relativi membri.|  
|Tipo di riferimento (contiene un puntatore a un'istanza di classe o struttura)|La routine non può modificare la variabile ma può modificare i membri dell'istanza a cui fa riferimento.|La procedura è possibile modificare la variabile e i membri dell'istanza a cui fa riferimento.|  
  
## <a name="see-also"></a>Vedere anche  
 [Procedure](./index.md)   
 [Gli argomenti e parametri di routine](./procedure-parameters-and-arguments.md)   
 [Procedura: passare argomenti a una routine](./how-to-pass-arguments-to-a-procedure.md)   
 [Passaggio di argomenti per valore e per riferimento](./passing-arguments-by-value-and-by-reference.md)   
 [Differenze tra argomenti modificabili e](./differences-between-modifiable-and-nonmodifiable-arguments.md)   
 [Procedura: modificare il valore di un argomento di routine](./how-to-change-the-value-of-a-procedure-argument.md)   
 [Procedura: proteggere un argomento di routine modifica del valore](./how-to-protect-a-procedure-argument-against-value-changes.md)   
 [Procedura: forzare un argomento sia passati per valore](./how-to-force-an-argument-to-be-passed-by-value.md)   
 [Passaggio di argomenti in base alla posizione e in base al nome](./passing-arguments-by-position-and-by-name.md)   
 [Tipi valore e tipi di riferimento](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)
