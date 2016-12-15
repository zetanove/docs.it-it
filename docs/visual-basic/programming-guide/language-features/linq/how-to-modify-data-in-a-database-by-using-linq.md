---
title: "How to: Modify Data in a Database by Using LINQ (Visual Basic) | Microsoft Docs"
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
  - "inserting rows [LINQ to SQL]"
  - "deleting rows [LINQ to SQL]"
  - "updating rows [LINQ to SQL]"
  - "inserting data [Visual Basic]"
  - "deleting data"
  - "data [Visual Basic], updating"
  - "updating data [LINQ]"
  - "queries [LINQ in Visual Basic], data changes in database"
  - "queries [LINQ in Visual Basic], how-to topics"
ms.assetid: cf52635f-0c1b-46c3-aff1-bdf181cf19b1
caps.latest.revision: 15
caps.handback.revision: 15
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Modify Data in a Database by Using LINQ (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Language\-Integrated Query \(LINQ\) semplifica l'accesso alle informazioni di un database e la modifica dei valori presenti nel database.  
  
 Nell'esempio seguente viene illustrato come creare una nuova applicazione che recuperi e aggiorni le informazioni in un database SQL Server.  
  
 Negli esempi di questo argomento viene utilizzato il database di esempio Northwind.  Se sul computer di sviluppo non è installato il database di esempio Northwind, è possibile scaricarlo da [Area download Microsoft](http://go.microsoft.com/fwlink/?LinkID=98088).  Per istruzioni, vedere [Download dei database di esempio](../Topic/Downloading%20Sample%20Databases.md).  
  
### Per creare una connessione al database  
  
1.  In Visual Studio, aprire **Esplora server**\/**Esplora database** facendo clic sul menu **Visualizza** e poi selezionando **Esplora server**\/**Esplora database**.  
  
2.  In **Esplora server**\/**Esplora database** fare clic con il pulsante destro del mouse su **Connessioni dati** e scegliere **Aggiungi connessione**.  
  
3.  Specificare una connessione valida al database di esempio Northwind.  
  
### Per aggiungere un progetto con un file LINQ to SQL  
  
1.  Scegliere **Nuovo** dal menu **File** di Visual Studio, quindi **Progetto**.  Selezionare **Applicazione Windows Form** di Visual Basic come tipo di progetto.  
  
2.  Scegliere **Aggiungi nuovo elemento** dal menu **Progetto**.  Selezionare il modello dell'elemento **Classi LINQ to SQL**.  
  
3.  Denominare il file `northwind.dbml`.  Scegliere **Aggiungi**.  Viene aperto Progettazione relazionale oggetti per il file `northwind.dbml`.  
  
### Per aggiungere tabelle su cui eseguire una query e da modificare alla finestra di progettazione.  
  
1.  In **Esplora server**\/**Esplora database** espandere la connessione al database Northwind.  Espandere la cartella **Tabelle**.  
  
     Se Progettazione relazionale oggetti è stato chiuso, è possibile riaprirlo facendo doppio clic sul file `northwind.dbml` aggiunto in precedenza.  
  
2.  Fare clic sulla tabella Customers e, tenendo premuto il pulsante del mouse, trascinarla nel riquadro di sinistra del Designer.  
  
     La finestra di progettazione crea un nuovo oggetto Customers per il progetto.  
  
3.  Salvare le modifiche e chiudere le finestra di progettazione.  
  
4.  Salvare il progetto.  
  
### Per aggiungere il codice per modificare il database e visualizzare i risultati:  
  
1.  Dalla **Casella degli strumenti**, trascinare un controllo <xref:System.Windows.Forms.DataGridView> nel Windows Form predefinito per il progetto, Form1.  
  
2.  Quando si aggiungono tabelle a Progettazione relazionale oggetti, la finestra di progettazione aggiunge un oggetto <xref:System.Data.Linq.DataContext> al progetto.  Questo oggetto contiene il codice che è possibile utilizzare per accedere alla tabella Customers.  Contiene anche il codice che definisce un oggetto Customer locale e una raccolta Customers per la tabella.  L'oggetto <xref:System.Data.Linq.DataContext> per il progetto viene denominato in base al nome del file .dbml.  Per questo progetto, l'oggetto <xref:System.Data.Linq.DataContext> viene denominato `northwindDataContext`.  
  
     È possibile creare un'istanza dell'oggetto <xref:System.Data.Linq.DataContext> nel codice ed eseguire una query e modificare le raccolte Customers specificate da Progettazione relazionale oggetti.  Le modifiche apportate alla raccolta Customers non vengono riflesse nel database fino a che non vengono inviate chiamando il metodo <xref:System.Data.Linq.DataContext.SubmitChanges%2A> dell'oggetto <xref:System.Data.Linq.DataContext>.  
  
     Fare doppio clic su Windows Form, Form1 per aggiungere il codice all'evento <xref:System.Windows.Forms.Form.Load> per eseguire una query nella tabella Customers esposta come una proprietà di <xref:System.Data.Linq.DataContext>.  Aggiungere il codice riportato di seguito.  
  
    ```vb#  
    Private db As northwindDataContext  
  
    Private Sub Form1_Load(ByVal sender As System.Object,   
                           ByVal e As System.EventArgs  
                          ) Handles MyBase.Load  
      db = New northwindDataContext()  
  
      RefreshData()  
    End Sub  
  
    Private Sub RefreshData()  
      Dim customers = From cust In db.Customers   
                      Where cust.City(0) = "W"   
                      Select cust  
  
      DataGridView1.DataSource = customers  
    End Sub  
    ```  
  
3.  Da **Casella degli strumenti**, trascinare tre controlli <xref:System.Windows.Forms.Button> nel form.  Selezionare il primo controllo `Button`.  Nella finestra **Proprietà**, impostare `Name` del controllo `Button` a `AddButton` e `Text` a `Aggiungi`.  Selezionare il secondo pulsante e impostare la proprietà `Name` a `UpdateButton` e la proprietà `Text` a `Aggiorna`.  Selezionare il terzo pulsante e impostare la proprietà `Name` a `DeleteButton` e la proprietà `Text` a `Elimina`.  
  
4.  Fare doppio clic sul pulsante **Aggiungi** per aggiungere il codice al relativo evento `Click`.  Aggiungere il codice riportato di seguito.  
  
    ```vb#  
    Private Sub AddButton_Click(ByVal sender As System.Object,   
                                ByVal e As System.EventArgs  
                               ) Handles AddButton.Click  
      Dim cust As New Customer With {   
        .City = "Wellington",   
        .CompanyName = "Blue Yonder Airlines",   
        .ContactName = "Jill Frank",   
        .Country = "New Zealand",   
        .CustomerID = "JILLF"}  
  
      db.Customers.InsertOnSubmit(cust)  
  
      Try  
        db.SubmitChanges()  
      Catch  
        ' Handle exception.  
      End Try  
  
      RefreshData()  
    End Sub  
    ```  
  
5.  Fare doppio clic sul pulsante **Aggiorna** per aggiungere il codice al relativo evento `Click`.  Aggiungere il codice riportato di seguito.  
  
    ```vb#  
    Private Sub UpdateButton_Click(ByVal sender As System.Object, _  
                                   ByVal e As System.EventArgs  
                                  ) Handles UpdateButton.Click  
      Dim updateCust = (From cust In db.Customers   
                        Where cust.CustomerID = "JILLF").ToList()(0)  
  
      updateCust.ContactName = "Jill Shrader"  
  
      Try  
        db.SubmitChanges()  
      Catch  
        ' Handle exception.  
      End Try  
  
      RefreshData()  
    End Sub  
    ```  
  
6.  Fare doppio clic sul pulsante **Elimina** per aggiungere il codice al relativo evento `Click`.  Aggiungere il codice riportato di seguito.  
  
    ```vb#  
    Private Sub DeleteButton_Click(ByVal sender As System.Object, _  
                                   ByVal e As System.EventArgs  
                                  ) Handles DeleteButton.Click  
      Dim deleteCust = (From cust In db.Customers   
                        Where cust.CustomerID = "JILLF").ToList()(0)  
  
      db.Customers.DeleteOnSubmit(deleteCust)  
  
      Try  
        db.SubmitChanges()  
      Catch  
        ' Handle exception.  
      End Try  
  
      RefreshData()  
    End Sub  
    ```  
  
7.  Premere F5 per eseguire il progetto.  Fare clic su **Aggiungi** per aggiungere un nuovo record.  Fare clic su **Aggiorna** per modificare il nuovo record.  Fare clic su **Elimina** per cancellare il nuovo record.  
  
## Vedere anche  
 [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)   
 [Queries](../../../../visual-basic/language-reference/queries/queries.md)   
 [LINQ to SQL](../Topic/LINQ%20to%20SQL.md)   
 [Metodi DataContext \(Progettazione relazionale oggetti\)](/visual-studio/data-tools/datacontext-methods-o-r-designer)   
 [Procedura: assegnare stored procedure per l'esecuzione dei comandi di aggiornamento, inserimento ed eliminazione \(Progettazione relazionale oggetti\)](../Topic/How%20to:%20Assign%20stored%20procedures%20to%20perform%20updates,%20inserts,%20and%20deletes%20\(O-R%20Designer\).md)   
 [Procedura dettagliata: creazione di classi LINQ to SQL \(Progettazione relazionale oggetti\)](../Topic/Walkthrough:%20Creating%20LINQ%20to%20SQL%20Classes%20\(O-R%20Designer\).md)