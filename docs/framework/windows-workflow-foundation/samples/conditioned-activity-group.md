---
title: "ConditionedActivityGroup | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f76ef924-34ce-48ae-8c8d-48faf9697754
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# ConditionedActivityGroup
Nell'esempio viene illustrata un'applicazione di prenotazione di viaggio.<xref:System.Workflow.Activities.ConditionedActivityGroup> \(CAG\) ha due attività di codice: un'attività Car e una attività Airline.Nel costruttore `SimpleCAGWorkflow`, un oggetto ArrayList "travelNeedType" viene popolato con i tipi di prenotazioni di viaggio richiesti.Tramite l'aggiunta di commenti a una o entrambe le istruzioni `travelNeeds.Add`, il comportamento di CAG viene modificato di conseguenza.Entrambi le attività Car e Airline dispongono della condizione <xref:System.Workflow.Activities.ConditionedActivityGroup.WhenConditionProperty> popolata con una <xref:System.Workflow.Activities.CodeCondition>.L'attività Car viene eseguita solo se la raccolta `travelNeeds` dispone di una voce `TravelNeeds.Car` e l'attività Airline viene eseguita solo se la raccolta `travelNeeds` dispone di una voce `TravelNeeds.Airline`.  
  
 L'esecuzione di ciascuna attività rimuove la voce corrispondente dalla raccolta.La condizione <xref:System.Workflow.Activities.ConditionedActivityGroup.UntilCondition%2A> predefinita specifica che CAG debba essere chiuso se non sono presenti esecuzione da parte dei figli o se i figli sono pronti per l'esecuzione \(in base alle condizioni <xref:System.Workflow.Activities.ConditionedActivityGroup.WhenConditionProperty>\).In questo esempio, ciò vuole dire che CAG viene chiuso quando la raccolta `travelNeeds` è vuota.  
  
### Per compilare l'esempio  
  
1.  Aprire la soluzione in [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
2.  Premere CTRL\+MAIUSC\+B per compilare la soluzione,  
  
3.  Eseguire la soluzione senza debug premendo CTRL\+F5.  
  
### Per eseguire l’esempio  
  
-   Nella finestra del prompt dei comandi di SDK eseguire il file con estensione exe nella cartella SimpleCAG\\bin\\debug \(oppure nella cartella SimpleCAG\\bin per la versione Visual Basic dell'esempio\), collocata sotto la cartella principale dell'esempio.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Rules\SimpleCAG`  
  
## Vedere anche  
 <xref:System.Workflow.Activities.ConditionedActivityGroup>   
 <xref:System.Workflow.Activities.ConditionedActivityGroup.WhenConditionProperty>   
 <xref:System.Workflow.Activities.CodeCondition>   
 <xref:System.Workflow.Activities.ConditionedActivityGroup.UntilCondition%2A>