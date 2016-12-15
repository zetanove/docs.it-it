---
title: "How to: Find the Minimum or Maximum Value in a Query Result by Using LINQ (Visual Basic) | Microsoft Docs"
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
  - "max operator [LINQ in Visual Basic]"
  - "aggregate operator [LINQ in Visual Basic]"
  - "aggregate queries"
  - "minimum values [LINQ in Visual Basic]"
  - "min operator [LINQ in Visual Basic]"
  - "queries [LINQ in Visual Basic], minimum and maximum values"
  - "Max property"
  - "maximum values [LINQ in Visual Basic]"
  - "Aggregate clause"
  - "queries [LINQ in Visual Basic], aggregate queries"
  - "queries [LINQ in Visual Basic], how-to topics"
ms.assetid: 238b763b-7dcd-4b14-8050-b65500a4f71c
caps.latest.revision: 6
caps.handback.revision: 6
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Find the Minimum or Maximum Value in a Query Result by Using LINQ (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Language\-Integrated Query \(LINQ\) semplifica l'accesso a informazioni di database e l'esecuzione di query.  
  
 Nell'esempio seguente viene illustrato come creare una nuova applicazione che esegue query su un database SQL Server.  Nell'esempio vengono determinati i valori minimi e massimi per i risultati utilizzando le clausole `Aggregate` e `Group By` Per ulteriori informazioni, vedere [Aggregate Clause](../../../../visual-basic/language-reference/queries/aggregate-clause.md) e [Clausola Group By](../../../../visual-basic/language-reference/queries/group-by-clause.md).  
  
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
  
3.  Quando si aggiungono tabelle a Progettazione relazionale oggetti, la finestra di progettazione aggiunge un oggetto <xref:System.Data.Linq.DataContext> al progetto.  Questo oggetto contiene il codice necessario per accedere a tali tabelle, oltre che a singoli oggetti e raccolte per ogni tabella.  L'oggetto <xref:System.Data.Linq.DataContext> per il progetto viene denominato in base al nome del file .dbml.  Per questo progetto, l'oggetto <xref:System.Data.Linq.DataContext> viene denominato `northwindDataContext`.  
  
     È possibile creare un'istanza di <xref:System.Data.Linq.DataContext> nel codice ed eseguire una query nelle tabelle specificate da Progettazione relazionale oggetti.  
  
     Aggiungere il codice seguente all'evento `Load`.  Il codice esegue una query sulle tabelle esposte come proprietà del contesto dati e determina i valori minimi e massimi dei risultati.  Nell'esempio viene utilizzata la clausola `Aggregate` per eseguire una query per un solo risultato e la clausola `Group By` per visualizzare una media dei risultati raggruppati.  
  
     [!code-vb[VbLINQToSQLHowTos#14](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/how-to-find-the-minimum-or-maximum-value-in-a-query-result_1.vb)]  
  
4.  Premere F5 per eseguire il progetto e visualizzare i risultati.  
  
## Vedere anche  
 [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)   
 [Queries](../../../../visual-basic/language-reference/queries/queries.md)   
 [LINQ to SQL](../Topic/LINQ%20to%20SQL.md)   
 [Metodi DataContext \(Progettazione relazionale oggetti\)](/visual-studio/data-tools/datacontext-methods-o-r-designer)   
 [Procedura dettagliata: creazione di classi LINQ to SQL \(Progettazione relazionale oggetti\)](../Topic/Walkthrough:%20Creating%20LINQ%20to%20SQL%20Classes%20\(O-R%20Designer\).md)