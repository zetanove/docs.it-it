---
title: "&lt;permission&gt; (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "permission"
  - "<permission>"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "<permission> (tag XML C#)"
  - "permission (tag XML C#)"
ms.assetid: 769e93fe-8404-443f-bf99-577aa42b6a49
caps.latest.revision: 12
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 12
---
# &lt;permission&gt; (Guida per programmatori C#)
## Sintassi  
  
```  
<permission cref="member">description</permission>  
```  
  
#### Parametri  
 cref \= "`member`"  
 Riferimento a un membro o a un campo disponibile per essere chiamato dall'ambiente di compilazione corrente.  Il compilatore verifica l'esistenza dell'elemento di codice specificato e converte `member` nel nome canonico dell'elemento nel file XML di output.  *member* deve essere racchiuso tra virgolette doppie \(" "\).  
  
 Per informazioni sulla creazione di un riferimento cref a un tipo generico, vedere [\<see\>](../../../csharp/programming-guide/xmldoc/see.md).  
  
 `description`  
 Descrizione dell'accesso al membro.  
  
## Note  
 Il tag \<permission\> consente di documentare l'accesso a un membro.  La classe <xref:System.Security.PermissionSet> consente di specificare l'accesso a un membro.  
  
 Eseguire la compilazione con [\/doc](../../../csharp/language-reference/compiler-options/doc-compiler-option.md) per elaborare in un file i commenti per la creazione della documentazione.  
  
## Esempio  
 [!code-cs[csProgGuideDocComments#8](../../../csharp/programming-guide/xmldoc/codesnippet/CSharp/permission_1.cs)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Tag consigliati per i commenti relativi alla documentazione](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)