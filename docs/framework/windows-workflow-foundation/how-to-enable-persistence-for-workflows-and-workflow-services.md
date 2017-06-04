---
title: "Procedura: abilitare la persistenza per i flussi di lavoro e i relativi servizi | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2b1c8bf3-9866-45a4-b06d-ee562393e503
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Procedura: abilitare la persistenza per i flussi di lavoro e i relativi servizi
In questo argomento viene descritto come abilitare la persistenza dei flussi di lavoro e dei servizi flusso di lavoro.  
  
## Abilitare la persistenza dei flussi di lavoro  
 È possibile associare un archivio di istanze a un oggetto **WorkflowApplication** tramite la proprietà <xref:System.Activities.WorkflowApplication.InstanceStore%2A> della classe <xref:System.Activities.WorkflowApplication>.Il metodo <xref:System.Activities.WorkflowApplication.Persist%2A> salva o rende persistente un flusso di lavoro nell'archivio di istanze associato all'applicazione.Il metodo <xref:System.Activities.WorkflowApplication.Unload%2A> rende persistente un flusso di lavoro nell'archivio di istanze, quindi scarica l'istanza dalla memoria.Il metodo **Load** carica un flusso di lavoro in memoria utilizzando i dati del flusso di lavoro archiviati nell'archivio di persistenza dell'istanza.  
  
 Il metodo **Persist** effettua i passaggi seguenti:  
  
1.  Sospende l'utilità di pianificazione del flusso di lavoro e attende finché il flusso di lavoro non entra nello stato inattivo.  
  
2.  Rende persistente o salva il flusso di lavoro nell'archivio di persistenza.  
  
3.  Riprende l'utilità di pianificazione del flusso di lavoro.  
  
 Il metodo **Unload** effettua i passaggi seguenti:  
  
1.  Sospende l'utilità di pianificazione del flusso di lavoro e attende finché il flusso di lavoro non entra nello stato inattivo.  
  
2.  Rende persistente o salva il flusso di lavoro nell'archivio di persistenza.  
  
3.  Elimina l'istanza del flusso di lavoro nella memoria.  
  
 Entrambi i metodi **Persist** e **Unload** verranno bloccati mentre un flusso di lavoro si trova in un'area di non persistenza finché non esce da tale area.Il metodo continua l'operazione di persistenza o di scarico una volta completata l'area di non persistenza.Se l'area di non persistenza non viene completata prima della scadenza del timeout, o se il processo di persistenza impiega molto tempo, verrà generata un'eccezione TimeoutException.  
  
## Abilitare la persistenza dei servizi di flusso di lavoro nel codice  
 Il membro **DurableInstancingOptions** della classe <xref:System.ServiceModel.WorkflowServiceHost> dispone di una proprietà denominata **InstanceStore** che può essere utilizzata per associare un archivio di istanze all'oggetto **WorkflowServiceHost**.  
  
```  
  
// wsh is an instance of WorkflowServiceHost class  
wsh.DurableInstancingOptions.InstanceStore = new SqlWorkflowInstanceStore();  
  
```  
  
 Quando l'oggetto **WorkflowServiceHost** viene aperto, la persistenza viene abilitata automaticamente se l'oggetto **DurableInstancingOptions.InstanceStore** non è Null.  
  
 In genere, un comportamento del servizio fornisce l'archivio di istanze concreto da utilizzare con un host del servizio flusso di lavoro tramite la proprietà **InstanceStore**.L'oggetto SqlWorkflowInstanceStoreBehavior ad esempio crea un'istanza dell'oggetto **SqlWorkflowInstanceStore**, lo configura e lo assegna all'oggetto **DurableInstancingOptions.InstanceStore**.  
  
## Abilitare la persistenza per i servizi di flusso di lavoro tramite un file di configurazione dell'applicazione.  
 È possibile abilitare la persistenza utilizzando un file di configurazione dell'applicazione tramite l'aggiunta al file app.config o web.config del codice riportato di seguito:  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name=”myBehavior”>  
          <SqlWorkflowInstanceStore connectionString=”Data Source=myDatatbaseServer;Initial Catalog=myPersistenceDatabase”>  
        </behavior>  
      </serviceBehaviors>  
    <behaviors>  
  </system.serviceModel>  
</configuration>  
  
```