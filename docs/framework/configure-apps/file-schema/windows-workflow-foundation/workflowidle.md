---
title: "&lt;workflowIdle&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: b2ef703c-3e01-4213-9d2e-c14c7dba94d2
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# &lt;workflowIdle&gt;
Un comportamento del servizio che controlla quando istanze del flusso di lavoro inattive vengono scaricate e rese persistenti.  
  
## Sintassi  
  
```  
  
<behaviors>  
  <serviceBehaviors>  
    <behavior name=String">  
      <workflowIdle timeToPersist=”TimeSpan”  
          timeToUnload=”TimeSpan” />  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
  
```  
  
## Attributi ed elementi  
 Le sezioni seguenti descrivono gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|timeToPersist|Valore TimeSpan che specifica l'intervallo di tempo tra l'ora in cui il flusso di lavoro diventa inattivo e quella in cui viene reso persistente.  Il valore predefinito è TimeSpan.MaxValue.<br /><br /> L'intervallo di tempo inizia quando l'istanza del flusso di lavoro diventa inattiva.  Questo attributo è utile se si desidera imporre la persistenza di un'istanza del flusso di lavoro e al tempo stesso memorizzare l'istanza per il periodo di tempo più lungo possibile.  Questo attributo è valido solo se il relativo valore è inferiore a quello dell'attributo **timeToUnload**.  Se è superiore, verrà ignorato.  Se l'intervallo di tempo specificato da questo attributo scade prima del valore specificato dall'attributo **timeToUnload**, è necessario completare prima la persistenza per poter scaricare il flusso di lavoro.  Questo significa che l'operazione di scaricamento può essere ritardata fino a quando il flusso di lavoro non verrà reso persistente.  Il livello di persistenza è responsabile della gestione dei tentativi effettuati in presenza di errori temporanei e genera eccezioni solo per gli errori irreversibili.  Le eventuali eccezioni generate durante la persistenza vengono pertanto considerate fatali e l'istanza del flusso di lavoro viene interrotta.|  
|timeToUnload|Valore TimeSpan che specifica l'intervallo di tempo tra l'ora in cui il flusso di lavoro diventa inattivo e quella in cui viene scaricato.  Il valore predefinito è 1 minuto.<br /><br /> Lo scaricamento di un flusso di lavoro lo rende anche persistente.  Se questo attributo viene impostato su zero, l'istanza del flusso di lavoro viene resa persistente e scaricata immediatamente dopo che il flusso di lavoro diventa inattivo.  L'impostazione di questo attributo su TimeSpan.MaxValue comporta in realtà la disabilitazione dell'operazione di scaricamento.  Le istanze del flusso di lavoro inattive non vengono mai scaricate.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<behavior\> di \<serviceBehaviors\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/behavior-of-servicebehaviors-of-workflow.md)|Specifica un elemento di comportamento.|  
  
## Vedere anche  
 <xref:System.ServiceModel.Activities.Description.WorkflowIdleBehavior>   
 <xref:System.ServiceModel.Activities.Configuration.WorkflowIdleElement>