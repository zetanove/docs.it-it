---
title: "Type parameters cannot be used as qualifiers | Microsoft Docs"
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
  - "vbc32098"
  - "bc32098"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC32098"
ms.assetid: bab05325-dde8-4621-a5f6-368b5b7b2d76
caps.latest.revision: 9
caps.handback.revision: 9
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Type parameters cannot be used as qualifiers
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Un elemento di programmazione viene qualificato con una stringa di qualificazione che include un parametro di tipo.  
  
 Un parametro di tipo rappresenta un requisito per un tipo che deve essere fornito al momento della creazione del tipo generico.  Non rappresenta un tipo specifico definito.  È necessario che una stringa di qualificazione includa solo gli elementi definiti in fase di compilazione.  
  
 Le istruzioni seguenti possono generare questo errore.  
  
```  
Public Function checkText(Of c As System.Windows.Forms.Control)(  
    ByVal badText As String) As Boolean  
  
    Dim saveText As c.Text  
    ' Insert code to look for badText within saveText.  
End Function  
```  
  
 **ID errore:** BC32098  
  
### Per correggere l'errore  
  
1.  Rimuovere il parametro di tipo dalla stringa di qualificazione o sostituirlo con un tipo definito.  
  
2.  Se è necessario utilizzare un tipo creato per individuare l'elemento di programmazione qualificato, è necessario utilizzare logica di programma aggiuntiva.  
  
## Vedere anche  
 [References to Declared Elements](../../../visual-basic/programming-guide/language-features/declared-elements/references-to-declared-elements.md)   
 [Tipi generici in Visual Basic](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [Type List](../../../visual-basic/language-reference/statements/type-list.md)