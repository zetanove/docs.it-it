---
title: Relazioni tra i tipi nelle operazioni di Query (Visual Basic) | Documenti di Microsoft
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
- variable relationships [LINQ in Visual Basic]
- type information inferred [LINQ in Visual Basic]
- type relationships [LINQ in Visual Basic]
- queries [LINQ in Visual Basic], type relationships
- data sources [LINQ in Visual Basic], type relationships
- LINQ [Visual Basic], type relationships
- inferring type information [LINQ in Visual Basic]
- relationships [LINQ in Visual Basic]
ms.assetid: b5ff4da5-f3fd-4a8e-aaac-1cbf52fa16f6
caps.latest.revision: 34
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
ms.openlocfilehash: a966b69feca7a7021cafbccb7971913ea781c479
ms.lasthandoff: 03/13/2017

---
# <a name="type-relationships-in-query-operations-visual-basic"></a>Relazioni tra i tipi nelle operazioni di query (Visual Basic)
Le variabili utilizzate nella [!INCLUDE[vbteclinqext](../../../../csharp/getting-started/includes/vbteclinqext_md.md)] query operazioni sono fortemente tipizzate e devono essere compatibili tra loro. Tipizzazione forte viene utilizzata nell'origine dati, nella query stessa e nell'esecuzione della query. Nella figura seguente identifica i termini utilizzati per descrivere un [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] query. Per ulteriori informazioni sulle parti di una query, vedere [Basic Query Operations (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/basic-query-operations.md).  
  
 ![Query pseudocodice con elementi evidenziati.](../../../../visual-basic/programming-guide/concepts/linq/media/sjltyperels.png "SJLtypeRels")  
Parti di una query LINQ  
  
 Il tipo della variabile di intervallo nella query deve essere compatibile con il tipo degli elementi nell'origine dati. Il tipo della variabile di query deve essere compatibile con l'elemento della sequenza definito nel `Select` clausola. Infine, il tipo degli elementi sequenza inoltre deve essere compatibile con il tipo della variabile di controllo del ciclo che viene utilizzata per il `For Each` istruzione che esegue la query. Questa tipizzazione forte semplifica l'identificazione degli errori di tipo in fase di compilazione.  
  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]tipizzazione forte viene applicata implementando l'inferenza del tipo locale, noto anche come *la tipizzazione implicita*. Funzionalità viene utilizzata nell'esempio precedente, che verrà utilizzato in tutta la [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] esempi e documentazione. In Visual Basic, l'inferenza del tipo locale viene eseguita utilizzando semplicemente un `Dim` istruzione senza un `As` clausola. Nell'esempio seguente, `city` è fortemente tipizzata come una stringa.  
  
 [!code-vb[VbLINQTypeRels n.&1;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/type-relationships-in-query-operations_1.vb)]  
  
> [!NOTE]
>  Inferenza del tipo locale funziona solo quando `Option Infer` è impostato su `On`. Per ulteriori informazioni, vedere [Option Infer Statement](../../../../visual-basic/language-reference/statements/option-infer-statement.md).  
  
 Tuttavia, anche se si utilizza l'inferenza del tipo locale in una query, le stesse relazioni di tipo presenti tra le variabili nell'origine dati, la variabile di query e il ciclo di esecuzione di query. È utile avere una conoscenza di base di queste relazioni di tipo durante la scrittura di [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] query o utilizzano gli esempi e gli esempi di codice nella documentazione.  
  
 Si potrebbe essere necessario specificare un tipo esplicito per una variabile di intervallo che corrisponde al tipo restituito dall'origine dati. È possibile specificare il tipo della variabile di intervallo mediante un `As` clausola. Tuttavia, questo comporta un errore se la conversione è un [conversione di restrizione](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md) e `Option Strict` è impostato su `On`. È pertanto consigliabile eseguire la conversione di valori recuperati dall'origine dati. È possibile convertire i valori dall'origine dati per il tipo di variabile di intervallo esplicito utilizzando il <xref:System.Linq.Enumerable.Cast%2A>(metodo).</xref:System.Linq.Enumerable.Cast%2A> È anche possibile convertire i valori selezionati nel `Select` clausola per un tipo esplicito diverso dal tipo della variabile di intervallo. Nel codice seguente sono illustrati questi punti.  
  
 [!code-vb[VbLINQTypeRels n.&4;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/type-relationships-in-query-operations_2.vb)]  
  
## <a name="queries-that-return-entire-elements-of-the-source-data"></a>Query che restituiscono gli elementi completi dei dati di origine  
 Nell'esempio seguente un [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] operazione che restituisce una sequenza di elementi selezionati dall'origine dei dati di query. L'origine, `names`, contiene una matrice di stringhe, e l'output della query è una sequenza contenente stringhe che iniziano con la lettera M.  
  
 [!code-vb[VbLINQTypeRels n.&2;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/type-relationships-in-query-operations_3.vb)]  
  
 Questo è equivalente al codice seguente, ma è molto più breve e facile da scrivere. Affidarsi all'inferenza del tipo locale nelle query sono lo stile preferito in Visual Basic.  
  
 [!code-vb[VbLINQTypeRels n.&3;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/type-relationships-in-query-operations_4.vb)]  
  
 Le relazioni seguenti disponibili in entrambi gli esempi di codice precedenti, se i tipi sono determinati in modo implicito o esplicito.  
  
1.  Il tipo degli elementi nell'origine dati, `names`, è il tipo della variabile di intervallo, `name`, nella query.  
  
2.  Il tipo di oggetto selezionato, `name`, determina il tipo della variabile di query, `mNames`. Qui `name` è una stringa, pertanto la variabile di query è IEnumerable (Of String) in Visual Basic.  
  
3.  La query definita in `mNames` viene eseguita nel `For Each` ciclo. Il ciclo scorre il risultato dell'esecuzione della query. Poiché `mNames`, quando eseguita, restituisce una sequenza di stringhe, la variabile di iterazione del ciclo, `nm`, inoltre è una stringa.  
  
## <a name="queries-that-return-one-field-from-selected-elements"></a>Query che restituiscono un singolo campo dagli elementi selezionati  
 Nell'esempio seguente un [!INCLUDE[vbtecdlinq](../../../../csharp/includes/vbtecdlinq_md.md)] operazione che restituisce una sequenza contenente solo una parte di ogni elemento selezionato dall'origine dati di query. La query accetta una raccolta di `Customer` oggetti come origine dati e solo per i progetti di `Name` proprietà nel risultato. Poiché il nome del cliente è una stringa, la query genera una sequenza di stringhe come output.  
  
<CodeContentPlaceHolder>0</CodeContentPlaceHolder>  
 Le relazioni tra le variabili sono analoghe a quelle di esempio più semplice.  
  
1.  Il tipo degli elementi nell'origine dati, `customers`, è il tipo della variabile di intervallo, `cust`, nella query. In questo esempio, il tipo è `Customer`.  
  
2.  Il `Select` istruzione restituisce il `Name` proprietà di ogni `Customer` oggetto anziché l'intero oggetto. Poiché `Name` è una stringa, la variabile di query, `custNames`, saranno ancora IEnumerable (Of String), non di `Customer`.  
  
3.  Poiché `custNames` rappresenta una sequenza di stringhe, il `For Each` variabile di iterazione del ciclo, `custName`, deve essere una stringa.  
  
 Senza l'inferenza del tipo locale, l'esempio precedente sarebbe più complesso da scrivere e da comprendere, come illustrato nell'esempio seguente.  
  
<CodeContentPlaceHolder>1</CodeContentPlaceHolder>  
## <a name="queries-that-require-anonymous-types"></a>Query che richiedono tipi anonimi  
 Nell'esempio seguente viene illustrata una situazione più complessa. Nell'esempio precedente, non era utile specificare tipi per tutte le variabili in modo esplicito. In questo esempio, è impossibile. Anziché selezionare intero `Customer` gli elementi dall'origine dati o un singolo campo da ogni elemento, il `Select` clausola in questa query restituisce due proprietà dell'originale `Customer` oggetto: `Name` e `City`. In risposta al `Select` clausola, il compilatore definisce un tipo anonimo che contiene queste due proprietà. Il risultato dell'esecuzione `nameCityQuery` nel `For Each` ciclo è una raccolta di istanze del nuovo tipo anonimo. Poiché il tipo anonimo dispone di un nome utilizzabile, è possibile specificare il tipo di `nameCityQuery` o `custInfo` in modo esplicito. Ovvero, con un tipo anonimo, non disponibile alcun nome del tipo da utilizzare al posto di `String` in `IEnumerable(Of String)`. Per ulteriori informazioni, vedere [tipi anonimi](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md).  
  
<CodeContentPlaceHolder>2</CodeContentPlaceHolder>  
 Anche se non è possibile specificare tipi per tutte le variabili nell'esempio precedente, le relazioni rimangono invariati.  
  
1.  Il tipo degli elementi nell'origine dati è anche in questo caso il tipo della variabile di intervallo nella query. In questo esempio, `cust` è un'istanza di `Customer`.  
  
2.  Poiché il `Select` istruzione produce un tipo anonimo, la variabile di query, `nameCityQuery`, devono essere digitati in modo implicito come tipo anonimo. Un tipo anonimo ha un nome utilizzabile e pertanto non può essere specificato in modo esplicito.  
  
3.  Il tipo della variabile di iterazione nel `For Each` ciclo è di tipo anonimo creata nel passaggio 2. Poiché il tipo ha un nome utilizzabile, il tipo della variabile di iterazione del ciclo deve essere determinato in modo implicito.  
  
## <a name="see-also"></a>Vedere anche  
 [Introduzione a LINQ in Visual Basic](../../../../visual-basic/programming-guide/concepts/linq/getting-started-with-linq.md)   
 [Tipi anonimi](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)   
 [Inferenza del tipo locale](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [Introduzione a LINQ in Visual Basic](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)   
 [Query](../../../../visual-basic/language-reference/queries/queries.md)
