---
title: "Expression of type &lt;type&gt; is not queryable | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "bc36593"
  - "vbc36593"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "BC36593"
ms.assetid: 6f1f5860-bf97-4885-9ebb-bc87d028095c
caps.latest.revision: 5
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 5
---
# Expression of type &lt;type&gt; is not queryable
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

L'espressione di tipo \<tipo\> non può essere sottoposta a query.Verificare che sia presente un riferimento all'assembly e\/o un'importazione dello spazio dei nomi per il provider LINQ.  
  
 I tipi sottoponibili a query sono definiti negli spazi dei nomi <xref:System.Linq>, <xref:System.Data.Linq> e <xref:System.Xml.Linq>.  È necessario importare uno o più di questi spazi dei nomi per eseguire query LINQ.  
  
 Lo spazio dei nomi <xref:System.Linq> consente di eseguire una query su oggetti, ad esempio raccolte e matrici, utilizzando LINQ.  
  
 Lo spazio dei nomi <xref:System.Data.Linq> consente di eseguire una query su dataset ADO.NET e database SQL Server utilizzando LINQ.  
  
 Lo spazio dei nomi <xref:System.Xml.Linq> consente di eseguire query XML utilizzando LINQ e di utilizzare le funzionalità XML di Visual Basic.  
  
 **ID errore:** BC36593  
  
### Per correggere l'errore  
  
1.  Aggiungere un'istruzione `Import` per lo spazio dei nomi <xref:System.Linq>, <xref:System.Data.Linq> o <xref:System.Xml.Linq> al file di codice.  È inoltre possibile importare spazi dei nomi per il progetto utilizzando la pagina **Riferimenti** di Progettazione progetti \(**Progetti**\).  
  
2.  Assicurarsi che il tipo identificato come origine della query sia un tipo sottoponibile a query,  ovvero un tipo che implementa <xref:System.Collections.Generic.IEnumerable%601> o <xref:System.Linq.IQueryable%601>.  
  
## Vedere anche  
 <xref:System.Linq>   
 <xref:System.Data.Linq>   
 <xref:System.Xml.Linq>   
 [Introduction to LINQ in Visual Basic](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [LINQ](../../../visual-basic/programming-guide/language-features/linq/index.md)   
 [XML](../../../visual-basic/programming-guide/language-features/xml/index.md)   
 [References and the Imports Statement](../../../visual-basic/programming-guide/program-structure/references-and-the-imports-statement.md)   
 [Imports Statement \(.NET Namespace and Type\)](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)   
 [Riferimenti \(pagina\), Creazione progetti \(Visual Basic\)](/visual-studio/ide/reference/references-page-project-designer-visual-basic)