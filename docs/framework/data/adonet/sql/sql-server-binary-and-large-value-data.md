---
title: "Dati binari e con valori di grandi dimensioni SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e00827b3-7511-4b2d-91d7-851ca86cc6b5
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# Dati binari e con valori di grandi dimensioni SQL Server
In SQL Server è disponibile l'identificatore `max`, che espande la capacità di archiviazione dei tipi di dati `varchar`, `nvarchar` e `varbinary`.  I tipi `varchar(max)`, `nvarchar(max)` e `varbinary(max)` vengono collettivamente definiti *tipi di dati con valori di grandi dimensioni*.  È possibile usare i tipi di dati con valori di grandi dimensioni per archiviare fino a 2^31\-1 byte di dati.  
  
 In SQL Server 2008 viene introdotto l'attributo FILESTREAM, che non è un tipo di dati ma piuttosto un attributo che può essere definito in una colonna, per consentire l'archiviazione dei dati con valori di grandi dimensioni nel file system anziché nel database.  
  
## In questa sezione  
 [Modifica di dati con valori di grandi dimensioni \(max\) in ADO.NET](../../../../../docs/framework/data/adonet/sql/modifying-large-value-max-data.md)  
 Viene descritto come usare tipi di dati con valori di grandi dimensioni.  
  
 [Dati FILESTREAM](../../../../../docs/framework/data/adonet/sql/filestream-data.md)  
 Viene descritto come usare tipi di dati con valori di grandi dimensioni archiviati in SQL Server 2008 con l'attributo FILESTREAM.  
  
## Vedere anche  
 [Tipi di dati SQL Server e ADO.NET](../../../../../docs/framework/data/adonet/sql/sql-server-data-types.md)   
 [Operazioni sui dati SQL Server in ADO.NET](../../../../../docs/framework/data/adonet/sql/sql-server-data-operations.md)   
 [Recupero e modifica di dati in ADO.NET](../../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)