---
title: "Metodi System.DateTimeOffset | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 25b3e5c0-7603-4a70-b3e5-2149e3da69a2
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Metodi System.DateTimeOffset
Una volta eseguito il mapping nel modello a oggetti o nel file di mapping esterno, LINQ to SQL consente di chiamare la maggior parte degli operatori, delle proprietà e dei metodi <xref:System.DateTimeOffset?displayProperty=fullName> dalle query LINQ to SQL.  
  
 Gli unici metodi non supportati sono quelli ereditati da <xref:System.Object?displayProperty=fullName> che non hanno senso nel contesto delle query LINQ to SQL, ad esempio `Finalize`, `GetHashCode`, `GetType` e `MemberwiseClone`.  Questi metodi non sono supportati in quanto LINQ to SQL non è in grado di convertirli per l'esecuzione in SQL Server.  
  
> [!NOTE]
>  La struttura di <xref:System.DateTimeOffset?displayProperty=fullName> CLR \(Common Language Runtime\) e la possibilità da eseguire il mapping a una colonna `DATETIMEOFFSET` SQL con LINQ to SQL richiedono .NET Framework 3.5 SP1 o versione successiva.  La colonna `DATETIMEOFFSET` SQL è disponibile solo in Microsoft SQL Server 2008 e versioni successive.  
  
## Metodi SQLMethods relativi a data e ora  
 Oltre ai metodi offerti dalla struttura di <xref:System.DateTimeOffset>, LINQ to SQL offre i metodi della classe <xref:System.Data.Linq.SqlClient.SqlMethods?displayProperty=fullName> elencati nella tabella seguente per l'uso di data e ora.  
  
||||  
|-|-|-|  
|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffDay%2A>|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffMillisecond%2A>|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffNanosecond%2A>|  
|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffHour%2A>|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffMinute%2A>|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffSecond%2A>|  
|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffMicrosecond%2A>|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffMonth%2A>|<xref:System.Data.Linq.SqlClient.SqlMethods.DateDiffYear%2A>|  
  
## Vedere anche  
 [Concetti relativi alle query](../../../../../../docs/framework/data/adonet/sql/linq/query-concepts.md)   
 [Creazione del modello a oggetti](../../../../../../docs/framework/data/adonet/sql/linq/creating-the-object-model.md)   
 [Mapping di tipi SQL\-CLR](../../../../../../docs/framework/data/adonet/sql/linq/sql-clr-type-mapping.md)