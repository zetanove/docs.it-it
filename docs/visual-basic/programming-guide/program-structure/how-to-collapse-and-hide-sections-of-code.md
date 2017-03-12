---
title: "How to: Collapse and Hide Sections of Code (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Visual Basic, code collapsing"
  - "Visual Basic, code hiding"
  - "Visual Basic code, collapsing and hiding"
ms.assetid: b770e8f5-e07d-491a-ab4b-a977980f9ba2
caps.latest.revision: 11
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 11
---
# How to: Collapse and Hide Sections of Code (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

La direttiva `#Region` consente di comprimere e nascondere sezioni di codice nei file di [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)].  La direttiva `#Region` consente di specificare un blocco di codice che è possibile espandere o comprimere quando si utilizza l'editor di codice di [!INCLUDE[vsprvs](../../../csharp/includes/vsprvs-md.md)].  La possibilità di nascondere il codice in modo selettivo rende i file più gestibili e ne facilita la lettura.  Per ulteriori informazioni, vedere [Struttura](/visual-studio/ide/outlining).  
  
 Le direttive `#Region` supportano la semantica dei blocchi di codice, ad esempio `#If...#End If`.  Pertanto non possono iniziare e terminare in blocchi diversi. È necessario che inizio e fine si trovino nello stesso blocco.  Le direttive `#Region` non sono supportate all'interno delle funzioni.  
  
### Per comprimere e nascondere una sezione di codice  
  
-   Inserire la sezione di codice tra le istruzioni `#Region` e `#End Region`, come nell'esempio che segue:  
  
     [!code-vb[VbVbalrConditionalComp#6](../../../visual-basic/language-reference/directives/codesnippet/visualbasic/how-to-collapse-and-hide_1.vb)]  
  
     Il blocco `#Region` può essere utilizzato più volte in un file di codice. Gli utenti possono quindi definire direttamente i blocchi di routine e di classi che potranno a loro volta essere compressi.  I blocchi `#Region` possono inoltre venire annidati all'interno di altri blocchi `#Region`.  
  
    > [!NOTE]
    >  Nascondere il codice non ne impedisce la compilazione e non ha effetto sulle istruzioni `#If...#End If`.  
  
## Vedere anche  
 [Conditional Compilation](../../../visual-basic/programming-guide/program-structure/conditional-compilation.md)   
 [\#Region Directive](../../../visual-basic/language-reference/directives/region-directive.md)   
 [\#If...Then...\#Else Directives](../../../visual-basic/language-reference/directives/if-then-else-directives.md)   
 [Struttura](/visual-studio/ide/outlining)