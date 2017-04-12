---
title: Eventi (Visual Basic) | Microsoft Docs
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
- events [Visual Basic], about events
- events [Visual Basic]
ms.assetid: 8fb0353a-e41b-4e23-b78f-da65db832f70
caps.latest.revision: 12
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
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 625f4b24dde4200187e1339983d89b9ce92609c9
ms.lasthandoff: 03/13/2017

---
# <a name="events-visual-basic"></a>Eventi (Visual Basic)
Sebbene sia possibile rappresentare graficamente un progetto [!INCLUDE[vsprvs](../../../../csharp/includes/vsprvs_md.md)] come una serie di procedure eseguite in sequenza, in realtà, la maggior parte dei programmi è basata su eventi, ovvero il flusso di esecuzione è determinato da occorrenze esterne denominate *eventi*.  
  
 Un evento è un segnale che informa un'applicazione che si è verificato qualcosa di importante. Ad esempio, quando un utente fa clic su un controllo in un form, il form può generare un evento `Click` e chiamare una routine che gestisce l'evento. Gli eventi consentono anche le comunicazioni tra attività separate. Si supponga, ad esempio, che un'applicazione esegua un'attività di ordinamento separatamente dall'applicazione principale. Se un utente annulla l'ordinamento, l'applicazione può inviare un evento di annullamento per segnalare la necessità di interrompere il processo di ordinamento.  
  
## <a name="event-terms-and-concepts"></a>Termini e concetti relativi agli eventi  
 Questa sezione descrive i termini e i concetti usati con gli eventi in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
### <a name="declaring-events"></a>Dichiarazione di eventi  
 Gli eventi vengono dichiarati all'interno di classi, strutture, moduli e interfacce tramite la parola chiave `Event`, come nell'esempio seguente:  
  
 [!code-vb[VbVbalrEvents#24](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/events_1.vb)]  
  
### <a name="raising-events"></a>Generazione di eventi  
 Un evento può essere paragonato a un messaggio che annuncia che si è verificato qualcosa di importante. L'atto di trasmettere il messaggio viene definito *generazione* dell'evento. In [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)], gli eventi vengono generati con l'istruzione `RaiseEvent`, come nell'esempio seguente:  
  
 [!code-vb[VbVbalrEvents#25](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/events_2.vb)]  
  
 Gli eventi devono essere generati nell'ambito della classe, del modulo o della struttura in cui sono dichiarati. Ad esempio, una classe derivata non può generare eventi ereditati da una classe di base.  
  
### <a name="event-senders"></a>Mittenti di eventi  
 Qualsiasi oggetto in grado di generare un evento è un *mittente di eventi*, noto anche come *origine di eventi*. I form, i controlli e gli oggetti definiti dall'utente sono alcuni esempi di mittenti di eventi.  
  
### <a name="event-handlers"></a>Gestori eventi  
 I *gestori eventi* sono le routine chiamate quando si verifica un evento corrispondente. È possibile usare qualsiasi subroutine valida con una firma corrispondente come gestore eventi. Non è possibile usare una funzione come gestore eventi, tuttavia, perché non può restituire un valore all'origine di eventi.  
  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] usa una convenzione di denominazione standard per i gestori eventi che combina il nome del mittente dell'evento, un carattere di sottolineatura e il nome dell'evento. Ad esempio, il nome dell'evento `Click` per un pulsante denominato `button1` sarebbe `Sub button1_Click`.  
  
> [!NOTE]
>  È consigliabile usare questa convenzione di denominazione durante la definizione dei gestori per gli eventi personalizzati, ma non è obbligatorio. Si può usare qualsiasi nome di subroutine valido.  
  
## <a name="associating-events-with-event-handlers"></a>Associazione di eventi a gestori eventi  
 Un gestore eventi diventa utilizzabile solo dopo averlo associato a un evento mediante l'istruzione `Handles` o `AddHandler`.  
  
### <a name="withevents-and-the-handles-clause"></a>WithEvents e clausola Handles  
 L'istruzione `WithEvents` e la clausola `Handles` offrono una modalità dichiarativa per specificare i gestori eventi. Un evento generato da un oggetto dichiarato con la parola chiave `WithEvents` può essere gestito da qualsiasi routine con un'istruzione `Handles` per tale evento, come illustrato nell'esempio seguente:  
  
 [!code-vb[VbVbalrEvents#1](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/events_3.vb)]  
  
 L'istruzione `WithEvents` e la clausola `Handles` rappresentano spesso la scelta migliore per i gestori eventi, perché la sintassi dichiarativa che usano semplifica la scrittura del codice, la lettura e il debug per la gestione degli eventi. Tenere presenti, tuttavia, le limitazioni seguenti per l'uso delle variabili `WithEvents`:  
  
-   Non è possibile usare una variabile `WithEvents` come variabile oggetto, ovvero non è possibile dichiararla come `Object`, ma è necessario specificare il nome della classe quando si dichiara la variabile.  
  
-   Dato che gli eventi condivisi non sono associati a istanze di classe, non è possibile usare `WithEvents` per gestire in modo dichiarativo eventi condivisi. In modo analogo, non è possibile usare `WithEvents` o `Handles` per gestire gli eventi da `Structure`. In entrambi i casi, è possibile usare l'istruzione `AddHandler` per gestire tali eventi.  
  
-   Non è possibile creare matrici di variabili `WithEvents`.  
  
 Le variabili `WithEvents` consentono a un unico gestore eventi di gestire uno o più tipi di evento oppure a uno o più gestori eventi di gestire lo stesso tipo di evento.  
  
 Anche se la clausola `Handles` rappresenta la modalità standard per associare un evento a un gestore eventi, è limitata all'associazione di eventi a gestori eventi in fase di compilazione.  
  
 In alcuni casi, ad esempio con gli eventi associati a form o controlli, [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] sottopone automaticamente a stub un gestore eventi vuoto e lo associa a un evento. Ad esempio, quando si fa doppio clic su un pulsante di comando in un form in modalità progettazione, [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] crea un gestore eventi vuoto e una variabile `WithEvents` per il pulsante di comando, come nel codice seguente:  
  
 [!code-vb[VbVbalrEvents#26](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/events_4.vb)]  
  
### <a name="addhandler-and-removehandler"></a>AddHandler e RemoveHandler  
 L'istruzione `AddHandler` è simile alla clausola `Handles`, perché entrambe consentono di specificare un gestore eventi. Tuttavia, l'uso di `AddHandler` con `RemoveHandler` offre una maggiore flessibilità rispetto alla clausola `Handles`, perché consente di aggiungere, rimuovere e modificare dinamicamente il gestore eventi associato a un evento. Per gestire eventi condivisi o eventi da una struttura, è necessario usare `AddHandler`.  
  
 `AddHandler` accetta due argomenti: il nome di un evento da un mittente di eventi, ad esempio un controllo e un'espressione che restituisce un delegato. Non è necessario specificare in modo esplicito la classe delegata quando si usa `AddHandler`, perché l'istruzione `AddressOf` restituisce sempre un riferimento al delegato. L'esempio seguente associa un gestore eventi a un evento generato da un oggetto:  
  
 [!code-vb[VbVbalrEvents#28](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/events_5.vb)]  
  
 `RemoveHandler`, che disconnette un evento da un gestore eventi, usa la stessa sintassi di `AddHandler`. Ad esempio:  
  
 [!code-vb[VbVbalrEvents#29](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/events_6.vb)]  
  
 Nell'esempio seguente un gestore eventi viene associato a un evento e l'evento viene generato. Il gestore eventi intercetta l'evento e visualizza un messaggio.  
  
 Il primo gestore eventi viene quindi rimosso e all'evento viene associato un diverso gestore eventi. Quando l'evento viene generato di nuovo, viene visualizzato un messaggio diverso.  
  
 Infine, il secondo gestore eventi viene rimosso e viene generato l'evento per una terza volta. Dato che all'evento non è più associato un gestore eventi, non viene eseguita alcuna azione.  
  
 [!code-vb[VbVbalrEvents#38](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/events_7.vb)]  
  
## <a name="handling-events-inherited-from-a-base-class"></a>Gestione degli eventi ereditati da una classe di base  
 *Le classi derivate*, ovvero le classi che ereditano le caratteristiche da una classe di base, possono gestire gli eventi generati dalla rispettiva classe di base usando l'istruzione `Handles``MyBase`.  
  
#### <a name="to-handle-events-from-a-base-class"></a>Per gestire gli eventi da una classe di base  
  
-   Dichiarare un gestore eventi nella classe derivata aggiungendo un'istruzione `Handles MyBase.`*nomeevento* alla riga della dichiarazione della routine del gestore eventi, dove *nomeevento* è il nome dell'evento nella classe di base che si sta gestendo. Ad esempio:  
  
     [!code-vb[VbVbalrEvents#12](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/events_8.vb)]  
  
## <a name="related-sections"></a>Sezioni correlate  
  
|Titolo|Descrizione|  
|-----------|-----------------|  
|[Procedura dettagliata: Dichiarazione e generazione di eventi](../../../../visual-basic/programming-guide/language-features/events/walkthrough-declaring-and-raising-events.md)|Descrizione dettagliata della procedura per dichiarare e generare eventi per una classe.|  
|[Procedura dettagliata: Gestione di eventi](../../../../visual-basic/programming-guide/language-features/events/walkthrough-handling-events.md)|Illustra come scrivere una routine di gestore eventi.|  
|[Procedura: Dichiarare eventi personalizzati per evitare il blocco](../../../../visual-basic/programming-guide/language-features/events/how-to-declare-custom-events-to-avoid-blocking.md)|Illustra come definire un evento personalizzato che consente la chiamata asincrona dei gestori eventi.|  
|[Procedura: Dichiarare eventi personalizzati per proteggere la memoria](../../../../visual-basic/programming-guide/language-features/events/how-to-declare-custom-events-to-conserve-memory.md)|Illustra come definire un evento personalizzato che usa la memoria solo quando viene gestito l'evento.|  
|[Risoluzione dei problemi relativi ai gestori eventi ereditati in Visual Basic](../../../../visual-basic/programming-guide/language-features/events/troubleshooting-inherited-event-handlers.md)|Elenca i problemi comuni che si verificano con i gestori eventi nei componenti ereditati.|  
|[Eventi](http://msdn.microsoft.com/library/b6f65241-e0ad-4590-a99f-200ce741bb1f)|Panoramica del modello di eventi usato in [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)].|  
|[Creazione di gestori eventi in Windows Form](https://msdn.microsoft.com/library/dacysss4.aspx)|Descrive come usare gli eventi associati agli oggetti di Windows Form.|  
|[Delegati](../../../../visual-basic/programming-guide/language-features/delegates/index.md)|Panoramica dei delegati in Visual Basic.|
