---
title: "Istanze utente di SQL Server Express | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 00c12376-cb26-4317-86ad-e6e9c089be57
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# Istanze utente di SQL Server Express
In Microsoft SQL Server Express Edition \(SQL Server Express\) è supportata la funzionalità istanze utente, disponibile solo quando si usa il provider di dati .NET Framework per SQL Server \(`SqlClient`\).  Un'istanza utente è un'istanza distinta del motore di database di SQL Server Express generata da un'istanza padre.  Le istanze utente consentono agli utenti non amministratori di collegarsi e connettersi ai database SQL Server Express dai propri computer locali.  Ogni istanza viene eseguita nel contesto di sicurezza del singolo utente, a livello di un'istanza per ogni utente.  
  
## Funzionalità dell'istanza utente  
 Le istanze utente risultano utili per gli utenti che eseguono Windows con un account utente con privilegi minimi \(LUA, Least\-Privilege User Account\), perché ogni utente dispone di privilegi di amministratore di sistema di SQL Server \(`sysadmin`\) sull'istanza eseguita nel proprio computer senza la necessità di disporre anche di privilegi di amministratore di Windows.  Il software eseguito con un'istanza utente con autorizzazioni limitate non può apportare modifiche a livello di sistema, perché l'istanza di SQL Server Express viene eseguita con l'account dell'utente non amministratore di Windows, non come servizio.  Ogni istanza utente è isolata dalla relativa istanza padre e da qualsiasi altra istanza utente in esecuzione nello stesso computer.  I database eseguiti in un'istanza utente vengono aperti solo in modalità utente singolo e non è possibile che più utenti si connettano ai database in esecuzione in un'istanza utente.  La replica e le query distribuite sono inoltre disabilitate per le istanze utente.  
  
 Per altre informazioni, vedere "Istanze utente" nella documentazione online di SQL Server.  
  
> [!NOTE]
>  Le istanze utente non sono necessarie per gli utenti che sono già amministratori del proprio computer o negli scenari che implicano più utenti di database.  
  
## Abilitazione delle istanze utente  
 Per generare le istanze utente, è necessario che sia in esecuzione un'istanza padre di SQL Server Express.  Le istanze utente vengono abilitate per impostazione predefinita durante l'installazione di SQL Server Express e possono essere abilitate o disabilitate in modo esplicito da un amministratore di sistema eseguendo la stored procedure di sistema **sp\_configure** sull'istanza padre.  
  
```  
-- Enable user instances.  
sp_configure 'user instances enabled','1'   
  
-- Disable user instances.  
sp_configure 'user instances enabled','0'  
```  
  
 Il protocollo di rete per le istanze utente deve essere Named Pipes locale.  Un'istanza utente non può essere avviata su un'istanza remota di SQL Server e gli account di accesso di SQL Server non sono supportati.  
  
## Connessione a un'istanza utente  
 Le parole chiave `User Instance`  e `AttachDBFilename` <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A> consentono la connessione di <xref:System.Data.SqlClient.SqlConnection> a un'istanza utente.  Le istanze utente sono supportate anche dalle proprietà <xref:System.Data.SqlClient.SqlConnectionStringBuilder> `UserInstance` e `AttachDBFilename`.  
  
 Si noti quanto segue sull'esempio di stringa di connessione illustrato di seguito:  
  
-   La parola chiave `Data Source` fa riferimento all'istanza padre di SQL Server Express che genera l'istanza utente.  L'istanza predefinita è .  \\sqlexpress.  
  
-   `Integrated Security` è impostato su `true`.  Per connettersi a un'istanza utente, è necessario usare l'autenticazione di Windows. Gli account di accesso di SQL Server non sono supportati.  
  
-   `User Instance` è impostata su `true`, che richiama un'istanza utente.  Il valore predefinito è `false`.  
  
-   La parola chiave per la stringa di connessione `AttachDbFileName` viene usata per collegare il file di database primario \(con estensione mdf\) che deve includere il nome del percorso completo.  `AttachDbFileName` corrisponde anche alle chiavi "extended properties" e "initial file name" all'interno della stringa di connessione <xref:System.Data.SqlClient.SqlConnection>.  
  
-   La stringa di sostituzione `|DataDirectory|` racchiusa tra barre verticali fa riferimento alla directory di dati dell'applicazione che apre la connessione e fornisce un percorso relativo che indica la posizione dei file di database e di log, con estensione mdf e ldf.  Se si desidera individuare altrove questi file, è necessario fornire il percorso completo.  
  
```  
Data Source=.\\SQLExpress;Integrated Security=true;  
User Instance=true;AttachDBFilename=|DataDirectory|\InstanceDB.mdf;  
Initial Catalog=InstanceDB;  
```  
  
> [!NOTE]
>  È anche possibile usare le proprietà <xref:System.Data.SqlClient.SqlConnectionStringBuilder><xref:System.Data.SqlClient.SqlConnectionStringBuilder.UserInstance%2A> e <xref:System.Data.SqlClient.SqlConnectionStringBuilder.AttachDBFilename%2A> per compilare una stringa di connessione in fase di esecuzione.  
  
### Utilizzo della stringa di sostituzione &#124;DataDirectory&#124;  
 `AttachDbFileName` è stata estesa in ADO.NET 2.0 con l'introduzione della stringa di sostituzione `|DataDirectory|` \(racchiusa tra barre verticali\).  `DataDirectory` viene usata insieme a `AttachDbFileName` per indicare un percorso relativo di un file di dati, consentendo agli sviluppatori di creare stringhe di connessione basate su un percorso relativo dell'origine dati senza che sia necessario specificare un percorso completo.   ``  
  
 La posizione fisica alla quale `DataDirectory` punta dipende dal tipo di applicazione.  In questo esempio il file Northwind.mdf da collegare è situato nella cartella \\app\_data dell'applicazione.  
  
```  
Data Source=.\\SQLExpress;Integrated Security=true;  
User Instance=true;  
AttachDBFilename=|DataDirectory|\app_data\Northwind.mdf;  
Initial Catalog=Northwind;  
```  
  
 Quando si usa `DataDirectory`, il percorso del file risultante non può trovarsi in una posizione della struttura della directory più alta rispetto alla directory a cui punta la stringa di sostituzione.  Se ad esempio il formato completamente espanso di `DataDirectory` è C:\\AppDirectory\\app\_data, la stringa di connessione di esempio illustrata in precedenza è valida perché si trova al di sotto di c:\\AppDirectory.  Se tuttavia si tenta di specificare `DataDirectory` come `|DataDirectory|\..\data`, verrà generato un errore perché \\data non è una sottodirectory di \\AppDirectory.  
  
 Se la stringa di connessione include una stringa di sostituzione in un formato errato, verrà generata un'eccezione <xref:System.ArgumentException>.  
  
> [!NOTE]
>  <xref:System.Data.SqlClient> risolve le stringhe di sostituzione in percorsi completi rispetto al file system del computer locale.  Pertanto, i nomi di percorso di server remoti, http e UNC non sono supportati.  Se il server non si trova nel computer locale, quando la connessione viene aperta verrà generata un'eccezione.  
  
 Quando viene aperto, l'oggetto <xref:System.Data.SqlClient.SqlConnection> viene reindirizzato dall'istanza di SQL Server Express predefinita a un'istanza avviata in fase di esecuzione che viene eseguita con l'account del chiamante.  
  
> [!NOTE]
>  Può essere necessario aumentare il valore di <xref:System.Data.SqlClient.SqlConnection.ConnectionTimeout%2A>, in quanto il caricamento delle istanze utente può richiedere più tempo delle istanze normali.  
  
 Con il frammento di codice seguente viene aperta una nuova connessione `SqlConnection`, la stringa di connessione viene visualizzata nella finestra della console e quindi la connessione viene chiusa all'uscita dal blocco di codice `using`.  
  
```vb  
Private Sub OpenSqlConnection()  
    ' Retrieve the connection string.  
    Dim connectionString As String = GetConnectionString()  
  
    Using connection As New SqlConnection(connectionString)  
        connection.Open()  
        Console.WriteLine("ConnectionString: {0}", _  
           connection.ConnectionString)  
    End Using  
End Sub  
```  
  
```csharp  
private static void OpenSqlConnection()  
{  
    // Retrieve the connection string.  
    string connectionString = GetConnectionString();  
  
    using (SqlConnection connection =   
        new SqlConnection(connectionString))  
    {  
        connection.Open();  
        Console.WriteLine("ConnectionString: {0}",   
             connection.ConnectionString);  
    }  
}  
```  
  
> [!NOTE]
>  Le istanze utente non sono supportate nel codice CLR \(Common Language Runtime\) in esecuzione in SQL Server.  Se viene eseguita una chiamata a `Open` su un oggetto <xref:System.Data.SqlClient.SqlConnection> nella cui stringa di connessione è presente `User Instance=true`, viene generata un'eccezione <xref:System.InvalidOperationException>.  
  
## Durata di una connessione a un'istanza utente  
 A differenza delle versioni di SQL Server che vengono eseguite come servizio, le istanze di SQL Server Express non devono necessariamente essere avviate e interrotte manualmente.  Ogni volta che un utente vi accede e si connette, l'istanza utente viene avviata se non è già in esecuzione.  Nei database dell'istanza utente è impostata l'opzione `AutoClose`, quindi il database viene automaticamente arrestato dopo un periodo di inattività.  Il processo sqlservr.exe che viene avviato rimane in esecuzione per un periodo di timeout limitato dopo la chiusura dell'ultima connessione all'istanza, quindi non deve essere riavviato se prima della scadenza del timeout viene aperta un'altra connessione.  L'istanza utente viene automaticamente arrestata se non vengono aperte nuove connessioni prima della scadenza del timeout.  Un amministratore di sistema dell'istanza padre può impostare la durata del periodo di timeout per un'istanza utente usando **sp\_configure** per modificare l'opzione **user instance timeout**.  Il valore predefinito è 60 minuti.  
  
> [!NOTE]
>  Se nella stringa di connessione si usa `Min Pool Size` con un valore maggiore di zero, il pool di connessioni manterrà sempre alcune connessioni aperte, quindi l'istanza utente non verrà automaticamente arrestata.  
  
## Funzionamento delle istanze utente  
 La prima volta che viene generata un'istanza utente per ogni utente, i database di sistema **master** e **msdb** vengono copiati dalla cartella Template Data in un percorso all'interno della directory di repository dei dati dell'applicazione locale dell'utente per l'uso esclusivo da parte dell'istanza utente.  Questo percorso è in genere `C:\Documents and Settings\<UserName>\Local Settings\Application Data\Microsoft\Microsoft SQL Server Data\SQLEXPRESS`.  Quando un'istanza utente viene avviata, in questa directory vengono scritti anche i file **tempdb**, di log e di traccia.  Per l'istanza viene generato un nome, che è assolutamente univoco per ogni utente.  
  
 Per impostazione predefinita, a tutti i membri del gruppo Windows Builtin\\\\Users sono concesse le autorizzazioni per connettersi all'istanza locale, nonché le autorizzazioni di lettura ed esecuzione sui binari di SQL Server.  Dopo la verifica delle credenziali dell'utente chiamante che ospita l'istanza utente, tale utente assume il ruolo di `sysadmin` sull'istanza.  Per le istanze utente è abilitata solo la memoria condivisa, il che significa che sono consentite soltanto operazioni nel computer locale.  
  
 Agli utenti è necessario concedere autorizzazioni di lettura e scrittura sui file mdf e ldf specificati nella stringa di connessione.  
  
> [!NOTE]
>  I file mdf e ldf rappresentano rispettivamente il file di database e il file di log.  Questi due file rappresentano un set corrispondente, quindi è necessario prestare attenzione durante le operazioni di backup e ripristino.  Il file di database contiene informazioni sulla versione esatta del file di log e non è possibile aprirlo se è abbinato al file di log errato.  
  
 Per evitare il danneggiamento dei dati, i database nell'istanza utente vengono aperti con accesso esclusivo.  Se due istanze utente diverse condividono lo stesso database nello stesso computer, l'utente nella prima istanza deve chiudere il database prima che possa essere aperto nella seconda istanza.  
  
## Scenari di istanza utente  
 Le istanze utente forniscono agli sviluppatori di applicazioni di database un archivio dati di SQL Server che non richiede la disponibilità di account amministrativi sui propri computer di sviluppo.  Le istanze utente sono basate sul modello Access\/Jet, in cui l'applicazione di database si connette a un file e l'utente ottiene automaticamente le autorizzazioni complete su tutti gli oggetti di database, senza richiedere l'intervento di un amministratore di sistema che le conceda.  Sono destinate alle situazioni in cui l'utente opera con un account con privilegi minimi e non dispone di privilegi amministrativi nel server o nel computer locale, anche se ha la necessità di creare applicazioni e oggetti di database.  Le istanze utente consentono di creare istanze in fase di esecuzione che vengono eseguite nel contesto di sicurezza dell'utente e non in quello di un servizio di sistema con più privilegi.  
  
> [!IMPORTANT]
>  Le istanze utente devono essere usate solo negli scenari in cui tutte le applicazioni che le usano sono completamente attendibili.  
  
 Gli scenari delle istanze utente includono:  
  
-   Qualsiasi applicazione in modalità utente singolo in cui non è necessario condividere dati.  
  
-   Distribuzione ClickOnce.  Se .NET Framework 2.0 \(o versione successiva\) e SQL Server Express sono già installati nel computer di destinazione, il pacchetto di installazione scaricato come risultato di un'azione ClickOnce può essere installato e usato da utenti non amministratori.  Si noti che un amministratore deve installare SQL Server Express se fa parte dell'installazione.  Per altre informazioni, vedere [ClickOnce Deployment for Windows Forms Applications](http://msdn.microsoft.com/it-it/34d8c770-48f2-460c-8d67-4ea5684511df).  
  
-   Hosting ASP.NET dedicato con autenticazione di Windows.  Una Intranet può contenere una singola istanza di SQL Server Express.  L'applicazione si connette usando l'account di Windows ASPNET, non tramite rappresentazione.  Le istanze utente non devono essere usate per scenari di hosting di terze parti o condivisi in cui tutte le applicazioni condividerebbero la stessa istanza utente e non rimarrebbero più isolate una dall'altra.  
  
## Vedere anche  
 [SQL Server e ADO.NET](../../../../../docs/framework/data/adonet/sql/index.md)   
 [Stringhe di connessione](../../../../../docs/framework/data/adonet/connection-strings.md)   
 [Connessione a un'origine dati](../../../../../docs/framework/data/adonet/connecting-to-a-data-source.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)