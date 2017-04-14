---
title: "Query LINQ to SQL | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f4897aaa-7f44-4c20-a471-b948c2971aae
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Query LINQ to SQL
Le query [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] vengono definite usando la stessa sintassi usata in [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)].  La sola differenza riguarda il mapping degli oggetti a cui viene fatto riferimento nelle query, che viene eseguito agli elementi in un database.  Per altre informazioni, vedere [Introduction to LINQ Queries \(C\#\)](../Topic/Introduction%20to%20LINQ%20Queries%20\(C%23\).md).  
  
 In [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] le query create vengono convertite in query SQL equivalenti e inviate al server per l'elaborazione. In particolare l'applicazione utilizza l'API [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] per richiedere l'esecuzione di query.  Il provider [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] trasforma quindi la query in testo SQL e delega l'esecuzione al provider ADO, che restituisce i risultati della query come `DataReader`.  Il provider [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] converte i risultati di ADO in una raccolta <xref:System.Linq.IQueryable> di oggetti utente.  
  
> [!NOTE]
>  Per la maggior parte dei metodi e degli operatori nei tipi [!INCLUDE[dnprdnshort](../../../../../../includes/dnprdnshort-md.md)] incorporati sono disponibili conversioni dirette in SQL.  Quelli che non possono essere convertiti da [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)] generano eccezioni in fase di esecuzione.  Per altre informazioni, vedere [Mapping di tipi SQL\-CLR](../../../../../../docs/framework/data/adonet/sql/linq/sql-clr-type-mapping.md).  
  
 Nella tabella seguente sono illustrate le similitudini e le differenze tra [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)] e gli elementi delle query [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  
  
|Item|Query LINQ|Query [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]|  
|----------|----------------|----------------------------------------------------------------------|  
|Tipo restituito della variabile locale che contiene la query \(per le query che restituiscono sequenze\)|`IEnumerable` generico|`IQueryable` generico|  
|Specifica dell'origine dati|Viene usata la clausola `From` \([!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)]\) o `from` \(C\#\)|Idem|  
|Filtro|Viene usata la clausola `Where`\/`where`|Idem|  
|Raggruppamento|Viene usata la clausola `Group…By`\/`groupby`|Idem|  
|Selezione \(proiezione\)|Viene usata la clausola `Select`\/`select`|Idem|  
|Esecuzione posticipata e immediata|Vedere [Introduction to LINQ Queries \(C\#\)](../Topic/Introduction%20to%20LINQ%20Queries%20\(C%23\).md)|Idem|  
|Implementazione di join|Viene usata la clausola `Join`\/`join`|Può essere usata la clausola `Join`\/`join`, ma più efficacemente viene usato l'attributo <xref:System.Data.Linq.Mapping.AssociationAttribute>.  Per altre informazioni, vedere [Esecuzione di query tra relazioni](../../../../../../docs/framework/data/adonet/sql/linq/querying-across-relationships.md).|  
|Esecuzione in modalità remota e locale||Per altre informazioni, vedere [Esecuzione in modalità locale e remota](../../../../../../docs/framework/data/adonet/sql/linq/remote-vs-local-execution.md).|  
|Esecuzione di query mediante trasmissione o memorizzate nella cache|Non applicabile in un scenario con memoria locale||  
  
## Vedere anche  
 [Introduction to LINQ Queries \(C\#\)](../Topic/Introduction%20to%20LINQ%20Queries%20\(C%23\).md)   
 [Basic LINQ Query Operations](../Topic/Basic%20LINQ%20Query%20Operations%20\(C%23\).md)   
 [Type Relationships in LINQ Query Operations](../Topic/Type%20Relationships%20in%20LINQ%20Query%20Operations%20\(C%23\).md)   
 [Concetti relativi alle query](../../../../../../docs/framework/data/adonet/sql/linq/query-concepts.md)