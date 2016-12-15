---
title: "&lt;include&gt; (Visual Basic) | Microsoft Docs"
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
  - "include XML tag"
  - "<include> XML tag"
ms.assetid: ba8e9173-82cd-460b-8938-a075a2dfb36d
caps.latest.revision: 11
caps.handback.revision: 11
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# &lt;include&gt; (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Fa riferimento a un altro file in cui sono descritti i tipi e i membri del codice sorgente.  
  
## Sintassi  
  
```  
<include file="filename" path="tagpath[@name='id']" />  
```  
  
#### Parametri  
 `filename`  
 Obbligatorio.  Nome del file che contiene la documentazione.  È possibile qualificare il nome del file tramite un percorso.  Racchiudere `filename` tra virgolette doppie \(" "\).  
  
 `tagpath`  
 Obbligatorio.  Percorso dei tag di `filename` che porta al `name` del tag.  Racchiudere il percorso tra virgolette doppie \(" "\).  
  
 `name`  
 Obbligatorio.  Identificatore del nome contenuto nel tag che precede i commenti.  `Name` avrà un `id`.  
  
 `id`  
 Obbligatorio.  ID del tag che precede i commenti.  Racchiudere l'ID tra virgolette singole \(' '\).  
  
## Note  
 Utilizzare il tag `<include>` per fare riferimento ai commenti di un altro file che descrivono i tipi e i membri del codice sorgente,  eliminando la necessità di inserire i commenti relativi alla documentazione direttamente nel file del codice sorgente.  
  
 Il tag `<include>` utilizza la raccomandazione XML Path Language \(XPath\) Version 1.0 del WC3.  Per ulteriori informazioni sulla personalizzazione di `<include>`, visitare il sito Web all'indirizzo http:\/\/www.w3.org\/TR\/xpath \(informazioni in lingua inglese\).  
  
## Esempio  
 Nell'esempio riportato di seguito il tag `<include>` viene utilizzato per importare i commenti relativi alla documentazione dei membri da un file denominato `commentFile.xml`.  
  
 [!code-vb[VbVbcnXmlDocComments#4](../../../visual-basic/language-reference/xmldoc/codesnippet/VisualBasic/include_1.vb)]  
  
 Il formato di `commentFile.xml` è il seguente:  
  
```  
<Docs>  
<Members name="Open">  
<summary>Opens a file.</summary>  
<param name="filename">File name to open.</param>  
</Members>  
<Members name="Close">  
<summary>Closes a file.</summary>  
<param name="filename">File name to close.</param>  
</Members>  
</Docs>  
```  
  
## Vedere anche  
 [XML Comment Tags](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)