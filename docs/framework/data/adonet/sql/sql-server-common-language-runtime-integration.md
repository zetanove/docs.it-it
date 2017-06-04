---
title: "Integrazione CLR (Common Language Runtime) per SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c7a324c4-160d-44c2-b593-641af06eca61
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Integrazione CLR (Common Language Runtime) per SQL Server
In SQL Server 2005 è stata introdotta l'integrazione del componente CLR di .NET Framework per Microsoft Windows.  Questo significa che è possibile scrivere stored procedure, trigger, tipi definiti dall'utente, funzioni definite dall'utente, aggregati definiti dall'utente e funzioni con valori di tabella di flusso usando qualsiasi linguaggio di .NET Framework, inclusi Microsoft Visual Basic .NET e Microsoft Visual C\#.  Lo spazio dei nomi <xref:Microsoft.SqlServer.Server> contiene un set di nuove API \(Application Programming Interface\) che consente l'interazione del codice gestito con l'ambiente Microsoft SQL Server.  
  
 Questa sezione descrive le funzionalità e i comportamenti specifici dell'integrazione CLR di SQL Server, nonché le estensioni specifiche in\-process di SQL Server per ADO.NET.  
  
 In questa sezione vengono fornite solo le informazioni di base per iniziare a programmare con l'integrazione CLR di SQL Server. Tali informazioni non sono da considerarsi esaustive.  Per informazioni più dettagliate, vedere la versione della documentazione online di SQL Server corrispondente alla versione di SQL Server in uso.  
  
 **Documentazione online di SQL Server**  
  
1.  [Concetti relativi alla programmazione dell'integrazione con CLR \(Common Language Runtime\)](http://go.microsoft.com/fwlink/?LinkId=115240)  
  
## In questa sezione  
 [Introduzione all'integrazione CLR di SQL Server](../../../../../docs/framework/data/adonet/sql/introduction-to-sql-server-clr-integration.md)  
 Viene fornita un'introduzione all'integrazione CLR di SQL Server.  Vengono forniti collegamenti ad argomenti aggiuntivi.  
  
 [Funzioni CLR definite dall'utente](../../../../../docs/framework/data/adonet/sql/clr-user-defined-functions.md)  
 Viene descritto come implementare e usare i diversi tipi di funzioni CLR, ovvero le funzioni con valori di tabella, le funzioni scalari e le funzioni di aggregazione definite dall'utente.  
  
 [Tipi CLR definiti dall'utente](../../../../../docs/framework/data/adonet/sql/clr-user-defined-types.md)  
 Viene descritto come implementare e usare i tipi CLR definiti dall'utente.  Vengono forniti collegamenti ad argomenti aggiuntivi.  
  
 [Stored procedure CLR](../../../../../docs/framework/data/adonet/sql/clr-stored-procedures.md)  
 Viene descritto come implementare e usare le stored procedure CLR.  Vengono forniti collegamenti ad argomenti aggiuntivi.  
  
 [Trigger CLR](../../../../../docs/framework/data/adonet/sql/clr-triggers.md)  
 Viene descritto come implementare e usare i trigger CLR.  Vengono forniti collegamenti ad argomenti aggiuntivi.  
  
 [Connessione di contesto](../../../../../docs/framework/data/adonet/sql/the-context-connection.md)  
 Viene descritta la connessione di contesto.  
  
 [Comportamento specifico in\-process di SQL Server per ADO.NET](../../../../../docs/framework/data/adonet/sql/sql-server-in-process-specific-behavior-of-adonet.md)  
 Vengono descritte le estensioni specifiche in\-process di SQL Server per ADO.NET e la connessione di contesto.  Vengono forniti collegamenti ad argomenti aggiuntivi.  
  
## Vedere anche  
 [SQL Server e ADO.NET](../../../../../docs/framework/data/adonet/sql/index.md)   
 [Creating SQL Server 2005 Objects In Managed Code](http://msdn.microsoft.com/it-it/5358a825-e19b-49aa-8214-674ce5fed1da)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)