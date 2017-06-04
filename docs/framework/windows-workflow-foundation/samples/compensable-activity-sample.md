---
title: "Esempio di CompensableActivity | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 58f4898c-b2b8-44a4-9a73-3bef4da6d5ba
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# Esempio di CompensableActivity
In questo esempio viene illustrato come utilizzare l'attività `CompensableActivity` per definire il lavoro da eseguire per un'azione specificata durante la normale esecuzione e il lavoro che è necessario eseguire per compensare tale azione, se necessario in un secondo tempo.Nella prima parte dell'esempio viene illustrato come possono essere definite unità di lavoro compensabile in [!INCLUDE[wf](../../../../includes/wf-md.md)] utilizzando un'attività `CompensableActivity` e come vengono eseguiti in un'esecuzione riuscita.Nella seconda parte dell'esempio viene illustrato in che modo le stesse unità di lavoro compensabile eseguono automaticamente la compensazione quando viene rilevato un evento imprevisto e l'istanza del flusso di lavoro viene annullata.  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Tramite Visual Studio 2010 aprire CompensableActivity.sln.  
  
2.  Premere CTRL\+MAIUSC\+B per compilare la soluzione,  
  
3.  Eseguire l'applicazione premendo F5.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Compensation\BasicCompensableActivity`  
  
## Vedere anche