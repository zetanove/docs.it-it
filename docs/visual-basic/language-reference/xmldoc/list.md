---
title: "&lt;list&gt; (Visual Basic) | Microsoft Docs"
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
  - "listheader XML tag"
  - "<item> XML tag"
  - "<list> XML tag"
  - "<listheader> XML tag"
  - "term XML tag"
  - "list XML tag"
  - "<description> XML tag"
  - "description XML tag"
  - "item XML tag"
  - "<term> XML tag"
ms.assetid: ec35fced-d58e-4520-a764-0691256e014b
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# &lt;list&gt; (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Definisce un elenco o una tabella.  
  
## Sintassi  
  
```  
<list type="type">  
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
 `type`  
 Tipo dell'elenco.  Deve corrispondere a "bullet", "number" o "table" rispettivamente per un elenco puntato, numerato o una tabella a due colonne.  
  
 `term`  
 Utilizzato solo quando `type` è "table". Termine da definire, definito nel tag di descrizione.  
  
 `description`  
 Quando il parametro `type` è "bullet" o "number", `description` è una voce dell'elenco. Quando invece `type` è "table", `description` corrisponde alla definizione di `term`.  
  
## Note  
 Il blocco `<listheader>` definisce l'intestazione di una tabella o di un elenco di definizioni.  Per definire una tabella, è sufficiente specificare una voce per il parametro `term` nell'intestazione.  
  
 Ciascun elemento dell'elenco viene specificato tramite un blocco `<item>`.  Quando si crea un elenco di definizioni, è necessario specificare sia `term` che `description`.  Per le tabelle e gli elenchi puntati o numerati, tuttavia, è sufficiente fornire una voce per `description`.  
  
 Gli elenchi e le tabelle possono contenere tutti i blocchi `<item>` necessari.  
  
 Eseguire la compilazione con [\/doc](../../../visual-basic/reference/command-line-compiler/doc.md) per elaborare in un file i commenti relativi alla documentazione.  
  
## Esempio  
 In questo esempio il tag `<list>` viene utilizzato per definire un elenco puntato nella sezione relativa alle note.  
  
 [!code-vb[VbVbcnXmlDocComments#5](../../../visual-basic/language-reference/xmldoc/codesnippet/visualbasic/list_1.vb)]  
  
## Vedere anche  
 [XML Comment Tags](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)