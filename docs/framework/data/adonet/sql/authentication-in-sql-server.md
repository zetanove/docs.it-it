---
title: "Autenticazione in SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 646ddbf5-dd4e-4285-8e4a-f565f666c5cc
caps.latest.revision: 9
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 9
---
# Autenticazione in SQL Server
In [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] sono supportate due modalità di autenticazione: la modalità dell'autenticazione di Windows e la modalità mista.  
  
-   L'autenticazione di Windows è l'impostazione predefinita e viene spesso definita sicurezza integrata perché questo modello di sicurezza di [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] è strettamente integrato con Windows.  Determinati account utente e gruppi di Windows vengono considerati attendibili per l'accesso a SQL Server.  Gli utenti di Windows che sono già stati autenticati non devono presentare credenziali aggiuntive.  
  
-   La modalità mista supporta l'autenticazione di Windows e quella di [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)].  Le coppie di nome utente e password vengono mantenute in [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]
>  Se possibile, si consiglia di usare l'autenticazione di Windows.  In questa modalità viene usata una serie di messaggi crittografati per autenticare gli utenti in [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)].  Quando vengono usati gli account di accesso di [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)], i nomi e le password di [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] vengono passati attraverso la rete, riducendone la sicurezza.  
  
 Con l'autenticazione di Windows, gli utenti sono già connessi a Windows e non devono eseguire separatamente l'accesso a [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)].  Nell'oggetto `SqlConnection.ConnectionString` seguente è specificata l'autenticazione di Windows senza la richiesta di immissione di nome utente o password.  
  
```  
"Server=MSSQL1;Database=AdventureWorks;Integrated Security=true;  
```  
  
> [!NOTE]
>  Gli account di accesso sono distinti dagli utenti del database.  È necessario eseguire il mapping degli account di accesso o gruppi di Windows agli utenti o ruoli del database in un'operazione separata.  È quindi possibile concedere le autorizzazioni agli utenti o ai ruoli per l'accesso agli oggetti di database.  
  
## Scenari di autenticazione  
 L'autenticazione di Windows risulta in genere la soluzione ideale nelle seguenti situazioni:  
  
-   È presente un controller di dominio.  
  
-   L'applicazione e il database si trovano nello stesso computer.  
  
-   Si usa un'istanza di [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] Express o LocalDB.  
  
 Gli account di accesso di SQL Server vengono in genere usati nelle seguenti situazioni:  
  
-   Si dispone di un gruppo di lavoro.  
  
-   Gli utenti si connettono da domini diversi, non attendibili.  
  
-   Si usano applicazioni Internet, ad esempio [!INCLUDE[vstecasp](../../../../../includes/vstecasp-md.md)].  
  
> [!NOTE]
>  Se si specifica l'autenticazione di Windows, gli account di accesso di [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] non vengono disabilitati.  Usare l'istruzione [!INCLUDE[tsql](../../../../../includes/tsql-md.md)] ALTER LOGIN DISABLE per disabilitare gli account di accesso di [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] con privilegi elevati.  
  
## Tipi di account di accesso  
 In [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] sono supportati tre tipi di account di accesso:  
  
-   Account utente di Windows locale o account di dominio attendibile.  [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] si affida a Windows per l'autenticazione degli account utente di Windows.  
  
-   Gruppo di Windows.  L'accesso concesso a un gruppo di Windows viene assegnato a tutti gli account di accesso degli utenti di Windows che sono membri di tale gruppo.  
  
-   Account di accesso di [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)].  In [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] sia il nome utente che un hash della password vengono archiviati nel database master, usando metodi di autenticazione interni per verificare i tentativi di accesso.  
  
> [!NOTE]
>  In [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] sono stati forniti gli account di accesso creati da certificati o chiavi asimmetriche, usati solo per la firma del codice,  che non possono essere usati per la connessione a [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)].  
  
## Autenticazione in modalità mista  
 Se è necessario usare l'autenticazione in modalità mista, occorre creare account di accesso di [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)], che vengono archiviati in SQL Server.  È quindi necessario specificare il nome utente e la password di [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] in fase di esecuzione.  
  
> [!IMPORTANT]
>  [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] viene installato con un account di accesso di [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] denominato `sa` \(abbreviazione di "system administrator"\).  Assegnare una password complessa all'account di accesso `sa` e non usare l'account di accesso `sa` nell'applicazione.  L'account di accesso `sa` viene mappato al ruolo predefinito del server `sysadmin`, che dispone di credenziali amministrative irrevocabili nell'intero server.  Non esistono limiti ai danni che potrebbero verificarsi se un utente non autorizzato ottiene accesso come amministratore di sistema.  Per impostazione predefinita, tutti i membri del gruppo `BUILTIN\Administrators` di Windows \(il gruppo di amministratori locali\) sono membri del ruolo `sysadmin`, ma possono essere rimossi da tale ruolo.  
  
 In [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] sono disponibili meccanismi dei criteri password di Windows per gli account di accesso di [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)], se eseguito in [!INCLUDE[winxpsvr](../../../../../includes/winxpsvr-md.md)] o versioni successive.  I criteri di complessità delle password sono progettati per fungere da deterrente agli attacchi a forza bruta aumentando il numero di password possibili.  [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] può applicare gli stessi criteri di complessità e scadenza usati in [!INCLUDE[winxpsvr](../../../../../includes/winxpsvr-md.md)] alle password usate all'interno di [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)].  
  
> [!IMPORTANT]
>  La concatenazione di stringhe di connessione dall'input dell'utente può lasciare il sistema vulnerabile a un attacco injection alle stringhe di connessione.  Usare <xref:System.Data.SqlClient.SqlConnectionStringBuilder> per creare stringhe di connessione sintatticamente valide in fase di esecuzione.  Per altre informazioni, vedere [Compilatori di stringhe di connessione](../../../../../docs/framework/data/adonet/connection-string-builders.md).  
  
## Risorse esterne  
 Per altre informazioni, vedere le risorse seguenti.  
  
|Risorsa|Descrizione|  
|-------------|-----------------|  
|[Entità](http://msdn.microsoft.com/library/bb543165.aspx) nella documentazione online di [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)]|Vengono descritti gli account di accesso e altre entità di sicurezza disponibili in [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)].|  
  
## Vedere anche  
 [Protezione di applicazioni ADO.NET](../../../../../docs/framework/data/adonet/securing-ado-net-applications.md)   
 [Scenari di sicurezza delle applicazioni in SQL Server](../../../../../docs/framework/data/adonet/sql/application-security-scenarios-in-sql-server.md)   
 [Connessione a un'origine dati](../../../../../docs/framework/data/adonet/connecting-to-a-data-source.md)   
 [Stringhe di connessione](../../../../../docs/framework/data/adonet/connection-strings.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)