---
title: "Concetti di base del flusso di lavoro di Windows | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0e930e80-5060-45d2-8a7a-95c0690105d4
caps.latest.revision: 27
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 27
---
# Concetti di base del flusso di lavoro di Windows
Lo sviluppo di flussi di lavoro in [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] si basa su concetti che potrebbero risultare nuovi ad alcuni sviluppatori.In questo argomento vengono descritti alcuni dei concetti e la relativa implementazione.  
  
## Flussi di lavoro e attività  
 Un flusso di lavoro è una raccolta strutturata di azioni che modella un processo.Ogni azione del flusso di lavoro viene modellata come un'attività.Un host interagisce con un flusso di lavoro utilizzando l'oggetto <xref:System.Activities.WorkflowInvoker> per richiamare un flusso di lavoro come se si trattasse di un metodo, l'oggetto <xref:System.Activities.WorkflowApplication> per controllare in modo esplicito l'esecuzione di una singola istanza del flusso di lavoro e l'oggetto <xref:System.ServiceModel.WorkflowServiceHost> per le interazioni basate su messaggi negli scenari a istanza multipla.Poiché i passaggi del flusso di lavoro sono definiti come una gerarchia di attività, si può affermare che l'attività in primo piano nella gerarchia definisce il flusso di lavoro stesso.Questo modello di gerarchia sostituisce le classi `SequentialWorkflow` e `StateMachineWorkflow` esplicite delle versioni precedenti.Le attività stesse vengono sviluppate come raccolte di altre attività \(utilizzando la classe <xref:System.Activities.Activity> come base che generalmente viene definita tramite XAML\) oppure sono personalizzate tramite la classe <xref:System.Activities.CodeActivity> che può utilizzare il runtime per accedere ai dati oppure la classe <xref:System.Activities.NativeActivity> che espone la varietà del runtime del flusso di lavoro all'autore di attività.Le attività sviluppate utilizzando le classi <xref:System.Activities.CodeActivity> e <xref:System.Activities.NativeActivity> vengono create tramite linguaggi conformi a CLR, ad esempio C\#.  
  
## Modello di dati delle attività  
 Le attività archiviano e condividono i dati utilizzando i tipi mostrati nella tabella seguente.  
  
|||  
|-|-|  
|Variabile|Archivia i dati in un'attività.|  
|Argomento|Sposta i dati all'interno e all'esterno di un'attività.|  
|Espressione|Attività con un valore restituito elevato utilizzato nelle associazioni degli argomenti.|  
  
## Runtime del flusso di lavoro  
 Il runtime del flusso di lavoro è un ambiente in cui vengono eseguiti i flussi di lavoro.<xref:System.Activities.WorkflowInvoker> è la modalità di base per eseguire un flusso di lavoro.L'host utilizza l'oggetto <xref:System.Activities.WorkflowInvoker> per eseguire le operazioni seguenti:  
  
-   Per richiamare in modo sincrono un flusso di lavoro.  
  
-   Per fornire input o recuperare output da un flusso di lavoro.  
  
-   Per aggiungere estensioni che devono essere utilizzate dalle attività.  
  
 L'oggetto <xref:System.Activities.ActivityInstance> è il proxy thread\-safe che gli host possono utilizzare per interagire con il runtime.L'host utilizza l'oggetto <xref:System.Activities.ActivityInstance> per eseguire le operazioni seguenti:  
  
-   Per acquisire un'istanza creandola o caricandola da un archivio di istanze.  
  
-   Per ricevere una notifica sugli eventi del ciclo di vita delle istanze.  
  
-   Per controllare l'esecuzione del flusso di lavoro.  
  
-   Per fornire input o recuperare output da un flusso di lavoro.  
  
-   Per segnalare la continuazione di un flusso di lavoro e passare i valori a tale flusso.  
  
-   Per rendere persistenti i dati del flusso di lavoro.  
  
-   Per aggiungere estensioni che devono essere utilizzate dalle attività.  
  
 Le attività accedono all'ambiente di runtime del flusso di lavoro tramite la classe derivata <xref:System.Activities.ActivityContext> appropriata, quale <xref:System.Activities.NativeActivityContext> o <xref:System.Activities.CodeActivityContext>.In questo modo possono risolvere argomenti e variabili, pianificare le attività figlio ed eseguire molte altre operazioni.  
  
## Servizi  
 I flussi di lavoro rappresentano un modo semplice per implementare e accedere a servizi loosely\-coupled utilizzando le attività di messaggistica.Le attività di messaggistica si basano su [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] e sono il meccanismo principale utilizzato per ottenere dati all'interno e all'esterno di un flusso di lavoro.È possibile comporre insieme attività di messaggistica per modellare qualsiasi tipo di modello di scambio di messaggi desiderato.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)] vedere [Attività di messaggistica](../../../docs/framework/wcf/feature-details/messaging-activities.md).I servizi di flusso di lavoro sono ospitati utilizzando la classe <xref:System.ServiceModel.Activities.WorkflowServiceHost>.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)][Panoramica dell'hosting dei servizi flusso di lavoro](../../../docs/framework/wcf/feature-details/hosting-workflow-services-overview.md).[!INCLUDE[crabout](../../../includes/crabout-md.md)] Servizi di flusso di lavoro vedere [Servizi flusso di lavoro](../../../docs/framework/wcf/feature-details/workflow-services.md)  
  
## Persistenza, scaricamento e flussi di lavoro con esecuzione prolungata  
 Il flusso di lavoro di Windows semplifica la creazione di programmi reattivi con esecuzione prolungata fornendo:  
  
-   Attività che accedono all'input esterno.  
  
-   Possibilità di creare oggetti <xref:System.Activities.Bookmark> che possono essere ripresi da un listener di host.  
  
-   Possibilità di rendere persistenti i dati di un flusso di lavoro e di scaricare quest'ultimo, quindi di ricaricarlo e riattivarlo in risposta alla ripresa di oggetti <xref:System.Activities.Bookmark> in un particolare flusso di lavoro.  
  
 Un flusso di lavoro esegue continuamente attività finché non sono terminate o finché tutte le attività attualmente in esecuzione stanno aspettando l'input.In quest'ultimo caso, il flusso di lavoro è inattivo.È normale che i flussi di lavoro che si trovano nello stato di inattività vengono scaricati e ricaricati dall'host per continuare l'esecuzione quando arriva un messaggio.<xref:System.ServiceModel.Activities.WorkflowServiceHost> fornisce la funzionalità per questa funzione e fornisce un criterio estendibile di scaricamento.Per i blocchi di esecuzione che utilizzando dati allo stato volatile o altri dati che non possono essere resi persistenti, un'attività può indicare a un host che non deve essere resa persistente utilizzando l'oggetto <xref:System.Activities.NoPersistHandle>.Un flusso di lavoro può rendere esplicitamente persistenti i propri dati in un supporto di archiviazione durevole tramite l'attività <xref:System.Activities.Statements.Persist>.