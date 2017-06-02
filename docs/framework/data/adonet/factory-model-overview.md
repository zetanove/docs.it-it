---
title: "Panoramica del modello di factory | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b5dc81c4-7554-44b9-b513-769bd61e2e7b
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Panoramica del modello di factory
In ADO.NET 2.0 sono state introdotte nuove classi di base nello spazio dei nomi <xref:System.Data.Common>.  Le classi di base sono astratte, ovvero non è possibile creare un'istanza di tali classi in modo diretto.  Includono <xref:System.Data.Common.DbConnection>, <xref:System.Data.Common.DbCommand>e <xref:System.Data.Common.DbDataAdapter> e sono condivise tra i provider di dati .NET Framework, ad esempio <xref:System.Data.SqlClient> e <xref:System.Data.OleDb>.  L'aggiunta di classi di base consente di aggiungere più facilmente funzionalità ai provider di dati .NET Framework senza dover creare nuove interfacce.  
  
 In ADO.NET 2.0 sono state inoltre introdotte classi di base astratte che consentono agli sviluppatori di scrivere codice per l'accesso ai dati generico e non dipendente da un provider di dati specifico.  
  
## Modello di progettazione a livello di factory  
 Il modello di programmazione per la scrittura di codice indipendente dal provider è basato sul modello di progettazione a livello di factory, che usa una singola API per accedere ai database di più provider.  Il nome di questo modello è appropriato in quanto richiede l'uso di un oggetto specializzato soltanto per creare altri oggetti, non molto diversamente da una fabbrica reale.  Per una descrizione più dettagliata del modello di progettazione a livello di factory, vedere gli articoli relativi alla [scrittura di codice di accesso ai dati in ASP.NET 2.0 e ADO.NET 2.0](http://go.microsoft.com/fwlink/?LinkId=55915) e alla codifica generica con le factory e le classi di base di ADO.NET 2.0 [http:\/\/msdn.microsoft.com\/library\/default.asp?url\=\/library\/dnvs05\/html\/vsgenerics.asp](http://msdn.microsoft.com/library/default.asp?url=/library/dnvs05/html/vsgenerics.asp) su MSDN.  
  
 A partire da ADO.NET 2.0 la classe <xref:System.Data.Common.DbProviderFactories> fornisce metodi `static` \(o `Shared` in Visual Basic\) per la creazione di un'istanza di <xref:System.Data.Common.DbProviderFactory>.  L'istanza restituisce quindi un oggetto fortemente tipizzato corretto basato sulle informazioni fornite dal provider e dalla stringa di connessione in fase di esecuzione.  
  
## Vedere anche  
 [Recupero di un oggetto DbProviderFactory](../../../../docs/framework/data/adonet/obtaining-a-dbproviderfactory.md)   
 [DbConnection, DbCommand e DbException](../../../../docs/framework/data/adonet/dbconnection-dbcommand-and-dbexception.md)   
 [Modifica di dati con un DbDataAdapter](../../../../docs/framework/data/adonet/modifying-data-with-a-dbdataadapter.md)   
 [Provider di dati gestiti ADO.NET e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)