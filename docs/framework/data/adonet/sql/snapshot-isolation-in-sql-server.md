---
title: "Isolamento dello snapshot in SQL Server | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 43ae5dd3-50f5-43a8-8d01-e37a61664176
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# Isolamento dello snapshot in SQL Server
L'isolamento dello snapshot migliora la concorrenza per le applicazioni OLTP.  
  
## Informazioni sull'isolamento dello snapshot e il controllo delle versioni delle righe  
 Una volta abilitato l'isolamento dello snapshot, le versioni delle righe aggiornate per ciascuna transazione vengono conservate nel database temporaneo **tempdb**.  Ciascuna transazione viene identificata mediante un numero di sequenza univoco. Questi numeri vengono registrati per ciascuna versione di riga.  La transazione funziona con le versioni di riga più recenti che dispongono di un numero di sequenza che precede il numero di sequenza della transazione.  La transazione ignora le versioni di riga più recenti, create dopo l'inizio della transazione stessa.  
  
 Il termine "snapshot" è dovuto al fatto che tutte le query nella transazione rilevano la stessa versione, o snapshot, del database, in base allo stato del database all'inizio della transazione.  In una transazione snapshot non vengono acquisiti blocchi sulle pagine di dati o sulle righe di dati sottostanti. In questo modo è possibile eseguire altre transazioni senza che vengano bloccate da una precedente transazione non completata.  Le transazioni di modifica dei dati non bloccano le transazioni di lettura dei dati così come queste ultime non bloccano le transazioni di scrittura dei dati, esattamente come avviene nel livello di isolamento READ COMMITTED in SQL Server.  Questo comportamento non bloccante riduce notevolmente la probabilità di blocchi critici per le transazioni complesse.  
  
 L'isolamento dello snapshot usa un modello di concorrenza ottimistica.  Se una transazione snapshot tenta di eseguire il commit delle modifiche apportate ai dati dall'inizio della transazione, verrà eseguito il rollback della transazione e verrà generato un errore.  Per evitare che questo si verifichi, è possibile usare i suggerimenti UPDLOCK per le istruzioni SELECT che accedono ai dati da modificare.  Per altre informazioni, vedere l'argomento relativo agli hint di blocco nella documentazione online di SQL Server.  
  
 L'isolamento dello snapshot deve essere abilitato impostando l'opzione di database ALLOW\_SNAPSHOT\_ISOLATION ON prima di usarlo per le transazioni.  Questa operazione consente di attivare il meccanismo di archiviazione delle versioni delle righe nel database temporaneo \(**tempdb**\).  È necessario abilitare l'isolamento dello snapshot in ciascun database in cui esso viene usato con l'istruzione ALTER DATABASE di Transact\-SQL.  In questo senso, l'isolamento dello snapshot differisce dai livelli di isolamento tradizionali di READ COMMITTED, REPEATABLE READ, SERIALIZABLE e READ UNCOMMITTED, che non richiedono alcuna configurazione.  Le istruzioni seguenti attivano l'isolamento dello snapshot e sostituiscono il comportamento READ COMMITTED predefinito con SNAPSHOT:  
  
```  
ALTER DATABASE MyDatabase  
SET ALLOW_SNAPSHOT_ISOLATION ON  
  
ALTER DATABASE MyDatabase  
SET READ_COMMITTED_SNAPSHOT ON  
```  
  
 L'impostazione dell'opzione READ\_COMMITTED\_SNAPSHOT ON consente di accedere alle righe la cui versione è stata controllata, al livello di isolamento READ COMMITTED predefinito.  Se l'opzione READ\_COMMITTED\_SNAPSHOT è impostata su OFF, per accedere alle righe della versione è necessario impostare il livello di isolamento dello snapshot in maniera esplicita per ciascuna sessione.  
  
## Gestione della concorrenza con livelli di isolamento  
 Il livello di isolamento al quale viene eseguita un'istruzione di Transact\-SQL determina il comportamento di blocco e di controllo della versione della riga.  Un livello di isolamento dispone di un ambito di connessione, che, una volta impostato per una connessione con l'istruzione SET TRANSACTION ISOLATION LEVEL, rimane attivo finché non viene chiusa la connessione o non viene impostato un livello di isolamento diverso.  Quando una connessione viene chiusa e restituita al pool, il livello di isolamento dall'ultima istruzione SET TRANSACTION ISOLATION LEVEL viene mantenuto.  Le successive connessioni che riutilizzano una connessione in pool usano il livello di isolamento che era attivo nel momento in cui la connessione è stata inserita nel pool.  
  
 Le singole query eseguite in una connessione possono contenere hint di blocco in grado di modificare l'isolamento per una singola istruzione o transazione, ma che non possono influire sul livello della connessione.  I livelli di isolamento o gli hint di blocco impostati in funzioni o stored procedure non modificano il livello di isolamento della connessione che li ha chiamati e restano validi solo per la durata della stored procedure o della chiamata di funzione.  
  
 I quattro livelli di isolamento definiti nello standard SQL\-92 sono supportati nelle prime versioni di SQL Server:  
  
-   READ UNCOMMITTED rappresenta il livello di isolamento meno restrittivo perché ignora i blocchi inseriti da altre transazioni.  Le transazioni eseguite in READ UNCOMMITTED possono leggere i valori dei dati modificati non ancora sottoposti a commit da altre transazioni. Queste letture vengono definite "dirty".  
  
-   READ COMMITTED è il livello di isolamento predefinito per SQL Server.  Questo livello consente di impedire le letture dirty, specificando che le istruzioni non possono leggere i valori dei dati modificati ma non ancora sottoposti a commit da altre transazioni.  Altre transazioni possono ancora modificare, inserire o eliminare dati tra le esecuzioni di singole istruzioni all'interno della transazione corrente, dando luogo a letture non ripetibili o dati "fantasma".  
  
-   REPEATABLE READ è un livello di isolamento più restrittivo di READ COMMITTED.  Esso include il livello READ COMMITTED e aggiunge la limitazione in base alla quale nessun'altra transazione può modificare o eliminare dati letti dalla transazione corrente finché questa non viene sottoposta a commit.  La concorrenza è minore rispetto al livello READ COMMITTED in quanto i blocchi condivisi sui dati letti vengono conservati per la durata della transazione anziché rilasciati al termine di ciascuna istruzione.  
  
-   SERIALIZABLE è il livello di isolamento più restrittivo, in quanto blocca intere gamme di chiavi e trattiene i blocchi finché la transazione non è stata completata.  Esso include il livello REPEATABLE READ e aggiunge la limitazione in base alla quale altre transazioni non possono inserire nuove righe negli intervalli letti dalla transazione finché quest'ultima non è stata completata.  
  
 Per altre informazioni, vedere l'argomento relativo ai livelli di isolamento nella documentazione online di SQL Server.  
  
### Estensione del livello di isolamento dello snapshot  
 In SQL Server sono state introdotte estensioni ai livelli di isolamento SQL\-92 sotto forma del livello di isolamento SNAPSHOT e un'implementazione aggiuntiva di READ COMMITTED.  Il livello di isolamento READ\_COMMITTED\_SNAPSHOT può sostituire READ COMMITTED per tutte le transazioni.  
  
-   L'isolamento SNAPSHOT specifica che i dati letti all'interno di una transazione non rifletteranno mai le modifiche apportate da altre transazioni simultanee.  La transazione usa le versioni delle righe dei dati esistenti al momento in cui tale transazione viene iniziata.  Sui dati non viene posizionato alcun blocco al momento della lettura, quindi le transazioni SNAPSHOT non impediscono la scrittura di dati da parte di altre transazioni.  Le transazioni di scrittura dei dati non bloccano la lettura dei dati da parte delle transazioni snapshot.  È necessario abilitare l'isolamento dello snapshot impostando l'opzione di database ALLOW\_SNAPSHOT\_ISOLATION.  
  
-   L'opzione di database READ\_COMMITTED\_SNAPSHOT determina il comportamento del livello di isolamento READ COMMITTED predefinito quando nel database viene abilitato l'isolamento dello snapshot.  Se non si specifica in maniera esplicita l'opzione READ\_COMMITTED\_SNAPSHOT ON, il livello READ COMMITTED viene applicato a tutte le transazioni implicite.  Ciò provoca lo stesso comportamento dell'impostazione READ\_COMMITTED\_SNAPSHOT OFF \(predefinita\).  Quando è attiva l'impostazione READ\_COMMITTED\_SNAPSHOT OFF, il motore di database usa i blocchi condivisi per l'applicazione del livello di isolamento.  Se si imposta l'opzione di database READ\_COMMITTED\_SNAPSHOT su ON, per impostazione predefinita il motore di database usa il controllo delle versioni delle righe e l'isolamento dello snapshot, anziché usare i blocchi per proteggere i dati.  
  
## Funzionamento dell'isolamento dello snapshot e del controllo delle versioni delle righe  
 Quando viene abilitato il livello di isolamento SNAPSHOT, ogni volta che una riga viene aggiornata, il motore di database di SQL Server archivia una copia della riga originale nel database temporaneo **tempdb** e aggiunge un numero di sequenza della transazione alla riga.  Di seguito è riportata la sequenza degli eventi che si verificano:  
  
-   Viene avviata una nuova transazione alla quale viene assegnato un numero di sequenza.  
  
-   Il motore di database legge una riga all'interno della transazione e recupera dal database temporaneo **tempdb** la versione della riga il cui numero di sequenza è il più vicino e inferiore al numero di sequenza della transazione.  
  
-   Il motore di database controlla se il numero di sequenza della transazione è presente nell'elenco dei numeri di sequenza delle transazioni attive non sottoposte a commit al momento dell'avvio della transazione snapshot.  
  
-   La transazione legge dal database temporaneo **tempdb** la versione della riga disponibile all'inizio della transazione.  Non rileverà nuove righe inserite dopo che la transazione è stata avviata in quanto questi valori del numero di sequenza sono maggiori del valore del numero di sequenza della transazione.  
  
-   La transazione corrente rileverà righe eliminate dopo che la transazione è stata iniziata, in quanto nel database temporaneo **tempdb** sarà disponibile una versione della riga che presenta un valore del numero di sequenza minore.  
  
 L'effetto dell'isolamento consiste nel fatto che la transazione rileva tutti i dati esattamente come erano al momento dell'avvio della transazione stessa, senza rispettare o posizionare blocchi sulle tabelle sottostanti.  Ciò può comportare un miglioramento delle prestazioni in situazioni di conflitto.  
  
 Una transazione snapshot usa sempre il controllo della concorrenza ottimistica, rifiutando blocchi che potrebbero impedire l'aggiornamento delle righe da parte di altre transazioni.  Se una transazione snapshot tenta di eseguire il commit di un aggiornamento per una riga modificata dopo l'inizio della transazione, viene eseguito il rollback della transazione e viene generato un errore.  
  
## Utilizzo dell'isolamento dello snapshot in ADO.NET  
 L'isolamento dello snapshot è supportato in ADO.NET dalla classe <xref:System.Data.SqlClient.SqlTransaction>.  Se un database è abilitato per l'isolamento dello snapshot ma non è configurato per READ\_COMMITTED\_SNAPSHOT ON, è necessario avviare una transazione <xref:System.Data.SqlClient.SqlTransaction> usando il valore di enumerazione **IsolationLevel.Snapshot** quando viene chiamato il metodo <xref:System.Data.SqlClient.SqlConnection.BeginTransaction%2A>.  Questo frammento di codice presuppone che la connessione sia un oggetto <xref:System.Data.SqlClient.SqlConnection> aperto.  
  
```vb  
Dim sqlTran As SqlTransaction = _  
  connection.BeginTransaction(IsolationLevel.Snapshot)  
```  
  
```csharp  
SqlTransaction sqlTran =   
  connection.BeginTransaction(IsolationLevel.Snapshot);  
```  
  
### Esempio  
 Nell'esempio seguente viene illustrato il comportamento dei diversi livelli di isolamento mediante il tentativo di accesso ai dati bloccati. Questo esempio non può essere usato nel codice di produzione.  
  
 Il codice esegue la connessione al database di esempio **AdventureWorks** in SQL Server, crea una tabella denominata **TestSnapshot** e inserisce una riga di dati.  Il codice usa l'istruzione ALTER DATABASE di Transact\-SQL per attivare l'isolamento dello snapshot per il database, ma non imposta l'opzione READ\_COMMITTED\_SNAPSHOT, lasciando attivo il comportamento a livello di isolamento READ COMMITTED predefinito.  Nel codice vengono eseguite le seguenti azioni:  
  
-   Inizia, ma non completa, sqlTransaction1, che usa il livello di isolamento SERIALIZABLE per avviare la transazione di aggiornamento.  Ciò consente di bloccare la tabella.  
  
-   Apre una seconda connessione e avvia una seconda transazione usando il livello di isolamento SNAPSHOT per leggere i dati nella tabella **TestSnapshot**.  Poiché l'isolamento dello snapshot è abilitato, la transazione può leggere i dati esistenti prima che venga avviata sqlTransaction1.  
  
-   Apre una terza connessione e avvia una transazione usando il livello di isolamento READ COMMITTED per tentare di leggere i dati nella tabella.  In tal caso, il codice non può leggere i dati perché non è in grado di leggere informazioni successive al posizionamento dei blocchi sulla tabella nella prima transazione, pertanto verrà eseguito il timeout.  Lo stesso risultato si ottiene con i livelli di isolamento REPEATABLE READ e SERIALIZABLE poiché questi non possono leggere le informazioni successive al posizionamento dei blocchi nella prima transazione.  
  
-   Apre una quarta connessione e avvia una transazione usando il livello di isolamento READ UNCOMMITTED, che esegue una lettura dirty del valore del quale non è stato eseguito il commit in sqlTransaction1.  Se non è stato eseguito il commit della prima transazione, questo valore non può esistere nel database.  
  
-   Esegue il rollback della prima transazione, elimina la tabella **TestSnapshot** e disattiva l'isolamento dello snapshot per il database **AdventureWorks**.  
  
> [!NOTE]
>  Negli esempi seguenti viene usata la stessa stringa di connessione con il pool di connessioni disattivato.  Se una connessione è in pool, la reimpostazione del relativo livello di isolamento non implica quella del livello di isolamento nel server.  Di conseguenza, le connessioni successive che usano la stessa connessione interna in pool vengono avviate con i livelli di isolamento impostati su quello della connessione in pool.  In alternativa a disattivare il pool di connessioni, è possibile impostare il livello di isolamento in modo esplicito per ogni connessione.  
  
 [!code-csharp[DataWorks SnapshotIsolation.Demo#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SnapshotIsolation.Demo/CS/source.cs#1)]
 [!code-vb[DataWorks SnapshotIsolation.Demo#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SnapshotIsolation.Demo/VB/source.vb#1)]  
  
### Esempio  
 Nell'esempio seguente viene illustrato il comportamento dell'isolamento dello snapshot durante la modifica dei dati.  Nel codice vengono eseguite le seguenti azioni:  
  
-   Connette il database di esempio **AdventureWorks** e abilita l'isolamento SNAPSHOT.  
  
-   Crea una tabella denominata **TestSnapshotUpdate** e inserisce tre righe di dati di esempio.  
  
-   Inizia, ma non completa, sqlTransaction1 usando l'isolamento SNAPSHOT.  Nella transazione vengono selezionate tre righe di dati.  
  
-   Crea una seconda **SqlConnection** in **AdventureWorks** e crea una seconda transazione usando il livello di isolamento READ COMMITTED che aggiorna un valore in una delle righe selezionate in sqlTransaction1.  
  
-   Esegue il commit di sqlTransaction2.  
  
-   Torna a sqlTransaction1 e tenta di aggiornare la stessa riga di cui è già stato eseguito il commit da sqlTransaction1.  Viene generato l'errore 3960 e viene eseguito il rollback automatico di sqlTransaction1.  **SqlException.Number** e **SqlException.Message** sono visualizzati nella finestra della console.  
  
-   Esegue il codice di pulizia per disattivare l'isolamento dello snapshot in **AdventureWorks** ed elimina la tabella **TestSnapshotUpdate**.  
  
 [!code-csharp[DataWorks SnapshotIsolation.DemoUpdate#1](../../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SnapshotIsolation.DemoUpdate/CS/source.cs#1)]
 [!code-vb[DataWorks SnapshotIsolation.DemoUpdate#1](../../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SnapshotIsolation.DemoUpdate/VB/source.vb#1)]  
  
### Utilizzo degli hint di blocco con l'isolamento dello snapshot  
 Nell'esempio precedente la prima transazione seleziona i dati mentre una seconda transazione li aggiorna prima del completamento della prima transazione, causando un conflitto di aggiornamento nel momento in cui la prima transazione tenta di aggiornare la stessa riga.  È possibile limitare le probabilità che si verifichi un conflitto di aggiornamento nelle transazioni snapshot a esecuzione prolungata fornendo hint di blocco all'inizio della transazione.  Nell'istruzione SELECT seguente viene usato l'hint UPDLOCK per bloccare le righe selezionate:  
  
```  
SELECT * FROM TestSnapshotUpdate WITH (UPDLOCK)   
  WHERE PriKey BETWEEN 1 AND 3  
```  
  
 L'utilizzo dell'hint di blocco UPDLOCK consente di bloccare eventuali tentativi di aggiornamento delle righe prima del completamento della prima transazione.  Ciò garantisce che non si verifichino conflitti quando le righe vengono aggiornate in seguito nella transazione.  Vedere l'argomento relativo agli hint di blocco nella documentazione online di SQL Server.  
  
 Se si verificano molti conflitti, l'isolamento dello snapshot potrebbe non rivelarsi la scelta migliore.  Gli hint devono essere usati solo se veramente necessari.  L'applicazione non è stata progettata per essere basata sugli hint di blocco dell'operazione.  
  
## Vedere anche  
 [SQL Server e ADO.NET](../../../../../docs/framework/data/adonet/sql/index.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)