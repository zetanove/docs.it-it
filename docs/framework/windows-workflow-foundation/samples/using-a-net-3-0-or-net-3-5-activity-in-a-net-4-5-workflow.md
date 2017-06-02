---
title: "Utilizzo di un&#39;attivit&#224; di .NET Framework 3.0 o .NET Framework 3.5 in un flusso di lavoro di .NET Framework 4.5 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6c53fd4c-5dd0-4fb4-ab6b-111302629548
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Utilizzo di un&#39;attivit&#224; di .NET Framework 3.0 o .NET Framework 3.5 in un flusso di lavoro di .NET Framework 4.5
L'attività <xref:System.Activities.Statements.Interop> consente di eseguire un'attività [!INCLUDE[wf](../../../../includes/wf-md.md)] di .NET Framework 3.0 in un flusso di lavoro di [!INCLUDE[netfx_current_short](../../../../includes/netfx-current-short-md.md)].In questo esempio viene illustrato come utilizzare l'attività <xref:System.Activities.Statements.Interop> per passare una stringa come argomento a un'attività [!INCLUDE[vstecwinfx](../../../../includes/vstecwinfx-md.md)] personalizzata.  
  
## Per utilizzare questo esempio  
  
1.  In [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] aprire il file della soluzione SimpleInterop.sln.  
  
2.  Per compilare la soluzione, premere CTRL\+MAIUSC\+B.  
  
3.  Per eseguire la soluzione, premere CTRL\+F5.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Migration\SimpleInterop`  
  
## Vedere anche