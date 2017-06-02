---
title: "Espressioni nelle query LINQ to Entities | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
ms.assetid: d70b502f-6a15-4120-b4fe-500b173ad9cc
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Espressioni nelle query LINQ to Entities
Un'espressione è un frammento di codice che può restituire un singolo valore, oggetto, metodo o spazio dei nomi.  Le espressioni possono contenere un valore letterale, una chiamata al metodo, un operatore e i relativi operandi oppure un nome semplice,  ad esempio il nome di una variabile, un membro di un tipo, un parametro di un metodo, uno spazio dei nomi o un tipo.  Le espressioni possono usare operatori che a loro volta usano altre espressioni come parametri oppure chiamate a metodi i cui parametri sono a loro volta altre chiamate a metodi.  Le espressioni possono pertanto essere da semplici a molto complesse.  
  
 Nelle query [!INCLUDE[linq_entities](../../../../../../includes/linq-entities-md.md)] le espressioni possono contenere qualsiasi elemento consentito dai tipi all'interno dello spazio dei nomi <xref:System.Linq.Expressions>, incluse le espressioni lambda.  Le espressioni che possono essere usate nelle query [!INCLUDE[linq_entities](../../../../../../includes/linq-entities-md.md)] sono un superset delle espressioni che possono essere usate per eseguire query su [!INCLUDE[adonet_ef](../../../../../../includes/adonet-ef-md.md)].  Le espressioni che fanno parte delle query su [!INCLUDE[adonet_ef](../../../../../../includes/adonet-ef-md.md)] sono limitate a operazioni supportate da `ObjectQuery<T>` e dall'origine dati sottostante.  
  
 Nell'esempio seguente il confronto nella clausola `Where` è un'espressione:  
  
 [!code-csharp[DP L2E Conceptual Examples#WhereExpression](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DP L2E Conceptual Examples/CS/Program.cs#whereexpression)]
 [!code-vb[DP L2E Conceptual Examples#WhereExpression](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DP L2E Conceptual Examples/VB/Module1.vb#whereexpression)]  
  
> [!NOTE]
>  I costrutti di linguaggio specifici, ad esempio `unchecked` C\#, non hanno significato in [!INCLUDE[linq_entities](../../../../../../includes/linq-entities-md.md)].  
  
## Contenuto della sezione  
 [Espressioni costanti](../../../../../../docs/framework/data/adonet/ef/language-reference/constant-expressions.md)  
  
 [Espressioni di confronto](../../../../../../docs/framework/data/adonet/ef/language-reference/comparison-expressions.md)  
  
 [Confronti di valori Null](../../../../../../docs/framework/data/adonet/ef/language-reference/null-comparisons.md)  
  
 [Espressioni di inizializzazione](../../../../../../docs/framework/data/adonet/ef/language-reference/initialization-expressions.md)  
  
 [Navigation Properties](http://msdn.microsoft.com/it-it/41e1e6b9-8a57-467d-99d9-1857d2ca2ea5)  
  
## Vedere anche  
 [ADO.NET Entity Framework](../../../../../../docs/framework/data/adonet/ef/index.md)