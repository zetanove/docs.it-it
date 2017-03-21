---
title: "Espressione di tipo &lt;tipo&gt; non è sottoposta a query | Documenti di Microsoft"
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- bc36593
- vbc36593
dev_langs:
- VB
helpviewer_keywords:
- BC36593
ms.assetid: 6f1f5860-bf97-4885-9ebb-bc87d028095c
caps.latest.revision: 5
author: stevehoag
ms.author: shoag
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 1e7e1e2652cf730ef6d14b0579d8a3ee3de67fbb
ms.lasthandoff: 03/13/2017

---
# <a name="expression-of-type-lttypegt-is-not-queryable"></a>Espressione di tipo &lt;tipo&gt; non è sottoposta a query
Espressione di tipo \<tipo > non è sottoposta a query. Assicurarsi che non manchi un'importazione di riferimento e/o dello spazio dei nomi di assembly per il provider LINQ.  
  
 Tipi queryable sono definiti nel <xref:System.Linq>, <xref:System.Data.Linq>, e <xref:System.Xml.Linq>gli spazi dei nomi.</xref:System.Xml.Linq> </xref:System.Data.Linq> </xref:System.Linq> È necessario importare uno o più di questi spazi dei nomi per eseguire query LINQ.  
  
 Il <xref:System.Linq>dello spazio dei nomi consente agli oggetti di query, ad esempio raccolte e matrici utilizzando LINQ.</xref:System.Linq>  
  
 Il <xref:System.Data.Linq>dello spazio dei nomi consente di eseguire query su DataSet ADO.NET e SQL Server database utilizzando LINQ.</xref:System.Data.Linq>  
  
 Il <xref:System.Xml.Linq>dello spazio dei nomi consente di eseguire query XML utilizzando LINQ e utilizzare le funzionalità XML in Visual Basic.</xref:System.Xml.Linq>  
  
 **ID errore:** BC36593  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
1.  Aggiungere un `Import` istruzione per il <xref:System.Linq>, <xref:System.Data.Linq>, o <xref:System.Xml.Linq>dello spazio dei nomi al file di codice.</xref:System.Xml.Linq> </xref:System.Data.Linq> </xref:System.Linq> È inoltre possibile importare gli spazi dei nomi per il progetto utilizzando il **riferimenti** pagina di Progettazione progetti (**progetto**).  
  
2.  Assicurarsi che il tipo identificato come origine della query è un tipo queryable. Ovvero, un tipo che implementa <xref:System.Collections.Generic.IEnumerable%601>o <xref:System.Linq.IQueryable%601>.</xref:System.Linq.IQueryable%601> </xref:System.Collections.Generic.IEnumerable%601>  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Linq></xref:System.Linq>   
 <xref:System.Data.Linq></xref:System.Data.Linq>   
 <xref:System.Xml.Linq>   
 [Introduzione a LINQ in Visual Basic](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [LINQ](../../../visual-basic/programming-guide/language-features/linq/index.md)   
 [XML](../../../visual-basic/programming-guide/language-features/xml/index.md)   
 [I riferimenti e istruzione Imports](../../../visual-basic/programming-guide/program-structure/references-and-the-imports-statement.md)   
 [Istruzione Imports (tipo e spazio dei nomi .NET)](../../../visual-basic/language-reference/statements/imports-statement-net-namespace-and-type.md)   
 [Pagina Riferimenti, Creazione progetti (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/references-page-project-designer-visual-basic)
