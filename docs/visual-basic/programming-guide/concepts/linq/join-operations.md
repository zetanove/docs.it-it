---
title: Creare un join Operations (Visual Basic) | Documenti di Microsoft
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
ms.assetid: 39ab4854-ac84-4738-9d0b-3cb79be84db4
caps.latest.revision: 3
author: stevehoag
ms.author: shoag
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: dce1adb5b918674bc8ee8fc48c8ff5b3c3814a88
ms.lasthandoff: 03/13/2017

---
# <a name="join-operations-visual-basic"></a>Creare un join Operations (Visual Basic)
Oggetto *join* di due origini dati è un'associazione di oggetti di un'origine dati con oggetti che condividono un attributo comune in un'altra origine dati.  
  
 La creazione di un join è un'operazione importante nelle query che fanno riferimento a origini dati le cui relazioni reciproche non possono essere seguite direttamente. Nella programmazione orientata a oggetti ciò potrebbe corrispondere a una correlazione non modellata tra oggetti, ad esempio la direzione inversa di una relazione unidirezionale. Un esempio di relazione unidirezionale è costituito da una classe Customer che include una proprietà di tipo City, ma la classe City non include una proprietà che sia una raccolta di oggetti Customer. Se si ha un elenco di oggetti City e si vogliono trovare tutti i clienti in ogni città, è possibile usare un'operazione join per individuarli.  
  
 I metodi di join disponibili nel framework LINQ sono <xref:System.Linq.Enumerable.Join%2A>e <xref:System.Linq.Enumerable.GroupJoin%2A>.</xref:System.Linq.Enumerable.GroupJoin%2A> </xref:System.Linq.Enumerable.Join%2A> Questi metodi eseguono equijoin, ovvero join che associano due origini dati in base all'uguaglianza delle rispettive chiavi. Per un confronto, si noti che Transact-SQL supporta operatori join diversi da 'uguale a', ad esempio l'operatore 'minore di'. In termini di database relazionali, <xref:System.Linq.Enumerable.Join%2A>implementa un inner join, un tipo di join in cui vengono restituiti solo gli oggetti che hanno una corrispondenza nel set di dati.</xref:System.Linq.Enumerable.Join%2A> Il <xref:System.Linq.Enumerable.GroupJoin%2A>metodo non ha equivalenti diretti in termini di database relazionale, ma implementa un superset di inner join e left outer join.</xref:System.Linq.Enumerable.GroupJoin%2A> Un left outer join è un join che restituisce ogni elemento della prima origine dati (a sinistra), anche se non ha elementi correlati in altra origine dati.  
  
 L'illustrazione seguente mostra una visualizzazione concettuale dei due set e degli elementi dei set che sono inclusi in un inner join o in un left outer join.  
  
 ![Due cerchi sovrapposti che mostrano interno/esterno. ] (../../../../csharp/programming-guide/concepts/linq/media/joincircles.png "JoinCircles")  
  
## <a name="methods"></a>Metodi  
  
|Nome metodo|Descrizione|Sintassi delle espressioni di Query Visual Basic|Altre informazioni|  
|-----------------|-----------------|------------------------------------------|----------------------|  
|Join|Unisce due sequenze in base a funzioni selector chiave ed estrae coppie di valori|`From x In …, y In … Where x.a = y.a`<br /><br /> -oppure-<br /><br /> `Join … [As …]In … On …`|<xref:System.Linq.Enumerable.Join%2A?displayProperty=fullName></xref:System.Linq.Enumerable.Join%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.Join%2A?displayProperty=fullName></xref:System.Linq.Queryable.Join%2A?displayProperty=fullName>|  
|GroupJoin|Unisce due sequenze in base a funzioni selector chiave e raggruppa le corrispondenze risultanti per ogni elemento.|`Group Join … In … On …`|<xref:System.Linq.Enumerable.GroupJoin%2A?displayProperty=fullName></xref:System.Linq.Enumerable.GroupJoin%2A?displayProperty=fullName><br /><br /> <xref:System.Linq.Queryable.GroupJoin%2A?displayProperty=fullName></xref:System.Linq.Queryable.GroupJoin%2A?displayProperty=fullName>|  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.Linq></xref:System.Linq>   
 [Cenni preliminari sugli operatori di Query standard (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/standard-query-operators-overview.md)   
 [Tipi anonimi](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)   
 [Formulare query su prodotto incrociato e join](http://msdn.microsoft.com/library/d8072ede-0521-4670-9bec-1778ceeb875b)   
 [Clausola join](../../../../visual-basic/language-reference/queries/join-clause.md)   
 [Procedura: unire contenuto da file dissimili (LINQ) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-join-content-from-dissimilar-files-linq.md)   
 [Procedura: popolare raccolte di oggetti da più origini (LINQ) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-populate-object-collections-from-multiple-sources-linq.md)
