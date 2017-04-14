---
title: "Events Overview (Windows Forms) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-winforms"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "jsharp"
helpviewer_keywords: 
  - "Windows Forms, event handling"
  - "events [Windows Forms], about events"
  - "delegates [Windows Forms], multicast"
  - "delegates [Windows Forms], events and"
  - "multicast event delegates"
  - "Windows Forms controls, events"
ms.assetid: 814a6a43-a312-4791-88d8-f75f9a4f8c4c
caps.latest.revision: 12
author: "dotnet-bot"
ms.author: "dotnetcontent"
manager: "wpickett"
caps.handback.revision: 12
---
# Events Overview (Windows Forms)
Un evento è un'azione a cui si può rispondere o che può essere "gestita" nel codice.  Gli eventi possono essere generati da un'azione utente, ad esempio un clic del mouse o la pressione di un tasto, oppure da codice programma o dal sistema.  
  
 Le applicazioni basate su eventi eseguono codice in risposta a un evento.  Ogni form e ogni controllo espone un set predefinito di eventi per cui è possibile creare codice.  Se si verifica uno di questi eventi e se il gestore eventi associato include codice, tale codice sarà richiamato.  
  
 Un oggetto può generare diversi tipi di eventi, ma molti tipi sono comuni alla maggior parte dei controlli.  Ad esempio, la maggior parte degli oggetti gestirà un evento <xref:System.Windows.Forms.Control.Click>.  Se un utente fa clic su un form, sarà eseguito il codice disponibile nel gestore eventi <xref:System.Windows.Forms.Control.Click> del codice.  
  
> [!NOTE]
>  Molti eventi si verificano insieme ad altri eventi.  Ad esempio, quando si verifica l'evento <xref:System.Windows.Forms.Control.DoubleClick>, si verificano anche gli eventi <xref:System.Windows.Forms.Control.MouseDown>, <xref:System.Windows.Forms.Control.MouseUp> e <xref:System.Windows.Forms.Control.Click>.  
  
 Per informazioni su come generare e usare un evento, vedere [Eventi](../../../docs/standard/events/index.md).  
  
## Delegati e rispettivo ruolo  
 I delegati sono classi usate comunemente in [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] per creare meccanismi di gestione degli eventi.  È possibile paragonare a grandi linee i delegati ai puntatori a funzioni, usati in genere in [!INCLUDE[vcprvc](../../../includes/vcprvc-md.md)] e in altri linguaggi orientati ad oggetti.  A differenza dei puntatori a funzioni, tuttavia, i delegati sono orientati ad oggetti, indipendenti dai tipi e sicuri.  Mentre un puntatore a funzioni, inoltre, include solo un riferimento a una funzione specifica, un delegato è costituito da un riferimento a un oggetto e fa riferimento a uno o più metodi nell'oggetto.  
  
 Questo modello di eventi usa i *delegati* per associare gli eventi ai metodi usati per gestirli.  Il delegato permette alle altre classi di effettuare la registrazione per la notifica di eventi specificando un metodo del gestore.  Quando si verifica l'evento, il delegato chiama il metodo associato.  Per informazioni su come definire delegati, vedere [Eventi](../../../docs/standard/events/index.md).  
  
 I delegati possono essere associati a un singolo metodo o a più metodi \(multicast\).  Quando si crea un delegato per un evento, l'utente o Progettazione Windows Form creano in genere un evento multicast.  Una rara eccezione può essere costituita da un evento che ha come risultato una procedura specifica, ad esempio la visualizzazione di una finestra di dialogo, che non si ripeterebbe in modo logico più volte per un evento.  Per informazioni su come creare un delegato multicast, vedere [Procedura: combinare delegati multicast](../Topic/How%20to:%20Combine%20Delegates%20\(Multicast%20Delegates\)\(C%23%20Programming%20Guide\).md).  
  
 Un delegato multicast mantiene un elenco di chiamate dei metodi a cui è associato.  Il delegato multicast supporta un metodo <xref:System.Delegate.Combine%2A> per aggiungere un metodo all'elenco di chiamate e un metodo <xref:System.Delegate.Remove%2A> per rimuoverlo.  
  
 Quando un evento è registrato dall'applicazione, il controllo genera l'evento richiamando il delegato corrispondente.  Il delegato chiama a sua volta il metodo associato.  Nel caso più comune, ovvero un delegato multicast, il delegato chiama a turno ogni metodo associato nell'elenco di chiamate, in modo da offrire una notifica di tipo uno\-a\-molti.  In base a questa strategia, il controllo non deve mantenere un elenco di oggetti di destinazione per la notifica di eventi, poiché il delegato gestisce tutte le registrazioni e le notifiche.  
  
 I delegati permettono anche l'associazione di più eventi allo stesso metodo, offrendo una notifica di tipo molti\-a\-uno.  Ad esempio, un evento di selezione di un pulsante e un evento di selezione di un comando di menu possono richiamare lo stesso delegato, che quindi chiama un singolo metodo per gestire questi eventi separati nello stesso modo.  
  
 Il meccanismo di associazione usato con i delegati è dinamico: un delegato può essere associato in fase di esecuzione a qualsiasi metodo la cui firma corrisponda a quella del gestore eventi.  Questa funzionalità consente di impostare o modificare il metodo associato in base a una condizione e di collegare in modo dinamico un gestore eventi a un controllo.  
  
## Vedere anche  
 [Creating Event Handlers in Windows Forms](../../../docs/framework/winforms/creating-event-handlers-in-windows-forms.md)   
 [Event Handlers Overview](../../../docs/framework/winforms/event-handlers-overview-windows-forms.md)