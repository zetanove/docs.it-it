---
title: "Architettura del flusso di lavoro di Windows | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1d4c6495-d64a-46d0-896a-3a01fac90aa9
caps.latest.revision: 20
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 20
---
# Architettura del flusso di lavoro di Windows
[!INCLUDE[wf](../../../includes/wf-md.md)] genera il livello di astrazione per lo sviluppo di applicazioni interattive con esecuzione prolungata.Le unità di lavoro vengono incapsulate come attività.Le attività vengono eseguite in un ambiente che fornisce funzionalità per il controllo del flusso, gestione delle eccezioni, propagazione degli errori, persistenza dei dati relativi allo stato, caricamento e scaricamento di flussi di lavoro in corso dalla memoria, rilevamento e flusso della transazione.  
  
## Architettura dell'attività  
 Le attività vengono sviluppate come tipi CLR che derivano dall'oggetto <xref:System.Activities.Activity>, <xref:System.Activities.CodeActivity>, <xref:System.Activities.AsyncCodeActivity> o <xref:System.Activities.NativeActivity> o dalle relative varianti che restituiscono un valore, <xref:System.Activities.Activity%601>, <xref:System.Activities.CodeActivity%601>, <xref:System.Activities.AsyncCodeActivity%601> o <xref:System.Activities.NativeActivity%601>.Lo sviluppo di attività che derivano dall'oggetto <xref:System.Activities.Activity> consente all'utente di assemblare attività preesistenti per creare rapidamente unità di lavoro che vengono eseguite nell'ambiente del flusso di lavoro.L'oggetto <xref:System.Activities.CodeActivity>, d'altra parte, consente la creazione della logica di esecuzione nel codice gestito utilizzando l'oggetto <xref:System.Activities.CodeActivityContext> principalmente per accedere agli argomenti delle attività.L'oggetto <xref:System.Activities.AsyncCodeActivity> è simile a <xref:System.Activities.CodeActivity> con la differenza che può essere utilizzato per implementare attività asincrone.Lo sviluppo di attività che derivano dall'oggetto <xref:System.Activities.NativeActivity> consente agli utenti di accedere al runtime tramite l'oggetto <xref:System.Activities.NativeActivityContext> per funzionalità quali la pianificazione di elementi figlio, la creazione di segnalibri, il richiamo di lavori asincroni, la registrazione di transazioni e così via.  
  
 La creazione di attività che derivano dall'oggetto <xref:System.Activities.Activity> è dichiarativa e questa attività possono essere create in XAML.Nell'esempio seguente viene creata un'attività denominata `Prompt` utilizzando altre attività per il corpo dell'esecuzione.  
  
```  
<Activity x:Class='Prompt'  
  xmlns:x='http://schemas.microsoft.com/winfx/2006/xaml'  
    xmlns:z='http://schemas.microsoft.com/netfx/2008/xaml/schema'  
xmlns:my='clr-namespace:XAMLActivityDefinition;assembly=XAMLActivityDefinition'  
xmlns:s="clr-namespace:System;assembly=mscorlib"  
xmlns="http://schemas.microsoft.com/2009/workflow">  
<z:SchemaType.Members>  
    <z:SchemaType.SchemaProperty Name='Text' Type=' InArgument(s:String)' />  
  <z:SchemaType.SchemaProperty Name='Response' Type='OutArgument(s:String)' />  
</z:SchemaType.Members>  
  <Sequence>  
    <my:WriteLine Text='[Text]' />  
    <my:ReadLine BookmarkName='r1' Result='[Response]' />  
  </Sequence>  
</Activity>  
```  
  
## Contesto dell'attività  
 L'oggetto <xref:System.Activities.ActivityContext> rappresenta l'interfaccia tra l'autore di attività e l'esecuzione del flusso di lavoro e fornisce l'accesso alle numerose funzionalità di esecuzione.Nell'esempio seguente viene definita un'attività che utilizza il contesto di esecuzione per creare un segnalibro \(meccanismo che consente a un'attività di registrare un punto di continuazione nella relativa esecuzione che può essere ripresa da un host che passa dati all'attività\).  
  
 [!code-csharp[CFX_WorkflowApplicationExample#15](../../../samples/snippets/csharp/VS_Snippets_CFX/cfx_workflowapplicationexample/cs/program.cs#15)]  
  
## Ciclo di vita dell'attività  
 Un'istanza di un'attività viene avviata nello stato <xref:System.Activities.ActivityInstanceState>.A meno che non si verifichino eccezioni, rimane in questo stato finché non viene completata l'esecuzione di tutte le attività figlio e di qualsiasi altro lavoro in sospeso \(ad esempio gli oggetti <xref:System.Activities.Bookmark>\); al termine dell'esecuzione esegue la transizione allo stato <xref:System.Activities.ActivityInstanceState>.L'elemento padre di un istanza dell'attività può richiedere l'annullamento di un elemento figlio. Se quest'ultimo può essere annullato, viene completato nello stato <xref:System.Activities.ActivityInstanceState>.Se durante l'esecuzione viene generata un'eccezione, il runtime passa l'attività nello stato <xref:System.Activities.ActivityInstanceState> e propaga l'eccezione fino alla catena di attività padre.Di seguito sono riportati i tre stati di completamento di un'attività:  
  
-   **Closed:** l'attività ha completato il proprio lavoro ed è stata chiusa.  
  
-   **Canceled:** l'attività ha interrotto normalmente il proprio lavoro ed è stata chiusa.Quando viene immesso questo stato, il lavoro non viene sottoposto a rollback in modo esplicito.  
  
-   **Faulted:** l'attività ha rilevato un errore ed è stata chiusa prima del completamento del lavoro.  
  
 Le attività rimangono nello stato <xref:System.Activities.ActivityInstanceState> quando sono persistenti o vengono scaricate.