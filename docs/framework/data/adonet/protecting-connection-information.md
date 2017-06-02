---
title: "Protezione delle informazioni di connessione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1471f580-bcd4-4046-bdaf-d2541ecda2f4
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Protezione delle informazioni di connessione
La protezione dell'accesso all'origine dati è uno dei principali obiettivi da raggiungere quando si imposta la sicurezza di un'applicazione.  Una stringa di connessione presenta una potenziale vulnerabilità se non è protetta.  Se le informazioni di connessione vengono archiviate in testo normale o mantenute nella memoria, si rischia di compromettere l'intero sistema.  Le stringhe di connessione incorporate nel codice sorgente possono essere lette tramite [Ildasm.exe \(IL Disassembler\)](../../../../docs/framework/tools/ildasm-exe-il-disassembler.md) per visualizzare il linguaggio MISL \(Microsoft Intermediate Language Microsoft\) in un assembly compilato.  
  
 Le vulnerabilità di sicurezza che riguardano le stringhe di connessione possono presentarsi in base al tipo di autenticazione usato, alla modalità con cui le stringhe di connessione vengono mantenute nella memoria e su disco e alle tecniche usate per crearle in fase di esecuzione.  
  
## Usa autenticazione di Windows  
 Per limitare l'accesso all'origine dati, è necessario proteggere le informazioni di connessione quali, ad esempio, identificatore utente, password e nome dell'origine dati.  Per evitare di esporre informazioni utente, si consiglia di usare l'autenticazione di Windows \(definita anche *sicurezza integrata*\) laddove possibile.  L'autenticazione di Windows viene specificata in una stringa di connessione usando le parole chiave `Integrated Security` o `Trusted_Connection`, eliminando la necessità di usare un ID utente e una password.  Tramite l'autenticazione di Windows, gli utenti vengono autenticati da Windows e l'accesso alle risorse di server e database viene determinato concedendo autorizzazioni a utenti e gruppi di Windows.  
  
 Nei casi in cui non sia possibile usare l'autenticazione di Windows, è necessario prestare una maggiore attenzione perché le credenziali utente sono esposte nella stringa di connessione.  Nelle applicazioni ASP.NET è possibile configurare un account di Windows come identità fissa usata per le connessioni a database e ad altre risorse di rete.  La rappresentazione viene abilitata nell'elemento identità nel file **web.config** e vengono specificati un nome utente e una password.  
  
```  
<identity impersonate="true"   
        userName="MyDomain\UserAccount"   
        password="*****" />  
```  
  
 L'account con identità fissa deve avere privilegi limitati che includono solo le autorizzazioni necessarie nel database.  È inoltre necessario crittografare il file di configurazione in modo da non esporre il nome utente e la password in testo non crittografato.  
  
## Non usare file UDL \(Universal Data Link\)  
 Evitare di archiviare le stringhe di connessione per <xref:System.Data.OleDb.OleDbConnection> in un file di collegamento dati universale \(UDL\).  I file UDL vengono archiviati in testo non crittografato e non possono essere crittografati.  Poiché per l'applicazione si tratta di una risorsa esterna basata su file, un file UDL non può essere protetto né crittografato tramite .NET Framework.  
  
## Evitare attacchi injection con i compilatori di stringhe di connessione  
 Un attacco injection alle stringhe di connessione può verificarsi quando si usa la concatenazione dinamica di stringhe per compilare stringhe di connessione basate sull'input dell'utente.  Se l'input dell'utente non viene convalidato e il testo o i caratteri dannosi non vengono convertiti in caratteri di escape, un utente non autorizzato potrebbe accedere a dati sensibili o ad altre risorse del server.  Per risolvere questo problema, in ADO.NET 2.0 sono state introdotte nuove classi di compilatori di stringhe di connessione per convalidare la sintassi delle stringhe e assicurarsi che non vengano inseriti parametri aggiuntivi.  Per altre informazioni, vedere [Compilatori di stringhe di connessione](../../../../docs/framework/data/adonet/connection-string-builders.md).  
  
## Usare Persist Security Info\=False  
 Il valore predefinito per `Persist Security Info` è false; si consiglia di usare questo valore in tutte le stringhe di connessione.  Se si imposta `Persist Security Info` su `true` o `yes`, è possibile che da una connessione aperta si ottengano informazioni sensibili, tra cui l'ID utente e la password.  Se si imposta `Persist Security Info` su `false` o `no`, le informazioni di sicurezza vengono eliminate dopo essere state usate per aprire la connessione. In questo modo un'origine non attendibile non ha accesso alle informazioni sensibili per la sicurezza.  
  
## Crittografare i file di configurazione  
 È anche possibile archiviare le stringhe di connessione in file di configurazione, eliminando la necessità di incorporarle nel codice dell'applicazione.  I file di configurazione sono file XML standard per i quali in .NET Framework è stato definito un set comune di elementi.  Le stringhe di connessione nei file di configurazione vengono in genere archiviate all'interno dell'elemento **\<connectionStrings\>** in **app.config** per le applicazioni Windows o nel file **web.config** per le applicazioni ASP.NET.  Per altre informazioni sull'archiviazione, il recupero e la crittografia di stringhe di connessione dai file di configurazione, vedere [Stringhe di connessione e file di configurazione](../../../../docs/framework/data/adonet/connection-strings-and-configuration-files.md).  
  
## Vedere anche  
 [Protezione di applicazioni ADO.NET](../../../../docs/framework/data/adonet/securing-ado-net-applications.md)   
 [Encrypting Configuration Information Using Protected Configuration](../Topic/Encrypting%20Configuration%20Information%20Using%20Protected%20Configuration.md)   
 [PAVE Security in Native and .NET Framework Code](http://msdn.microsoft.com/it-it/bd61be84-c143-409a-a75a-44253724f784)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)