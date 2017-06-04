---
title: "Formattazione di messaggi nei servizi flusso di lavoro | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6d15d44b-20f8-4cb7-bd4f-598c32781ebc
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Formattazione di messaggi nei servizi flusso di lavoro
In questo esempio viene illustrato come tipi utente diversi possono essere utilizzati nelle attività di messaggistica \(servizi WF\).Il servizio di esempio è un semplice servizio di approvazione spese ed espone tre operazioni.`ApproveExpense` accetta un tipo di contratto dati e mostra come utilizzare i tipi noti.L'operazione restituisce `true` o `false` in base all'ammontare della spesa.`ApprovePO` accetta un tipo XmlSerializer e restituisce `true` o `false` in base all'ammontare della spesa.`ApprovedVendor` accetta un tipo di contratto di messaggio e restituisce `true` o `false` se il fornitore è presente nell'elenco dei fornitori approvati o se la richiesta viene dal reparto finanziario \(il reparto finanziario può utilizzare qualsiasi fornitore\).  
  
#### Per utilizzare questo esempio  
  
1.  Caricare la soluzione del progetto in [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] e compilare il progetto.  
  
2.  Eseguire innanzitutto il servizio, generato in \[directory soluzione di base\]FormatterService\\bin\\debug\\.  
  
3.  Eseguire quindi l'applicazione Client, generata in \[directory soluzione di base\]\\FormatterClient\\bin\\debug.  
  
4.  Il client chiama tre operazioni nel servizio e stampa i risultati.Al termine premere INVIO per uscire dal client e quindi dal servizio.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Services\Formatter`  
  
## Vedere anche