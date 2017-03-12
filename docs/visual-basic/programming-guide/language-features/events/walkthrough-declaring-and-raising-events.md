---
title: "Walkthrough: Declaring and Raising Events (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "declarations, events"
  - "events [Visual Basic], walkthroughs"
  - "declaring events, walkthroughs"
  - "events [Visual Basic], declaring"
  - "events [Visual Basic], raising"
  - "raising events, walkthroughs"
ms.assetid: 8ffb3be8-097d-4d3c-b71e-04555ebda2a2
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# Walkthrough: Declaring and Raising Events (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

In questa procedura dettagliata vengono illustrate la dichiarazione e la generazione di eventi per una classe denominata `Widget`.  Dopo aver completato i passaggi richiesti, è possibile leggere l'argomento correlato, [Walkthrough: Handling Events](../../../../visual-basic/programming-guide/language-features/events/walkthrough-handling-events.md), in cui viene descritto come utilizzare eventi da oggetti `Widget` per fornire informazioni sullo stato in un'applicazione.  
  
## Classe Widget  
 Si supponga per il momento di disporre di una classe `Widget`.  Poiché alla classe `Widget` è associato un metodo il cui tempo di esecuzione potrebbe essere elevato, si desidera che nell'applicazione venga visualizzato un indicatore di completamento.  
  
 Naturalmente è possibile fare in modo che l'oggetto `Widget` mostri una finestra di dialogo relativa alla percentuale di completamento, ma tale finestra verrebbe visualizzata in tutti i progetti in cui viene utilizzata la classe `Widget`.  Nel corso della progettazione di oggetti è consigliabile lasciare che l'interfaccia utente venga gestita dall'applicazione che utilizza un oggetto, a meno che lo scopo dell'oggetto non sia la gestione di un form o di una finestra di dialogo.  
  
 Poiché lo scopo di `Widget` è l'esecuzione di altre attività, è consigliabile aggiungere un evento `PercentDone` e consentire alla routine che chiama i metodi `Widget` di gestire tale evento e di visualizzare gli aggiornamenti relativi allo stato.  L'evento `PercentDone` è inoltre in grado di fornire un meccanismo per l'annullamento dell'attività.  
  
#### Per compilare un esempio di codice per questo argomento  
  
1.  Aprire un nuovo progetto Applicazione Windows di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] e creare un form denominato `Form1`.  
  
2.  Aggiungere due pulsanti e un'etichetta a `Form1`.  
  
3.  Assegnare un nome agli oggetti, come illustrato nella tabella riportata di seguito.  
  
    |Object|Proprietà|Impostazione|  
    |------------|---------------|------------------|  
    |`Button1`|`Text`|Inizia attività|  
    |`Button2`|`Text`|Cancel|  
    |`Label`|`(Name)`, `Text`|lblPercentDone, 0|  
  
4.  Scegliere **Aggiungi classe** dal menu **Progetto** per aggiungere una classe denominata `Widget.vb` al progetto.  
  
#### Per dichiarare un evento per la classe Widget  
  
-   Utilizzare la parola chiave `Event` per dichiarare un evento nella classe `Widget`.  Si noti che è possibile che a un evento siano associati gli argomenti `ByVal` e `ByRef`, come dimostrato dall'evento `PercentDone` di `Widget`:  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents#1](../../../../visual-basic/programming-guide/language-features/events/codesnippet/visualbasic/VbEventWalkthrough/Widget.vb#1)]  
  
 Quando l'oggetto chiamante riceve un evento `PercentDone`, l'argomento `Percent` indica la percentuale completata dell'attività.  Per annullare il metodo che ha generato l'evento, è possibile impostare su `True` l'argomento `Cancel`.  
  
> [!NOTE]
>  È possibile dichiarare argomenti per gli eventi analogamente a quanto avviene per gli argomenti delle routine. Non è tuttavia possibile specificare per gli eventi argomenti `Optional` o `ParamArray`; gli eventi inoltre non hanno valori restituiti.  
  
 L'evento `PercentDone` viene generato dal metodo `LongTask` della classe `Widget`.  `LongTask` accetta due argomenti: il periodo di tempo apparentemente richiesto dal metodo per eseguire le operazioni e l'intervallo di tempo minimo necessario prima che `LongTask` sospenda le operazioni per generare l'evento `PercentDone`.  
  
#### Per generare l'evento PercentDone  
  
1.  Per semplificare l'accesso alla proprietà `Timer` utilizzata da questa classe, aggiungere un'istruzione `Imports` alla sezione delle dichiarazioni del modulo di classe, sopra l'istruzione `Class Widget`.  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents#2](../../../../visual-basic/programming-guide/language-features/events/codesnippet/visualbasic/VbEventWalkthrough/Widget.vb#2)]  
  
2.  Aggiungere il codice seguente alla classe `Widget`:  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents#3](../../../../visual-basic/programming-guide/language-features/events/codesnippet/visualbasic/VbEventWalkthrough/Widget.vb#3)]  
  
 Quando l'applicazione chiama il metodo `LongTask`, la classe `Widget` genera l'evento `PercentDone` con un intervallo pari ai secondi definiti in `MinimumInterval`.  Al ritorno dell'evento, `LongTask` controlla se l'argomento `Cancel` è stato impostato su `True`.  
  
 A questo punto sono necessarie alcune osservazioni.  Per semplificare, la routine `LongTask` presuppone che si conosca anticipatamente il tempo richiesto dall'attività.  In realtà questo dato non è quasi mai disponibile.  È possibile che la suddivisione delle attività in blocchi di dimensioni uniformi risulti difficoltosa e spesso gli utenti desiderano soprattutto sapere quanto tempo è necessario attendere prima di ottenere un'indicazione relativa a operazioni in corso.  
  
 Nell'esempio riportato è inoltre presente un ulteriore difetto.  La proprietà `Timer` restituisce il numero di secondi dalla mezzanotte. Se avviata poco prima di mezzanotte, l'applicazione non funzionerà in modo corretto.  Per una misurazione più precisa del tempo si consiglia di tenere in considerazione simili limitazioni o di utilizzare proprietà quali `Now`.  
  
 Ora che la classe `Widget` può generare eventi, è possibile passare alla prossima procedura dettagliata.  In [Walkthrough: Handling Events](../../../../visual-basic/programming-guide/language-features/events/walkthrough-handling-events.md) viene illustrato come utilizzare `WithEvents` per associare un gestore eventi all'evento `PercentDone`.  
  
## Vedere anche  
 <xref:Microsoft.VisualBasic.DateAndTime.Timer%2A>   
 <xref:Microsoft.VisualBasic.DateAndTime.Now%2A>   
 [Walkthrough: Handling Events](../../../../visual-basic/programming-guide/language-features/events/walkthrough-handling-events.md)   
 [Events](../../../../visual-basic/programming-guide/language-features/events/events.md)