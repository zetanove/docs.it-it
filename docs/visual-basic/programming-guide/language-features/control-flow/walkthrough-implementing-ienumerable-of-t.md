---
title: Implementazione di IEnumerable in Visual Basic | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- control flow [Visual Basic]
- enumerable interfaces
- loop structures, optimizing performance
- control flow
ms.assetid: c60d7589-51f2-4463-a2d5-22506bbc1554
caps.latest.revision: 15
author: stevehoag
ms.author: shoag
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 68c37c46cbceb1056d50972cdc58ddb7c7577447
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-implementing-ienumerableof-t-in-visual-basic"></a>Procedura dettagliata: implementazione di IEnumerable(Of T) in Visual Basic
Il <xref:System.Collections.Generic.IEnumerable%601>interfaccia viene implementata da classi che possono restituire una sequenza di valori un elemento alla volta.</xref:System.Collections.Generic.IEnumerable%601> Il vantaggio di restituzione dei dati è un elemento in un momento non è necessario caricare il set completo di dati in memoria per utilizzarlo. È sufficiente l'utilizzo di memoria sufficiente per caricare un singolo elemento dai dati. Le classi che implementano il `IEnumerable(T)` interfaccia può essere utilizzata con `For Each` cicli o le query LINQ.  
  
 Ad esempio, si consideri un'applicazione che deve leggere un file di testo di grandi dimensioni e restituire ogni riga del file che corrisponde a determinati criteri di ricerca. L'applicazione utilizza una query LINQ per restituire le righe dal file che corrispondono ai criteri specificati. Per eseguire query sul contenuto del file tramite una query LINQ, l'applicazione potrebbe caricare il contenuto del file in una matrice o una raccolta. Tuttavia, il caricamento dell'intero file in una matrice o raccolta richiederebbe molta più memoria rispetto a quelli necessari. La query LINQ può invece eseguire una query il contenuto del file utilizzando una classe enumerabile, restituendo solo i valori che corrispondono ai criteri di ricerca. Le query che restituiscono solo alcuni valori corrispondenti utilizzeranno molta meno memoria.  
  
 È possibile creare una classe che implementa il <xref:System.Collections.Generic.IEnumerable%601>interfaccia da esporre i dati di origine dati enumerabili.</xref:System.Collections.Generic.IEnumerable%601> La classe che implementa il `IEnumerable(T)` interfaccia richiederà un'altra classe che implementa il <xref:System.Collections.Generic.IEnumerator%601>interfaccia per scorrere i dati di origine.</xref:System.Collections.Generic.IEnumerator%601> Queste due classi consentono di restituire gli elementi di dati in sequenza come un tipo specifico.  
  
 In questa procedura dettagliata, si creerà una classe che implementa il `IEnumerable(Of String)` interfaccia e una classe che implementa il `IEnumerator(Of String)` interfaccia per leggere un file di testo una riga alla volta.  
  
[!INCLUDE[note_settings_general](../../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
## <a name="creating-the-enumerable-class"></a>Creazione della classe Enumerable  
  
|Per creare il progetto della classe enumerable|  
|---|  
|1.  In [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]via il **File** dal menu **New** e quindi fare clic su **progetto**.<br />2.  Nel **nuovo progetto** della finestra di dialogo di **tipi di progetto** riquadro, assicurarsi che **Windows** è selezionata. Selezionare **libreria di classi** nel **modelli** riquadro. Nel **nome** digitare `StreamReaderEnumerable`, quindi fare clic su **OK**. Viene visualizzato il nuovo progetto.<br />3.  In **Esplora**, il file Class1. vb e fare clic su **rinominare**. Rinominare il file in `StreamReaderEnumerable.vb` e premere INVIO. Ridenominazione del file verrà anche rinominare la classe come `StreamReaderEnumerable`. Questa classe implementerà il `IEnumerable(Of String)` interfaccia.<br />4.  Fare clic sul progetto StreamReaderEnumerable, scegliere **Aggiungi**, quindi fare clic su **nuovo elemento**. Selezionare il **classe** modello. Nel **nome** digitare `StreamReaderEnumerator.vb` e fare clic su **OK**.|  
  
 La prima classe nel progetto è la classe enumerable e verrà implementata il `IEnumerable(Of String)` interfaccia. Implementa l'interfaccia generica di <xref:System.Collections.IEnumerable>interfaccia e garantisce che gli utenti di questa classe possono accedere a valori tipizzati come `String`.</xref:System.Collections.IEnumerable>  
  
|Per aggiungere il codice per implementare IEnumerable|  
|---|  
|1.  Aprire il file StreamReaderEnumerable.<br />2.  Nella riga dopo `Public Class StreamReaderEnumerable`, digitare quanto segue e premere INVIO.<br />     [!code-vb[VbVbalrIteratorWalkthrough n.&1;](../../../../visual-basic/programming-guide/language-features/control-flow/codesnippet/VisualBasic/walkthrough-implementing-ienumerable-of-t_1.vb)]<br />     [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]popola automaticamente la classe con i membri necessari per il `IEnumerable(Of String)` interfaccia.<br />3.  Questa classe enumerable leggerà righe da un file di testo una riga alla volta. Aggiungere il codice seguente alla classe per esporre un costruttore pubblico che accetta un percorso di file come parametro di input.<br />     [!code-vb[VbVbalrIteratorWalkthrough n.&2;](../../../../visual-basic/programming-guide/language-features/control-flow/codesnippet/VisualBasic/walkthrough-implementing-ienumerable-of-t_2.vb)]<br />4.  L'implementazione del <xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A>metodo il `IEnumerable(Of String)` interfaccia restituirà una nuova istanza della `StreamReaderEnumerator` classe</xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A> L'implementazione di `GetEnumerator` metodo il `IEnumerable` interfaccia può essere reso `Private`, in quanto è necessario esporre solo i membri del `IEnumerable(Of String)` interfaccia. Sostituire il codice che [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] generato per il `GetEnumerator` metodi con il codice seguente.<br />     [!code-vb[VbVbalrIteratorWalkthrough n.&3;](../../../../visual-basic/programming-guide/language-features/control-flow/codesnippet/VisualBasic/walkthrough-implementing-ienumerable-of-t_3.vb)]|  
  
|Per aggiungere il codice per implementare IEnumerator|  
|---|  
|1.  Aprire il file StreamReaderEnumerator.<br />2.  Nella riga dopo `Public Class StreamReaderEnumerator`, digitare quanto segue e premere INVIO.<br />     [!code-vb[VbVbalrIteratorWalkthrough n.&4;](../../../../visual-basic/programming-guide/language-features/control-flow/codesnippet/VisualBasic/walkthrough-implementing-ienumerable-of-t_4.vb)]<br />     [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]popola automaticamente la classe con i membri necessari per il `IEnumerator(Of String)` interfaccia.<br />3.  La classe dell'enumeratore apre il file di testo ed esegue il file dei / o per leggere le righe dal file. Aggiungere il codice seguente alla classe per esporre un costruttore pubblico che accetta un percorso di file come parametro di input e aprire il file di testo per la lettura.<br />     [!code-vb[VbVbalrIteratorWalkthrough n.&5;](../../../../visual-basic/programming-guide/language-features/control-flow/codesnippet/VisualBasic/walkthrough-implementing-ienumerable-of-t_5.vb)]<br />4.  Il `Current` proprietà per entrambi i `IEnumerator(Of String)` e `IEnumerator` interfacce restituiscono l'elemento corrente dal file di testo come un `String`. L'implementazione di `Current` proprietà del `IEnumerator` interfaccia può essere reso `Private`, in quanto è necessario esporre solo i membri del `IEnumerator(Of String)` interfaccia. Sostituire il codice che [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] generato per la `Current` proprietà con il codice seguente.<br />     [!code-vb[6 VbVbalrIteratorWalkthrough](../../../../visual-basic/programming-guide/language-features/control-flow/codesnippet/VisualBasic/walkthrough-implementing-ienumerable-of-t_6.vb)]<br />5.  Il `MoveNext` metodo il `IEnumerator` interfaccia consente di passare all'elemento successivo nel file di testo e aggiorna il valore restituito dalla `Current` proprietà. Se sono presenti più elementi da leggere, il `MoveNext` restituisce `False`; in caso contrario il `MoveNext` restituisce `True`. Aggiungere al metodo `MoveNext` il seguente codice.<br />     [!code-vb[VbVbalrIteratorWalkthrough&#7;](../../../../visual-basic/programming-guide/language-features/control-flow/codesnippet/VisualBasic/walkthrough-implementing-ienumerable-of-t_7.vb)]<br />6.  Il `Reset` metodo il `IEnumerator` interfaccia consente di indirizzare l'iteratore in modo che punti all'inizio del file di testo e cancella il valore dell'elemento corrente. Aggiungere al metodo `Reset` il seguente codice.<br />     [!code-vb[VbVbalrIteratorWalkthrough n.&8;](../../../../visual-basic/programming-guide/language-features/control-flow/codesnippet/VisualBasic/walkthrough-implementing-ienumerable-of-t_8.vb)]<br />7.  Il `Dispose` metodo il `IEnumerator` interfaccia garantisce che tutte le risorse non gestite vengono rilasciate prima che l'iteratore venga eliminato. L'handle di file che viene utilizzato il `StreamReader` oggetto è una risorsa non gestita e deve essere chiuso prima che l'istanza dell'iteratore venga eliminato. Sostituire il codice che [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] generato per il `Dispose` metodo con il codice seguente.<br />     [!code-vb[9 VbVbalrIteratorWalkthrough](../../../../visual-basic/programming-guide/language-features/control-flow/codesnippet/VisualBasic/walkthrough-implementing-ienumerable-of-t_9.vb)]|  
  
## <a name="using-the-sample-iterator"></a>Utilizzo dell'iteratore di esempio  
 È possibile utilizzare una classe enumerabile nel codice dell'insieme di strutture di controllo che richiedono un oggetto che implementa `IEnumerable`, ad esempio un `For Next` ciclo o una query LINQ. Nell'esempio seguente il `StreamReaderEnumerable` in una query LINQ.  
  
 [!code-vb[VbVbalrIteratorWalkthrough&#10;](../../../../visual-basic/programming-guide/language-features/control-flow/codesnippet/VisualBasic/walkthrough-implementing-ienumerable-of-t_10.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 [Introduzione a LINQ in Visual Basic](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [Flusso di controllo](../../../../visual-basic/programming-guide/language-features/control-flow/index.md)   
 [Cicli (strutture)](../../../../visual-basic/programming-guide/language-features/control-flow/loop-structures.md)   
 [Istruzione For Each...Next](../../../../visual-basic/language-reference/statements/for-each-next-statement.md)

