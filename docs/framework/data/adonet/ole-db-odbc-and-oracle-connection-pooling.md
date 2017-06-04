---
title: "Pool di connessioni OLEDB, ODBC e Oracle | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2bd83b1e-3ea9-43c4-bade-d9cdb9bbbb04
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Pool di connessioni OLEDB, ODBC e Oracle
Il pool di connessioni consente di migliorare notevolmente le prestazioni e di aumentare la scalabilità dell'applicazione.  Questa sezione descrive il pool di connessioni per i provider di dati .NET Framework per OLE DB, ODBC e Oracle.  
  
## Pool di connessioni per OleDb  
 Il provider di dati .NET Framework per OLE DB esegue automaticamente il pool di connessioni usando i pool di sessioni OLE DB.  È possibile usare gli argomenti di tipo stringa di connessione per abilitare o disabilitare i servizi OLE DB, incluso il pool.  La stringa di connessione seguente, ad esempio, disabilita il pool di sessioni OLE DB e l'inserimento automatico negli elenchi delle transazioni.  
  
```  
Provider=SQLOLEDB;OLE DB Services=-4;Data Source=localhost;Integrated Security=SSPI;  
```  
  
 Al termine dell'uso chiudere o eliminare sempre la connessione, in modo da restituirla al pool.  Le connessioni che non vengono chiuse in modo esplicito potrebbero non essere restituite al pool.  Ad esempio, una connessione che esce dall'ambito ma non viene chiusa in modo esplicito verrà restituita al pool di connessioni solo se è stata raggiunta la dimensione massima del pool e la connessione è ancora valida.  
  
 Per altre informazioni sul pool di sessioni OLE DB o sul pool di risorse, nonché su come disabilitare il pool eseguendo l'override dei valori predefiniti dei servizi del provider OLE DB, vedere i [riferimenti per i programmatori OLE DB](http://go.microsoft.com/fwlink/?linkid=45232) in MSDN Library.  
  
## Pool di connessioni per Odbc  
 Il pool di connessioni per il provider di dati .NET Framework per ODBC è gestito da Gestione driver ODBC, che viene usato anche per la connessione e non è influenzato dal provider di dati .NET Framework per ODBC.  
  
 Per abilitare o disabilitare il pool di connessioni, aprire **Amministratore origine dati ODBC** disponibile nella cartella Strumenti di amministrazione in Pannello di controllo.  Nella scheda **Pool di connessioni** è possibile specificare i parametri del pool di connessioni per ogni driver ODBC installato.  Notare che le modifiche apportate al pool di connessioni per uno specifico driver ODBC avranno effetto su tutte le applicazioni che usano tale driver ODBC.  
  
 Per altre informazioni sul pool di connessioni ODBC, vedere le [domande frequenti sul pool di connessioni ODBC](http://support.microsoft.com/kb/169470) in MSDN Library.  
  
## Pool di connessioni per client Oracle  
 Il provider di dati .NET Framework per Oracle fornisce automaticamente pool di connessioni per l'applicazione client ADO.NET.  È possibile inoltre specificare diversi modificatori delle stringhe di connessione per controllare il comportamento del pool. Per altre informazioni, vedere "Controllo del pool di connessioni con le parole chiave delle stringhe di connessione" in questo argomento.  
  
### Creazione e assegnazione di pool  
 Quando viene aperta una connessione, viene creato un pool di connessioni in base a un algoritmo esattamente corrispondente che associa il pool alla stringa di connessione.  Ogni pool di connessioni è associato a una stringa di connessione distinta.  Quando viene aperta una nuova connessione, se la stringa di connessione non corrisponde esattamente a un pool esistente, viene creato un nuovo pool.  
  
 Una volta creati, i pool di connessioni non vengono eliminati fino a quando non termina il processo attivo.  Per i pool che restano inattivi o vuoti vengono usate pochissime risorse di sistema.  
  
### Aggiunta di connessioni  
 Per ogni stringa di connessione univoca viene creato un pool di connessioni.  Quando si crea un pool, vengono creati e aggiunti al pool più oggetti connessione in modo da soddisfare il requisito relativo alle dimensioni minime del pool.  Le connessioni vengono aggiunte al pool in base alle necessità, fino a raggiungere le dimensioni massime del pool.  
  
 Quando viene richiesto un oggetto <xref:System.Data.OracleClient.OracleConnection>, esso viene ottenuto dal pool se è disponibile una connessione usabile.  Per essere usabile, la connessione non deve essere in uso, deve disporre di un contesto di transazione corrispondente oppure non deve essere associata ad alcun contesto di transazione e deve disporre, infine, di un collegamento valido al server.  
  
 Se le dimensioni massime del pool sono state raggiunte e non è disponibile alcuna connessione usabile, la richiesta viene accodata.  Con la funzione di pool delle connessioni questi requisiti vengono soddisfatti tramite la riallocazione delle connessioni rilasciate nel pool.  Una volta chiuse o eliminate, le connessioni vengono rilasciate nel pool.  
  
### Rimozione della connessione  
 La funzione di pool delle connessioni rimuove una connessione dal pool dopo un periodo di inattività prolungato o se rileva che la connessione al server è stata interrotta.  Notare che questa condizione può essere rilevata solo dopo un tentativo di comunicare con il server.  Se viene individuata una connessione al server che non è più attiva, la connessione viene contrassegnata come non valida.  La funzione di pool delle connessioni analizza periodicamente i pool di connessioni alla ricerca di oggetti che sono stati rilasciati nel pool e che sono contrassegnati come non validi.  Queste connessioni vengono rimosse in modo permanente.  
  
 Se esiste una connessione a un server non più disponibile, la connessione può essere recuperata dal pool anche se nessuna connessione è stata rilevata come interrotta e pertanto non è stata contrassegnata come non valida.  Quando si verifica questa situazione, viene generata un'eccezione.  È necessario, tuttavia, chiudere la connessione in modo da rilasciarla nel pool.  
  
 Non chiamare `Close` o `Dispose` su un oggetto `Connection`, `DataReader` o su qualsiasi altro oggetto gestito nel metodo `Finalize` della classe.  Nei finalizzatori rilasciare solo le risorse non gestite che la classe controlla direttamente.  Se nella classe non sono presenti risorse non gestite, non includere un metodo `Finalize` nella relativa definizione della classe.  Per altre informazioni, vedere [Garbage Collection](../../../../docs/standard/garbage-collection/index.md).  
  
### Supporto delle transazioni  
 Le connessioni vengono recuperate dal pool e assegnate in base al contesto della transazione.  Il contesto del thread richiedente e la connessione assegnata devono corrispondere.  Pertanto ogni pool di connessioni viene effettivamente suddiviso in connessioni senza alcun contesto di transazione associato e in *N* suddivisioni, ognuna delle quali contiene connessioni con un particolare contesto di transazione.  
  
 Una volta chiusa, la connessione viene rilasciata nel pool e nella suddivisione appropriata in base al relativo contesto di transazione.  La connessione può quindi essere chiusa senza generare un errore anche se è ancora in sospeso una transazione distribuita.  Questo sistema consente di eseguire o interrompere la transazione distribuita in un secondo momento.  
  
### Controllo del pool di connessioni con parole chiave delle stringhe di connessione  
 La proprietà <xref:System.Data.OracleClient.OracleConnection.ConnectionString%2A> dell'oggetto <xref:System.Data.OracleClient.OracleConnection> supporta le coppie chiave\/valore della stringa di connessione che possono essere usare per regolare il comportamento della logica del pool di connessioni.  
  
 La tabella seguente descrive i valori <xref:System.Data.OracleClient.OracleConnection.ConnectionString%2A> che consentono di regolare il comportamento del pool di connessioni.  
  
|Nome|Default|Descrizione|  
|----------|-------------|-----------------|  
|`Connection Lifetime`|0|Quando una connessione viene restituita al pool, l'ora di creazione viene confrontata con l'ora corrente e la connessione viene eliminata se l'intervallo è superiore al valore in secondi della durata della connessione specificato da `Connection Lifetime`.  Questa è utile nelle configurazioni cluster per applicare il bilanciamento del carico tra un server in esecuzione e un server appena portato online.<br /><br /> Un valore zero \(0\) imposta il timeout massimo delle connessioni in pool.|  
|`Enlist`|'true'|Se l'impostazione è `true`, la funzione di pool inserisce automaticamente la connessione nel contesto della transazione corrente del thread di creazione, se è disponibile un contesto di transazione.|  
|`Max Pool Size`|100|Numero massimo di connessioni consentite nel pool.|  
|`Min Pool Size`|0|Numero minimo di connessioni gestite nel pool.|  
|`Pooling`|'true'|Se l'impostazione è `true`, la connessione viene recuperata dal pool appropriato o, se necessario, creata e aggiunta al pool appropriato.|  
  
## Vedere anche  
 [Pool di connessioni](../../../../docs/framework/data/adonet/connection-pooling.md)   
 [Contatori di prestazioni](../../../../docs/framework/data/adonet/performance-counters.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)