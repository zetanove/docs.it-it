---
redirect_url: /dotnet/articles/csharp/linq/query-expression-basics
caps.handback.revision: 32
---
# Nozioni fondamentali sulle espressioni di query (Guida per programmatori C#)
## Definizione e scopo di una query  
 Una *query* è un set di istruzioni che descrive quali dati recuperare da una o più origini dati specificate e quale forma e organizzazione devono avere i dati restituiti.  Una query è distinta dai risultati che produce.  
  
 I dati di origine sono in genere organizzati in modo logico, come sequenza di elementi dello stesso tipo.  Una tabella di database SQL contiene una sequenza di righe.  In modo analogo, un oggetto [!INCLUDE[vstecado](../../../csharp/programming-guide/concepts/linq/includes/vstecado-md.md)]<xref:System.Data.DataTable> contiene una sequenza di oggetti <xref:System.Data.DataRow>.  In un file XML, esiste una "sequenza" di elementi XML \(anche se questi sono organizzati gerarchicamente in una struttura ad albero\).  Una raccolta in memoria contiene una sequenza di oggetti.  
  
 Dal punto di vista di un'applicazione, il tipo e la struttura specifici dei dati di origine di partenza non sono importanti.  L'applicazione considera sempre i dati di origine una raccolta <xref:System.Collections.Generic.IEnumerable%601> o <xref:System.Linq.IQueryable%601>.  In [!INCLUDE[sqltecxlinq](../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq-md.md)], i dati di origine sono resi visibili come `IEnumerable`\<<xref:System.Xml.Linq.XElement>\>.  In [!INCLUDE[linq_dataset](../../../csharp/programming-guide/linq-query-expressions/includes/linq-dataset-md.md)], si tratta di un `IEnumerable`\<<xref:System.Data.DataRow>\>.  In [!INCLUDE[vbtecdlinq](../../../csharp/includes/vbtecdlinq-md.md)], si tratta di un `IEnumerable` o `IQueryable` di qualsiasi oggetto personalizzato definito per rappresentare i dati nella tabella SQL.  
  
 Data questa sequenza di origine, una query può eseguire una delle tre azioni seguenti:  
  
-   Recuperare un subset degli elementi per produrre una nuova sequenza senza modificare i singoli elementi.  La query può quindi ordinare o raggruppare la sequenza restituita in svariati modi, come illustrato nell'esempio seguente \(si supponga che `scores` sia `int[]`\):  
  
     [!code-cs[csrefQueryExpBasics#45](../../../csharp/programming-guide/linq-query-expressions/codesnippet/csharp/query-expression-basics_1.cs)]  
  
-   Recuperare una sequenza di elementi come nell'esempio precedente, ma trasformarli in un nuovo tipo di oggetto.  Una query, ad esempio, può recuperare solo i cognomi da determinati record cliente in un'origine dati  oppure può recuperare il record completo e quindi utilizzarlo per costruire un altro tipo di oggetto in memoria o persino dati XML prima di generare la sequenza di risultati finale.  Nell'esempio riportato di seguito viene illustrata una trasformazione da `int` a `string`.  Si noti il nuovo tipo di `highScoresQuery`.  
  
     [!code-cs[csrefQueryExpBasics#46](../../../csharp/programming-guide/linq-query-expressions/codesnippet/csharp/query-expression-basics_2.cs)]  
  
-   Recuperare un valore singleton sui dati di origine, ad esempio:  
  
    -   Numero di elementi che corrispondono a una determinata condizione.  
  
    -   Elemento con il valore maggiore o minore.  
  
    -   Primo elemento che corrisponde a una condizione o somma di particolari valori in un set specificato di elementi.  Nella query seguente, ad esempio, viene restituito il numero di punteggi superiori a 80 dalla matrice di integer `scores`:  
  
     [!code-cs[csrefQueryExpBasics#47](../../../csharp/programming-guide/linq-query-expressions/codesnippet/csharp/query-expression-basics_3.cs)]  
  
     Nell'esempio precedente, si noti l'utilizzo di parentesi nell'espressione di query prima della chiamata al metodo `Count`.  È inoltre possibile esprimere ciò utilizzando una variabile nuova per archiviare il risultato concreto.  Questa tecnica è più leggibile perché mantiene la variabile che archivia la query separata dalla query che archivia un risultato.  
  
     [!code-cs[csrefQueryExpBasics#48](../../../csharp/programming-guide/linq-query-expressions/codesnippet/csharp/query-expression-basics_4.cs)]  
  
 Nell'esempio precedente, la query viene eseguita nella chiamata a `Count`, perché `Count` deve scorrere i risultati per determinare il numero di elementi restituiti da `highScoresQuery`.  
  
## Definizione di espressione di query  
 Un'*espressione di query* è una query espressa nella sintassi della query.  Un'espressione di query è un costrutto di linguaggio di prima categoria.  È analoga a qualsiasi altra espressione e può essere utilizzata in qualsiasi contesto in cui è valida un'espressione C\#.  Un'espressione di query è costituita da un set di clausole scritte in una sintassi dichiarativa analoga a SQL o a XQuery.  Ogni clausola contiene a sua volta una o più espressioni C\# e queste espressioni possono essere un'espressione di query o contenere un'espressione di query.  
  
 Un'espressione di query deve iniziare con una clausola [from](../../../csharp/language-reference/keywords/from-clause.md) e terminare con una clausola [select](../../../csharp/language-reference/keywords/select-clause.md) o [group](../../../csharp/language-reference/keywords/group-clause.md).  Tra la prima clausola `from` e l'ultima clausola `select` o `group`, può essere contenuta una o più delle seguenti clausole facoltative: [where](../../../csharp/language-reference/keywords/where-clause.md), [orderby](../../../csharp/language-reference/keywords/orderby-clause.md), [join](../../../csharp/language-reference/keywords/join-clause.md), [let](../../../csharp/language-reference/keywords/let-clause.md) nonché clausole [from](../../../csharp/language-reference/keywords/from-clause.md) aggiuntive.  È inoltre possibile utilizzare la parola chiave [into](../../../csharp/language-reference/keywords/into.md) per consentire al risultato di una clausola `join` o `group` di fungere da origine per le clausole query aggiuntive nella stessa espressione di query.  
  
### Variabile di query  
 In [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq-md.md)], una variabile di query è qualsiasi variabile che archivia una *query* anziché i *risultati* di una query. In particolare, una variabile di query è sempre un tipo enumerabile che produrrà una sequenza di elementi quando viene scorso in un'istruzione `foreach` o in una chiamata diretta al metodo `IEnumerator.MoveNext`.  
  
 Nell'esempio di codice seguente viene illustrata un'espressione di query semplice con un'origine dati, una clausola di filtro, una clausola di ordinamento e nessuna trasformazione degli elementi di origine.  La clausola `select` termina la query.  
  
 [!code-cs[csrefQueryExpBasics#49](../../../csharp/programming-guide/linq-query-expressions/codesnippet/csharp/query-expression-basics_5.cs)]  
  
 Nell'esempio precedente, `scoreQuery` è una *variabile di query* che viene talvolta semplicemente definita  *query*.  La variabile della query non archivia alcun dato del risultato effettivo, che viene prodotto nel ciclo `foreach`.  Quando l'istruzione `foreach` viene eseguita, i risultati della query non sono restituiti tramite la variabile della query `scoreQuery`.  Vengono invece restituiti tramite la variabile di iterazione `testScore`.  La variabile `scoreQuery` può essere iterata in un secondo ciclo `foreach`.  Produrrà gli stessi risultati purché non vengano modificate né la variabile stessa né l'origine dati.  
  
 Una variabile di query può archiviare una query espressa nella sintassi della query o nella sintassi del metodo oppure in una combinazione delle due.  Negli esempi seguenti, `queryMajorCities` e `queryMajorCities2` sono variabili di query:  
  
 [!code-cs[csrefQueryExpBasics#50](../../../csharp/programming-guide/linq-query-expressions/codesnippet/csharp/query-expression-basics_6.cs)]  
  
 Nei due esempi seguenti vengono invece illustrate variabili che non sono variabili di query anche se ognuna viene inizializzata con una query.  Non sono variabili di query perché archiviano risultati:  
  
 [!code-cs[csrefQueryExpBasics#51](../../../csharp/programming-guide/linq-query-expressions/codesnippet/csharp/query-expression-basics_7.cs)]  
  
> [!NOTE]
>  Nella documentazione di [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq-md.md)], nei nomi delle variabili che archiviano una query è presente la parola "query".  Nei nomi delle variabili che archiviano un risultato effettivo non appare "query".  
  
 Per ulteriori informazioni sulle diverse modalità di espressione delle query, vedere [Query Syntax and Method Syntax in LINQ](../../../csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq.md).  
  
#### Tipizzazione esplicita e implicita di variabili di query  
 In questa documentazione viene in genere fornito il tipo esplicito della variabile della query al fine di illustrare la relazione del tipo tra la variabile della query e la [clausola select](../../../csharp/language-reference/keywords/select-clause.md).  È anche tuttavia possibile utilizzare la parola chiave [var](../../../csharp/language-reference/keywords/var.md) per indicare al compilatore di dedurre il tipo di una variabile di query \(o di qualsiasi altra variabile locale\) in fase di compilazione.  La query di esempio illustrata in precedenza in questo argomento può essere espressa anche utilizzando la tipizzazione implicita:  
  
 [!code-cs[csrefQueryExpBasics#52](../../../csharp/programming-guide/linq-query-expressions/codesnippet/csharp/query-expression-basics_8.cs)]  
  
 Per ulteriori informazioni, vedere [Variabili locali tipizzate in modo implicito](../../../csharp/programming-guide/classes-and-structs/implicitly-typed-local-variables.md) e [Type Relationships in LINQ Query Operations](../../../csharp/programming-guide/concepts/linq/type-relationships-in-linq-query-operations.md).  
  
### Inizio di un'espressione di query  
 Un'espressione di query deve iniziare con la clausola `from`.  Specifica un'origine dati insieme a una variabile di intervallo.  La variabile di intervallo, che rappresenta ogni elemento successivo nella sequenza di origine quando la sequenza di origine viene attraversata,  è fortemente tipizzata in base al tipo degli elementi nell'origine dati.  Nell'esempio seguente, poiché `countries` è una matrice di oggetti `Country`, la variabile di intervallo viene tipizzata anche come `Country`.  Poiché la variabile di intervallo è fortemente tipizzata, è possibile utilizzare l'operatore punto per accedere a qualsiasi membro disponibile del tipo.  
  
 [!code-cs[csrefQueryExpBasics#53](../../../csharp/programming-guide/linq-query-expressions/codesnippet/csharp/query-expression-basics_9.cs)]  
  
 La variabile di intervallo si trova nell'ambito finché la query non viene chiusa con un punto e virgola o con una clausola di *continuazione*.  
  
 Un'espressione di query può contenere più clausole `from`.  Utilizzare clausole `from` aggiuntive quando ogni elemento nella sequenza di origine è una raccolta o contiene una raccolta.  Si supponga, ad esempio, di disporre di una raccolta di oggetti `Country`, ognuno dei quali contiene una raccolta di oggetti `City` denominati `Cities`.  Per eseguire una query sugli oggetti `City` in ogni `Country`, utilizzare due clausole `from` come illustrato di seguito:  
  
 [!code-cs[csrefQueryExpBasics#54](../../../csharp/programming-guide/linq-query-expressions/codesnippet/csharp/query-expression-basics_10.cs)]  
  
 Per ulteriori informazioni, vedere [Clausola from](../../../csharp/language-reference/keywords/from-clause.md).  
  
### Fine di un'espressione di query  
 Un'espressione di query deve terminare con una clausola `select` o con una clausola `group`.  
  
#### Clausola group  
 Utilizzare la clausola `group` per produrre una sequenza di gruppi organizzati da una chiave specificata.  La chiave  può essere qualsiasi tipo di dato.  Nella query seguente, ad esempio, viene creata una sequenza di gruppi che contiene uno o più oggetti `Country` e la cui chiave è un valore di `char`.  
  
 [!code-cs[csrefQueryExpBasics#55](../../../csharp/programming-guide/linq-query-expressions/codesnippet/csharp/query-expression-basics_11.cs)]  
  
 Per ulteriori informazioni sul raggruppamento, vedere [Clausola group](../../../csharp/language-reference/keywords/group-clause.md).  
  
#### Clausola select  
 Utilizzare la clausola `select` per produrre tutti gli altri tipi di sequenze.  Una clausola `select` semplice produce solo una sequenza di oggetti dello stesso tipo degli oggetti contenuti nell'origine dati.  In questo esempio, l'origine dati contiene oggetti `Country`.  La clausola `orderby` ordina semplicemente gli elementi in un ordine nuovo e la clausola `select` produce una sequenza degli oggetti `Country` riordinati.  
  
 [!code-cs[csrefQueryExpBasics#56](../../../csharp/programming-guide/linq-query-expressions/codesnippet/csharp/query-expression-basics_12.cs)]  
  
 La clausola `select` può essere utilizzata per trasformare i dati di origine in sequenze di nuovi tipi.  Questa trasformazione è detta anche *proiezione*.  Nell'esempio seguente, la clausola `select` *proietta* una sequenza di tipi anonimi che contiene solo un subset dei campi nell'elemento originale.  Si noti che i nuovi oggetti vengono inizializzati utilizzando un inizializzatore di oggetto.  
  
 [!code-cs[csrefQueryExpBasics#57](../../../csharp/programming-guide/linq-query-expressions/codesnippet/csharp/query-expression-basics_13.cs)]  
  
 Per ulteriori informazioni su tutti i modi in cui una clausola `select` può essere utilizzata per trasformare i dati di origine, vedere [Clausola select](../../../csharp/language-reference/keywords/select-clause.md).  
  
#### Continuazioni con "into"  
 È possibile utilizzare la parola chiave `into` in una clausola `select` o `group` per creare un identificatore temporaneo che archivia una query.  Ricorrere a questa operazione quando è necessario eseguire operazioni aggiuntive su una query dopo un'operazione di raggruppamento o di selezione.  Nel seguente esempio gli oggetti `countries` vengono raggruppati a seconda della popolazione in intervalli di 10 milioni.  Dopo la creazione di questi gruppi, clausole aggiuntive ne filtrano alcuni e quindi li ordinano in ordine crescente.  Per eseguire tali operazioni aggiuntive, è necessaria la continuazione rappresentata da `countryGroup`.  
  
 [!code-cs[csrefQueryExpBasics#58](../../../csharp/programming-guide/linq-query-expressions/codesnippet/csharp/query-expression-basics_14.cs)]  
  
 Per ulteriori informazioni, vedere [into](../../../csharp/language-reference/keywords/into.md).  
  
### Filtro, ordinamento e unione  
 Tra la clausola `from` iniziale e la clausola `select` o `group` finale, tutte le altre clausole \(`where`, `join`, `orderby`, `from`, `let`\) sono facoltative.  Qualsiasi clausola facoltativa può essere utilizzata da zero a più volte in un corpo di query.  
  
#### Clausola where  
 Utilizzare la clausola `where` per filtrare elementi dai dati di origine in basa a una o più espressioni di predicato.  La clausola `where` nell'esempio seguente presenta due predicati.  
  
 [!code-cs[csrefQueryExpBasics#59](../../../csharp/programming-guide/linq-query-expressions/codesnippet/csharp/query-expression-basics_15.cs)]  
  
 Per ulteriori informazioni, vedere [Clausola where](../../../csharp/language-reference/keywords/where-clause.md).  
  
#### Clausola orderby  
 Utilizzare la clausola `orderby` per ordinare i risultati in ordine crescente o decrescente.  È anche possibile specificare ordinamenti secondari.  Nell'esempio seguente viene eseguito un ordinamento primario sugli oggetti `country` utilizzando la proprietà `Area` e quindi un ordinamento secondario utilizzando la proprietà `Population`.  
  
 [!code-cs[csrefQueryExpBasics#60](../../../csharp/programming-guide/linq-query-expressions/codesnippet/csharp/query-expression-basics_16.cs)]  
  
 La parola chiave `ascending` è facoltativa e costituisce l'ordinamento predefinito se non viene specificato alcun ordine.  Per ulteriori informazioni, vedere [Clausola orderby](../../../csharp/language-reference/keywords/orderby-clause.md).  
  
#### Clausola join  
 Utilizzare la clausola `join` per associare e\/o combinare gli elementi di un'origine dati con gli elementi di un'altra origine dati in base a un confronto di uguaglianza tra chiavi specificate in ogni elemento.  In [!INCLUDE[vbteclinq](../../../csharp/includes/vbteclinq-md.md)], le operazioni di join vengono eseguite su sequenze di oggetti i cui elementi sono tipi diversi.  Dopo avere unito due sequenze, è necessario utilizzare un'istruzione `select` o `group` per specificare quale elemento archiviare nella sequenza di output.  È anche possibile utilizzare un tipo anonimo per combinare proprietà da ogni set di elementi associati in un nuovo tipo per la sequenza di output.  Nell'esempio seguente vengono associati gli oggetti `prod` la cui proprietà `Category` corrisponde a una delle categorie nella matrice di stringhe `categories`.  Vengono filtrati i prodotti la cui proprietà `Category` non corrisponde a nessuna stringa in `categories`.  L'istruzione `select` proietta un nuovo tipo le cui proprietà sono accettate sia da `cat` che da `prod`.  
  
 [!code-cs[csrefQueryExpBasics#61](../../../csharp/programming-guide/linq-query-expressions/codesnippet/csharp/query-expression-basics_17.cs)]  
  
 È anche possibile eseguire un group join archiviando i risultati dell'operazione di `join` in una variabile temporanea utilizzando la parola chiave [in](../../../csharp/language-reference/keywords/into.md).  Per ulteriori informazioni, vedere [Clausola join](../../../csharp/language-reference/keywords/join-clause.md).  
  
#### Clausola let  
 Utilizzare la clausola `let` per archiviare il risultato di un'espressione, ad esempio una chiamata al metodo, in una nuova variabile di intervallo.  Nell'esempio seguente, la variabile di intervallo `firstName` archivia il primo elemento della matrice di stringhe restituita da `Split`.  
  
 [!code-cs[csrefQueryExpBasics#62](../../../csharp/programming-guide/linq-query-expressions/codesnippet/csharp/query-expression-basics_18.cs)]  
  
 Per ulteriori informazioni, vedere [Clausola let](../../../csharp/language-reference/keywords/let-clause.md).  
  
### Sottoquery in un'espressione di query  
 Una clausola query può contenere un'espressione di query, che viene talvolta detta *sottoquery*.  Ogni sottoquery inizia con la propria clausola `from` che non punta necessariamente alla stessa origine dati nella prima clausola `from`.  Nella query seguente, ad esempio, viene illustrata un'espressione di query utilizzata nell'istruzione select per recuperare i risultati di un'operazione di raggruppamento.  
  
 [!code-cs[csrefQueryExpBasics#63](../../../csharp/programming-guide/linq-query-expressions/codesnippet/csharp/query-expression-basics_19.cs)]  
  
 Per ulteriori informazioni, vedere [Procedura: eseguire una sottoquery su un'operazione di raggruppamento](../../../csharp/programming-guide/linq-query-expressions/how-to-perform-a-subquery-on-a-grouping-operation.md).  
  
## Vedere anche  
 [Guida per programmatori C\#](../../../csharp/programming-guide/index.md)   
 [Espressioni di query LINQ](../../../csharp/programming-guide/linq-query-expressions/index.md)   
 [LINQ \(Language\-Integrated Query\)](../Topic/LINQ%20\(Language-Integrated%20Query\).md)   
 [Parole chiave di query \(LINQ\)](../../../csharp/language-reference/keywords/query-keywords.md)   
 [Standard Query Operators Overview](../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)