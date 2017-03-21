---
title: Tipo di promozione (Visual Basic) | Documenti di Microsoft
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
- declared elements, scope
- visibility, declared elements
- Partial keyword, unexpected results with type promotion
- scope, declared elements
- scope, Visual Basic
- type promotion
- declared elements, visibility
ms.assetid: 035eeb15-e4c5-4288-ab3c-6bd5d22f7051
caps.latest.revision: 17
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
ms.openlocfilehash: d732e765fc28eaedc0deab477dbf9955a40e97c9
ms.lasthandoff: 03/13/2017

---
# <a name="type-promotion-visual-basic"></a>Promozione tipo (Visual Basic)
Quando si dichiara un elemento di programmazione in un modulo, [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] promuove l'ambito per lo spazio dei nomi che contiene il modulo. Ciò è noto come *promozione del tipo*.  
  
 Nell'esempio seguente viene illustrata una definizione di base di un modulo e due membri del modulo.  
  
 [!code-vb[VbVbalrDeclaredElements n.&1;](../../../../visual-basic/programming-guide/language-features/declared-elements/codesnippet/VisualBasic/type-promotion_1.vb)]  
  
 All'interno di `projModule`, programmazione gli elementi dichiarati a livello di modulo vengono promossi alla `projNamespace`. Nell'esempio precedente, `basicEnum` e `innerClass` alzate di livello, ma `numberSub` non lo è, poiché non è dichiarato a livello di modulo.  
  
## <a name="effect-of-type-promotion"></a>Effetto della promozione del tipo  
 L'effetto della promozione del tipo è che la stringa di qualificazione non è necessario includere il nome del modulo. Nell'esempio seguente effettuate due chiamate alla procedura nell'esempio precedente.  
  
 [!code-vb[VbVbalrDeclaredElements n.&2;](../../../../visual-basic/programming-guide/language-features/declared-elements/codesnippet/VisualBasic/type-promotion_2.vb)]  
  
 Nell'esempio precedente, la prima chiamata utilizza stringhe di qualificazione complete. Tuttavia, questo non è necessario a causa di promozione del tipo. Anche la seconda chiamata accede a membri del modulo senza includere `projModule` nelle stringhe di qualificazione.  
  
## <a name="defeat-of-type-promotion"></a>Annullamento dell'effetto della promozione del tipo  
 Se lo spazio dei nomi dispone già di un membro con lo stesso nome di un membro del modulo, la promozione del tipo viene annullato per tale membro. Nell'esempio seguente viene illustrata una definizione di base di un'enumerazione e un modulo all'interno dello stesso spazio dei nomi.  
  
 [!code-vb[VbVbalrDeclaredElements n.&3;](../../../../visual-basic/programming-guide/language-features/declared-elements/codesnippet/VisualBasic/type-promotion_3.vb)]  
  
 Nell'esempio precedente, [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] Impossibile promuovere la classe `abc` a `thisNameSpace` perché esiste già un'enumerazione con lo stesso nome a livello di spazio dei nomi. Per accedere a `abcSub`, è necessario utilizzare la stringa di qualificazione completo `thisNamespace.thisModule.abc.abcSub`. Tuttavia, classe `xyz` ancora viene promosso, ed è possibile accedere `xyzSub` con la stringa più corta qualificazione `thisNamespace.xyz.xyzSub`.  
  
### <a name="defeat-of-type-promotion-for-partial-types"></a>Annullamento dell'effetto della promozione del tipo per i tipi parziali  
 Se una classe o struttura all'interno di un modulo viene utilizzato il [parziale](../../../../visual-basic/language-reference/modifiers/partial.md) (parola chiave), la promozione dei tipi viene automaticamente annullata da tale classe o struttura, se lo spazio dei nomi ha un membro con lo stesso nome. Altri elementi del modulo sono comunque idonei per la promozione del tipo.  
  
 **Conseguenze.** Annullamento dell'effetto della promozione del tipo di una definizione parziale può causare risultati imprevisti e persino errori del compilatore. L'esempio seguente mostra alcune definizioni parziali di una classe, uno dei quali è all'interno di un modulo.  
  
 [!code-vb[VbVbalrDeclaredElements n.&4;](../../../../visual-basic/programming-guide/language-features/declared-elements/codesnippet/VisualBasic/type-promotion_4.vb)]  
  
 Nell'esempio precedente, lo sviluppatore potrebbe aspettarsi che il compilatore per unire le due definizioni parziali di `sampleClass`. Tuttavia, il compilatore non considera promozione per la definizione parziale all'interno di `sampleModule`. Di conseguenza, il tentativo di compilare due classi separate e distinte, denominate entrambe `sampleClass` ma con percorsi di qualificazione differenti.  
  
 Il compilatore unisce le definizioni parziali solo se i relativi percorsi completi sono identici.  
  
## <a name="recommendations"></a>Suggerimenti  
 I suggerimenti seguenti rappresentano una buona norma di programmazione.  
  
-   **Nomi univoci.** Quando si dispone di un controllo completo sulla denominazione degli elementi di programmazione, è sempre una buona idea utilizzare nomi univoci ovunque. I nomi identici richiedono una qualificazione aggiuntiva e possono rendere difficile leggere il codice. Si può inoltre causare errori difficili da rilevare e risultati imprevisti.  
  
-   **Nome completo.** Quando si lavora con i moduli e altri elementi dello stesso spazio dei nomi, l'approccio più sicuro consiste nell'utilizzare sempre il nome completo per tutti gli elementi di programmazione. Se la promozione del tipo viene annullato per un membro del modulo e non è completamente qualificare tale membro, è possibile accedere accidentalmente un elemento di programmazione diversi.  
  
## <a name="see-also"></a>Vedere anche  
 [Module (istruzione)](../../../../visual-basic/language-reference/statements/module-statement.md)   
 [Istruzione Namespace](../../../../visual-basic/language-reference/statements/namespace-statement.md)   
 [Parziale](../../../../visual-basic/language-reference/modifiers/partial.md)   
 [Ambito in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/scope.md)   
 [Procedura: controllare l'ambito di una variabile](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-control-the-scope-of-a-variable.md)   
 [Riferimenti a elementi dichiarati](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)
