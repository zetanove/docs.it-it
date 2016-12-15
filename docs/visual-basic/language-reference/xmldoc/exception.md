---
title: "&lt;exception&gt; (Visual Basic) | Microsoft Docs"
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
  - "<exception> XML tag"
  - "exception XML tag"
ms.assetid: c0517549-171e-4dae-ab88-a9c1700b6eee
caps.latest.revision: 9
caps.handback.revision: 9
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# &lt;exception&gt; (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Specifica le eccezioni che è possibile generare.  
  
## Sintassi  
  
```  
<exception cref="member">description</exception>  
```  
  
#### Parametri  
 `member`  
 Riferimento a un'eccezione disponibile dall'ambiente di compilazione corrente.  Il compilatore verifica che l'eccezione specificata esiste e converte `member` nel nome canonico dell'elemento nell'XML di output.  Il parametro `member` deve essere visualizzato tra virgolette doppie \(" "\).  
  
 `description`  
 Descrizione.  
  
## Note  
 Utilizzare il tag `<exception>` per specificare le eccezioni che è possibile generare.  Questo tag viene applicato a una definizione di metodo.  
  
 Eseguire la compilazione con [\/doc](../../../visual-basic/reference/command-line-compiler/doc.md) per elaborare in un file i commenti relativi alla documentazione.  
  
## Esempio  
 Nell'esempio riportato di seguito il tag `<exception>` viene utilizzato per descrivere un'eccezione che può essere generata dalla funzione `IntDivide`.  
  
 [!code-vb[VbVbcnXmlDocComments#3](../../../visual-basic/language-reference/xmldoc/codesnippet/VisualBasic/exception_1.vb)]  
  
## Vedere anche  
 [XML Comment Tags](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)