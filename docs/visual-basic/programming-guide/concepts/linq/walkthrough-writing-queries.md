---
title: Scrittura di query in Visual Basic | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: get-started-article
dev_langs:
- VB
helpviewer_keywords:
- queries [LINQ in Visual Basic], writing
- LINQ [Visual Basic], walkthroughs
- LINQ [Visual Basic], writing queries
- writing LINQ queries [Visual Basic]
ms.assetid: f0045808-b9fe-4d31-88d1-473d9957211e
caps.latest.revision: 70
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: e870d5d0640c68fa57b07986f2bf8268fd5246c9
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-writing-queries-in-visual-basic"></a>Procedura dettagliata: Scrittura delle query in Visual Basic
Questa procedura dettagliata viene illustrato come è possibile utilizzare funzionalità del linguaggio Visual Basic per scrivere [!INCLUDE[vbteclinqext](../../../../csharp/getting-started/includes/vbteclinqext_md.md)] espressioni di query. La procedura dettagliata viene illustrato come creare query su un elenco di oggetti Student, come eseguire le query e come modificarli. Le query incorporano diverse funzionalità tra cui tipi anonimi, inferenza del tipo locale e gli inizializzatori di oggetto.  
  
 Dopo aver completato questa procedura dettagliata, sarà possibile passare agli esempi e documentazione per la specifica [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] provider si è interessati. [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]i provider includono [!INCLUDE[vbtecdlinq](../../../../csharp/includes/vbtecdlinq_md.md)], [!INCLUDE[linq_dataset](../../../../csharp/programming-guide/concepts/linq/includes/linq_dataset_md.md)], e [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)].  
  
## <a name="create-a-project"></a>Creare un progetto  
  
#### <a name="to-create-a-console-application-project"></a>Per creare un progetto applicazione console  
  
1.  Avviare Visual Studio.  
  
2.  Scegliere **Nuovo** dal menu **File**, quindi fare clic su **Progetto**.  
  
3.  Nel **modelli installati** elenco, fare clic su **Visual Basic**.  
  
4.  Nell'elenco dei tipi di progetto, fare clic su **applicazione Console**. Nel **nome** casella, digitare un nome per il progetto e quindi fare clic su **OK**.  
  
     Viene creato un progetto. Per impostazione predefinita, contiene un riferimento a System.Core.dll. Inoltre, il **spazi dei nomi importati** elenco il [pagina riferimenti, Progettazione progetti (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/references-page-project-designer-visual-basic) include il <xref:System.Linq?displayProperty=fullName>dello spazio dei nomi.</xref:System.Linq?displayProperty=fullName>  
  
5.  Nel [pagina Compila, Progettazione progetti (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/compile-page-project-designer-visual-basic), assicurarsi che **Option infer** è impostato su **su**.  
  
## <a name="add-an-in-memory-data-source"></a>Aggiungere un'origine dati In memoria  
 L'origine dati per le query in questa procedura dettagliata è un elenco di `Student` oggetti. Ogni `Student` oggetto contiene un nome, cognome, un anno di classe e un grado accademico del corpo studenti.  
  
#### <a name="to-add-the-data-source"></a>Per aggiungere l'origine dati  
  
-   Definire un `Student` classe e creare un elenco di istanze della classe.  
  
    > [!IMPORTANT]
    >  Il codice necessario per definire il `Student` classe e creare l'elenco utilizzato nella procedura dettagliata esempi viene fornito [procedura: creare un elenco di elementi](../../../../visual-basic/programming-guide/concepts/linq/how-to-create-a-list-of-items.md). È possibile copiarlo e incollarlo nel progetto. Il nuovo codice sostituisce il codice visualizzato al momento della creazione del progetto.  
  
#### <a name="to-add-a-new-student-to-the-students-list"></a>Per aggiungere un nuovo studente all'elenco di studenti  
  
-   Seguire il modello nel `getStudents` metodo per aggiungere un'altra istanza della `Student` classe all'elenco. Aggiunta dello studente verrà introdotti gli inizializzatori di oggetto. Per ulteriori informazioni, vedere [gli inizializzatori di oggetto: tipi denominati e anonimi](../../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md).  
  
## <a name="create-a-query"></a>Creare una query  
 Quando viene eseguito, la query è stato aggiunto in questa sezione produce un elenco di studenti il cui grado accademico li inserisce i primi dieci. Poiché la query seleziona l'intero `Student` oggetto ogni volta, il tipo del risultato della query è `IEnumerable(Of Student)`. Tuttavia, il tipo di query in genere non è specificato nelle definizioni di query. Al contrario, il compilatore utilizza l'inferenza del tipo locale per determinare il tipo. Per ulteriori informazioni, vedere [l'inferenza del tipo locale](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md). Variabile di intervallo della query, `currentStudent`, funge da riferimento a ogni `Student` istanza dell'origine, `students`, che fornisce accesso alle proprietà di ciascun oggetto `students`.  
  
#### <a name="to-create-a-simple-query"></a>Per creare una query semplice  
  
1.  Trovare la posizione di `Main` metodo del progetto che è contrassegnato come indicato di seguito:  
  
     [!code-vb[VbLINQWalkthrough n.&1;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/walkthrough-writing-queries_1.vb)]  
  
     Copiare il codice seguente e incollarlo in.  
  
     [!code-vb[VbLINQWalkthrough n.&2;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/walkthrough-writing-queries_2.vb)]  
  
2.  Posizionare il puntatore del mouse su `studentQuery` nel codice per verificare che il tipo assegnato dal compilatore è `IEnumerable(Of Student)`.  
  
## <a name="run-the-query"></a>Eseguire la Query  
 La variabile `studentQuery` contiene la definizione della query, non i risultati dell'esecuzione della query. Un meccanismo tipico per l'esecuzione di una query è un `For Each` ciclo. Ogni elemento della sequenza restituita è accessibile tramite la variabile di iterazione del ciclo. Per ulteriori informazioni sull'esecuzione delle query, vedere [scrittura la prima Query LINQ](../../../../visual-basic/programming-guide/concepts/linq/writing-your-first-linq-query.md).  
  
#### <a name="to-run-the-query"></a>Per eseguire la query  
  
1.  Aggiungere il codice seguente `For Each` ciclo sotto la query nel progetto.  
  
     [!code-vb[VbLINQWalkthrough n.&3;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/walkthrough-writing-queries_3.vb)]  
  
2.  Posizionare il puntatore del mouse sulla variabile di controllo del ciclo `studentRecord` per visualizzarne il tipo di dati. Il tipo di `studentRecord` viene dedotto come `Student`, in quanto `studentQuery` restituisce una raccolta di `Student` istanze.  
  
3.  Compilare ed eseguire l'applicazione premendo CTRL + F5. Si noti che i risultati nella finestra della console.  
  
## <a name="modify-the-query"></a>Modificare la Query  
 È più semplice analizzare i risultati della query se sono nell'ordine specificato. È possibile ordinare la sequenza restituita in base a qualsiasi campo disponibile.  
  
#### <a name="to-order-the-results"></a>Per ordinare i risultati  
  
1.  Aggiungere il codice seguente `Order By` clausola tra il `Where` istruzione e `Select` istruzione della query. Il `Order By` clausola ordina i risultati in ordine alfabetico da A Z, in base all'ultimo nome di ogni studente.  
  
    ```  
    Order By currentStudent.Last Ascending   
    ```  
  
2.  Per ordinare in base al cognome e poi al nome, aggiungere campi alla query:  
  
    ```  
    Order By currentStudent.Last Ascending, currentStudent.First Ascending   
    ```  
  
     È inoltre possibile specificare `Descending` all'ordine da Z ad A.  
  
3.  Compilare ed eseguire l'applicazione premendo CTRL + F5. Si noti che i risultati nella finestra della console.  
  
#### <a name="to-introduce-a-local-identifier"></a>Per introdurre un identificatore locale  
  
1.  Aggiungere il codice in questa sezione per introdurre un identificatore locale nell'espressione di query. L'identificatore locale conterrà un risultato intermedio. Nell'esempio seguente, `name` è un identificatore che contiene una concatenazione dello studente nome e cognome. Un identificatore locale può essere utilizzato per comodità, o può migliorare le prestazioni archiviando i risultati di un'espressione che altrimenti verrebbe calcolato più volte.  
  
     [!code-vb[VbLINQWalkthrough n.&4;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/walkthrough-writing-queries_4.vb)]  
  
2.  Compilare ed eseguire l'applicazione premendo CTRL + F5. Si noti che i risultati nella finestra della console.  
  
#### <a name="to-project-one-field-in-the-select-clause"></a>Per proiettare un campo nella clausola Select  
  
1.  Aggiungere la query e `For Each` ciclo in questa sezione per creare una query che produce una sequenza i cui elementi differiscono dagli elementi nell'origine. Nell'esempio seguente, l'origine è una raccolta di `Student` gli oggetti, ma solo un membro di ogni oggetto viene restituito: il nome degli studenti il cui cognome sia Garcia. Poiché `currentStudent.First` è una stringa, il tipo di dati della sequenza restituita da `studentQuery3` è `IEnumerable(Of String)`, una sequenza di stringhe. Come illustrato negli esempi precedenti, l'assegnazione dei dati di tipo per `studentQuery3` viene lasciato il compilatore può determinare tramite inferenza del tipo locale.  
  
     [!code-vb[VbLINQWalkthrough n.&5;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/walkthrough-writing-queries_5.vb)]  
  
2.  Posizionare il puntatore del mouse su `studentQuery3` nel codice per verificare che il tipo assegnato sia `IEnumerable(Of String)`.  
  
3.  Compilare ed eseguire l'applicazione premendo CTRL + F5. Si noti che i risultati nella finestra della console.  
  
#### <a name="to-create-an-anonymous-type-in-the-select-clause"></a>Per creare un tipo anonimo nella clausola Select  
  
1.  Aggiungere il codice in questa sezione per visualizzare i tipi anonimi come vengono utilizzate nelle query. Utilizzarli nelle query, quando si desidera restituire diversi campi dall'origine dati anziché record completi (`currentStudent` record negli esempi precedenti) o singoli campi (`First` nella sezione precedente). Anziché definire un nuovo tipo denominato che contiene i campi che si desidera includere nel risultato, specificare i campi di `Select` clausola e il compilatore crea un tipo anonimo con tali campi come proprietà. Per ulteriori informazioni, vedere [tipi anonimi](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md).  
  
     Nell'esempio seguente crea una query che restituisce il nome e il cui grado accademico sia compreso tra 1 e 10, in ordine di rango accademico dirigenti. In questo esempio, il tipo di `studentQuery4` deve essere dedotto, poiché il `Select` clausola restituisce un'istanza di un tipo anonimo, e un tipo anonimo non hanno nome utilizzabile.  
  
     [!code-vb[6 VbLINQWalkthrough](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/walkthrough-writing-queries_6.vb)]  
  
2.  Compilare ed eseguire l'applicazione premendo CTRL + F5. Si noti che i risultati nella finestra della console.  
  
## <a name="additional-examples"></a>Esempi aggiuntivi  
 Dopo aver appreso le nozioni di base, di seguito è un elenco di altri esempi per illustrare la flessibilità e potenza di [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] query. Ogni esempio è preceduto da una breve descrizione del risultato. Posizionare il puntatore del mouse sulla variabile di risultato di query per ogni query visualizzare il tipo derivato. Utilizzare un `For Each` ciclo per ottenere i risultati.  
  
 [!code-vb[VbLINQWalkthrough&#7;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/walkthrough-writing-queries_7.vb)]  
  
## <a name="additional-information"></a>Informazioni aggiuntive  
 Dopo aver acquisito familiarità con i concetti di base delle query, si è pronti per leggere la documentazione ed esempi per il tipo specifico di [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] provider che si è interessati:  
  
 [LINQ to Objects](http://msdn.microsoft.com/library/73cafe73-37cf-46e7-bfa7-97c7eea7ced9)  
  
 [LINQ to SQL](https://msdn.microsoft.com/library/bb386976)  
  
 [LINQ to XML](http://msdn.microsoft.com/library/f0fe21e9-ee43-4a55-b91a-0800e5782c13)  
  
 [LINQ to DataSet](http://msdn.microsoft.com/library/743e3755-3ecb-45a2-8d9b-9ed41f0dcf17)  
  
## <a name="see-also"></a>Vedere anche  
 [Language-Integrated Query (LINQ) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/index.md)   
 [Introduzione a LINQ in Visual Basic](../../../../visual-basic/programming-guide/concepts/linq/getting-started-with-linq.md)   
 [Inferenza del tipo locale](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [Inizializzatori di oggetto: Tipi denominati e anonimi](../../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)   
 [Tipi anonimi](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)   
 [Introduzione a LINQ in Visual Basic](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)   
 [Query](../../../../visual-basic/language-reference/queries/queries.md)
