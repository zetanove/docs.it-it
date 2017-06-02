---
title: 'Procedura: chiamare una Stored Procedure utilizzando LINQ (Visual Basic) | Documenti di Microsoft'
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- queries [LINQ in Visual Basic], stored procedure calls
- stored procedures sample [Visual Basic]
- stored procedures [LINQ to SQL]
- queries [LINQ in Visual Basic], how-to topics
ms.assetid: 6436d384-d1e0-40aa-8afd-451007477260
caps.latest.revision: 12
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
ms.translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: abc3970fc5ab6f4a2f4b67b5efa2b19afb07337b
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-call-a-stored-procedure-by-using-linq-visual-basic"></a>Procedura: chiamare una stored procedure utilizzando LINQ (Visual Basic)
Language-Integrated Query (LINQ) consente di accedere alle informazioni di database, inclusi oggetti quali stored procedure di database.  
  
 Nell'esempio seguente viene illustrato come creare un'applicazione che chiama una stored procedure in un database di SQL Server. Nell'esempio viene illustrato come chiamare due diverse stored procedure nel database. Ogni procedura restituisce i risultati di una query. Una procedura accetta parametri di input e l'altra procedura non accetta parametri.  
  
 Gli esempi in questo argomento usano il database di esempio Northwind. Se si dispone di esempio Northwind nel computer di sviluppo, è possibile scaricarlo dal [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkID=98088) sito Web. Per istruzioni, vedere [download dei database di esempio](https://msdn.microsoft.com/library/bb399411).  
  
[!INCLUDE[note_settings_general](~/includes/note-settings-general-md.md)]  
  
### <a name="to-create-a-connection-to-a-database"></a>Per creare una connessione a un database  
  
1.  In Visual Studio, aprire **Esplora Server**/**Esplora Database** facendo **Esplora Server**/**Esplora Database** sul **visualizzazione** menu.  
  
2.  Fare doppio clic su **connessioni dati** in **Esplora Server**/**Esplora Database** e quindi fare clic su **Aggiungi connessione**.  
  
3.  Specificare una connessione valida al database di esempio Northwind.  
  
### <a name="to-add-a-project-that-contains-a-linq-to-sql-file"></a>Per aggiungere un progetto che contiene un file LINQ to SQL  
  
1.  In Visual Studio, nel **File** dal menu **New** e quindi fare clic su **progetto**. Selezionare Visual Basic **applicazione Windows Form** come tipo di progetto.  
  
2.  Nel menu **Progetto** fare clic su **Aggiungi nuovo elemento**. Selezionare il **classi LINQ to SQL** modello di elemento.  
  
3.  Nome del file `northwind.dbml`. Fare clic su **Aggiungi**. Per il file Northwind. dbml viene aperta la Object Relational Designer (O/R Designer).  
  
### <a name="to-add-stored-procedures-to-the-or-designer"></a>Per aggiungere stored procedure a O/R Designer  
  
1.  In **Esplora Server**/**Esplora Database**, espandere la connessione al database Northwind. Espandere il **Stored procedure** cartella.  
  
     Se è stato chiuso O/R Designer, è possibile riaprirlo facendo doppio clic sul file Northwind. dbml aggiunto in precedenza.  
  
2.  Fare clic su di **Sales by Year** stored procedure e trascinarlo nel riquadro a destra della finestra di progettazione. Fare clic su di **Ten Most Expensive Products** stored procedure trascinarlo nel riquadro a destra della finestra di progettazione.  
  
3.  Salvare le modifiche e chiudere la finestra di progettazione.  
  
4.  Salvare il progetto.  
  
### <a name="to-add-code-to-display-the-results-of-the-stored-procedures"></a>Per aggiungere il codice per visualizzare i risultati delle stored procedure  
  
1.  Dal **della casella degli strumenti**, trascinare un <xref:System.Windows.Forms.DataGridView>controllo nel Form di Windows predefinito per il progetto, Form1.</xref:System.Windows.Forms.DataGridView>  
  
2.  Fare doppio clic su Form1 per aggiungere codice al relativo `Load` evento.  
  
3.  Quando si aggiungono stored procedure per la Progettazione relazionale oggetti, la finestra di progettazione aggiunge un <xref:System.Data.Linq.DataContext>oggetto per il progetto.</xref:System.Data.Linq.DataContext> Questo oggetto contiene il codice che è necessario disporre per accedere a tali procedure. Il <xref:System.Data.Linq.DataContext>oggetto per il progetto viene denominato in base al nome del file. dbml.</xref:System.Data.Linq.DataContext> Per questo progetto, il <xref:System.Data.Linq.DataContext>oggetto è denominato `northwindDataContext`.</xref:System.Data.Linq.DataContext>  
  
     È possibile creare un'istanza di <xref:System.Data.Linq.DataContext>nel codice e chiamare i metodi della stored procedure specificato da O/R Designer.</xref:System.Data.Linq.DataContext> Per associare il <xref:System.Windows.Forms.DataGridView>dell'oggetto, potrebbe essere necessario forzare la query per eseguire immediatamente la chiamata il <xref:System.Linq.Enumerable.ToList%2A>metodo sui risultati della stored procedure.</xref:System.Linq.Enumerable.ToList%2A> </xref:System.Windows.Forms.DataGridView>  
  
     Aggiungere il codice seguente per il `Load` eventi per chiamare una qualsiasi delle stored procedure esposte come metodi per il contesto dati.  
  
     [!code-vb[VbLINQtoSQLHowTos n.&1;](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/how-to-call-a-stored-procedure-by-using-linq_1.vb)]  
    [!code-vb[VbLINQtoSQLHowTos n.&2;](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/how-to-call-a-stored-procedure-by-using-linq_2.vb)]  
  
4.  Premere F5 per eseguire il progetto e visualizzare i risultati.  
  
## <a name="see-also"></a>Vedere anche  
 [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)   
 [Query](../../../../visual-basic/language-reference/queries/queries.md)   
 [LINQ to SQL](https://msdn.microsoft.com/library/bb386976)   
 [Metodi DataContext (O/R Designer)](https://docs.microsoft.com/visualstudio/data-tools/datacontext-methods-o-r-designer)   
 [Procedura: assegnare stored procedure per eseguire aggiornamenti, inserimenti ed eliminazioni (O/R Designer)](http://msdn.microsoft.com/library/e88224ab-ff61-4a3a-b6b8-6f3694546cac)

