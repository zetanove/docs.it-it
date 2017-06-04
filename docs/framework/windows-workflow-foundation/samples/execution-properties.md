---
title: "Propriet&#224; di esecuzione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 31c009db-397c-4653-87e2-32dc77fa4b13
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# Propriet&#224; di esecuzione
In questo esempio viene illustrato come definire e utilizzare una proprietà di esecuzione in un'attività personalizzata.In questo esempio la proprietà di esecuzione determina il colore di primo piano della console.Un flusso di lavoro di esempio illustra come i diversi percorsi logici di esecuzione \(rami di un'attività <xref:System.Activities.Statements.Parallel> \) possono gestire diversi colori della console nonostante esecuzione interleave delle attività \(attraverso i rami dell'attività <xref:System.Activities.Statements.Parallel> \).  
  
#### Per impostare, compilare ed eseguire l'esempio  
  
1.  Aprire la soluzione di esempio ExecutionProperties.sln in [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
    > [!NOTE]
    >  Se si visualizza ThreeColors.xaml prima di compilare la soluzione viene visualizzato un errore, perché le attività personalizzate utilizzate devono essere compilate contemporaneamente alla soluzione.  
  
2.  Compilare ed eseguire la soluzione.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\CustomActivities\Code-Bodied\ExecutionProperties`  
  
## Vedere anche