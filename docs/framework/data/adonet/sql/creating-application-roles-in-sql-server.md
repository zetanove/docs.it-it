---
title: "Creazione di ruoli applicazione in SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 27442435-dfb2-4062-8c59-e2960833a638
caps.latest.revision: 9
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 9
---
# Creazione di ruoli applicazione in SQL Server
I ruoli applicazione consentono di assegnare autorizzazioni a un'applicazione anziché a un ruolo o a un utente del database.  Gli utenti possono connettersi al database, attivare il ruolo applicazione e assumere le autorizzazioni concesse all'applicazione.  Le autorizzazioni concesse al ruolo applicazione sono effettive per la durata della connessione.  
  
> [!IMPORTANT]
>  I ruoli applicazione vengono attivati quando un'applicazione client fornisce un nome e una password di ruolo applicazione nella stringa di connessione.  Presentano una vulnerabilità di sicurezza nelle applicazioni a 2 livelli perché la password deve essere archiviata nel computer client.  Nelle applicazioni a 3 livelli è possibile archiviare la password in modo che non sia accessibile agli utenti dell'applicazione.  
  
## Funzionalità dei ruoli applicazione  
 Le funzionalità dei ruoli applicazione includono:  
  
-   A differenza dei ruoli del database, i ruoli applicazione non contengono membri.  
  
-   I ruoli applicazione vengono attivati quando un'applicazione fornisce il nome e una password del ruolo applicazione alla stored procedure di sistema `sp_setapprole`.  
  
-   La password deve essere archiviata nel computer client e specificata in fase di esecuzione. I ruoli applicazione non possono essere attivati dall'interno di SQL Server.  
  
-   La password non è crittografata.  La password con parametri viene archiviata come hash unidirezionale.  
  
-   Una volta attivate, le autorizzazioni acquisite tramite il ruolo applicazione rimangono effettive per la durata della connessione.  
  
-   Il ruolo applicazione eredita le autorizzazioni concesse al ruolo `public`.  
  
-   Se un membro del ruolo predefinito del server `sysadmin` attiva un ruolo applicazione, il contesto di sicurezza diventa quello del ruolo applicazione per la durata della connessione.  
  
-   Se si crea un account `guest` in un database che include un ruolo applicazione, non è necessario creare un account utente di database per il ruolo applicazione o per uno degli account di accesso che lo richiamano.  I ruoli applicazione possono accedere direttamente a un altro database solo se in quest'ultimo esiste un account `guest`.  
  
-   Le funzioni predefinite che restituiscono nomi di account di accesso, ad esempio SYSTEM\_USER, restituiscono il nome dell'account di accesso che ha richiamato il ruolo applicazione.  Le funzioni predefinite che restituiscono nomi utente del database restituiscono il nome del ruolo applicazione.  
  
### Principio dei privilegi minimi  
 Ai ruoli applicazione è necessario concedere solo le autorizzazioni necessarie in caso la password sia compromessa.  Le autorizzazioni al ruolo `public` devono essere revocate in qualsiasi database che usa un ruolo applicazione.  Disabilitare l'account utente `guest` in ogni database a cui non si desidera che i chiamanti del ruolo applicazione abbiano accesso.  
  
### Miglioramenti dei ruoli applicazione  
 Il contesto di esecuzione può essere restituito al chiamante originale dopo l'attivazione di un ruolo applicazione, eliminando la necessità di disabilitare il pool di connessioni.  La procedura `sp_setapprole` include una nuova opzione che crea un cookie, contenente informazioni di contesto sul chiamante.  È possibile ripristinare la sessione chiamando la procedura `sp_unsetapprole`, passando il cookie.  
  
## Alternative ai ruoli applicazione  
 I ruoli applicazione dipendono dalla sicurezza di una password, che presenta una potenziale vulnerabilità per la sicurezza.  Le password possono essere esposte se vengono incorporate nel codice dell'applicazione o salvate su disco.  
  
 Può essere opportuno considerare le seguenti alternative.  
  
-   Usare il passaggio di contesto con l'istruzione EXECUTE AS e le relative clausole NO REVERT e WITH COOKIE.  È possibile creare un account utente in un database non mappato a un account di accesso.  Assegnare quindi le autorizzazioni a questo account.  L'uzo di EXECUTE AS con un utente senza account di accesso è un sistema più sicuro, perché si basa su autorizzazioni e non su password.  Per altre informazioni, vedere [Personalizzazione delle autorizzazioni mediante la rappresentazione in SQL Server](../../../../../docs/framework/data/adonet/sql/customizing-permissions-with-impersonation-in-sql-server.md).  
  
-   Firmare le stored procedure con certificati, concedendo solo l'autorizzazione per eseguirle.  Per altre informazioni, vedere [Firma di stored procedure in SQL Server](../../../../../docs/framework/data/adonet/sql/signing-stored-procedures-in-sql-server.md).  
  
## Risorse esterne  
 Per altre informazioni, vedere le risorse seguenti.  
  
|Risorsa|Descrizione|  
|-------------|-----------------|  
|[Ruoli applicazione](http://msdn.microsoft.com/library/ms190998.aspx) nella documentazione online di SQL Server|Viene descritto come creare e usare i ruoli applicazione in SQL Server 2008.|  
  
## Vedere anche  
 [Protezione di applicazioni ADO.NET](../../../../../docs/framework/data/adonet/securing-ado-net-applications.md)   
 [Panoramica della sicurezza di SQL Server](../../../../../docs/framework/data/adonet/sql/overview-of-sql-server-security.md)   
 [Scenari di sicurezza delle applicazioni in SQL Server](../../../../../docs/framework/data/adonet/sql/application-security-scenarios-in-sql-server.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)