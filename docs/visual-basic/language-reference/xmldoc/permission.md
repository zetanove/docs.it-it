---
title: "&lt;permission&gt; (Visual Basic) | Microsoft Docs"
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
  - "<permission> XML tag"
  - "permission XML tag"
ms.assetid: 0edf0500-5cd7-49c0-9255-64c48f972b77
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# &lt;permission&gt; (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Specifica un'autorizzazione obbligatoria per il membro.  
  
## Sintassi  
  
```  
<permission cref="member">description</permission>  
```  
  
#### Parametri  
 `member`  
 Riferimento a un membro o a un campo disponibile per essere chiamato dall'ambiente di compilazione corrente.  Il compilatore verifica che l'elemento di codice fornito esista e converte `member` nel nome canonico dell'elemento nell'XML di output.  Racchiudere `member` tra virgolette \(" "\).  
  
 `description`  
 Descrizione dell'accesso al membro.  
  
## Note  
 Utilizzare il tag `<permission>` per documentare l'accesso di un membro.  Utilizzare la classe <xref:System.Security.PermissionSet> per specificare l'accesso a un membro.  
  
 Eseguire la compilazione con [\/doc](../../../visual-basic/reference/command-line-compiler/doc.md) per elaborare in un file i commenti relativi alla documentazione.  
  
## Esempio  
 In questo esempio il tag `<permission>` viene utilizzato per descrivere che <xref:System.Security.Permissions.FileIOPermission> è obbligatorio per il funzionamento del metodo `ReadFile`.  
  
 [!code-vb[VbVbcnXmlDocComments#7](../../../visual-basic/language-reference/xmldoc/codesnippet/VisualBasic/permission_1.vb)]  
  
## Vedere anche  
 [XML Comment Tags](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)