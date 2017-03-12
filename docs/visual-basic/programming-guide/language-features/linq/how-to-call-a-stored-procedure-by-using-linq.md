---
title: "How to: Call a Stored Procedure by Using LINQ (Visual Basic) | Microsoft Docs"
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
  - "queries [LINQ in Visual Basic], stored procedure calls"
  - "stored procedures sample [Visual Basic]"
  - "stored procedures [LINQ to SQL]"
  - "queries [LINQ in Visual Basic], how-to topics"
ms.assetid: 6436d384-d1e0-40aa-8afd-451007477260
caps.latest.revision: 12
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 12
---
# How to: Call a Stored Procedure by Using LINQ (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Language\-Integrated Query \(LINQ\) semplifica l'accesso alle informazioni del database, inclusi gli oggetti di database come le stored procedure.  
  
 Nell'esempio seguente viene illustrato come creare una applicazione che chiama una stored procedure in un database SQL Server.  Nell'esempio viene illustrato come chiamare due stored procedure diverse nel database.  Ogni procedura restituisce i risultati di una query.  Una procedura accetta parametri di input mentre l'altra procedura non accetta parametri.  
  
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
  
### Per aggiungere le stored procedure a Progettazione relazionale oggetti  
  
1.  In **Esplora server**\/**Esplora database** espandere la connessione al database Northwind.  Espandere la cartella **Stored Procedures**.  
  
     Se Progettazione relazionale oggetti è stato chiuso , è possibile riaprirlo facendo doppio clic sul file northwind.dbml aggiunto in precedenza.  
  
2.  Fare clic sullo stored procedure **Sales by Year** e trascinarlo nel riquadro di destra della finestra di progettazione.  Fare clic sullo stored procedure **Ten Most Expensive Products** e trascinarla nel riquadro di destra della finestra di progettazione.  
  
3.  Salvare le modifiche e chiudere le finestra di progettazione.  
  
4.  Salvare il progetto.  
  
### Per aggiungere il codice per visualizzare i risultati delle stored procedure  
  
1.  Dalla **Casella degli strumenti**, trascinare un controllo <xref:System.Windows.Forms.DataGridView> nel Windows Form predefinito per il progetto, Form1.  
  
2.  Fare doppio clic su Form1 per aggiungere il codice all'evento `Load`.  
  
3.  Quando si aggiungono stored procedure a Progettazione relazionale oggetti, la finestra di progettazione aggiunge un oggetto <xref:System.Data.Linq.DataContext> al progetto.  Questo oggetto contiene il codice necessario per accedere a tali procedure.  L'oggetto <xref:System.Data.Linq.DataContext> per il progetto viene denominato in base al nome del file .dbml.  Per questo progetto, l'oggetto <xref:System.Data.Linq.DataContext> viene denominato `northwindDataContext`.  
  
     È possibile creare un'istanza di <xref:System.Data.Linq.DataContext> nel codice e chiamare i metodi della stored procedure specificati da Progettazione relazionale oggetti.  Per eseguire l'associazione all'oggetto <xref:System.Windows.Forms.DataGridView> può essere necessario forzare la query all'esecuzione immediata chiamando il metodo <xref:System.Linq.Enumerable.ToList%2A> sui risultati della stored procedure.  
  
     Aggiungere il codice seguente all'evento `Load` per chiamare una qualsiasi delle stored procedure esposte come metodi per il contesto dati.  
  
     [!code-vb[VbLINQtoSQLHowTos#1](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/visualbasic/StoredProcedureHowTo/Form3.vb#1)]  
    [!code-vb[VbLINQtoSQLHowTos#2](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/visualbasic/StoredProcedureHowTo/Form3.vb#2)]  
  
4.  Premere F5 per eseguire il progetto e visualizzare i risultati.  
  
## Vedere anche  
 [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)   
 [Queries](../../../../visual-basic/language-reference/queries/queries.md)   
 [LINQ to SQL](../Topic/LINQ%20to%20SQL.md)   
 [Metodi DataContext \(Progettazione relazionale oggetti\)](/visual-studio/data-tools/datacontext-methods-o-r-designer)   
 [Procedura: assegnare stored procedure per l'esecuzione dei comandi di aggiornamento, inserimento ed eliminazione \(Progettazione relazionale oggetti\)](../Topic/How%20to:%20Assign%20stored%20procedures%20to%20perform%20updates,%20inserts,%20and%20deletes%20\(O-R%20Designer\).md)   
 [Procedura dettagliata: creazione di classi LINQ to SQL \(Progettazione relazionale oggetti\)](../Topic/Walkthrough:%20Creating%20LINQ%20to%20SQL%20Classes%20\(O-R%20Designer\).md)