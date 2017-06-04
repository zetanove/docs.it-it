---
title: "Attivit&#224; NoPersistScope | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9a0baeb7-a05c-4fac-b905-252758cb71bb
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# Attivit&#224; NoPersistScope
In questo esempio viene illustrato come modificare uno stato Non\-serializable e Disposable all'interno di un flusso di lavoro.È importante che i flussi di lavoro non tentino di rendere persistente lo stato Non\-serializable e che venga eseguita la pulizia degli oggetti eliminabili dopo essere stati utilizzati nel flusso di lavoro.  
  
## Dimostrazione  
 Attività personalizzata `NoPersistScope` e finestra di progettazione.  
  
## Utilizzo dell'attività NoPersistZone  
 Quando viene eseguito il flusso di lavoro di esempio, un'attività personalizzata denominata `CreateTextWriter` crea un oggetto di tipo <xref:System.IO.TextWriter> e lo salva in un variabile del flusso di lavoro.<xref:System.IO.TextWriter> è un oggetto <xref:System.IDisposable>.Questo oggetto <xref:System.IO.TextWriter>, configurato per scrivere in un file denominato 'out.txt' nella directory in cui viene eseguito l'esempio, viene utilizzato da un'attività <xref:System.Activities.Statements.WriteLine> poiché restituisce qualsiasi testo digitato nella console.  
  
 La logica echo viene eseguita all'interno di un'attività `NoPersistScope` \(il cui codice fa anche parte di questo esempio\) che evita la persistenza del flusso di lavoro.Se si digita `unload` nella console, l'host tenta di rendere persistente l'istanza del flusso di lavoro, tuttavia questa operazione scade poiché il flusso di lavoro rimane all'interno di un oggetto `NoPersistScope`.Il flusso di lavoro utilizza anche un'attività personalizzata denominata `Dispose` per eliminare l'oggetto <xref:System.IO.TextWriter> quando il flusso di lavoro viene completato utilizzandolo.L'attività `Dispose` viene posizionata all'interno del blocco <xref:System.Activities.Statements.TryCatch.Finally%2A> dell'attività <xref:System.Activities.Statements.TryCatch> in cui viene dichiarata la variabile <xref:System.IO.TextWriter>, per assicurarsi che venga eseguita anche se si dovesse verificare un'eccezione durante l'esecuzione del blocco Try.  
  
 È possibile digitare `exit` per completare l'istanza del flusso di lavoro e uscire dal programma.  
  
#### Per eseguire l'esempio  
  
1.  Aprire la soluzione NoPersistZone.sln in [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
2.  Per compilare la soluzione, premere CTRL\+MAIUSC\+B o scegliere **Compila soluzione** dal menu **Compila**.  
  
3.  Una volta eseguita correttamente la compilazione, premere F5 o selezionare **Avvia debug** dal menu **Debug** oppure, in alternativa, premere CTRL\+F5 o selezionare **Avvia senza eseguire debug** dal menu **Debug** per consentire l'esecuzione senza debug.  
  
#### Per eseguire la pulizia \(facoltativo\)  
  
1.  Per rimuovere l'archivio di istanze SQL, eseguire Cleanup.cmd.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Scenario\ActivityLibrary\NoPersistScope`  
  
## Vedere anche