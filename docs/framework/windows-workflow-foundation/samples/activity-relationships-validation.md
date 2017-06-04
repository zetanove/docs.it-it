---
title: "Convalida di relazioni tra attivit&#224; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6f11a34e-ed67-4bce-88ce-7e96bbb4d052
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Convalida di relazioni tra attivit&#224;
Il presente esempio è costituito da tre attività, `CreateCity`, `CreateState` e `CreateCountry`.`CreateCity` deve trovarsi all'interno di un'attività `CreateState` e `CreateState` deve trovarsi all'interno di un'attività `CreateCountry`.Ai fini di questo esempio, la logica di convalida è nel codice per l'attività `CreateState` e in XAML per l'attività `CreateCity`.Entrambi i vincoli presentano lo stesso comportamento.  
  
 [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)] fornisce le tre attività di supporto seguenti che consentono allo sviluppatore di convalidare relazioni tra attività.  
  
 <xref:System.Activities.Validation.GetParentChain>  
 Viene fornita la raccolta di tutte le attività che appartengono all'elemento padre del nodo corrente.  
  
 <xref:System.Activities.Validation.GetChildSubtree>  
 Viene fornita la raccolta di tutte le attività che appartengono al sottoalbero del nodo corrente, escluso il nodo corrente.  
  
 <xref:System.Activities.Validation.GetWorkflowTree>  
 Viene fornita la raccolta di tutte le attività nello stesso albero del nodo corrente.  
  
 Nell'esempio, un'attività <xref:System.Activities.Statements.ForEach%601> viene utilizzata per esaminare la raccolta restituita da <xref:System.Activities.Validation.GetParentChain>.Per ogni elemento nella raccolta, il relativo tipo viene confrontato con `CreateCountry` \(o `CreateState` se è in corso la convalida di `CreateCity`\) e, una volta trovata una corrispondenza, il flag del risultato viene impostato su `true`.Infine, viene utilizzato <xref:System.Activities.Validation.AssertValidation> per generare un errore di convalida se il flag del risultato viene impostato su `false`.  
  
### Per utilizzare questo esempio  
  
1.  Aprire la soluzione di esempio ContainmentValidation.sln in [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
2.  Compilare la soluzione.  
  
3.  Premere CTRL\+F5 per avviare il programma.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Validation\ActivityRelationships`  
  
## Vedere anche