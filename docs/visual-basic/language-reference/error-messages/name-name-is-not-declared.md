---
title: "Name &#39;&lt;name&gt;&#39; is not declared | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "bc30451"
  - "vbc30451"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC30451"
ms.assetid: 765f099b-e21e-47c6-a906-a065444e56b3
caps.latest.revision: 11
caps.handback.revision: 11
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Name &#39;&lt;name&gt;&#39; is not declared
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Un'istruzione fa riferimento a un elemento di programmazione, ma non è possibile trovare una corrispondenza esatta con il nome di tale elemento.  
  
 **ID errore:** BC30451  
  
### Per correggere l'errore  
  
1.  Verificare che il nome nell'istruzione di riferimento sia stato digitato correttamente.  [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] non distingue tra maiuscole e minuscole, ma qualsiasi altra variazione nell'ortografia verrà considerata come un nome completamente diverso.  Il carattere di sottolineatura \(`_`\) fa parte del nome ed è pertanto parte dell'ortografia.  
  
2.  Verificare che sia presente l'operatore di accesso ai membri \(`.`\) tra un oggetto e il relativo membro.  Se ad esempio è presente un controllo <xref:System.Windows.Forms.TextBox> denominato `TextBox1`, per accedere alla relativa proprietà <xref:System.Windows.Forms.TextBoxBase.Text%2A> è necessario digitare `TextBox1.Text`.  Se invece si digita `TextBox1Text`, viene creato un nome diverso.  
  
3.  Se l'ortografia e la sintassi per l'accesso ai membri di un oggetto sono corrette, verificare che l'elemento sia stato dichiarato.  Per ulteriori informazioni, vedere [Declared Elements](../../../visual-basic/programming-guide/language-features/declared-elements/index.md).  
  
4.  Se l'elemento di programmazione è stato dichiarato, verificare che si trovi nell'ambito.  Se l'istruzione di riferimento non è inclusa nell'area che dichiara l'elemento di programmazione, può essere necessario qualificare il nome dell'elemento.  Per ulteriori informazioni, vedere [Scope in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/scope.md).  
  
## Vedere anche  
 [Declarations and Constants Summary](../../../visual-basic/language-reference/keywords/declarations-and-constants-summary.md)   
 [Visual Basic Naming Conventions](../../../visual-basic/programming-guide/program-structure/naming-conventions.md)   
 [Declared Element Names](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md)   
 [References to Declared Elements](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)