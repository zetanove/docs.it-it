---
title: 'Procedura: restituire un risultato di Query LINQ come tipo specifico (Visual Basic) | Documenti di Microsoft'
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
- queries [LINQ in Visual Basic], specific type returned
- projection [LINQ in Visual Basic]
- anonymous types [Visual Basic]
- querying databases [LINQ]
- queries [LINQ in Visual Basic], how-to topics
- query samples [Visual Basic]
ms.assetid: 621bb10a-e5d7-44fb-a025-317964b19d92
caps.latest.revision: 8
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
ms.openlocfilehash: 2031e24ca0fe5aa86ca6c0bcd0e0e4f27238c8ae
ms.contentlocale: it-it
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-return-a-linq-query-result-as-a-specific-type-visual-basic"></a>Procedura: restituire un risultato di query LINQ come tipo specifico (Visual Basic)
Language-Integrated Query (LINQ) semplifica accedere alle informazioni di database ed eseguire query. Per impostazione predefinita, le query LINQ restituiscono un elenco di oggetti come un tipo anonimo. È inoltre possibile specificare che la query restituisca un elenco di un tipo specifico utilizzando il `Select` clausola.  
  
 Nell'esempio seguente viene illustrato come creare una nuova applicazione che esegue query su un database di SQL Server e vengono proiettati i risultati come un tipo denominato specifico. Per ulteriori informazioni, vedere [tipi anonimi](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md) e [clausola Select](../../../../visual-basic/language-reference/queries/select-clause.md).  
  
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
  
### <a name="to-add-tables-to-query-to-the-or-designer"></a>Per aggiungere le tabelle di eseguire query O/R Designer  
  
1.  In **Esplora Server**/**Esplora Database**, espandere la connessione al database Northwind. Espandere il **tabelle** cartella.  
  
     Se è stato chiuso O/R Designer, è possibile riaprirlo facendo doppio clic sul file Northwind. dbml aggiunto in precedenza.  
  
2.  Fare clic sulla tabella Customers e trascinarlo nel riquadro sinistro della finestra di progettazione.  
  
     La finestra di progettazione crea un nuovo `Customer` oggetto per il progetto. È possibile progettare un risultato della query come la `Customer` tipo o come un tipo creato. In questo esempio crea un nuovo tipo in una procedura successiva e il risultato della query come tipo di progetto.  
  
3.  Salvare le modifiche e chiudere la finestra di progettazione.  
  
4.  Salvare il progetto.  
  
### <a name="to-add-code-to-query-the-database-and-display-the-results"></a>Per aggiungere codice per eseguire query sul database e visualizzare i risultati  
  
1.  Dal **della casella degli strumenti**, trascinare un <xref:System.Windows.Forms.DataGridView>controllo nel Form di Windows predefinito per il progetto, Form1.</xref:System.Windows.Forms.DataGridView>  
  
2.  Fare doppio clic su Form1 per modificare la classe Form1.  
  
3.  Dopo il `End Class` istruzione della classe Form1, aggiungere il codice seguente per creare un `CustomerInfo` tipo per contenere i risultati della query per questo esempio.  
  
     [!code-vb[VbLINQToSQLHowTos&#16;](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/how-to-return-a-linq-query-result-as-a-specific-type_1.vb)]  
  
4.  Quando si aggiungono tabelle alla finestra di Progettazione relazionale, la finestra di progettazione aggiunge un <xref:System.Data.Linq.DataContext>oggetto al progetto.</xref:System.Data.Linq.DataContext> Questo oggetto contiene il codice che è necessario disporre per accedere a tali tabelle e accedere ai singoli oggetti e raccolte per ogni tabella. Il <xref:System.Data.Linq.DataContext>oggetto per il progetto viene denominato in base al nome del file. dbml.</xref:System.Data.Linq.DataContext> Per questo progetto, il <xref:System.Data.Linq.DataContext>oggetto è denominato `northwindDataContext`.</xref:System.Data.Linq.DataContext>  
  
     È possibile creare un'istanza di <xref:System.Data.Linq.DataContext>nel codice e query nelle tabelle specificate da O/R Designer.</xref:System.Data.Linq.DataContext>  
  
     Nel `Load` evento della classe Form1, aggiungere il codice seguente per eseguire query su tabelle che sono esposte come proprietà del contesto dati. Il `Select` clausola della query verrà creato un nuovo `CustomerInfo` tipo anziché un tipo anonimo per ogni elemento del risultato della query.  
  
     [!code-vb[VbLINQToSQLHowTos&#15;](../../../../visual-basic/programming-guide/language-features/linq/codesnippet/VisualBasic/how-to-return-a-linq-query-result-as-a-specific-type_2.vb)]  
  
5.  Premere F5 per eseguire il progetto e visualizzare i risultati.  
  
## <a name="see-also"></a>Vedere anche  
 [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)   
 [Query](../../../../visual-basic/language-reference/queries/queries.md)   
 [LINQ to SQL](https://msdn.microsoft.com/library/bb386976)   
 [Metodi DataContext (O/R Designer)](https://docs.microsoft.com/visualstudio/data-tools/datacontext-methods-o-r-designer)

