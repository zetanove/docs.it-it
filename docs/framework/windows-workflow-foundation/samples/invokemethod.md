---
title: "InvokeMethod | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 04988eb3-65f8-456d-b1bd-509f5d05a57c
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# InvokeMethod
In questo esempio vengono illustrate le diverse modalità di utilizzo dell'attività <xref:System.Activities.Statements.InvokeMethod> per richiamare metodi di una classe.  
  
 Un metodo appartiene a una classe e rappresenta un set di operazioni autonomo.L'attività <xref:System.Activities.Statements.InvokeMethod> consente di chiamare metodi in base a oggetti o tipi, passare parametri e ottenere il valore restituito.È possibile richiamare i metodi in modo sincrono o asincrono.  
  
## Dettagli dell'esempio  
 In questo esempio viene utilizzata l'attività <xref:System.Activities.Statements.InvokeMethod> per eseguire gli scenari seguenti:  
  
1.  Richiamare un metodo di istanza senza parametri.  
  
2.  Richiamare un metodo di istanza con due parametri \(<xref:System.String> e <xref:System.Int32>\).  
  
3.  Richiamare un metodo di istanza con due parametri \(<xref:System.String> e <xref:System.Int32>\) e una matrice di parametri di tipo <xref:System.String>\[\].  
  
4.  Richiamare un metodo di istanza con due parametri di tipo <xref:System.Int32> e un risultato di tipo <xref:System.Int32>.In questo scenario il valore restituito viene associato a una variabile e utilizzato in un'altra attività.Viene visualizzato nella console utilizzando l'attività <xref:System.Activities.Statements.WriteLine>.  
  
5.  Richiamare un metodo statico con due parametri di tipo <xref:System.String> e <xref:System.Int32>.  
  
6.  Richiamare un metodo di istanza con un parametro generico di tipo <xref:System.String>.  
  
7.  Richiamare un metodo statico con due parametri generici di tipo <xref:System.String> e <xref:System.Int32>.  
  
8.  Richiamare un metodo di istanza che dispone di un parametro passato da un riferimento di tipo <xref:System.String>.In questo scenario il parametro di riferimento viene associato a una variabile \(`outParam`\) e utilizzato in un'altra attività.Viene visualizzato nella console utilizzando l'attività <xref:System.Activities.Statements.WriteLine>.  
  
9. Richiamare un metodo di istanza asincrono.  
  
10. Richiamare due metodi diversi nella stessa istanza di un oggetto utilizzando due attività <xref:System.Activities.Statements.InvokeMethod>.  
  
11. Archiviare un valore in un'istanza di un oggetto.  
  
12. Recuperare un valore da un'istanza di un oggetto.  
  
## Per utilizzare questo esempio  
 Questo esempio è fornito in due versioni.La prima versione di questo esempio, che si trova nella cartella CodedWorkflow\\CS, illustra l'utilizzo di <xref:System.Activities.Statements.InvokeMethod> tramite codice C\# utilizzando il modello di programmazione [!INCLUDE[wf](../../../../includes/wf-md.md)].La seconda versione, che si trova nella cartella DesignerWorkflow\\CS, illustra l'utilizzo di <xref:System.Activities.Statements.InvokeMethod> tramite XAML.  
  
#### Per eseguire l'esempio di flusso di lavoro codificato  
  
1.  Tramite [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] aprire il file della soluzione InvokeMethodUsage.sln nella cartella CodedWorkflow\\CS.  
  
2.  Per compilare la soluzione, premere CTRL\+MAIUSC\+B.  
  
3.  Per eseguire la soluzione, premere CTRL\+F5.  
  
#### Per eseguire l'esempio di flusso di lavoro di progettazione  
  
1.  Tramite [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] aprire il file della soluzione InvokeMethodUsage.sln nella cartella DesignerWorkflow\\CS.  
  
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