---
title: "Utilizzo di ExpressionTextBox in un ActivityDesigner personalizzato | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f82e73e7-a256-4a4d-82b7-c0d62f4ab5e7
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Utilizzo di ExpressionTextBox in un ActivityDesigner personalizzato
In questo esempio viene illustrato come utilizzare l'oggetto <xref:System.Activities.Presentation.View.ExpressionTextBox> in un ActivityDesigner personalizzato.L'attività personalizzata, `MultiAssign`, assegna due valori stringa a due variabili di stringa.Alcuni controlli <xref:System.Activities.Presentation.View.ExpressionTextBox> vengono associati a oggetti <xref:System.Activities.InArgument> mentre altri a oggetti <xref:System.Activities.OutArgument>.  
  
## Dettagli dell'esempio  
 L'oggetto `ArgumentToExpressionConverter` è il convertitore di tipi utilizzato in caso di associazione di espressioni agli argomenti.La proprietà `ConverterParameter` deve essere impostata su `In`, `Out`, a seconda delle esigenze.L'oggetto `InOut` non è supportato.  
  
 L'attributo `UseLocationExpression` viene utilizzato in oggetti `OutArgument` per specificare che l'espressione deve essere L\-value \("valore a sinistra" o "valore Location"\).Nella maggior parte dei casi, un'espressione L\-value è un identificatore di Visual Basic valido utilizzato per indicare che l'oggetto `OutArgument` restituito è una variabile o un nome dell'argomento.  
  
 L'attributo `MaxLines` viene impostato su uno in questo esempio mentre `MinLines` non viene impostato.Pertanto, l'oggetto <xref:System.Activities.Presentation.View.ExpressionTextBox> è una dimensione fissa di una riga, indipendentemente dalla quantità di testo digitato dall'utente.Per consentire all'oggetto <xref:System.Activities.Presentation.View.ExpressionTextBox> di ingrandirsi per adattarsi all'input dell'utente, impostare per `MaxLines` un valore maggiore rispetto a `MinLines`.  
  
 Un oggetto ExpressionTextBox può essere associato solo agli argomenti e non alle proprietà CLR.  
  
#### Per utilizzare questo esempio  
  
1.  In [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] aprire il file della soluzione ExpressionTextBoxSample.sln.  
  
2.  Per compilare la soluzione, premere CTRL\+MAIUSC\+B.  
  
#### Per eseguire l'esempio  
  
1.  Aggiungere una nuova applicazione console flusso di lavoro alla soluzione.  
  
2.  Aggiungere un riferimento al progetto **ExpressionTextBoxSample** dal nuovo progetto applicazione console flusso di lavoro.  
  
3.  Compilare la soluzione.  
  
4.  Trascinare l'attività **MultiAssign** dalla casella degli strumenti e rilasciarla nel flusso di lavoro.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\CustomActivities\CustomActivityDesigners\ExpressionTextBox`  
  
## Vedere anche  
 <xref:System.Activities.Presentation.View.ExpressionTextBox>   
 [Sviluppo di applicazioni con Progettazione flussi di lavoro](../Topic/Developing%20Applications%20with%20the%20Workflow%20Designer.md)