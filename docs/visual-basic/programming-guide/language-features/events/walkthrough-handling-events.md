---
title: "Walkthrough: Handling Events (Visual Basic) | Microsoft Docs"
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
  - "event handling [Visual Basic], walkthroughs"
  - "walkthroughs [Visual Basic], event handling"
  - "variables [Visual Basic], WithEvents"
  - "events [Visual Basic], walkthroughs"
  - "WithEvents keyword, walkthroughs"
  - "event handlers [Visual Basic], walkthroughs"
ms.assetid: f145b3fc-5ae0-4509-a2aa-1ff6934706bd
caps.latest.revision: 18
caps.handback.revision: 18
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Walkthrough: Handling Events (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

In questo argomento viene illustrato l'utilizzo degli eventi.  In un argomento precedente, [Procedura dettagliata: dichiarazione e generazione di eventi](../../../../visual-basic/programming-guide/language-features/events/walkthrough-declaring-and-raising-events.md), sono fornite informazioni sulla dichiarazione e sulla generazione di eventi.  In questa sezione il form e la classe creati nella prima procedura dettagliata verranno utilizzati per descrivere la gestione degli eventi nel momento in cui si verificano.  
  
 Nella classe `Widget` dell'esempio vengono utilizzate le istruzioni di gestione degli eventi tradizionali.  In [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] sono tuttavia disponibili altre tecniche di elaborazione degli eventi.  Come esercitazione è possibile modificare questo esempio utilizzando le istruzioni `AddHandler` e `Handles`.  
  
### Per gestire l'evento PercentDone della classe Widget  
  
1.  Digitare il codice riportato di seguito in `Form1`:  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents#4](../../../../visual-basic/programming-guide/language-features/events/codesnippet/VisualBasic/walkthrough-handling-events_1.vb)]  
  
     Utilizzando la parola chiave `WithEvents` è possibile specificare che la variabile `mWidget` viene utilizzata per la gestione degli eventi di un oggetto.  Per specificare il tipo di oggetto è necessario fornire il nome della classe da cui l'oggetto verrà creato.  
  
     La variabile `mWidget` viene dichiarata in `Form1` perché le variabili `WithEvents` possono essere solo di livello classe,  indipendentemente dal tipo di classe in cui sono contenute.  
  
     La variabile `mblnCancel` viene utilizzata per annullare il metodo `LongTask`.  
  
## Scrittura di codice per la gestione di un evento  
 Non appena una variabile viene dichiarata tramite `WithEvents`, il nome della variabile viene visualizzato nella casella di riepilogo a discesa sinistra dell'**editor di codice** della classe.  Quando si seleziona `mWidget`, gli eventi della classe `Widget` vengono visualizzati nella casella di riepilogo a discesa destra.  Se si seleziona un evento, verrà visualizzata la corrispondente routine evento, con il prefisso `mWidget` e un carattere di sottolineatura.  A tutte le routine evento associate alla variabile `WithEvents` viene assegnato come prefisso il nome della variabile.  
  
#### Per gestire un evento  
  
1.  Selezionare `mWidget` dalla casella di riepilogo a discesa sinistra nell'**editor di codice**.  
  
2.  Selezionare l'evento `PercentDone` dalla casella di riepilogo a discesa destra.  Verrà aperta la routine dell'evento `mWidget_PercentDone`.  
  
    > [!NOTE]
    >  L'**editor di codice** è utile ma non obbligatorio per l'inserimento di nuovi gestori eventi.  Nella seguente procedura dettagliata, è più semplice copiare i gestori eventi direttamente nel codice.  
  
3.  Aggiungere il codice seguente al gestore eventi `mWidget_PercentDone`:  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents#5](../../../../visual-basic/programming-guide/language-features/events/codesnippet/VisualBasic/walkthrough-handling-events_2.vb)]  
  
     Ogni volta che viene generato l'evento `PercentDone`, la percentuale di completamento in un controllo `Label`viene visualizzato dalla routine dell'evento.  Il metodo `DoEvents` consente di ridisegnare l'etichetta e di fare clic sul pulsante **Annulla**.  
  
4.  Aggiungere il codice seguente al gestore eventi `Button2_Click`:  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents#6](../../../../visual-basic/programming-guide/language-features/events/codesnippet/VisualBasic/walkthrough-handling-events_3.vb)]  
  
 Se l'utente fa clic sul pulsante **Annulla** durante l'esecuzione di `LongTask`, l'evento `Button2_Click` viene eseguito non appena l'istruzione `DoEvents` consente l'elaborazione degli eventi.  La variabile a livello di classe `mblnCancel` viene impostata su `True`. L'evento `mWidget_PercentDone` verifica tale variabile, quindi imposta l'argomento `ByRef Cancel` su `True`.  
  
## Collegamento di una variabile WithEvents a un oggetto  
 `Form1` è stato impostato per la gestione degli eventi dell'oggetto `Widget`.  È ora necessario individuare `Widget`.  
  
 Quando si dichiara una variabile utilizzando `WithEvents` in fase di progettazione, a tale variabile non è associato alcun oggetto.  Una variabile `WithEvents` non si differenzia dalle altre variabili oggetto.  È necessario creare un oggetto e assegnare il relativo riferimento alla variabile `WithEvents`.  
  
#### Per creare un oggetto e assegnare un riferimento a tale oggetto  
  
1.  Selezionare **\(Form1 Events\)** dalla casella di riepilogo a discesa sinistra nell'**editor di codice**.  
  
2.  Selezionare l'evento `Load` dalla casella di riepilogo a discesa destra.  Verrà aperta la routine dell'evento `Form1_Load`.  
  
3.  Aggiungere il seguente codice per la routine dell'evento `Form1_Load` in modo da creare `Widget`:  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents#7](../../../../visual-basic/programming-guide/language-features/events/codesnippet/VisualBasic/walkthrough-handling-events_4.vb)]  
  
 All'esecuzione del codice verrà creato un oggetto `Widget` e i relativi eventi verranno collegati alle routine evento associate a `mWidget`.  Da quel momento in poi la routine evento `mWidget_PercentDone` verrà eseguita ad ogni generazione dell'evento `PercentDone` da parte dell'oggetto `Widget`.  
  
#### Per chiamare il metodo LongTask  
  
-   Aggiungere il codice seguente al gestore eventi `Button1_Click`:  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents#8](../../../../visual-basic/programming-guide/language-features/events/codesnippet/VisualBasic/walkthrough-handling-events_5.vb)]  
  
 Prima che venga chiamato il metodo `LongTask` è necessario inizializzare l'etichetta che riporta la percentuale di completamento e impostare su `False` il flag `Boolean` a livello di classe per l'annullamento del metodo.  
  
 Il metodo `LongTask` viene chiamato con una durata di attività pari a 12,2 secondi.  L'evento `PercentDone` viene generato con intervalli pari a un terzo di secondo.  A ogni generazione dell'evento viene eseguita la routine `mWidget_PercentDone`.  
  
 Una volta completato il metodo `LongTask`, `mblnCancel` viene verificato per controllare se `LongTask` è stato completato correttamente o se è stato arrestato perché `mblnCancel` è stato impostato su `True`.  La percentuale di completamento viene aggiornata solo nel primo caso.  
  
#### Per eseguire il programma  
  
1.  Premere F5 per mettere il progetto in modalità di esecuzione.  
  
2.  Fare clic sul pulsante **Inizia attività**.  A ogni generazione dell'evento `PercentDone`, la percentuale di completamento dell'attività riportata sull'etichetta viene aggiornata.  
  
3.  Fare clic sul pulsante **Annulla** per arrestare l'attività.  Si noti che l'aspetto del pulsante **Annulla** non viene modificato nel momento stesso in cui si fa clic su di esso.  L'evento `Click` si verifica solo dopo che l'istruzione `My.Application.DoEvents` consente l'elaborazione dell'evento.  
  
    > [!NOTE]
    >  Per l'elaborazione degli eventi, il metodo `My.Application.DoEvents` si comporta in modo leggermente diverso rispetto al form.  Nella procedura dettagliata, ad esempio, è necessario fare clic due volte sul pulsante **Annulla**.  Per consentire al form di gestire gli eventi direttamente, è possibile ricorrere al multithreading.  Per ulteriori informazioni, vedere [Threading](../Topic/Threading%20\(C%23%20and%20Visual%20Basic\).md).  
  
 È possibile premere F11 e scorrere il codice una riga alla volta.  Si può chiaramente notare come a ogni generazione dell'evento `PercentDone` viene immesso `LongTask`, quindi viene velocemente reimmesso `Form1`.  
  
 Se il metodo `LongTask` viene chiamato a ogni generazione dell'evento e viene richiamato mentre l'esecuzione è ancora nel codice di `Form1`,  nella peggiore delle ipotesi è possibile che si verifichi un overflow dello stack.  
  
 Al nuovo oggetto `Widget` è possibile assegnare un riferimento a `mWidget` in modo che la variabile `mWidget` gestisca eventi per un oggetto `Widget` diverso.  È infatti possibile impostare il codice in `Button1_Click` in modo che questa operazione venga eseguita ogni volta che si fa clic sul pulsante.  
  
#### Per gestire eventi per un oggetto Widget diverso  
  
-   Aggiungere la seguente riga di codice alla routine `Button1_Click`, che precede direttamente la riga `mWidget.LongTask(12.2, 0.33)`:  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents#9](../../../../visual-basic/programming-guide/language-features/events/codesnippet/VisualBasic/walkthrough-handling-events_6.vb)]  
  
 Utilizzando questo codice è possibile creare un nuovo oggetto `Widget` ogni volta che si fa clic sul pulsante.  Non appena il metodo `LongTask` viene completato, il riferimento all'oggetto `Widget` viene rilasciato e tale oggetto viene eliminato.  
  
 Una variabile `WithEvents` è in grado di contenere un solo riferimento oggetto alla volta. Se quindi si assegna un oggetto `Widget` diverso a `mWidget`, gli eventi del precedente oggetto `Widget` non verranno più gestiti.  Se `mWidget` è l'unica variabile oggetto che contiene un riferimento all'oggetto `Widget` precedente, tale oggetto verrà eliminato.  Se si desidera gestire eventi da svariati oggetti `Widget`, è necessario utilizzare l'istruzione `AddHandler` per elaborare separatamente gli eventi relativi a ogni oggetto.  
  
> [!NOTE]
>  È possibile dichiarare tutte le variabili `WithEvents` necessarie. Tuttavia, le matrici di variabili `WithEvents` non sono supportate.  
  
## Vedere anche  
 [Walkthrough: Declaring and Raising Events](../../../../visual-basic/programming-guide/language-features/events/walkthrough-declaring-and-raising-events.md)   
 [Events](../../../../visual-basic/programming-guide/language-features/events/events.md)