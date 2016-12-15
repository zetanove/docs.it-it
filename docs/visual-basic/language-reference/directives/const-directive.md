---
title: "#Const Directive | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.#Const"
  - "#vb.Const"
  - "#Const"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "#Const directive"
  - "conditional compilation, directives"
  - "Const directive (#Const)"
  - "Visual Basic compiler, compiler directives"
  - "constants, Const directive"
  - "constants, declaring"
  - "Const statement [Visual Basic], directive (#Const)"
  - "declaring constants, #const directive"
ms.assetid: 707669e5-23f9-4f17-8622-a0d534429386
caps.latest.revision: 17
caps.handback.revision: 17
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# #Const Directive
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Definisce le costanti di compilazione condizionale per Visual Basic.  
  
## Sintassi  
  
```  
#Const constname = expression  
```  
  
## Parti  
 `constname`  
 Obbligatorio.  Nome della costante definita.  
  
 `expression`  
 Obbligatorio.  Valore letterale, altra costante di compilazione condizionale o una combinazione che includa uno o tutti gli operatori aritmetici o logici, eccetto `Is`.  
  
## Note  
 Le costanti di compilazione condizionale sono sempre private rispetto al file nel quale vengono visualizzate.  Non è possibile creare costanti di compilazione pubbliche utilizzando la direttiva `#Const`. Tali costanti possono essere create solo all'interno dell'interfaccia utente o mediante l'opzione del compilatore `/define`.  
  
 All'interno di `expression` è possibile utilizzare solo costanti di compilazione condizionale e valori letterali.  L'utilizzo di una costante standard definita con `Const` provoca un errore.  È invece possibile utilizzare le costanti definite con la parola chiave `#Const` solo per la compilazione condizionale.  Le costanti possono anche essere non definite, nel qual caso hanno valore `Nothing`.  
  
## Esempio  
 In questo esempio viene utilizzata la direttiva `#Const`.  
  
 [!code-vb[VbVbalrConditionalComp#3](../../../visual-basic/language-reference/directives/codesnippet/VisualBasic/const-directive_1.vb)]  
  
## Vedere anche  
 [\/define](../../../visual-basic/reference/command-line-compiler/define.md)   
 [\#If...Then...\#Else Directives](../../../visual-basic/language-reference/directives/if-then-else-directives.md)   
 [Const Statement](../../../visual-basic/language-reference/statements/const-statement.md)   
 [Conditional Compilation](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)   
 [If...Then...Else Statement](../../../visual-basic/language-reference/statements/if-then-else-statement.md)