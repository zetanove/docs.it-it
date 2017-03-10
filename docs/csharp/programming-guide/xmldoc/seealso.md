---
title: "&lt;seealso&gt; (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "cref"
  - "<seealso>"
  - "seealso"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "<seealso> (tag XML C#)"
  - "cref [C#]"
  - "cref [C#], vedere anche"
  - "riferimenti incrociati [C#], tag"
  - "seealso (tag XML C#)"
ms.assetid: 8e157f3f-f220-4fcf-9010-88905b080b18
caps.latest.revision: 11
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 11
---
# &lt;seealso&gt; (Guida per programmatori C#)
## Sintassi  
  
```  
<seealso cref="member"/>  
```  
  
#### Parametri  
 cref \= "`member`"  
 Riferimento a un membro o a un campo disponibile per essere chiamato dall'ambiente di compilazione corrente.  Il compilatore verifica l'esistenza dell'elemento di codice specificato e passa `member` al nome di elemento nel file XML di output. `member` deve essere racchiuso tra virgolette doppie \(" "\).  
  
 Per informazioni sulla creazione di un riferimento cref a un tipo generico, vedere [\<see\>](../../../csharp/programming-guide/xmldoc/see.md).  
  
## Note  
 Il tag \<seealso\> consente di specificare il testo che si desidera visualizzare in una sezione Vedere anche.  Utilizzare [\<see\>](../../../csharp/programming-guide/xmldoc/see.md) per specificare un collegamento nel testo.  
  
 Eseguire la compilazione con [\/doc](../../../csharp/language-reference/compiler-options/doc-compiler-option.md) per elaborare in un file i commenti per la creazione della documentazione.  
  
## Esempio  
 Per un esempio sull'utilizzo di \<seealso\>, vedere [\<summary\>](../../../csharp/programming-guide/xmldoc/summary.md).  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Tag consigliati per i commenti relativi alla documentazione](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)