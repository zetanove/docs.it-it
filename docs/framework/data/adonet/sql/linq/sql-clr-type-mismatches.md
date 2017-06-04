---
title: "Mancata corrispondenza tra tipi SQL e CLR | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0a90c33f-7ed7-4501-ad5f-6224c5da8e9b
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Mancata corrispondenza tra tipi SQL e CLR
[!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] consente di automatizzare la maggior parte delle operazioni di conversione tra il modello a oggetti e SQL Server.  Alcune situazioni impediscono tuttavia che la conversione venga eseguita esattamente.  Questi importanti casi di mancata corrispondenza tra i tipi CLR \(Common Language Runtime\) e i tipi dei database di SQL Server sono riepilogati nelle sezioni seguenti.  Per altre informazioni sui mapping di tipi specifici e sulla conversione di funzioni, vedere [Mapping di tipi SQL\-CLR](../../../../../../docs/framework/data/adonet/sql/linq/sql-clr-type-mapping.md) e [Tipi di dati e funzioni](../../../../../../docs/framework/data/adonet/sql/linq/data-types-and-functions.md).  
  
## Riepilogo dei tipi di dati  
 La conversione tra CLR e SQL Server viene eseguita quando una query viene inviata al database e quando i risultati vengono restituiti al modello a oggetti.  Nella query Transact\-SQL seguente sono ad esempio necessarie due conversioni di valori:  
  
```  
Select DateOfBirth From Customer Where CustomerId = @id     
```  
  
 Per poter eseguire la query in SQL Server, è necessario specificare il valore per il parametro Transact\-SQL.  In questo esempio il valore del parametro `id` deve prima essere convertito da un tipo <xref:System.Int32?displayProperty=fullName> CLR a un tipo `INT` SQL Server in modo da poter essere compreso dal database.  Per recuperare i risultati, la colonna `DateOfBirth` di SQL Server deve quindi essere convertita da un tipo `DATETIME` SQL Server a un tipo <xref:System.DateTime?displayProperty=fullName> CLR per l'uso nel modello a oggetti.  In questo esempio i tipi nel modello a oggetti CLR e nel database di SQL Server dispongono di mapping naturali.  Ma non sempre questo avviene.  
  
### Controparti mancanti  
 I tipi seguenti non dispongono di controparti logiche.  
  
-   Mancate corrispondenze nello spazio dei nomi <xref:System> CLR:  
  
    -   **Integer senza segno**.  Per questi tipi viene in genere eseguito il mapping alle controparti con segno di dimensioni maggiori per evitare l'overflow.  I valori letterali possono essere convertiti in un valore numerico con segno di dimensioni uguali o inferiori, in base al valore.  
  
    -   **Boolean**.  Per questi tipi può essere eseguito il mapping a un valore numerico o stringa di un bit o maggiore.  È possibile eseguire il mapping di un valore letterale a un'espressione che restituisca lo stesso valore, ad esempio, `1=1` in SQL per `True` in CLS.  
  
    -   **TimeSpan**.  Questo tipo rappresenta la differenza tra due valori `DateTime` e non corrisponde al valore `timestamp` di SQL Server.  In alcuni casi, è anche possibile eseguire il mapping del tipo <xref:System.Timespan?displayProperty=fullName> CLR al tipo `TIME` SQL Server.  Il tipo `TIME` SQL Server consente di rappresentare solo valori positivi inferiori alle 24 ore.  Il tipo <xref:System.Timespan> consente di rappresentare un intervallo molto più ampio.  
  
    > [!NOTE]
    >  I tipi [!INCLUDE[dnprdnshort](../../../../../../includes/dnprdnshort-md.md)] specifici di SQL Server in <xref:System.Data.SqlTypes> non sono inclusi in questo confronto.  
  
-   Mancate corrispondenze in SQL Server:  
  
    -   **Tipi di carattere a lunghezza fissa**.  In Transact\-SQL viene fatta distinzione tra categorie Unicode e non Unicode e sono disponibili tre tipi distinti in ogni categoria: `nchar`\/`char` a lunghezza fissa, `nvarchar`\/`varchar` a lunghezza variabile e `ntext`\/`text` con una dimensione maggiore.  I tipi di carattere a lunghezza fissa possono essere mappati al tipo <xref:System.Char?displayProperty=fullName> CLR per il recupero di caratteri, ma in realtà non corrispondono esattamente allo stesso tipo sia in termini di conversione che di comportamento.  
  
    -   **Bit**.  Anche se nel dominio `bit` è presente lo stesso numero di valori di `Nullable<Boolean>`, i due tipi sono diversi.  `Bit` accetta i valori `1` e `0` anziché `true`\/`false` e non può essere usato come equivalente delle espressioni booleane.  
  
    -   **Timestamp**.  A differenza del tipo <xref:System.Timespan?displayProperty=fullName> CLR, il tipo `TIMESTAMP` SQL Server rappresenta un numero di 8 byte generato dal database, univoco per ogni aggiornamento e non basato sulla differenza tra valori <xref:System.DateTime>.  
  
    -   **Money** e **SmallMoney**.  Per questi tipi è possibile eseguire il mapping a <xref:System.Decimal>, ma si tratta di tipi fondamentalmente diversi e come tali vengono gestiti dalle funzioni e conversioni basate su server.  
  
### Più mapping  
 Vi sono molti tipi di dati SQL Server che è possibile mappare a uno o più tipi di dati CLR,  nonché molti tipi di dati CLR che è possibile mappare a uno o più tipi SQL Server.  Anche se un mapping è supportato da LINQ to SQL, questo non significa che vi sia una perfetta corrispondenza tra i due tipi mappati tra CLR e SQL Server per quanto riguarda precisione, intervallo e semantica.  Alcuni mapping possono includere differenze per quanto riguarda una o tutte queste dimensioni.  Per informazioni dettagliate su queste differenze potenziali per le varie possibilità di mapping, vedere [Mapping di tipi SQL\-CLR](../../../../../../docs/framework/data/adonet/sql/linq/sql-clr-type-mapping.md).  
  
### Tipi definiti dall'utente  
 I tipi CLR definiti dall'utente sono progettati per consentire di colmare la lacuna nel sistema di tipi.  Tuttavia, fanno emergere problemi che richiamano l'attenzione sul controllo delle versioni dei tipi.  Una modifica nella versione sul client potrebbe non corrispondere a una modifica nel tipo archiviato sul server database.  Una modifica di questo genere causa un altro tipo non corrispondente in cui la semantica del tipo potrebbe non corrispondere e la lacuna nel controllo delle versioni diventerà molto probabilmente visibile.  Ulteriori problemi si verificano durante il refactoring delle gerarchie di ereditarietà nelle versioni successive.  
  
## Semantica dell'espressione  
 Oltre alle coppie non corrispondenti tra tipi CLR e tipi di database, le espressioni aggiungono complessità ai casi di mancata corrispondenza.  È necessario considerare le errate corrispondenze nella semantica degli operatori, nella semantica delle funzioni, nella conversione implicita dei tipi e nelle regole di precedenza.  
  
 Nelle sottosezioni seguenti viene illustrata l'errata corrispondenza tra espressioni apparentemente simili.  È possibile generare espressioni SQL semanticamente equivalenti a una particolare espressione CLR.  Non è tuttavia chiaro se le differenze semantiche tra espressioni apparentemente simili siano evidenti a un utente CLR e, pertanto, se le modifiche richieste per l'equivalenza semantica possano essere intenzionali o meno.  Si tratta di un problema particolarmente critico quando un'espressione viene valutata per un set di valori.  La visibilità della differenza può dipendere da dati ed essere difficilmente identificabile durante la scrittura del codice e il debug.  
  
### Semantica Null  
 Le espressioni SQL forniscono una logica a tre valori per le espressioni booleane.  Il risultato può essere vero, falso o null.  In CLR, invece, viene specificato un risultato booleano a due valori per i confronti che prevedono valori null.  Esaminare il codice seguente:  
  
 [!code-csharp[DLinqMismatch#2](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqMismatch/cs/Program.cs#2)]
 [!code-vb[DLinqMismatch#2](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqMismatch/vb/Module1.vb#2)]  
  
```  
-- Assume col1 and col2 are integer columns with null values.   
-- Assume that ANSI null behavior has not been explicitly  
--    turned off.  
Select …  
From …  
Where col1 = col2  
-- Evaluates to null, not true and the corresponding row is not  
--     selected.  
-- To obtain matching behavior (i -> col1, j -> col2) change  
--     the query to the following:  
Select …  
From …  
Where  
    col1 = col2   
or (col1 is null and col2 is null)  
-- (Visual Basic 'Nothing'.)  
```  
  
 Si verifica un problema analogo presupponendo risultati a due valori.  
  
 [!code-csharp[DLinqMismatch#3](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqMismatch/cs/Program.cs#3)]
 [!code-vb[DLinqMismatch#3](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqMismatch/vb/Module1.vb#3)]  
  
```  
-- Assume col1 and col2 are nullable columns.  
-- Assume that ANSI null behavior has not been explicitly  
--     turned off.  
Select …  
From …  
Where  
    col1 = col2        
or col1 != col2  
-- Visual Basic: col1 <> col2.  
  
-- Excludes the case where the boolean expression evaluates  
--     to null. Therefore the where clause does not always  
--     evaluate to true.  
```  
  
 Nel caso precedente è possibile ottenere un comportamento equivalente nella generazione di codice SQL, tuttavia la conversione potrebbe non riflettere esattamente l'intenzione.  
  
 [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] non impone valori `null` C\# o la semantica di confronto `nothing` di [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)] in SQL.  Gli operatori di confronto vengono sintatticamente convertiti negli equivalenti SQL.  La semantica riflette la semantica SQL secondo quanto definito nelle impostazioni di connessione o del server.  Due valori null sono considerati non uguali secondo le impostazioni di SQL Server predefinite, anche se è possibile modificare tali impostazioni per modificare la semantica.  Indipendentemente da questa premessa, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] non considera le impostazioni del server nella conversione della query.  
  
 Un confronto con il valore letterale `null` \(`nothing`\) viene convertito nella versione SQL appropriata \(`is null` o `is not null`\).  
  
 Il valore di `null` \(`nothing`\) nelle regole di confronto viene definito da SQL Server. [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] non modifica le regole di confronto.  
  
### Conversione e promozione del tipo  
 SQL supporta un vasta gamma di conversioni implicite nelle espressioni.  Espressioni simili in C\# richiederebbero un cast esplicito.  Ad esempio:  
  
-   I tipi `Nvarchar` e `DateTime` possono essere confrontati in SQL senza cast espliciti, mentre in C\# è richiesta la conversione esplicita.  
  
-   In SQL `Decimal` viene convertito implicitamente in `DateTime`.  C\# non consente una conversione implicita.  
  
 In modo analogo, la precedenza dei tipi in Transact\-SQL è diversa da quella in C\#, in quanto il set di tipi sottostante è diverso.  Non esiste infatti una chiara relazione di subset o superset tra gli elenchi di precedenza.  Ad esempio, il confronto di un tipo `nvarchar` con un tipo `varchar` causa la conversione implicita dell'espressione `varchar` in `nvarchar`.  In CLR non viene fornita alcuna promozione equivalente.  
  
 Nei casi più semplici queste differenze provocano la ridondanza di espressioni CLR con cast per un'espressione SQL corrispondente.  È importante notare che i risultati intermedi di un'espressione SQL potrebbero essere implicitamente promossi in un tipo privo di un'esatta controparte in C\# e viceversa.  Complessivamente le operazioni di test, debug e convalida di tali espressioni comportano un carico di lavoro significativo per l'utente.  
  
### Regole di confronto  
 Transact\-SQL supporta regole di confronto esplicite come annotazioni ai tipi stringa di caratteri.  Queste regole di confronto determinano la validità di certi confronti.  Ad esempio, è errato confrontare due colonne con regole di confronto esplicite diverse.  L'utilizzo di un tipo stringa CTS molto semplificato non provoca tali errori.  Si consideri l'esempio seguente:  
  
```  
create table T2 (  
    Col1 nvarchar(10),  
    Col2      nvarchar(10) collate Latin_general_ci_as  
)  
```  
  
 [!code-csharp[DLinqMismatch#4](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqMismatch/cs/Program.cs#4)]
 [!code-vb[DLinqMismatch#4](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqMismatch/vb/Module1.vb#4)]  
  
```  
Select …  
From …  
Where Col1 = Col2  
-- Error, collation conflict.  
```  
  
 Di fatto, la sottoclausola delle regole di confronto crea un *tipo limitato* non sostituibile.  
  
 In modo analogo, il criterio di ordinamento può essere significativamente diverso nei diversi sistemi di tipi.  Questa differenza influisce sull'ordinamento dei risultati.  <xref:System.Guid> viene ordinato in base a tutti i 16 byte in ordine lessicografico \(`IComparable()`\), mentre in T\-SQL vengono confrontati i GUID in base all'ordine seguente: node\(10\-15\), clock\-seq\(8\-9\), time\-high\(6\-7\), time\-mid\(4\-5\), time\-low\(0\-3\).  Questo ordinamento veniva eseguito in SQL 7.0 dove i GUID generati da NT erano caratterizzati da tale ordine di ottetti.  Questo approccio assicura che i GUID generati nello stesso cluster del nodo vengano uniti in ordine sequenziale in base al timestamp.  L'approccio è inoltre utile per la compilazione di indici \(gli inserimenti diventano aggiunte anziché I\/O casuali\).  Successivamente questo ordine è stato codificato in Windows per evitare problemi di privacy, ma in SQL è stata mantenuta la compatibilità.  Una soluzione alternativa consiste nell'usare <xref:System.Data.SqlTypes.SqlGuid> anziché <xref:System.Guid>.  
  
### Differenze di operatori e funzioni  
 Operatori e funzioni essenzialmente simili presentano tuttavia una semantica leggermente diversa.  Ad esempio:  
  
-   In C\# viene specificata una semantica di corto circuito basata su un ordine lessicale di operandi per gli operatori logici `&&` e `||`.  D'altra parte, SQL è destinato alle query basate su set, pertanto consente all'utilità di ottimizzazione di stabilire più liberamente l'ordine di esecuzione.  Di seguito sono riportate alcune implicazioni:  
  
    -   Una conversione semanticamente equivalente richiederebbe il costrutto "`CASE` ... `WHEN`. `THEN`" in SQL per evitare di riordinare l'esecuzione dell'operando.  
  
    -   Una conversione non rigida negli operatori `AND`\/`OR` potrebbe provocare errori imprevisti se per la valutazione del secondo operando l'espressione C\# si basa sul risultato della valutazione del primo operando.  
  
-   La semantica della funzione `Round()` è diversa in [!INCLUDE[dnprdnshort](../../../../../../includes/dnprdnshort-md.md)] e in T\-SQL.  
  
-   L'indice iniziale per le stringhe è 0 in CLR, ma 1 in SQL.  Pertanto, qualsiasi funzione con un indice deve essere sottoposta alla conversione dell'indice.  
  
-   CLR supporta l'operatore modulo \("%"\) per i numeri a virgola mobile, al contrario di SQL.  
  
-   L'operatore `Like` acquisisce efficacemente gli overload automatici in base a conversioni implicite.  Anche se l'operatore `Like` viene definito per il funzionamento con tipi stringa di caratteri, la conversione implicita da tipi numerici o tipi `DateTime` consente di usare anche i tipi non stringa con `Like`.  In CTS non esistono conversioni implicite confrontabili.  Di conseguenza sono necessari overload aggiuntivi.  
  
    > [!NOTE]
    >  Questo comportamento dell'operatore `Like` si applica solo a C\#; la parola chiave `Like` di Visual Basic rimane invariata.  
  
-   L'overflow viene sempre controllato in SQL, ma deve essere specificato in modo esplicito in C\# \(non in [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)]\) per evitare wraparound.  Date le colonne di valori integer C1, C2 e C3, se C1\+C2 viene archiviato in C3 \(aggiorna il set T C3 \= C1 \+ C2\).  
  
    ```  
    create table T3 (  
        Col1      integer,  
        Col2      integer  
    )  
    insert into T3 (col1, col2) values (2147483647, 5)  
    -- Valid values: max integer value and 5.  
    select * from T3 where col1 + col2 < 0  
    -- Produces arithmetic overflow error.  
    ```  
  
 [!code-csharp[DLinqMismatch#5](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqMismatch/cs/Program.cs#5)]
 [!code-vb[DLinqMismatch#5](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqMismatch/vb/Module1.vb#5)]  
  
-   In SQL viene eseguito l'arrotondamento aritmetico simmetrico, mentre in [!INCLUDE[dnprdnshort](../../../../../../includes/dnprdnshort-md.md)] viene usato un particolare tipo di arrotondamento.  Per ulteriori dettagli, vedere l'articolo della Knowledge Base 196652.  
  
-   Per impostazione predefinita, in SQL non viene fatta distinzione tra maiuscole e minuscole nelle operazioni di confronto tra stringhe di caratteri per le impostazioni locali comuni.  In Visual Basic e in C\#, invece, viene fatta distinzione tra maiuscole e minuscole.  Ad esempio, `s == "Food"` \(`s = "Food"` in [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)]\) e `s == "Food"` possono restituire risultati diversi se `s` è `food`.  
  
    ```  
    -- Assume default US-English locale (case insensitive).  
    create table T4 (  
        Col1      nvarchar (256)  
    )  
    insert into T4 values (‘Food’)   
    insert into T4 values (‘FOOD’)  
    select * from T4 where Col1 = ‘food’  
    -- Both the rows are returned because of case-insensitive matching.  
    ```  
  
 [!code-csharp[DLinqMismatch#6](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqMismatch/cs/Program.cs#6)]
 [!code-vb[DLinqMismatch#6](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqMismatch/vb/Module1.vb#6)]  
  
-   Le funzioni o gli operatori applicati agli argomenti dei tipi di carattere a lunghezza fissa in SQL hanno una semantica significativamente diversa rispetto alle funzioni o agli operatori analoghi applicati a <xref:System.String?displayProperty=fullName> CLR.  Anche questo può essere considerato come un'estensione del problema relativo alle controparti mancanti discusso nella sezione sui tipi.  
  
    ```  
    create table T4 (  
        Col1      nchar(4)  
    )  
    Insert into T5(Col1) values ('21');  
    Insert into T5(Col1) values ('1021');  
    Select * from T5 where Col1 like '%1'  
    -- Only the second row with Col1 = '1021' is returned.  
    -- Not the first row!  
    ```  
  
     [!code-csharp[DLinqMismatch#7](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqMismatch/cs/Program.cs#7)]
     [!code-vb[DLinqMismatch#7](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqMismatch/vb/Module1.vb#7)]  
  
     Un problema analogo si verifica con la concatenazione di stringhe.  
  
    ```  
    create table T6 (  
        Col1      nchar(4)  
        Col2       nchar(4)  
    )  
    Insert into T6 values ('a', 'b');  
    Select Col1+Col2 from T6  
    -- Returns concatenation of padded strings "a   b   " and not "ab".  
    ```  
  
 In sintesi, per le espressioni CLR potrebbe essere necessaria una conversione complessa, mentre per esporre le funzionalità SQL potrebbero essere necessari funzioni o operatori aggiuntivi.  
  
### Cast di tipo  
 In C\# e in SQL gli utenti possono eseguire l'override della semantica delle espressioni predefinita usando cast di tipo espliciti \(`Cast` e `Convert`\).  Tuttavia, l'esposizione di questa funzionalità oltre il limite del sistema di tipi costituisce un dilemma.  Un cast SQL che fornisce la semantica desiderata non può essere convertito facilmente nel corrispondente cast C\#.  D'altra parte un cast C\# non può essere convertito direttamente in un cast SQL equivalente a causa di tipi non corrispondenti, controparti mancanti e gerarchie di precedenza dei tipi diverse.  Esiste un compromesso tra l'esposizione del sistema di tipi non corrispondente e la perdita significativa di potenza di un'espressione.  
  
 Negli altri casi il cast dei tipi potrebbe non essere necessario in alcun dominio per la convalida di un'espressione, ma potrebbe essere richiesto per garantire che un mapping non predefinito venga applicato correttamente all'espressione.  
  
```  
-- Example from "Non-default Mapping" section extended  
create table T5 (  
    Col1      nvarchar(10),  
    Col2      nvarchar(10)  
)  
Insert into T5(col1, col2) values (‘3’, ‘2’);  
```  
  
 [!code-csharp[DLinqMismatch#8](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqMismatch/cs/Program.cs#8)]
 [!code-vb[DLinqMismatch#8](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqMismatch/vb/Module1.vb#8)]  
  
```  
Select *  
From T5  
Where Col1 + Col2 > 4     
-- "Col1 + Col2" expr evaluates to '32'   
```  
  
## Problemi relativi alle prestazioni  
 Le differenze tra i tipi SQL Server e CLR possono comportare un calo delle prestazioni nel passaggio tra i sistemi di tipi CLR e SQL Server.  Di seguito vengono indicati alcuni esempi di scenari che influenzano le prestazioni:  
  
-   Ordine di valutazione forzato per gli operatori And\/Or logici  
  
-   La generazione di codice SQL per applicare l'ordine di valutazione del predicato limita la funzionalità dell'utilità di ottimizzatore SQL.  
  
-   Le conversioni dei tipi, che vengano introdotte da un compilatore CLR o dall'implementazione di una query relazionale a oggetti, possono limitare l'uso dell'indice.  
  
     Di seguito è riportato un esempio:  
  
    ```  
    -- Table DDL  
    create table T5 (  
        Col1      varchar(100)  
    )  
    ```  
  
     [!code-csharp[DLinqMismatch#9](../../../../../../samples/snippets/csharp/VS_Snippets_Data/DLinqMismatch/cs/Program.cs#9)]
     [!code-vb[DLinqMismatch#9](../../../../../../samples/snippets/visualbasic/VS_Snippets_Data/DLinqMismatch/vb/Module1.vb#9)]  
  
     Considerare la conversione dell'espressione `(s = SOME_STRING_CONSTANT)`.  
  
    ```  
    -- Corresponding part of SQL where clause  
    Where …  
    Col1 = SOME_STRING_CONSTANT  
    -- This expression is of the form <varchar> = <nvarchar>.  
    -- Hence SQL introduces a conversion from varchar to nvarchar,  
    --     resulting in  
    Where …  
    Convert(nvarchar(100), Col1) = SOME_STRING_CONSTANT  
    -- Cannot use the index for column Col1 for some implementations.  
    ```  
  
 Oltre alle differenze semantiche, è importante considerare l'impatto sulle prestazioni nel passaggio tra i sistemi di tipi SQL Server e CLR.  Per i set di dati di grandi dimensioni questi problemi di prestazioni possono determinare l'implementazione o meno di un'applicazione.  
  
## Vedere anche  
 [Informazioni complementari](../../../../../../docs/framework/data/adonet/sql/linq/background-information.md)