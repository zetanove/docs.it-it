---
title: "Determinazione della durata di esecuzione del flusso di lavoro tramite traccia | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f04ad0fd-edc7-4cbc-8979-356f2a1131c4
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Determinazione della durata di esecuzione del flusso di lavoro tramite traccia
In questo argomento viene illustrato come determinare il tempo necessario per l'esecuzione corretta di un flusso di lavoro indipendente tramite la traccia del flusso di lavoro.  
  
### Per determinare la durata di esecuzione di un'applicazione flusso di lavoro tramite la traccia del flusso di lavoro  
  
1.  Aprire [!INCLUDE[vs2010](../../../includes/vs2010-md.md)].Scegliere **Nuovo** dal menu **File**, quindi **Progetto**.In **C\#** selezionare il nodo **Flusso di lavoro**.Selezionare **Applicazione console flusso di lavoro** nell'elenco di modelli.Assegnare il nome `WorkflowDurationTracing` al nuovo progetto, quindi fare clic su **OK**.  
  
2.  Aprire Workflow1.xaml.Trascinare un'attività <xref:System.Activities.Statements.Delay> nell'area di progettazione.Assegnare il valore 00.00.10 \(dieci secondi\) alla proprietà Duration dell'attività.  
  
3.  Aprire il Visualizzatore eventi facendo clic sul pulsante **Start**, quindi scegliendo **Esegui** e immettendo `eventvwr.exe`.  
  
4.  Se la traccia del flusso di lavoro non è stata abilitata, espandere **Registri applicazioni e servizi**, **Microsoft**, **Windows**, **Server applicazioni\-Applicazioni**.Selezionare **Visualizza**, **Visualizza registri analitici e di debug**.Fare clic con il pulsante destro del mouse su **Debug** e selezionare **Attiva log**.Lasciare aperto il Visualizzatore eventi in modo che sia possibile visualizzare le tracce dopo l'esecuzione del flusso di lavoro.  
  
5.  Premere CTRL\+SHIFT\+B per eseguire l'applicazione flusso di lavoro.  
  
6.  Nel Visualizzatore eventi trovare un recente evento con ID 1009 e un messaggio analogo al seguente.Annotare l'ora in cui il messaggio è stato registrato.  
  
 **Attività padre '', NomeVisualizzato: '', IDIstanza: '' Attività figlio pianificata 'RilevamentoDurataFlussodilavoro.Flussodilavoro1', NomeVisualizzato: 'Flussodilavoro1', IDIstanza: '1'.**  
  
7.  Trovare un altro evento recente con ID 1001 e un messaggio analogo al seguente.Sottrarre l'ora del messaggio precedente dal valore registrato per questo messaggio per determinare la durata di esecuzione del flusso di lavoro che deve essere di circa 10 secondi.  
  
 **ID IstanzaFlussodilavoro: '1bbac57b\-3322\-498e\-9e27\-8833fda3a5bf' completata con stato Chiuso.**  
  
## Vedere anche  
 [Traccia del flusso di lavoro](../../../docs/framework/windows-workflow-foundation//workflow-tracing.md)   
 [Concetti di monitoraggio](http://go.microsoft.com/fwlink/?LinkId=201273)   
 [Monitoraggio delle applicazioni](http://go.microsoft.com/fwlink/?LinkId=201275)