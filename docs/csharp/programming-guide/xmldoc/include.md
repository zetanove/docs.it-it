---
title: "&lt;include&gt; (Guida per programmatori C#) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "include"
  - "<include>"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "<include> (tag XML C#)"
  - "include (tag XML C#)"
ms.assetid: a8a70302-6196-4643-bd09-ef33f411f18f
caps.latest.revision: 19
caps.handback.revision: 19
author: "BillWagner"
ms.author: "wiwagn"
manager: "wpickett"
---
# &lt;include&gt; (Guida per programmatori C#)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

## Sintassi  
  
```  
<include file='filename' path='tagpath[@name="id"]' />  
```  
  
#### Parametri  
 `filename`  
 Nome del file XML che contiene la documentazione.  È possibile qualificare il nome del file tramite un percorso.  Racchiudere `filename` tra virgolette singole \(' '\).  
  
 `tagpath`  
 Percorso dei tag di `filename` che porta al `name` del tag.  Racchiudere il percorso tra virgolette singole \(' '\).  
  
 `name`  
 Identificatore del nome contenuto nel tag che precede i commenti. `name` ha sempre un `id`.  
  
 `id`  
 ID del tag che precede i commenti.  Racchiudere l'ID tra virgolette doppie \(" "\).  
  
## Note  
 Il tag \<include\> consente di fare riferimento ai commenti in un altro file che descrivono i tipi e i membri del codice sorgente,  eliminando la necessità di inserire i commenti relativi alla documentazione direttamente nel file del codice sorgente.  Inserendo la documentazione in un file separato, è possibile applicare separatamente il controllo del codice sorgente alla documentazione dal codice sorgente.  Una persona può disporre del file di codice sorgente estratto e un altro utente può disporre del file della documentazione estratto.  
  
 Il tag \<include\> utilizza la sintassi XML XPath.  Per informazioni sulla personalizzazione dell'utilizzo di \<include\>, consultare la documentazione relativa a XPath.  
  
## Esempio  
 In questo esempio vengono presi in considerazione più file.  Il primo file, che utilizza \<include\>, è riportato di seguito.  
  
 [!code-cs[csProgGuideDocComments#5](../../../csharp/programming-guide/xmldoc/codesnippet/CSharp/include_1.cs)]  
  
 Nel secondo file, xml\_include\_tag.doc, sono contenuti i seguenti commenti relativi alla documentazione:  
  
```  
<MyDocs>  
  
<MyMembers name="test">  
<summary>  
The summary for this type.  
</summary>  
</MyMembers>  
  
<MyMembers name="test2">  
<summary>  
The summary for this other type.  
</summary>  
</MyMembers>  
  
</MyDocs>  
```  
  
## Output di programma  
 L'output seguente viene generato quando si compilano le classi Test e Test2 con la riga di comando seguente: `/doc:DocFileName.xml.`. In Visual Studio, è possibile specificare l'opzione dei commenti XML relativi alla documentazione nel riquadro Compilazione della Progettazione progetti.  Se tramite il compilatore C\# viene visualizzato il tag \<include\>, i commenti relativi alla documentazione verranno cercati nel file xml\_include\_tag.doc anziché nel file di origine corrente.  Il compilatore genera quindi il file DocFileName.xml utilizzato dagli strumenti della documentazione come [Sandcastle](http://go.microsoft.com/fwlink/?LinkId=124061) \(la pagina potrebbe essere in inglese\) per realizzare la documentazione finale.  
  
```  
<?xml version="1.0"?>   
<doc>   
    <assembly>   
        <name>xml_include_tag</name>   
    </assembly>   
    <members>   
        <member name="T:Test">   
            <summary>   
The summary for this type.   
</summary>   
        </member>   
        <member name="T:Test2">   
            <summary>   
The summary for this other type.   
</summary>   
        </member>   
    </members>   
</doc>   
```  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Tag consigliati per i commenti relativi alla documentazione](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)