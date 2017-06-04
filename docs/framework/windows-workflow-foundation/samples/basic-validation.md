---
title: "Convalida di base | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ba1343cc-aaab-4ade-b0c0-1dd5063bf4ad
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Convalida di base
Questo esempio è costituito da un'attività `CreateProduct` che verifica che l'argomento `Cost` sia minore o uguale al relativo argomento `Price`.  
  
## Dettagli dell'esempio  
 Esistono due autori che utilizzano la convalida, l'autore di attività \(crea la logica di convalida per l'attività\) e l'autore del flusso di lavoro che chiama i servizi di convalida in un flusso di lavoro specifico.In questo scenario, l'autore di attività desidera che ogni istanza dell'attività abbia un costo minore o uguale a un determinato prezzo.  
  
 L'autore di attività \(nell'attività\) deve:  
  
-   Creare un vincolo \(`PriceGreaterThanCost`\),ovvero il punto in cui far risiedere l'intera logica di convalida.  
  
-   Eseguire l'override del metodo <xref:System.Activities.CodeActivity%601.OnGetConstraints%2A> e aggiungere il vincolo \(`PriceGreaterThanCost`\) ai vincoli <xref:System.Collections.IList>.  
  
 L'autore del flusso di lavoro \(programma principale\) deve:  
  
-   Creare un flusso di lavoro con un'istanza dell'attività da convalidare \(`CreateProduct`\).  
  
-   Chiamare il metodo <xref:System.Activities.Validation.ActivityValidationServices.Validate%2A>, che restituisce una raccolta <xref:System.Activities.Validation.ValidationResults> di oggetti <xref:System.Activities.Validation.ConstraintViolation>.  
  
-   \(Facoltativo\) Stampare gli oggetti <xref:System.Activities.Validation.ConstraintViolation>.  
  
#### Per impostare, compilare ed eseguire l'esempio  
  
1.  Aprire la soluzione di esempio BasicValidation.sln in [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
2.  Compilare ed eseguire la soluzione.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Validation\BasicValidation`  
  
## Vedere anche