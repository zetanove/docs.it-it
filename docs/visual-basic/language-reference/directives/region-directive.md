---
title: "#Region Directive | Microsoft Docs"
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
  - "vb.Region"
  - "vb.#Region"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Visual Basic compiler, compiler directives"
  - "#region directive"
  - "region directive (#region)"
  - "#Region keyword"
ms.assetid: 90a6a104-3cbf-47d0-bdc4-b585d0921b87
caps.latest.revision: 14
caps.handback.revision: 14
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# #Region Directive
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Comprime e nasconde sezioni di codice in file di Visual Basic.  
  
## Sintassi  
  
```  
  
        #Region "identifier_string"  
#End Region  
```  
  
## Parti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`identifier_string`|Necessario.  Stringa che funge da titolo di un'area quando viene compressa.  Le aree sono compresse per impostazione predefinita.|  
|`#End Region`|Termina il blocco `#Region`.|  
  
## Note  
 Usare la direttiva `#Region` per specificare un blocco di codice da espandere o comprimere durante l'uso della funzionalità di struttura dell'editor di codice di Visual Studio.  È possibile posizionare o *annidare* aree all'interno di altre aree per raggruppare aree simili.  
  
## Esempio  
 In questo esempio viene usata la direttiva `#Region`.  
  
 [!code-vb[VbVbalrConditionalComp#4](../../../visual-basic/language-reference/directives/codesnippet/VisualBasic/region-directive_1.vb)]  
  
## Vedere anche  
 [\#If...Then...\#Else Directives](../../../visual-basic/language-reference/directives/if-then-else-directives.md)   
 [Struttura](/visual-studio/ide/outlining)   
 [How to: Collapse and Hide Sections of Code](../../../visual-basic/programming-guide/program-structure/how-to-collapse-and-hide-sections-of-code.md)