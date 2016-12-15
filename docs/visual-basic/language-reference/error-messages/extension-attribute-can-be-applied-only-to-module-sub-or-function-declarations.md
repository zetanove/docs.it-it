---
title: "&#39;Extension&#39; attribute can be applied only to &#39;Module&#39;, &#39;Sub&#39;, or &#39;Function&#39; declarations | Microsoft Docs"
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
  - "bc36550"
  - "vbc36550"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC36550"
ms.assetid: 4387a51f-733c-45d7-abdb-eb64d4f51078
caps.latest.revision: 18
caps.handback.revision: 18
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# &#39;Extension&#39; attribute can be applied only to &#39;Module&#39;, &#39;Sub&#39;, or &#39;Function&#39; declarations
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

L'unica modalità per estendere un tipo di dati in Visual Basic è definire un metodo di estensione in un modulo standard.  Il metodo di estensione può essere una procedura `Sub` o una procedura `Function`.  Tutti i metodi di estensione devono essere contrassegnati dall'attributo dell'estensione, `<Extension()>`, dallo spazio dei nomi <xref:System.Runtime.CompilerServices?displayProperty=fullName>.  Facoltativamente, un modulo che contiene un metodo di estensione può essere contrassegnato nello stesso modo.  Nessun altro utilizzo dell'attributo di estensione è valido.  
  
 **ID errore:** BC36550  
  
### Per correggere l'errore  
  
-   Rimuovere l'attributo di estensione.  
  
-   Riprogettare l'estensione come un metodo, definito in un modulo di inclusione.  
  
## Esempio  
 Nell'esempio riportato di seguito viene definita un metodo `Print` per il tipo di dati `String`.  
  
```  
Imports StringUtility  
Imports System.Runtime.CompilerServices  
Namespace StringUtility  
    <Extension()>   
    Module StringExtensions  
        <Extension()>   
        Public Sub Print (ByVal str As String)  
            Console.WriteLine(str)  
        End Sub  
    End Module  
End Namespace  
  
```  
  
## Vedere anche  
 [Attributi](../Topic/Attributes%20\(C%23%20and%20Visual%20Basic\).md)   
 [Metodi di estensione](../../../visual-basic/programming-guide/language-features/procedures/extension-methods.md)   
 [Module Statement](../../../visual-basic/language-reference/statements/module-statement.md)