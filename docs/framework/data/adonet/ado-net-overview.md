---
title: "Cenni preliminari su ADO.NET | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ee3bc1d8-11db-4be4-89eb-c708cf04117d
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Cenni preliminari su ADO.NET
ADO.NET fornisce uniformità di accesso sia per origini dati quali SQL Server e XML, sia per origini dati esposte tramite OLE DB e ODBC.  Le applicazioni consumer che supportano la condivisione dei dati sono in grado di usare ADO.NET per connettersi a tali origini dati e recuperare, gestire e aggiornare i dati contenuti.  
  
 ADO.NET consente di separare l'accesso ai dati dalla modifica dei dati in componenti discreti, utilizzabili separatamente o congiuntamente.  In ADO.NET sono inclusi i provider di dati .NET Framework per la connessione a un database, l'esecuzione di comandi e il recupero di risultati.  Tali risultati vengono elaborati direttamente, inseriti nell'oggetto <xref:System.Data.DataSet> di ADO.NET in modo da consentirne l'esposizione adeguata all'utente, combinati con dati provenienti da più origini o passati tra livelli.  È inoltre possibile usare l'oggetto `DataSet` indipendentemente da un provider di dati .NET Framework per gestire i dati locali dell'applicazione o derivati da XML.  
  
 Le classi di ADO.NET sono incluse in System.Data.dll e vengono integrate con le classi XML presenti in System.Xml.dll.  Per un esempio di codice che consente di connettersi a un database, recuperare dati da esso e quindi visualizzare tali dati un una finestra della console, vedere [Esempi di codice ADO.NET](../../../../docs/framework/data/adonet/ado-net-code-examples.md).  
  
 ADO.NET fornisce agli sviluppatori che scrivono codice gestito funzionalità simili a quelle offerte da ADO \(ActiveX Data Objects\) agli sviluppatori con COM \(Component Object Model\) nativo.  Per l'accesso ai dati nelle applicazioni .NET è consigliabile usare ADO.NET e non ADO.  
  
 ADO.NET fornisce il metodo più diretto per l'accesso ai dati in .NET Framework.  Per un'astrazione di livello superiore che consente alle applicazioni di usare un modello concettuale al posto del modello di archiviazione sottostante, vedere [ADO.NET Entity Framework](../../../../docs/framework/data/adonet/ef/index.md).  
  
 **Informativa sulla privacy**: negli assembly System.Data.dll, System.Data.Design.dll, System.Data.OracleClient.dll, System.Data.SqlXml.dll, System.Data.Linq.dll, System.Data.SqlServerCe.dll e System.Data.DataSetExtensions.dll non viene fatta distinzione tra dati privati e non privati di un utente.  Questi assembly non raccolgono, archiviano o trasportano i dati privati degli utenti,  tuttavia possono essere usati da applicazioni di terze parti per tali scopi.  
  
## In questa sezione  
 [Architettura di ADO.NET](../../../../docs/framework/data/adonet/ado-net-architecture.md)  
 Viene fornita una descrizione generale dell'architettura e dei componenti di ADO.NET.  
  
 [Linee guida e opzioni della tecnologia ADO.NET](../../../../docs/framework/data/adonet/ado-net-technology-options-and-guidelines.md)  
 Vengono descritti i prodotti e le tecnologie inclusi nella piattaforma EDM.  
  
 [LINQ e ADO.NET](../../../../docs/framework/data/adonet/linq-and-ado-net.md)  
 Viene descritta l'implementazione di Language\-Integrated Query \(LINQ\) in ADO.NET e vengono forniti collegamenti agli argomenti rilevanti.  
  
 [Provider di dati .NET Framework](../../../../docs/framework/data/adonet/data-providers.md)  
 Vengono fornite informazioni generali sulle caratteristiche del provider di dati .NET Framework e dei provider di dati .NET Framework inclusi in ADO.NET.  
  
 [DataSet ADO.NET](../../../../docs/framework/data/adonet/ado-net-datasets.md)  
 Vengono fornite informazioni generali relative all'architettura e ai componenti del `DataSet`.  
  
 [Esecuzione side\-by\-side in ADO.NET](../../../../docs/framework/data/adonet/side-by-side-execution.md)  
 Vengono descritte le differenze tra le diverse versioni di ADO.NET e le relative ripercussioni sull'esecuzione contemporanea di diverse versioni e la compatibilità tra applicazioni.  
  
 [Esempi di codice ADO.NET](../../../../docs/framework/data/adonet/ado-net-code-examples.md)  
 Vengono forniti esempi di codice in cui vengono recuperati dati usando i provider di dati di ADO.NET.  
  
## Sezioni correlate  
 [Novità di ADO.NET](../../../../docs/framework/data/adonet/whats-new.md)  
 Vengono descritte le nuove funzionalità di [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)].  
  
 [Protezione di applicazioni ADO.NET](../../../../docs/framework/data/adonet/securing-ado-net-applications.md)  
 Vengono descritte le tecniche che consentono di scrivere codice protetto quando si usa ADO.NET.  
  
 [Mapping dei tipi di dati in ADO.NET](../../../../docs/framework/data/adonet/data-type-mappings-in-ado-net.md)  
 Vengono descritti i mapping tra i tipi di dati .NET Framework e i provider di dati .NET Framework.  
  
 [Recupero e modifica di dati in ADO.NET](../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md)  
 Viene descritto come connettersi a un'origine dati, recuperare e modificare i dati,  inclusi `DataReaders` e `DataAdapters`.  
  
## Vedere anche  
 [ADO.NET](../../../../docs/framework/data/adonet/index.md)   
 [Accesso ai dati in Visual Studio](../Topic/Accessing%20data%20in%20Visual%20Studio.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)