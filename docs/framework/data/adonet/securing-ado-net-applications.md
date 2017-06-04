---
title: "Protezione di applicazioni ADO.NET | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 005a1d43-6ee5-471e-ad98-1d30a44d49d5
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Protezione di applicazioni ADO.NET
Per scrivere un'applicazione ADO.NET protetta, non è sufficiente evitare i problemi più comuni di codifica, ad esempio la mancata convalida dell'input dell'utente.  Un'applicazione che consente di accedere ai dati può presentare molti punti di errore, che possono essere sfruttati da utenti non autorizzati per recuperare, modificare o distruggere dati sensibili.  È pertanto importante considerare tutti gli aspetti della sicurezza, a partire dal processo di classificazione dei rischi durante la fase di progettazione dell'applicazione, fino all'eventuale distribuzione e alla manutenzione costante.  
  
 Con .NET Framework vengono forniti numerosi servizi, classi e strumenti utili per la protezione e l'amministrazione di applicazioni di database.  Common Language Runtime \(CLR\) fornisce un ambiente indipendente dai tipi in cui eseguire il codice, con una Sicurezza dall'accesso di codice \(CAS, Code Access Security\) per limitare ulteriormente le autorizzazioni del codice gestito.  Attenendosi alle tecniche per la generazione di codice di accesso ai dati protetto, è possibile limitare i danni inflitti da un potenziale utente non autorizzato.  
  
 Il codice protetto non difende dai problemi di sicurezza che si possono verificare quando si usano risorse non gestite quali i database.  La maggior parte dei database di server, ad esempio SQL Server, dispone di sistemi di sicurezza interni, che aumentano la protezione se correttamente implementati.  Tuttavia, anche un'origine dati con un sistema di sicurezza efficace può subire danni da un attacco se non è configurata in modo appropriato.  
  
## In questa sezione  
 [Cenni preliminari sulla sicurezza](../../../../docs/framework/data/adonet/security-overview.md)  
 Vengono forniti consigli per la progettazione di applicazioni ADO.NET protette.  
  
 [Accesso protetto ai dati](../../../../docs/framework/data/adonet/secure-data-access.md)  
 Viene descritto come usare i dati di un'origine dati protetta.  
  
 [Applicazioni client protette](../../../../docs/framework/data/adonet/secure-client-applications.md)  
 Vengono riportate alcune considerazioni sulla sicurezza per le applicazioni client.  
  
 [Sicurezza dall'accesso di codice e ADO.NET](../../../../docs/framework/data/adonet/code-access-security.md)  
 Viene descritto come usare la sicurezza dall'accesso di codice per migliorare la protezione del codice ADO.NET.  Viene inoltre illustrato come operare in un contesto di attendibilità parziale.  
  
 [Privacy e sicurezza dei dati](../../../../docs/framework/data/adonet/privacy-and-data-security.md)  
 Vengono descritte le opzioni di crittografia disponibili per le applicazioni ADO.NET.  
  
## Sezioni correlate  
 [Sicurezza di SQL Server](../../../../docs/framework/data/adonet/sql/sql-server-security.md)  
 Vengono descritte le funzionalità di sicurezza di SQL Server dal punto di vista di uno sviluppatore.  
  
 [Considerazioni sulla sicurezza](../../../../docs/framework/data/adonet/ef/security-considerations.md)  
 Viene descritta la sicurezza per le applicazioni Entity Framework.  
  
 [Security](../../../../docs/standard/security/index.md)  
 Contiene collegamenti ad argomenti in cui vengono descritti tutti gli aspetti della sicurezza in .NET Framework.  
  
 [Security Tools](http://msdn.microsoft.com/it-it/2a3eb98a-2de6-4fba-b41c-01a74d354c11)  
 Vengono fornite informazioni sugli strumenti di .NET Framework per la protezione e l'amministrazione dei criteri di sicurezza.  
  
 [Resources for Creating Secure Applications](http://msdn.microsoft.com/it-it/0ebf5f69-76f2-498a-a2df-83cf3443e132)  
 Vengono forniti collegamenti ad argomenti relativi alla creazione di applicazioni protette.  
  
 [Bibliografia sulla sicurezza](../Topic/Security%20Bibliography.md)  
 Vengono forniti collegamenti a risorse esterne disponibili online e in formato cartaceo.  
  
## Vedere anche  
 [ADO.NET](../../../../docs/framework/data/adonet/index.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)