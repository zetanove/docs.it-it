---
title: "XML comment exception must have a &#39;cref&#39; attribute | Microsoft Docs"
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
  - "bc42319"
  - "vbc42319"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC42319"
ms.assetid: 62eeeba3-6811-48be-b1ef-c2e4feda3177
caps.latest.revision: 13
caps.handback.revision: 13
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# XML comment exception must have a &#39;cref&#39; attribute
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Il tag \<exception\> consente di documentare le eccezioni che potrebbero essere generate da un metodo.  L'attributo obbligatorio `cref` designa il nome di un membro la cui presenza viene verificata dal generatore di documentazione.  Se il membro esiste, viene convertito nel nome canonico dell'elemento nel file di documentazione.  
  
 **ID errore:** BC42319  
  
### Per correggere l'errore  
  
-   Aggiungere l'attributo `cref` all'eccezione come descritto di seguito:  
  
    ```  
    '''<exception cref="member">description</exception>  
    ```  
  
## Vedere anche  
 [\<exception\>](../../../visual-basic/language-reference/xmldoc/exception.md)   
 [How to: Create XML Documentation](../../../visual-basic/programming-guide/program-structure/how-to-create-xml-documentation.md)   
 [XML Comment Tags](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)