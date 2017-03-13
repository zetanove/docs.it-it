---
title: "&lt;seealso&gt; (Visual Basic) | Microsoft Docs"
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
  - "<seealso> XML tag"
  - "seealso XML tag"
ms.assetid: 36050c95-1af2-4284-b9b6-1a70691ed978
caps.latest.revision: 10
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 10
---
# &lt;seealso&gt; (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Specifica un collegamento visualizzato nella sezione Vedere anche.  
  
## Sintassi  
  
```  
<seealso cref="member"/>  
```  
  
#### Parametri  
 `member`  
 Riferimento a un membro o a un campo disponibile per essere chiamato dall'ambiente di compilazione corrente.  Il compilatore verifica l'esistenza dell'elemento di codice specificato e passa `member` al nome di elemento nel file XML di output.  Il parametro `member` deve essere visualizzato tra virgolette doppie \(" "\).  
  
## Note  
 Utilizzare il tag `<seealso>` per specificare il testo che si desidera visualizzare in una sezione Vedere anche.  Utilizzare [\<see\>](../../../visual-basic/language-reference/xmldoc/see.md) per specificare un collegamento nel testo.  
  
 Eseguire la compilazione con [\/doc](../../../visual-basic/reference/command-line-compiler/doc.md) per elaborare in un file i commenti relativi alla documentazione.  
  
## Esempio  
 Nell'esempio riportato di seguito il tag `<seealso>` viene utilizzato nella sezione relativa alle osservazioni di `DoesRecordExist` per fare riferimento al metodo `UpdateRecord`.  
  
 [!code-vb[VbVbcnXmlDocComments#6](../../../visual-basic/language-reference/xmldoc/codesnippet/VisualBasic/seealso_1.vb)]  
  
## Vedere anche  
 [XML Comment Tags](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)