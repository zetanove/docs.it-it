---
title: "Events (Visual Basic) | Microsoft Docs"
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
  - "events [Visual Basic], about events"
  - "events [Visual Basic]"
ms.assetid: 8fb0353a-e41b-4e23-b78f-da65db832f70
caps.latest.revision: 12
caps.handback.revision: 12
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Events (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Sebbene sia possibile rappresentare graficamente un progetto di [!INCLUDE[vsprvs](../../../../csharp/includes/vsprvs_md.md)] come una serie di procedure eseguite in sequenza, in realtà la maggior parte dei programmi è guidata dagli eventi, ovvero il flusso di esecuzione è determinato da occorrenze esterne denominate *eventi*.  
  
 Un evento è un segnale che informa un'applicazione che si è verificato qualcosa di importante.  Quando ad esempio l'utente fa clic su un controllo in un form, quest'ultimo può generare un evento `Click` e chiamare una routine che gestisce tale evento.  Gli eventi consentono anche la comunicazione tra diverse attività.  Se ad esempio l'applicazione esegue un'attività di ordinamento separatamente rispetto all'applicazione principale,  e l'ordinamento viene annullato dall'utente, l'applicazione può inviare un evento di annullamento che determina l'interruzione del processo di ordinamento.  
  
## Termini e concetti relativi agli eventi  
 In questa sezione vengono descritti i termini e i concetti utilizzati con gli eventi in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
### Dichiarazione di eventi  
 Per dichiarare eventi all'interno di classi, strutture, moduli e interfacce, è possibile utilizzare la parola chiave `Event`, come nell'esempio seguente:  
  
 [!code-vb[VbVbalrEvents#24](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/events_1.vb)]  
  
### Generazione di eventi  
 Un evento è una sorta di messaggio che informa che è accaduto qualcosa di importante.  L'atto di trasmettere il messaggio è detto *generazione* dell'evento.  In [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] è possibile generare eventi con l'istruzione `RaiseEvent`, come nell'esempio seguente:  
  
 [!code-vb[VbVbalrEvents#25](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/events_2.vb)]  
  
 È necessario generare gli eventi nell'ambito della classe, modulo o struttura quando sono dichiarati.  Non è ad esempio possibile che una classe derivata generi eventi ereditati da una classe base.  
  
### Origini eventi  
 Qualsiasi oggetto capace di generare un evento è un *mittente dell'evento*, noto anche come *origine eventi*.  Form, controlli e oggetti definiti dall'utente sono esempi di origini eventi.  
  
### Gestori di eventi  
 I *gestori di eventi* sono routine che vengono richiamate quando si verifica un evento corrispondente.  È possibile utilizzare qualsiasi subroutine valida con una firma corrispondente come gestore di eventi.  Non è invece possibile utilizzare una funzione come gestore di eventi in quanto questa non è in grado di restituire un valore all'origine evento.  
  
 In [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] per i gestori degli eventi viene utilizzata una convenzione di denominazione standard che combina il nome del mittente dell'evento, seguito da un carattere di sottolineatura e dal nome dell'evento.  Ad esempio, l'evento `Click` di un pulsante denominato `button1` verrebbe denominato `Sub button1_Click`.  
  
> [!NOTE]
>  L'utilizzo di questa convenzione di denominazione è consigliato ma non obbligatorio per la definizione dei gestori eventi; è possibile utilizzare qualsiasi nome di subroutine valido.  
  
## Associazione di eventi a gestori di eventi  
 Perché un gestore di eventi diventi utilizzabile, è necessario dapprima associarlo a un evento utilizzando l'istruzione `Handles` o `AddHandler`.  
  
### WithEvents e clausola Handles  
 L'istruzione `WithEvents` e la clausola `Handles` forniscono una modalità dichiarativa per specificare i gestori di eventi.  Un evento generato da un oggetto dichiarato con la parola chiave `WithEvents` può essere gestito mediante qualsiasi routine con un'istruzione `Handles` relativa a tale evento, come illustrato nell'esempio seguente:  
  
 [!code-vb[VbVbalrEvents#1](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/events_3.vb)]  
  
 L'istruzione `WithEvents` e la clausola `Handles` spesso costituiscono la soluzione ottimale per i gestori di eventi, poiché la sintassi dichiarativa che utilizzano semplifica le attività di codifica, lettura e debug per la gestione degli eventi.  Si tengano tuttavia presenti le seguenti limitazioni relative all'utilizzo delle variabili `WithEvents`:  
  
-   Non è possibile utilizzare una variabile `WithEvents` come variabile di oggetto.  In altre parole, non è possibile dichiararla come `Object` ma è necessario specificare il nome della classe quando la si dichiara.  
  
-   Poiché gli eventi condivisi  `` non sono collegati a istanze di classe, non è possibile utilizzare `WithEvents` per gestire eventi condivisi in maniera dichiarativa.  In modo analogo, non è possibile utilizzare `WithEvents` o `Handles` per gestire eventi da una `Structure`.  In entrambi i casi, è possibile utilizzare l'istruzione `AddHandler` per gestire tali eventi.  
  
-   Non è possibile creare matrici di variabili `WithEvents`.  
  
 Le variabili `WithEvents` consentono a unico gestore di eventi di gestire uno o più tipi di evento o a uno o più gestori di eventi di gestire lo stesso tipo di evento.  
  
 Sebbene la clausola `Handles` sia il metodo standard per associare un evento a un gestore di eventi, questa si limita ad associare gli eventi ai gestori di eventi in fase di compilazione.  
  
 In alcuni casi, ad esempio con eventi associati a form o controlli, in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] viene generato automaticamente un gestore degli eventi vuoto che viene associato a un evento.  Quando ad esempio si fa doppio clic su un pulsante di comando in un form in modalità progettazione, [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] crea un gestore degli eventi vuoto e una variabile `WithEvents` per tale pulsante, come nel codice seguente:  
  
 [!code-vb[VbVbalrEvents#26](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/events_4.vb)]  
  
### AddHandler e RemoveHandler  
 L'istruzione `AddHandler` è simile alla clausola `Handles`, poiché entrambe consentono di specificare un gestore eventi.  `AddHandler`, utilizzato con `RemoveHandler`, offre tuttavia un grado superiore di flessibilità rispetto alla clausola `Handles`, in quanto consente di aggiungere, rimuovere e modificare dinamicamente il gestore eventi associato a un evento.  Se si desidera gestire eventi condivisi o eventi da una struttura, è necessario utilizzare `AddHandler`.  
  
 `AddHandler` richiede due argomenti: il nome di un evento da un'origine eventi, ad esempio un controllo, e un'espressione che identifica un delegato.  Con `AddHandler` non è necessario specificare esplicitamente la classe delegata poiché l'istruzione `AddressOf` restituisce sempre un riferimento al delegato.  Di seguito è fornito un esempio di associazione tra un gestore di eventi e un evento generato da un oggetto:  
  
 [!code-vb[VbVbalrEvents#28](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/events_5.vb)]  
  
 `RemoveHandler`, che disconnette un evento da un gestore di eventi, utilizza la stessa sintassi di `AddHandler`.  Di seguito è riportato un esempio:  
  
 [!code-vb[VbVbalrEvents#29](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/events_6.vb)]  
  
 Nell'esempio seguente un gestore degli eventi viene associato a un evento e l'evento viene generato.  Il gestore degli eventi rileva l'evento e visualizza un messaggio.  
  
 Il primo gestore degli eventi viene quindi rimosso e all'evento viene associato un gestore diverso.  Quando l'evento viene generato di nuovo, viene visualizzato un messaggio diverso.  
  
 Infine viene rimosso il secondo gestore degli eventi e l'evento viene generato per la terza volta.  Poiché all'evento non è più associato alcun gestore, non viene eseguita alcuna azione.  
  
 [!code-vb[VbVbalrEvents#38](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/events_7.vb)]  
  
## Gestione di eventi ereditati da una classe base  
 Le *classi derivate*, ossia le classi che ereditano le caratteristiche da una classe base, sono in grado di gestire gli eventi generati dalla classe base utilizzando l'istruzione `Handles` `MyBase`.  
  
#### Per gestire gli eventi ereditati da una classe base  
  
-   Dichiarare un gestore eventi nella classe derivata aggiungendo un'istruzione `Handles MyBase.`*eventname* alla riga della dichiarazione della routine per la gestione di eventi, in cui *eventname* corrisponde al nome dell'evento nella classe base che viene gestita.  Di seguito è riportato un esempio:  
  
     [!code-vb[VbVbalrEvents#12](../../../../visual-basic/language-reference/statements/codesnippet/VisualBasic/events_8.vb)]  
  
## Sezioni correlate  
  
|Titolo|Descrizione|  
|------------|-----------------|  
|[Walkthrough: Declaring and Raising Events](../../../../visual-basic/programming-guide/language-features/events/walkthrough-declaring-and-raising-events.md)|Viene fornita una descrizione dettagliata di come dichiarare e generare eventi per una classe.|  
|[Walkthrough: Handling Events](../../../../visual-basic/programming-guide/language-features/events/walkthrough-handling-events.md)|Viene mostrato come scrivere una routine di gestione di eventi.|  
|[How to: Declare Custom Events To Avoid Blocking](../../../../visual-basic/programming-guide/language-features/events/how-to-declare-custom-events-to-avoid-blocking.md)|Viene mostrato come definire un evento personalizzato che consenta la chiamata asincrona dei gestori eventi.|  
|[How to: Declare Custom Events To Conserve Memory](../../../../visual-basic/programming-guide/language-features/events/how-to-declare-custom-events-to-conserve-memory.md)|Viene mostrato come definire un evento personalizzato che consenta l'uso della memoria solo quando l'evento viene gestito.|  
|[Troubleshooting Inherited Event Handlers in Visual Basic](../../../../visual-basic/programming-guide/language-features/events/troubleshooting-inherited-event-handlers.md)|Vengono elencati problemi comuni relativi ai gestori eventi nei componenti ereditati.|  
|[Eventi](../Topic/Handling%20and%20Raising%20Events.md)|Vengono forniti i cenni preliminari sul modello eventi in [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)].|  
|[Creating Event Handlers in Windows Forms](../Topic/Creating%20Event%20Handlers%20in%20Windows%20Forms.md)|Viene descritto come utilizzare gli eventi associati agli oggetti Windows Form.|  
|[Delegates](../../../../visual-basic/programming-guide/language-features/delegates/delegates.md)|Vengono forniti i cenni preliminari sui delegati di Visual Basic.|