---
title: "Where Clause (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.QueryWhere"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Where statement"
  - "queries [Visual Basic], Where"
  - "Where clause"
ms.assetid: 48b5c2c5-3181-429c-8545-894296798c89
caps.latest.revision: 18
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 18
---
# Where Clause (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Specifica le condizioni di filtro per una query.  
  
## Sintassi  
  
```  
Where condition  
```  
  
## Parti  
 `condition`  
 Obbligatorio.  Espressione che determina se i valori per l'elemento corrente della raccolta vengono inclusi nella raccolta di output.  L'espressione deve restituire un valore `Boolean` oppure l'equivalente di un valore `Boolean`.  Se la condizione restituisce `True`, l'elemento viene incluso nel risultato della query; in caso contrario, l'elemento viene escluso dal risultato della query.  
  
## Note  
 La clausola `Where` consente di filtrare i dati della query selezionando solo gli elementi che soddisfano determinati criteri.  Gli elementi i cui valori sono tali che la clausola `Where` restituisce `True` vengono inclusi nel risultato della query; gli altri elementi vengono esclusi.  L'espressione utilizzata in una clausola `Where` deve restituire un `Boolean` o l'equivalente di un `Boolean`, ad esempio un Integer che restituisce `False` quando il valore è zero.  È possibile combinare più espressioni in una clausola `Where` utilizzando operatori logici come `And`, `Or`, `AndAlso`, `OrElse`, `Is`, e `IsNot`.  
  
 Per impostazione predefinita, le espressioni di query non vengono valutate fino a che si accede ad esse, ad esempio quando sono associate a dati o quando vengono fatte scorrere in un ciclo `For`.  Di conseguenza, la clausola `Where` non viene valutata, fino a che si accede alla query.  Se si dispone di valori esterni alla query utilizzati nella clausola `Where`, assicurarsi che venga utilizzato il valore adatto nella clausola `Where` quando la query viene eseguita.  Per ulteriori informazioni sull'esecuzione delle query, vedere [Scrittura della prima query LINQ](../../../visual-basic/programming-guide/concepts/linq/writing-your-first-linq-query.md).  
  
 È possibile chiamare funzioni all'interno di una clausola `Where` per eseguire un calcolo o un'operazione su un valore dall'elemento corrente della raccolta.  La chiamata di una funzione in una clausola `Where` può fare in modo che la query venga eseguita immediatamente quando viene definita anziché quando si accede ad essa.  Per ulteriori informazioni sull'esecuzione delle query, vedere [Scrittura della prima query LINQ](../../../visual-basic/programming-guide/concepts/linq/writing-your-first-linq-query.md).  
  
## Esempio  
 Nell'espressione di query seguente viene utilizzata una clausola `From` per dichiarare una variabile di intervallo `cust` per ogni oggetto `Customer` nella raccolta `customers`.  La clausola `Where` utilizza la variabile di intervallo per restringere l'output ai clienti dalla regione specificata.  Il ciclo `For Each` visualizza il nome di azienda per ogni cliente nel risultato della query.  
  
 [!code-vb[VbSimpleQuerySamples#23](../../../visual-basic/language-reference/queries/codesnippet/visualbasic/VbSimpleQuerySamples/QuerySamples1.vb#23)]  
  
## Esempio  
 Nell'esempio seguente viene utilizzato `And` e  `Or` operatori logici in  `Where` clausola.  
  
 [!code-vb[VbSimpleQuerySamples#31](../../../visual-basic/language-reference/queries/codesnippet/visualbasic/VbSimpleQuerySamples/QuerySamples1.vb#31)]  
  
## Vedere anche  
 [Introduction to LINQ in Visual Basic](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [Queries](../../../visual-basic/language-reference/queries/queries.md)   
 [From Clause](../../../visual-basic/language-reference/queries/from-clause.md)   
 [Select Clause](../../../visual-basic/language-reference/queries/select-clause.md)   
 [Istruzione For Each...Next](../../../visual-basic/language-reference/statements/for-each-next-statement.md)