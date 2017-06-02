---
title: "Domande frequenti | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 252ed666-0679-4eea-b71b-2f14117ef443
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Domande frequenti
Nelle sezioni seguenti vengono fornite le risposte ad alcuni problemi comuni che possono verificarsi durante l'implementazione di [!INCLUDE[vbteclinq](../../../../../../includes/vbteclinq-md.md)].  
  
 In [Risoluzione dei problemi](../../../../../../docs/framework/data/adonet/sql/linq/troubleshooting.md) vengono esaminati altri problemi.  
  
## Impossibile connettersi  
 D.  Non è possibile connettersi al database.  
  
 Un   Assicurarsi che la stringa di connessione sia corretta e che l'istanza [!INCLUDE[ssNoVersion](../../../../../../includes/ssnoversion-md.md)] sia in esecuzione.  Tenere inoltre presente che [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] richiede che sia abilitato il protocollo Named Pipes.  Per altre informazioni, vedere [Apprendimento tramite le procedure dettagliate](../../../../../../docs/framework/data/adonet/sql/linq/learning-by-walkthroughs.md).  
  
## Perdita delle modifiche al database  
 D.  Quando si riesegue l'applicazione dopo avere apportato una modifica ai dati presenti nel database, la modifica va persa.  
  
 Un   Accertarsi di chiamare <xref:System.Data.Linq.DataContext.SubmitChanges%2A> per salvare i risultati nel database.  
  
## Durata di una connessione di database aperta  
 D.  Per quanto tempo rimane aperta la connessione di database?  
  
 Un   Una connessione rimane in genere aperta finché non si usano i risultati della query.  Se si prevede di impiegare tempo per elaborare tutti i risultati ed è possibile memorizzare nella cache i risultati, applicare <xref:System.Linq.Enumerable.ToList%2A> alla query.  Negli scenari comuni dove ogni oggetto viene elaborato solo una volta, il modello di flusso è superiore in `DataReader` e [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  
  
 I dettagli esatti di utilizzo della connessione dipendono dagli elementi seguenti:  
  
-   Stato della connessione se <xref:System.Data.Linq.DataContext> viene costruito con un oggetto connessione.  
  
-   Impostazioni della stringa di connessione, ad esempio abilitando MARS \(Multiple Active Result Sets\).  Per altre informazioni, vedere [MARS \(Multiple Active Result Set\)](../../../../../../docs/framework/data/adonet/sql/multiple-active-result-sets-mars.md).  
  
## Aggiornamento senza query  
 D.  È possibile aggiornare i dati della tabella senza prima eseguire una query sul database?  
  
 Un   Sebbene [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] non disponga di comandi di aggiornamento basati su set, è possibile usare le tecniche seguenti per aggiornare senza prima eseguire una query:  
  
-   Usare <xref:System.Data.Linq.DataContext.ExecuteCommand%2A> per inviare il codice SQL.  
  
-   Creare una nuova istanza dell'oggetto e inizializzare tutti i valori \(campi\) correnti che influiscono sull'aggiornamento.  Associare quindi l'oggetto a <xref:System.Data.Linq.DataContext> usando <xref:System.Data.Linq.Table%601.Attach%2A> e modificare il campo desiderato.  
  
## Risultati imprevisti delle query  
 D.  La query restituisce risultati imprevisti.  Come è possibile controllare quello che si sta verificando?  
  
 Un   [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] fornisce molti strumenti per controllare il codice SQL generato.  Uno dei più importanti è <xref:System.Data.Linq.DataContext.Log%2A>.  Per altre informazioni, vedere [Supporto per il debug](../../../../../../docs/framework/data/adonet/sql/linq/debugging-support.md).  
  
## Risultati imprevisti delle stored procedure  
 D.  Il valore restituito di una stored procedure viene calcolato da `MAX()`.  Quando si trascina la stored procedure nell'area della [!INCLUDE[vs_ordesigner_short](../../../../../../includes/vs-ordesigner-short-md.md)], il valore restituito non è corretto.  
  
 Un   [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] fornisce due modalità per restituire i valori generati dal database tramite le stored procedure:  
  
-   Assegnando un nome al risultato di output.  
  
-   Specificando in modo esplicito un parametro di output.  
  
 Di seguito viene riportato un esempio di output non corretto.  Poiché in [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] non è possibile eseguire il mapping dei risultati, viene restituito sempre 0:  
  
 `create procedure proc2`  
  
 `as`  
  
 `begin`  
  
 `select max(i) from t where name like 'hello'`  
  
 `end`  
  
 Di seguito viene riportato un esempio di output corretto usando un parametro di output:  
  
 `create procedure proc2`  
  
 `@result int OUTPUT`  
  
 `as`  
  
 `select @result = MAX(i) from t where name like 'hello'`  
  
 `go`  
  
 Di seguito viene riportato un esempio di output corretto assegnando un nome al risultato di output:  
  
 `create procedure proc2`  
  
 `as`  
  
 `begin`  
  
 `select nax(i) AS MaxResult from t where name like 'hello'`  
  
 `end`  
  
 Per altre informazioni, vedere [Personalizzazione delle operazioni tramite l'utilizzo di stored procedure](../../../../../../docs/framework/data/adonet/sql/linq/customizing-operations-by-using-stored-procedures.md).  
  
## Errori di inizializzazione  
 D.  Durante la serializzazione, si verifica il seguente errore: "Tipo 'System.Data.Linq.ChangeTracker\+StandardChangeTracker' ...  non contrassegnato come serializzabile".  
  
 Un   La generazione del codice in [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] supporta la serializzazione <xref:System.Runtime.Serialization.DataContractSerializer>.  Non supporta <xref:System.Xml.Serialization.XmlSerializer> o <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>.  Per altre informazioni, vedere [Serializzazione](../../../../../../docs/framework/data/adonet/sql/linq/serialization.md).  
  
## Più file DBML  
 D.  Quando si dispone di più file DBML che condividono alcune tabelle, si verifica un errore del compilatore.  
  
 Un   Impostare le proprietà **Context Namespace** e **Entity Namespace** della [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)] su un valore distinto per ogni file DBML.  Questo approccio elimina il conflitto di nome\/spazio dei nomi.  
  
## Come evitare l'impostazione esplicita dei valori generati dal database nelle operazioni di inserimento o aggiornamento  
 D.  Quando in una tabella di database con una colonna `DateCreated` la cui impostazione predefinita è SQL `Getdate()` si tenta di inserire un nuovo record usando [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)], il valore viene impostato su `NULL` anziché sul valore predefinito del database.  
  
 Un   [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] gestisce automaticamente questa situazione per le colonne Identity \(incremento automatico\) e rowguidcol \(GUID generato dal database\) e timestamp.  Negli altri casi, impostare manualmente le proprietà <xref:System.Data.Linq.Mapping.ColumnAttribute.IsDbGenerated%2A>\=`true` e <xref:System.Data.Linq.Mapping.ColumnAttribute.AutoSync%2A>\=<xref:System.Data.Linq.Mapping.AutoSync>\/<xref:System.Data.Linq.Mapping.AutoSync>\/<xref:System.Data.Linq.Mapping.AutoSync>.  
  
## Più valori DataLoadOptions  
 D.  È possibile specificare opzioni di caricamento aggiuntive senza sovrascrivere la prima?  
  
 Un   Sì.  La prima opzione non viene sovrascritta, come illustrato nell'esempio seguente:  
  
```vb  
Dim dlo As New DataLoadOptions()  
dlo.LoadWith(Of Order)(Function(o As Order) o.Customer)  
dlo.LoadWith(Of Order)(Function(o As Order) o.OrderDetails)  
```  
  
```csharp  
DataLoadOptions dlo = new DataLoadOptions();  
dlo.LoadWith<Order>(o => o.Customer);  
dlo.LoadWith<Order>(o => o.OrderDetails);  
```  
  
## Errori durante l'uso di SQL Compact 3.5  
 D.  Quando si trascinano le tabelle al di fuori di un database [!INCLUDE[ssEW](../../../../../../includes/ssew-md.md)], si verifica un errore.  
  
 Un   [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)] non supporta [!INCLUDE[ssEW](../../../../../../includes/ssew-md.md)], sebbene sia supportato dal runtime [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  In questa situazione, è necessario creare classi dell'entità personalizzate e aggiungere gli attributi adatti.  
  
## Errori nelle relazioni di ereditarietà  
 D.  Quando si usa la forma di ereditarietà della casella degli strumenti nella [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)] per connettere due entità, si verificano errori.  
  
 Un   Non è sufficiente creare la relazione.  È necessario fornire informazioni quali la colonna del discriminatore, il valore del discriminatore della classe base e il valore del discriminatore della classe derivata.  
  
## Modello provider  
 D.  È disponibile un modello provider pubblico?  
  
 Un   Non è disponibile alcun un modello provider pubblico.  Attualmente, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] supporta solo [!INCLUDE[ssNoVersion](../../../../../../includes/ssnoversion-md.md)] e [!INCLUDE[ssEW](../../../../../../includes/ssew-md.md)].  
  
## Attacchi SQL injection  
 D.  Come viene protetto [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] dagli attacchi SQL injection?  
  
 Un   L'intrusione nel codice SQL ha rappresentato un pericolo significativo per le query SQL tradizionali formate concatenando l'input dell'utente.  [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] evita tale intrusione usando <xref:System.Data.SqlClient.SqlParameter> nelle query.  L'input dell'utente viene convertito in valori di parametro.  Questo approccio impedisce l'uso di comandi dannosi dall'input del cliente.  
  
## Modifica del flag di sola lettura nei file DBML  
 D.  Come è possibile eliminare i metodi di impostazione da alcune proprietà quando si crea un modello a oggetti da un file DBML?  
  
 Un   Attenersi alla procedura riportata di seguito per questo scenario avanzato:  
  
1.  Nel file con estensione dbml modificare la proprietà impostando il flag <xref:System.Data.Linq.ITable.IsReadOnly%2A> su `True`.  
  
2.  Aggiungere una classe parziale.  Creare un costruttore con i parametri per i membri di sola lettura.  
  
3.  Esaminare il valore <xref:System.Data.Linq.Mapping.UpdateCheck> predefinito \(<xref:System.Data.Linq.Mapping.UpdateCheck>\) per determinare se questo valore è corretto per l'applicazione.  
  
    > [!CAUTION]
    >  Se si usa [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)] in [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)], è possibile che le modifiche vengano sovrascritte.  
  
## APTCA  
 D.  System.Data.Linq è contrassegnato per l'uso da codice parzialmente attendibile?  
  
 Un   Sì, l'assembly System.Data.Linq.dll è tra gli assembly [!INCLUDE[dnprdnshort](../../../../../../includes/dnprdnshort-md.md)] contrassegnati con l'attributo <xref:System.Security.AllowPartiallyTrustedCallersAttribute>.  Senza questo contrassegno, gli assembly in [!INCLUDE[dnprdnshort](../../../../../../includes/dnprdnshort-md.md)] vengono usati solo da codice completamente attendibile.  
  
 Lo scenario principale in [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] per consentire chiamanti parzialmente attendibili è fornire all'assembly [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] l'accesso dalle applicazioni Web, dove la configurazione *trust* è impostata su Medio.  
  
## Esecuzione del mapping dei dati da più tabelle  
 D.  I dati dell'entità derivano da più tabelle.  Come è possibile eseguirne il mapping?  
  
 Un   È possibile creare una visualizzazione in un database ed eseguire il mapping dell'entità alla visualizzazione.  [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] genera lo stesso codice SQL per le visualizzazioni come per le tabelle.  
  
> [!NOTE]
>  L'utilizzo di visualizzazioni in questo scenario presenta delle limitazioni.  Questo approccio funziona in modo più sicuro quando le operazioni eseguite su <xref:System.Data.Linq.Table%601> vengono supportate dalla visualizzazione sottostante.  Solo l'utente conosce le operazioni desiderate da eseguire.  Ad esempio, la maggior parte delle applicazioni sono di sola lettura mentre altre applicazioni eseguono le operazioni `Create`\/`Update`\/`Delete` solo usando le stored procedure sulle visualizzazioni.  
  
## Pool di connessioni  
 D.  È disponibile un costrutto che possa facilitare il pool <xref:System.Data.Linq.DataContext>?  
  
 Un   Non tentare di riutilizzare le istanze di <xref:System.Data.Linq.DataContext>.  Ogni oggetto <xref:System.Data.Linq.DataContext> conserva lo stato \(inclusa una cache delle identità\) per una determinata sessione di modifica\/query.  Per ottenere nuove istanze basate sullo stato corrente del database, usare un nuovo oggetto <xref:System.Data.Linq.DataContext>.  
  
 È tuttavia possibile usare il pool di connessioni [!INCLUDE[vstecado](../../../../../../includes/vstecado-md.md)] sottostante.  Per altre informazioni, vedere [Pool di connessioni di SQL Server \(ADO.NET\)](../../../../../../docs/framework/data/adonet/sql-server-connection-pooling.md).  
  
## Il secondo oggetto DataContext non viene aggiornato  
 D.  Un'istanza di <xref:System.Data.Linq.DataContext> è stata usata per archiviare i valori nel database.  Tuttavia, un secondo oggetto <xref:System.Data.Linq.DataContext> nello stesso database non riflette i valori aggiornati.  La seconda istanza <xref:System.Data.Linq.DataContext> sembra restituire i valori memorizzati nella cache.  
  
 Un   Questo comportamento è previsto dalla progettazione.  [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] continua a restituire gli stessi valori o le stesse istanze specificate nella prima istanza.  Quando si effettuano gli aggiornamenti, usare la concorrenza ottimistica.  I dati originali vengono usati per controllare lo stato corrente del database in modo da asserire che risulta ancora invariato.  Se è stato modificato, si verifica un conflitto e l'applicazione deve risolverlo.  Un'opzione dell'applicazione è reimpostare lo stato originale allo stato corrente del database e provare nuovamente l'aggiornamento.  Per altre informazioni, vedere [Procedura: gestire i conflitti di modifiche](../../../../../../docs/framework/data/adonet/sql/linq/how-to-manage-change-conflicts.md).  
  
 È anche possibile impostare <xref:System.Data.Linq.DataContext.ObjectTrackingEnabled%2A> su false, in modo da disattivare la memorizzazione nella cache e la ricerca delle modifiche.  È quindi possibile recuperare gli ultimi valori ogni volta che si esegue una query.  
  
## Impossibile chiamare SubmitChanges in modalità di sola lettura  
 D.  Quando si tenta di chiamare <xref:System.Data.Linq.DataContext.SubmitChanges%2A> in modalità di sola lettura, si verifica un errore.  
  
 Un   La modalità di sola lettura non consente al contesto di tenere traccia delle modifiche.  
  
## Vedere anche  
 [Riferimenti](../../../../../../docs/framework/data/adonet/sql/linq/reference.md)   
 [Risoluzione dei problemi](../../../../../../docs/framework/data/adonet/sql/linq/troubleshooting.md)   
 [Sicurezza in LINQ to SQL](../../../../../../docs/framework/data/adonet/sql/linq/security-in-linq-to-sql.md)