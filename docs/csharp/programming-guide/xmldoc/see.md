---
title: "&lt;see&gt; (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "<see>"
  - "see"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "<see> (tag XML C#)"
  - "cref [C#], <see> (tag)"
  - "riferimenti incrociati [C#]"
  - "see (tag XML C#)"
ms.assetid: 0200de01-7e2f-45c4-9094-829d61236383
caps.latest.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 19
---
# &lt;see&gt; (Guida per programmatori C#)
## Sintassi  
  
```  
<see cref="member"/>  
```  
  
#### Parametri  
 cref \= "`member`"  
 Riferimento a un membro o a un campo disponibile per essere chiamato dall'ambiente di compilazione corrente.  Il compilatore verifica l'esistenza dell'elemento di codice specificato e passa `member` al nome di elemento nel file XML di output.Racchiudere *member* tra virgolette doppie \(" "\).  
  
## Note  
 Il tag \<see\> consente di specificare un collegamento nel testo.  Utilizzare [\<seealso\>](../../../csharp/programming-guide/xmldoc/seealso.md) per indicare che il testo deve essere inserito in una sezione See Also.  Utilizzare l'[attributo cref](../../../csharp/programming-guide/xmldoc/cref-attribute.md) per creare collegamenti ipertestuali interni alle pagine della documentazione per gli elementi di codice.  
  
 Eseguire la compilazione con [\/doc](../../../csharp/language-reference/compiler-options/doc-compiler-option.md) per elaborare in un file i commenti per la creazione della documentazione.  
  
 Nell'esempio seguente viene illustrato un tag \<see\> all'interno di una sezione del riepilogo.  
  
 [!code-cs[csProgGuideDocComments#12](../../../csharp/programming-guide/xmldoc/codesnippet/csharp/see_1.cs)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Tag consigliati per i commenti relativi alla documentazione](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)