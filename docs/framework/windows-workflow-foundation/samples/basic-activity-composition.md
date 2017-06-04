---
title: "Composizione dell&#39;attivit&#224; di base | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c283a1a7-1245-4ecd-8072-206c1b4ca379
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Composizione dell&#39;attivit&#224; di base
In questo esempio viene illustrato come creare attività personalizzate e attività fornite dal sistema per compilare attività più personalizzate.  
  
 Il flusso di lavoro che utilizza attività Survey pianifica tale attività con un elenco di domande, quindi restituisce le risposte ricevute.  
  
## Dettagli dell'esempio  
 In questo esempio sono utilizzate tre attività personalizzate.`ReadLine` è una semplice \<stringa\> di <xref:System.Activities.NativeActivity> che crea un oggetto <xref:System.Activities.Bookmark> quando pianificato, successivamente imposta `Return`<xref:System.Activities.OutArgument%601> sul valore con cui viene ripreso <xref:System.Activities.Bookmark>.`Prompt` è una \<stringa\> di <xref:System.Activities.Activity%601>\<string\> che accetta una \<stringa\> di <xref:System.Activities.InArgument%601> denominato `Text` e restituisce la risposta degli utenti nella \<stringa\> di `Result`<xref:System.Activities.OutArgument%601>.L'attività `Prompt` utilizza le attività <xref:System.Activities.Statements.Sequence> e <xref:System.Activities.Statements.WriteLine> che vengono fornite come parte di .NET Framework e inoltre incorpora l'attività `ReadLine` personalizzata per l'acquisizione di input dell'utente.`Survey` è l'ultima attività personalizzata.È un oggetto <xref:System.Activities.Activity>\<ICollection\<string\>\>.Questa attività accetta un oggetto <xref:System.Activities.InArgument%601>\<IEnumerable\<string\>\> denominato `Questions` e popola l'argomento out `Result` con le risposte.L'attività `Survey` utilizza gli oggetti <xref:System.Activities.Statements.ForEach>, <xref:System.Activities.Statements.Sequence> e <xref:System.Activities.Statements.AddToCollection%601> da .NET Framework e l'attività `Prompt` per porre le domande del sondaggio e ottenere le risposte.  
  
#### Per impostare, compilare ed eseguire l'esempio  
  
1.  Aprire la soluzione di esempio **BasicActivityComposition.sln** in [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
2.  Compilare ed eseguire la soluzione.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\CustomActivities\Composite\ActivityComposition`  
  
## Vedere anche