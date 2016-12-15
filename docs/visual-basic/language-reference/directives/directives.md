---
title: "Directives (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
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
  - "directives, Visual Basic compiler"
  - "Visual Basic code, directives"
  - "directives"
ms.assetid: 20d5fe65-490a-4c23-88c2-ee4f490ed762
caps.latest.revision: 9
caps.handback.revision: 9
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Directives (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Gli argomenti in questa sezione descrivono le direttive del compilatore del codice sorgente di Visual Basic.  
  
## In questa sezione  
 [\#Const Directive](../../../visual-basic/language-reference/directives/const-directive.md) \- Definisce una costante del compilatore  
  
 [\#ExternalSource Directive](../../../visual-basic/language-reference/directives/externalsource-directive.md) \- Indica un mapping tra righe di codice sorgente e testo esterno  
  
 [\#If...Then...\#Else Directives](../../../visual-basic/language-reference/directives/if-then-else-directives.md) \- Compilano blocchi di codice selezionati  
  
 [\#Region Directive](../../../visual-basic/language-reference/directives/region-directive.md) \- Comprime e nasconde sezioni di codice nell'editor di Visual Studi.  
  
 **\#Disable, \#Enable** \- Disabilitano e abilitano avvisi specifici per le aree di codice.  
  
```vb  
#Disable Warning BC42356 ' suppress warning about no awaits in this method  
    Async Function TestAsync() As Task  
        Console.WriteLine("testing")  
    End Function  
#Enable Warning BC42356  
  
```  
  
 È anche possibile disabilitare e abilitare un elenco di codici di avviso delimitato da virgole.  
  
## Sezioni correlate  
 [Visual Basic Language Reference](../../../visual-basic/language-reference/index.md)  
  
 [Visual Basic](../../../visual-basic/index.md)