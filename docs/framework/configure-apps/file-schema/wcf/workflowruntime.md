---
title: "&lt;runtimeFlussoDiLavoro&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 304c70fa-78d1-4d0f-b89f-0ca23d734c6f
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# &lt;runtimeFlussoDiLavoro&gt;
Specifica le impostazioni di un'istanza della classe <xref:System.Workflow.Runtime.WorkflowRuntime> per ospitare servizi [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] basati sul flusso di lavoro.  
  
## Sintassi  
  
```  
  
<workflowRuntime cachedInstanceExpiration="TimeSpan"  
                                  enablePerformanceCounters="Boolean"  
                                  name="String"  
                                  validateOnCreate="Boolean">  
                 <commonParameters>  
                    <add name="String" value="String" />  
                 </commonParameters>  
                 <services>  
                    <add type="String"/>  
                 </services>  
</workflowRuntime>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|cachedInstanceExpiration|Valore <xref:System.Timespan> facoltativo che specifica la durata massima di memorizzazione in stato inattivo di un'istanza del flusso di lavoro prima che venga interrotta o scaricata automaticamente.  Se l'attributo `PersistenceService` di workflowruntime esegue il metodo unloadOnIdle, questo attributo viene ignorato.|  
|enablePerformanceCounters|Valore booleano facoltativo che specifica se i contatori delle prestazioni sono attivi.  I contatori delle prestazioni forniscono informazioni su varie statistiche correlate al flusso di lavoro, ma provocano una riduzione delle prestazioni quando il motore di runtime del flusso di lavoro viene avviato e quando le istanze del flusso di lavoro sono in esecuzione.  Il valore predefinito è `true`.|  
|name|Stringa contenente il nome del motore di runtime del flusso di lavoro.  Il nome viene usato in output per distinguere questo runtime da altri runtime che potrebbero essere in esecuzione nel sistema, ad esempio nei contatori delle prestazioni.<br /><br /> Il valore predefinito è una stringa vuota.|  
|validateOnCreate|Valore booleano facoltativo che specifica se all'apertura dell'elemento WorkflowServiceHost verrà eseguita la convalida della definizione del flusso di lavoro.  Quando questo attributo viene impostato su `true`, la convalida del flusso di lavoro viene eseguita ogni volta che viene chiamato il metodo `WorkflowServiceHost.Open`.  Se vengono individuati errori di convalida, viene generata un'eccezione <xref:System.Workflow.ComponentModel.Compiler.WorkflowValidationFailedException>.<br /><br /> Quando questa proprietà è impostata su `false` la definizione del flusso di lavoro non viene convalidata.<br /><br /> Il valore predefinito di questa proprietà è `true`.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|commonParameters|Raccolta di parametri comuni usati dai servizi.  Questa raccolta in genere contiene la stringa di connessione del database che potrebbe essere condivisa dai servizi durevoli.|  
|servizi|Raccolta di servizi da aggiungere al motore di <xref:System.Workflow.Runtime.WorkflowRuntime>.  Gli elementi sono di tipo <xref:System.Workflow.Runtime.Configuration.WorkflowRuntimeServiceElement>.  I servizi specificati nella raccolta verranno inizializzati dal motore di runtime del flusso di lavoro e verranno aggiunti ai relativi servizi quando verrà chiamato il costruttore <xref:System.Workflow.Runtime.WorkflowRuntime> appropriato.  Pertanto, i servizi specificati nella raccolta devono seguire regole precise riguardanti le firme dei relativi costruttori.  Per altre informazioni, vedere <xref:System.Workflow.Runtime.Configuration.WorkflowRuntimeServiceElement>.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<comportamento\>](../../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md)|Specifica un elemento di comportamento.|  
  
## Note  
 Per altre informazioni sull'utilizzo di un file di configurazione per il controllo del comportamento di un oggetto <xref:System.Workflow.Runtime.WorkflowRuntime> di un'applicazione host di Windows Workflow Foundation, vedere [Workflow Configuration Files](http://msdn.microsoft.com/it-it/ada4bb90-6c9d-4f3d-a9d0-b559bb0f9909).  
  
## Esempio  
  
```  
<serviceBehaviors>  
   <behavior name="ServiceBehavior">  
      <workflowRuntime name="WorkflowServiceHostRuntime"  
                       validateOnCreate="true"  
                       enablePerformanceCounters="true">  
         <commonParameters>  
            <add name="ConnectionString" value="Initial Catalog=WorkflowStore;Data Source=localhost;Integrated Security=SSPI;" />  
            <add name="EnableRetries" value="True" />  
         </commonParameters>  
         <services>  
             <add type="NetFx.Checkin.Scenario.WorkflowServices.WorkflowBasedServices.Common.TestPersistenceService.FilePersistenceService, NetFx.Checkin.Scenario.WorkflowServices.WorkflowBasedServices.Common"/>  
         </services>  
      </workflowRuntime>  
   </behavior>  
</serviceBehaviors>  
```  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.WorkflowRuntimeElement>   
 <xref:System.Workflow.Runtime.Configuration.WorkflowRuntimeServiceElement>   
 <xref:System.Workflow.Runtime.WorkflowRuntime>   
 [Workflow Configuration Files](http://msdn.microsoft.com/it-it/ada4bb90-6c9d-4f3d-a9d0-b559bb0f9909)