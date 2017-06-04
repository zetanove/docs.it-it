---
title: "Tipi di dati di base | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: eca2c472-9548-4800-bd31-5d8d9f11752b
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Tipi di dati di base
Poiché le query LINQ to SQL vengono convertite in Transact\-SQL prima di essere eseguite in Microsoft SQL Server,  in LINQ to SQL è supportata buona parte delle funzionalità predefinite di SQL Server  per i tipi di dati di base.  
  
## Cast  
 I cast impliciti o espliciti vengono abilitati da un tipo CLR di origine in un tipo CLR di destinazione se è disponibile una conversione valida simile all'interno di SQL Server.  Per altre informazioni sul cast CLR vedere [Funzione CType](../Topic/CType%20Function%20\(Visual%20Basic\).md) \([!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)]\) e [as](../Topic/as%20\(C%23%20Reference\).md).  Dopo la conversione i cast modificano il comportamento delle operazioni eseguite su un'espressione CLR, in modo che corrisponda a quello di altre espressioni CLR di cui viene eseguito naturalmente il mapping al tipo di destinazione. I cast sono inoltre convertibili nel contesto del mapping di ereditarietà.  È possibile eseguire il cast degli oggetti in sottotipi dell'entità più specifici, in modo che sia possibile accedere ai dati specifici del sottotipo.  
  
## Operatori di uguaglianza  
 LINQ to SQL all'interno di query LINQ to SQL supporta i seguenti operatori di uguaglianza sui tipi di dati di base:  
  
-   Operatore di uguaglianza e disuguaglianza: tali operatori sono supportati per i tipi numerici <xref:System.Boolean>, <xref:System.DateTime> e <xref:System.TimeSpan>.  Per altre informazioni sugli operatori [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)] `=` e `<>`, vedere [Comparison Operators](../Topic/Comparison%20Operators%20\(Visual%20Basic\).md). Per ulteriori informazioni sugli operatori di confronto C\# `==` e `!=`, vedere rispettivamente [Operatore \=\=](../Topic/==%20Operator%20\(C%23%20Reference\).md) e [Operatore \!\=](../Topic/!=%20Operator%20\(C%23%20Reference\).md).  
  
-   Operatore Is: l'operatore `IS` supporta la conversione quando viene usato il mapping di ereditarietà.  È possibile usarlo invece di testare direttamente la colonna del discriminatore per determinare se un oggetto è di un tipo di entità specifico e viene convertito in un controllo nella colonna del discriminatore.  Per altre informazioni sugli operatori Is di Visual Basic e C\#, vedere [Is Operator](../Topic/Is%20Operator%20\(Visual%20Basic\).md) e [is](../Topic/is%20\(C%23%20Reference\).md).  
  
## Vedere anche  
 [Mapping di tipi SQL\-CLR](../../../../../../docs/framework/data/adonet/sql/linq/sql-clr-type-mapping.md)   
 [Tipi di dati e funzioni](../../../../../../docs/framework/data/adonet/sql/linq/data-types-and-functions.md)