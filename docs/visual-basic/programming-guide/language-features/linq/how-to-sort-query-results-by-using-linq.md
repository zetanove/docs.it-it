---
title: "How to: Sort Query Results by Using LINQ (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/14/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "sorting query results, multiple columns"
  - "sorting data [Visual Basic]"
  - "sorting data [LINQ in Visual Basic]"
  - "sorting query results [LINQ in Visual Basic]"
  - "queries [LINQ in Visual Basic], sorting results"
  - "querying databases [LINQ]"
  - "queries [LINQ in Visual Basic], how-to topics"
  - "query samples [Visual Basic]"
ms.assetid: 07a4584d-9fd8-4a1d-b7d9-ccf2efa5c84e
caps.latest.revision: 5
caps.handback.revision: 5
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Sort Query Results by Using LINQ (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Language\-Integrated Query \(LINQ\) semplifica l'accesso a informazioni di database e l'esecuzione di query.  
  
 Nell'esempio riportato di seguito viene illustrato come creare una nuova applicazione che esegue query su un database SQL Server e ordina i risultati in base a più campi utilizzando la clausola `Order By`.  L'ordinamento per ogni campo può essere in senso crescente o decrescente.  Per ulteriori informazioni, vedere [Order By Clause](../../../../visual-basic/language-reference/queries/order-by-clause.md).  
  
 Negli esempi di questo argomento viene utilizzato il database di esempio Northwind.  Se sul computer di sviluppo non è installato il database di esempio Northwind, è possibile scaricarlo da [Area download Microsoft](http://go.microsoft.com/fwlink/?LinkID=98088).  Per istruzioni, vedere [Download dei database di esempio](../Topic/Downloading%20Sample%20Databases.md).  
  
 [!INCLUDE[note_settings_general](../../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
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
  
     Aggiungere il codice seguente all'evento `Load` per eseguire una query nelle tabelle esposte come proprietà del contesto dati e ordinare i risultati.  La query ordina i risultati in base al numero di ordini del cliente, in ordine decrescente.  I clienti che hanno lo stesso numero di ordini vengono ordinati in senso crescente \(impostazione predefinita\) in base al nome di azienda.  
  
     [!code-vb[VbLINQToSQLHowTos#10](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/how-to-sort-query-results-by-using-linq_1.vb)]  
  
4.  Premere F5 per eseguire il progetto e visualizzare i risultati.  
  
## Vedere anche  
 [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)   
 [Queries](../../../../visual-basic/language-reference/queries/queries.md)   
 [LINQ to SQL](../Topic/LINQ%20to%20SQL.md)   
 [Metodi DataContext \(Progettazione relazionale oggetti\)](/visual-studio/data-tools/datacontext-methods-o-r-designer)   
 [Procedura dettagliata: creazione di classi LINQ to SQL \(Progettazione relazionale oggetti\)](../Topic/Walkthrough:%20Creating%20LINQ%20to%20SQL%20Classes%20\(O-R%20Designer\).md)