---
title: "Recupero di informazioni sullo schema di database | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 79038d52-f122-4fd4-9bfb-aaa22d6a114b
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Recupero di informazioni sullo schema di database
Il recupero di informazioni sullo schema da un database viene eseguito tramite il processo di individuazione dello schema.  L'individuazione dello schema consente alle applicazioni di richiedere ai provider gestiti di trovare e restituire informazioni sullo schema di database, note anche come *metadati* di un determinato database.  Nella raccolta di schemi vengono esposti vari elementi dello schema del database, quali tabelle, colonne e stored procedure.  Ogni raccolta di schemi contiene una varietà di informazioni sullo schema specifiche del provider usato.  
  
 In ogni provider .NET Framework gestito viene implementato il metodo **GetSchema** nella classe **Connection** e le informazioni sullo schema restituite dal metodo**GetSchema** vengono visualizzate sotto forma di <xref:System.Data.DataTable>.  **GetSchema** è un metodo di overload che fornisce parametri facoltativi per specificare la raccolta di schemi da restituire e per limitare la quantità di informazioni restituite.  
  
 I provider di dati .NET Framework per OLE DB, ODBC, Oracle e SqlClient forniscono un metodo **GetSchemaTable** che restituisce un oggetto DataTable descrivente i metadati della colonna dell'oggetto **Datareader**.  
  
 Il provider di dati .NET Framework per OLE DB presenta le informazioni sullo schema usando anche il metodo <xref:System.Data.OleDb.OleDbConnection.GetOleDbSchemaTable%2A> dell'oggetto <xref:System.Data.OleDb.OleDbConnection>.  Il metodo **GetOleDbSchemaTable** accetta come argomenti un tipo <xref:System.Data.OleDb.OleDbSchemaGuid> che identifica le informazioni sullo schema da restituire e una matrice di restrizioni sulle colonne restituite.  Il metodo **GetOleDbSchemaTable** restituisce un tipo <xref:System.Data.DataTable> compilato con le informazioni richieste sullo schema.  
  
## In questa sezione  
 [GetSchema e raccolte di schemi](../../../../docs/framework/data/adonet/getschema-and-schema-collections.md)  
 Viene descritto il metodo **GetSchema** e come usarlo per recuperare e limitare le informazioni sullo schema da un database.  
  
 Restrizione dello schema  
 Vengono illustrate le restrizioni di schema che è possibile usare con **GetSchema**.  
  
 [Raccolte di schemi comuni](../../../../docs/framework/data/adonet/common-schema-collections.md)  
 Vengono descritte tutte le raccolte di schemi comuni supportate dai provider .NET Framework gestiti.  
  
 [Raccolte di schemi di SQL Server](../../../../docs/framework/data/adonet/sql-server-schema-collections.md)  
 Viene illustrata la raccolta di schemi supportata dal provider .NET Framework per SQL Server.  
  
 [Raccolte di schemi Oracle](../../../../docs/framework/data/adonet/oracle-schema-collections.md)  
 Viene illustrata la raccolta di schemi supportata dal provider .NET Framework per Oracle.  
  
 [Raccolte di schemi ODBC](../../../../docs/framework/data/adonet/odbc-schema-collections.md)  
 Vengono illustrate le raccolte di schemi per i driver ODBC.  
  
 [Raccolte di schemi OLE DB](../../../../docs/framework/data/adonet/ole-db-schema-collections.md)  
 Vengono illustrate le raccolte di schemi per i provider OLE DB.  
  
## Riferimenti  
 <xref:System.Data.Common.DbConnection.GetSchema%2A>  
 Viene descritto il metodo **GetSchema** della classe <xref:System.Data.Common.DbConnection>.  
  
 <xref:System.Data.Odbc.OdbcConnection.GetSchema%2A>  
 Viene descritto il metodo **GetSchema** della classe <xref:System.Data.Odbc.OdbcConnection>.  
  
 <xref:System.Data.OleDb.OleDbConnection.GetSchema%2A>  
 Viene descritto il metodo **GetSchema** della classe <xref:System.Data.OleDb.OleDbConnection>.  
  
 <xref:System.Data.OracleClient.OracleConnection.GetSchema%2A>  
 Viene descritto il metodo **GetSchema** della classe <xref:System.Data.OracleClient.OracleConnection>.  
  
 <xref:System.Data.SqlClient.SqlConnection.GetSchema%2A>  
 Viene descritto il metodo **GetSchema** della classe <xref:System.Data.SqlClient.SqlConnection>.  
  
 <xref:System.Data.Common.DbDataReader.GetSchemaTable%2A>  
 Viene descritto il metodo **GetSchemaTable** della classe <xref:System.Data.Common.DbDataReader>.  
  
 <xref:System.Data.Odbc.OdbcDataReader.GetSchemaTable%2A>  
 Viene descritto il metodo **GetSchemaTable** della classe <xref:System.Data.Odbc.OdbcDataReader>.  
  
 <xref:System.Data.OleDb.OleDbDataReader.GetSchemaTable%2A>  
 Viene descritto il metodo **GetSchemaTable** della classe <xref:System.Data.OleDb.OleDbDataReader>.  
  
 <xref:System.Data.OracleClient.OracleDataReader.GetSchemaTable%2A>  
 Viene descritto il metodo **GetSchemaTable** della classe <xref:System.Data.OracleClient.OracleDataReader>.  
  
 <xref:System.Data.SqlClient.SqlDataReader.GetSchemaTable%2A>  
 Viene descritto il metodo **GetSchemaTable** della classe <xref:System.Data.SqlClient.SqlDataReader>.  
  
## Vedere anche  
 [Recupero e modifica di dati in ADO.NET](../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)