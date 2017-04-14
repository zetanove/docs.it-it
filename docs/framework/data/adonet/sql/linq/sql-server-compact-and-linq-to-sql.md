---
title: "SQL Server Compact e LINQ to SQL | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 59022359-a5a2-4c42-9a6a-5c0259c3ad17
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# SQL Server Compact e LINQ to SQL
SQL Server Compact è il database predefinito installato con Visual Studio. Per ulteriori informazioni, vedere [PAVE OVER Using SQL Server Compact \(Visual Studio\)](http://msdn.microsoft.com/it-it/13320dd1-94e5-4077-bf76-8df253695ccc).  
  
 In questo argomento vengono delineate le principali differenze per quanto riguarda utilizzo, configurazione, set di funzionalità e ambito di supporto di [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  
  
## Caratteristiche di SQL Server Compact in relazione a LINQ to SQL  
 Per impostazione predefinita, SQL Server Compact è installato per tutte le edizioni di [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] ed è pertanto disponibile nel computer di sviluppo per essere usato con [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  La distribuzione di un'applicazione che utilizza SQL Server Compact e [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] differisce tuttavia dalla distribuzione di un'applicazione [!INCLUDE[ssNoVersion](../../../../../../includes/ssnoversion-md.md)].  SQL Server Compact non fa parte di .NET Framework e pertanto deve essere fornito con l'applicazione o scaricato separatamente dal sito Microsoft.  
  
 Tenere presente le seguenti caratteristiche:  
  
-   SQL Server Compact viene fornito come una DLL che può essere usata direttamente sui file di database \(con estensione sdf\).  
  
-   SQL Server Compact viene eseguito nello stesso processo dell'applicazione client.  L'efficienza della comunicazione con SQL Server Compact può quindi essere significativamente più elevata rispetto alla comunicazione con [!INCLUDE[ssNoVersion](../../../../../../includes/ssnoversion-md.md)].  D'altra parte SQL Server Compact richiede l'interoperabilità fra codice gestito e non gestito con i relativi costi associati.  
  
-   Le dimensioni della DLL di SQL Server Compact sono limitate.  Questa funzionalità riduce le dimensioni complessive dell'applicazione.  
  
-   Il runtime di [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] e lo strumento della riga di comando SQLMetal supportano SQL Server Compact.  
  
-   [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)] non supporta SQL Server Compact.  
  
## Set di funzionalità  
 Il set di funzionalità di SQL Server Compact è molto più semplice rispetto a quello di [!INCLUDE[ssNoVersion](../../../../../../includes/ssnoversion-md.md)] nei modi riportati di seguito che possono influire sulle applicazioni [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]:  
  
-   SQL Server Compact non supporta stored procedure o visualizzazioni.  
  
-   SQL Server Compact supporta solo un subset di tipi di dati e funzioni SQL.  
  
-   SQL Server Compact supporta solo un subset di costrutti SQL.  
  
-   SQL Server Compact fornisce solo un'utilità di ottimizzazione con funzionalità minime.  È possibile che si verifichi il timeout di alcune query.  
  
-   SQL Server Compact non supporta il trust parziale.  
  
## Vedere anche  
 [Riferimenti](../../../../../../docs/framework/data/adonet/sql/linq/reference.md)