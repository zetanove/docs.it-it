---
title: "Opzioni di creazione di attivit&#224; in WF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b9061f5f-12c3-47f0-adbe-1330e2714c94
caps.latest.revision: 20
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 20
---
# Opzioni di creazione di attivit&#224; in WF
In [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] sono disponibili numerose opzioni per la creazione di attività personalizzate.  Il metodo corretto da usare per la creazione di un'attività specifica dipende dalle funzionalità di runtime richieste.  
  
## Scelta della classe di attività di base da usare per la creazione di attività personalizzate  
 Nella tabella seguente sono elencate le funzionalità disponibili nelle classi di base di attività personalizzate.  
  
|Classe di attività di base|Funzionalità disponibili|  
|--------------------------------|------------------------------|  
|<xref:System.Activities.Activity>|Compone gruppi di attività fornite dal sistema e personalizzate in un'attività composita.|  
|<xref:System.Activities.CodeActivity>|Implementa la funzionalità imperativa fornendo un metodo <xref:System.Activities.CodeActivity%601.Execute%2A> di cui può essere eseguito l'override.  Inoltre fornisce l'accesso a rilevamenti, variabili e argomenti.|  
|<xref:System.Activities.NativeActivity>|Fornisce tutte le funzionalità dell'oggetto <xref:System.Activities.CodeActivity>, oltre all'interruzione dell'esecuzione di attività, all'annullamento dell'esecuzione di attività figlio, all'utilizzo di segnalibri e alla pianificazione di attività, azioni di attività e funzioni.|  
|<xref:System.Activities.DynamicActivity>|Fornisce un approccio di tipo DOM alla costruzione di attività che si interfacciano con l'utilità di progettazione di WF e il sistema di runtime tramite l'oggetto <xref:System.ComponentModel.IcustomTypeDescriptor>, consentendo la creazione di nuove attività senza definire nuovi tipi.|  
  
## Creazione di attività tramite la classe Activity  
 Le attività che derivano dalla classe <xref:System.Activities.Activity> compongono la funzionalità assemblando altre attività esistenti.  Queste attività possono essere attività personalizzate esistenti e attività dell'apposita libreria di [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)].  L'assemblaggio di queste attività è il modo più comunemente usato per creare la funzionalità personalizzata.  Questo approccio viene generalmente adottato quando si usa un ambiente di progettazione visiva per la creazione di flussi di lavoro.  
  
## Creazione di attività tramite CodeActivity o AsyncCodeActivity  
 Le attività che derivano dalla classe <xref:System.Activities.CodeActivity> o <xref:System.Activities.AsyncCodeActivity> possono implementare la funzionalità imperativa eseguendo l'override del metodo <xref:System.Activities.CodeActivity%601.Execute%2A> con codice imperativo personalizzato.  Il codice personalizzato viene eseguito quando l'attività viene eseguita dal runtime.  Le attività create in questo modo possono accedere alla funzionalità personalizzata, ma non a tutte le funzionalità del runtime, ad esempio non dispongono dell'accesso completo all'ambiente di esecuzione, non dispongono della capacità di pianificare le attività figlio, di creare segnalibri o di supportare un metodo Cancel o Abort.  Quando una classe <xref:System.Activities.CodeActivity> viene eseguita, dispone dell'accesso a una versione ridotta dell'ambiente di esecuzione \(tramite la classe <xref:System.Activities.CodeActivityContext> o <xref:System.Activities.AsyncCodeActivityContext>\).  Le attività create usando la classe <xref:System.Activities.CodeActivity> dispongono dell'accesso alla risoluzione di argomenti e variabili, alle estensioni e ai rilevamenti.  La pianificazione di attività asincrone può essere eseguita usando la classe <xref:System.Activities.AsyncCodeActivity>.  
  
## Creazione di attività tramite la classe NativeActivity  
 Le attività che derivano dalla classe <xref:System.Activities.NativeActivity>, come quelle che derivano dalla classe <xref:System.Activities.CodeActivity> creano la funzionalità imperativa eseguendo l'override del metodo <xref:System.Activities.NativeActivity.Execute%2A>, ma dispongono anche dell'accesso a tutta la funzionalità del runtime del flusso di lavoro tramite la classe <xref:System.Activities.NativeActivityContext> che viene passata al metodo <xref:System.Activities.NativeActivity.Execute%2A>.  Questo contesto supporta la pianificazione e l'annullamento di attività figlio, eseguendo gli oggetti <xref:System.Activities.ActivityAction> e <xref:System.Activities.ActivityFunc>, propagando le transazioni in un flusso di lavoro, richiamando i processi asincroni, annullando e interrompendo l'esecuzione, accedendo alle proprietà e alle estensioni di esecuzione e ai segnalibri \(handle per il ripristino dei flussi di lavoro sospesi\).  
  
## Creazione di attività tramite la classe DynamicActivity  
 A differenza degli altri tre tipi di attività, non viene creata una nuova funzionalità derivando nuovi tipi dalla classe <xref:System.Activities.DynamicActivity> \(la classe è sealed\), bensì assemblando la funzionalità nelle proprietà <xref:System.Activities.DynamicActivity.Properties%2A> e <xref:System.Activities.DynamicActivity.Implementation%2A> tramite un modello a oggetti documento \(DOM\) dell'attività.  
  
## Creazione di attività che restituiscono un risultato  
 Molte attività devono restituire un risultato dopo la relativa esecuzione.  Anche se a tal fine è sempre possibile definire un oggetto <xref:System.Activities.OutArgument%601> personalizzato in un'attività, è consigliabile usare invece l'oggetto <xref:System.Activities.Activity%601> o derivare dall'oggetto <xref:System.Activities.CodeActivity%601> o <xref:System.Activities.NativeActivity%601>.  Ognuna di queste classi di base dispone di un oggetto <xref:System.Activities.OutArgument%601> denominato Result che l'attività può usare per il relativo valore restituito.  Le attività che restituiscono un risultato devono essere usate solo se solo un risultato deve essere restituito da un'attività. Se devono essere restituiti più risultati, è necessario usare i membri <xref:System.Activities.OutArgument%601> separati.