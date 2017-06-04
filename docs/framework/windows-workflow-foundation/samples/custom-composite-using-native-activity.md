---
title: "Attivit&#224; composta personalizzata tramite l&#39;oggetto NativeActivity | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ef9e739c-8a8a-4d11-9e25-cb42c62e3c76
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# Attivit&#224; composta personalizzata tramite l&#39;oggetto NativeActivity
In questo esempio viene illustrato come scrivere un oggetto <xref:System.Activities.NativeActivity> che pianifica altri oggetti <xref:System.Activities.Activity> per controllare il flusso dell'esecuzione di un flusso di lavoro.In questo esempio vengono utilizzati due flussi di controllo comuni, Sequence e While, per illustrate le operazioni da eseguire.  
  
## Dettagli dell'esempio  
 Iniziando da `MySequence`, la prima cosa da notare è che deriva da <xref:System.Activities.NativeActivity>.<xref:System.Activities.NativeActivity> è l'oggetto <xref:System.Activities.Activity> che espone l'intero runtime del flusso di lavoro attraverso l'oggetto <xref:System.Activities.NativeActivityContext> passato al metodo `Execute`.  
  
 L'oggetto `MySequence` espone una raccolta pubblica di oggetti <xref:System.Activities.Activity> che viene popolata dall'autore del flusso di lavoro.Prima dell'esecuzione del flusso di lavoro, il relativo runtime chiama il metodo <xref:System.Activities.Activity.CacheMetadata%2A> in ogni attività di un flusso di lavoro.Durante questo processo, il runtime stabilisce relazioni padre\-figlio per l'ambito dei dati e la gestione di durata.L'implementazione predefinita del metodo <xref:System.Activities.Activity.CacheMetadata%2A> utilizza la classe dell'istanza <xref:System.ComponentModel.TypeDescriptor> affinché l'attività `MySequence` aggiunga qualsiasi proprietà pubblica di tipo <xref:System.Activities.Activity> o <xref:System.Collections.IEnumerable>\<<xref:System.Activities.Activity>\> come elementi figlio dell'attività `MySequence`.  
  
 Ogni volta che un'attività espone una raccolta pubblica di attività figlio, è probabile che queste ultime condividano lo stato.Una procedura consigliata per l'attività padre, in questo caso `MySequence`, consiste nell'esporre anche una raccolta di variabili tramite cui le attività figlio possono portare a termine questa operazione.Come nel caso delle attività figlio, il metodo <xref:System.Activities.Activity.CacheMetadata%2A> aggiunge proprietà pubbliche di tipo <xref:System.Activities.Variable> o <xref:System.Collections.IEnumerable>\<<xref:System.Activities.Variable>\> come variabili associate all'attività `MySequence`.  
  
 Oltre alle variabili pubbliche che vengono modificate dagli elementi figlio dell'oggetto `MySequence`, quest'ultimo deve anche tenere traccia della posizione occupata nell'esecuzione dei relativi elementi figlio.Per eseguire questa operazione, utilizza una variabile privata, ovvero `currentIndex`.Questa variabile viene registrata come parte dell'ambiente `MySequence` aggiungendo una chiamata al metodo <xref:System.Activities.NativeActivityMetadata.AddImplementationVariable%2A> all'interno del metodo <xref:System.Activities.Activity.CacheMetadata%2A> dell'attività `MySequence`.Gli oggetti <xref:System.Activities.Activity> aggiunti alla raccolta `MySequence` `Activities` non possono accedere alle variabili aggiunte in questo modo.  
  
 Quando l'oggetto `MySequence` viene eseguito dal runtime, quest'ultimo chiama il metodo <xref:System.Activities.NativeActivity.Execute%2A>, passando un oggetto <xref:System.Activities.NativeActivityContext>.L'oggetto <xref:System.Activities.NativeActivityContext> è il proxy dell'attività di nuovo nel runtime per dereferenziare gli argomenti e le variabili nonché pianificare altri oggetti <xref:System.Activities.Activity> o `ActivityDelegates`.`MySequence` utilizza un metodo `InternalExecute` per incapsulare la logica di pianificazione del primo elemento figlio e di tutti gli elementi figlio successivi in un singolo metodo.Inizia dereferenziando il riferimento `currentIndex`.Se è uguale al conteggio nella raccolta `Activities`, la sequenza è completata, l'attività viene restituita senza pianificare nessuna operazione e lo stato del runtime viene impostato su <xref:System.Activities.ActivityInstanceState>.Se l'oggetto `currentIndex` è inferiore al conteggio delle attività, l'elemento figlio successivo viene ottenuto dalla raccolta `Activities` e l'oggetto `MySequence` chiama il metodo <xref:System.Activities.NativeActivityContext.ScheduleActivity%2A>, passando l'elemento figlio da pianificare e un oggetto <xref:System.Activities.CompletionCallback> che punta al metodo `InternalExecute`.Infine, viene incrementato l'oggetto `currentIndex` e il controllo viene di nuovo restituito al runtime.Finché un'istanza dell'oggetto `MySequence` dispone di un oggetto <xref:System.Activities.Activity> figlio pianificato, il runtime considera che si trovi nello stato Executing.  
  
 Una volta completata l'attività figlio, viene eseguito l'oggetto <xref:System.Activities.CompletionCallback>.Il ciclo continua dall'inizio.Come per `Execute`, un oggetto <xref:System.Activities.CompletionCallback> accetta un oggetto <xref:System.Activities.NativeActivityContext>, consentendo al responsabile dell'implementazione di accedere al runtime.  
  
 L'oggetto `MyWhile` è diverso dall'oggetto `MySequence` in quanto pianifica ripetutamente un singolo oggetto <xref:System.Activities.Activity> e utilizza un oggetto <xref:System.Activities.Activity%601>\<bool\> denominato `Condition` per determinare se è necessario che si verifichi questa pianificazione.Come per `MySequence`, l'oggetto `MyWhile` utilizza un metodo `InternalExecute` per centralizzare la relativa logica di pianificazione.Pianifica l'oggetto `Condition`<xref:System.Activities.Activity>\<bool\> con un oggetto <xref:System.Activities.CompletionCallback%601>\<bool\> denominato `OnEvaluationCompleted`.Quando viene completata l'esecuzione dell'oggetto `Condition`, il risultato diventa disponibile tramite questo oggetto <xref:System.Activities.CompletionCallback> in un parametro fortemente tipizzato denominato `result`.Se `true`, l'oggetto `MyWhile` chiama il metodo <xref:System.Activities.NativeActivityContext.ScheduleActivity%2A>, passando gli oggetti `Body`<xref:System.Activities.Activity> e `InternalExecute` come oggetto <xref:System.Activities.CompletionCallback>.Quando viene completata l'esecuzione dell'oggetto `Body`, l'oggetto `Condition` viene nuovamente pianificato in `InternalExecute`, avviando di nuovo il ciclo.Quando l'oggetto `Condition` restituisce `false`, un'istanza dell'oggetto `MyWhile` restituisce il controllo al runtime senza pianificare l'oggetto `Body` e il runtime ne imposta lo stato su <xref:System.Activities.ActivityInstanceState>.  
  
#### Per impostare, compilare ed eseguire l'esempio  
  
1.  Aprire la soluzione di esempio Composite.sln in [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
2.  Compilare ed eseguire la soluzione.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\CustomActivities\Code-Bodied\CustomCompositeNativeActivity`  
  
## Vedere anche