---
title: "Sintassi della stringa di connessione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0977aeee-04d1-4cce-bbed-750c77fce06e
caps.latest.revision: 11
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 11
---
# Sintassi della stringa di connessione
Ogni provider di dati .NET Framework include un oggetto `Connection` che eredita da <xref:System.Data.Common.DbConnection> oltre a una proprietà <xref:System.Data.Common.DbConnection.ConnectionString%2A> specifica del provider.  La sintassi della stringa di connessione specifica per ogni provider è documentata in questa proprietà `ConnectionString`.  Nella tabella seguente sono elencati i quattro provider di dati inclusi in .NET Framework.  
  
|Provider di dati .NET Framework|Descrizione|  
|-------------------------------------|-----------------|  
|<xref:System.Data.SqlClient>|Consente l'accesso ai dati per Microsoft SQL Server.  Per altre informazioni sulla sintassi della stringa di connessione, vedere <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A>.|  
|<xref:System.Data.OleDb>|Offre accesso ai dati per le origini dati esposte tramite OLE DB.  Per altre informazioni sulla sintassi della stringa di connessione, vedere <xref:System.Data.OleDb.OleDbConnection.ConnectionString%2A>.|  
|<xref:System.Data.Odbc>|Offre accesso ai dati per le origini dati esposte tramite ODBC.  Per altre informazioni sulla sintassi della stringa di connessione, vedere <xref:System.Data.Odbc.OdbcConnection.ConnectionString%2A>.|  
|<xref:System.Data.OracleClient>|Offre accesso ai dati per Oracle 8.1.7 o versione successiva.  Per altre informazioni sulla sintassi della stringa di connessione, vedere <xref:System.Data.OracleClient.OracleConnection.ConnectionString%2A>.|  
  
## Generatori di stringhe di connessione  
 In ADO.NET 2.0 sono stati introdotti i generatori di stringhe di connessione seguenti per i provider di dati .NET Framework.  
  
-   <xref:System.Data.SqlClient.SqlConnectionStringBuilder>  
  
-   <xref:System.Data.OleDb.OleDbConnectionStringBuilder>  
  
-   <xref:System.Data.Odbc.OdbcConnectionStringBuilder>  
  
-   <xref:System.Data.OracleClient.OracleConnectionStringBuilder>  
  
 I generatori di stringhe di connessione consentono di costruire stringhe di connessione sintatticamente valide in fase di esecuzione, pertanto non è necessario concatenare manualmente i valori delle stringhe di connessione nel codice.  Per altre informazioni, vedere [Compilatori di stringhe di connessione](../../../../docs/framework/data/adonet/connection-string-builders.md).  
  
## Autenticazione di Windows  
 Si consiglia di usare l'autenticazione di Windows \(definita anche *sicurezza integrata*\) per connettersi alle origini dati che la supportano.  La sintassi usata nella stringa di connessione varia a seconda del provider.  La tabella seguente illustra la sintassi dell'autenticazione di Windows usata con i provider di dati .NET Framework.  
  
|Provider|Sintassi|  
|--------------|--------------|  
|`SqlClient`|`Integrated Security=true;`<br /><br /> `-- or --`<br /><br /> `Integrated Security=SSPI;`|  
|`OleDb`|`Integrated Security=SSPI;`|  
|`Odbc`|`Trusted_Connection=yes;`|  
|`OracleClient`|`Integrated Security=yes;`|  
  
> [!NOTE]
>  `Integrated Security=true` genera un'eccezione se usata con il provider `OleDb`.  
  
## Stringhe di connessione SqlClient  
 La sintassi per una stringa di connessione <xref:System.Data.SqlClient.SqlConnection> è documentata nella proprietà <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A?displayProperty=fullName>.  È possibile usare la proprietà <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A> per ottenere o impostare una stringa di connessione per un database di SQL Server.  Per eseguire la connessione a una versione precedente di SQL Server, è necessario usare il provider di dati .NET Framework per OleDb \(<xref:System.Data.OleDb>\).  La maggior parte delle parole chiave delle stringhe di connessione sono inoltre mappate alle proprietà dell'oggetto <xref:System.Data.SqlClient.SqlConnectionStringBuilder>.  
  
 Con tutti i tipi di sintassi seguenti verrà usata l'autenticazione di Windows per stabilire la connessione al database **AdventureWorks** su un server locale.  
  
```  
"Persist Security Info=False;Integrated Security=true;  
    Initial Catalog=AdventureWorks;Server=MSSQL1"  
"Persist Security Info=False;Integrated Security=SSPI;  
    database=AdventureWorks;server=(local)"  
"Persist Security Info=False;Trusted_Connection=True;  
    database=AdventureWorks;server=(local)"  
```  
  
### Account di accesso di SQL Server  
 L'autenticazione di Windows è il sistema consigliato per le connessioni a SQL Server.  Se tuttavia è necessario usare l'autenticazione di SQL Server, usare la sintassi seguente per specificare un nome utente e una password.  In questo esempio per rappresentare un nome utente e una password validi vengono usati asterischi.  
  
```  
"Persist Security Info=False;User ID=*****;Password=*****;Initial Catalog=AdventureWorks;Server=MySqlServer"  
```  
  
> [!IMPORTANT]
>  L'impostazione predefinita per la parola chiave `Persist` `` `Security Info` è `false`.  Impostandola su `true` o `yes`, è possibile ottenere informazioni sensibili, compresi l'ID utente e la password, dalla connessione dopo che questa è stata aperta.  Mantenere `Persist` `` `Security Info` impostata su `false` per assicurarsi che le origini non attendibili non abbiano accesso a informazioni sensibili sulle stringhe di connessione.  
  
 Per connettersi a un'istanza denominata di SQL Server, usare la sintassi *nome server\\nome istanza*.  
  
```  
Data Source=MySqlServer\MSSQL1;"  
```  
  
 È anche possibile impostare la proprietà <xref:System.Data.SqlClient.SqlConnectionStringBuilder.DataSource%2A> di `SqlConnectionStringBuilder` sul nome dell'istanza quando si compila una stringa di connessione.  La proprietà <xref:System.Data.SqlClient.SqlConnection.DataSource%2A> di un oggetto <xref:System.Data.SqlClient.SqlConnection> è di sola lettura.  
  
> [!NOTE]
>  L'autenticazione di Windows ha la precedenza sugli account di accesso di SQL Server.  Se si specifica sia Integrated Security\=true sia un nome utente e una password, questi ultimi saranno ignorati e sarà usata l'autenticazione di Windows.  
  
### Modifiche alla versione del sistema di tipi  
 La parola chiave `Type System Version` in <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A?displayProperty=fullName> specifica la rappresentazione lato client dei tipi di [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)].  Per altre informazioni sulla parola chiave `Type System Version`, vedere <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A?displayProperty=fullName>.  
  
## Connessione e collegamento alle istanze utente di SQL Server Express  
 Le istanze utente sono una funzionalità di SQL Server Express.  consentono a un utente che usa un account di Windows locale con privilegi minimi di collegarsi ed eseguire un database SQL Server senza la necessità di privilegi amministrativi.  Un'istanza utente viene eseguita con le credenziali di Windows dell'utente, non come un servizio.  
  
 Per altre informazioni sull'uso delle istanze utente, vedere [Istanze utente di SQL Server Express](../../../../docs/framework/data/adonet/sql/sql-server-express-user-instances.md).  
  
## Uso di TrustServerCertificate  
 La parola chiave `TrustServerCertificate` è valida solo quando ci si connette a un'istanza di [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)] con un certificato valido.  Se `TrustServerCertificate` è impostata su `true`, il livello trasporto userà SSL per crittografare il canale e ignorerà l'analisi della catena di certificati per la convalida dell'attendibilità.  
  
```  
"TrustServerCertificate=true;"   
```  
  
> [!NOTE]
>  Se `TrustServerCertificate` è impostata su `true` e la crittografia è attivata, il livello di crittografia specificato nel server verrà usato anche se `Encrypt` è impostato su `false` nella stringa di connessione.  In caso contrario, la connessione non riuscirà.  
  
### Attivazione della crittografia  
 Per attivare la crittografia quando non è stato eseguito il provisioning di un certificato nel server, è necessario che le opzioni **Forza crittografia protocollo** e **Considera attendibile certificato server** siano impostate in Gestione configurazione SQL Server.  In questo caso, la crittografia userà un certificato server autofirmato senza convalida se nel server non è stato eseguito il provisioning di alcun certificato verificabile.  
  
 Le impostazioni delle applicazioni non possono ridurre il livello di sicurezza configurato in SQL Server, ma facoltativamente possono potenziarlo.  Un'applicazione può richiedere la crittografia impostando le parole chiave `TrustServerCertificate` e `Encrypt` su `true`, garantendo che la crittografia venga applicata anche quando non è stato eseguito il provisioning di un certificato server e l'opzione **Forza crittografia protocollo** non è stata configurata per il client.  Tuttavia, se `TrustServerCertificate` non è attivata nella configurazione client, è comunque necessario il provisioning di un certificato server.  
  
 La tabella seguente descrive tutti i casi.  
  
|Impostazione client Forza crittografia protocollo|Impostazione client Considera attendibile certificato server|Attributo\/stringa di connessione Encrypt\/Use Encryption for Data|Attributo\/stringa di connessione Trust Server Certificate|Risultato|  
|-------------------------------------------------------|------------------------------------------------------------------|------------------------------------------------------------------------|----------------------------------------------------------------|---------------|  
|No|N\/D|No \(impostazione predefinita\)|Ignorato|Nessuna crittografia.|  
|No|N\/D|Sì|No \(impostazione predefinita\)|La crittografia viene applicata solo se è disponibile un certificato server verificabile; in caso contrario, il tentativo di connessione non riesce.|  
|No|N\/D|Sì|Sì|La crittografia viene applicata solo se è disponibile un certificato server verificabile; in caso contrario, il tentativo di connessione non riesce.|  
|Sì|No|Ignorato|Ignorato|La crittografia viene applicata solo se è disponibile un certificato server verificabile; in caso contrario, il tentativo di connessione non riesce.|  
|Sì|Sì|No \(impostazione predefinita\)|Ignorato|La crittografia viene applicata solo se è disponibile un certificato server verificabile; in caso contrario, il tentativo di connessione non riesce.|  
|Sì|Sì|Sì|No \(impostazione predefinita\)|La crittografia viene applicata solo se è disponibile un certificato server verificabile; in caso contrario, il tentativo di connessione non riesce.|  
|Sì|Sì|Sì|Sì|La crittografia viene applicata solo se è disponibile un certificato server verificabile; in caso contrario, il tentativo di connessione non riesce.|  
  
 Per altre informazioni, vedere [Utilizzo della crittografia senza convalida](http://go.microsoft.com/fwlink/?LinkId=120500) nella documentazione online di SQL Server.  
  
## Stringhe di connessione OleDb  
 La proprietà <xref:System.Data.OleDb.OleDbConnection.ConnectionString%2A> di un oggetto <xref:System.Data.OleDb.OleDbConnection> consente di ottenere o impostare una stringa di connessione per un'origine dati OLE DB quale Microsoft Access.  È anche possibile creare una stringa di connessione `OleDb` in fase di esecuzione usando la classe <xref:System.Data.OleDb.OleDbConnectionStringBuilder>.  
  
### Sintassi della stringa di connessione OleDb  
 È necessario specificare il nome di un provider per una stringa di connessione <xref:System.Data.OleDb.OleDbConnection>.  La seguente stringa di connessione consente di connettersi a un database Microsoft Access usando il provider Jet.  Si noti che le parole chiave `UserID` e `Password` sono facoltative se il database non è protetto \(impostazione predefinita\).  
  
```  
Provider=Microsoft.Jet.OLEDB.4.0; Data Source=d:\Northwind.mdb;User ID=Admin;Password=;   
```  
  
 Se il database Jet è protetto tramite sicurezza a livello utente, è necessario specificare il percorso del file di informazioni sul gruppo di lavoro, con estensione mdw.  Il file di informazioni sul gruppo di lavoro viene usato per convalidare le credenziali fornite nella stringa di connessione.  
  
```  
Provider=Microsoft.Jet.OLEDB.4.0;Data Source=d:\Northwind.mdb;Jet OLEDB:System Database=d:\NorthwindSystem.mdw;User ID=*****;Password=*****;  
```  
  
> [!IMPORTANT]
>  È possibile fornire informazioni di connessione per un oggetto **OleDbConnection** in un file UDL \(Universal Data Link\). Si consiglia, tuttavia, di evitare questa procedura.  I file UDL non sono crittografati, pertanto espongono le informazioni nella stringa di connessione come testo non crittografato.  Poiché per l'applicazione si tratta di una risorsa esterna basata su file, un file UDL non può essere protetto tramite .NET Framework.  I file UDL non sono supportati per **SqlClient**.  
  
### Uso di DataDirectory per la connessione a Access\/Jet  
 `DataDirectory` non è riservata esclusivamente a `SqlClient`.  Può essere usata anche con i provider di dati .NET <xref:System.Data.OleDb> e <xref:System.Data.Odbc>.  Nell'esempio seguente la stringa <xref:System.Data.OleDb.OleDbConnection> indica la sintassi richiesta per connettersi al database Northwind.mdb situato nella cartella app\_data dell'applicazione.  In tale percorso è archiviato anche il database di sistema \(System.mdw\).  
  
```  
"Provider=Microsoft.Jet.OLEDB.4.0;  
Data Source=|DataDirectory|\Northwind.mdb;  
Jet OLEDB:System Database=|DataDirectory|\System.mdw;"  
```  
  
> [!IMPORTANT]
>  Se il database Acces\/Jet non è protetto, non è necessario specificare il percorso del database di sistema nella stringa di connessione.  La sicurezza è disattivata per impostazione predefinita, con tutti gli utenti che si connettono come utente Admin incorporato con una password vuota.  Anche quando la sicurezza a livello di utente è implementata correttamente, un database Jet rimane vulnerabile agli attacchi.  Pertanto, considerando la debolezza intrinseca dello schema di sicurezza basato su file dei database Access\/Jet, si sconsiglia di archiviare informazioni sensibili in tali database.  
  
### Connessione a Excel  
 Il provider Microsoft Jet viene usato per la connessione a una cartella di lavoro Excel.  Nella seguente stringa di connessione la parola chiave `Extended Properties` imposta le proprietà specifiche di Excel. "  HDR\=Yes;" indica che la prima riga contiene nomi di colonne e non dati, mentre "IMEX\=1;" indica al driver di leggere sempre come testo colonne di dati misti.  
  
```  
Provider=Microsoft.Jet.OLEDB.4.0;Data Source=D:\MyExcel.xls;Extended Properties=""Excel 8.0;HDR=Yes;IMEX=1""  
```  
  
 Si noti che le virgolette doppie richieste per `Extended Properties` devono essere racchiuse a loro volta tra virgolette doppie.  
  
### Sintassi della stringa di connessione di Data Shape Provider  
 Con il provider Microsoft Data Shape Provider, usare le parole chiave `Provider` e `Data Provider`.  Nell'esempio seguente viene usato il provider Shape per eseguire la connessione a un'istanza locale di SQL Server.  
  
```  
"Provider=MSDataShape;Data Provider=SQLOLEDB;Data Source=(local);Initial Catalog=pubs;Integrated Security=SSPI;"   
```  
  
## Stringhe di connessione Odbc  
 La proprietà <xref:System.Data.Odbc.OdbcConnection.ConnectionString%2A> di un oggetto <xref:System.Data.Odbc.OdbcConnection> consente di ottenere o impostare una stringa di connessione per un'origine dati OLE DB.  Le stringhe di connessione ODBC sono supportate anche da <xref:System.Data.Odbc.OdbcConnectionStringBuilder>.  
  
 Nella seguente stringa di connessione viene usato il driver Microsoft per file di testo.  
  
```  
Driver={Microsoft Text Driver (*.txt; *.csv)};DBQ=d:\bin  
```  
  
### Uso di DataDirectory per la connessione a Visual FoxPro  
 Nell'esempio di stringa di connessione <xref:System.Data.Odbc.OdbcConnection> seguente viene illustrato l'uso di `DataDirectory` per eseguire la connessione a un file di Microsoft Visual FoxPro.  
  
```  
"Driver={Microsoft Visual FoxPro Driver};  
SourceDB=|DataDirectory|\MyData.DBC;SourceType=DBC;"  
```  
  
## Stringhe di connessione Oracle  
 La proprietà <xref:System.Data.OracleClient.OracleConnection.ConnectionString%2A> di un oggetto <xref:System.Data.OracleClient.OracleConnection> consente di ottenere o impostare una stringa di connessione per un'origine dati OLE DB.  Le stringhe di connessione Oracle sono supportate anche da <xref:System.Data.OracleClient.OracleConnectionStringBuilder>.  
  
```  
Data Source=Oracle9i;User ID=*****;Password=*****;  
```  
  
 Per altre informazioni sulla sintassi delle stringhe di connessione ODBC, vedere <xref:System.Data.OracleClient.OracleConnection.ConnectionString%2A>.  
  
## Vedere anche  
 [Stringhe di connessione](../../../../docs/framework/data/adonet/connection-strings.md)   
 [Connessione a un'origine dati](../../../../docs/framework/data/adonet/connecting-to-a-data-source.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)