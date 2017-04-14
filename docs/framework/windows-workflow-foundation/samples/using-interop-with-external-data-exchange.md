---
title: "Utilizzo di interoperabilit&#224; con scambio di dati esterni | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 96f6fe26-5305-494f-9119-7748e0c4b3fa
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Utilizzo di interoperabilit&#224; con scambio di dati esterni
L'attività <xref:System.Activities.Statements.Interop> può essere utilizzata per eseguire le attività da [!INCLUDE[wf](../../../../includes/wf-md.md)] in [!INCLUDE[vstecwinfx](../../../../includes/vstecwinfx-md.md)] e [!INCLUDE[netfx35_long](../../../../includes/netfx35-long-md.md)] \(WF3\) e flussi di lavoro all'interno di [!INCLUDE[wf2](../../../../includes/wf2-md.md)] in [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] \(WF4\).In questo esempio viene illustrato come configurare ed eseguire un flusso di lavoro WF3 che utilizza <xref:System.Workflow.Activities.ExternalDataExchangeService> \(e le attività personalizzate corrispondenti per i metodi di chiamata e di gestione degli eventi\) tramite l'attività <xref:System.Activities.Statements.Interop> in un servizio di flusso di lavoro WF4.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Migration\ExternalDataExchange`  
  
#### Per utilizzare questo esempio  
  
1.  Aprire il file ExternalDataExchange.sln in [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
2.  Per compilare l'esempio, premere CTRL\+MAIUSC\+B.  
  
3.  Premere F5 per eseguire l'esempio.