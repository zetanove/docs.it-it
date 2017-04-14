---
title: "Utilizzo dell&#39;attivit&#224; InvokeMethod | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b6643550-d043-4ac7-8069-9c55ebbb4233
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Utilizzo dell&#39;attivit&#224; InvokeMethod
In questo esempio viene illustrato come utilizzare l'attività <xref:System.Activities.Statements.InvokeMethod%601> per richiamare metodi pubblici nelle classi pubbliche.L'attività <xref:System.Activities.Statements.InvokeMethod%601> consente a un flusso di lavoro di chiamare metodi negli oggetti, passare parametri, ottenere il valore restituito, specificare tipi per i metodi generici e indicare se il metodo è sincrono o asincrono.  
  
 Esiste una versione non generica dell'attività <xref:System.Activities.Statements.InvokeMethod> in cui il valore restituito viene impostato sulla proprietà <xref:System.Activities.Statements.InvokeMethod.Result%2A> e una versione generica dell'attività <xref:System.Activities.Statements.InvokeMethod%601> in cui la restituzione del valore viene eseguita tramite la proprietà <xref:System.Activities.Statements.InvokeMethod.Result%601.Result%2A> di tipo `TResult`.  
  
 In questo esempio viene illustrato come chiamare diversi tipi di metodo.Nell'elenco seguente sono indicati in dettaglio i tipi di metodo illustrati nell'esempio:  
  
-   Richiamare un metodo di istanza senza parametri.  
  
-   Richiamare un metodo di istanza con due parametri \(System.String e System.Int32\).  
  
-   Richiamare un metodo di istanza con due parametri \(System.String e System.Int32\) e una matrice di parametri di tipo System.String\[\].  
  
-   Richiamare un metodo di istanza con due parametri \(due numeri System.Int32\) e un risultato di tipo System.Int32.  
  
     Il valore restituito viene associato a una variabile e stampato nella console tramite l'attività <xref:System.Activities.Statements.WriteLine>.  
  
-   Richiamare un metodo statico con due parametri \(System.String e System.Int32\).  
  
-   Richiamare un metodo di istanza con un parametro generico \(System.String\).  
  
-   Richiamare un metodo statico con due parametri generici \(System.String e System.Int32\).  
  
-   Richiamare un metodo di istanza che dispone di un parametro passato dal riferimento \(System.String\).  
  
     Il parametro a cui si fa riferimento viene associato a una variabile e stampato nella console tramite l'attività <xref:System.Activities.Statements.WriteLine>.  
  
-   Richiamare un metodo di istanza asincrono.  
  
## Per utilizzare questo esempio  
  
1.  In [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] aprire il file della soluzione InvokeMethodUsage.sln.  
  
2.  Per compilare la soluzione, premere CTRL\+MAIUSC\+B.  
  
3.  Per eseguire la soluzione, premere CTRL\+F5.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Built-InActivities\InvokeMethod`  
  
## Vedere anche