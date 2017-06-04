---
title: "Utilizzo delle attivit&#224; WF di .NET Framework 3.0 in .NET Framework 4 con l&#39;attivit&#224; Interop | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 71f112ba-abb0-46f7-b05f-a5d2eb9d0c5c
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# Utilizzo delle attivit&#224; WF di .NET Framework 3.0 in .NET Framework 4 con l&#39;attivit&#224; Interop
Il <xref:System.Activities.Statements.Interop> attività è un [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] attività (WF 4.5) che esegue il wrapping di un [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)] attività (WF 3.5) all'interno di un [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] flusso di lavoro. L'attività di WF 3 può essere una singola attività foglia o un intero albero di attività. L'esecuzione (annullamento e gestione delle eccezioni inclusi) e la persistenza dell'attività di [!INCLUDE[netfx35_short](../../../includes/netfx35-short-md.md)] si verificano all'interno del contesto dell'istanza del flusso di lavoro di [!INCLUDE[netfx_current_short](../../../includes/netfx-current-short-md.md)] in esecuzione.  
  
> [!NOTE]
>  Il <xref:System.Activities.Statements.Interop> attività non viene visualizzato nella casella degli strumenti della finestra di progettazione del flusso di lavoro a meno che non dispone di progetto del flusso di lavoro relativo **Framework di destinazione** impostazione **.NET Framework 4.5**.  
  
## <a name="criteria-for-using-a-wf-3-activity-with-an-interop-activity"></a>Criteri per l'uso di un'attività di WF 3 con un'attività di interoperabilità  
 Per un'attività di WF 3 venga eseguita correttamente all'interno di un <xref:System.Activities.Statements.Interop> attività, devono essere soddisfatti i criteri seguenti:  
  
-   L'attività di WF 3 deve derivare da <xref:System.Workflow.ComponentModel.Activity?displayProperty=fullName>.  
  
-   L'attività di WF 3 deve essere dichiarata come `public` e non può essere `abstract`.  
  
-   L'attività di WF 3 deve disporre di un costruttore predefinito pubblico.  
  
-   A causa delle limitazioni nell'interfaccia di tipi di <xref:System.Activities.Statements.Interop> attività può supportare, <xref:System.Workflow.Activities.HandleExternalEventActivity> e <xref:System.Workflow.Activities.CallExternalMethodActivity> non possono essere usate direttamente, ma derivative attività create usando lo strumento di attività di comunicazione del flusso di lavoro (WCA.exe) può essere utilizzato. Vedere [Strumenti di Windows Workflow Foundation](http://go.microsoft.com/fwlink/?LinkId=178889) per informazioni dettagliate.  
  
## <a name="configuring-a-wf-3-activity-within-an-interop-activity"></a>Configurazione di un'attività di WF 3 all'interno di un'attività di interoperabilità  
 Per configurare e passare i dati in e da un'attività di WF 3, oltre i limiti di interoperabilità, l'attività di WF 3 proprietà e le proprietà dei metadati vengono esposti dal <xref:System.Activities.Statements.Interop> attività. Proprietà dei metadati dell'attività di WF 3 (ad esempio <xref:System.Workflow.ComponentModel.Activity.Name%2A>) vengono esposti tramite il <xref:System.Activities.Statements.Interop.ActivityMetaProperties%2A> insieme. Si tratta di una raccolta di coppie nome-valore usata per definire i valori delle proprietà dei metadati dell'attività di WF 3. Una proprietà dei metadati è una proprietà supportata dalla proprietà di dipendenza per il quale il <xref:System.Workflow.ComponentModel.DependencyPropertyOptions> flag è impostato.  
  
 Proprietà dell'attività di WF 3 sono esposte tramite il <xref:System.Activities.Statements.Interop.ActivityProperties%2A> insieme. Si tratta di un set di coppie nome-valore, in cui ogni valore è un <xref:System.Activities.Argument> oggetto usato per definire gli argomenti per le proprietà dell'attività di WF 3. Poiché la direzione di una proprietà di attività di WF 3 non può essere dedotto, ogni proprietà viene esposto come un <xref:System.Activities.InArgument>/<xref:System.Activities.OutArgument> coppia. A seconda dell'utilizzo dell'attività della proprietà, si desidera fornire un <xref:System.Activities.InArgument> voce, un <xref:System.Activities.OutArgument> voce o entrambi. Il nome previsto del <xref:System.Activities.InArgument> voce nella raccolta è il nome della proprietà come definito nell'attività di WF 3. Il nome previsto del <xref:System.Activities.OutArgument> voce nella raccolta è una concatenazione del nome della proprietà e la stringa "Out".  
  
## <a name="limitations-of-using-a-wf-3-activity-within-an-interop-activity"></a>Limitazioni sull'utilizzo di un'attività di WF 3 all'interno di un'attività di interoperabilità  
 L'attività di WF 3 fornite dal sistema non può essere incluso direttamente in un <xref:System.Activities.Statements.Interop> attività. Per alcune attività di WF 3, ad esempio <xref:System.Workflow.Activities.DelayActivity>, perché vi è un'attività di WF 4.5 analoga. Per altre, è invece dovuto al fatto che la funzionalità dell'attività non è supportata. Molte attività WF 3 fornite dal sistema possono essere utilizzate in flussi di lavoro sottoposto a wrapping dal <xref:System.Activities.Statements.Interop> attività, soggetti alle restrizioni seguenti:  
  
1.  <xref:System.ServiceModel.Activities.Send> e <xref:System.ServiceModel.Activities.Receive> non può essere utilizzato un <xref:System.Activities.Statements.Interop> attività.  
  
2.  <xref:System.Workflow.Activities.WebServiceInputActivity>, <xref:System.Workflow.Activities.WebServiceOutputActivity>, e <xref:System.Workflow.Activities.WebServiceFaultActivity> non può essere utilizzato all'interno di un <xref:System.Activities.Statements.Interop> attività.  
  
3.  <xref:System.Workflow.Activities.InvokeWorkflowActivity> non può essere utilizzato all'interno di un <xref:System.Activities.Statements.Interop> attività.  
  
4.  <xref:System.Workflow.ComponentModel.SuspendActivity> non può essere utilizzato all'interno di un <xref:System.Activities.Statements.Interop> attività.  
  
5.  Attività correlate alla compensazione non può essere utilizzata all'interno di un <xref:System.Activities.Statements.Interop> attività.  
  
 Esistono inoltre alcune specifiche di comportamento importanti per l'utilizzo delle attività di WF 3 all'interno di <xref:System.Activities.Statements.Interop> attività:  
  
1.  WF 3 attività contenute all'interno di un <xref:System.Activities.Statements.Interop> attività vengono inizializzate quando il <xref:System.Activities.Statements.Interop> attività viene eseguita. In WF 4.5 non esiste alcuna fase di inizializzazione di un'istanza del flusso di lavoro precedente alla relativa esecuzione.  
  
2.  Il runtime di WF 4.5 non non stato dell'istanza del flusso di lavoro checkpoint quando inizia una transazione, indipendentemente in cui inizia quella transazione (all'interno o all'esterno di un <xref:System.Activities.Statements.Interop> attività).  
  
3.  Record di rilevamento 3 WF per le attività all'interno di un <xref:System.Activities.Statements.Interop> attività vengono forniti ai partecipanti di rilevamento di WF 4.5 come <xref:System.Activities.Tracking.InteropTrackingRecord> oggetti. <xref:System.Activities.Tracking.InteropTrackingRecord> è un derivato di <xref:System.Activities.Tracking.CustomTrackingRecord>.  
  
4.  Un'attività personalizzata di WF 3 può accedere ai dati usando le code del flusso di lavoro all'interno dell'ambiente di interazione, esattamente come avviene all'interno del runtime del flusso di lavoro WF 3. Non è richiesta alcuna modifica al codice di attività personalizzata. Sull'host, i dati vengono accodati a una coda del flusso di lavoro di WF 3 Riprendendo un <xref:System.Activities.Bookmark>. Il nome del segnalibro è il formato della stringa di <xref:System.IComparable> nome della coda del flusso di lavoro.  
  
## <a name="see-also"></a>Vedere anche  
 [Utilizzo di attività di .NET Framework 3.5 di .NET Framework 3.0 in un flusso di lavoro di .NET Framework 4.5](../../../docs/framework/windows-workflow-foundation/samples/using-a-net-3-0-or-net-3-5-activity-in-a-net-4-5-workflow.md)