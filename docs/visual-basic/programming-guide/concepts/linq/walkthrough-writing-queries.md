---
title: "Procedura dettagliata: Scrittura delle query in Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "query [LINQ in Visual Basic], scrittura"
  - "LINQ [Visual Basic], procedure dettagliate"
  - "LINQ [Visual Basic], scrittura di query"
  - "Scrittura di query LINQ [Visual Basic]"
ms.assetid: f0045808-b9fe-4d31-88d1-473d9957211e
caps.latest.revision: 70
caps.handback.revision: 68
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Procedura dettagliata: Scrittura delle query in Visual Basic
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

In questa procedura viene descritto come utilizzare le funzionalità del linguaggio Visual Basic per scrivere espressioni di query [!INCLUDE[vbteclinqext](../../../../csharp/getting-started/includes/vbteclinqext_md.md)].  Nella procedura dettagliata viene illustrato come creare query su un elenco di oggetti Student, come eseguire le query e come modificarle.  Le query incorporano diverse funzionalità nuove di Visual Basic 2008, tra cui gli inizializzatori di oggetto, l'inferenza del tipo di variabile locale e i tipi anonimi.  
  
 Dopo avere completato questa procedura dettagliata sarà possibile passare agli esempi e alla documentazione per il provider [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] specifico desiderato.  I provider [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] includono [!INCLUDE[vbtecdlinq](../../../../csharp/includes/vbtecdlinq_md.md)], [!INCLUDE[linq_dataset](../../../../csharp/programming-guide/linq-query-expressions/includes/linq_dataset_md.md)] e [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)].  
  
## Creazione di un progetto  
  
#### Per creare un progetto di applicazione console  
  
1.  Avviare Visual Studio.  
  
2.  Scegliere **Nuovo** dal menu **File**, quindi fare clic su **Progetto**.  
  
3.  Nell'elenco **Modelli installati** fare clic su **Visual Basic**.  
  
4.  Nell'elenco di tipi di progetto fare clic su **Applicazione console**.  Nella casella **Nome** digitare un nome per il progetto, quindi scegliere **OK**.  
  
     Viene creato un progetto.  Per impostazione predefinita, contiene un riferimento a System.Core.dll.  Inoltre, nell'elenco **Spazi dei nomi importati** nella [Riferimenti \(pagina\), Creazione progetti \(Visual Basic\)](/visual-studio/ide/reference/references-page-project-designer-visual-basic) è incluso lo spazio dei nomi <xref:System.Linq?displayProperty=fullName>.  
  
5.  In [Compilazione \(pagina\), Creazione progetti \(Visual Basic\)](/visual-studio/ide/reference/compile-page-project-designer-visual-basic), assicurarsi che **Option Infer** è impostato su **In**.  
  
## Aggiunta di un'origine dati in memoria  
 L'origine dati per le query in questa procedura dettagliata è un elenco di oggetti `Student`.  Ogni oggetto `Student` contiene un nome, un cognome, un anno della classe e un grado accademico del corpo studenti.  
  
#### Per aggiungere l'origine dati  
  
-   Definire una classe `Student` e creare un elenco di istanze della classe.  
  
    > [!IMPORTANT]
    >  Il codice necessario per definire la classe `Student` e creare l'elenco utilizzato negli esempi della procedura dettagliata viene fornito in [How to: Create a List of Items](../../../../visual-basic/programming-guide/concepts/linq/how-to-create-a-list-of-items.md).  È possibile copiarlo e incollarlo nel progetto.  Il codice nuovo sostituisce il codice visualizzato al momento della creazione del progetto.  
  
#### Per aggiungere un nuovo studente all'elenco di studenti  
  
-   Seguire il modello nel metodo `getStudents` per aggiungere un'altra istanza della classe `Student` all'elenco.  Con l'aggiunta dello studente vengono introdotti gli inizializzatori di oggetto.  Per ulteriori informazioni, vedere [Object Initializers: Named and Anonymous Types](../../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md).  
  
## Creazione di una query  
 Quando viene eseguita, la query aggiunta in questa sezione genera un elenco di studenti il cui grado accademico li inserisce tra i primi dieci.  Poiché la query seleziona ogni volta l'intero oggetto `Student`, il tipo del risultato della query è `IEnumerable(Of Student)`.  Tuttavia, il tipo della query non viene generalmente specificato nelle definizioni della query.  Il compilatore utilizza invece l'inferenza del tipo di variabile locale per determinare il tipo.  Per ulteriori informazioni, vedere [Local Type Inference](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md).  La variabile di intervallo della query, `currentStudent`, funge da riferimento a ogni istanza `Student` nell'origine, `students`, fornendo l'accesso alle proprietà di ogni oggetto in `students`.  
  
#### Per creare una query semplice  
  
1.  Individuare il punto nel metodo `Main` del progetto contrassegnato come segue:  
  
     [!code-vb[VbLINQWalkthrough#1](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/walkthrough-writing-queries_1.vb)]  
  
     Copiare il seguente codice e incollarlo.  
  
     [!code-vb[VbLINQWalkthrough#2](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/walkthrough-writing-queries_2.vb)]  
  
2.  Posizionare il puntatore del mouse su `studentQuery` nel codice per verificare che il tipo assegnato dal compilatore sia `IEnumerable(Of Student)`.  
  
## Esecuzione della query  
 La variabile `studentQuery` contiene la definizione della query, non i risultati dell'esecuzione della query.  Un meccanismo tipico per l'esecuzione di una query è il ciclo `For Each`.  È possibile accedere a ogni elemento nella sequenza restituita mediante la variabile di iterazione del ciclo.  Per ulteriori informazioni sull'esecuzione delle query, vedere [Scrittura della prima query LINQ](../../../../visual-basic/programming-guide/concepts/linq/writing-your-first-linq-query.md).  
  
#### Per eseguire la query  
  
1.  Aggiungere il seguente ciclo `For Each` sotto la query all'interno del progetto.  
  
     [!code-vb[VbLINQWalkthrough#3](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/walkthrough-writing-queries_3.vb)]  
  
2.  Posizionare il puntatore del mouse sulla variabile di controllo del ciclo `studentRecord` per visualizzarne il tipo di dati.  Si deduce che il tipo di `studentRecord` sia `Student`, poiché `studentQuery` restituisce una raccolta di istanze `Student`.  
  
3.  Compilare ed eseguire l'applicazione premendo CTRL\+F5.  Osservare i risultati nella finestra della console.  
  
## Modifica della query  
 È più semplice analizzare i risultati della query se vengono disposti in un determinato ordine.  È possibile ordinare la sequenza restituita in base a qualsiasi campo disponibile.  
  
#### Per ordinare i risultati  
  
1.  Aggiungere la seguente clausola `Order By` tra l'istruzione `Where` e l'istruzione `Select` della query.  La clausola `Order By` ordina i risultati alfabeticamente dalla A alla Z in base al cognome di ogni studente.  
  
    ```  
    Order By currentStudent.Last Ascending   
    ```  
  
2.  Per ordinare in base al cognome e poi al nome, aggiungere entrambi i campi alla query:  
  
    ```  
    Order By currentStudent.Last Ascending, currentStudent.First Ascending   
    ```  
  
     È inoltre possibile specificare `Descending` per ordinare dalla Z alla A.  
  
3.  Compilare ed eseguire l'applicazione premendo CTRL\+F5.  Osservare i risultati nella finestra della console.  
  
#### Per introdurre un identificatore locale  
  
1.  Aggiungere il codice in questa sezione per introdurre un identificatore locale nell'espressione di query.  L'identificatore locale conterrà un risultato intermedio.  Nell'esempio seguente `name` è un identificatore che contiene una concatenazione del nome e cognome dello studente.  È possibile utilizzare un identificatore locale per motivi di praticità o perché migliora le prestazioni archiviando i risultati di un'espressione in modo da non doverla calcolare più volte.  
  
     [!code-vb[VbLINQWalkthrough#4](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/walkthrough-writing-queries_4.vb)]  
  
2.  Compilare ed eseguire l'applicazione premendo CTRL\+F5.  Osservare i risultati nella finestra della console.  
  
#### Per proiettare un campo nella clausola Select  
  
1.  Aggiungere la query e il ciclo `For Each` da questa sezione per creare una query che generi una sequenza i cui elementi differiscono dagli elementi presenti nell'origine.  Nell'esempio seguente l'origine è una raccolta di oggetti `Student`, ma viene restituito solo un membro di ogni oggetto: il nome degli studenti il cui cognome sia Garcia.  Poiché `currentStudent.First` è una stringa, il tipo di dati della sequenza restituita da `studentQuery3` è `IEnumerable(Of String)`, una sequenza di stringhe.  Come negli esempi precedenti, il compilatore effettua l'assegnazione del tipo di dati per `studentQuery3` utilizzando l'inferenza del tipo di variabile locale.  
  
     [!code-vb[VbLINQWalkthrough#5](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/walkthrough-writing-queries_5.vb)]  
  
2.  Posizionare il puntatore del mouse su `studentQuery3` nel codice per verificare che il tipo assegnato sia `IEnumerable(Of String)`.  
  
3.  Compilare ed eseguire l'applicazione premendo CTRL\+F5.  Osservare i risultati nella finestra della console.  
  
#### Per creare un tipo anonimo nella clausola Select  
  
1.  Aggiungere il codice da questa sezione per vedere come vengono utilizzati i tipi anonimi nelle query.  Vengono utilizzati nelle query per restituire diversi campi dall'origine dati anziché record completi \(i record `currentStudent` negli esempi precedenti\) o singoli campi \(`First` nella sezione precedente\).  Anziché definire un nuovo tipo denominato contenente i campi da includere nel risultato, specificare i campi nella clausola di `Select` e il compilatore crea un tipo anonimo con tali campi come proprietà. Per ulteriori informazioni, vedere [Anonymous Types](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md).  
  
     Nell'esempio seguente viene creata una query che restituisce il nome e il grado di studenti senior il cui grado accademico sia compreso tra 1 e 10.  In questo esempio il tipo di `studentQuery4` deve essere dedotto, poiché la clausola `Select` restituisce un'istanza di un tipo anonimo e i tipi anonimi non hanno un nome utilizzabile.  
  
     [!code-vb[VbLINQWalkthrough#6](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/walkthrough-writing-queries_6.vb)]  
  
2.  Compilare ed eseguire l'applicazione premendo CTRL\+F5.  Osservare i risultati nella finestra della console.  
  
## Esempi aggiuntivi  
 Una volta apprese le nozioni di base, è possibile esaminare l'elenco di esempi aggiuntivi riportato di seguito per comprendere la flessibilità e la potenza delle query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)].  Ogni esempio è preceduto da una breve descrizione della relativa funzione.  Posizionare il puntatore del mouse sulla variabile del risultato di ciascuna query per visualizzare il tipo derivato. Utilizzare un ciclo di `For Each` per generare i risultati.  
  
 [!code-vb[VbLINQWalkthrough#7](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/walkthrough-writing-queries_7.vb)]  
  
## Informazioni aggiuntive  
 Dopo aver acquisito dimestichezza con i concetti di base relativi all'utilizzo delle query, è possibile leggere la documentazione e gli esempi per il tipo specifico di provider [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] desiderato:  
  
 [LINQ to Objects](../../../../visual-basic/programming-guide/concepts/linq/linq-to-objects.md)  
  
 [LINQ to SQL](../Topic/LINQ%20to%20SQL.md)  
  
 [LINQ to XML](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml.md)  
  
 [LINQ to DataSet](../Topic/LINQ%20to%20DataSet.md)  
  
## Vedere anche  
 [LINQ \(Language\-Integrated Query\)](../Topic/LINQ%20\(Language-Integrated%20Query\).md)   
 [Getting Started with LINQ in Visual Basic](../../../../visual-basic/programming-guide/concepts/linq/getting-started-with-linq.md)   
 [Supplementary LINQ Resources](../Topic/Supplementary%20LINQ%20Resources.md)   
 [Local Type Inference](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [Object Initializers: Named and Anonymous Types](../../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)   
 [Anonymous Types](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)   
 [Introduction to LINQ in Visual Basic](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)   
 [Queries](../../../../visual-basic/language-reference/queries/queries.md)   
 [Walkthrough: Writing Queries in C\#](../../../../csharp/programming-guide/concepts/linq/walkthrough-writing-queries-linq.md)