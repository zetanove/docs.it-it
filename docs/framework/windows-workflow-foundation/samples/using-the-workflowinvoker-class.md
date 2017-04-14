---
title: "Utilizzo della classe WorkflowInvoker | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0a966164-3990-4e78-8aa2-c6797ebbee94
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Utilizzo della classe WorkflowInvoker
In questo esempio viene illustrato come utilizzare la classe <xref:System.Activities.WorkflowInvoker> per richiamare un'attività come se fosse un metodo.  
  
## Dettagli dell'esempio  
 L'utilizzo della classe <xref:System.Activities.WorkflowInvoker> è il modo più semplice per eseguire un'attività.È progettata per eseguire direttamente un'attività come una chiamata al metodo.Questa API ad alte prestazioni, leggera e semplice da utilizzare in scenari in cui l'esecuzione di un'attività non richiede l'infrastruttura di controllo fornita da altre varianti di hosting.  
  
 Nell'esempio viene utilizzata un'attività personalizzata che deriva da <xref:System.Activities.CodeActivity%601>\<Int32\> denominata `Add` che aggiunge due <xref:System.Activities.InArgument%601>, `X` e `Y` e restituisce `Result`<xref:System.Activities.OutArgument%601>.\(<xref:System.Activities.CodeActivity%601>\<T\> deriva da <xref:System.Activities.Activity%601>\<T\>che dispone di un oggetto <xref:System.Activities.OutArgument%601>\<T\> denominato `Result`.\) `Dictionary`\<stringa, oggetto\> viene utilizzato per passare argomenti in un'attività richiamata tramite <xref:System.Activities.WorkflowInvoker>.La chiave del dizionario corrisponde al nome di un argomento nell'attività richiamata.Il valore associato a una particolare chiave viene associato all'argomento identificato dalla chiave.  
  
 Nell'esempio viene chiamato <xref:System.Activities.WorkflowInvoker.Invoke%2A> e viene passato un dizionario che contiene valori per `X` e `Y`.La classe <xref:System.Activities.WorkflowInvoker> associa questi valori agli argomenti dell'attività `Add`, esegue l'attività e restituisce il risultato.  
  
#### Per utilizzare questo esempio  
  
1.  Tramite [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] aprire il file della soluzione Invoker.sln.  
  
2.  Per compilare la soluzione, premere CTRL\+MAIUSC\+B.  
  
3.  Per eseguire la soluzione, premere F5.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Execution\WorkflowInvoker`  
  
## Vedere anche