---
title: "REM Statement (Visual Basic) | Microsoft Docs"
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
  - "vb.'"
  - "vb.Rem"
  - "Rem"
  - "'"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "REM statement"
  - "comments, Visual Basic code"
  - "code comments, Visual Basic"
  - "Visual Basic code, comments"
  - "' comment marker character [Visual Basic]"
ms.assetid: 34126d7f-e0f9-476d-91e6-b31b398615dc
caps.latest.revision: 11
caps.handback.revision: 11
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# REM Statement (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Viene utilizzata per includere note esplicative nel codice sorgente di un programma.  
  
## Sintassi  
  
```  
REM comment  
' comment  
```  
  
## Parti  
 `comment`  
 Parametro facoltativo.  Testo del commento da includere.  È necessario tra uno spazio di `REM` parola chiave e `comment`.  
  
## Note  
 È necessario specificare l'istruzione `REM` da sola in una riga o, al massimo, dopo un'altra istruzione.  È necessario che l'istruzione `REM` sia l'ultima della riga e,  se segue un'altra istruzione, è necessario che `REM` sia separata da questa da uno spazio.  
  
 L'istruzione `REM` può essere sostituita da una virgoletta singola \(`'`\).  sia che il commento segua un'altra istruzione nella stessa riga o che sia isolato in una riga.  
  
> [!NOTE]
>  Non è possibile continuare un'istruzione `REM` utilizzando una sequenza di continuazione di riga \(`_`\).  Una volta iniziato un commento, i caratteri non vengono esaminati dal compilatore alla ricerca di un significato speciale.  Per un commento a più righe, utilizzare un'altra istruzione `REM` o un simbolo di commento \(`'`\) su ogni riga.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato l'utilizzo dell'istruzione `REM` per includere note esplicative in un programma.  Viene inoltre presentato l'impiego alternativo della virgoletta singola \(`'`\) in sostituzione di `REM`.  
  
 [!code-vb[VbVbalrStatements#6](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/rem-statement_1.vb)]  
  
## Vedere anche  
 [Comments in Code](../../../visual-basic/programming-guide/program-structure/comments-in-code.md)   
 [Procedura: Interrompere e combinare istruzioni nel codice](../../../visual-basic/programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md)