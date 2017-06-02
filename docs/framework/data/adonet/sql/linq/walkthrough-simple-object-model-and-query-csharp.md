---
title: "Procedura dettagliata: modello a oggetti e query semplici (C#) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 419961cc-92d6-45f5-ae8a-d485bdde3a37
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Procedura dettagliata: modello a oggetti e query semplici (C#)
Questa procedura dettagliata descrive uno scenario [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] end\-to\-end di base con complessità minime. Verranno create una classe di entità per la modellazione della tabella Customers nel database Northwind di esempio,  quindi una semplice query per elencare i clienti residenti nell'area londinese.  
  
 Questa procedura dettagliata è basata sul codice in fase di progettazione per illustrare i concetti di [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  Normalmente per creare il modello a oggetti si usa [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)].  
  
 [!INCLUDE[note_settings_general](../../../../../../includes/note-settings-general-md.md)]  
  
 Questa procedura è stata scritta usando Impostazioni di sviluppo di Visual C\#.  
  
## Prerequisiti  
  
-   Per i file usati nella procedura dettagliata viene usata una cartella dedicata \("c:\\linqtest5"\).  Creare la cartella prima di avviare la procedura.  
  
-   Per questa procedura dettagliata è richiesto il database di esempio Northwind.  Se questo database non è disponibile nel computer di sviluppo, è possibile scaricarlo dal sito di download Microsoft.  Per istruzioni, vedere [Download dei database di esempio](../../../../../../docs/framework/data/adonet/sql/linq/downloading-sample-databases.md).  Dopo avere scaricato il database, copiare il file nella cartella c:\\linqtest5.  
  
## Panoramica  
 La procedura dettagliata è costituita da sei attività principali:  
  
-   Creazione di una soluzione [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] in [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)].  
  
-   Mapping di una classe a una tabella del database.  
  
-   Definizione di proprietà nella classe per rappresentare colonne del database.  
  
-   Definizione della connessione al database Northwind.  
  
-   Creazione di una semplice query da eseguire sul database.  
  
-   Esecuzione della query e analisi dei risultati.  
  
## Creazione di una soluzione LINQ to SQL  
 In questa prima attività verrà creata una soluzione [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] che contiene i riferimenti necessari per compilare ed eseguire un progetto [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  
  
#### Per creare una soluzione LINQ to SQL  
  
1.  In [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] scegliere **Nuovo** dal menu **File**, quindi **Progetto**.  
  
2.  Nella finestra di dialogo **Nuovo progetto** selezionare **Visual C\#** nel riquadro **Tipi progetto**.  
  
3.  Nel riquadro **Modelli** fare clic su **Applicazione console**.  
  
4.  Nella casella **Nome** digitare LinqConsoleApp.  
  
5.  Nella casella **Percorso** verificare il percorso per l'archiviazione dei file di progetto.  
  
6.  Fare clic su **OK**.  
  
## Aggiunta di riferimenti e direttive LINQ  
 In questa procedura dettagliata vengono usati assembly che potrebbero non essere installati per impostazione predefinita nel progetto.  Se System.Data.Linq non viene elencato come riferimento nel progetto espandendo il nodo **Riferimenti** in **Esplora soluzioni**, aggiungerlo come spiegato nella procedura seguente.  
  
#### Per aggiungere System.Data.Linq  
  
1.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Riferimenti**, quindi scegliere **Aggiungi riferimento**.  
  
2.  Nella finestra di dialogo **Aggiungi riferimento** fare clic su **.NET**, fare clic sull'assembly System.Data.Linq, quindi scegliere **OK**.  
  
     L'assembly verrà aggiunto al progetto.  
  
3.  Aggiungere le seguenti direttive all'inizio di **Program.cs**:  
  
     [!code-csharp[DLinqWalk1CS#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk1CS/cs/Program.cs#1)]  
  
## Mapping di una classe a una tabella del database  
 In questo passaggio verrà creata una classe ed eseguito il mapping della classe a una tabella di database.  Tale classe è detta *classe di entità*.  Notare che il mapping viene eseguito semplicemente aggiungendo l'attributo <xref:System.Data.Linq.Mapping.TableAttribute>.  La proprietà <xref:System.Data.Linq.Mapping.TableAttribute.Name%2A> consente di specificare il nome della tabella nel database.  
  
#### Per creare una classe di entità ed eseguire il mapping della classe a una tabella di database  
  
-   Digitare o incollare il codice seguente in Program.cs immediatamente sopra la dichiarazione della classe `Program`:  
  
     [!code-csharp[DLinqWalk1CS#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk1CS/cs/Program.cs#2)]  
  
## Definizione di proprietà nella classe per rappresentare colonne del database  
 In questo passaggio si completeranno diverse attività.  
  
-   Usare l'attributo <xref:System.Data.Linq.Mapping.ColumnAttribute> per definire le proprietà `CustomerID` e `City` nella classe di entità in modo che rappresentino colonne nella tabella del database.  
  
-   Definire la proprietà `CustomerID` in modo che rappresenti una colonna di chiave primaria nel database.  
  
-   Definire i campi `_CustomerID` e `_City` per l'archiviazione privata.  [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] sarà quindi in grado di archiviare e recuperare direttamente i valori, anziché usare funzioni di accesso pubbliche che potrebbero includere la logica di business.  
  
#### Per rappresentare caratteristiche di due colonne del database  
  
-   Digitare o incollare il codice seguente in Program.cs all'interno delle parentesi graffe della classe `Customer`:  
  
     [!code-csharp[DLinqWalk1CS#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk1CS/cs/Program.cs#3)]  
  
## Definizione della connessione al database Northwind  
 In questo passaggio viene usato un oggetto <xref:System.Data.Linq.DataContext> per stabilire una connessione tra le strutture di dati basate sul codice e il database stesso.  <xref:System.Data.Linq.DataContext> è il canale principale tramite il quale vengono recuperati oggetti dal database e vengono inviate modifiche.  
  
 Viene anche dichiarato un oggetto `Table<Customer>` che fungerà da tabella tipizzata logica per le query sulla tabella Customers nel database.  Tali query verranno quindi create ed eseguite nei passaggi successivi.  
  
#### Per specificare la connessione al database  
  
-   Digitare o incollare il codice seguente nel metodo `Main`:  
  
     Si presuppone che il file `northwnd.mdf` si trovi nella cartella linqtest5.  Per altre informazioni, vedere la sezione precedente relativa ai prerequisiti.  
  
     [!code-csharp[DLinqWalk1CS#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk1CS/cs/Program.cs#4)]  
  
## Creazione di una query semplice  
 In questo passaggio viene creata una query per cercare i clienti nella tabella di database Customers residenti nell'area londinese.  Il codice della query in questo passaggio descrive semplicemente la query,  ma non la esegue.  Questo approccio è noto come *esecuzione posticipata*.  Per altre informazioni, vedere la sezione relativa alle [Introduction to LINQ Queries \(C\#\)](../Topic/Introduction%20to%20LINQ%20Queries%20\(C%23\).md).  
  
 Verrà anche prodotto un output del log per mostrare i comandi SQL generati da [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  Questa funzionalità di registrazione, che usa <xref:System.Data.Linq.DataContext.Log%2A>, è utile per eseguire il debug e per determinare che i comandi inviati al database rappresentano accuratamente la query.  
  
#### Per creare una query semplice  
  
-   Digitare o incollare il codice seguente nel metodo `Main` dopo la dichiarazione `Table<Customer>`.  
  
     [!code-csharp[DLinqWalk1ACS#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk1ACS/cs/Program.cs#5)]  
  
## Esecuzione della query  
 In questo passaggio verrà effettivamente eseguita la query.  Le espressioni di query create nei passaggi precedenti non vengono valutate finché i risultati non saranno necessari.  Quando si inizia l'iterazione `foreach`, viene eseguito un comando SQL sul database e gli oggetti vengono materializzati.  
  
#### Per eseguire la query  
  
1.  Digitare o incollare il codice seguente alla fine del metodo `Main` dopo la descrizione della query.  
  
     [!code-csharp[DLinqWalk1ACS#6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk1ACS/cs/Program.cs#6)]  
  
2.  ‎Premere F5 per eseguire il debug dell'applicazione.  
  
    > [!NOTE]
    >  Se l'applicazione genera un errore di run\-time, vedere la sezione Risoluzione dei problemi dell'articolo [Apprendimento tramite le procedure dettagliate](../../../../../../docs/framework/data/adonet/sql/linq/learning-by-walkthroughs.md).  
  
     I risultati della query nella finestra della console dovrebbero avere il seguente aspetto:  
  
     `ID=AROUT, City=London`  
  
     `ID=BSBEV, City=London`  
  
     `ID=CONSH, City=London`  
  
     `ID=EASTC, City=London`  
  
     `ID=NORTS, City=London`  
  
     `ID=SEVES, City=London`  
  
3.  Premere INVIO nella finestra della console per chiudere l'applicazione.  
  
## Passaggi successivi  
 L'argomento relativo alla [Procedura dettagliata: query tra relazioni \(C\#\)](../../../../../../docs/framework/data/adonet/sql/linq/walkthrough-querying-across-relationships-csharp.md) continua dal punto in cui termina questa procedura dettagliata.  In tale procedura dettagliata viene dimostrato come sia possibile eseguire una query tra tabelle in [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)], in modo analogo ai *join* in un database relazionale.  
  
 Se si desidera eseguire la procedura dettagliata relativa all'esecuzione di query tra relazioni, è indispensabile salvare la soluzione per la procedura dettagliata appena completata.  
  
## Vedere anche  
 [Apprendimento tramite le procedure dettagliate](../../../../../../docs/framework/data/adonet/sql/linq/learning-by-walkthroughs.md)