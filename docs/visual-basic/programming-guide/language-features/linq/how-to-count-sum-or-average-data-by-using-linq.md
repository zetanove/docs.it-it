---
title: "How to: Count, Sum, or Average Data by Using LINQ (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "average operator [LINQ in Visual Basic]"
  - "aggregate operator [LINQ in Visual Basic]"
  - "aggregate queries"
  - "queries [LINQ in Visual Basic], sum results"
  - "Aggregate clause"
  - "sum operator [LINQ in Visual Basic]"
  - "queries [LINQ in Visual Basic], aggregate queries"
  - "queries [LINQ in Visual Basic], counting results"
  - "querying databases [LINQ]"
  - "queries [LINQ in Visual Basic], how-to topics"
  - "query samples [Visual Basic]"
  - "count operator [LINQ in Visual Basic]"
ms.assetid: 51ca1f59-7770-4884-8b76-113002e54fc0
caps.latest.revision: 9
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 9
---
# How to: Count, Sum, or Average Data by Using LINQ (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Language\-Integrated Query \(LINQ\) semplifica l'accesso a informazioni di database e l'esecuzione di query.  
  
 Nell'esempio seguente viene illustrato come creare una nuova applicazione che esegue query su un database SQL Server.  Nell'esempio vengono eseguiti il conteggio, la somma e la media dei risultati utilizzando le clausole `Aggregate` e `Group By` Per ulteriori informazioni, vedere [Aggregate Clause](../../../../visual-basic/language-reference/queries/aggregate-clause.md) e [Clausola Group By](../../../../visual-basic/language-reference/queries/group-by-clause.md).  
  
 Negli esempi di questo argomento viene utilizzato il database di esempio Northwind.  Se sul computer di sviluppo non è installato il database di esempio Northwind, è possibile scaricarlo da [Area download Microsoft](http://go.microsoft.com/fwlink/?LinkID=98088).  Per istruzioni, vedere [Download dei database di esempio](../Topic/Downloading%20Sample%20Databases.md).  
  
 [!INCLUDE[note_settings_general](../../../../csharp/language-reference/compiler-messages/includes/note-settings-general-md.md)]  
  
### Per creare una connessione al database  
  
1.  In Visual Studio, aprire **Esplora server**\/**Esplora database** scegliendo **Esplora server** o **Esplora database** dal menu **Visualizza**.  
  
2.  Fare clic con il pulsante destro del mouse su **Connessioni dati** in **Esplora server**\/**Esplora database** e quindi scegliere **Aggiungi connessione**.  
  
3.  Specificare una connessione valida al database di esempio Northwind.  
  
### Per aggiungere un progetto che contiene un file LINQ to SQL  
  
1.  Scegliere **Nuovo** dal menu **File** di Visual Studio, quindi **Progetto**.  Selezionare **Applicazione Windows Form** di Visual Basic come tipo di progetto.  
  
2.  Scegliere **Aggiungi nuovo elemento** dal menu **Progetto**.  Selezionare il modello dell'elemento **Classi LINQ to SQL**.  
  
3.  Denominare il file `northwind.dbml`.  Scegliere **Aggiungi**.  Viene aperto Progettazione relazionale oggetti per il file northwind.dbml.  
  
### Per aggiungere tabelle per eseguire una query a Progettazione relazionale oggetti  
  
1.  In **Esplora server**\/**Esplora database** espandere la connessione al database Northwind.  Espandere la cartella **Tabelle**.  
  
     Se Progettazione relazionale oggetti è stato chiuso , è possibile riaprirlo facendo doppio clic sul file northwind.dbml aggiunto in precedenza.  
  
2.  Fare clic sulla tabella Customers e, tenendo premuto il pulsante del mouse, trascinarla nel riquadro di sinistra del Designer.  Fare clic sulla tabella Orders e, tenendo premuto il pulsante del mouse, trascinarla nel riquadro di sinistra del Designer.  
  
     La finestra di progettazione crea nuovi oggetti `Customer` e `Order` per il progetto.  Si noti che la finestra di progettazione rileva automaticamente le relazioni tra le tabelle e crea le proprietà figlio per gli oggetti correlati.  Ad esempio, IntelliSense mostrerà che l'oggetto `Customer` ha una proprietà `Orders` per tutti gli ordini riferiti a quel cliente.  
  
3.  Salvare le modifiche e chiudere le finestra di progettazione.  
  
4.  Salvare il progetto.  
  
### Per aggiungere il codice per eseguire query sul database e visualizzare i risultati:  
  
1.  Dalla **Casella degli strumenti**, trascinare un controllo <xref:System.Windows.Forms.DataGridView> nel Windows Form predefinito per il progetto, Form1.  
  
2.  Fare doppio clic su Form1 per aggiungere il codice all'evento `Load` del form.  
  
3.  Quando si aggiungono tabelle a Progettazione relazionale oggetti, la finestra di progettazione aggiunge un oggetto <xref:System.Data.Linq.DataContext> al progetto.  Questo oggetto contiene il codice necessario per accedere a quelle tabelle e per accedere a singoli oggetti e a raccolte per ogni tabella.  L'oggetto <xref:System.Data.Linq.DataContext> per il progetto viene denominato in base al nome del file .dbml.  Per questo progetto, l'oggetto <xref:System.Data.Linq.DataContext> viene denominato `northwindDataContext`.  
  
     È possibile creare un'istanza di <xref:System.Data.Linq.DataContext> nel codice ed eseguire una query nelle tabelle specificate da Progettazione relazionale oggetti.  
  
     Aggiungere il seguente codice all'evento `Load` per eseguire una query nelle tabelle esposte come proprietà dell'oggetto <xref:System.Data.Linq.DataContext> ed eseguire il conteggio, la somma e la media dei risultati.  L'esempio utilizza la clausola `Aggregate` per eseguire una query per un solo risultato e la clausola `Group By` per visualizzare una media dei risultati raggruppati.  
  
     [!code-vb[VbLINQToSQLHowTos#13](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/how-to-count-sum-or-average-data-by-using-linq_1.vb)]  
  
4.  Premere F5 per eseguire il progetto e visualizzare i risultati.  
  
## Vedere anche  
 [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)   
 [Queries](../../../../visual-basic/language-reference/queries/queries.md)   
 [LINQ to SQL](../Topic/LINQ%20to%20SQL.md)   
 [Metodi DataContext \(Progettazione relazionale oggetti\)](/visual-studio/data-tools/datacontext-methods-o-r-designer)   
 [Procedura dettagliata: creazione di classi LINQ to SQL \(Progettazione relazionale oggetti\)](../Topic/Walkthrough:%20Creating%20LINQ%20to%20SQL%20Classes%20\(O-R%20Designer\).md)   
 [Aggregate Clause](../../../../visual-basic/language-reference/queries/aggregate-clause.md)   
 [Clausola Group By](../../../../visual-basic/language-reference/queries/group-by-clause.md)