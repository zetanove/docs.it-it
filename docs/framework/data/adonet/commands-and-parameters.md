---
title: "Comandi e parametri | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b623f810-d871-49a5-b0f5-078cc3c34db6
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Comandi e parametri
Una volta stabilita una connessione a un'origine dati, è possibile eseguire i comandi e restituire i risultati dell'origine dati usando un oggetto <xref:System.Data.Common.DbCommand>.  È possibile creare un comando usando uno dei costruttori di comando del provider di dati .NET Framework usato.  I costruttori possono accettare argomenti facoltativi, ad esempio un'istruzione SQL da eseguire nell'origine dati, un oggetto <xref:System.Data.Common.DbConnection> o un oggetto <xref:System.Data.Common.DbTransaction>.  È inoltre possibile configurare tali oggetti come proprietà del comando,  nonché creare un comando per una particolare connessione usando il metodo <xref:System.Data.Common.DbConnection.CreateCommand%2A> di un oggetto `DbConnection`.  È possibile configurare l'istruzione SQL eseguita dal comando tramite la proprietà <xref:System.Data.Common.DbCommand.CommandText%2A>.  
  
 In ogni provider di dati .NET Framework fornito con .NET Framework è incluso un oggetto `Command`.  Nel provider di dati .NET Framework per OLE DB è incluso un oggetto <xref:System.Data.OleDb.OleDbCommand>, in quello per SQL Server un oggetto <xref:System.Data.SqlClient.SqlCommand>, in quello per ODBC un oggetto <xref:System.Data.Odbc.OdbcCommand> e in quello per Oracle un oggetto <xref:System.Data.OracleClient.OracleCommand>.  
  
## In questa sezione  
 [Esecuzione di un comando](../../../../docs/framework/data/adonet/executing-a-command.md)  
 Viene descritto l'oggetto `Command` di ADO.NET e viene illustrato come usarlo per eseguire query e comandi su un'origine dati.  
  
 [Configurazione dei parametri e tipi di dati dei parametri](../../../../docs/framework/data/adonet/configuring-parameters-and-parameter-data-types.md)  
 Viene descritto l'uso dei parametri di `Command`, inclusa la direzione, i tipi di dati e la sintassi.  
  
 [Generazione di comandi con CommandBuilder](../../../../docs/framework/data/adonet/generating-commands-with-commandbuilders.md)  
 Viene descritto come usare compilatori di comandi per generare automaticamente i comandi INSERT, UPDATE e DELETE per un `DataAdapter` in cui è presente il comando SELECT di una singola tabella.  
  
 [Recupero di un singolo valore da un database](../../../../docs/framework/data/adonet/obtaining-a-single-value-from-a-database.md)  
 Viene descritto come usare il metodo `ExecuteScalar` di un oggetto `Command` per restituire un singolo valore in una query sul database.  
  
 [Utilizzo di oggetti Command per la modifica dei dati](../../../../docs/framework/data/adonet/using-commands-to-modify-data.md)  
 Viene descritto come usare un provider di dati per eseguire stored procedure o istruzioni DDL \(Data Definition Language\).  
  
## Vedere anche  
 [DataAdapter e DataReader](../../../../docs/framework/data/adonet/dataadapters-and-datareaders.md)   
 [DataSet, DataTable e DataView](../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [Connessione a un'origine dati](../../../../docs/framework/data/adonet/connecting-to-a-data-source.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)