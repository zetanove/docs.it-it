---
title: LINQ e stringhe (Visual Basic) | Documenti di Microsoft
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
ms.assetid: 75ddb201-d97a-4f98-8cdf-4ad51714529a
caps.latest.revision: 4
author: stevehoag
ms.author: shoag
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: a79d1427331070da9c545fdd3175115fe187e879
ms.lasthandoff: 03/13/2017

---
# <a name="linq-and-strings-visual-basic"></a>LINQ e stringhe (Visual Basic)
LINQ può essere utilizzato per eseguire query e trasformare stringhe e raccolte di stringhe. Può essere particolarmente utile con dati semistrutturati nei file di testo. Le query LINQ possono essere combinate con espressioni regolari e le funzioni stringa tradizionale. Ad esempio, è possibile utilizzare il <xref:System.String.Split%2A>o <xref:System.Text.RegularExpressions.Regex.Split%2A>per creare una matrice di stringhe che è possibile eseguire una query o modificare utilizzando LINQ.</xref:System.Text.RegularExpressions.Regex.Split%2A> </xref:System.String.Split%2A> È possibile utilizzare il <xref:System.Text.RegularExpressions.Regex.IsMatch%2A>metodo il `where` clausola di una query LINQ.</xref:System.Text.RegularExpressions.Regex.IsMatch%2A> Ed è possibile utilizzare LINQ per eseguire una query o modificare il <xref:System.Text.RegularExpressions.MatchCollection>risultati restituiti da un'espressione regolare.</xref:System.Text.RegularExpressions.MatchCollection>  
  
 È inoltre possibile utilizzare le tecniche descritte in questa sezione per trasformare dati semistrutturati testo in XML. Per ulteriori informazioni, vedere [procedura: generare XML da file CSV](how-to-generate-xml-from-csv-files.md).  
  
 Negli esempi inclusi in questa sezione rientrano in due categorie:  
  
## <a name="querying-a-block-of-text"></a>Esecuzione di query su un blocco di testo  
 È possibile eseguire una query, analizzare e modificare i blocchi di testo suddividendoli in una matrice queryable di stringhe più piccole utilizzando il <xref:System.String.Split%2A>metodo o <xref:System.Text.RegularExpressions.Regex.Split%2A>(metodo).</xref:System.Text.RegularExpressions.Regex.Split%2A> </xref:System.String.Split%2A> È possibile suddividere il testo di origine in parole, frasi, paragrafi, pagine o altri criteri e quindi eseguire ulteriori suddivisioni se sono richiesti nella query.  
  
 [Procedura: contare le occorrenze di una parola in una stringa (LINQ) (Visual Basic)](how-to-count-occurrences-of-a-word-in-a-string-linq.md)  
 Viene illustrato come utilizzare LINQ per eseguire una query semplice sul testo.  
  
 [Procedura: eseguire una Query per trovare frasi che contengono un Set specificato di parole (LINQ) (Visual Basic)](how-to-query-for-sentences-that-contain-a-specified-set-of-words.md)

 Viene illustrato come suddividere i file di testo su limiti arbitrari e come eseguire query su ciascuna parte.  
  
 [Procedura: eseguire una Query per i caratteri in una stringa (LINQ) (Visual Basic)](how-to-query-for-characters-in-a-string-linq.md)  
 Viene illustrato che una stringa è un tipo queryable.  
  
 [Procedura: combinare query LINQ con espressioni regolari (Visual Basic)](how-to-combine-linq-queries-with-regular-expressions.md)  
 Viene illustrato come utilizzare espressioni regolari nelle query LINQ per complesso criteri di ricerca nei risultati della query filtrati.  
  
## <a name="querying-semi-structured-data-in-text-format"></a>Esecuzione di query su dati semistrutturati in formato testo  
 Molti tipi diversi di file di testo sono costituiti da una serie di linee, spesso con formattazione simile, ad esempio file delimitato da tabulazione o virgole o righe di lunghezza fissa. Dopo aver letto un file di testo in memoria, è possibile utilizzare LINQ per eseguire una query e/o modificare le righe. Le query LINQ semplificano anche la combinazione dei dati da più origini.  
  
 [Procedura: trovare la differenza dei Set tra due elenchi (LINQ) (Visual Basic)](how-to-find-the-set-difference-between-two-lists-linq.md)  
 Viene illustrato come trovare tutte le stringhe che sono presenti in un elenco ma non l'altro.  
  
 [Procedura: ordinare o filtrare i dati di testo da qualsiasi parola o campo (LINQ) (Visual Basic)](how-to-sort-or-filter-text-data-by-any-word-or-field-linq.md)  
 Viene illustrato come ordinare le righe di testo in base a qualsiasi parola o campo.  
  
 [Procedura: riordinare i campi di un File delimitato (LINQ) (Visual Basic)](how-to-reorder-the-fields-of-a-delimited-file.md)  
 Di seguito viene illustrato come riordinare i campi in una riga in un file con estensione csv.  
  
 [Procedura: combinare e confrontare raccolte di stringhe (LINQ) (Visual Basic)](how-to-combine-and-compare-string-collections-linq.md)  
 Viene illustrato come combinare elenchi di stringhe in vari modi.  
  
 [Procedura: popolare raccolte di oggetti da più origini (LINQ) (Visual Basic)](how-to-populate-object-collections-from-multiple-sources-linq.md)  
 Viene illustrato come creare raccolte di oggetti utilizzando più file di testo come origini dati.  
  
 [Procedura: unire contenuto da file dissimili (LINQ) (Visual Basic)](how-to-join-content-from-dissimilar-files-linq.md)  
 Viene illustrato come combinare le stringhe in due elenchi in un'unica stringa utilizzando una chiave corrispondente.  
  
 [Procedura: suddividere un File in molti file utilizzando i gruppi (LINQ) (Visual Basic)](how-to-split-a-file-into-many-files-by-using-groups-linq.md)  
 Di seguito viene illustrato come creare nuovi file utilizzando un singolo file come origine dati.  
  
 [Procedura: calcolare i valori di colonna in un File di testo CSV (LINQ) (Visual Basic)](how-to-compute-column-values-in-a-csv-text-file-linq.md)  
 Viene illustrato come eseguire calcoli matematici sui dati di testo in file con estensione csv.  
  
## <a name="see-also"></a>Vedere anche  
 [Language-Integrated Query (LINQ) (Visual Basic)](index.md)   
 [Procedura: generare XML da file CSV](how-to-generate-xml-from-csv-files.md)

