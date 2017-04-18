---
title: Nozioni fondamentali sulle espressioni di query
description: Vengono introdotti concetti relativi alle espressioni di query
keywords: .NET, .NET Core, C#
author: BillWagner
manager: wpickett
ms.author: wiwagn
ms.date: 11/30/2016
ms.topic: article
ms.prod: .net-core
ms.technology: .net-core-technologies
ms.devlang: dotnet
ms.assetid: 027db1f8-346f-44d2-a16e-043fcea3a4e0
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 9fd0ef3c71d66ceca28d3ae7025058df469655c2
ms.lasthandoff: 03/13/2017

---
# <a name="query-expression-basics"></a>Nozioni fondamentali sulle espressioni di query

## <a name="what-is-a-query-and-what-does-it-do"></a>Che cos'è una query e cosa fa? 

 Una *query* è un set di istruzioni che descrive i dati da recuperare da una determinata origine (o più origini) dati e indica quale forma e organizzazione devono avere i dati restituiti. Una query è distinta dai risultati che produce.  
  
 In genere, i dati di origine vengono organizzati logicamente come una sequenza di elementi dello stesso tipo. Ad esempio, una tabella di database SQL contiene una sequenza di righe. In un file XML è presente una "sequenza" di elementi XML, anche se questi sono organizzati gerarchicamente in una struttura ad albero. Una raccolta in memoria contiene una sequenza di oggetti. 
  
 Dal punto di vista di un'applicazione, il tipo e la struttura specifici dei dati di origine non è importante. L'applicazione considera sempre i dati di origine come raccolta <xref:System.Collections.Generic.IEnumerable%601> o <xref:System.Linq.IQueryable%601>. In LINQ to XML i dati di origine ad esempio sono resi visibili come oggetto `IEnumerable` \< <xref:System.Xml.Linq.XElement>>.  
  
 Data questa sequenza di origine, una query può eseguire una delle tre operazioni seguenti:  
  
-   Recuperare un subset di elementi per produrre una nuova sequenza senza modificare i singoli elementi. La query può quindi ordinare o raggruppare la sequenza restituita in vari modi, come illustrato nell'esempio seguente (si presuppone che `scores` sia un elemento `int[]`):  
  
     [!code-cs[csrefQueryExpBasics#45](../../../samples/snippets/csharp/concepts/linq/query-expression-basics_1.cs)]  
  
-   Recuperare una sequenza di elementi come nell'esempio precedente, ma trasformandoli in un nuovo tipo di oggetto. Ad esempio, una query può recuperare solo i cognomi da determinati record cliente in un'origine dati. Oppure può recuperare il record completo e quindi usarlo per creare un altro tipo di oggetto in memoria o anche dati XML prima di generare la sequenza di risultati finale. L'esempio seguente illustra una proiezione da `int` a `string`. Si noti il nuovo tipo di `highScoresQuery`.  
  
     [!code-cs[csrefQueryExpBasics#46](../../../samples/snippets/csharp/concepts/linq/query-expression-basics_2.cs)]  
  
-   Recuperare un valore singleton sui dati di origine, ad esempio:  
  
    -   Il numero di elementi che corrispondono a una determinata condizione.  
  
    -   L'elemento con il valore massimo o minimo.  
  
    -   Il primo elemento che corrisponde a una condizione o la somma di particolari valori in un set specificato di elementi. Ad esempio, la query seguente restituisce il numero di punteggi superiori a 80 dalla matrice di interi `scores`:  
  
     [!code-cs[csrefQueryExpBasics#47](../../../samples/snippets/csharp/concepts/linq/query-expression-basics_3.cs)]  
  
     Nell'esempio precedente si noti l'uso delle parentesi attorno all'espressione di query prima della chiamata al metodo `Count`. Un'espressione analoga è usare una nuova variabile per archiviare il risultato concreto. Questa tecnica è più leggibile perché mantiene la variabile che contiene la query separata dalla query che archivia un risultato.  
  
     [!code-cs[csrefQueryExpBasics#48](../../../samples/snippets/csharp/concepts/linq/query-expression-basics_4.cs)]  
  
 Nell'esempio precedente la query viene eseguita nella chiamata a `Count`, poiché `Count` deve eseguire l'iterazione dei risultati per determinare il numero di elementi restituiti da `highScoresQuery`.  
  
## <a name="what-is-a-query-expression"></a>Che cos'è un'espressione di query?  

 Un'*espressione di query* è una query espressa nella sintassi delle query. È un costrutto di linguaggio di prima classe. È esattamente come qualsiasi altra espressione e può essere usata in qualsiasi contesto in cui un'espressione C# è valida. Un'espressione di query consiste in un set di clausole scritte in una sintassi dichiarativa simile a SQL o XQuery. Ogni clausola contiene a sua volta una o più espressioni C# e queste espressioni possono essere espressioni di query o contenere un'espressione di query.  
  
 Un'espressione di query deve iniziare con una clausola [from](../language-reference/keywords/from-clause.md) e terminare con una clausola [select](../language-reference/keywords/select-clause.md) o [group](../language-reference/keywords/group-clause.md). Tra la prima clausola `from` e l'ultima clausola `select` o `group` può contenere una o più delle seguenti clausole facoltative: [where](../language-reference/keywords/where-clause.md), [orderby](../language-reference/keywords/orderby-clause.md), [join](../language-reference/keywords/join-clause.md), [let](../language-reference/keywords/let-clause.md) e anche clausole [from](../language-reference/keywords/from-clause.md) aggiuntive. È anche possibile usare la parola chiave [into](../language-reference/keywords/into.md) per consentire al risultato di una clausola `join` o `group` di funzionare come origine per le clausole di query aggiuntive nella stessa espressione di query.  
  
### <a name="query-variable"></a>Variabile di query  
 
 In LINQ una variabile di query è qualsiasi variabile che archivia una *query* anziché i *risultati* di una query. In particolare, una variabile di query è sempre un tipo enumerabile che genera una sequenza di elementi quando viene iterato in un'istruzione `foreach` o una chiamata diretta al relativo metodo `IEnumerator.MoveNext`.  
  
 L'esempio di codice seguente illustra un'espressione di query semplice con un'origine dati, una clausola di filtro, una clausola di ordinamento e nessuna trasformazione degli elementi di origine. La clausola `select` termina la query.  
  
 [!code-cs[csrefQueryExpBasics#49](../../../samples/snippets/csharp/concepts/linq/query-expression-basics_5.cs)]  
  
 Nell'esempio precedente `scoreQuery` è una *variabile di query,* che a volte viene definita semplicemente *query*. La variabile di query non archivia dati sul risultato effettivo, che vengono generati nel ciclo `foreach`. E quando viene eseguita l'istruzione `foreach` i risultati della query non vengono restituiti attraverso la variabile di query `scoreQuery`. Vengono piuttosto restituiti attraverso la variabile di iterazione `testScore`. La variabile `scoreQuery` può essere iterata in un secondo ciclo `foreach`. Verranno generati gli stessi risultati purché non siano state modificate né la variabile né l'origine dati.  
  
 Una variabile di query può archiviare una query espressa nella sintassi di query, nella sintassi di metodo o in una combinazione delle due. Negli esempi seguenti sia `queryMajorCities` che `queryMajorCities2` sono variabili di query:  
  
 [!code-cs[csrefQueryExpBasics#50](../../../samples/snippets/csharp/concepts/linq/query-expression-basics_6.cs)]  
  
 I due esempi seguenti illustrano invece le variabili che non sono variabili di query anche se ognuna viene inizializzata con una query. Non sono variabili di query perché archiviano i risultati:  
  
 [!code-cs[csrefQueryExpBasics#51](../../../samples/snippets/csharp/concepts/linq/query-expression-basics_7.cs)]  
  
 Per altre informazioni sui diversi modi di esprimere le query, vedere [Sintassi di query e sintassi di metodi in LINQ](../programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq.md).  
  
#### <a name="explicit-and-implicit-typing-of-query-variables"></a>Tipizzazione esplicita e implicita delle variabili di query  
 
 In questa documentazione viene usato in genere il tipo esplicito della variabile di query allo scopo di evidenziare la relazione di tipo tra la variabile di query e la [clausola select](../language-reference/keywords/select-clause.md). Tuttavia, è possibile usare anche la parola chiave [var](../language-reference/keywords/var.md) per indicare al compilatore di dedurre il tipo di una variabile di query, o qualsiasi altra variabile locale, in fase di compilazione. L'esempio di query illustrato in precedenza in questo argomento può essere espresso anche usando la tipizzazione implicita:  
  
 [!code-cs[csrefQueryExpBasics#52](../../../samples/snippets/csharp/concepts/linq/query-expression-basics_8.cs)]  
  
 Per altre informazioni, vedere [Variabili locali tipizzate in modo implicito](../programming-guide/classes-and-structs/implicitly-typed-local-variables.md) e [Relazioni tra i tipi nelle operazioni di query LINQ](../programming-guide/concepts/linq/type-relationships-in-linq-query-operations.md).  
  
### <a name="starting-a-query-expression"></a>Avviare un'espressione di query  
 
 Un'espressione di query deve iniziare con una clausola `from`. Specifica un'origine dati insieme a una variabile di intervallo. La variabile di intervallo rappresenta ogni elemento successivo nella sequenza di origine man mano che si attraversa la sequenza di origine. La variabile di intervallo è fortemente tipizzata in base al tipo di elementi nell'origine dati. Nell'esempio seguente, poiché `countries` è una matrice di oggetti `Country`, anche la variabile di intervallo è tipizzata come `Country`. Poiché la variabile di intervallo è fortemente tipizzata, è possibile usare l'operatore punto per accedere ai membri disponibili del tipo.  
  
 [!code-cs[csrefQueryExpBasics#53](../../../samples/snippets/csharp/concepts/linq/query-expression-basics_9.cs)]  
  
 La variabile di intervallo è nell'ambito finché la query viene terminata con un punto e virgola o con una clausola *continuation*.  
  
 Un'espressione di query può contenere più clausole `from`. Usare clausole `from` aggiuntive quando ogni elemento nella sequenza di origine è a sua volta una raccolta o contiene una raccolta. Ad esempio, si supponga di avere una raccolta di oggetti `Country`, ognuna delle quali contiene una raccolta di oggetti `City` denominata `Cities`. Per eseguire query sugli oggetti `City` in ogni `Country`, usare due clausole `from` come illustrato di seguito:  
  
 [!code-cs[csrefQueryExpBasics#54](../../../samples/snippets/csharp/concepts/linq/query-expression-basics_10.cs)]  
  
 Per altre informazioni, vedere [Clausola from](../language-reference/keywords/from-clause.md).  
  
### <a name="ending-a-query-expression"></a>Terminare un'espressione di query  
 
 Un'espressione di query deve terminare con una clausola `group` o una clausola `select`.  
  
#### <a name="group-clause"></a>Clausola group  
 
 Usare la clausola `group` per produrre una sequenza di gruppi organizzata in base a una chiave specificata. La chiave può essere qualsiasi tipo di dati. Ad esempio, la query seguente crea una sequenza di gruppi che contiene uno o più oggetti `Country` e la cui chiave è un valore `char`.  
  
 [!code-cs[csrefQueryExpBasics#55](../../../samples/snippets/csharp/concepts/linq/query-expression-basics_11.cs)]  
  
 Per altre informazioni sul raggruppamento, vedere [Clausola group](../language-reference/keywords/group-clause.md).  
  
#### <a name="select-clause"></a>Clausola select  
 Usare la clausola `select` per creare tutti gli altri tipi di sequenze. Una clausola `select` semplice produce una sequenza usando lo stesso tipo di oggetti dell'origine dati. In questo esempio l'origine dati contiene oggetti `Country`. La clausola `orderby` si limita a ordinare gli elementi in base a un nuovo ordine e la clausola `select` produce una sequenza degli oggetti `Country` riordinati.  
  
 [!code-cs[csrefQueryExpBasics#56](../../../samples/snippets/csharp/concepts/linq/query-expression-basics_12.cs)]  
  
 La clausola `select` può essere usata per trasformare i dati di origine in sequenze di nuovi tipi. Questa trasformazione è detta anche *proiezione*. Nell'esempio seguente la clausola `select` *proietta* una sequenza di tipi anonimi che contiene solo un subset dei campi dell'elemento originale. Si noti che i nuovi oggetti vengono inizializzati usando un inizializzatore di oggetto.  
  
 [!code-cs[csrefQueryExpBasics#57](../../../samples/snippets/csharp/concepts/linq/query-expression-basics_13.cs)]  
  
 Per altre informazioni su tutti i modi in cui una clausola `select` può essere usata per trasformare i dati di origine, vedere [Clausola select](../language-reference/keywords/select-clause.md).  
  
#### <a name="continuations-with-into"></a>Continuazioni con "into"  
 
 È possibile usare la parola chiave `into` in una clausola `select` o `group` per creare un identificatore temporaneo che archivia una query. Eseguire questa operazione quando è necessario eseguire altre operazioni di query per una query dopo un'operazione di raggruppamento o selezione. Nell'esempio seguente `countries` indica i paesi raggruppati in base alla popolazione in intervalli di 10 milioni. Dopo avere creato questi gruppi, le clausole aggiuntive escludono alcuni gruppi, quindi ordinano i gruppi in ordine crescente. Per eseguire le operazioni aggiuntive, è richiesta la continuazione rappresentata da `countryGroup`.  
  
 [!code-cs[csrefQueryExpBasics#58](../../../samples/snippets/csharp/concepts/linq/query-expression-basics_14.cs)]  
  
 Per altre informazioni, vedere [into](../language-reference/keywords/into.md).  
  
### <a name="filtering-ordering-and-joining"></a>Filtro, ordinamento e join

 Tra la clausola iniziale `from` e la clausola finale `select` o `group`, tutte le altre clausole (`where`, `join`, `orderby`, `from`, `let`) sono facoltative. Qualsiasi clausola facoltativa può essere usata zero o più volte nel corpo di una query.  
  
#### <a name="where-clause"></a>Clausola where  

 Usare la clausola `where` per escludere gli elementi dai dati di origine in base a una o più espressioni del predicato. La clausola `where` nell'esempio seguente include un predicato con due condizioni.  
  
 [!code-cs[csrefQueryExpBasics#59](../../../samples/snippets/csharp/concepts/linq/query-expression-basics_15.cs)]  
  
 Per altre informazioni, vedere [Clausola where](../language-reference/keywords/where-clause.md).  
  
#### <a name="orderby-clause"></a>Clausola orderby

 Usare la clausola `orderby` per ordinare i risultati in ordine crescente o decrescente. È anche possibile specificare gli ordinamenti secondari. Nell'esempio seguente viene eseguito un ordinamento primario per gli oggetti `country` usando la proprietà `Area`. Viene quindi eseguito un ordinamento secondario usando la proprietà `Population`.  
  
 [!code-cs[csrefQueryExpBasics#60](../../../samples/snippets/csharp/concepts/linq/query-expression-basics_16.cs)]  
  
 La parola chiave `ascending` è facoltativa, ma consente l'ordinamento predefinito se non viene specificato alcun ordine. Per altre informazioni, vedere [Clausola orderby](../language-reference/keywords/orderby-clause.md).  
  
#### <a name="join-clause"></a>Clausola join

 Usare la clausola `join` per associare e/o combinare gli elementi di un'origine dati con gli elementi di un'altra origine dati in base a un confronto di uguaglianza tra le chiavi specificate in ogni elemento. In LINQ le operazioni di join vengono eseguite su sequenze di oggetti i cui elementi sono tipi diversi. Dopo avere unito due sequenze, è necessario usare un'istruzione `select` o `group` per specificare l'elemento da archiviare nella sequenza di output. È anche possibile usare un tipo anonimo per combinare le proprietà da ogni set di elementi associati in un nuovo tipo per la sequenza di output. L'esempio seguente associa oggetti `prod` la cui proprietà `Category` corrisponde a una delle categorie nella matrice di stringhe `categories`. I prodotti il cui valore `Category` non corrisponde a una delle stringhe in `categories` vengono esclusi. L'istruzione `select` proietta un nuovo tipo le cui proprietà sono accettate sia da `cat` che da `prod`.  
  
 [!code-cs[csrefQueryExpBasics#61](../../../samples/snippets/csharp/concepts/linq/query-expression-basics_17.cs)]  
  
 È anche possibile creare un join di gruppo archiviando i risultati dell'operazione `join` in una variabile temporanea usando la parola chiave [into](../language-reference/keywords/into.md). Per altre informazioni, vedere [Clausola join](../language-reference/keywords/join-clause.md).  
  
#### <a name="let-clause"></a>Clausola let 

 Usare la clausola `let` per archiviare il risultato di un'espressione, ad esempio una chiamata al metodo, in una nuova variabile di intervallo. Nell'esempio seguente la variabile di intervallo `firstName` archivia il primo elemento della matrice di stringhe restituita da `Split`.  
  
 [!code-cs[csrefQueryExpBasics#62](../../../samples/snippets/csharp/concepts/linq/query-expression-basics_18.cs)]  
  
 Per altre informazioni, vedere [Clausola let](../language-reference/keywords/let-clause.md).  
  
### <a name="subqueries-in-a-query-expression"></a>Sottoquery in un'espressione di query  

 Una clausola di query può contenere un'espressione di query, a volte detta *sottoquery*. Ogni sottoquery inizia con la propria clausola `from` che non fa necessariamente riferimento alla stessa origine dati nella prima clausola `from`. Ad esempio, la query seguente rappresenta un'espressione di query usate nell'istruzione select per recuperare i risultati di un'operazione di raggruppamento.  
  
 [!code-cs[csrefQueryExpBasics#63](../../../samples/snippets/csharp/concepts/linq/query-expression-basics_19.cs)]  
  
 Per altre informazioni, vedere [Procedura: Eseguire una sottoquery su un'operazione di raggruppamento](perform-a-subquery-on-a-grouping-operation.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Guida per programmatori C#](../programming-guide/index.md)   
 [Espressioni di query LINQ](index.md)   
 [Parole chiave di query (LINQ)](../language-reference/keywords/query-keywords.md)   
 [Standard query operators overview](../programming-guide/concepts/linq/standard-query-operators-overview.md) (Panoramica degli operatori di query standard)

