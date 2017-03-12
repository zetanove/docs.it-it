---
title: "Walkthrough: Writing Queries in C# (LINQ) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-csharp"
ms.topic: "get-started-article"
dev_langs: 
  - "CSharp"
helpviewer_keywords: 
  - "LINQ [C#], walkthroughs"
  - "LINQ [C#], writing queries"
  - "queries [LINQ in C#], writing"
  - "writing LINQ queries"
ms.assetid: 2962a610-419a-4276-9ec8-4b7f2af0c081
caps.latest.revision: 32
author: "BillWagner"
ms.author: "wiwagn"
caps.handback.revision: 30
---
# Walkthrough: Writing Queries in C# (LINQ)
In questa procedura guidata vengono illustrate le funzionalità del linguaggio C\# utilizzate per scrivere espressioni di query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)].  Dopo avere completato questa procedura dettagliata sarà possibile passare agli esempi e alla documentazione per il provider [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] specifico desiderato, ad esempio [!INCLUDE[vbtecdlinq](../../../../csharp/includes/vbtecdlinq-md.md)], [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] to DataSets o [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq-md.md)].  
  
## Prerequisiti  
 In questa procedura dettagliata richiede le funzionalità introdotte in Visual Studio 2008.  
  
 ![Collegamento a video](../../../../csharp/programming-guide/concepts/linq/media/playvideo.png "PlayVideo") Per una versione video di questo argomento, vedere [Procedura relativa a contenuti video: scrittura di query in C\# \(LINQ\)](http://go.microsoft.com/fwlink/?LinkId=100393) \(informazioni in lingua inglese\).  
  
## Creazione di un progetto C\#  
  
#### Per creare un progetto  
  
1.  Avviare Visual Studio.  
  
2.  Nella barra del menu, scegliere **File**, **Nuovo**, **Progetto**.  
  
     Verrà visualizzata la finestra di dialogo **Nuovo progetto**.  
  
3.  Espandere **Installato**, espandere **Modelli**, espandere **Visual C\#**e quindi scegliere **Applicazione console**.  
  
4.  Nella casella di testo **Nome**, un altro nome o accettare il nome predefinito e quindi scegliere il pulsante **OK**.  
  
     Il nuovo progetto verrà visualizzato in **Esplora soluzioni**.  
  
5.  Il progetto include un riferimento a System.Core.dll e una direttiva `using` per lo spazio dei nomi <xref:System.Linq?displayProperty=fullName>.  
  
## Creazione di un'origine dati in memoria  
 L'origine dati per le query è un semplice elenco di oggetti `Student`.  Ogni record `Student` contiene un nome, un cognome e una matrice di valori interi che rappresentano i punteggi dei test della classe.  Copiare questo codice nel progetto.  Tenere presente le seguenti caratteristiche:  
  
-   La classe `Student` è costituita da proprietà implementate automaticamente.  
  
-   Ogni studente nell'elenco viene inizializzato con un inizializzatore di oggetto.  
  
-   L'elenco stesso viene inizializzato con un inizializzatore di raccolta.  
  
 Tutta la struttura dei dati verrà inizializzata e ne verrà creata un'istanza senza chiamate esplicite a un costruttore o accesso esplicito a un membro.  Per ulteriori informazioni su queste nuove funzionalità, vedere [Proprietà implementate automaticamente](../../../../csharp/programming-guide/classes-and-structs/auto-implemented-properties.md) e [Inizializzatori di oggetto e di raccolta](../../../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md).  
  
#### Per aggiungere l'origine dati  
  
-   Aggiungere la classe `Student` e l'elenco di studenti inizializzato alla classe `Program` nel progetto.  
  
     [!code-cs[CsLinqGettingStarted#11](../../../../csharp/programming-guide/concepts/linq/codesnippet/csharp/GettingStarted/Class1.cs#11)]  
  
#### Per aggiungere un nuovo oggetto Student all'elenco Students  
  
1.  Aggiungere un nuovo oggetto `Student` all'elenco `Students` e utilizzare un nome e i punteggi dei test desiderati.  Provare a immettere tutte le informazioni sul nuovo studente in modo da acquisire dimestichezza con la sintassi per l'inizializzatore di oggetto.  
  
## Creazione della query  
  
#### Per creare una query semplice  
  
-   Nel metodo `Main` dell'applicazione creare una query semplice che, quando verrà eseguita, produrrà un elenco di tutti gli studenti il cui punteggio nel primo test era superiore a 90.  Si noti che, poiché viene selezionato l'intero oggetto `Student`, il tipo della query è `IEnumerable<Student>`.  Sebbene nel codice poteva essere utilizzata la tipizzazione implicita mediante la parola chiave [var](../../../../csharp/language-reference/keywords/var.md), è stata utilizzata la tipizzazione esplicita per illustrare dettagliatamente i risultati.  Per ulteriori informazioni su `var`, vedere [Variabili locali tipizzate in modo implicito](../../../../csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables.md).  
  
     Tenere inoltre presente che la variabile di intervallo della query, `student`, funge da riferimento a ogni oggetto `Student` presente nell'origine, fornendo l'accesso al membro per ogni oggetto.  
  
 [!code-cs[CsLINQGettingStarted#12](../../../../csharp/programming-guide/concepts/linq/codesnippet/csharp/GettingStarted/Class1.cs#12)]  
  
## Esecuzione della query  
  
#### Per eseguire la query  
  
1.  Scrivere ora il ciclo `foreach` che consente di eseguire la query.  In relazione al codice tenere presente quanto segue:  
  
    -   È possibile accedere a ogni elemento della sequenza restituita mediante la variabile di iterazione nel ciclo `foreach`.  
  
    -   Il tipo di questa variabile è `Student` e il tipo della variabile di query è compatibile, `IEnumerable<Student>`.  
  
2.  Dopo avere aggiunto questo codice, compilare ed eseguire l'applicazione premendo CTRL \+ F5 per visualizzare i risultati nella finestra della console.  
  
 [!code-cs[CsLINQGettingStarted#13](../../../../csharp/programming-guide/concepts/linq/codesnippet/csharp/GettingStarted/Class1.cs#13)]  
  
#### Per aggiungere un'altra condizione di filtro  
  
1.  È possibile combinare più condizioni booleane nella clausola `where` in modo da perfezionare ulteriormente la query.  Il codice seguente aggiunge una condizione in modo che la query restituisca gli studenti di cui il primo punteggio era superiore a 90 e l'ultimo inferiore a 80.  La clausola `where` dovrebbe essere analoga al codice seguente.  
  
    ```  
    where student.Scores[0] > 90 && student.Scores[3] < 80  
    ```  
  
     Per ulteriori informazioni, vedere [Clausola where](../../../../csharp/language-reference/keywords/where-clause.md).  
  
## Modifica della query  
  
#### Per ordinare i risultati  
  
1.  Sarà più semplice analizzare i risultati se vengono ordinati.  È possibile ordinare la sequenza restituita in base a qualsiasi campo accessibile negli elementi di origine.  Ad esempio, la clausola `orderby` riportata di seguito ordina i risultati alfabeticamente dalla A alla Z in base al cognome di ogni studente.  Aggiungere alla query la clausola `orderby` riportata di seguito, subito dopo l'istruzione `where` e prima dell'istruzione `select`:  
  
    ```  
    orderby student.Last ascending  
    ```  
  
2.  Modificare ora la clausola `orderby` in modo da disporre i risultati in ordine inverso in base al punteggio del primo test, iniziando dal punteggio più alto fino a quello più basso.  
  
    ```  
    orderby student.Scores[0] descending  
    ```  
  
3.  Modificare la stringa di formato `WriteLine` in modo da poter visualizzare i punteggi:  
  
    ```  
    Console.WriteLine("{0}, {1} {2}", student.Last, student.First, student.Scores[0]);  
    ```  
  
     Per ulteriori informazioni, vedere [Clausola orderby](../../../../csharp/language-reference/keywords/orderby-clause.md).  
  
#### Per raggruppare i risultati  
  
1.  Il raggruppamento è una funzionalità potente nelle espressioni di query.  Una query con una clausola group genera una sequenza di gruppi e ogni gruppo contiene un oggetto `Key` e una sequenza costituita da tutti i membri di tale gruppo.  Nella nuova query riportata di seguito gli studenti vengono raggruppati utilizzando la prima lettera del cognome come chiave.  
  
     [!code-cs[CsLINQGettingStarted#14](../../../../csharp/programming-guide/concepts/linq/codesnippet/csharp/GettingStarted/Class1.cs#14)]  
  
2.  Il tipo della query è stato ora modificato.  Vengono ora generate una sequenza di gruppi con il tipo `char` come chiave e una sequenza di oggetti `Student`.  Poiché il tipo della query è stato modificato, nel codice seguente viene modificato anche il ciclo di esecuzione `foreach`:  
  
     [!code-cs[CsLINQGettingStarted#15](../../../../csharp/programming-guide/concepts/linq/codesnippet/csharp/GettingStarted/Class1.cs#15)]  
  
3.  Premere CTRL \+ F5 per eseguire l'applicazione e visualizzare i risultati nella finestra della console.  
  
     Per ulteriori informazioni, vedere [Clausola group](../../../../csharp/language-reference/keywords/group-clause.md).  
  
#### Per creare le variabili tipizzate in modo implicito  
  
1.  Codificare in modo esplicito `IEnumerables` di `IGroupings` può risultare noioso.  È possibile scrivere la stessa query e il ciclo `foreach` in modo notevolmente più pratico utilizzando `var`.  La parola chiave `var` non modifica i tipi degli oggetti ma indica solo al compilatore di dedurre i tipi.  Modificare il tipo di `studentQuery` e la variabile di iterazione `group`a `var` e rieseguire la query.  Nel ciclo `foreach` interno la variabile di iterazione è ancora tipizzata come `Student` e la query funziona esattamente come prima.  Impostare la variabile di iterazione `s` su `var` e rieseguire la query.  Si otterranno esattamente gli stessi risultati.  
  
     [!code-cs[CsLINQGettingStarted#16](../../../../csharp/programming-guide/concepts/linq/codesnippet/csharp/GettingStarted/Class1.cs#16)]  
  
     Per ulteriori informazioni su [var](../../../../csharp/language-reference/keywords/var.md), vedere [Variabili locali tipizzate in modo implicito](../../../../csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables.md).  
  
#### Per ordinare i gruppi in base al valore della chiave  
  
1.  Quando si esegue la query precedente, i gruppi non sono in ordine alfabetico.  Per modificare questo comportamento, è necessario fornire la clausola `orderby` dopo la clausola `group`.  Per utilizzare la clausola `orderby`, è necessario però utilizzare prima un identificatore che funga da riferimento ai gruppi creati dalla clausola `group`.  Fornire l'identificatore utilizzando la parola chiave `into`, come segue:  
  
     [!code-cs[csLINQGettingStarted#17](../../../../csharp/programming-guide/concepts/linq/codesnippet/csharp/GettingStarted/Class1.cs#17)]  
  
     Quando si esegue questa query, i gruppi verranno ora ordinati alfabeticamente.  
  
#### Per introdurre un identificatore utilizzando let  
  
1.  È possibile utilizzare la parola chiave `let` per introdurre un identificatore per qualsiasi risultato dell'espressione di query.  Questo identificatore può risultare utile come nell'esempio seguente o può migliorare le prestazioni archiviando i risultati di un'espressione in modo da non doverla calcolare più volte.  
  
     [!code-cs[csLINQGettingStarted#18](../../../../csharp/programming-guide/concepts/linq/codesnippet/csharp/GettingStarted/Class1.cs#18)]  
  
     Per ulteriori informazioni, vedere [Clausola let](../../../../csharp/language-reference/keywords/let-clause.md).  
  
#### Per utilizzare la sintassi del metodo in un'espressione di query  
  
1.  Come descritto in [Query Syntax and Method Syntax in LINQ](../../../../csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq.md), alcune operazioni di query possono essere espresse solo utilizzando la sintassi del metodo.  Nel codice seguente viene calcolato il punteggio totale per ogni `Student` nella sequenza di origine e viene quindi chiamato il metodo `Average()` sui risultati della query per calcolare il punteggio medio della classe.  Notare l'utilizzo delle parentesi nell'espressione di query.  
  
     [!code-cs[csLINQGettingStarted#19](../../../../csharp/programming-guide/concepts/linq/codesnippet/csharp/GettingStarted/Class1.cs#19)]  
  
#### Per trasformare o proiettare nella clausola select  
  
1.  Una query genera normalmente una sequenza i cui elementi differiscono dagli elementi delle sequenze di origine.  Eliminare o impostare come commento la query precedente e il ciclo di esecuzione e sostituirli con il codice seguente.  La query restituisce una sequenza di stringhe \(non `Students`\) che si riflette nel ciclo `foreach`.  
  
     [!code-cs[csLINQGettingStarted#20](../../../../csharp/programming-guide/concepts/linq/codesnippet/csharp/GettingStarted/Class1.cs#20)]  
  
2.  Il codice precedente in questa procedura dettagliata indica che il punteggio medio della classe è pari a circa 334.  Per produrre una sequenza di `Students` il cui punteggio totale sia superiore alla media della classe, insieme al relativo `Student ID`, è possibile utilizzare un tipo anonimo nell'istruzione `select`:  
  
     [!code-cs[csLINQGettingStarted#21](../../../../csharp/programming-guide/concepts/linq/codesnippet/csharp/GettingStarted/Class1.cs#21)]  
  
## Passaggi successivi  
 Dopo aver acquisito dimestichezza con le caratteristiche principali delle query in C\#, è possibile leggere la documentazione e gli esempi per il tipo specifico di provider [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq-md.md)] desiderato:  
  
 [LINQ to SQL](../Topic/LINQ%20to%20SQL.md)  
  
 [LINQ to DataSet](../Topic/LINQ%20to%20DataSet.md)  
  
 [LINQ to XML](../../../../visual-basic/programming-guide/concepts/linq/linq-to-xml.md)  
  
 [LINQ to Objects](../../../../visual-basic/programming-guide/concepts/linq/linq-to-objects.md)  
  
## Vedere anche  
 [LINQ \(Language\-Integrated Query\)](../Topic/LINQ%20\(Language-Integrated%20Query\).md)   
 [Getting Started with LINQ in C\#](../../../../csharp/programming-guide/concepts/linq/getting-started-with-linq.md)   
 [Espressioni di query LINQ](../../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [Supplementary LINQ Resources](../Topic/Supplementary%20LINQ%20Resources.md)   
 [Procedura dettagliata: Scrittura delle query in Visual Basic](../../../../visual-basic/programming-guide/concepts/linq/walkthrough-writing-queries.md)