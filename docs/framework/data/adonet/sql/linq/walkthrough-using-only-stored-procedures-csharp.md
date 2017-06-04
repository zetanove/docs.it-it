---
title: "Procedura dettagliata: utilizzo delle sole stored procedure (C#) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ecde4bf2-fa4d-4252-b5e4-96a46b9e097d
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Procedura dettagliata: utilizzo delle sole stored procedure (C#)
In questa procedura dettagliata viene descritto uno scenario [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] end\-to\-end di base per l'accesso ai dati eseguendo solo stored procedure.  Questo approccio viene spesso è usato dagli amministratori di database per limitare l'accesso all'archivio dati.  
  
> [!NOTE]
>  È inoltre possibile usare stored procedure nelle applicazioni [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] per eseguire l'override del comportamento predefinito, specialmente per i processi `Create`, `Update` e `Delete`.  Per altre informazioni, vedere [Personalizzazione delle operazioni Insert, Update e Delete](../../../../../../docs/framework/data/adonet/sql/linq/customizing-insert-update-and-delete-operations.md).  
  
 Per le finalità di questa procedura dettagliata si utilizzeranno due metodi di cui è stato eseguito il mapping alle stored procedure CustOrdersDetail e CustOrderHist nel database di esempio Northwind.  Il mapping viene applicato quando si esegue lo strumento della riga di comando SqlMetal per generare un file C\#.  Per altre informazioni, vedere la sezione successiva relativa ai prerequisiti.  
  
 Questa procedura dettagliata non si basa su [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)].  Gli sviluppatori che usano [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] possono inoltre usare [!INCLUDE[vs_ordesigner_short](../../../../../../includes/vs-ordesigner-short-md.md)] per implementare la funzionalità delle stored procedure.  Vedere [LINQ to SQL Tools in Visual Studio](../Topic/LINQ%20to%20SQL%20Tools%20in%20Visual%20Studio2.md).  
  
 [!INCLUDE[note_settings_general](../../../../../../includes/note-settings-general-md.md)]  
  
 Questa procedura è stata scritta usando Impostazioni di sviluppo di Visual C\#.  
  
## Prerequisiti  
 Per l'esecuzione di questa procedura sono richiesti i seguenti elementi:  
  
-   Per i file usati nella procedura dettagliata viene usata una cartella dedicata \("c:\\linqtest7"\).  Creare la cartella prima di avviare la procedura.  
  
-   Il database di esempio Northwind.  
  
     Se questo database non è disponibile nel computer di sviluppo, è possibile scaricarlo dal sito di download Microsoft.  Per istruzioni, vedere [Download dei database di esempio](../../../../../../docs/framework/data/adonet/sql/linq/downloading-sample-databases.md).  Dopo avere scaricato il database, copiare il file northwnd.mdf nella cartella c:\\linqtest7 .  
  
-   Un file di codice C\# generato dal database Northwind.  
  
     Questa procedura dettagliata è stata scritta usando lo strumento SqlMetal con la riga di comando seguente:  
  
     **sqlmetal \/code:"c:\\linqtest7\\northwind.cs" \/language:csharp "c:\\linqtest7\\northwnd.mdf" \/sprocs \/functions \/pluralize**  
  
     Per altre informazioni, vedere [SqlMetal.exe \(strumento per la generazione del codice\)](../../../../../../docs/framework/tools/sqlmetal-exe-code-generation-tool.md).  
  
## Panoramica  
 La procedura dettagliata è costituita da sei attività principali:  
  
-   Impostazione della soluzione [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] in [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)].  
  
-   Aggiunta dell'assembly System.Data.Linq al progetto.  
  
-   Aggiunta del file di codice del database al progetto.  
  
-   Creazione di una connessione con il database.  
  
-   Impostazione dell'interfaccia utente.  
  
-   Esecuzione e test dell'applicazione.  
  
## Creazione di una soluzione LINQ to SQL  
 In questa prima attività verrà creata una soluzione [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] che contiene i riferimenti necessari per compilare ed eseguire un progetto [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  
  
#### Per creare una soluzione LINQ to SQL  
  
1.  In [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] scegliere **Nuovo** dal menu **File**, quindi **Progetto**.  
  
2.  Nella finestra di dialogo **Nuovo progetto** selezionare **Visual C\#** nel riquadro **Tipi progetto**.  
  
3.  Nel riquadro **Modelli** scegliere **Applicazione Windows Form**.  
  
4.  Digitare SprocOnlyApp nella casella **Nome**.  
  
5.  Nella casella **Percorso** verificare il percorso per l'archiviazione dei file di progetto.  
  
6.  Fare clic su **OK**.  
  
     Verrà aperto Progettazione Windows Form.  
  
## Aggiunta del riferimento all'assembly LINQ to SQL  
 L'assembly [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] non è incluso nel modello Applicazione Windows Form standard.  Sarà pertanto necessario aggiungere l'assembly manualmente, come descritto nei passaggi seguenti:  
  
#### Per aggiungere System.Data.Linq.dll  
  
1.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Riferimenti**, quindi scegliere **Aggiungi riferimento**.  
  
2.  Nella finestra di dialogo **Aggiungi riferimento** fare clic su **.NET**, fare clic sull'assembly System.Data.Linq, quindi scegliere **OK**.  
  
     L'assembly verrà aggiunto al progetto.  
  
## Aggiunta del file di codice di Northwind al progetto  
 In questa procedura si presuppone che sia stato usato lo strumento SqlMetal per generare un file di codice dal database di esempio Northwind.  Per altre informazioni, vedere la sezione precedente relativa ai prerequisiti.  
  
#### Per aggiungere il file di codice di Northwind al progetto  
  
1.  Scegliere **Aggiungi elemento esistente** dal menu **Progetto**.  
  
2.  Nella finestra di dialogo **Aggiungi elemento esistente** passare a c:\\linqtest7\\northwind.cs, quindi fare clic su **Aggiungi**.  
  
     Il file northwind.cs viene aggiunto al progetto.  
  
## Creazione di connessioni a database  
 In questo passaggio si definirà la connessione al database di esempio Northwind.  Per questa procedura dettagliata viene usato il percorso "c:\\linqtest7\\northwnd.mdf".  
  
#### Per creare la connessione al database  
  
1.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Form1.cs**, quindi scegliere **Visualizza codice**.  
  
2.  Digitare il codice riportato di seguito nella classe `Form1`.  
  
     [!code-csharp[DLinqWalk4CS#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk4CS/cs/Form1.cs#1)]  
  
## Impostazione dell'interfaccia utente  
 In questa attività verrà impostata un'interfaccia per consentire agli utenti di eseguire stored procedure per l'accesso ai dati nel database.  Nelle applicazioni create con questa procedura dettagliata gli utenti potranno accedere ai dati nel database solo usando le stored procedure incorporate nell'applicazione.  
  
#### Per impostare l'interfaccia utente  
  
1.  Tornare a Progettazione Windows Form facendo clic su **Form1.cs\[Design\]**.  
  
2.  Scegliere **Casella degli strumenti** dal menu **Visualizza**.  
  
     Verrà aperta la Casella degli strumenti.  
  
    > [!NOTE]
    >  Fare clic sull'icona **Nascondi automaticamente** raffigurante una puntina da disegno per tenere aperta la Casella degli strumenti mentre si eseguono i passaggi rimanenti di questa sezione.  
  
3.  Trascinare due pulsanti, due caselle di testo e due etichette dalla casella degli strumenti in **Form1**.  
  
     Disporre i controlli come raffigurato nell'illustrazione.  Espandere **Form1** per consentire l'adattamento dei controlli.  
  
4.  Fare clic con il pulsante destro del mouse su **label1**, quindi scegliere **Proprietà**.  
  
5.  Modificare la proprietà **Text** da **label1** in **Enter OrderID:**.  
  
6.  Allo stesso modo per **label2** modificare la proprietà **Text** da **label2** in **Enter CustomerID:**.  
  
7.  Modificare inoltre la proprietà **Text** per **button1** in **Order Details**.  
  
8.  Modificare la proprietà **Text** per **button2** in **Order History**.  
  
     Ampliare i controlli pulsante in modo che tutto il testo sia visibile.  
  
#### Per gestire i clic sui pulsanti  
  
1.  Fare doppio clic su **Order Details** in **Form1** per aprire il gestore eventi button1 nell'editor di codice.  
  
2.  Digitare il codice riportato di seguito nel gestore eventi `button1`:  
  
     [!code-csharp[DLinqWalk4CS#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk4CS/cs/Form1.cs#2)]  
  
3.  Ora fare doppio clic **su button2** in **Form1** aprire il gestore `button2`  
  
4.  Digitare il codice riportato di seguito nel gestore eventi `button2`:  
  
     [!code-csharp[DLinqWalk4CS#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk4CS/cs/Form1.cs#3)]  
  
## Verifica dell'applicazione  
 A questo punto è possibile procedere al test dell'applicazione.  Notare che il contatto con l'archivio dati è limitato alle azioni supportate dalle due stored procedure  che, in questo caso, consistono nel restituire i prodotti inclusi per qualsiasi ID ordine immesso o nel restituire una cronologia dei prodotti ordinati per qualsiasi ID cliente immesso.  
  
#### Per eseguire il test dell'applicazione  
  
1.  Premere F5 per avviare il debug.  
  
     Viene visualizzato Form1.  
  
2.  Nella casella **Enter OrderID** digitare `10249`, quindi fare clic su **Order Details**.  
  
     I prodotti inclusi nell'ordine 10249 vengono elencati in una finestra di messaggio.  
  
     Scegliere **OK** per chiudere la finestra di messaggio.  
  
3.  Nella casella **Enter CustomerID** digitare `ALFKI`, quindi fare clic su **Order History**.  
  
     Viene visualizzata una finestra di messaggio con l'elenco della cronologia degli ordini per il cliente ALFKI.  
  
     Scegliere **OK** per chiudere la finestra di messaggio.  
  
4.  Nella casella **Enter OrderID** digitare `123`, quindi fare clic su **Order Details**.  
  
     Viene visualizzata una finestra di messaggio con l'indicazione che non è stato trovato alcun risultato.  
  
     Scegliere **OK** per chiudere la finestra di messaggio.  
  
5.  Scegliere **Termina debug** dal menu **Debug**.  
  
     La sessione di debug viene chiusa.  
  
6.  Al termine delle prove è possibile scegliere **Chiudi progetto** nel menu **File** e salvare il progetto quando viene richiesto.  
  
## Passaggi successivi  
 Questo progetto può essere migliorato apportandovi alcune modifiche.  Ad esempio, è possibile elencare le stored procedure disponibili in una casella di riepilogo, in modo che l'utente possa selezionare quella da eseguire.  È inoltre possibile trasmettere l'output dei rapporti a un file di testo.  
  
## Vedere anche  
 [Apprendimento tramite le procedure dettagliate](../../../../../../docs/framework/data/adonet/sql/linq/learning-by-walkthroughs.md)   
 [Stored procedure](../../../../../../docs/framework/data/adonet/sql/linq/stored-procedures.md)