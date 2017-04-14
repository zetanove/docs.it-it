---
title: "Utilizzo di AsyncOperationContext in un esempio di attivit&#224; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0888a0bd-d227-4c00-ad6a-b654a01740e8
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# Utilizzo di AsyncOperationContext in un esempio di attivit&#224;
In questo esempio viene dimostrato come sviluppare un oggetto <xref:System.Activities.CodeActivity> personalizzato che utilizza <xref:System.Activities.AsyncOperationContext> per eseguire operazioni asincrone al di fuori del flusso di lavoro.  
  
## Dettagli dell'esempio  
 L'attività di esempio utilizza i metodi <xref:System.IO.FileStream.BeginWrite> e <xref:System.IO.FileStream.EndWrite> nella classe <xref:System.IO.FileStream> per scrivere in modo asincrono dati in un file.Il modello introdotto qui può essere adattato per l'utilizzo con gli altri metodi asincroni.Mentre l'operazione asincrona è in esecuzione, possono essere eseguite le altre attività nel flusso di lavoro, ma il flusso di lavoro non può essere salvato in modo permanente.  
  
#### Per impostare, compilare ed eseguire l'esempio  
  
1.  Aprire la soluzione di esempio Async.sln in [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
2.  Compilare ed eseguire la soluzione.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\CustomActivities\Code-Bodied\Async`  
  
## Vedere anche