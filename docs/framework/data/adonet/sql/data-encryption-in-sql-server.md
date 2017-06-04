---
title: "Crittografia dei dati in SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 83b992f7-b351-4678-b4b9-f4ffd58134cc
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# Crittografia dei dati in SQL Server
In SQL Server sono disponibili funzioni per di crittografia e decrittografia dei dati tramite certificato, chiave asimmetrica o chiave simmetrica.  Tutte queste funzionalità vengono gestite in un archivio di certificati interno.  Nell'archivio viene usata una gerarchia di crittografia per proteggere i certificati e le chiavi di un livello con il livello superiore nella gerarchia.  Quest'area di funzionalità di SQL Server è denominata archivio segreto.  
  
 La modalità più veloce supportata dalle funzioni di crittografia è la crittografia con chiave simmetrica.  Questa modalità è adatta per la gestione di grandi volumi di dati.  Le chiavi simmetriche possono essere crittografate tramite certificati, password o altre chiavi simmetriche.  
  
## Chiavi e algoritmi  
 In SQL Server sono supportati diversi algoritmi di crittografia con chiave simmetrica, tra cui DES, Triple DES, RC2, RC4, RC4 a 128 bit, DESX, AES a 128 bit, AES a 192 bit e AES a 256 bit.  Gli algoritmi sono implementati usando CryptoAPI di Windows.  
  
 All'interno dell'ambito di una connessione al database, SQL Server consente di mantenere più chiavi simmetriche aperte.  Una chiave aperta viene recuperata dall'archivio ed è disponibile per la decrittografia dei dati.  Quando un dato viene decrittografato, non è necessario specificare la chiave simmetrica da usare.  Ogni valore crittografato contiene l'identificatore della chiave \(GUID chiave\) usata per crittografarlo.  Il motore fa corrispondere il flusso di byte crittografati con una chiave simmetrica aperta, se la chiave corretta è stata decrittografata ed è aperta.  La chiave viene quindi usata per eseguire la decrittografia e restituire i dati.  Se non viene aperta la chiave corretta, viene restituito Null.  
  
 Per un esempio in cui viene illustrato come usare i dati crittografati in un database, vedere [Procedura: Crittografia di una colonna di dati](http://go.microsoft.com/fwlink/?LinkID=128559) nella Documentazione online di SQL Server.  
  
## Risorse esterne  
 Per altre informazioni sulla crittografia dei dati, vedere le risorse seguenti.  
  
|||  
|-|-|  
|[Crittografia di SQL Server](http://msdn.microsoft.com/library/bb510663.aspx) nella documentazione online di SQL Server|Viene fornita una panoramica della crittografia in SQL Server.  Sono inclusi collegamenti ad argomenti aggiuntivi e procedure.|  
|[Gerarchia della crittografia](http://msdn.microsoft.com/library/ms189586.aspx) e [Procedure relative alla crittografia](http://msdn.microsoft.com/library/aa337557.aspx) nella documentazione online di SQL Server|Viene fornita una panoramica della crittografia in SQL Server.  Sono inclusi collegamenti ad argomenti aggiuntivi e procedure.|  
  
## Vedere anche  
 [Protezione di applicazioni ADO.NET](../../../../../docs/framework/data/adonet/securing-ado-net-applications.md)   
 [Scenari di sicurezza delle applicazioni in SQL Server](../../../../../docs/framework/data/adonet/sql/application-security-scenarios-in-sql-server.md)   
 [Autenticazione in SQL Server](../../../../../docs/framework/data/adonet/sql/authentication-in-sql-server.md)   
 [Ruoli del server e del database in SQL Server](../../../../../docs/framework/data/adonet/sql/server-and-database-roles-in-sql-server.md)   
 [Proprietà e distinzione tra utente e schema in SQL Server](../../../../../docs/framework/data/adonet/sql/ownership-and-user-schema-separation-in-sql-server.md)   
 [Autorizzazioni in SQL Server](../../../../../docs/framework/data/adonet/sql/authorization-and-permissions-in-sql-server.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)