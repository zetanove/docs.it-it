---
title: "Tipi di dati SQL Server e ADO.NET | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 81b43550-23e8-43bb-b460-7eb8ac825c33
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# Tipi di dati SQL Server e ADO.NET
SQL Server e .NET Framework sono basati su sistemi di tipi diversi che possono comportare una potenziale perdita di dati.  Per mantenere l'integrità dei dati, il provider di dati .NET Framework per SQL Server \(<xref:System.Data.SqlClient>\) fornisce metodi delle funzioni di accesso tipizzate per l'uso dei dati SQL Server.  È possibile usare le enumerazioni nelle classi <xref:System.Data.SqlDbType> per specificare i tipi di dati <xref:System.Data.SqlClient.SqlParameter>.  
  
 Per altre informazioni e una tabella in cui sono descritti i mapping tra tipi di dati SQL Server e .NET Framework, vedere [Mapping dei tipi di dati SQL Server](../../../../../docs/framework/data/adonet/sql-server-data-type-mappings.md).  
  
 In SQL Server 2008 vengono introdotti nuovi tipi di dati progettati per soddisfare le esigenze aziendali di uso di dati relativi a data e ora, strutturati, semistrutturati e non strutturati.  Questi tipi sono illustrati nella documentazione online di SQL Server 2008.  
  
 I tipi di dati SQL Server disponibili per l'uso nell'applicazione dipendono dalla versione di SQL Server in uso.  Per altre informazioni, vedere la versione rilevante della documentazione online di SQL Server nella tabella seguente.  
  
 **Documentazione online di SQL Server**  
  
1.  [Tipi di dati \(Motore di database\)](http://go.microsoft.com/fwlink/?LinkID=107468)  
  
## In questa sezione  
 [SqlTypes e il DataSet](../../../../../docs/framework/data/adonet/sql/sqltypes-and-the-dataset.md)  
 Viene descritto il supporto dei tipi per `SqlTypes` in `DataSet`.  
  
 [Gestione di valori null](../../../../../docs/framework/data/adonet/sql/handling-null-values.md)  
 Viene illustrato come usare i valori null e la logica a tre valori.  
  
 [Confronto di valori GUID e uniqueidentifier \(ADO.NET\)](../../../../../docs/framework/data/adonet/sql/comparing-guid-and-uniqueidentifier-values.md)  
 Viene illustrato come usare valori GUID e uniqueidentifier in SQL Server e in .NET Framework.  
  
 [Dati relativi a data e ora](../../../../../docs/framework/data/adonet/sql/date-and-time-data.md)  
 Viene descritto come usare i nuovi tipi di dati relativi a data e ora in SQL Server 2008.  
  
 [Tipi di grandi dimensioni definiti dall'utente](../../../../../docs/framework/data/adonet/sql/large-udts.md)  
 Viene illustrato come recuperare i dati dai tipi UDT con valori di grandi dimensioni introdotti in SQL Server 2008.  
  
 [Dati XML in SQL Server](../../../../../docs/framework/data/adonet/sql/xml-data-in-sql-server.md)  
 Viene descritto come usare i dati XML recuperati da SQL Server.  
  
## Riferimenti  
 <xref:System.Data.DataSet>  
 Vengono descritti la classe `DataSet` e tutti i relativi membri.  
  
 <xref:System.Data.SqlTypes>  
 Vengono descritti lo spazio dei nomi `SqlTypes` e tutti i relativi membri.  
  
 <xref:System.Data.SqlDbType>  
 Vengono descritti l'enumerazione `SqlDbType` e tutti i relativi membri.  
  
 <xref:System.Data.DbType>  
 Vengono descritti l'enumerazione `DbType` e tutti i relativi membri.  
  
## Vedere anche  
 [Mapping dei tipi di dati SQL Server](../../../../../docs/framework/data/adonet/sql-server-data-type-mappings.md)   
 [Configurazione dei parametri e tipi di dati dei parametri](../../../../../docs/framework/data/adonet/configuring-parameters-and-parameter-data-types.md)   
 [Parametri valutati a livello di tabella](../../../../../docs/framework/data/adonet/sql/table-valued-parameters.md)   
 [Dati binari e con valori di grandi dimensioni SQL Server](../../../../../docs/framework/data/adonet/sql/sql-server-binary-and-large-value-data.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)