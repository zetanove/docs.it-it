---
title: "Walkthrough: Implementing IEnumerable(Of T) in Visual Basic | Microsoft Docs"
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
  - "control flow [Visual Basic]"
  - "enumerable interfaces"
  - "loop structures, optimizing performance"
  - "control flow"
ms.assetid: c60d7589-51f2-4463-a2d5-22506bbc1554
caps.latest.revision: 15
caps.handback.revision: 15
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Walkthrough: Implementing IEnumerable(Of T) in Visual Basic
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

L'interfaccia <xref:System.Collections.Generic.IEnumerable%601> viene implementata da classi che sono in grado di restituire una sequenza di valori un elemento alla volta.  Il vantaggio della restituzione dei dati un elemento alla volta è che non è necessario caricare il set di dati completo in memoria per utilizzarlo.  È necessario utilizzare solo la memoria sufficiente per caricare un solo elemento dai dati.  Le classi che implementano l'interfaccia `IEnumerable(T)` possono essere utilizzate con cicli `For Each` o query LINQ.  
  
 Si consideri, ad esempio, un'applicazione che deve leggere un file di testo di grandi dimensioni e restituire ogni riga del file che corrisponde a determinati criteri di ricerca.  L'applicazione utilizza una query LINQ per restituire le righe del file corrispondenti ai criteri specificati.  Per eseguire una query sul contenuto del file tramite una query LINQ, l'applicazione potrebbe caricare il contenuto del file in una matrice o una raccolta.  Tuttavia, il caricamento dell'intero file in una matrice o in una raccolta richiederebbe molta più memoria del necessario.  La query LINQ consente invece eseguire una query sul contenuto del file tramite una classe enumerabile, restituendo solo i valori corrispondenti ai criteri di ricerca.  Le query che restituiscono solo alcuni valori corrispondenti utilizzeranno molta meno memoria.  
  
 È possibile creare una classe che implementa l'interfaccia <xref:System.Collections.Generic.IEnumerable%601> per esporre i dati di origine come dati enumerabili.  La classe che implementa l'interfaccia `IEnumerable(T)` richiederà un'altra classe che implementa l'interfaccia <xref:System.Collections.Generic.IEnumerator%601> per scorrere i dati di origine.  Queste due classi consentono di restituire elementi di dati in sequenza come tipo specifico.  
  
 In questa procedura dettagliata, verrà creata una classe che implementa l'interfaccia `IEnumerable(Of String)` e una classe che implementa l'interfaccia `IEnumerator(Of String)` per leggere un file di testo una riga per volta.  
  
 [!INCLUDE[note_settings_general](../../../../csharp/language-reference/compiler-messages/includes/note_settings_general_md.md)]  
  
## Creazione della classe enumerabile  
  
||  
|-|  
|Per creare il progetto della classe enumerabile|  
|1.  Scegliere **Nuovo** dal menu **File** di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)], quindi fare clic su **Progetto**.<br />2.  Nel riquadro **Tipi progetto** della finestra di dialogo **Nuovo progetto** verificare che sia selezionata la voce **Finestre**.  Selezionare **Libreria di classi** nel riquadro **Modelli**.  Nella casella **Nome** digitare `StreamReaderEnumerable`, quindi fare clic su **OK**.  Verrà visualizzato il nuovo progetto.<br />3.  In **Esplora soluzioni** fare clic con il pulsante destro del mouse sul file Class1.vb e scegliere **Rinomina**.  Assegnare al file il nome `StreamReaderEnumerable.vb` e premere INVIO.  Rinominando il file, anche la classe verrà rinominata `StreamReaderEnumerable`.  Questa classe implementerà l'interfaccia `IEnumerable(Of String)`.<br />4.  Fare clic con il pulsante destro del mouse sul progetto StreamReaderEnumerable, scegliere **Aggiungi**, quindi fare clic su **Nuovo elemento**.  Selezionare il modello **Classe**.  Digitare `StreamReaderEnumerator.vb` nella casella **Nome** e scegliere **OK**.|  
  
 La prima classe di questo progetto è la classe enumerabile che implementerà l'interfaccia `IEnumerable(Of String)`.  Questa interfaccia generica implementa l'interfaccia <xref:System.Collections.IEnumerable> e garantisce che gli utenti di questa classe possano accedere a valori tipizzati come `String`.  
  
||  
|-|  
|Per aggiungere il codice per implementare IEnumerable|  
|1.  Aprire il file StreamReaderEnumerable.vb.<br />2.  Nella riga dopo `Public Class StreamReaderEnumerable` digitare quanto segue e premere INVIO.<br />     [!code-vb[VbVbalrIteratorWalkthrough#1](../../../../visual-basic/programming-guide/language-features/control-flow/codesnippet/VisualBasic/walkthrough-implementing-ienumerable-of-t_1.vb)]<br />     In [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] la classe viene automaticamente popolata con i membri richiesti dall'interfaccia `IEnumerable(Of String)`<br />3.  Questa classe enumerabile consentirà di leggere le righe da un file di testo una per volta.  Aggiungere il codice seguente alla classe per esporre un costruttore pubblico che accetta un percorso di file come parametro di input.<br />     [!code-vb[VbVbalrIteratorWalkthrough#2](../../../../visual-basic/programming-guide/language-features/control-flow/codesnippet/VisualBasic/walkthrough-implementing-ienumerable-of-t_2.vb)]<br />4.  L'implementazione del metodo <xref:System.Collections.Generic.IEnumerable%601.GetEnumerator%2A> dell'interfaccia `IEnumerable(Of String)` restituirà una nuova istanza della classe `StreamReaderEnumerator`.  L'implementazione del metodo `GetEnumerator` dell'interfaccia `IEnumerable` può essere eseguita come `Private`, perché è necessario esporre solo i membri dell'interfaccia `IEnumerable(Of String)`.  Sostituire il codice generato da [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] per i metodi `GetEnumerator` con il codice seguente.<br />     [!code-vb[VbVbalrIteratorWalkthrough#3](../../../../visual-basic/programming-guide/language-features/control-flow/codesnippet/VisualBasic/walkthrough-implementing-ienumerable-of-t_3.vb)]|  
  
||  
|-|  
|Per aggiungere il codice per implementare IEnumerator|  
|1.  Aprire il file StreamReaderEnumerator.vb.<br />2.  Nella riga dopo `Public Class StreamReaderEnumerator` digitare quanto segue e premere INVIO.<br />     [!code-vb[VbVbalrIteratorWalkthrough#4](../../../../visual-basic/programming-guide/language-features/control-flow/codesnippet/VisualBasic/walkthrough-implementing-ienumerable-of-t_4.vb)]<br />     In [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] la classe viene automaticamente popolata con i membri richiesti dall'interfaccia `IEnumerator(Of String)`<br />3.  La classe dell'enumeratore apre il file di testo ed esegue l'I\/O di file per leggere le righe dal file.  Aggiungere il codice seguente alla classe per esporre un costruttore pubblico che accetta un percorso di file come parametro di input e aprire il file di testo per la lettura.<br />     [!code-vb[VbVbalrIteratorWalkthrough#5](../../../../visual-basic/programming-guide/language-features/control-flow/codesnippet/VisualBasic/walkthrough-implementing-ienumerable-of-t_5.vb)]<br />4.  Le proprietà `Current` per le interfacce `IEnumerator(Of String)` e `IEnumerator` restituiscono l'elemento corrente dal file di testo come `String`.  L'implementazione della proprietà `Current` dell'interfaccia `IEnumerator` può essere eseguita come `Private`, perché è necessario esporre solo i membri dell'interfaccia `IEnumerator(Of String)`.  Sostituire il codice generato da [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] per le proprietà `Current` con il codice seguente.<br />     [!code-vb[VbVbalrIteratorWalkthrough#6](../../../../visual-basic/programming-guide/language-features/control-flow/codesnippet/VisualBasic/walkthrough-implementing-ienumerable-of-t_6.vb)]<br />5.  Il metodo `MoveNext` dell'interfaccia `IEnumerator` consente di passare all'elemento successivo nel file di testo e di aggiornare il valore restituito dalla proprietà `Current`.  Se non sono presenti altri elementi da leggere, il metodo `MoveNext` restituisce `False`. In caso contrario, il metodo `MoveNext` restituisce `True`.  Aggiungere al metodo `MoveNext` il seguente codice.<br />     [!code-vb[VbVbalrIteratorWalkthrough#7](../../../../visual-basic/programming-guide/language-features/control-flow/codesnippet/VisualBasic/walkthrough-implementing-ienumerable-of-t_7.vb)]<br />6.  Il metodo `Reset` dell'interfaccia `IEnumerator` consente di indirizzare l'iteratore in modo che faccia riferimento all'inizio del file di testo e di cancellare il valore dell'elemento corrente.  Aggiungere al metodo `Reset` il seguente codice.<br />     [!code-vb[VbVbalrIteratorWalkthrough#8](../../../../visual-basic/programming-guide/language-features/control-flow/codesnippet/VisualBasic/walkthrough-implementing-ienumerable-of-t_8.vb)]<br />7.  Il metodo `Dispose` dell'interfaccia `IEnumerator` garantisce che tutte le risorse non gestite vengano rilasciate prima che venga eliminato l'iteratore.  L'handle di file utilizzato dall'oggetto `StreamReader` è una risorsa non gestita e deve essere chiuso prima che venga eliminata l'istanza dell'iteratore.  Sostituire il codice generato da [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] per il metodo `Dispose` con il codice seguente.<br />     [!code-vb[VbVbalrIteratorWalkthrough#9](../../../../visual-basic/programming-guide/language-features/control-flow/codesnippet/VisualBasic/walkthrough-implementing-ienumerable-of-t_9.vb)]|  
  
## Utilizzo dell'iteratore di esempio  
 È possibile utilizzare una classe enumerabile nel codice insieme alle strutture di controllo che richiedono un oggetto che implementa `IEnumerable`, quale un ciclo `For Next` o una query LINQ.  Nell'esempio seguente viene illustrato `StreamReaderEnumerable` in una query LINQ.  
  
 [!code-vb[VbVbalrIteratorWalkthrough#10](../../../../visual-basic/programming-guide/language-features/control-flow/codesnippet/VisualBasic/walkthrough-implementing-ienumerable-of-t_10.vb)]  
  
## Vedere anche  
 [Introduction to LINQ in Visual Basic](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [Control Flow](../../../../visual-basic/programming-guide/language-features/control-flow/index.md)   
 [Loop Structures](../../../../visual-basic/programming-guide/language-features/control-flow/loop-structures.md)   
 [Istruzione For Each...Next](../../../../visual-basic/language-reference/statements/for-each-next-statement.md)