---
title: "Connessione a un&#39;origine dati in ADO.NET | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9abc3f92-1be3-4e1a-b360-762dc689650e
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Connessione a un&#39;origine dati in ADO.NET
In ADO.NET è possibile usare un oggetto **Connection** per connettersi a un'origine dati specifica inserendo le informazioni di autenticazione necessarie in una stringa di connessione.  L'oggetto **Connection** usato dipende dal tipo dell'origine dati.  
  
 Per ogni provider di dati .NET Framework incluso in .NET Framework è disponibile un oggetto <xref:System.Data.Common.DbConnection>: nel provider di dati .NET Framework per OLE DB è incluso un oggetto <xref:System.Data.OleDb.OleDbConnection>, in quello per SQL Server è incluso un oggetto <xref:System.Data.SqlClient.SqlConnection>, in quello per ODBC è incluso un oggetto <xref:System.Data.Odbc.OdbcConnection> e in quello per Oracle è incluso un oggetto <xref:System.Data.OracleClient.OracleConnection>.  
  
## In questa sezione  
 [Esecuzione della connessione](../../../../docs/framework/data/adonet/establishing-the-connection.md)  
 Viene descritto come usare un oggetto **Connection** per stabilire una connessione a un'origine dati.  
  
 [Eventi di connessione](../../../../docs/framework/data/adonet/connection-events.md)  
 Viene descritta la procedura per usare un evento **InfoMessage** per recuperare i messaggi informativi da un'origine dati.  
  
## Vedere anche  
 [Stringhe di connessione](../../../../docs/framework/data/adonet/connection-strings.md)   
 [Pool di connessioni](../../../../docs/framework/data/adonet/connection-pooling.md)   
 [Comandi e parametri](../../../../docs/framework/data/adonet/commands-and-parameters.md)   
 [DataAdapter e DataReader](../../../../docs/framework/data/adonet/dataadapters-and-datareaders.md)   
 [Transazioni e concorrenza](../../../../docs/framework/data/adonet/transactions-and-concurrency.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)