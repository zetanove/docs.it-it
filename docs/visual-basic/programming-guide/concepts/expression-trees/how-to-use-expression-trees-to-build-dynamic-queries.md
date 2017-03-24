---
title: 'Procedura: utilizzare strutture ad albero dell&quot;espressione per creare query dinamiche (Visual Basic) | Documenti di Microsoft'
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
ms.assetid: 16278787-7532-4b65-98b2-7a412406c4ee
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 8d69be78a9f3568535dffe54e21af80c6eb12f70
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-use-expression-trees-to-build-dynamic-queries-visual-basic"></a>Procedura: utilizzare strutture ad albero dell'espressione per creare query dinamiche (Visual Basic)
In LINQ, gli alberi delle espressioni vengono utilizzate per rappresentare le query strutturate destinate alle origini dei dati che implementano <xref:System.Linq.IQueryable%601>.</xref:System.Linq.IQueryable%601> Ad esempio, implementa il provider LINQ di <xref:System.Linq.IQueryable%601>interfaccia per l'esecuzione di query su archivi dati relazionali.</xref:System.Linq.IQueryable%601> Il compilatore Visual Basic vengono compilate in query destinate a tali origini dati nel codice che compila un albero delle espressioni in fase di esecuzione. Il provider di query può quindi attraversare la struttura di dati ad albero di espressione e convertirla in un linguaggio di query appropriato per l'origine dati.  
  
 Gli alberi delle espressioni vengono utilizzate anche in LINQ per rappresentare le espressioni lambda che vengono assegnate a variabili di tipo <xref:System.Linq.Expressions.Expression%601>.</xref:System.Linq.Expressions.Expression%601>  
  
 In questo argomento viene descritto come utilizzare gli alberi delle espressioni per creare query dinamiche di LINQ. Query dinamiche sono utili quando le specifiche di una query non sono noti in fase di compilazione. Ad esempio, un'applicazione può fornire un'interfaccia utente che consente all'utente finale specificare uno o più predicati per filtrare i dati. Per utilizzare LINQ per eseguire la query, questo tipo di applicazione deve utilizzare strutture ad albero dell'espressione per creare la query LINQ in fase di esecuzione.  
  
## <a name="example"></a>Esempio  
 Nell'esempio seguente viene illustrato come utilizzare gli alberi delle espressioni per costruire una query su un `IQueryable` origine dati e quindi eseguirla. Il codice verrà compilato un albero delle espressioni per rappresentare la query seguente:  
  
 `companies.Where(Function(company) company.ToLower() = "coho winery" OrElse company.Length > 16).OrderBy(Function(company) company)`  
  
 I metodi factory il <xref:System.Linq.Expressions>dello spazio dei nomi vengono utilizzati per creare alberi delle espressioni che rappresentano le espressioni che costituiscono la query.</xref:System.Linq.Expressions> Le espressioni che rappresentano le chiamate ai metodi degli operatori di query standard si intende il <xref:System.Linq.Queryable>implementazioni di questi metodi.</xref:System.Linq.Queryable> L'albero delle espressioni finale viene passato per il <xref:System.Linq.IQueryProvider.CreateQuery%60%601%28System.Linq.Expressions.Expression%29>implementazione del provider del `IQueryable` origine dati per creare una query eseguibile di tipo `IQueryable`.</xref:System.Linq.IQueryProvider.CreateQuery%60%601%28System.Linq.Expressions.Expression%29> I risultati vengono ottenuti enumerando quella variabile di query.  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
 Questo codice utilizza un numero fisso di espressioni nel predicato che viene passato per il `Queryable.Where` metodo. Tuttavia, è possibile scrivere un'applicazione che combina un numero variabile di espressioni del predicato che dipende da input dell'utente. È anche possibile modificare gli operatori query standard che vengono chiamati nella query, in base all'input dell'utente.  
  
## <a name="compiling-the-code"></a>Compilazione del codice  
  
-   Creare un nuovo **applicazione Console** progetto.  
  
-   Se non è già presente, aggiungere un riferimento a System.Core.dll.  
  
-   Includere lo spazio dei nomi System.Linq.Expressions.  
  
-   Copiare il codice dell'esempio e incollarlo il `Main` `Sub` procedura.  
  
## <a name="see-also"></a>Vedere anche  
 [Alberi delle espressioni (Visual Basic)](../../../../visual-basic/programming-guide/concepts/expression-trees/index.md)   
 [Procedura: eseguire alberi delle espressioni (Visual Basic)](../../../../visual-basic/programming-guide/concepts/expression-trees/how-to-execute-expression-trees.md)
