---
title: "&lt;value&gt; (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "<value>"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "<value> (tag XML C#)"
  - "value (tag XML C#)"
ms.assetid: 08dbadaf-9ab6-43d9-9493-98e43bed199a
caps.latest.revision: 12
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 12
---
# &lt;value&gt; (Guida per programmatori C#)
## Sintassi  
  
```  
<value>property-description</value>  
```  
  
#### Parametri  
 `property-description`  
 Descrizione della proprietà.  
  
## Note  
 Il tag \<value\> consente di descrivere il valore rappresentato da una proprietà.  Tenere presente che l'aggiunta di una proprietà mediante la procedura guidata per la creazione di codice nell'ambiente di sviluppo di Visual Studio .NET, implica l'aggiunta di un tag [\<summary\>](../../../csharp/programming-guide/xmldoc/summary.md) alla nuova proprietà.  È quindi necessario aggiungere manualmente un tag \<value\> per descrivere il valore rappresentato dalla proprietà.  
  
 Eseguire la compilazione con [\/doc](../../../csharp/language-reference/compiler-options/doc-compiler-option.md) per elaborare in un file i commenti per la creazione della documentazione.  
  
## Esempio  
 [!code-cs[csProgGuideDocComments#14](../../../csharp/programming-guide/xmldoc/codesnippet/csharp/value_1.cs)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Tag consigliati per i commenti relativi alla documentazione](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)