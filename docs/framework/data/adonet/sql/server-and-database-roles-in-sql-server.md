---
title: "Ruoli del server e del database in SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5482dfdb-e498-4614-8652-b174829eed13
caps.latest.revision: 9
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 9
---
# Ruoli del server e del database in SQL Server
In tutte le versioni di SQL Server si usa la sicurezza basata sui ruoli, che consente di assegnare le autorizzazioni a un ruolo, ovvero un gruppo di utenti, anziché ai singoli utenti.  Ai ruoli predefiniti del server e del database è assegnato un set predefinito di autorizzazioni.  
  
## Ruoli predefiniti del server  
 I ruoli predefiniti del server hanno un set fisso di autorizzazioni e un ambito a livello di server.  Sono destinati a essere usati per l'amministrazione di SQL Server e non è possibile modificare le autorizzazioni ad essi assegnate.  È possibile assegnare account di accesso ai ruoli predefiniti del server senza avere un account utente in un database.  
  
> [!IMPORTANT]
>  Il ruolo predefinito del server `sysadmin` incorpora tutti gli altri ruoli e ha un ambito illimitato.  Non aggiungere entità a questo ruolo a meno che non siano considerate estremamente attendibili.  I membri del ruolo `sysadmin` dispongono di privilegi amministrativi irrevocabili su tutti i database e le risorse del server.  
  
 È necessario aggiungere in modo selettivo gli utenti ai ruoli predefiniti del server.  Ad esempio, il ruolo `bulkadmin` consente agli utenti di inserire il contenuto di qualsiasi file locale in una tabella, il che potrebbe compromettere l'integrità dei dati.  Per l'elenco completo dei ruoli predefiniti del server e delle autorizzazioni, vedere la documentazione online di [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)].  
  
## Ruoli predefiniti del database  
 I ruoli predefiniti del database includono un set di autorizzazioni predefinito progettato per semplificare la gestione di gruppi di autorizzazioni.  I membri del ruolo `db_owner` possono eseguire tutte le attività di configurazione e di manutenzione nel database.  
  
 Per altre informazioni sui ruoli predefiniti di SQL Server, vedere le risorse seguenti.  
  
|Risorsa|Descrizione|  
|-------------|-----------------|  
|[Ruoli a livello di server](http://msdn.microsoft.com/library/ms188659.aspx) e [Autorizzazioni dei ruoli predefiniti del server](http://msdn.microsoft.com/library/ms175892.aspx) nella documentazione online di [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)]|Vengono descritti i ruoli predefiniti del server e le autorizzazioni associate in [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)].|  
|[Ruoli a livello di database](http://msdn.microsoft.com/library/ms189121.aspx) e [Autorizzazioni dei ruoli predefiniti del database](http://msdn.microsoft.com/library/ms189612.aspx) nella documentazione online di [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)]|Vengono descritti i ruoli predefiniti del database e le autorizzazioni associate.|  
  
## Ruoli e utenti del database  
 Gli account di accesso devono essere mappati ad account utente di database per poter essere usati con gli oggetti di database.  Gli utenti del database possono quindi essere aggiunti ai ruoli del database, ereditando i set di autorizzazioni associati a tali ruoli.  È possibile concedere tutte le autorizzazioni.  
  
 È anche necessario prendere in considerazione il ruolo `public`, l'account utente `dbo` e l'account `guest` quando si progetta la sicurezza per l'applicazione.  
  
### Ruolo public  
 Il ruolo `public` è contenuto in ogni database, inclusi i database di sistema.  Non può essere eliminato e non è possibile aggiungere o rimuovere utenti.  Le autorizzazioni concesse al ruolo `public` sono ereditate da tutti gli altri utenti e ruoli, perché appartengono al ruolo `public` per impostazione predefinita.  Concedere al ruolo `public` solo le autorizzazioni che si desidera assegnare a tutti gli utenti.  
  
### Account utente dbo  
 L'utente `dbo`, o proprietario del database, è un account utente che dispone di autorizzazioni implicite per l'esecuzione di tutte le attività nel database.  I membri del ruolo predefinito del server `sysadmin` vengono automaticamente mappati a `dbo`.  
  
> [!NOTE]
>  A par`dbo` è anche il nome di uno schema, come descritto in [Proprietà e distinzione tra utente e schema in SQL Server](../../../../../docs/framework/data/adonet/sql/ownership-and-user-schema-separation-in-sql-server.md).  
  
 L'account utente `dbo` viene spesso confuso con il ruolo predefinito del database `db_owner`.  L'ambito di `db_owner` è un database, mentre quello di `sysadmin` corrisponde all'intero server.  L'appartenenza al ruolo `db_owner` non conferisce i privilegi dell'utente `dbo`.  
  
### Account utente guest  
 Dopo aver autenticato un utente e dopo avergli consentito l'accesso a un'istanza di SQL Server, è necessario rendere disponibile un account utente distinto in ogni database cui l'utente deve accedere.  Il requisito di un account utente in ogni database impedisce agli utenti di connettersi a un'istanza di SQL Server e di accedere a tutti i database di un server.  L'esistenza di un account utente `guest` nel database aggira questo requisito consentendo l'accesso a un database con un account di accesso senza un account utente di database.  
  
 L'account `guest` è un account incorporato in tutte le versioni di SQL Server.  Per impostazione predefinita, è disabilitato nei nuovi database.  Se viene abilitato, è possibile disabilitarlo revocando la relativa autorizzazione CONNECT tramite l'esecuzione dell'istruzione Transact\-SQL REVOKE CONNECT FROM GUEST.  
  
> [!IMPORTANT]
>  Evitare di usare l'account `guest`; tutti gli account di accesso senza autorizzazioni per il database ottengono le autorizzazioni concesse a questo account.  Se è necessario usarlo, concedere le autorizzazioni minime all'account `guest`.  
  
 Per altre informazioni su account di accesso, utenti e ruoli di SQL Server, vedere le risorse seguenti.  
  
|Risorsa|Descrizione|  
|-------------|-----------------|  
|[Identità e controllo di accesso](http://msdn.microsoft.com/library/bb510418.aspx) nella Documentazione online di SQL Server|Contiene collegamenti ad argomenti in cui vengono descritti entità, ruoli, credenziali, entità a protezione diretta e autorizzazioni.|  
|[Entità](http://msdn.microsoft.com/library/ms181127.aspx) nella documentazione online di [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)]|Contiene una descrizione delle entità e collegamenti ad argomenti in cui sono illustrati i ruoli del server e del database.|  
  
## Vedere anche  
 [Protezione di applicazioni ADO.NET](../../../../../docs/framework/data/adonet/securing-ado-net-applications.md)   
 [Scenari di sicurezza delle applicazioni in SQL Server](../../../../../docs/framework/data/adonet/sql/application-security-scenarios-in-sql-server.md)   
 [Autenticazione in SQL Server](../../../../../docs/framework/data/adonet/sql/authentication-in-sql-server.md)   
 [Proprietà e distinzione tra utente e schema in SQL Server](../../../../../docs/framework/data/adonet/sql/ownership-and-user-schema-separation-in-sql-server.md)   
 [Autorizzazioni in SQL Server](../../../../../docs/framework/data/adonet/sql/authorization-and-permissions-in-sql-server.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)