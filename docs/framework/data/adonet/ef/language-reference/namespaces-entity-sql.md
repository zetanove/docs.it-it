---
title: "Spazi dei nomi (Entity SQL) | Microsoft Docs"
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
ms.assetid: 83991c21-60db-4af9-aca3-b416f6cae98e
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Spazi dei nomi (Entity SQL)
In [!INCLUDE[esql](../../../../../../includes/esql-md.md)] vengono introdotti gli spazi dei nomi per evitare conflitti di nome per gli identificatori globali, ad esempio nomi di tipi, set di entità, funzioni e così via.  Il supporto dello spazio dei nomi in [!INCLUDE[esql](../../../../../../includes/esql-md.md)] è analogo a quello in [!INCLUDE[dnprdnshort](../../../../../../includes/dnprdnshort-md.md)].  
  
 [!INCLUDE[esql](../../../../../../includes/esql-md.md)] fornisce due tipi di clausola USING: spazi dei nomi qualificati \(dove viene fornito un alias più breve per lo spazio dei nomi\) e spazi dei nomi non qualificati, come illustrato nell'esempio seguente:  
  
 `USING System.Data;`  
  
 `USING tsql = System.Data;`  
  
## Regole per la risoluzione dei nomi  
 Se non è possibile risolvere un identificatore negli ambiti locali, [!INCLUDE[esql](../../../../../../includes/esql-md.md)] tenta di individuare il nome negli ambiti globali \(gli spazi dei nomi\).  [!INCLUDE[esql](../../../../../../includes/esql-md.md)] tenta innanzitutto di confrontare l'identificatore \(prefisso\) con uno degli spazi dei nomi qualificati.  Se è presente una corrispondenza, tramite [!INCLUDE[esql](../../../../../../includes/esql-md.md)] viene eseguito un tentativo di risolvere il resto dell'identificatore nello spazio dei nomi specificato.  Se non viene trovata alcuna corrispondenza, viene generata un'eccezione .  
  
 Tramite [!INCLUDE[esql](../../../../../../includes/esql-md.md)] viene quindi eseguito un tentativo di cercare l'identificatore in tutti gli spazi dei nomi non qualificati \(specificati nel prologo\).  Se l'identificatore può essere individuato esattamente in uno spazio dei nomi, viene restituito tale percorso.  Se la corrispondenza per l'identificatore è presente in più di uno spazio dei nomi, viene generata un'eccezione.  Se non è possibile identificare alcuno spazio dei nomi per l'identificatore, [!INCLUDE[esql](../../../../../../includes/esql-md.md)] passa il nome all'ambito esterno successivo \(oggetto <xref:System.Data.Common.DbCommand> o <xref:System.Data.Common.DbConnection>\), come illustrato nell'esempio seguente:  
  
```  
SELECT TREAT(p AS NamespaceName.Employee)  
FROM ContainerName.Person AS p  
WHERE p IS OF (NamespaceName.Employee)  
```  
  
## Differenze rispetto a .NET Framework  
 In [!INCLUDE[dnprdnshort](../../../../../../includes/dnprdnshort-md.md)] non è possibile usare spazi dei nomi parzialmente qualificati.  Ciò non è consentito in [!INCLUDE[esql](../../../../../../includes/esql-md.md)].  
  
## Uso di ADO.NET  
 Le query sono espresse attraverso oggetti <xref:System.Data.Common.DbCommand> ADO.NET.  Gli oggetti <xref:System.Data.Common.DbCommand> possono essere creati in base a oggetti <xref:System.Data.Common.DbConnection>.  Anche gli spazi dei nomi possono essere specificati come parte degli oggetti <xref:System.Data.Common.DbCommand> e <xref:System.Data.Common.DbConnection>.  Se [!INCLUDE[esql](../../../../../../includes/esql-md.md)] non è in grado di risolvere un identificatore all'interno della query stessa, viene eseguito un tentativo negli spazi dei nomi esterni \(in base a regole simili\).  
  
## Vedere anche  
 [Riferimenti a Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-reference.md)   
 [Panoramica su Entity SQL](../../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-overview.md)