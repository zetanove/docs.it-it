---
title: Dichiarazione e generazione di eventi (Visual Basic) | Documenti di Microsoft
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
- declarations, events
- events [Visual Basic], walkthroughs
- declaring events, walkthroughs
- events [Visual Basic], declaring
- events [Visual Basic], raising
- raising events, walkthroughs
ms.assetid: 8ffb3be8-097d-4d3c-b71e-04555ebda2a2
caps.latest.revision: 16
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
ms.openlocfilehash: 233673c1d42684b7caa9042d18fb341a1043a31b
ms.lasthandoff: 03/13/2017

---
# <a name="walkthrough-declaring-and-raising-events-visual-basic"></a>Procedura dettagliata: dichiarazione e generazione di eventi (Visual Basic)
Questa procedura dettagliata viene illustrato come dichiarare e generare eventi per una classe denominata `Widget`. Dopo aver completato i passaggi, è possibile leggere l'argomento correlato, [procedura dettagliata: gestione degli eventi](../../../../visual-basic/programming-guide/language-features/events/walkthrough-handling-events.md), che illustra come utilizzare gli eventi da `Widget` gli oggetti da fornire informazioni sullo stato in un'applicazione.  
  
## <a name="the-widget-class"></a>La classe Widget  
 Si supponga che si dispone di un `Widget` (classe). La `Widget` classe dispone di un metodo che può richiedere un tempo di esecuzione e si desidera che l'applicazione in grado di venga visualizzato un indicatore di completamento.  
  
 Naturalmente, è possibile apportare il `Widget` oggetto visualizzare una finestra di dialogo percentuale di completamento, ma quindi verrebbe con tale finestra di dialogo in ogni progetto in cui viene utilizzata la `Widget` classe. Una buona regola della progettazione di oggetti consiste nel consentire all'applicazione che utilizza un handle di oggetto dell'interfaccia utente, a meno che non è lo scopo dell'oggetto per la gestione di un modulo o finestra di dialogo.  
  
 Lo scopo di `Widget` per eseguire altre attività, pertanto è consigliabile aggiungere un `PercentDone` evento e consentire alla routine che chiama `Widget`di metodi gestiscono che lo stato di evento e di visualizzare gli aggiornamenti. Il `PercentDone` eventi possono anche fornire un meccanismo per l'annullamento dell'attività.  
  
#### <a name="to-build-the-code-example-for-this-topic"></a>Per compilare l'esempio di codice per questo argomento  
  
1.  Aprire un nuovo [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] applicazione Windows di progetto e creare un form denominato `Form1`.  
  
2.  Aggiungere due pulsanti e un'etichetta a `Form1`.  
  
3.  Denominare gli oggetti come illustrato nella tabella seguente.  
  
    |Oggetto|Proprietà|Impostazione|  
    |------------|--------------|-------------|  
    |`Button1`|`Text`|Attività di avvio|  
    |`Button2`|`Text`|Annulla|  
    |`Label`|`(Name)`, `Text`|lblPercentDone, 0|  
  
4.  Nel **progetto** menu, scegliere **Aggiungi classe** per aggiungere una classe denominata `Widget.vb` al progetto.  
  
#### <a name="to-declare-an-event-for-the-widget-class"></a>Per dichiarare un evento per la classe Widget  
  
-   Utilizzare il `Event` parola chiave per dichiarare un evento nella `Widget` classe. Si noti che un evento può avere `ByVal` e `ByRef` argomenti, come `Widget`del `PercentDone` dimostrato dall'evento:  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents n.&1;](../../../../visual-basic/programming-guide/language-features/events/codesnippet/VisualBasic/walkthrough-declaring-and-raising-events_1.vb)]  
  
 Quando l'oggetto chiamante riceve un `PercentDone` evento, il `Percent` argomento contiene la percentuale di completamento dell'attività. Il `Cancel` argomento può essere impostato su `True` per annullare il metodo che ha generato l'evento.  
  
> [!NOTE]
>  È possibile dichiarare argomenti dell'evento come argomenti di procedure, con le seguenti eccezioni: gli eventi devono avere `Optional` o `ParamArray` gli argomenti e gli eventi non dispongono di valori restituiti.  
  
 Il `PercentDone` evento viene generato dal `LongTask` metodo la `Widget` classe. `LongTask`accetta due argomenti: il periodo di tempo apparentemente richiesto dal metodo eseguire le operazioni e l'intervallo di tempo minimo prima `LongTask` pause per generare il `PercentDone` evento.  
  
#### <a name="to-raise-the-percentdone-event"></a>Per generare l'evento PercentDone  
  
1.  Per semplificare l'accesso per il `Timer` proprietà utilizzata da questa classe, aggiungere un `Imports` istruzione all'inizio della sezione relativa alle dichiarazioni del modulo di classe, sopra il `Class Widget` istruzione.  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents n.&2;](../../../../visual-basic/programming-guide/language-features/events/codesnippet/VisualBasic/walkthrough-declaring-and-raising-events_2.vb)]  
  
2.  Aggiungere il codice seguente alla classe `Widget` :  
  
     [!code-vb[VbVbcnWalkthroughDeclaringAndRaisingEvents n.&3;](../../../../visual-basic/programming-guide/language-features/events/codesnippet/VisualBasic/walkthrough-declaring-and-raising-events_3.vb)]  
  
 Quando l'applicazione chiama il `LongTask` (metodo), il `Widget` classe genera il `PercentDone` evento ogni `MinimumInterval` secondi. Quando termina, l'evento `LongTask` verifica se il `Cancel` argomento è stato impostato su `True`.  
  
 Di seguito sono necessarie alcune osservazioni. Per semplicità, la `LongTask` procedura si presuppone che si conosce in anticipo la durata dell'attività. Ciò avviene quasi mai. Suddivisione delle attività in blocchi di dimensioni pari può essere difficile e spesso gli utenti desiderano soprattutto è semplicemente la quantità di tempo di attesa prima di ottenere un'indicazione che si è verificato.  
  
 In questo esempio si potrebbe individua un difetto di un altro. Il `Timer` proprietà restituisce il numero di secondi trascorsi dalla mezzanotte; pertanto, l'applicazione ottiene bloccata se è stato avviato prima di mezzanotte. Un approccio più precisa per misurare il tempo necessario tenere in considerazione o evitarli del tutto, utilizzando le proprietà, ad esempio `Now`.  
  
 Ora che la `Widget` classe può generare eventi, è possibile spostare la successiva procedura dettagliata. [Procedura dettagliata: Gestione degli eventi](../../../../visual-basic/programming-guide/language-features/events/walkthrough-handling-events.md) viene illustrato come utilizzare `WithEvents` per associare un gestore eventi con il `PercentDone` evento.  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.DateAndTime.Timer%2A></xref:Microsoft.VisualBasic.DateAndTime.Timer%2A>   
 <xref:Microsoft.VisualBasic.DateAndTime.Now%2A></xref:Microsoft.VisualBasic.DateAndTime.Now%2A>   
 [Procedura dettagliata: Gestione degli eventi](../../../../visual-basic/programming-guide/language-features/events/walkthrough-handling-events.md)   
 [Eventi](../../../../visual-basic/programming-guide/language-features/events/index.md)
