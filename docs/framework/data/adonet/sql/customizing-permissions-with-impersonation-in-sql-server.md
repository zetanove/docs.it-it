---
title: "Personalizzazione delle autorizzazioni mediante la rappresentazione in SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: dc733d09-1d6d-4af0-9c4b-8d24504860f1
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# Personalizzazione delle autorizzazioni mediante la rappresentazione in SQL Server
In molte applicazioni vengono usate le stored procedure per accedere ai dati, basandosi sul concatenamento delle proprietà per restringere l'accesso alle tabelle di base.  È possibile concedere autorizzazioni EXECUTE sulle stored procedure, revocando o negando le autorizzazioni sulle tabelle di base.  SQL Server non verifica le autorizzazioni del chiamante se il proprietario della stored procedure coincide con quello delle tabelle.  Il concatenamento delle proprietà non funziona se i proprietari degli oggetti sono diversi oppure se si usano istruzioni SQL dinamiche.  
  
 È possibile usare la clausola EXECUTE AS in una stored procedure quando il chiamante non dispone delle autorizzazioni sugli oggetti di database cui viene fatto riferimento.  Per effetto della clausola EXECUTE AS il contesto di esecuzione viene passato all'utente proxy.  Tutto il codice, nonché qualsiasi chiamata a stored procedure o trigger annidati, viene eseguito nel contesto di sicurezza dell'utente proxy.  Viene ripristinato il contesto di esecuzione del chiamante originale solo dopo l'esecuzione della stored procedure o quando viene eseguita un'istruzione REVERT.  
  
## Cambio del contesto con l'istruzione EXECUTE AS  
 L'istruzione EXECUTE AS Transact\-SQL consente di cambiare il contesto di esecuzione di un'istruzione mediante la rappresentazione di un altro account di accesso o utente del database.  Si tratta di una tecnica utile per testare query e stored procedure usando le credenziali di un altro utente.  
  
```  
EXECUTE AS LOGIN = 'loginName';  
EXECUTE AS USER = 'userName';  
```  
  
 È necessario disporre delle autorizzazioni IMPERSONATE per l'account di accesso o l'utente che si intende rappresentare.  Questa autorizzazione è implica per `sysadmin` su tutti i database e per i membri del ruolo `db_owner` sui database di cui sono proprietari.  
  
## Concessione delle autorizzazioni con la clausola EXECUTE AS  
 È possibile usare la clausola EXECUTE AS nell'intestazione della definizione di una stored procedure, un trigger o una funzione definita dall'utente, ad eccezione delle funzioni inline valutate a livello di tabella.  La stored procedure viene quindi eseguita nel contesto del nome utente o della parola chiave specificata nella clausola EXECUTE AS.  È possibile creare un utente proxy nel database di cui non è stato eseguito il mapping a un account di accesso, concedendo solo le autorizzazioni necessarie sugli oggetti cui la stored procedure ha accesso.  Solo l'utente proxy specificato nella clausola EXECUTE AS deve disporre delle autorizzazioni su tutti gli oggetti cui il modulo ha accesso.  
  
> [!NOTE]
>  Per alcune azioni, ad esempio TRUNCATE TABLE, non sono disponibili autorizzazioni da concedere.  Incorporando l'istruzione all'interno di una stored procedure e specificando un utente proxy che dispone delle autorizzazioni ALTER TABLE, è possibile estendere le autorizzazioni necessarie per troncare la tabella ai chiamanti che dispongono solo delle autorizzazioni EXECUTE per la stored procedure.  
  
 Il contesto specificato nella clausola EXECUTE AS è valido per la durata della stored procedura, incluse stored procedure e trigger annidati.  Il contesto ritorna al chiamante al termine dell'esecuzione o quando viene eseguita l'istruzione REVERT.  
  
 L'uso di una clausola EXECUTE AS in una stored procedure implica tre passaggi:  
  
1.  Creazione di un utente proxy nel database non mappato a un account di accesso.  Questo passaggio non è necessario ma risulta utile durante la gestione delle autorizzazioni.  
  
```  
CREATE USER proxyUser WITHOUT LOGIN  
```  
  
1.  Concessione delle autorizzazioni necessarie all'utente proxy.  
  
2.  Aggiunta della clausola EXECUTE AS alla stored procedure o alla funzione definita dall'utente.  
  
```  
CREATE PROCEDURE [procName] WITH EXECUTE AS 'proxyUser' AS ...  
```  
  
> [!NOTE]
>  È possibile che le applicazioni che richiedono il controllo vengano interrotte perché il contesto di sicurezza originale del chiamante non viene mantenuto.  Le funzioni predefinite che restituiscono l'identità dell'utente corrente, ad esempio SESSION\_USER, USER, o USER\_NAME, restituiscono l'utente associato alla clausola EXECUTE AS, non il chiamante originale.  
  
### Uso di EXECUTE AS con REVERT  
 È possibile usare l'istruzione REVERT Transact\-SQL per ripristinare il contesto di esecuzione originale.  
  
 Quando si usa la clausola facoltativa WITH NO REVERT COOKIE \= @variableName, il contesto di esecuzione torna al chiamante purché la variabile @variableName contiene il valore corretto.  Viene quindi ripristinato il contesto di esecuzione del chiamante negli ambienti in cui viene usato il pool di connessioni.  Poiché il valore di @variableName è noto solo al chiamante dell'istruzione EXECUTE AS, il chiamante è in grado di garantire che il contesto di esecuzione stabilito non venga modificato dall'utente finale che richiama l'applicazione.  Alla chiusura della connessione, il contesto viene restituito al pool.  Per altre informazioni sul pool di connessioni in ADO.NET, vedere [Pool di connessioni di SQL Server \(ADO.NET\)](../../../../../docs/framework/data/adonet/sql-server-connection-pooling.md).  
  
### Specifica del contesto di esecuzione  
 Oltre a specificare un utente, è inoltre possibile usare EXECUTE AS con le parole chiave seguenti.  
  
-   CALLER.  L'esecuzione come CALLER corrisponde all'impostazione predefinita. Se non vengono specificate altre opzioni, la stored procedure viene eseguita nel contesto di sicurezza del chiamante.  
  
-   OWNER.  Con questa parola chiave la stored procedure viene eseguita nel contesto del proprietario.  Se la stored procedure viene creata in uno schema di cui è proprietario `dbo` o il proprietario del database, verrà eseguita con autorizzazioni senza restrizioni.  
  
-   SELF.  Con questa parola chiave la stored procedure viene eseguita nel contesto di sicurezza del creatore.  Questa opzione equivale all'esecuzione come utente specificato, dove l'utente specificato è la persona che crea o modifica la stored procedure.  
  
## Risorse esterne  
 Per altre informazioni, vedere le risorse seguenti.  
  
|Risorsa|Descrizione|  
|-------------|-----------------|  
|[Cambio di contesto](http://msdn.microsoft.com/library/ms188268.aspx) nella documentazione online di SQL Server|Sono inclusi collegamenti ad argomenti in cui viene descritto l'uso della clausola EXECUTE AS.|  
|[Uso di EXECUTE AS per creare set di autorizzazioni personalizzate](http://msdn.microsoft.com/library/ms190384.aspx) e [Uso di EXECUTE AS nei moduli](http://msdn.microsoft.com/library/ms178106.aspx) nella documentazione online di SQL Server|Argomenti in cui viene descritto l'uso della clausola EXECUTE AS.|  
  
## Vedere anche  
 [Protezione di applicazioni ADO.NET](../../../../../docs/framework/data/adonet/securing-ado-net-applications.md)   
 [Panoramica della sicurezza di SQL Server](../../../../../docs/framework/data/adonet/sql/overview-of-sql-server-security.md)   
 [Scenari di sicurezza delle applicazioni in SQL Server](../../../../../docs/framework/data/adonet/sql/application-security-scenarios-in-sql-server.md)   
 [Gestione delle autorizzazioni con le stored procedure in SQL Server](../../../../../docs/framework/data/adonet/sql/managing-permissions-with-stored-procedures-in-sql-server.md)   
 [Scrittura di istruzioni SQL dinamiche protette in SQL Server](../../../../../docs/framework/data/adonet/sql/writing-secure-dynamic-sql-in-sql-server.md)   
 [Firma di stored procedure in SQL Server](../../../../../docs/framework/data/adonet/sql/signing-stored-procedures-in-sql-server.md)   
 [Modifica di dati con le stored procedure](../../../../../docs/framework/data/adonet/modifying-data-with-stored-procedures.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)