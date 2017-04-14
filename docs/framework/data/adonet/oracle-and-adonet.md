---
title: "Oracle e ADO.NET | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8ee8e389-53cf-45cf-80bd-1df63ef34f2e
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Oracle e ADO.NET
> [!NOTE]
>  I tipi in <xref:System.Data.OracleClient> sono deprecati.  I tipi restano supportati nella versione corrente di .NET Framework, ma saranno rimossi in una versione futura.  Microsoft consiglia di usare un provider Oracle di terze parti.  
  
 Contenuto della sezione vengono descritte le caratteristiche e i comportamenti specifici del provider di dati [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] per Oracle.  
  
 Il provider di dati [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] per Oracle fornisce l'accesso a un database Oracle mediante l'interfaccia OCI \(Oracle Call Interface\) del software client Oracle.  La funzionalità del provider di dati è simile a quella presente nei provider di dati [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] per [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)], OLE DB e ODBC.  
  
 Per usare il provider di dati [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] per Oracle, è necessario che l'applicazione faccia riferimento allo spazio dei nomi <xref:System.Data.OracleClient> come indicato di seguito:  
  
```vb  
Imports System.Data.OracleClient  
```  
  
```csharp  
using System.Data.OracleClient;  
```  
  
 Quando si compila il codice, inoltre, è necessario includere un riferimento alla DLL.  Ad esempio, se si compila un programma C\#, la riga di comando deve includere:  
  
```  
csc /r:System.Data.OracleClient.dll  
```  
  
## In questa sezione  
 [Requisiti di sistema](../../../../docs/framework/data/adonet/system-requirements-for-the-dotnet-data-provider-for-oracle.md)  
 Vengono descritti i requisiti e i problemi relativi all'utilizzo del provider di dati [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] per Oracle.  
  
 [BFILE Oracle](../../../../docs/framework/data/adonet/oracle-bfiles.md)  
 Viene descritta la classe <xref:System.Data.OracleClient.OracleBFile> usata per il tipo di dati BFILE Oracle.  
  
 [LOB Oracle](../../../../docs/framework/data/adonet/oracle-lobs.md)  
 Viene descritta la classe <xref:System.Data.OracleClient.OracleLob> usata per il tipo di dati LOB Oracle.  
  
 [REF CURSOR Oracle](../../../../docs/framework/data/adonet/oracle-ref-cursors.md)  
 Viene descritto il supporto del tipo di dati REF CURSOR Oracle.  
  
 [OracleTypes](../../../../docs/framework/data/adonet/oracletypes.md)  
 Vengono descritte le strutture utilizzabili con i tipi di dati Oracle, inclusi tipi <xref:System.Data.OracleClient.OracleNumber> e <xref:System.Data.OracleClient.OracleString>.  
  
 [Sequenze di Oracle](../../../../docs/framework/data/adonet/oracle-sequences.md)  
 Viene descritto il supporto per il recupero dei valori chiave di sequenze di Oracle generati dal server.  
  
 [Mapping dei tipi di dati Oracle](../../../../docs/framework/data/adonet/oracle-data-type-mappings.md)  
 Vengono presentati i tipi di dati Oracle e i relativi mapping alla classe <xref:System.Data.OracleClient.OracleDataReader>.  
  
 [Transazioni distribuite Oracle](../../../../docs/framework/data/adonet/oracle-distributed-transactions.md)  
 Viene descritto come l'oggetto <xref:System.Data.OracleClient.OracleConnection>, in presenza di una transazione attiva, esegue l'inserimento automatico nella transazione distribuita.  
  
## Sezioni correlate  
 [Protezione di applicazioni ADO.NET](../../../../docs/framework/data/adonet/securing-ado-net-applications.md)  
 Vengono descritte le tecniche che consentono di scrivere codice protetto quando si usa [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)].  
  
 [DataSet, DataTable e DataView](../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)  
 Viene descritto come creare e usare `DataSets`, `DataSets` tipizzati, `DataTables` e `DataViews`.  
  
 [Recupero e modifica di dati in ADO.NET](../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md)  
 Viene descritto come usare i dati in ADO.NET.  
  
 [SQL Server e ADO.NET](../../../../docs/framework/data/adonet/sql/index.md)  
 Viene descritto come usare le funzionalità e le caratteristiche specifiche di [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)].  
  
 [DbProviderFactory](../../../../docs/framework/data/adonet/dbproviderfactories.md)  
 Vengono descritte le classi generiche che consentono di scrivere codice indipendente dal provider in [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)].  
  
## Vedere anche  
 [ADO.NET](../../../../docs/framework/data/adonet/index.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)