---
title: "Procedura dettagliata: modifica dei dati (C#) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 24adfbe0-0ad6-449f-997d-8808e0770d2e
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Procedura dettagliata: modifica dei dati (C#)
In questa procedura dettagliata viene descritto uno scenario [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] end\-to\-end di base per l'aggiunta, la modifica e l'eliminazione dei dati in un database.  Si utilizzerà una copia del database di esempio Northwind per aggiungere un cliente, modificare il nome di un cliente ed eliminare un ordine.  
  
 [!INCLUDE[note_settings_general](../../../../../../includes/note-settings-general-md.md)]  
  
 Questa procedura è stata scritta usando Impostazioni di sviluppo di Visual C\#.  
  
## Prerequisiti  
 Per l'esecuzione di questa procedura sono richiesti i seguenti elementi:  
  
-   Una cartella dedicata \("c:\\linqtest6"\) in cui inserire i file usati nella procedura dettagliata.  Creare la cartella prima di avviare la procedura.  
  
-   Il database di esempio Northwind.  
  
     Se questo database non è disponibile nel computer di sviluppo, è possibile scaricarlo dal sito di download Microsoft.  Per istruzioni, vedere [Download dei database di esempio](../../../../../../docs/framework/data/adonet/sql/linq/downloading-sample-databases.md).  Dopo avere scaricato il database, copiare il file northwnd.mdf nella cartella c:\\linqtest6.  
  
-   Un file di codice C\# generato dal database Northwind.  
  
     È possibile generare questo file usando [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)] o lo strumento SQLMetal.  Questa procedura dettagliata è stata scritta usando lo strumento SQLMetal con la riga di comando seguente:  
  
     **sqlmetal \/code:"c:\\linqtest6\\northwind.cs" \/language:csharp "C:\\linqtest6\\northwnd.mdf" \/pluralize**  
  
     Per altre informazioni, vedere [SqlMetal.exe \(strumento per la generazione del codice\)](../../../../../../docs/framework/tools/sqlmetal-exe-code-generation-tool.md).  
  
## Panoramica  
 La procedura dettagliata è costituita da sei attività principali:  
  
-   Creazione della soluzione [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] in [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)].  
  
-   Aggiunta del file di codice del database al progetto.  
  
-   Creazione di un nuovo oggetto Customer  
  
-   Modifica del nome di contatto di un cliente.  
  
-   Eliminazione di un ordine.  
  
-   Invio delle modifiche al database Northwind.  
  
## Creazione di una soluzione LINQ to SQL  
 In questa prima attività verrà creata una soluzione [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] che contiene i riferimenti necessari per compilare ed eseguire un progetto [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  
  
#### Per creare una soluzione LINQ to SQL  
  
1.  In [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] scegliere **Nuovo** dal menu **File**, quindi **Progetto**.  
  
2.  Nella finestra di dialogo **Nuovo progetto** selezionare **Visual C\#** nel riquadro **Tipi progetto**.  
  
3.  Nel riquadro **Modelli** fare clic su **Applicazione console**.  
  
4.  Nella casella **Nome** digitare LinqDataManipulationApp.  
  
5.  Nella casella **Percorso** verificare il percorso per l'archiviazione dei file di progetto.  
  
6.  Fare clic su **OK**.  
  
## Aggiunta di riferimenti e direttive LINQ  
 In questa procedura dettagliata vengono usati assembly che potrebbero non essere installati per impostazione predefinita nel progetto.  Se System.Data.Linq non è elencato come un riferimento nel progetto, aggiungerlo seguendo le indicazioni fornite nei passaggi seguenti:  
  
#### Per aggiungere System.Data.Linq  
  
1.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse su **Riferimenti**, quindi scegliere **Aggiungi riferimento**.  
  
2.  Nella finestra di dialogo **Aggiungi riferimento** fare clic su **.NET**, fare clic sull'assembly System.Data.Linq, quindi scegliere **OK**.  
  
     L'assembly verrà aggiunto al progetto.  
  
3.  Aggiungere le seguenti direttive all'inizio di Program.cs:  
  
     [!code-csharp[DLinqWalk3CS#1](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk3CS/cs/Program.cs#1)]  
  
## Aggiunta del file di codice di Northwind al progetto  
 In questa procedura si presuppone che sia stato usato lo strumento SQLMetal per generare un file di codice dal database di esempio Northwind.  Per altre informazioni, vedere la sezione precedente relativa ai prerequisiti.  
  
#### Per aggiungere il file di codice di Northwind al progetto  
  
1.  Scegliere **Aggiungi elemento esistente** dal menu **Progetto**.  
  
2.  Nella finestra di dialogo **Aggiungi elemento esistente** individuare il file c:\\linqtest2\\northwind.vb, quindi fare clic su **Aggiungi**.  
  
     Il file northwind.cs viene aggiunto al progetto.  
  
## Impostazione della connessione al database  
 Eseguire innanzitutto il test della connessione al database.  Notare in particolare che nel nome del database, Northwnd, non è presente il carattere i.  Se vengono generati errori nei passaggi successivi, esaminare il file northwind.cs per determinare come è digitata la classe parziale Northwind.  
  
#### Per impostare e testare la connessione al database  
  
1.  Digitare o incollare il codice che segue nel metodo `Main` della classe Program:  
  
     [!code-csharp[DLinqWalk3CS#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk3CS/cs/Program.cs#2)]  
  
2.  A questo punto premere F5 per eseguire il test dell'applicazione.  
  
     Viene visualizzata una finestra **Console**.  
  
     È possibile chiudere l'applicazione premendo INVIO nella finestra **Console** o scegliendo **Termina debug** dal menu  **Debug** di [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)].  
  
## Creazione di una nuova entità  
 La creazione di una nuova entità è un processo semplice.  È possibile creare oggetti, ad esempio `Customer`, usando la parola chiave `new`.  
  
 In questa e nelle sezioni seguenti vengono apportate modifiche solo alla cache locale.  Non viene inviata alcuna modifica al database finché, verso la fine di questa procedura dettagliata, non si chiamerà <xref:System.Data.Linq.DataContext.SubmitChanges%2A>.  
  
#### Per aggiungere un nuovo oggetto dell'entità Customer  
  
1.  Creare un nuovo oggetto `Customer` aggiungendo il codice riportato di seguito prima di `Console.ReadLine();` nel metodo `Main`:  
  
     [!code-csharp[DLinqWalk3CS#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk3CS/cs/Program.cs#3)]  
  
2.  Premere F5 per eseguire il debug della soluzione.  
  
3.  Premere INVIO nella finestra **Console** per terminare il debug e continuare la procedura dettagliata.  
  
## Aggiornamento di un'entità  
 Nei passaggi seguenti si recupererà un oggetto `Customer` e si modificherà una delle relative proprietà.  
  
#### Per modificare il nome di un oggetto Customer  
  
-   Aggiungere il codice seguente sopra `Console.ReadLine();`:  
  
     [!code-csharp[DLinqWalk3CS#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk3CS/cs/Program.cs#4)]  
  
## Eliminazione di un'entità  
 Usando lo stesso oggetto Customer, è possibile eliminare il primo ordine.  
  
 Nel codice seguente viene illustrato come interrompere le relazioni tra le righe e come eliminare una riga dal database.  Aggiungere il codice seguente prima di `Console.ReadLine` per vedere come è possibile eliminare oggetti:  
  
#### Per eliminare una riga  
  
-   Aggiungere il codice seguente sopra `Console.ReadLine();`:  
  
     [!code-csharp[DLinqWalk3CS#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk3CS/cs/Program.cs#5)]  
  
## Invio di modifiche al database  
 Il passaggio finale necessario per la creazione, l'aggiornamento e l'eliminazione di oggetti consiste nell'inviare effettivamente le modifiche al database.  Senza questo passaggio le modifiche vengono applicate solo localmente e non saranno visualizzate nei risultati della query.  
  
#### Per inviare le modifiche al database  
  
1.  Inserire il codice seguente sopra `Console.ReadLine`:  
  
     [!code-csharp[DLinqWalk3CS#6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk3CS/cs/Program.cs#6)]  
  
2.  Inserire il codice seguente dopo `SubmitChanges` per mostrare gli effetti precedenti e successivi all'invio delle modifiche:  
  
     [!code-csharp[DLinqWalk3CS#7](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqWalk3CS/cs/Program.cs#7)]  
  
3.  Premere F5 per eseguire il debug della soluzione.  
  
4.  Premere INVIO nella finestra **Console** per chiudere l'applicazione.  
  
> [!NOTE]
>  Dopo avere aggiunto il nuovo oggetto Customer mediante l'invio delle modifiche, non sarà possibile eseguire nuovamente questa soluzione così com'è.  Per eseguire nuovamente la soluzione, modificare il nome del cliente e l'ID dell'oggetto Customer da aggiungere.  
  
## Vedere anche  
 [Apprendimento tramite le procedure dettagliate](../../../../../../docs/framework/data/adonet/sql/linq/learning-by-walkthroughs.md)