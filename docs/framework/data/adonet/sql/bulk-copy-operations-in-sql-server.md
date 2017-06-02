---
title: "Operazioni di copia di massa in SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 83a7a0d2-8018-4354-97b9-0b1d99f8342b
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Operazioni di copia di massa in SQL Server
In Microsoft SQL Server è disponibile un'utilità della riga di comando molto diffusa denominata **bcp** che consente di eseguire velocemente la copia di massa di file di grandi dimensioni in tabelle o visualizzazioni nei database SQL Server.  La classe <xref:System.Data.SqlClient.SqlBulkCopy> consente di scrivere soluzioni di codice gestito che offrono funzionalità simili.  Esistono altri metodi per caricare dati in una tabella SQL Server \(ad esempio con l'istruzione INSERT\) ma <xref:System.Data.SqlClient.SqlBulkCopy> offre prestazioni molto più vantaggiose.  
  
 La classe <xref:System.Data.SqlClient.SqlBulkCopy> consente di scrivere dati solo su tabelle SQL Server.  Tuttavia l'origine dati non si limita a SQL Server ed è possibile usare qualsiasi origine i cui dati possano essere caricati in un'istanza <xref:System.Data.DataTable> oppure letti con un'istanza <xref:System.Data.IDataReader>.  
  
 Con la classe <xref:System.Data.SqlClient.SqlBulkCopy> è possibile eseguire le seguenti operazioni:  
  
-   Copia di massa singola  
  
-   Più copie di massa  
  
-   Copia di massa all'interno di una transazione  
  
> [!NOTE]
>  Con .NET Framework versione 1.1 o precedenti \(in cui non è supportata la classe <xref:System.Data.SqlClient.SqlBulkCopy>\), è possibile eseguire l'istruzione **BULK INSERT** usando l'oggetto <xref:System.Data.SqlClient.SqlCommand>.  
  
## In questa sezione  
 [Installazione dell'esempio relativo alla copia di massa](../../../../../docs/framework/data/adonet/sql/bulk-copy-example-setup.md)  
 Vengono descritte le tabelle usate negli esempi di copia di massa e vengono forniti gli script SQL per la creazione di tabelle nel database AdventureWorks.  
  
 [Esecuzione di singole operazioni di copia di massa](../../../../../docs/framework/data/adonet/sql/single-bulk-copy-operations.md)  
 Viene descritto come eseguire una copia di massa singola di dati in un'istanza di SQL Server usando la classe <xref:System.Data.SqlClient.SqlBulkCopy> e come eseguire la copia di massa con istruzioni Transact\-SQL e con la classe <xref:System.Data.SqlClient.SqlCommand>.  
  
 [Esecuzione di più operazioni di copia di massa](../../../../../docs/framework/data/adonet/sql/multiple-bulk-copy-operations.md)  
 Viene descritto come eseguire più copie di massa di dati in un'istanza di SQL Server usando la classe <xref:System.Data.SqlClient.SqlBulkCopy>.  
  
 [Transazioni e operazioni di copia di massa](../../../../../docs/framework/data/adonet/sql/transaction-and-bulk-copy-operations.md)  
 Viene descritto come eseguire una copia di massa all'interno di una transazione e come eseguire il commit e il rollback della transazione.  
  
## Vedere anche  
 [SQL Server e ADO.NET](../../../../../docs/framework/data/adonet/sql/index.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)