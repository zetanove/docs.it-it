---
title: Operazioni di Query di base (Visual Basic) | Documenti di Microsoft
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
- data sources [LINQ in Visual Basic]
- Join clause [LINQ in Visual Basic]
- ordering data [LINQ in Visual Basic]
- projections [LINQ in Visual Basic]
- LINQ [Visual Basic], query operations
- Order By clause [LINQ in Visual Basic]
- joining data [LINQ in Visual Basic]
- queries [LINQ in Visual Basic], basic operations
- selecting data [LINQ in Visual Basic]
- Group By clause [LINQ in Visual Basic]
- grouping data [LINQ in Visual Basic]
- Select clause [LINQ in Visual Basic]
ms.assetid: 1146f6d0-fcb8-4f4d-8223-c9db52620d21
caps.latest.revision: 37
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
ms.openlocfilehash: 87ff9173b5ff72385c8ecdc3ff13735e7be2a21d
ms.lasthandoff: 03/13/2017

---
# <a name="basic-query-operations-visual-basic"></a>Operazioni di query di base (Visual Basic)
In questo argomento fornisce una breve introduzione a [!INCLUDE[vbteclinqext](../../../../csharp/getting-started/includes/vbteclinqext_md.md)] espressioni in Visual Basic e di alcuni tipi di operazioni eseguite in una query tipici. Per altre informazioni, vedere i seguenti argomenti:  
  
 [Introduzione a LINQ in Visual Basic](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)  
  
 [Query](../../../../visual-basic/language-reference/queries/queries.md)  
  
 [Procedura dettagliata: Scrittura di query in Visual Basic](../../../../visual-basic/programming-guide/concepts/linq/walkthrough-writing-queries.md)  
  
## <a name="specifying-the-data-source-from"></a>Specificare l'origine dati (da)  
 In un [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] query, il primo passaggio consiste nel specificare l'origine dati che si desidera eseguire una query. Pertanto, il `From` sempre in una query per primo. Operatori di query selezionano ed elaborano il risultato in base al tipo dell'origine.  
  
 [!code-vb[VbLINQBasicOps n.&1;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/basic-query-operations_1.vb)]  
  
 Il `From` clausola specifica l'origine dati, `customers`e un *variabile di intervallo*, `cust`. La variabile di intervallo è come una variabile di iterazione del ciclo, ad eccezione del fatto che in un'espressione di query, si verifica alcun iterazione effettiva. Quando viene eseguita la query, spesso utilizzando un `For Each` ciclo, la variabile di intervallo funge da riferimento a ogni elemento successivo in `customers`. Poiché il compilatore è in grado di dedurre il tipo di `cust`, non è necessario specificarlo in modo esplicito. Per esempi di query scritte con e senza la tipizzazione esplicita, vedere [relazioni tra i tipi nelle operazioni di Query (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/type-relationships-in-query-operations.md).  
  
 Per ulteriori informazioni sull'utilizzo di `From` clausola in Visual Basic, vedere [dalla clausola](../../../../visual-basic/language-reference/queries/from-clause.md).  
  
## <a name="filtering-data-where"></a>Filtraggio dei dati (in)  
 Probabilmente l'operazione di query più comune è un filtro sotto forma di un'espressione booleana. Quindi, la query restituisce solo gli elementi per cui l'espressione è true. Oggetto `Where` clausola viene utilizzata per eseguire l'applicazione di filtri. Il filtro specifica quali elementi nell'origine dati da includere nella sequenza risultante. Nell'esempio seguente, sono inclusi solo i clienti che dispongono di un indirizzo di Londra.  
  
 [!code-vb[VbLINQBasicOps n.&2;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/basic-query-operations_2.vb)]  
  
 È possibile utilizzare gli operatori logici, ad esempio `And` e `Or` per combinare le espressioni di filtro in un `Where` clausola. Ad esempio, per restituire solo i clienti di Londra e il cui nome è Devon, utilizzare il codice seguente:  
  
```vb  
Where cust.City = "London" And cust.Name = "Devon"   
```  
  
 Per restituire i clienti di Londra o Parigi, utilizzare il codice seguente:  
  
```vb  
Where cust.City = "London" Or cust.City = "Paris"   
```  
  
 Per ulteriori informazioni sull'utilizzo di `Where` clausola in Visual Basic, vedere [clausola Where](../../../../visual-basic/language-reference/queries/where-clause.md).  
  
## <a name="ordering-data-order-by"></a>Ordinamento di dati (Order By)  
 Spesso è utile ordinare i dati restituiti in un ordine particolare. Il `Order By` clausola consente di ordinare gli elementi della sequenza restituita per ordinare in base a una o più campi specificati. Ad esempio, la query seguente consente di ordinare i risultati in base la `Name` proprietà. Poiché `Name` è una stringa, i dati restituiti verranno ordinati in ordine alfabetico da a Z.  
  
 [!code-vb[VbLINQBasicOps n.&3;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/basic-query-operations_3.vb)]  
  
 Per ordinare i risultati in ordine inverso, da Z ad A, utilizzare il `Order By...Descending` clausola. Il valore predefinito è `Ascending` quando nessuno `Ascending` né `Descending` specificato.  
  
 Per ulteriori informazioni sull'utilizzo di `Order By` clausola in Visual Basic, vedere [clausola Order By](../../../../visual-basic/language-reference/queries/order-by-clause.md).  
  
## <a name="selecting-data-select"></a>La selezione dei dati (Select)  
 Il `Select` clausola specifica la forma e il contenuto di elementi restituiti. Ad esempio, è possibile specificare se i risultati saranno costituiti completo `Customer` oggetti, uno `Customer` proprietà, un subset di proprietà, una combinazione di proprietà da diverse origini dati o un nuovo tipo di risultati basato su un calcolo. Quando il `Select` clausola produce un valore diverso da una copia dell'elemento di origine, l'operazione viene chiamata una *proiezione*.  
  
 Per recuperare un insieme costituito da completo `Customer` oggetti, selezionare la variabile di intervallo stessa:  
  
 [!code-vb[VbLINQBasicOps n.&4;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/basic-query-operations_4.vb)]  
  
 Se un `Customer` istanza è un oggetto di grandi dimensioni con molti campi, e che si desidera recuperare solo il nome, è possibile selezionare `cust.Name`, come illustrato nell'esempio seguente. Inferenza del tipo locale riconosce che in questo modo il tipo di risultato da una raccolta di `Customer` oggetti da una raccolta di stringhe.  
  
 [!code-vb[VbLINQBasicOps n.&5;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/basic-query-operations_5.vb)]  
  
 Per selezionare più campi dall'origine dati, sono disponibili due opzioni:  
  
-   Nel `Select` clausola, specificare i campi che si desidera includere nel risultato. Il compilatore definirà un tipo anonimo con tali campi come proprietà. Per ulteriori informazioni, vedere [tipi anonimi](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md).  
  
     Poiché gli elementi restituiti nell'esempio seguente sono istanze di un tipo anonimo, è possibile fare riferimento al tipo di base al nome in un' posizione nel codice. Il nome definito dal compilatore per il tipo contiene caratteri non validi nel normale codice Visual Basic. Nell'esempio seguente, gli elementi nella raccolta restituita dalla query in `londonCusts4` sono istanze di un tipo anonimo  
  
     [!code-vb[6 VbLINQBasicOps](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/basic-query-operations_6.vb)]  
  
     -oppure-  
  
-   Definire un tipo denominato che contiene i campi specifici che si desidera includere nel risultato e creare e inizializzare istanze del tipo nel `Select` clausola. Utilizzare questa opzione solo se è necessario utilizzare i singoli risultati esterne alla raccolta in cui vengono restituiti o se si dispone di passarle come parametri nelle chiamate al metodo. Il tipo di `londonCusts5` nell'esempio seguente è IEnumerable (Of NamePhone).  
  
     [!code-vb[VbLINQBasicOps&#7;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/basic-query-operations_7.vb)]  
  
     [!code-vb[VbLINQBasicOps n.&8;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/basic-query-operations_8.vb)]  
  
 Per ulteriori informazioni sull'utilizzo di `Select` clausola in Visual Basic, vedere [clausola Select](../../../../visual-basic/language-reference/queries/select-clause.md).  
  
## <a name="joining-data-join-and-group-join"></a>Dati join (Join e Group Join)  
 È possibile combinare più origini dati nel `From` clausola in diversi modi. Ad esempio, il codice seguente vengono utilizzate due origini dati e in modo implicito combina le proprietà da entrambi gli elementi nel risultato. La query Seleziona gli studenti il cui cognome iniziano con una vocale.  
  
 [!code-vb[9 VbLINQBasicOps](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/basic-query-operations_9.vb)]  
  
> [!NOTE]
>  È possibile eseguire questo codice con l'elenco di studenti creato in [procedura: creare un elenco di elementi](../../../../visual-basic/programming-guide/concepts/linq/how-to-create-a-list-of-items.md).  
  
 Il `Join` parola chiave è equivalente a un `INNER JOIN` in SQL. Combina due raccolte in base ai valori chiave corrispondenti tra gli elementi in due raccolte. La query restituisce tutto o parte del elementi della raccolta che hanno valori chiave corrispondenti. Ad esempio, il codice seguente consente di duplicare l'azione del join implicito precedente.  
  
 [!code-vb[VbLINQBasicOps&#10;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/basic-query-operations_10.vb)]  
  
 `Group Join`Combina le raccolte in un'unica raccolta gerarchica, come un `LEFT JOIN` in SQL. Per ulteriori informazioni, vedere [clausola Join](../../../../visual-basic/language-reference/queries/join-clause.md) e [clausola Group Join](../../../../visual-basic/language-reference/queries/group-join-clause.md).  
  
## <a name="grouping-data-group-by"></a>Raggruppamento di dati (Group By)  
 È possibile aggiungere un `Group By` clausola per raggruppare gli elementi nel risultato di una query in base a uno o più campi degli elementi. Ad esempio, il codice seguente Raggruppa gli studenti per anno di classe.  
  
 [!code-vb[VbLINQBasicOps&#11;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/basic-query-operations_11.vb)]  
  
 Se si esegue questo codice utilizzando l'elenco di studenti creato in [procedura: creare un elenco di elementi](../../../../visual-basic/programming-guide/concepts/linq/how-to-create-a-list-of-items.md), l'output di `For Each` istruzione:  
  
 Anno: Junior  
  
 Tucker, Michael  
  
 Garcia, Hugo  
  
 Garcia, Eva  
  
 Tucker, Lance  
  
 Anno: Senior  
  
 Omelchenko, Svetlana  
  
 Osada, Michiko  
  
 Fakhouri, Fadi  
  
 Feng, Hanying  
  
 Terry Adams  
  
 Anno: seconda superiore  
  
 Mortensen, Sven  
  
 Garcia, Cesar  
  
 La variazione illustrata nel codice seguente Ordina gli anni di classe e quindi ordinati gli studenti all'interno di ogni anno in base al cognome.  
  
 [!code-vb[VbLINQBasicOps&#12;](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/basic-query-operations_12.vb)]  
  
 Per ulteriori informazioni su `Group By`, vedere [Group By Clause](../../../../visual-basic/language-reference/queries/group-by-clause.md).  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Collections.Generic.IEnumerable%601></xref:System.Collections.Generic.IEnumerable%601>   
 [Introduzione a LINQ in Visual Basic](../../../../visual-basic/programming-guide/concepts/linq/getting-started-with-linq.md)   
 [Query](../../../../visual-basic/language-reference/queries/queries.md)   
 [Cenni preliminari sugli operatori di Query standard (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)   
 [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)
