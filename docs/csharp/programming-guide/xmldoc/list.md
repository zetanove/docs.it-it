---
title: "&lt;list&gt; (Guida per programmatori C#) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.technology: 
  - "devlang-csharp"
ms.topic: "article"
f1_keywords: 
  - "list"
  - "<list>"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "<item> (tag XML C#)"
  - "<list> (tag XML C#)"
  - "<listheader> (tag XML C#)"
  - "item (tag XML C#)"
  - "list (tag XML C#)"
  - "listheader (tag XML C#)"
ms.assetid: c9620b1b-c2e6-43f1-ab88-8ab47308ffec
caps.latest.revision: 11
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 11
---
# &lt;list&gt; (Guida per programmatori C#)
## Sintassi  
  
```  
<list type="bullet" | "number" | "table">  
    <listheader>  
        <term>term</term>  
        <description>description</description>  
    </listheader>  
    <item>  
        <term>term</term>  
        <description>description</description>  
    </item>  
</list>  
```  
  
#### Parametri  
 `term`  
 Termine da definire, che verrà definito in `description`.  
  
 `description`  
 Elemento di un elenco puntato o numerato oppure la definizione di un `term`.  
  
## Note  
 Il blocco \<listheader\> viene utilizzato per definire la riga di intestazione di una tabella o di un elenco di definizioni.  Per definire una tabella, è sufficiente specificare una voce per il termine nell'intestazione.  
  
 Ciascun elemento dell'elenco viene specificato tramite un blocco \<item\>.  Quando si crea un elenco di definizioni, è necessario specificare sia `term` che `description`.  Per le tabelle e gli elenchi puntati o numerati, tuttavia, è sufficiente fornire una voce per `description`.  
  
 Gli elenchi e le tabelle possono contenere un numero qualsiasi di blocchi \<item\>.  
  
 Eseguire la compilazione con [\/doc](../../../csharp/language-reference/compiler-options/doc-compiler-option.md) per elaborare in un file i commenti per la creazione della documentazione.  
  
## Esempio  
 [!code-cs[csProgGuideDocComments#6](../../../csharp/programming-guide/xmldoc/codesnippet/csharp/list_1.cs)]  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Tag consigliati per i commenti relativi alla documentazione](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)