---
title: "Recupero di un singolo valore da un database | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b38526cd-a62a-48cb-822a-e91dfa68e02d
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Recupero di un singolo valore da un database
Può essere necessario restituire informazioni del database costituite semplicemente da un singolo valore anziché da una tabella o da un flusso di dati.  È possibile, ad esempio, restituire il risultato di una funzione di aggregazione quale COUNT\(\*\), SUM\(Price\) o AVG\(Quantity\).  L'oggetto **Command** consente di restituire singoli valori usando il metodo **ExecuteScalar**,  che restituisce come valore scalare il valore della prima colonna della prima riga del set di risultati.  
  
 Nell'esempio di codice seguente viene inserito un nuovo valore nel database usando un <xref:System.Data.SqlClient.SqlCommand>.  Per restituire il valore della colonna Identity per il record inserito, viene usato il metodo <xref:System.Data.SqlClient.SqlCommand.ExecuteScalar%2A>.  
  
 [!code-csharp[DataWorks SqlCommand.ExecuteScalar#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlCommand.ExecuteScalar/CS/source.cs#1)]
 [!code-vb[DataWorks SqlCommand.ExecuteScalar#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlCommand.ExecuteScalar/VB/source.vb#1)]  
  
## Vedere anche  
 [Comandi e parametri](../../../../docs/framework/data/adonet/commands-and-parameters.md)   
 [Esecuzione di un comando](../../../../docs/framework/data/adonet/executing-a-command.md)   
 [DbConnection, DbCommand e DbException](../../../../docs/framework/data/adonet/dbconnection-dbcommand-and-dbexception.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)