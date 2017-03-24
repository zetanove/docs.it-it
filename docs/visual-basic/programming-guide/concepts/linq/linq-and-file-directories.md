---
title: LINQ e le directory del File (Visual Basic) | Documenti di Microsoft
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
ms.assetid: 159fd5c3-3926-4071-ae78-d8e423287eb7
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
ms.openlocfilehash: 5536ae95b42cdaddda2c4cae97a114681e94b0ab
ms.lasthandoff: 03/13/2017

---
# <a name="linq-and-file-directories-visual-basic"></a>Directory di File (Visual Basic) e LINQ
Molte operazioni del file system sono essenzialmente query e pertanto sono particolarmente adatte per l'approccio LINQ.  
  
 Si noti che le query in questa sezione non distruttiva. Non vengono utilizzati per modificare il contenuto del file originali o delle cartelle. Si basa la regola che le query non dovrebbero causare effetti collaterali. In generale, qualsiasi codice (incluse le query che eseguono creano, aggiornamento ed eliminazione operatori) che vengono modificati i dati di origine deve essere mantenuto separato dal codice che esegue solo una query dei dati.  
  
 Questa sezione contiene i seguenti argomenti:  
  
 [Procedura: eseguire una Query per i file con un attributo specificato o un nome (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-query-for-files-with-a-specified-attribute-or-name.md)  
 Viene illustrato come cercare file esaminando una o più proprietà del relativo <xref:System.IO.FileInfo>oggetto.</xref:System.IO.FileInfo>  
  
 [Procedura: raggruppare i file per estensione (LINQ) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-group-files-by-extension-linq.md)  
 Viene illustrato come restituire gruppi di <xref:System.IO.FileInfo>oggetto in base all'estensione di file.</xref:System.IO.FileInfo>  
  
 [Procedura: eseguire una Query per il numero totale di byte in un Set di cartelle (LINQ) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-query-for-the-total-number-of-bytes-in-a-set-of-folders.md)  
 Viene illustrato come restituire il numero totale di byte in tutti i file in una struttura di directory specificato.  
  
 [Procedura: confrontare il contenuto di due cartelle (LINQ) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-compare-the-contents-of-two-folders-linq.md)s  
 Viene illustrato come restituire tutti i file presenti in due cartelle specifiche e anche tutti i file presenti in una cartella, ma non l'altro.  
  
 [Procedura: eseguire una Query per il più grande o più file in una struttura di Directory (LINQ) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-query-for-the-largest-file-or-files-in-a-directory-tree.md)  
 Viene illustrato come ripristinare il file massimo o minimo o un numero specificato di file, in una struttura di directory.  
  
 [Procedura: eseguire una Query per i file duplicati in una struttura di Directory (LINQ) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-query-for-duplicate-files-in-a-directory-tree-linq.md)  
 Viene illustrato come raggruppare tutti i nomi file che si verificano in più di una posizione in una struttura di directory specificato. Viene inoltre illustrato come eseguire confronti più complessi basati su un operatore di confronto personalizzato.  
  
 [Procedura: eseguire Query sul contenuto dei file in una cartella (LINQ) (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/how-to-query-the-contents-of-files-in-a-folder-linq.md)  
 Viene illustrato come scorrere le cartelle in una struttura ad albero, aprire ogni file e il contenuto del file di query.  
  
## <a name="comments"></a>Commenti  
 Esiste un livello di complessità per la creazione di un'origine dati che rappresenta il contenuto del file system e gestisce correttamente le eccezioni in modo accurato. Negli esempi inclusi in questa sezione creano un insieme di snapshot <xref:System.IO.FileInfo>gli oggetti che rappresentano tutti i file nella cartella principale specificata e tutte le relative sottocartelle.</xref:System.IO.FileInfo> Lo stato di ogni <xref:System.IO.FileInfo>può cambiare nel tempo tra l'inizio e la fine dell'esecuzione di una query.</xref:System.IO.FileInfo> Ad esempio, è possibile creare un elenco di <xref:System.IO.FileInfo>degli oggetti da utilizzare come origine dati.</xref:System.IO.FileInfo> Se si tenta di accedere il `Length` proprietà in una query, il <xref:System.IO.FileInfo>oggetto tenterà di accedere al file system per aggiornare il valore di `Length`.</xref:System.IO.FileInfo> Se il file non esiste più, si otterrà un <xref:System.IO.FileNotFoundException>nella query, anche se non si è eseguendo una query direttamente nel file system.</xref:System.IO.FileNotFoundException> Alcune query in questa sezione utilizzare un metodo separato che utilizza queste particolari eccezioni in determinati casi. Un'altra opzione consiste nel mantenere l'origine dati aggiornata in modo dinamico utilizzando <xref:System.IO.FileSystemWatcher>.</xref:System.IO.FileSystemWatcher>  
  
## <a name="see-also"></a>Vedere anche  
 [LINQ to Objects (Visual Basic)](../../../../visual-basic/programming-guide/concepts/linq/linq-to-objects.md)
