---
title: "&lt;workflowUnhandledException&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "reference"
ms.assetid: 57adeab5-f06a-44b2-916b-0e177cf0f4a6
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# &lt;workflowUnhandledException&gt;
Comportamento del servizio che consente di specificare l'azione da intraprendere quando si verifica un'eccezione non gestita all'interno di un servizio flusso di lavoro.  
  
## Sintassi  
  
```  
  
<behaviors>  
  <serviceBehaviors>  
    <behavior name=String">  
      <workflowUnhandledException action=”Abandon/AbandonAndSuspend/Cancel/Terminate” />  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
  
```  
  
## Attributi ed elementi  
 Le sezioni seguenti descrivono gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|action|Stringa che specifica l'azione da intraprendere quando si verifica un'eccezione non gestita.  L'attributo è di tipo <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionaction>.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<behavior\> di \<serviceBehaviors\>](../../../../../docs/framework/configure-apps/file-schema/windows-workflow-foundation/behavior-of-servicebehaviors-of-workflow.md)|Specifica un elemento di comportamento.|  
  
## Vedere anche  
 <xref:System.ServiceModel.Activities.Description.WorkflowUnhandledExceptionBehavior>   
 <xref:System.ServiceModel.Activities.Configuration.WorkflowUnhandledExceptionElement>