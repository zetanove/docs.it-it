---
title: "Accesso protetto ai dati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 473ebd69-21a3-4627-b95e-4e04d035c56f
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# Accesso protetto ai dati
Per scrivere codice ADO.NET protetto, è necessario comprendere i meccanismi di sicurezza disponibili nell'archivio dati o nel database sottostante.  Considerare inoltre le implicazioni di sicurezza di altre funzionalità o componenti che potrebbero essere inclusi nell'applicazione.  
  
## Autenticazione e autorizzazioni  
 Quando ci si connette a Microsoft SQL Server, è possibile usare la sicurezza di Windows, nota anche come sicurezza integrata, che si basa sull'identità dell'utente attivo corrente di Windows anziché sull'immissione di un ID utente e una password.  L'uso dell'autenticazione di Windows è consigliato perché le credenziali dell'utente non vengono esposte nella stringa di connessione.  Se non è possibile usare l'autenticazione di Windows per connettersi a SQL Server, creare stringhe di connessione in fase di esecuzione tramite <xref:System.Data.SqlClient.SqlConnectionStringBuilder>.  
  
 Le credenziali usate per l'autenticazione devono essere gestite in modo diverso a seconda del tipo di applicazione.  Ad esempio, in un'applicazione Windows Form all'utente può essere richiesto di fornire le informazioni di autenticazione oppure possono essere usate le credenziali di Windows dell'utente.  Tuttavia, in un'applicazione Web in genere l'accesso ai dati viene eseguito tramite le credenziali fornite dall'applicazione stessa invece che dall'utente.  
  
 Dopo l'autenticazione degli utenti, l'ambito delle loro azioni dipende dalle autorizzazioni che gli sono state concesse.  Attenersi sempre al principio dei privilegi minimi e concedere solo le autorizzazioni strettamente necessarie.  
  
 Per altre informazioni, vedere le risorse seguenti.  
  
|Risorsa|Descrizione|  
|-------------|-----------------|  
|[Protezione delle informazioni di connessione](../../../../docs/framework/data/adonet/protecting-connection-information.md)|Vengono descritte le procedure consigliate e le tecniche in materia di sicurezza per la protezione delle informazioni di connessione, ad esempio l'uso della configurazione protetta per crittografare le stringhe di connessione.|  
|[Recommendations for Data Access Strategies](http://msdn.microsoft.com/it-it/72411f32-d12a-4de8-b961-e54fca7faaf5)|Vengono forniti suggerimenti per l'accesso ai dati e l'esecuzione di operazioni di database.|  
|[Compilatori di stringhe di connessione](../../../../docs/framework/data/adonet/connection-string-builders.md)|Viene descritto come compilare stringhe di esecuzione dall'input dell'utente in fase di esecuzione.|  
|[Panoramica della sicurezza di SQL Server](../../../../docs/framework/data/adonet/sql/overview-of-sql-server-security.md)|Viene descritta l'architettura di sicurezza di SQL Server.|  
  
## Comandi con parametri e SQL injection  
 L'uso di comandi con parametri consente di salvaguardarsi da attacchi SQL injection, un cui un utente non autorizzato inserisce in un'istruzione SQL un comando che compromette la sicurezza del server.  I comandi con parametri consentono di evitare attacchi SQL injection garantendo che i valori ricevuti da un'origine esterna verranno passati come semplici valori e non come parte di un'istruzione Transact\-SQL.  Pertanto, i comandi Transact\-SQL inseriti in un valore non verranno eseguiti sull'origine dati.  Verranno invece valutati unicamente come un valore del parametro.  Oltre ai vantaggi in termini di sicurezza, i comandi con parametri rappresentano un metodo pratico per organizzare i valori passati con un'istruzione Transact\-SQL o a una stored procedure.  
  
 Per altre informazioni sull'uso dei comandi con parametri, vedere le risorse seguenti.  
  
|Risorsa|Descrizione|  
|-------------|-----------------|  
|[Parametri di DataAdapter](../../../../docs/framework/data/adonet/dataadapter-parameters.md)|Viene descritto come usare parametri con `DataAdapter`.|  
|[Modifica di dati con le stored procedure](../../../../docs/framework/data/adonet/modifying-data-with-stored-procedures.md)|Viene descritto come specificare i parametri e ottenere un valore restituito.|  
|[Gestione delle autorizzazioni con le stored procedure in SQL Server](../../../../docs/framework/data/adonet/sql/managing-permissions-with-stored-procedures-in-sql-server.md)|Viene descritto come usare le stored procedure di SQL Server per incapsulare l'accesso ai dati.|  
  
## Attacchi tramite script  
 Gli attacchi tramite script sono un altro tipo di intrusione in cui vengono inseriti caratteri dannosi in una pagina Web.  I caratteri inseriti non vengono convalidati nel browser e verranno elaborati come parte della pagina.  
  
 Per altre informazioni, vedere le risorse seguenti.  
  
|Risorsa|Descrizione|  
|-------------|-----------------|  
|[Script Exploits Overview](../Topic/Script%20Exploits%20Overview.md)|Viene descritto come salvaguardarsi da attacchi tramite script e istruzioni SQL.|  
  
## Attacchi di tipo probe  
 Gli utenti non autorizzati usano spesso informazioni provenienti da un'eccezione, quale un nome di server, database o tabella, per eseguire un tentativo di attacco al sistema.  Dal momento che le eccezioni possono presentare informazioni specifiche sull'applicazione o sull'origine dati, è possibile migliorarne la protezione esponendo al client solo le informazioni necessarie.  
  
 Per altre informazioni, vedere le risorse seguenti.  
  
|Risorsa|Descrizione|  
|-------------|-----------------|  
|[Nozioni fondamentali sulla gestione delle eccezioni](../../../../docs/standard/exceptions/exception-handling-fundamentals.md)|Vengono descritte le forme di base di gestione delle eccezioni strutturata di tipo try\/catch\/finally|  
|[Suggerimenti per le eccezioni](../../../../docs/standard/exceptions/best-practices-for-exceptions.md)|Vengono descritte le procedure consigliate per la gestione delle eccezioni.|  
  
## Protezione delle origini dati di Microsoft Access ed Excel  
 Se i requisiti di sicurezza sono minimi o non esistenti, Microsoft Access e Microsoft Excel possono fungere da archivio dati per un'applicazione ADO.NET.  Le funzionalità di sicurezza di queste applicazioni sono efficaci per la prevenzione, ma non devono essere considerate affidabili se non per scoraggiare le intrusioni di utenti non informati.  I file di dati fisici per Access ed Excel si trovano nel file system e devono essere accessibili a tutti gli utenti.  Questo li rende vulnerabili ad attacchi che possono comportare il furto o la perdita di dati, in quando i file possono essere facilmente copiati o modificati.  Se è necessaria una soluzione di sicurezza più affidabile, usare SQL Server o un altro database basato su server in cui i file di dati non sono leggibili dal file system.  
  
 Per altre informazioni sulla protezione dei dati di Access ed Excel, vedere le risorse seguenti.  
  
|Risorsa|Descrizione|  
|-------------|-----------------|  
|[Considerazioni e indicazioni relative alla sicurezza per Access 2007](http://go.microsoft.com/fwlink/?LinkId=98354)|Vengono descritte le tecniche di sicurezza disponibili per Access 2007, ad esempio crittografia dei file, amministrazione delle password, conversione dei database nei nuovi formati ACCDB e ACCDE e uso di altre opzioni di sicurezza.|  
|[Proteggere un database di Access e i relativi oggetti con la protezione a livello utente \(MDB\)](http://go.microsoft.com/fwlink/?LinkId=47697)|Per Access 2003,  vengono fornite le istruzioni per implementare la sicurezza dei dati a livello di utente.|  
|[Ruolo dei file di informazioni sul gruppo di lavoro nella sicurezza di Access](http://support.microsoft.com/kb/305542)|Vengono illustrati il ruolo e la relazione del file di informazioni sul gruppo di lavoro nella sicurezza di Access 2003.|  
|[Domande frequenti sulla sicurezza di Microsoft Access disponibili nell'area download](http://go.microsoft.com/fwlink/?LinkId=47698)|Versione scaricabile delle domande frequenti sulla sicurezza di Microsoft Access.|  
|[Risolvere i problemi relativi a sicurezza e protezione](http://go.microsoft.com/fwlink/?LinkId=47703)|Vengono fornite soluzioni a problemi comuni relativi alla sicurezza di Excel 2003.|  
  
## Servizi aziendali  
 In COM\+ è incluso un modello di sicurezza che si basa sugli account di Windows NT e sulla rappresentazione di processi e thread.  Lo spazio dei nomi <xref:System.EnterpriseServices> fornisce dei wrapper che consentono alle applicazioni .NET di integrare codice non gestito con i servizi di sicurezza COM\+ tramite la classe <xref:System.EnterpriseServices.ServicedComponent>.  
  
 Per altre informazioni, vedere la seguente risorsa.  
  
|Risorsa|Descrizione|  
|-------------|-----------------|  
|[COM\+ Role\-Based Security and the .NET Framework](http://msdn.microsoft.com/it-it/02ab22ef-e5e2-4d29-b33a-6e03d94c4981)|Viene illustrato come integrare codice gestito con i servizi di sicurezza COM\+.|  
  
## Interoperabilità con codice non gestito  
 .NET Framework rende disponibile l'interazione con codice non gestito, inclusi componenti COM, servizi COM\+, librerie dei tipi esterni e numerosi servizi del sistema operativo.  L'uso di codice non gestito implica l'allontanamento del perimetro di sicurezza disponibile per il codice gestito.  Sia il codice sia il codice da cui viene chiamato devono disporre dell'autorizzazione <xref:System.Security.Permissions.SecurityPermission> per codice non gestito con il flag <xref:System.Security.Permissions.SecurityPermissionFlag> specificato.  Il codice non gestito può introdurre vulnerabilità di sicurezza impreviste nell'applicazione.  Pertanto, è necessario evitare di interoperare con codice non gestito a meno che non sia assolutamente necessario.  
  
 Per altre informazioni, vedere le risorse seguenti.  
  
|Risorsa|Descrizione|  
|-------------|-----------------|  
|[Interoperating with Unmanaged Code](../../../../docs/framework/interop/index.md)|Contiene argomenti in cui viene descritto come esporre componenti COM a .NET Framework e componenti .NET Framework a COM.|  
|[Advanced COM Interoperability](http://msdn.microsoft.com/it-it/3ada36e5-2390-4d70-b490-6ad8de92f2fb)|Contiene componenti avanzati relativi, ad esempio, ad assembly di interoperabilità primari, threading e marshalling personalizzato.|  
  
## Vedere anche  
 [Protezione di applicazioni ADO.NET](../../../../docs/framework/data/adonet/securing-ado-net-applications.md)   
 [Sicurezza di SQL Server](../../../../docs/framework/data/adonet/sql/sql-server-security.md)   
 [Recommendations for Data Access Strategies](http://msdn.microsoft.com/it-it/72411f32-d12a-4de8-b961-e54fca7faaf5)   
 [Protezione delle informazioni di connessione](../../../../docs/framework/data/adonet/protecting-connection-information.md)   
 [Compilatori di stringhe di connessione](../../../../docs/framework/data/adonet/connection-string-builders.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)