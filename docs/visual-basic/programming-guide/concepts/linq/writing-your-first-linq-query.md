---
title: "Scrittura della prima query LINQ (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
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
  - "query [LINQ in Visual Basic], scrittura"
  - "query LINQ [Visual Basic]"
  - "LINQ [Visual Basic], scrittura di query"
ms.assetid: 4affb732-3e9b-4479-aa31-1f9bd8183cbe
caps.latest.revision: 56
caps.handback.revision: 54
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Scrittura della prima query LINQ (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Una *query* è un'espressione che recupera dati da un'origine dati.  Le query sono espresse in un linguaggio di query dedicato.  Nel tempo sono stati sviluppati diversi linguaggi per i vari tipi di origini dati, ad esempio SQL per database relazionali e XQuery per XML.  Lo sviluppatore di applicazioni deve pertanto imparare un nuovo linguaggio di query per ogni tipo di origine dati o formato dati supportato.  
  
 [!INCLUDE[vbteclinqext](../../../../csharp/getting-started/includes/vbteclinqext_md.md)] semplifica la situazione offrendo un modello coerente per l'utilizzo dei dati con tutti i diversi tipi di origini e formati dati.  In una query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] vengono utilizzati sempre gli oggetti.  Vengono utilizzati gli stessi modelli di codifica di base per eseguire una query e trasformare i dati in documenti XML, database SQL, dataset ed entità ADO.NET, raccolte .NET Framework e qualsiasi altra origine o formato per cui sia disponibile un provider [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)].  In questo documento vengono illustrate le tre fasi della creazione e dell'utilizzo delle query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] di base.  
  
 ![Collegamento a video](../../../../csharp/programming-guide/concepts/linq/media/playvideo.png "PlayVideo") Per la dimostrazione video correlata, vedere [Ricerca per categorie: Introduzione a LINQ](http://go.microsoft.com/fwlink/?LinkId=133021).  
  
## Tre fasi di un'operazione di query  
 Le operazioni di query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] sono costituite da tre azioni:  
  
1.  Ottenere l'origine o le origini dati.  
  
2.  Creare la query.  
  
3.  Eseguire la query.  
  
 In [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] l'esecuzione di una query è distinta dalla creazione della query.  I dati non vengono recuperati solo creando una query.  Questo punto viene illustrato più dettagliatamente in seguito in questo argomento.  
  
 Nell'esempio riportato di seguito vengono illustrate le tre parti di un'operazione di query.  Nell'esempio viene utilizzata una matrice di valori interi come pratica origine dati a mero scopo esemplificativo.  Gli stessi concetti si applicano però anche ad altre origini dati.  
  
> [!NOTE]
>  In [Compilazione \(pagina\), Creazione progetti \(Visual Basic\)](/visual-studio/ide/reference/compile-page-project-designer-visual-basic), assicurarsi che **Option Infer** è impostato su **In**.  
  
 [!code-vb[VbLINQFirstQuery#1](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/writing-your-first-linq-query_1.vb)]  
  
 Output:  
  
 `0 2 4 6`  
  
## Origine dati  
 Poiché nell'esempio precedente è stata utilizzata una matrice come origine dati, viene supportata implicitamente l'interfaccia generica <xref:System.Collections.Generic.IEnumerable%601>.  Per questo motivo è possibile utilizzare una matrice come origine dati per una query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)].  I tipi che supportano <xref:System.Collections.Generic.IEnumerable%601> o un'interfaccia derivata come <xref:System.Linq.IQueryable%601> generico sono denominati *tipi queryable*.  
  
 Come tipo queryable in modo implicito, la matrice non richiede alcuna modifica o trattamento speciale per essere utilizzata come origine dati [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)].  Lo stesso vale per qualsiasi tipo di raccolta che supporta <xref:System.Collections.Generic.IEnumerable%601>, inclusi <xref:System.Collections.Generic.List%601>generico, <xref:System.Collections.Generic.Dictionary%602>e altre classi nella libreria di classi.NET Framework.  
  
 Se i dati di origine non implementano <xref:System.Collections.Generic.IEnumerable%601>, di un provider di [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] è necessario per implementare la funzionalità degli *operatori di query standard* per l'origine dati.  Ad esempio, [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] gestisce il caricamento di un documento XML in un tipo <xref:System.Xml.Linq.XElement> queryable, come illustrato nell'esempio seguente.  Per ulteriori informazioni sugli operatori di query standard, vedere [Standard Query Operators Overview](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md).  
  
 [!code-vb[VbLINQFirstQuery#2](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/writing-your-first-linq-query_2.vb)]  
  
 Con [!INCLUDE[vbtecdlinq](../../../../csharp/includes/vbtecdlinq_md.md)] è necessario creare prima un mapping relazionale a oggetti in fase di progettazione, manualmente o utilizzando [Progettazione relazionale oggetti](/visual-studio/data-tools/linq-to-sql-tools-in-visual-studio2).  È possibile quindi scrivere le query sugli oggetti e in fase di esecuzione [!INCLUDE[vbtecdlinq](../../../../csharp/includes/vbtecdlinq_md.md)] gestisce la comunicazione con il database.  Nell'esempio seguente `customers` rappresenta una tabella specifica nel database e <xref:System.Data.Linq.Table%601> supporta l'interfaccia generica <xref:System.Linq.IQueryable%601>.  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
 Per ulteriori informazioni sulla creazione di tipi specifici di origini dati, vedere la documentazione dei diversi provider [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)].  Per un elenco di questi provider, vedere [LINQ \(Language\-Integrated Query\)](../Topic/LINQ%20\(Language-Integrated%20Query\).md). La regola di base è semplice: un'origine dati [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] è rappresentata da qualsiasi oggetto che supporti l'interfaccia generica <xref:System.Collections.Generic.IEnumerable%601> o un'interfaccia da essa ereditata.  
  
> [!NOTE]
>  È inoltre possibile utilizzare come origini dati [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] i tipi quali <xref:System.Collections.ArrayList>, che supportano l'interfaccia non generica <xref:System.Collections.IEnumerable>.  Per un esempio che utilizza un oggetto <xref:System.Collections.ArrayList>, vedere [How to: Query an ArrayList with LINQ](../Topic/How%20to:%20Query%20an%20ArrayList%20with%20LINQ.md).  
  
## Query  
 Nella query vengono specificate le informazioni da recuperare dall'origine o dalle origini dati.  È inoltre possibile specificare il modo in cui ordinare, raggruppare o strutturare le informazioni prima che vengano restituite.  Per consentire la creazione della query, Visual Basic ha incorporato una nuova sintassi della query nel linguaggio.  
  
 Quando viene eseguita, la query dell'esempio seguente restituisce tutti i numeri pari da una matrice di valori interi, `numbers`.  
  
 [!code-vb[VbLINQFirstQuery#1](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/writing-your-first-linq-query_1.vb)]  
  
 L'espressione di query contiene tre clausole: `From`, `Where` e `Select`.  La funzione e lo scopo specifici di ogni clausola dell'espressione di query vengono illustrati in [Operazioni di query di base \(Visual Basic\)](../../../../visual-basic/programming-guide/concepts/linq/basic-query-operations.md).  Per ulteriori informazioni, vedere [Queries](../../../../visual-basic/language-reference/queries/queries.md).  Tenere presente che in [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] una definizione di query viene spesso archiviata in una variabile ed eseguita successivamente.  La variabile di query, ad esempio `evensQuery` nell'esempio precedente, deve essere un tipo queryable. Il tipo di `evensQuery` è `IEnumerable(Of Integer)`, assegnato dal compilatore mediante l'inferenza del tipo di variabile locale.  
  
 È importante tenere presente che la variabile di query stessa non effettua alcuna azione e non restituisce dati.  Archivia solo la definizione della query.  Nell'esempio precedente è il ciclo `For Each` che esegue la query.  
  
## Esecuzione della query  
 L'esecuzione della query è distinta dalla creazione della query.  La creazione della query definisce la query, mentre l'esecuzione viene attivata da un meccanismo diverso.  Una query può essere eseguita appena definita \(*esecuzione immediata*\) oppure è possibile archiviare la definizione ed eseguire la query in un secondo momento \(*esecuzione posticipata*\).  
  
### Esecuzione posticipata  
 Una tipica query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] è analoga a quella riportata nell'esempio precedente in cui è stata definita la variabile di query `evensQuery`.  La query viene creata ma non eseguita immediatamente.  La definizione della query viene invece archiviata nella variabile di query `evensQuery`.  La query viene eseguita successivamente, in genere utilizzando un ciclo `For Each` che restituisce una sequenza di valori o applicando un operatore di query standard, ad esempio `Count` o `Max`.  Questo processo viene denominato *esecuzione posticipata*.  
  
 [!code-vb[VbLINQFirstQuery#7](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/writing-your-first-linq-query_3.vb)]  
  
 Per una sequenza di valori è possibile accedere ai dati recuperati utilizzando la variabile di iterazione nel ciclo `For Each` \(`number` nell'esempio precedente\).  Poiché la variabile di query, `evensQuery`, contiene la definizione della query invece dei risultati della query, è possibile eseguire una query un numero illimitato di volte utilizzando la variabile di query più volte.  Ad esempio, è possibile avere un database nell'applicazione che viene aggiornato continuamente mediante un'applicazione separata.  Dopo avere creato una query che recupera i dati da tale database, è possibile utilizzare un ciclo `For Each` per eseguire ripetutamente la query, recuperando ogni volta i dati più recenti.  
  
 Nell'esempio seguente viene illustrato l'utilizzo dell'esecuzione posticipata.  Dopo aver definito ed eseguito `evensQuery2` con un ciclo `For Each`, come negli esempi precedenti, vengono modificati alcuni elementi nell'origine dati `numbers`.  Un secondo ciclo `For Each` esegue quindi nuovamente `evensQuery2`.  La seconda volta i risultati sono diversi, poiché il ciclo `For Each` esegue nuovamente la query utilizzando i nuovi valori di `numbers`.  
  
 [!code-vb[VbLINQFirstQuery#3](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/writing-your-first-linq-query_4.vb)]  
  
 Output:  
  
 `Evens in original array:`  
  
 `0 2 4 6`  
  
 `Evens in changed array:`  
  
 `0 10 2 22 8`  
  
### Esecuzione immediata  
 Nell'esecuzione posticipata delle query la definizione della query viene archiviata in una variabile di query in modo da essere eseguita successivamente.  Nell'esecuzione immediata la query viene eseguita al momento della definizione.  L'esecuzione viene attivata quando si applica un metodo che richiede l'accesso ai singoli elementi del risultato della query.  L'esecuzione immediata viene spesso forzata utilizzando uno degli operatori di query standard che restituiscono singoli valori,  ad esempio `Count`, `Max`, `Average` e `First`.  Questi operatori di query standard eseguono la query appena vengono applicati in modo da calcolare e restituire un risultato singleton.  Per ulteriori informazioni sugli operatori di query standard che restituiscono singoli valori, vedere [Aggregation Operations](../../../../visual-basic/programming-guide/concepts/linq/aggregation-operations.md), [Element Operations](../../../../visual-basic/programming-guide/concepts/linq/element-operations.md) e [Quantifier Operations](../../../../visual-basic/programming-guide/concepts/linq/quantifier-operations.md).  
  
 Nella query seguente viene restituito un conteggio dei numeri pari in una matrice di valori interi.  La definizione della query non viene salvata e `numEvens` è un semplice oggetto `Integer`.  
  
 [!code-vb[VbLINQFirstQuery#4](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/writing-your-first-linq-query_5.vb)]  
  
 È possibile ottenere lo stesso risultato utilizzando il metodo `Aggregate`.  
  
 [!code-vb[VbLINQFirstQuery#5](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/writing-your-first-linq-query_6.vb)]  
  
 È inoltre possibile forzare l'esecuzione di una query chiamando il metodo `ToList` o `ToArray` su una query \(esecuzione immediata\) o una variabile di query \(esecuzione posticipata\), come illustrato nel codice seguente.  
  
 [!code-vb[VbLINQFirstQuery#6](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/writing-your-first-linq-query_7.vb)]  
  
 Negli esempi precedenti `evensQuery3` è una variabile di query, mentre `evensList` è un elenco e `evensArray` è una matrice.  
  
 L'utilizzo di `ToList` o `ToArray` per forzare l'esecuzione immediata è particolarmente utile negli scenari in cui si desidera eseguire immediatamente la query e memorizzarne nella cache i risultati di un singolo oggetto della raccolta.  Per ulteriori informazioni su tali metodi, vedere [Converting Data Types](../../../../visual-basic/programming-guide/concepts/linq/converting-data-types.md).  
  
 È inoltre possibile eseguire una query utilizzando un metodo `IEnumerable`, ad esempio il metodo <xref:Microsoft.VisualBasic.Collection.System%23Collections%23IEnumerable%23GetEnumerator%2A>.  
  
## Dimostrazioni video correlate  
 [Ricerca per categorie: Introduzione a LINQ](http://go.microsoft.com/fwlink/?LinkId=133021)  
  
 [Procedura: scrittura di query in Visual Basic](http://go.microsoft.com/fwlink/?LinkID=100356)  
  
## Vedere anche  
 [Getting Started with LINQ in Visual Basic](../../../../visual-basic/programming-guide/concepts/linq/getting-started-with-linq.md)   
 [Esempi LINQ](../Topic/LINQ%20Samples.md)   
 [Cenni preliminari su Progettazione relazionale oggetti](../Topic/LINQ%20to%20SQL%20Tools%20in%20Visual%20Studio1.md)   
 [Local Type Inference](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [Standard Query Operators Overview](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)   
 [Introduction to LINQ in Visual Basic](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)   
 [Queries](../../../../visual-basic/language-reference/queries/queries.md)