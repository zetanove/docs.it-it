---
title: "Type Promotion (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "declared elements, scope"
  - "visibility, declared elements"
  - "Partial keyword, unexpected results with type promotion"
  - "scope, declared elements"
  - "scope, Visual Basic"
  - "type promotion"
  - "declared elements, visibility"
ms.assetid: 035eeb15-e4c5-4288-ab3c-6bd5d22f7051
caps.latest.revision: 17
caps.handback.revision: 17
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Type Promotion (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Quando si dichiara un elemento di programmazione in un modulo, [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] promuove l'ambito dell'elemento allo spazio dei nomi contenente il modulo.  Questa operazione è denominata *promozione tipo*.  
  
 Nell'esempio riportato di seguito viene illustrata la definizione di base di un modulo e due membri di tale modulo.  
  
 [!code-vb[VbVbalrDeclaredElements#1](../../../../visual-basic/programming-guide/language-features/declared-elements/codesnippet/VisualBasic/type-promotion_1.vb)]  
  
 All'interno di `projModule`, gli elementi di programmazione dichiarati a livello di modulo vengono promossi al tipo `projNamespace`.  Nell'esempio precedente vengono promossi i tipi `basicEnum` e `innerClass`, ma non `numberSub`, poiché quest'ultimo non è dichiarato a livello di modulo.  
  
## Effetto della promozione del tipo  
 L'effetto della promozione del tipo è che una stringa di qualificazione non deve includere necessariamente il nome del modulo.  Nell'esempio riportato di seguito vengono effettuate due chiamate alla routine dell'esempio precedente.  
  
 [!code-vb[VbVbalrDeclaredElements#2](../../../../visual-basic/programming-guide/language-features/declared-elements/codesnippet/VisualBasic/type-promotion_2.vb)]  
  
 Nell'esempio precedente la prima chiamata utilizza stringhe di qualificazione complete.  Questa informazione, tuttavia, non è necessaria grazie alla promozione del tipo.  Anche la seconda chiamata accede ai membri del modulo senza includere `projModule` nelle stringhe di qualificazione.  
  
## Annullamento dell'effetto della promozione del tipo  
 Se lo spazio dei nomi contiene già come membro del modulo un membro con lo stesso nome, gli effetti della promozione del tipo per tale membro vengono annullati.  Nell'esempio riportato di seguito viene illustrata la definizione di base di un'enumerazione e un modulo all'interno dello stesso spazio dei nomi.  
  
 [!code-vb[VbVbalrDeclaredElements#3](../../../../visual-basic/programming-guide/language-features/declared-elements/codesnippet/VisualBasic/type-promotion_3.vb)]  
  
 Nell'esempio precedente [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] non può promuovere la classe `abc` al tipo `thisNameSpace` perché è già presente un'enumerazione con lo stesso nome a livello di spazio dei nomi.  Per accedere a `abcSub`, è necessario utilizzare la stringa di qualificazione completa `thisNamespace.thisModule.abc.abcSub`.  Tuttavia, la promozione del tipo per la classe `xyz` viene comunque eseguita ed è quindi possibile accedere a `xyzSub` utilizzando la stringa di qualificazione più breve `thisNamespace.xyz.xyzSub`.  
  
### Annullamento dell'effetto della promozione del tipo per i tipi parziali  
 Se una classe o una struttura all'interno di un modulo utilizza la parola chiave [Partial](../../../../visual-basic/language-reference/modifiers/partial.md), l'effetto della promozione del tipo per tale classe o struttura viene annullato automaticamente, indipendentemente dal fatto che nello spazio dei nomi sia presente o meno un membro con lo stesso nome.  Gli altri elementi nel modulo sono comunque idonei per la promozione del tipo.  
  
 **Conseguenze.** L'annullamento dell'effetto della promozione del tipo per una definizione parziale può causare risultati imprevisti e persino errori del compilatore.  Nell'esempio riportato di seguito sono illustrate alcune definizioni parziali di base di una classe, una delle quali si trova all'interno di un modulo.  
  
 [!code-vb[VbVbalrDeclaredElements#4](../../../../visual-basic/programming-guide/language-features/declared-elements/codesnippet/VisualBasic/type-promotion_4.vb)]  
  
 Nell'esempio precedente lo sviluppatore potrebbe aspettarsi che il compilatore unisca le due definizioni parziali di `sampleClass`.  Il compilatore, tuttavia, non prende in considerazione la promozione per la definizione parziale all'interno di `sampleModule`.  Di conseguenza, tenta di compilare due classi distinte e separate, entrambe denominate `sampleClass`, ma con percorsi di qualificazione differenti.  
  
 Il compilatore unisce le definizioni parziali solo se i relativi percorsi completi sono identici.  
  
## Consigli  
 Di seguito sono riportati alcuni consigli che possono risultare utili in fase di programmazione.  
  
-   **Nomi univoci.** Se si dispone del controllo completo sulla denominazione degli elementi di programmazione, è preferibile utilizzare sempre nomi univoci.  I nomi identici richiedono una qualificazione aggiuntiva e rendono più difficile la lettura del codice.  Possono, inoltre, causare errori difficili da rilevare nonché generare risultati imprevisti.  
  
-   **Nome completo.** Quando si utilizzano moduli e altri elementi nello stesso spazio dei nomi, si consiglia di utilizzare sempre il nome completo per tutti gli elementi di programmazione.  Se l'effetto della promozione del tipo viene annullato per un membro del modulo e non si dispone del percorso completo per tale membro, è possibile che si acceda inavvertitamente a un elemento di programmazione differente.  
  
## Vedere anche  
 [Module Statement](../../../../visual-basic/language-reference/statements/module-statement.md)   
 [Namespace Statement](../../../../visual-basic/language-reference/statements/namespace-statement.md)   
 [Partial](../../../../visual-basic/language-reference/modifiers/partial.md)   
 [Scope in Visual Basic](../../../../visual-basic/programming-guide/language-features/declared-elements/scope.md)   
 [How to: Control the Scope of a Variable](../../../../visual-basic/programming-guide/language-features/declared-elements/how-to-control-the-scope-of-a-variable.md)   
 [References to Declared Elements](../../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)