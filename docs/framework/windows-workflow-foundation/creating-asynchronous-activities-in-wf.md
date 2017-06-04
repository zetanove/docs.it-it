---
title: "Creazione di attivit&#224; asincrone in WF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 497e81ed-5eef-460c-ba55-fae73c05824f
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Creazione di attivit&#224; asincrone in WF
<xref:System.Activities.AsyncCodeActivity> fornisce agli autori dell'attività una classe di base che consente alle attività derivate di implementare la logica di esecuzione asincrona.Ciò si rivela utile per attività personalizzate che devono eseguire un lavoro asincrono senza contenere il thread dell'utilità di pianificazione del flusso di lavoro e senza bloccare nessuna attività che può essere eseguita in parallelo.In questo argomento viene fornita una panoramica su come creare attività asincrone personalizzate utilizzando l'oggetto <xref:System.Activities.AsyncCodeActivity>.  
  
## Utilizzo di AsyncCodeActivity  
 L'oggetto <xref:System.Activities?displayProperty=fullName> fornisce agli autori dell'attività personalizzata classi di base diverse per requisiti di creazione di attività differenti.Ognuna presenta una particolare semantica e offre a un autore del flusso di lavoro \(e al runtime attività\) un contratto corrispondente.Un'attività basata sull'oggetto <xref:System.Activities.AsyncCodeActivity> è un'attività che esegue un lavoro in modo asincrono relativo al thread dell'utilità di pianificazione e la cui logica di esecuzione viene espressa in codice gestito.Come conseguenza di tale modalità asincrona, un oggetto <xref:System.Activities.AsyncCodeActivity> può determinare un punto di inattività durante l'esecuzione.A causa della natura volatile del lavoro asincrono, un oggetto <xref:System.Activities.AsyncCodeActivity> crea sempre un blocco di non persistenza per la durata dell'esecuzione dell'attività.In questo modo si evita che l'esecuzione del flusso di lavoro renda persistente l'istanza del flusso di lavoro durante il lavoro asincrono e si evita anche lo scaricamento dell'istanza del flusso di lavoro mentre il codice asincrono è in esecuzione.  
  
### Metodi AsyncCodeActivity  
 Le attività che derivano dall'oggetto <xref:System.Activities.AsyncCodeActivity> possono creare la logica di esecuzione asincrona eseguendo l'override dei metodi <xref:System.Activities.AsyncCodeActivity.BeginExecute%2A> e <xref:System.Activities.AsyncCodeActivity.EndExecute%2A> con codice personalizzato.Quando chiamati dal runtime, a questi metodi viene passato un oggetto <xref:System.Activities.AsyncCodeActivityContext>.<xref:System.Activities.AsyncCodeActivityContext> consente all'autore dell'attività di fornire lo stato condiviso attraverso <xref:System.Activities.AsyncCodeActivity.BeginExecute%2A>\/ <xref:System.Activities.AsyncCodeActivity.EndExecute%2A> nella proprietà <xref:System.Activities.AsyncCodeActivityContext.UserState%2A> del contesto.Nell'esempio seguente un'attività `GenerateRandom` genera in modo asincrono un numero casuale.  
  
 [!code-csharp[CFX_ActivityExample#8](../../../samples/snippets/csharp/VS_Snippets_CFX/CFX_ActivityExample/cs/Program.cs#8)]  
  
 L'attività dell'esempio precedente deriva da <xref:System.Activities.AsyncCodeActivity%601> e dispone di un oggetto `OutArgument<int>` elevato denominato `Result`.Il valore restituito dal metodo `GetRandom` viene estratto e restituito dall'override del metodo <xref:System.Activities.AsyncCodeActivity%601.EndExecute%2A> e tale valore viene impostato come valore `Result`.Le attività asincrone che non restituiscono un risultato devono derivare da <xref:System.Activities.AsyncCodeActivity>.Nell'esempio seguente viene definita un'attività `DisplayRandom` che deriva da <xref:System.Activities.AsyncCodeActivity>.Questa attività è come l'attività `GetRandom` ma anziché restituire un risultato visualizza un messaggio nella console.  
  
 [!code-csharp[CFX_ActivityExample#11](../../../samples/snippets/csharp/VS_Snippets_CFX/CFX_ActivityExample/cs/Program.cs#11)]  
  
 Notare che a causa dell'assenza di un valore restituito, `DisplayRandom` utilizza <xref:System.Action> anziché <xref:System.Func%602> per richiamare il delegato e il delegato non restituisce alcun valore.  
  
 Anche <xref:System.Activities.AsyncCodeActivity> fornisce un override di <xref:System.Activities.AsyncCodeActivity.Cancel%2A>.Mentre <xref:System.Activities.AsyncCodeActivity.BeginExecute%2A> e <xref:System.Activities.AsyncCodeActivity.EndExecute%2A> sono override obbligatori, <xref:System.Activities.AsyncCodeActivity.Cancel%2A> è facoltativo e può essere sottoposto a override in modo che l'attività possa pulire il relativo stato asincrono in attesa quando è in fase di annullamento o di interruzione.Se la pulizia è possibile e l'oggetto `AsyncCodeActivity.ExecutingActivityInstance.IsCancellationRequested` è `true`, l'attività deve chiamare il metodo <xref:System.Activities.AsyncCodeActivityContext.MarkCanceled%2A>.Qualsiasi eccezione generata da questo metodo è irreversibile per l'istanza del flusso di lavoro.  
  
 [!code-csharp[CFX_ActivityExample#10](../../../samples/snippets/csharp/VS_Snippets_CFX/CFX_ActivityExample/cs/Program.cs#10)]  
  
### Richiamo di metodi asincroni su una classe  
 Molte delle classi in [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] dispongono di funzionalità asincrona che può essere richiamata in modo asincrono tramite un'attività basata su <xref:System.Activities.AsyncCodeActivity>.Nell'esempio seguente di [Utilizzo di AsyncOperationContext in un'attività](../../../docs/framework/windows-workflow-foundation/samples/using-asyncoperationcontext-in-an-activity-sample.md), viene creata un'attività che crea in modo asincrono un file tramite la classe <xref:System.IO.FileStream>.  
  
 [!code-csharp[CFX_ActivityExample#12](../../../samples/snippets/csharp/VS_Snippets_CFX/CFX_ActivityExample/cs/Program.cs#12)]  
  
### Condivisione dello stato tra i metodi BeginExecute e EndExecute  
 Nell'esempio precedente, è stato effettuato l'accesso in <xref:System.Activities.AsyncCodeActivity.EndExecute%2A> all'oggetto <xref:System.IO.FileStream> creato in <xref:System.Activities.AsyncCodeActivity.BeginExecute%2A>.Ciò è possibile poiché la variabile `file` è stata passata nella proprietà <xref:System.Activities.AsyncCodeActivityContext.UserState%2A?displayProperty=fullName> in <xref:System.Activities.AsyncCodeActivity.BeginExecute%2A>.Questo è il metodo corretto per condividere lo stato tra <xref:System.Activities.AsyncCodeActivity.BeginExecute%2A> e <xref:System.Activities.AsyncCodeActivity.EndExecute%2A>.È errato utilizzare una variabile membro nella classe derivata \(in questo caso `FileWriter`\) per condividere lo stato tra <xref:System.Activities.AsyncCodeActivity.BeginExecute%2A> e <xref:System.Activities.AsyncCodeActivity.EndExecute%2A> perché più istanze dell'attività possono fare riferimento agli oggetti attività.Tentare di utilizzare una variabile membro per condividere lo stato può causare la sovrascrizione o la cancellazione di valori da un oggetto <xref:System.Activities.ActivityInstance> a un altro oggetto <xref:System.Activities.ActivityInstance>.  
  
### Accesso ai valori degli argomenti  
 L'ambiente di un oggetto <xref:System.Activities.AsyncCodeActivity> è costituito dagli argomenti definiti nell'attività.L'accesso a questi argomenti può essere eseguito dagli override <xref:System.Activities.AsyncCodeActivity.BeginExecute%2A>\/<xref:System.Activities.AsyncCodeActivity.EndExecute%2A> utilizzando il parametro <xref:System.Activities.AsyncCodeActivityContext>.L'accesso agli argomenti non può essere eseguito nel delegato, ma i valori dell'argomento o i dati desiderati possono essere passati al delegato utilizzando i relativi parametri.Nell'esempio seguente viene definita un'attività che genera un numero casuale e ottiene il limite superiore incluso dal relativo argomento `Max`.Il valore dell'argomento viene passato al codice asincrono quando viene richiamato il delegato.  
  
 [!code-csharp[CFX_ActivityExample#9](../../../samples/snippets/csharp/VS_Snippets_CFX/CFX_ActivityExample/cs/Program.cs#9)]  
  
### Azioni di programmazione o attività figlio utilizzando AsyncCodeActivity  
 Le attività personalizzate derivate <xref:System.Activities.AsyncCodeActivity> forniscono un metodo per eseguire il lavoro in modo asincrono rispetto al thread del flusso di lavoro, ma non consentono di pianificare le attività figlio o le azioni.Tuttavia, il comportamento asincrono può essere incorporato nella pianificazione delle attività figlio tramite la composizione.Un'attività asincrona può essere creata e quindi composta con un'attività <xref:System.Activities.Activity> o <xref:System.Activities.NativeActivity> derivata per fornire il comportamento asincrono e la pianificazione delle attività figlio o delle azioni.Ad esempio, è possibile creare un'attività che deriva da <xref:System.Activities.Activity> e ha come implementazione un oggetto <xref:System.Activities.Statements.Sequence> che contiene l'attività asincrona nonché le altre attività che implementano la logica dell'attività.Per ulteriori esempi sulla composizione di attività tramite <xref:System.Activities.Activity> e <xref:System.Activities.NativeActivity>, vedere [Procedura: creare un'attività](../../../docs/framework/windows-workflow-foundation//how-to-create-an-activity.md), [Opzioni di creazione di attività](../../../docs/framework/windows-workflow-foundation//activity-authoring-options-in-wf.md) e gli esempi delle attività [Composito](../../../docs/framework/windows-workflow-foundation/samples/composite.md).  
  
## Vedere anche  
 <xref:System.Action>   
 <xref:System.Func%602>   
 [Utilizzo di AsyncOperationContext in un'attività](../../../docs/framework/windows-workflow-foundation/samples/using-asyncoperationcontext-in-an-activity-sample.md)