---
title: "SqlClient per Entity Framework | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
ms.assetid: 9a5d6d39-d955-43a5-a5c2-931c239398f1
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# SqlClient per Entity Framework
Contenuto della sezione viene descritto il provider di dati .NET Framework per SQL Server \(SqlClient\), che consente a Entity Framework di funzionare su Microsoft SQL Server.  
  
## Attributo Provider dell'elemento Schema  
 `Provider` è un attributo dell'elemento `Schema` in SSDL \(Store Schema Definition Language\).  
  
 Per usare SqlClient, assegnare la stringa "System.Data.SqlClient" all'attributo `Provider` dell'elemento `Schema`.  
  
## Attributo ProviderManifestToken dell'elemento Schema  
 `ProviderManifestToken` è un attributo obbligatorio dell'elemento `Schema` in SSDL.  Questo token è usato per caricare il manifesto del provider per gli scenari non in linea.  Per altre informazioni sull'attributo `ProviderManifestToken`, vedere [Schema Element \(SSDL\)](http://msdn.microsoft.com/it-it/fec75ae4-7f16-4421-9265-9dac61509222).  
  
 SqlClient può essere usato come provider di dati per versioni diverse di [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)].  Queste versioni dispongono di funzionalità diverse.  Ad esempio, [!INCLUDE[ssVersion2000](../../../../../includes/ssversion2000-md.md)] non supporta i tipi `varchar(max)` e `nvarchar(max)` introdotti con [!INCLUDE[ssVersion2005](../../../../../includes/ssversion2005-md.md)].  
  
 SqlClient produce e accetta i token del manifesto del provider seguenti per versioni diverse di SQL Server.  
  
||||  
|-|-|-|  
|SQL Server 2000|SQL Server 2005|SQL Server 2008|  
|2000|2005|2008|  
  
> [!NOTE]
>  A partire da [!INCLUDE[vsprvs](../../../../../includes/vsprvs-md.md)] 2010, [ADO.NET Entity Data Model  Tools](http://msdn.microsoft.com/it-it/91076853-0881-421b-837a-f582f36be527) non supporta SQL Server 2000.  
  
## Nome dello spazio dei nomi del provider  
 Tutti i provider devono specificare uno spazio dei nomi.  Questa proprietà consente a Entity Framework di individuare quale prefisso viene usato dal provider per costrutti specifici, ad esempio tipi e funzioni.  Lo spazio dei nomi per i manifesti del provider SqlClient è `SqlServer`.  Per altre informazioni sugli spazi dei nomi, vedere [Namespaces](../../../../../docs/framework/data/adonet/ef/language-reference/namespaces-entity-sql.md).  
  
## Tipi  
 Il provider SqlClient per Entity Framework fornisce informazioni di mapping tra i tipi del modello concettuale e i tipi SQL Server.  Per altre informazioni, vedere [SqlClient per i tipi Entity Framework](../../../../../docs/framework/data/adonet/ef/sqlclient-for-ef-types.md).  
  
## Funzioni  
 Nel provider SqlClient per Entity Framework viene definito l'elenco di funzioni supportate dal provider.  Per un elenco delle funzioni supportate, vedere [Funzioni di SqlClient per Entity Framework](../../../../../docs/framework/data/adonet/ef/sqlclient-for-ef-functions.md).  
  
## Contenuto della sezione  
 [Funzioni di SqlClient per Entity Framework](../../../../../docs/framework/data/adonet/ef/sqlclient-for-ef-functions.md)  
  
 [SqlClient per i tipi Entity Framework](../../../../../docs/framework/data/adonet/ef/sqlclient-for-ef-types.md)  
  
 [Problemi noti in SqlClient per Entity Framework](../../../../../docs/framework/data/adonet/ef/known-issues-in-sqlclient-for-entity-framework.md)  
  
## Vedere anche  
 [Linguaggio Entity SQL](../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-language.md)   
 [Riferimenti per il linguaggio](../../../../../docs/framework/data/adonet/ef/language-reference/index.md)   
 [Known Issues in SqlClient Provider for Entity Framework](../../../../../docs/framework/data/adonet/ef/sqlclient-for-the-entity-framework.md)