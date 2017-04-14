---
title: "Sistema di tipi (Entity SQL) | Microsoft Docs"
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
  - "ESQL"
ms.assetid: 818a505b-a196-41dd-aaac-2ccd5f7a2f1a
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Sistema di tipi (Entity SQL)
[!INCLUDE[esql](../../../../../../includes/esql-md.md)] supporta diversi tipi:  
  
-   Tipi primitivi \(semplici\), come `Int32` e `String.`.  
  
-   Tipi nominali definiti nello schema, ad esempio <xref:System.Data.Metadata.Edm.EntityType>, <xref:System.Data.Metadata.Edm.ComplexType> e <xref:System.Data.Metadata.Edm.RelationshipType>.  
  
-   Tipi anonimi non definiti esplicitamente nello schema: <xref:System.Data.Metadata.Edm.CollectionType>, <xref:System.Data.Metadata.Edm.RowType> e <xref:System.Data.Metadata.Edm.RefType>.  
  
 Contenuto della sezione vengono descritti i tipi anonimi non definiti in modo esplicito nello schema ma supportati da [!INCLUDE[esql](../../../../../../includes/esql-md.md)].  Per informazioni sui tipi primitivi e nominali, vedere [Conceptual Model Types \(CSDL\)](http://msdn.microsoft.com/it-it/987b995f-e429-4569-9559-b4146744def4).  
  
## Righe  
 La struttura di una riga dipende dalla sequenza di membri tipizzati e denominati di cui è composta la riga stessa.  Un tipo di riga non dispone dell'identità e non può essere ereditato.  Le istanze dello stesso tipo di riga sono equivalenti se i membri sono rispettivamente equivalenti.  Le righe non hanno alcun comportamento al di là dell'equivalenza strutturale e non dispongono di equivalenti in Common Language Runtime.  Le query possono produrre strutture contenenti righe o raccolte di righe.  L'associazione API tra le query [!INCLUDE[esql](../../../../../../includes/esql-md.md)] e il linguaggio host definisce la realizzazione delle righe nella query che ha prodotto il risultato.  Per informazioni su come costruire un'istanza della riga, vedere [Costruzione di tipi](../../../../../../docs/framework/data/adonet/ef/language-reference/constructing-types-entity-sql.md).  
  
## Raccolte  
 I tipi di raccolta rappresentano zero o più istanze di altri oggetti.  Per informazioni su come costruire una raccolta, vedere [Costruzione di tipi](../../../../../../docs/framework/data/adonet/ef/language-reference/constructing-types-entity-sql.md).  
  
## Riferimenti  
 Un riferimento è un puntatore logico a un'entità specifica in un set di entità specifico.  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] supporta gli operatori seguenti per costruire o annullare i riferimenti, nonché eseguire la navigazione al loro interno:  
  
-   [REF](../../../../../../docs/framework/data/adonet/ef/language-reference/ref-entity-sql.md)  
  
-   [CREATEREF](../../../../../../docs/framework/data/adonet/ef/language-reference/createref-entity-sql.md)  
  
-   [KEY](../../../../../../docs/framework/data/adonet/ef/language-reference/key-entity-sql.md)  
  
-   [DEREF](../../../../../../docs/framework/data/adonet/ef/language-reference/deref-entity-sql.md)  
  
 È possibile navigare da un riferimento all'altro tramite l'operatore \(punto\) di accesso ai membri \(`.`\).  Nel frammento seguente viene estratta la proprietà Id \(di Order\) spostandosi nella proprietà r \(riferimento\).  
  
```  
select o2.r.Id   
from (select ref(o) as r from LOB.Orders as o) as o2   
```  
  
 Se il valore di riferimento è null o la destinazione del riferimento non esiste, il risultato è null.  
  
## Vedere anche  
 [Panoramica su Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-overview.md)   
 [Riferimenti a Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)   
 [CAST](../../../../../../docs/framework/data/adonet/ef/language-reference/cast-entity-sql.md)   
 [Specifiche CSDL, SSDL e MSL](../../../../../../docs/framework/data/adonet/ef/language-reference/csdl-ssdl-and-msl-specifications.md)