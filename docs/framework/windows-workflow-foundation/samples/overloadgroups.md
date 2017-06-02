---
title: "OverloadGroups | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d1d547d2-f5fb-4de3-a959-ee6139a4f1ad
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# OverloadGroups
Questo esempio è costituito da un'attività \(`CreateLocation`\) che dispone di due caratteristiche interessanti:  
  
1.  Presenta alcuni argomenti obbligatori e alcuni facoltativi.  
  
2.  Consente all'utente di scegliere di fornire uno di due set diversi di argomenti.  
  
 Questi comportamenti sono portati a termine utilizzando queste due funzionalità:  
  
-   `[isRequired]` convalida l'assegnazione di un'attività specifica da parte di una proprietà e, in caso contrario, genera un'eccezione.  
  
-   `[OverloadGroup]` raggruppa un set di argomenti, in modo che l'utente dell'attività possa scegliere quale utilizzare.L'utente non può utilizzare argomenti da gruppi di overload diversi nella stessa istanza.  
  
 Dopo avere configurato flussi di lavoro diversi, chiamare il metodo <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A> che restituisce una raccolta <xref:System.Activities.Validation.ValidationResults> di oggetti <xref:System.Activities.Validation.ConstraintViolation>.Stampare gli oggetti <xref:System.Activities.Validation.ConstraintViolation> nella console.  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Aprire la soluzione di esempio **OverloadGroups.sln** in [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
2.  Compilare ed eseguire la soluzione.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Validation\OverloadGroups`  
  
## Vedere anche