---
title: "Order By Clause (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.QueryOrderBy"
  - "vb.QueryAscending"
  - "vb.QueryDescending"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "queries [Visual Basic], Order By"
  - "Order By clause"
  - "Order By statement"
ms.assetid: fa911282-6b81-44c7-acfa-46b5bb93df75
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# Order By Clause (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Specifica l'ordinamento dei risultati di una query.  
  
## Sintassi  
  
```  
Order By orderExp1 [ Ascending | Descending ] [, orderExp2 [...] ]  
```  
  
## Parti  
 `orderExp1`  
 Obbligatorio.  Uno o più campi dal risultato corrente della query che identificano come ordinare i valori restituiti.  I nomi di campo devono essere separati da virgole \(\).  È possibile identificare ogni campo come ordinato in senso crescente o decrescente utilizzando le parole chiave `Ascending` o `Descending`.  Se non viene specificata la parola chiave `Ascending` o `Descending`, l'ordinamento predefinito è in senso crescente.  I campi di ordinamento hanno la precedenza da sinistra verso destra.  
  
## Note  
 È possibile utilizzare la clausola `Order By` per ordinare i risultati di una query.  La clausola `Order By` può ordinare un risultato solo in base alla variabile di intervallo per l'ambito corrente.  Ad esempio, la clausola `Select` introduce un nuovo ambito in un'espressione di query con nuove variabili di iterazione per tale ambito.  Le variabili di intervallo definite prima di una clausola `Select` in una query non sono disponibili dopo la clausola `Select`.  Pertanto, se si desidera ordinare i risultati tramite un campo non disponibile nella clausola `Select`, è necessario inserire la clausola `Order By` prima della clausola `Select`.  Ad esempio quando si desidera ordinare la query tramite campi che non vengono restituiti come parte del risultato.  
  
 Il senso crescente e decrescente ordinare per un campo viene determinato dall'implementazione dell'interfaccia <xref:System.IComparable> per il tipo di dati del campo.  Se il tipo di dati non implementa l'interfaccia <xref:System.IComparable>, il senso di ordinamento viene ignorato.  
  
## Esempio  
 Nell'espressione di query seguente viene utilizzata una clausola `From` per dichiarare una variabile di intervallo `book` per la raccolta `books`.  La clausola `Order By` ordina in senso crescente \(impostazione predefinita\) in base al prezzo il risultato della query.  I libri con lo stesso prezzo vengono ordinati in senso crescente in base al titolo.  Mediante la clausola `Select` vengono selezionate le proprietà `Title` e `Price` come valori restituiti dalla query.  
  
 [!code-vb[VbSimpleQuerySamples#24](../../../visual-basic/language-reference/queries/codesnippet/visualbasic/VbSimpleQuerySamples/QuerySamples1.vb#24)]  
  
## Esempio  
 Nell'espressione di query seguente viene utilizzata la clausola `Order By` per ordinare in senso decrescente il risultato della query in base al prezzo.  I libri con lo stesso prezzo vengono ordinati in senso crescente in base al titolo.  
  
 [!code-vb[VbSimpleQuerySamples#25](../../../visual-basic/language-reference/queries/codesnippet/visualbasic/VbSimpleQuerySamples/QuerySamples1.vb#25)]  
  
## Esempio  
 Nell'espressione di query seguente viene utilizzata una clausola `Select` per selezionare il titolo del libro, il prezzo, la data di pubblicazione e l'autore.  Vengono quindi popolati i campi `Title`, `Price`, `PublishDate`e `Author` della variabile di intervallo per il nuovo ambito.  La clausola `Order By` ordina la nuova variabile di intervallo per autore, titolo del libro e poi prezzo.  Ogni colonna viene ordinata nel senso predefinito \(crescente\).  
  
 [!code-vb[VbSimpleQuerySamples#26](../../../visual-basic/language-reference/queries/codesnippet/visualbasic/VbSimpleQuerySamples/QuerySamples1.vb#26)]  
  
## Vedere anche  
 [Introduction to LINQ in Visual Basic](../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [Queries](../../../visual-basic/language-reference/queries/queries.md)   
 [Select Clause](../../../visual-basic/language-reference/queries/select-clause.md)   
 [From Clause](../../../visual-basic/language-reference/queries/from-clause.md)