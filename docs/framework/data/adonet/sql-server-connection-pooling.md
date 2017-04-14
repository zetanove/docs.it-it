---
title: "Pool di connessioni di SQL Server (ADO.NET) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7e51d44e-7c4e-4040-9332-f0190fe36f07
caps.latest.revision: 11
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 11
---
# Pool di connessioni di SQL Server (ADO.NET)
Generalmente, la connessione a un server database comporta passaggi che richiedono molto tempo.  È necessario, infatti, stabilire un canale fisico, ad esempio un socket oppure una named pipe. Deve verificarsi l'handshake iniziale con il server, deve essere analizzata l'informazione sulla stringa di connessione, la connessione deve essere autenticata dal server, sono necessarie verifiche per l'inserimento in un elenco nella transazione corrente e così via.  
  
 In pratica, la maggior parte delle applicazioni usa solo una o alcune configurazioni di connessione.  Per questo motivo, durante l'esecuzione dell'applicazione, verranno aperte e chiuse più volte connessioni identiche.  Per ridurre al minimo il costo dell'apertura delle connessioni, in [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] viene usata una tecnica di ottimizzazione denominata *pool di connessioni*.  
  
 Il pool di connessioni riduce il numero di volte in cui è necessario aprire nuove connessioni.  Il *pool* conserva la proprietà della connessione fisica.  Gestisce le connessioni mantenendo attivo un set di connessioni attive per ogni configurazione di connessione.  Quando un utente chiama `Open` su una connessione, il pool verifica la presenza di una connessione disponibile.  Se è disponibile una connessione, il pool la restituisce al chiamante invece di aprirne una nuova.  Quando l'applicazione chiama `Close`, il pool restituisce la connessione al set di connessioni attive invece di chiuderla realmente.  Una volta restituita al pool, la connessione può essere usata nuovamente nella successiva chiamata `Open`.  
  
 È possibile raggruppare in pool solo le connessioni che presentano la stessa configurazione.  In [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] vengono mantenuti diversi pool contemporaneamente, uno per ogni configurazione.  Le connessioni vengono divise in pool in base alla stringa di connessione e, quando si usa la sicurezza integrata, in base all'identità Windows.  Le connessioni vengono inserite nei pool anche in base a dove sono inserite in una transazione.  Quando si usa un <xref:System.Data.SqlClient.SqlConnection.ChangePassword%2A>, le istanze di <xref:System.Data.SqlClient.SqlCredential> influiscono sul pool di connessioni.  Diverse istanze di <xref:System.Data.SqlClient.SqlCredential> useranno pool di connessioni diversi, anche se l'ID utente e la password sono uguali.  
  
 Il pool di connessioni consente di migliorare notevolmente le prestazioni e di aumentare la scalabilità dell'applicazione.  Per impostazione predefinita, in [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] il pool di connessioni è attivato.  A meno che non venga disabilitato in modo esplicito, il pool ottimizza le connessioni che vengono aperte e chiuse nell'applicazione.  È possibile, inoltre, fornire più modificatori delle stringhe di connessione per controllare il comportamento del pool di connessioni.  Per altre informazioni, vedere "Controllo del pool di connessioni con le parole chiave delle stringhe di connessione" in questo argomento.  
  
> [!NOTE]
>  Quando il pool di connessioni è abilitato e se si verifica un errore di timeout o un altro errore di accesso, viene generata un'eccezione e i tentativi di connessione successivi avranno esito negativo per i prossimi cinque secondi, "il periodo di blocco".  Se l'applicazione tenta di connettersi durante il periodo di blocco, viene generata di nuovo la prima eccezione.  Gli errori successivi al termine del periodo di blocco causeranno nuovi periodi di blocco di lunghezza doppia rispetto al periodo di blocco precedente, fino a un massimo di un minuto.  
  
## Creazione e assegnazione di pool  
 Quando una connessione viene aperta per la prima volta, il pool di connessioni viene creato in base a un algoritmo esattamente corrispondente che associa il pool alla stringa di connessione.  Ogni pool di connessioni è associato a una stringa di connessione distinta.  Quando viene aperta una nuova connessione, se la stringa di connessione non corrisponde esattamente a un pool esistente, viene creato un nuovo pool.  Il pool di connessioni viene eseguito in base al processo, al dominio applicazione, alla stringa di connessione e, quando si usa la sicurezza integrata, in base all'identità Windows.  Le stringhe di connessione devono anche essere una corrispondenza esatta. Le parole chiave fornite in un ordine diverso per la stessa connessione verranno inserite in pool separatamente.  
  
 Nell'esempio C\# seguente vengono creati tre nuovi oggetti <xref:System.Data.SqlClient.SqlConnection>, ma per gestirli bastano solo due pool di connessioni.  Si noti che la differenza tra la prima e la seconda stringa di connessione consiste nel valore assegnato a `Initial Catalog`.  
  
```  
using (SqlConnection connection = new SqlConnection(  
  "Integrated Security=SSPI;Initial Catalog=Northwind"))  
    {  
        connection.Open();        
        // Pool A is created.  
    }  
  
using (SqlConnection connection = new SqlConnection(  
  "Integrated Security=SSPI;Initial Catalog=pubs"))  
    {  
        connection.Open();        
        // Pool B is created because the connection strings differ.  
    }  
  
using (SqlConnection connection = new SqlConnection(  
  "Integrated Security=SSPI;Initial Catalog=Northwind"))  
    {  
        connection.Open();        
        // The connection string matches pool A.  
    }  
```  
  
 Se `MinPoolSize` non è specificato nella stringa di connessione oppure è specificato come zero, le connessioni nel pool verranno chiuse dopo un periodo di inattività.  Tuttavia, se il valore `MinPoolSize` specificato è maggiore di zero, il pool di connessioni verrà eliminato solo dopo lo scaricamento di `AppDomain` e la fine del processo.  La manutenzione di pool inattivi o vuoti implica un overhead minimo del sistema.  
  
> [!NOTE]
>  Il pool viene cancellato automaticamente quando si verifica un errore irreversibile, quale un failover.  
  
## Aggiunta di connessioni  
 Per ogni stringa di connessione univoca viene creato un pool di connessioni.  Quando si crea un pool, vengono creati e aggiunti al pool più oggetti connessione in modo da soddisfare il requisito relativo alle dimensioni minime del pool.  Le connessioni sono aggiunte al pool a seconda della necessità, fino al raggiungimento delle dimensioni massime del pool \(l'impostazione predefinita è 100\).  Una volta chiuse o eliminate, le connessioni vengono rilasciate nel pool.  
  
 Quando viene richiesto un oggetto <xref:System.Data.SqlClient.SqlConnection>, esso viene ottenuto dal pool se è disponibile una connessione usabile.  Per essere utilizzabile, una connessione non deve essere in uso, deve disporre di un contesto di transazione corrispondente oppure non deve essere associata ad alcun contesto di transazione e, infine, deve disporre di un collegamento valido al server.  
  
 Il pool di connessioni soddisfa le richieste di connessione grazie alla riallocazione delle connessioni rilasciate nel pool.  Se le dimensioni massime del pool sono state raggiunte e non è disponibile alcuna connessione usabile, la richiesta viene accodata.  Il pool tenta quindi di recuperare le connessioni fino alla scadenza del timeout \(l'impostazione predefinita è 15 secondi\).  Se il pool non è in grado di soddisfare la richiesta prima che scada la connessione, viene generata un'eccezione.  
  
> [!CAUTION]
>  Al termine dell'uso, si consiglia di chiudere sempre la connessione in modo che possa essere restituita al pool.  È possibile eseguire questa operazione usando il metodo `Close` o `Dispose` dell'oggetto `Connection` oppure aprendo tutte le connessioni in un'istruzione `using` in C\# o in un'istruzione `Using` in [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)].  Le connessioni che non vengono chiuse in modo esplicito potrebbero non essere aggiunte o restituite al pool.  Per altre informazioni, vedere [Istruzione using](../Topic/using%20Statement%20\(C%23%20Reference\).md) o [How to: Dispose of a System Resource](../Topic/How%20to:%20Dispose%20of%20a%20System%20Resource%20\(Visual%20Basic\).md) per [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)].  
  
> [!NOTE]
>  Non chiamare `Close` o `Dispose` su un oggetto `Connection`, `DataReader` o su qualsiasi altro oggetto gestito nel metodo `Finalize` della classe.  Nei finalizzatori rilasciare solo le risorse non gestite che la classe controlla direttamente.  Se nella classe non sono presenti risorse non gestite, non includere un metodo `Finalize` nella relativa definizione della classe.  Per altre informazioni, vedere [Garbage Collection](../../../../docs/standard/garbage-collection/index.md).  
  
> [!NOTE]
>  Nel server non verranno generati eventi di accesso e di disconnessione quando una connessione viene recuperata dal o restituita al pool di connessioni,  in quanto la connessione non è effettivamente chiusa quando viene restituita al pool di connessioni.  Per altre informazioni, vedere [Classe di evento Audit Login](http://msdn.microsoft.com/library/ms190260.aspx) e [Classe di evento Audit Logout](http://msdn.microsoft.com/library/ms175827.aspx) nella documentazione online di [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)].  
  
## Rimozione di connessioni  
 Il pool di connessioni rimuove una connessione dopo un periodo di inattività pari a circa 4\-8 minuti oppure se rileva che la connessione al server è stata interrotta.  Notare che una connessione interrotta può essere rilevata solo dopo che è stato effettuato il tentativo di comunicare con il server.  Se viene individuata una connessione al server che non è più attiva, la connessione viene contrassegnata come non valida.  Le connessioni non valide vengono rimosse dal pool di connessioni solo quando vengono chiuse o recuperate.  
  
 Se esiste una connessione a un server non più disponibile, la connessione può essere recuperata dal pool anche se nessuna connessione è stata rilevata come interrotta e pertanto non è stata contrassegnata come non valida.  In caso contrario, l'overhead per la verifica della validità della connessione annullerebbe i vantaggi derivanti dal pool provocando un'ulteriore sequenza di andata e ritorno al server.  In questo caso, al primo tentativo di uso della connessione verrà rilevato che la connessione è stata interrotta e verrà generata un'eccezione.  
  
## Cancellazione del pool  
 In [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] 2.0 sono stati introdotti due nuovi metodi per cancellare il pool: <xref:System.Data.SqlClient.SqlConnection.ClearAllPools%2A> e <xref:System.Data.SqlClient.SqlConnection.ClearPool%2A>.  `ClearAllPools` cancella i pool di connessioni per un determinato provider, mentre `ClearPool` cancella il pool di connessioni associato a una connessione specifica.  Le connessioni in uso al momento della chiamata vengono contrassegnate in modo appropriato.  Una volta chiuse, anziché essere restituite al pool, queste connessioni vengono eliminate.  
  
## Supporto delle transazioni  
 Le connessioni vengono recuperate dal pool e assegnate in base al contesto della transazione.  Se nella stringa di connessione non è specificato `Enlist=false`, il pool di connessioni assicura che la connessione venga inserita in un elenco del contesto <xref:System.Transactions.Transaction.Current%2A>.  Quando una connessione viene chiusa e restituita al pool con una transazione `System.Transactions` in elenco, questa connessione viene conservata in modo tale che, quando si richiederà nuovamente il pool di connessioni con la stessa transazione `System.Transactions`, verrà restituita la stessa connessione, se è disponibile.  Se viene eseguita una richiesta di questo tipo e non sono disponibili connessioni in pool, viene prelevata e inserita in elenco una connessione della parte non transazionale del pool.  Se non sono disponibili connessioni in alcuna area del pool, viene creata e inserita in elenco una nuova connessione.  
  
 Una volta chiusa, la connessione viene rilasciata nel pool e nella suddivisione appropriata in base al relativo contesto di transazione.  La connessione può quindi essere chiusa senza generare un errore anche se è ancora in sospeso una transazione distribuita.  In questo modo è possibile eseguire il commit o interrompere la transazione distribuita in un secondo momento.  
  
## Controllo del pool di connessioni con parole chiave delle stringhe di connessione  
 La proprietà `ConnectionString` dell'oggetto <xref:System.Data.SqlClient.SqlConnection> supporta le coppie chiave\/valore della stringa di connessione che possono essere usare per regolare il comportamento della logica del pool di connessioni.  Per altre informazioni, vedere <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A>.  
  
## Frammentazione di pool  
 La frammentazione di pool rappresenta un problema comune di varie applicazioni Web in cui l'applicazione può creare numerosi pool che vengono rilasciati solo al termine del processo.  In questo modo, molte connessioni vengono lasciate aperte, occupando memoria e riducendo le prestazioni.  
  
### Frammentazione di pool dovuta alla sicurezza integrata  
 Le connessioni vengono eseguite in pool in base alla stringa di connessione e all'identità utente.  Di conseguenza, se nel sito Web si usa l'autenticazione di base o l'autenticazione Windows, nonché un accesso di sicurezza, si otterrà un pool per ogni utente.  Anche se in questo modo migliorano le prestazioni delle successive richieste di database per il singolo utente, l'utente non può usare le connessioni eseguite da altri.  Viene generata, inoltre, almeno una connessione per utente al server database.  Questo è un effetto collaterale di una particolare architettura di applicazione Web che gli sviluppatori devono tenere in considerazione per non compromettere la sicurezza e il controllo.  
  
### Frammentazione di pool dovuta a numerosi database  
 Molti provider di servizi Internet ospitano numerosi siti Web su un unico server.  Possono usare un unico database per confermare un accesso basato su form e aprire una connessione a un database specifico di un utente o di un gruppo di utenti.  La connessione al database di autenticazione viene eseguita in pool e può essere usata da tutti.  Tuttavia è presente un pool di connessioni separato per ogni database, aumentando il numero di connessioni al server.  
  
 Anche questo è un effetto collaterale della progettazione dell'applicazione.  È relativamente semplice evitare questo effetto collaterale senza compromettere la sicurezza quando ci si connette a [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)].  Invece di connettersi a un solo database per ogni utente o gruppo, è sufficiente connettersi allo stesso database sul server e successivamente eseguire l'istruzione USE [!INCLUDE[tsql](../../../../includes/tsql-md.md)] per passare al database desiderato.  Nel frammento di codice seguente viene illustrata la creazione di una connessione iniziale al database `master` e il passaggio al database specificato nella variabile di tipo stringa `databaseName`.  
  
```vb  
' Assumes that command is a valid SqlCommand object and that  
' connectionString connects to master.  
    command.Text = "USE DatabaseName"  
Using connection As New SqlConnection(connectionString)  
    connection.Open()  
    command.ExecuteNonQuery()  
End Using  
```  
  
```csharp  
// Assumes that command is a SqlCommand object and that  
// connectionString connects to master.  
command.Text = "USE DatabaseName";  
using (SqlConnection connection = new SqlConnection(  
  connectionString))  
  {  
    connection.Open();  
    command.ExecuteNonQuery();  
  }  
```  
  
## Ruoli dell'applicazione e pool di connessioni  
 Dopo che un ruolo dell'applicazione [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)] è stato attivato chiamando la stored procedure di sistema `sp_setapprole`, non è possibile impostare nuovamente il contesto di sicurezza di tale connessione.  Se è attivata la creazione di pool, la connessione verrà restituita al pool e si verificherà un errore quando la connessione in pool verrà riutilizzata.  Per altre informazioni, vedere l'articolo della Knowledge Base relativo agli [errori dei ruoli applicazione SQL con il pool di risorse OLE DB](http://support.microsoft.com/default.aspx?scid=KB;EN-US;Q229564).  
  
### Alternative ai ruoli applicazione  
 Si consiglia di trarre vantaggio dai meccanismi di sicurezza che è possibile usare al posto dei ruoli applicazione.  Per altre informazioni, vedere [Creazione di ruoli applicazione in SQL Server](../../../../docs/framework/data/adonet/sql/creating-application-roles-in-sql-server.md)  
  
## Vedere anche  
 [Pool di connessioni](../../../../docs/framework/data/adonet/connection-pooling.md)   
 [SQL Server e ADO.NET](../../../../docs/framework/data/adonet/sql/index.md)   
 [Contatori di prestazioni](../../../../docs/framework/data/adonet/performance-counters.md)   
 [Provider di dati gestiti ADO.NET e Centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)