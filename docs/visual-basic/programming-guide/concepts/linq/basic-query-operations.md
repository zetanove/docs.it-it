---
title: "Operazioni di query di base (Visual Basic) | Microsoft Docs"
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
  - "origini dati [LINQ in Visual Basic]"
  - "Join (clausola) [LINQ in Visual Basic]"
  - "ordinamento di dati [LINQ in Visual Basic]"
  - "proiezioni [LINQ in Visual Basic]"
  - "LINQ [Visual Basic], operazioni di query"
  - "Order By (clausola) [LINQ in Visual Basic]"
  - "unione di dati [LINQ in Visual Basic]"
  - "query [LINQ in Visual Basic], operazioni di base"
  - "selezione di dati [LINQ in Visual Basic]"
  - "Group By (clausola) [LINQ in Visual Basic]"
  - "raggruppamento di dati [LINQ in Visual Basic]"
  - "Select (clausola) [LINQ in Visual Basic]"
ms.assetid: 1146f6d0-fcb8-4f4d-8223-c9db52620d21
caps.latest.revision: 37
caps.handback.revision: 35
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Operazioni di query di base (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

In questo argomento viene fornita una breve introduzione alle espressioni [!INCLUDE[vbteclinqext](../../../../csharp/getting-started/includes/vbteclinqext_md.md)] in Visual Basic e ad alcune operazioni comuni eseguite in una query.  Per ulteriori informazioni, vedere i seguenti argomenti:  
  
 [Introduction to LINQ in Visual Basic](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)  
  
 [Queries](../../../../visual-basic/language-reference/queries/queries.md)  
  
 [Procedura dettagliata: Scrittura delle query in Visual Basic](../../../../visual-basic/programming-guide/concepts/linq/walkthrough-writing-queries.md)  
  
## Specifica dell'origine dati \(From\)  
 In una query [!INCLUDE[vbteclinq](../../../../csharp/includes/vbteclinq_md.md)] il primo passaggio consiste nello specificare l'origine dati della query.  Di conseguenza, la clausola di `From` in una query non sempre in primo luogo. Gli operatori di query selezionano ed elaborano il risultato in base al tipo di origine.  
  
 [!code-vb[VbLINQBasicOps#1](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/basic-query-operations_1.vb)]  
  
 La clausola `From` specifica l'origine dati, `customers`, e una *variabile di intervallo*, `cust`.  La variabile di intervallo è simile a una variabile di iterazione del ciclo, con la differenza che in un'espressione di query non si verifica un'effettiva iterazione.  Quando viene eseguita la query, spesso utilizzando un ciclo `For Each`, la variabile di intervallo funge da riferimento a ogni elemento successivo di `customers`.  Poiché il compilatore è in grado di dedurre il tipo di `cust`, non è necessario specificarlo in modo esplicito.  Per esempi di query scritte con e senza la tipizzazione esplicita, vedere [Type Relationships in Query Operations \(Visual Basic\)](../../../../visual-basic/programming-guide/concepts/linq/type-relationships-in-query-operations.md).  
  
 Per ulteriori informazioni sull'utilizzo della clausola `From` in Visual Basic, vedere [From Clause](../../../../visual-basic/language-reference/queries/from-clause.md).  
  
## Filtro dei dati \(Where\)  
 Probabilmente l'operazione di query più comune consiste nell'applicazione di un filtro sotto forma di espressione booleana.  La query restituisce quindi solo gli elementi per i quali l'espressione sia true.  Per eseguire l'operazione di filtro viene utilizzata la clausola `Where`.  Il filtro specifica gli elementi presenti nell'origine dati da includere nella sequenza risultante.  Nell'esempio seguente vengono inclusi solo i clienti con un indirizzo di Londra.  
  
 [!code-vb[VbLINQBasicOps#2](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/basic-query-operations_2.vb)]  
  
 È possibile utilizzare gli operatori logici, ad esempio `And` e `Or`, per combinare le espressioni di filtro in una clausola `Where`.  Per restituire, ad esempio, solo i clienti di Londra di nome Devon, utilizzare il codice seguente:  
  
```vb#  
Where cust.City = "London" And cust.Name = "Devon"   
```  
  
 Per restituire i clienti di Londra o Parigi, utilizzare il codice seguente:  
  
```vb#  
Where cust.City = "London" Or cust.City = "Paris"   
```  
  
 Per ulteriori informazioni sull'utilizzo della clausola `Where` in Visual Basic, vedere [Where Clause](../../../../visual-basic/language-reference/queries/where-clause.md).  
  
## Ordinamento dei dati \(Order By\)  
 È spesso consigliabile disporre i dati restituiti in un determinato ordine.  La clausola `Order By` consente di ordinare gli elementi presenti nella sequenza restituita in base a uno o più campi specificati.  Ad esempio, nella query seguente i risultati vengono ordinati in base alla proprietà `Name`.  Poiché `Name` è una stringa, i dati restituiti verranno ordinati alfabeticamente, dalla A alla Z.  
  
 [!code-vb[VbLINQBasicOps#3](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/basic-query-operations_3.vb)]  
  
 Per disporre i risultati in ordine inverso, ovvero dalla Z alla A, utilizzare la clausola `Order By...Descending`.  Se non viene specificato né `Ascending` né `Descending`, viene utilizzata l'impostazione predefinita `Ascending`.  
  
 Per ulteriori informazioni sull'utilizzo della clausola `Order By` in Visual Basic, vedere [Order By Clause](../../../../visual-basic/language-reference/queries/order-by-clause.md).  
  
## Selezione dei dati \(Select\)  
 La clausola `Select` specifica il formato e il contenuto degli elementi restituiti.  È possibile, ad esempio, specificare se i risultati devono essere costituiti da oggetti `Customer` completi, solo da una proprietà `Customer`, da un sottoinsieme di proprietà, da una combinazione di proprietà di diverse origini dati o da un nuovo tipo di risultati basato su un calcolo.  Quando la clausola `Select` genera un risultato diverso da una copia dell'elemento di origine, l'operazione viene denominata *proiezione*.  
  
 Per recuperare una raccolta costituita da oggetti `Customer` completi, selezionare la variabile di intervallo stessa:  
  
 [!code-vb[VbLINQBasicOps#4](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/basic-query-operations_4.vb)]  
  
 Se un'istanza `Customer` è costituita da un oggetto di grandi dimensioni contenente molti campi e si desidera recuperare solo il nome, è possibile selezionare `cust.Name`, come illustrato nell'esempio seguente.  L'inferenza del tipo di variabile locale riconosce che in questo modo il tipo di risultati viene modificato da una raccolta di oggetti `Customer` in una raccolta di stringhe.  
  
 [!code-vb[VbLINQBasicOps#5](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/basic-query-operations_5.vb)]  
  
 Per selezionare più campi dall'origine dati, sono disponibili due opzioni:  
  
-   Nella clausola `Select` specificare i campi da includere nel risultato.  Il compilatore definirà un tipo anonimo contenente tali campi come proprietà.  Per ulteriori informazioni, vedere [Anonymous Types](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md).  
  
     Poiché gli elementi restituiti nell'esempio seguente sono istanze di un tipo anonimo, non è possibile fare riferimento al tipo in base al nome in altri punti del codice.  Il nome definito dal compilatore per il tipo contiene caratteri che non sono validi nel normale codice Visual Basic.  Nell'esempio seguente gli elementi presenti nella raccolta restituita dalla query in `londonCusts4` sono istanze di un tipo anonimo.  
  
     [!code-vb[VbLINQBasicOps#6](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/basic-query-operations_6.vb)]  
  
     In alternativa  
  
-   Definire un tipo denominato contenente i campi specifici da includere nel risultato e creare e inizializzare le istanze del tipo nella clausola `Select`.  Utilizzare questa opzione solo se è necessario utilizzare i singoli risultati al di fuori della raccolta nella quale sono stati restituiti o se è necessario passarli come parametri nelle chiamate al metodo.  Il tipo di `londonCusts5` nell'esempio seguente è IEnumerable\(Of NamePhone\).  
  
     [!code-vb[VbLINQBasicOps#7](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/basic-query-operations_7.vb)]  
  
     [!code-vb[VbLINQBasicOps#8](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/basic-query-operations_8.vb)]  
  
 Per ulteriori informazioni sull'utilizzo della clausola `Select` in Visual Basic, vedere [Select Clause](../../../../visual-basic/language-reference/queries/select-clause.md).  
  
## Creazione di join di dati \(Join e Group Join\)  
 È possibile combinare più origini dati nella clausola `From` in diversi modi.  Ad esempio, nel codice seguente vengono utilizzate due origini dati combinando in modo implicito nel risultato le proprietà di entrambe le origini.  La query seleziona gli studenti il cui cognome inizia con una vocale.  
  
 [!code-vb[VbLINQBasicOps#9](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/basic-query-operations_9.vb)]  
  
> [!NOTE]
>  È possibile eseguire questo codice con l'elenco di studenti creato in [How to: Create a List of Items](../../../../visual-basic/programming-guide/concepts/linq/how-to-create-a-list-of-items.md).  
  
 La parola chiave `Join` è equivalente a `INNER JOIN` in SQL.  Le due raccolte vengono combinate in base ai valori chiave corrispondenti tra gli elementi delle due raccolte.  La query restituisce tutti o parte degli elementi della raccolta che hanno valori chiave corrispondenti.  Ad esempio, nel codice seguente viene duplicata l'azione della precedente operazione di join implicito.  
  
 [!code-vb[VbLINQBasicOps#10](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/basic-query-operations_10.vb)]  
  
 `Group Join` combina le raccolte in un'unica raccolta gerarchica, in modo analogo a `LEFT JOIN` in SQL.  Per ulteriori informazioni, vedere [Join Clause](../../../../visual-basic/language-reference/queries/join-clause.md) e [Group Join Clause](../../../../visual-basic/language-reference/queries/group-join-clause.md).  
  
## Raggruppamento dei dati \(Group By\)  
 È possibile aggiungere una clausola `Group By` per raggruppare gli elementi nel risultato di una query in base a uno o più campi degli elementi.  Ad esempio, nel codice seguente gli studenti vengono raggruppati in base all'anno della classe.  
  
 [!code-vb[VbLINQBasicOps#11](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/basic-query-operations_11.vb)]  
  
 Se si esegue questo codice utilizzando l'elenco di studenti creato in [How to: Create a List of Items](../../../../visual-basic/programming-guide/concepts/linq/how-to-create-a-list-of-items.md), l'output restituito dall'istruzione `For Each` sarà:  
  
 Year: Junior  
  
 Tucker, Michael  
  
 Garcia, Hugo  
  
 Garcia, Debra  
  
 Tucker, Lance  
  
 Year: Senior  
  
 Omelchenko, Svetlana  
  
 Osada, Michiko  
  
 Fakhouri, Fadi  
  
 Feng, Hanying  
  
 Adams, Terry  
  
 Year: Freshman  
  
 Mortensen, Sven  
  
 Garcia, Cesar  
  
 Nella variante illustrata nel codice seguente vengono ordinati gli anni della classe e vengono quindi ordinati gli studenti all'interno di ogni anno in base al cognome.  
  
 [!code-vb[VbLINQBasicOps#12](../../../../visual-basic/programming-guide/concepts/linq/codesnippet/VisualBasic/basic-query-operations_12.vb)]  
  
 Per ulteriori informazioni su `Group By`, vedere [Clausola Group By](../../../../visual-basic/language-reference/queries/group-by-clause.md).  
  
## Vedere anche  
 <xref:System.Collections.Generic.IEnumerable%601>   
 [Getting Started with LINQ in Visual Basic](../../../../visual-basic/programming-guide/concepts/linq/getting-started-with-linq.md)   
 [Queries](../../../../visual-basic/language-reference/queries/queries.md)   
 [Standard Query Operators Overview](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)   
 [LINQ](../../../../visual-basic/programming-guide/language-features/linq/index.md)   
 [Basic LINQ Query Operations](../../../../csharp/programming-guide/concepts/linq/basic-linq-query-operations.md)