---
title: "Esposizione e richiamo di ActivityAction | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 97ce4797-426e-463d-9cc4-1261afad6df4
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# Esposizione e richiamo di ActivityAction
In questo esempio viene illustrato come sviluppare un'attività personalizzata che dispone di un oggetto <xref:System.Activities.ActivityAction>.Viene inoltre illustrato come utilizzare questa attività fornendo un'implementazione dell'oggetto <xref:System.Activities.ActivityAction>.  
  
 Un oggetto <xref:System.Activities.ActivityAction> consente a un autore di attività di esporre "problemi di sicurezza" relativi a firme specifiche a cui l'utente di attività può associare un comportamento personalizzato.Ad esempio, l'attività <xref:System.Activities.Statements.ForEach> \(che agisce su una raccolta di elementi\) dispone di un oggetto <xref:System.Activities.ActivityAction> che consente all'utente di attività di associare un comportamento che agisce sull'elemento di iterazione corrente.  
  
#### Per impostare, compilare ed eseguire l'esempio  
  
1.  Aprire la soluzione di esempio **ActivityAction.sln** in [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
2.  Compilare ed eseguire la soluzione.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\CustomActivities\Code-Bodied\ActivityAction`  
  
## Vedere anche