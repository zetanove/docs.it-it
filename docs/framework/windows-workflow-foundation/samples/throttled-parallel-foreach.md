---
title: "ThrottledParallelForEach | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f2855b5f-e9a7-433d-96a4-40fc31025215
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# ThrottledParallelForEach
L'attività `ThrottleParallelForEach` è simile all'attività <xref:System.Activities.Statements.ParallelForEach> con l'unica eccezione che consente l'impostazione di un fattore di concorrenza per limitare il numero di rami simultanei da eseguire.L'attività `ThrottleParallelForEach` deriva dall'oggetto <xref:System.Activities.NativeActivity>, poiché deve pianificare altre attività \(le attività figlio\) ed è accessibile solo tramite la classe <xref:System.Activities.NativeActivityContext>.  
  
## Progetti  
  
||||  
|-|-|-|  
|**Nome progetto**|**Descrizione**|**File principali**|  
|ThrottledParallelForEach|Contiene l'attività `ThrottledParallelForEach` e la relativa finestra di progettazione.|ThrottledParallelForEach.cs<br /><br /> Definizione dell'attività `ThrottledParallelForEach`.|  
|CodeTestClient|Applicazione client di esempio che configura ed esegue un flusso di lavoro con un oggetto `ThrottledParallelForEach` utilizzando il codice imperativo.|Program.cs<br /><br /> Definisce ed esegue un'istanza del flusso di lavoro di esempio.|  
  
#### Per utilizzare questo esempio  
  
1.  In [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] aprire il file della soluzione ThrottledParallelForEach.sln.  
  
2.  Per compilare la soluzione, premere CTRL\+MAIUSC\+B.  
  
3.  Per eseguire la soluzione, premere F5.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\ThrottledParallelForEach`  
  
## Vedere anche