---
title: Gestione degli eventi (Visual Basic) | Documenti di Microsoft
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
- event handling [Visual Basic], walkthroughs
- walkthroughs [Visual Basic], event handling
- variables [Visual Basic], WithEvents
- events [Visual Basic], walkthroughs
- WithEvents keyword, walkthroughs
- event handlers [Visual Basic], walkthroughs
ms.assetid: f145b3fc-5ae0-4509-a2aa-1ff6934706bd
caps.latest.revision: 18
author: dotnet-bot
ms.author: dotnetcontent
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
ms.openlocfilehash: 17cd0bddbe8c89cf60e19f3f2af6f448ad465d70
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-handling-events-visual-basic"></a>Procedura dettagliata: gestione di eventi (Visual Basic)
Questo è il secondo di due argomenti che illustrano come usare gli eventi. Il primo argomento, [procedura dettagliata: dichiarazione e generazione di eventi](../../../../visual-basic/programming-guide/language-features/events/walkthrough-declaring-and-raising-events.md), viene illustrato come dichiarare e generare eventi. Questa sezione viene usato il modulo e una classe da tale procedura dettagliata per illustrare come gestire gli eventi quando si verificano.  
  
 Il `Widget` esempio di classe vengono utilizzate istruzioni di gestione degli eventi tradizionali. [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]sono disponibili altre tecniche per l'utilizzo di eventi. Come esercizio, è possibile modificare questo esempio per utilizzare il `AddHandler` e `Handles` istruzioni.  
  
### <a name="to-handle-the-percentdone-event-of-the-widget-class"></a>Gestire l'evento PercentDone della classe Widget  
  
1.  Inserire il codice seguente in `Form1`:  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents n.&4;](../../../../visual-basic/programming-guide/language-features/events/codesnippet/VisualBasic/walkthrough-handling-events_1.vb)]  
  
     Il `WithEvents` la parola chiave specifica che la variabile `mWidget` viene utilizzata per gestire gli eventi di un oggetto. Specificare il tipo di oggetto, indicando il nome della classe da cui verrà creato l'oggetto.  
  
     La variabile `mWidget` viene dichiarata in `Form1` poiché `WithEvents` variabili devono essere a livello di classe. Questo vale indipendentemente dal tipo di classe in cui sono contenute.  
  
     La variabile `mblnCancel` viene utilizzato per annullare il `LongTask` metodo.  
  
## <a name="writing-code-to-handle-an-event"></a>Scrittura di codice per gestire un evento  
 Non appena si dichiara una variabile utilizzando `WithEvents`, il nome della variabile viene visualizzato nell'elenco di riepilogo a discesa a sinistra della classe **Editor di codice**. Quando si seleziona `mWidget`, `Widget` gli eventi della classe vengono visualizzati nell'elenco a discesa a destra. Se si seleziona un evento consente di visualizzare la corrispondente routine evento, con il prefisso `mWidget` e un carattere di sottolineatura. Tutte le routine evento associate a un `WithEvents` variabile viene assegnato il nome di variabile come prefisso.  
  
#### <a name="to-handle-an-event"></a>Per gestire un evento  
  
1.  Selezionare `mWidget` dall'elenco di riepilogo a discesa a sinistra nel **Editor di codice**.  
  
2.  Selezionare il `PercentDone` evento dall'elenco a discesa a destra. Il **Editor di codice** apre il `mWidget_PercentDone` routine evento.  
  
    > [!NOTE]
    >  Il **Editor di codice** è utile, ma non obbligatorio, per l'inserimento di nuovi gestori di eventi. In questa procedura dettagliata, è più semplice copiare i gestori eventi direttamente nel codice.  
  
3.  Aggiungere il codice seguente al gestore eventi `mWidget_PercentDone`:  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents n.&5;](../../../../visual-basic/programming-guide/language-features/events/codesnippet/VisualBasic/walkthrough-handling-events_2.vb)]  
  
     Ogni volta che il `PercentDone` evento viene generato, la routine evento Visualizza la percentuale di completamento in un `Label` controllo. Il `DoEvents` metodo consente di ridisegnare l'etichetta e offre inoltre all'utente la possibilità di scegliere il **Annulla** pulsante.  
  
4.  Aggiungere il codice seguente per il `Button2_Click` gestore dell'evento:  
  
     [!code-vb[6 VbVbcnWalkthroughDeclaringAndRaisingEvents](../../../../visual-basic/programming-guide/language-features/events/codesnippet/VisualBasic/walkthrough-handling-events_3.vb)]  
  
 Se l'utente fa clic il **Annulla** pulsante durante `LongTask` è in esecuzione, il `Button2_Click` eventi viene eseguito non appena il `DoEvents` istruzione consente l'elaborazione degli eventi. La variabile a livello di classe `mblnCancel` è impostato su `True`e `mWidget_PercentDone` evento quindi verifica l'evento e imposta il `ByRef Cancel` argomento `True`.  
  
## <a name="connecting-a-withevents-variable-to-an-object"></a>Una variabile WithEvents la connessione a un oggetto  
 `Form1`è ora configurato per gestire un `Widget` eventi dell'oggetto. È ora per trovare un `Widget` da qualche parte.  
  
 Quando si dichiara una variabile `WithEvents` in fase di progettazione non è associato alcun oggetto. Oggetto `WithEvents` variabile è esattamente come qualsiasi altra variabile di oggetto. È necessario creare un oggetto e assegnare un riferimento a esso con il `WithEvents` variabile.  
  
#### <a name="to-create-an-object-and-assign-a-reference-to-it"></a>Per creare un oggetto e assegnare un riferimento a esso  
  
1.  Selezionare **(eventi Form1)** dall'elenco di riepilogo a discesa a sinistra nel **Editor di codice**.  
  
2.  Selezionare il `Load` evento dall'elenco a discesa a destra. Il **Editor di codice** apre il `Form1_Load` routine evento.  
  
3.  Aggiungere il codice seguente per il `Form1_Load` routine evento per creare il `Widget`:  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents&#7;](../../../../visual-basic/programming-guide/language-features/events/codesnippet/VisualBasic/walkthrough-handling-events_4.vb)]  
  
 Quando viene eseguito questo codice, [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] crea un `Widget` dell'oggetto e si connette gli eventi per le routine evento associate a `mWidget`. Da quel momento, ogni volta che il `Widget` genera il `PercentDone` evento, il `mWidget_PercentDone` viene eseguita la routine evento.  
  
#### <a name="to-call-the-longtask-method"></a>Per chiamare il metodo LongTask  
  
-   Aggiungere il codice seguente al gestore eventi `Button1_Click`:  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents n.&8;](../../../../visual-basic/programming-guide/language-features/events/codesnippet/VisualBasic/walkthrough-handling-events_5.vb)]  
  
 Prima di `LongTask` metodo viene chiamato, l'etichetta che visualizza la percentuale di completamento deve essere inizializzato e a livello di classe `Boolean` flag di annullamento del metodo deve essere impostato su `False`.  
  
 `LongTask`viene chiamato con una durata di attività pari a 12,2 secondi. Il `PercentDone` evento viene generato una volta ogni un terzo di secondo. Ogni volta che viene generato l'evento, il `mWidget_PercentDone` viene eseguita la routine evento.  
  
 Quando `LongTask` viene eseguita, `mblnCancel` viene verificato se `LongTask` è stato completato correttamente, o se è stato arrestato perché `mblnCancel` è stata impostata su `True`. La percentuale di completamento viene aggiornata solo nel caso precedente.  
  
#### <a name="to-run-the-program"></a>Per eseguire il programma  
  
1.  Premere F5 per attivare il progetto in modalità di esecuzione.  
  
2.  Fare clic su di **Avvia attività** pulsante. Ogni volta che il `PercentDone` viene generato l'evento, l'etichetta viene aggiornata con la percentuale di completamento dell'attività.  
  
3.  Fare clic su di **Annulla** pulsante per arrestare l'attività. Si noti che l'aspetto di **Annulla** pulsante Modifica immediatamente quando viene selezionata. Il `Click` evento non può verificarsi fino a quando il `My.Application.DoEvents` istruzione consente l'elaborazione di eventi.  
  
    > [!NOTE]
    >  Il `My.Application.DoEvents` metodo elabora gli eventi esattamente allo stesso modo del form. Ad esempio, in questa procedura dettagliata, è necessario fare clic il **Annulla** due volte sul pulsante. Per consentire al modulo gestire gli eventi direttamente, è possibile utilizzare il multithreading. Per ulteriori informazioni, vedere [Threading](http://msdn.microsoft.com/library/552f6c68-dbdb-4327-ae36-32cf9063d88c).  
  
 Può risultare utile eseguire il programma con F11 e scorrere il codice una riga alla volta. È possibile visualizzare chiaramente come esecuzione entra `LongTask`, quindi brevemente viene `Form1` ogni volta che il `PercentDone` viene generato l'evento.  
  
 Che cosa accadrebbe se, durante l'esecuzione torna nel codice di `Form1`, `LongTask` metodo viene chiamato? Nel peggiore dei casi, potrebbe verificarsi un overflow dello stack se `LongTask` chiamate ogni volta che è stato generato l'evento.  
  
 È possibile che la variabile `mWidget` per gestire gli eventi per un altro `Widget` assegnando un riferimento al nuovo oggetto `Widget` a `mWidget`. Infatti, è possibile che il codice in `Button1_Click` eseguire questa operazione ogni volta che si sceglie il pulsante.  
  
#### <a name="to-handle-events-for-a-different-widget"></a>Per gestire gli eventi per un widget diverso  
  
-   Aggiungere la seguente riga di codice per il `Button1_Click` procedura, la riga che precede immediatamente `mWidget.LongTask(12.2, 0.33)`:  
  
     [!code-vb[9 VbVbcnWalkthroughDeclaringAndRaisingEvents](../../../../visual-basic/programming-guide/language-features/events/codesnippet/VisualBasic/walkthrough-handling-events_6.vb)]  
  
 Il codice sopra riportato crea un nuovo `Widget` ogni volta che si fa clic sul pulsante. Non appena il `LongTask` metodo viene completato, il riferimento il `Widget` viene rilasciato e `Widget` viene eliminato.  
  
 Oggetto `WithEvents` variabile può contenere un solo riferimento oggetto alla volta, pertanto se assegnare un diverso `Widget` oggetto `mWidget`, precedente `Widget` non verranno gestiti non sono più eventi dell'oggetto. Se `mWidget` è l'unica variabile di oggetto che contiene un riferimento alla precedente `Widget`, l'oggetto viene eliminato. Se si desidera gestire eventi da svariati `Widget` oggetti, utilizzare il `AddHandler` istruzione per elaborare gli eventi di ogni oggetto separatamente.  
  
> [!NOTE]
>  È possibile dichiarare un numero `WithEvents` matrici di variabili necessarie `WithEvents` variabili non sono supportate.  
  
## <a name="see-also"></a>Vedere anche  
 [Procedura dettagliata: Dichiarazione e generazione di eventi](../../../../visual-basic/programming-guide/language-features/events/walkthrough-declaring-and-raising-events.md)   
 [Eventi](../../../../visual-basic/programming-guide/language-features/events/index.md)
