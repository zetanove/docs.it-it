---
title: Scrittura della prima Query LINQ (Visual Basic) | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- queries [LINQ in Visual Basic], writing
- LINQ queries [Visual Basic]
- LINQ [Visual Basic], writing queries
ms.assetid: 4affb732-3e9b-4479-aa31-1f9bd8183cbe
caps.latest.revision: 56
author: stevehoag
ms.author: shoag
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
ms.openlocfilehash: 48f1c5e15654580b6e4d060860a0d7001af5e2ef
ms.lasthandoff: 03/13/2017

---
# <a name="writing-your-first-linq-query-visual-basic"></a>Scrittura della prima query LINQ (Visual Basic)
Oggetto *query* è un'espressione che recupera dati da un'origine dati. Le query sono espresse in un linguaggio di query dedicato. Nel corso del tempo, sono stati sviluppati diversi linguaggi per diversi tipi di origini dati, ad esempio, SQL per i database relazionali e XQuery per XML. Ciò rende necessario per lo sviluppatore dell'applicazione per informazioni su un nuovo linguaggio di query per ogni tipo di origine dati o formato dati è supportata.  
  
 [!INCLUDE[vbteclinqext](../../../../csharp/getting-started/includes/vbteclinqext_md.md)]semplifica la situazione offrendo un modello coerente per l'utilizzo di dati in diversi tipi di origini e formati dati. In un [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] query, sempre utilizzano gli oggetti. Utilizzare gli stessi modelli di codifica di base per eseguire query e trasformare i dati nei documenti XML, database SQL, DataSet ADO.NET e le entità, le raccolte di .NET Framework e qualsiasi altri origine o formato per il quale un [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] provider è disponibile. Questo documento vengono descritte le tre fasi della creazione e utilizzo di basic [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] query.  
  
## <a name="three-stages-of-a-query-operation"></a>Tre fasi di un'operazione di Query  
 [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)]le operazioni di query sono costituite da tre azioni:  
  
1.  Ottenere l'origine dati o origini.  
  
2.  Creare la query.  
  
3.  Eseguire la query.  
  
 In [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)], l'esecuzione di una query è distinta dalla creazione della query. Non si recuperano i dati solo tramite la creazione di una query. Questo punto viene trattato in dettaglio più avanti in questo argomento.  
  
 L'esempio seguente illustra le tre parti di un'operazione di query. L'esempio utilizza una matrice di interi come origine dati con facilità a scopo dimostrativo. Tuttavia, gli stessi concetti si applicano anche ad altre origini dati.  
  
> [!NOTE]
>  Nel [pagina Compila, Progettazione progetti (Visual Basic)](https://docs.microsoft.com/visualstudio/ide/reference/compile-page-project-designer-visual-basic), assicurarsi che **Option infer** è impostato su **su**.  
  
 [!code-vb[VbLINQFirstQuery n.&1;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/writing-your-first-linq-query_1.vb)]  
  
 Output:  
  
 `0 2 4 6`  
  
## <a name="the-data-source"></a>L'origine dati  
 Poiché l'origine dati nell'esempio precedente è una matrice, sono supportate in modo implicito generica <xref:System.Collections.Generic.IEnumerable%601>interfaccia.</xref:System.Collections.Generic.IEnumerable%601> È il fatto che consente di utilizzare una matrice come origine dati per un [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] query. Tipi che supportano la <xref:System.Collections.Generic.IEnumerable%601>o un'interfaccia derivata come generica <xref:System.Linq.IQueryable%601>vengono chiamati *tipi queryable*.</xref:System.Linq.IQueryable%601> </xref:System.Collections.Generic.IEnumerable%601>  
  
 Come un tipo queryable in modo implicito, la matrice non richiede alcuna modifica o trattamento speciale da utilizzare come un [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] origine dati. Lo stesso vale per qualsiasi tipo di insieme che supporta <xref:System.Collections.Generic.IEnumerable%601>, incluse le interfacce generiche <xref:System.Collections.Generic.List%601>, <xref:System.Collections.Generic.Dictionary%602>e altre classi nella libreria di classi .NET Framework.</xref:System.Collections.Generic.Dictionary%602> </xref:System.Collections.Generic.List%601> </xref:System.Collections.Generic.IEnumerable%601>  
  
 Se i dati di origine non implementano già <xref:System.Collections.Generic.IEnumerable%601>, un [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] è necessario per implementare la funzionalità del provider di *operatori di query standard* per l'origine dati.</xref:System.Collections.Generic.IEnumerable%601> Ad esempio, [!INCLUDE[sqltecxlinq](../../../../csharp/programming-guide/concepts/linq/includes/sqltecxlinq_md.md)] gestisce il caricamento di un documento XML in un tipo queryable <xref:System.Xml.Linq.XElement>digitare, come mostrato nell'esempio seguente.</xref:System.Xml.Linq.XElement> Per ulteriori informazioni sugli operatori di query standard, vedere [Panoramica di operatori Query Standard (Visual Basic)](standard-query-operators-overview.md).  
  
 [!code-vb[VbLINQFirstQuery n.&2;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/writing-your-first-linq-query_2.vb)]  
  
 Con [!INCLUDE[vbtecdlinq](../../../../csharp/includes/vbtecdlinq_md.md)], creare innanzitutto un mapping relazionale a oggetti in fase di progettazione, manualmente o utilizzando il [LINQ to SQL Tools in Visual Studio](https://docs.microsoft.com/visualstudio/data-tools/linq-to-sql-tools-in-visual-studio2) in Visual Studio. È possibile scrivere le query sugli oggetti e in fase di esecuzione [!INCLUDE[vbtecdlinq](../../../../csharp/includes/vbtecdlinq_md.md)] gestisce la comunicazione con il database. Nell'esempio seguente, `customers` rappresenta una specifica tabella nel database e <xref:System.Data.Linq.Table%601>supporta generico <xref:System.Linq.IQueryable%601>.</xref:System.Linq.IQueryable%601> </xref:System.Data.Linq.Table%601>  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
 Per ulteriori informazioni su come creare tipi specifici di origini dati, vedere la documentazione per i vari [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] provider. (Per un elenco di questi provider, vedere [LINQ (Language-Integrated Query)](http://msdn.microsoft.com/library/a73c4aec-5d15-4e98-b962-1274021ea93d).) La regola di base è semplice: un [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] origine dati è qualsiasi oggetto che supporta l' <xref:System.Collections.Generic.IEnumerable%601>interfaccia o un'interfaccia che eredita da tale ambito.</xref:System.Collections.Generic.IEnumerable%601>  
  
> [!NOTE]
>  Tipi, ad esempio <xref:System.Collections.ArrayList>che supportano non generica <xref:System.Collections.IEnumerable>interfaccia può essere utilizzata anche come [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] origini dati.</xref:System.Collections.IEnumerable> </xref:System.Collections.ArrayList> Per un esempio che utilizza un <xref:System.Collections.ArrayList>, vedere [procedura: eseguire Query su un ArrayList con LINQ (Visual Basic)](how-to-query-an-arraylist-with-linq.md).</xref:System.Collections.ArrayList>  
  
## <a name="the-query"></a>La Query  
 Nella query, è necessario specificare quali informazioni si desidera recuperare dall'origine dati o origini. È inoltre possibile specificare come tali informazioni devono essere ordinate, raggruppate o strutturate prima che venga restituito. Per abilitare la creazione della query, Visual Basic è stato incorporato nuova sintassi di query nel linguaggio.  
  
 Quando viene eseguita, la query nell'esempio seguente restituisce tutti i numeri pari da una matrice di interi, `numbers`.  
  
 [!code-vb[VbLINQFirstQuery n.&1;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/writing-your-first-linq-query_1.vb)]  
  
 L'espressione di query contiene tre clausole: `From`, `Where`, e `Select`. Viene illustrata la funzione specifica e lo scopo di ogni clausola dell'espressione di query in [Basic Query Operations (Visual Basic)](basic-query-operations.md). Per ulteriori informazioni, vedere [query](../../../../visual-basic/language-reference/queries/queries.md). Si noti che in [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)], una definizione di query viene spesso archiviata in una variabile ed eseguita in un secondo momento. La query variabile, ad esempio `evensQuery` nell'esempio precedente, deve essere un tipo queryable. Il tipo di `evensQuery` è `IEnumerable(Of Integer)`, assegnato dal compilatore mediante l'inferenza del tipo locale.  
  
 È importante ricordare che la variabile di query viene eseguita alcuna azione e non restituisce dati. Memorizza solo la definizione della query. Nell'esempio precedente, è il `For Each` ciclo che esegue la query.  
  
## <a name="query-execution"></a>Esecuzione di query  
 Esecuzione di query è distinta dalla creazione della query. Creazione della query definisce la query, ma viene attivata da un meccanismo diverso. Una query può essere eseguita non appena viene definito (*l'esecuzione immediata*), o può essere archiviata la definizione e la query può essere eseguita in un secondo momento (*esecuzione posticipata*).  
  
### <a name="deferred-execution"></a>Esecuzione posticipata  
 Una tipica [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] query simile a quello nell'esempio precedente, in cui `evensQuery` è definito. Crea la query, ma non la esegue immediatamente. Al contrario, la definizione di query viene archiviata nella variabile di query `evensQuery`. La query viene eseguita in un secondo momento, in genere utilizzando un `For Each` ciclo, che restituisce una sequenza di valori o applicando un operatore di query standard, ad esempio `Count` o `Max`. Questo processo è detto *esecuzione posticipata*.  
  
 [!code-vb[VbLINQFirstQuery&#7;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/writing-your-first-linq-query_3.vb)]  
  
 Per una sequenza di valori, accedere ai dati recuperati utilizzando la variabile di iterazione nel `For Each` ciclo (`number` nell'esempio precedente). Poiché la variabile di query, `evensQuery`, contiene la definizione della query anziché i risultati della query, è possibile eseguire una query ogni volta che si desidera utilizzare la variabile di query più di una volta. Ad esempio, potrebbe essere un database dell'applicazione che viene aggiornato continuamente da un'applicazione separata. Dopo aver creato una query che recupera dati dal database, è possibile utilizzare un `For Each` loop per eseguire ripetutamente la query, recuperando i dati più recenti ogni volta.  
  
 Nell'esempio seguente viene illustrata l'esecuzione posticipata funziona. Dopo aver `evensQuery2` definito ed eseguito con un `For Each` del ciclo, come negli esempi precedenti, alcuni elementi nell'origine dati `numbers` vengono modificati. Quindi un secondo `For Each` eseguito ciclo `evensQuery2` nuovamente. I risultati sono diversi la seconda volta, in quanto il `For Each` ciclo esegue nuovamente la query utilizzando i nuovi valori in `numbers`.  
  
 [!code-vb[VbLINQFirstQuery n.&3;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/writing-your-first-linq-query_4.vb)]  
  
 Output:  
  
 `Evens in original array:`  
  
 `0  2  4  6`  
  
 `Evens in changed array:`  
  
 `0  10  2  22  8`  
  
### <a name="immediate-execution"></a>Esecuzione immediata  
 Esecuzione posticipata di query, la definizione di query viene archiviata in una variabile di query per un'esecuzione successiva. In esecuzione immediata, la query viene eseguita al momento della relativa definizione. Esecuzione viene attivata quando si applica un metodo che richiede l'accesso ai singoli elementi del risultato della query. Spesso l'esecuzione immediata viene forzato utilizzando uno degli operatori di query standard che restituiscono valori singoli. Examples are `Count`, `Max`, `Average`, and `First`. Questi operatori di query standard eseguire la query non appena vengono applicate per calcolare e restituire un risultato singleton. Per ulteriori informazioni sugli operatori di query standard che restituiscono valori singoli, vedere [operazioni di aggregazione](aggregation-operations.md), [operazioni con elementi](element-operations.md), e [le operazioni del quantificatore](quantifier-operations.md).  
  
 La query seguente restituisce un conteggio dei numeri pari in una matrice di interi. La definizione della query non viene salvata e `numEvens` è un semplice `Integer`.  
  
 [!code-vb[VbLINQFirstQuery n.&4;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/writing-your-first-linq-query_5.vb)]  
  
 È possibile ottenere lo stesso risultato utilizzando il `Aggregate` metodo.  
  
 [!code-vb[VbLINQFirstQuery n.&5;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/writing-your-first-linq-query_6.vb)]  
  
 È inoltre possibile forzare l'esecuzione di una query chiamando la `ToList` o `ToArray` metodo su una query (esecuzione immediata) o una variabile di query (esecuzione posticipata), come illustrato nel codice seguente.  
  
 [!code-vb[6 VbLINQFirstQuery](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/writing-your-first-linq-query_7.vb)]  
  
 Negli esempi precedenti, `evensQuery3` è una query, variabile, ma `evensList` è riportato un elenco e `evensArray` è una matrice.  
  
 Utilizzando `ToList` o `ToArray` per forzare immediatamente l'esecuzione è particolarmente utile negli scenari in cui si desidera eseguire immediatamente la query e nella cache i risultati in un singolo oggetto collection. Per ulteriori informazioni su questi metodi, vedere [la conversione di tipi di dati](converting-data-types.md).  
  
 È anche possibile causare una query da eseguire utilizzando un `IEnumerable` metodo, ad esempio il <xref:Microsoft.VisualBasic.Collection.System%23Collections%23IEnumerable%23GetEnumerator%2A>(metodo).</xref:Microsoft.VisualBasic.Collection.System%23Collections%23IEnumerable%23GetEnumerator%2A>  
  
## <a name="see-also"></a>Vedere anche  
 [Introduzione a LINQ in Visual Basic](getting-started-with-linq.md)   
 [Inferenza del tipo locale](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [Cenni preliminari sugli operatori di Query standard (Visual Basic)](standard-query-operators-overview.md)   
 [Introduzione a LINQ in Visual Basic](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)   
 [Query](../../../../visual-basic/language-reference/queries/queries.md)
