---
title: "Estrarre dati di WF utilizzando il rilevamento | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e30c68f5-8c6a-495a-bd20-667a4364c68e
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# Estrarre dati di WF utilizzando il rilevamento
In questo esempio viene illustrato come utilizzare il rilevamento del flusso di lavoro per estrarre variabili e argomenti del flusso di lavoro dalle attività.Vengono inoltre illustrate l'aggiunta di annotazioni ai record di rilevamento e l'estrazione del payload di dati all'interno dei record di rilevamento personalizzati.Nell'esempio viene utilizzato il partecipante del rilevamento Traccia eventi per Windows \(ETW\) per estrarre i dati dal flusso di lavoro.  
  
## Dettagli dell'esempio  
 [!INCLUDE[wf](../../../../includes/wf-md.md)] fornisce il rilevamento per ottenere visibilità nell'esecuzione di un'istanza del flusso di lavoro.Il runtime di rilevamento crea record di rilevamento del flusso di lavoro durante l'esecuzione di quest'ultimo.Insieme ai record di rilevamento del flusso di lavoro, da quest'ultimo è possibile estrarre i dati presenti nell'istanza del flusso di lavoro.Nell'elenco seguente sono indicati in dettaglio i tipi di dati che possono essere estratti dai record di rilevamento:  
  
1.  Variabili del flusso di lavoro all'interno di un'attività e record di rilevamento durante l'esecuzione dell'attività.  
  
     Le variabili del flusso di lavoro da estrarre sono specificate in un profilo.Le variabili da estrarre possono essere specificate solo con `ActivityStateQueries`.Nell'esempio di codice seguente viene illustrato un profilo di rilevamento utilizzato per estrarre la variabile del flusso di lavoro da un'attività.  
  
    ```xml  
    <activityStateQuery activityName="StockPriceService">  
         <states>  
              <state name="Closed"/>  
         </states>  
         <variables>  
              <variable name="symbol"/>  
         </variables>  
    </activityStateQuery>  
    ```  
  
2.  Argomenti e record di rilevamento dello stato dell'attività.  
  
     Gli argomenti definiscono il modo in cui i dati entrano ed escono da un'attività.Gli argomenti da estrarre vengono specificati utilizzando un oggetto <xref:System.Activities.Tracking.ActivityStateQuery>. L'esempio di codice seguente è un profilo di rilevamento che estrae l'argomento `Value`.  
  
    ```xml  
    <activityStateQuery activityName="GetStockPrice">  
         <states>  
              <state name="Closed"/>  
         </states>  
         <arguments>  
              <argument name="Value"/>  
         </arguments>  
    </activityStateQuery>  
    ```  
  
3.  Le annotazioni sono coppie chiave\/valore che possono essere aggiunte a qualsiasi record di rilevamento creato.  
  
     Le annotazioni servono come meccanismo di tag per i record di rilevamento,vengono aggiunte ai record di rilevamento tramite un profilo di rilevamento epossono essere aggiunte a qualsiasi tipo di query di rilevamento di un flusso di lavoro.L'esempio di codice seguente è un profilo di rilevamento che mostra il modo in cui è possibile aggiungere un'annotazione a un record di rilevamento.  
  
    ```xml  
    <workflowInstanceQuery>  
         <states>  
              <state name="Started"/>  
         </states>  
         <annotations>  
              <annotation name="StockPriceWorkflow" value="Begin"/>  
         </annotations>  
    </workflowInstanceQuery>  
    ```  
  
4.  I record di rilevamento personalizzati vengono creati dalle attività definite dall'utente.  
  
     I record di rilevamento personalizzati possono contenere i dati di payload definiti all'interno di questa attività.La sottoscrizione di record di rilevamento personalizzati in un profilo di rilevamento consente l'estrazione del payload all'interno del record di rilevamento.I record di rilevamento personalizzati possono essere estratti con un oggetto <xref:System.Activities.Tracking.TrackingQuery> personalizzato.L'esempio di codice seguente è un profilo di rilevamento che estrae un record di rilevamento personalizzato insieme al payload.  
  
    ```  
    <customTrackingQuery name="QuoteLookupEvent" activityName="GetStockPrice"/>  
    ```  
  
 Nell'esempio vengono illustrate l'estrazione di variabili, argomenti, record personalizzati e l'aggiunta di annotazioni tramite un profilo specificato in un file Web.config.Il rilevamento è abilitato sul servizio flusso di lavoro di esempio aggiungendo un elemento del comportamento `<etwTracking>`.Nell'esempio di codice seguente viene abilitato il rilevamento per il profilo di rilevamento `ExtractWorkflowVariables`.  
  
```  
<serviceBehaviors>  
     <behavior>  
               <etwTracking profileName="ExtractWorkflowVariables"/>  
     </behavior>  
</serviceBehaviors>  
```  
  
#### Per utilizzare questo esempio  
  
1.  In [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] aprire il file della soluzione WFStockPriceApplication.sln.  
  
2.  Per compilare la soluzione, premere CTRL\+MAIUSC\+B.  
  
3.  Per eseguire la soluzione, premere F5.  
  
     Verrà aperta la finestra del browser in cui viene mostrata la visualizzazione directory per l'applicazione.  
  
4.  Nel browser fare clic su StockPriceService.xamlx.  
  
5.  Nel browser viene visualizzata la pagina StockPriceService contenente l'indirizzo WSDL del servizio locale.Copiare questo indirizzo.  
  
     Nell'esempio seguente viene mostrato un indirizzo WSDL del servizio locale.`http://localhost:53797/StockPriceService.xamlx?wsdl`  
  
6.  Prima di richiamare il servizio, avviare Visualizzatore eventi e assicurarsi che il registro eventi sia in ascolto per rilevare eventi creati dal servizio del flusso di lavoro.  
  
7.  Nel menu **Start** selezionare **Strumenti di amministrazione**, quindi **Visualizzatore eventi**.  
  
8.  Nella visualizzazione struttura ad albero del Visualizzatore eventi passare a **Visualizzatore eventi**, **Registri applicazioni e servizi**, quindi a **Microsoft**.Fare clic con il pulsante destro del mouse su **Microsoft**, selezionare **Visualizza**, quindi **Visualizza registri analitici e di debug**.  
  
     Assicurarsi che l'opzione **Visualizza registri analitici e di debug** sia selezionata.  
  
9. Nella visualizzazione struttura ad albero in Visualizzatore eventi passare a **Visualizzatore eventi**, **Registri applicazioni e servizi**, **Microsoft**, **Windows**, **Server applicazioni\-Applicazioni**.Fare clic con il pulsante destro del mouse su **Analitico** e scegliere **Attiva registro**.  
  
10. Se si utilizza [!INCLUDE[fileExplorer](../../../../includes/fileexplorer-md.md)], aprire il client di prova WCF.  
  
     Il client di prova WCF \(WcfTestClient.exe\) si trova nella cartella \<cartella di installazione di [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)]\>\\Common7\\IDE\\.  
  
     La cartella di installazione di [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] predefinita è C:\\Programmi\\Microsoft Visual Studio 10.0.  
  
11. Nel client di prova WCF selezionare **Aggiungi servizio** dal menu **File**.  
  
     Aggiungere l'indirizzo WSDL del servizio locale che è stato copiato precedentemente nella casella di input.  
  
12. Nel client di prova WCF fare doppio clic su `GetStockPrice`.  
  
     Verrà visualizzato il metodo `GetStockPrice`.La richiesta accetta un parametro.Utilizzare il valore **Contoso**.  
  
13. Fare clic su **Richiama**.  
  
14. Tornare a Visualizzatore eventi e passare a **Visualizzatore eventi**, **Registri applicazioni e servizi**, **Microsoft**, **Windows**, **Server applicazioni\-Applicazioni**.Fare clic con il pulsante destro del mouse su **Analitico** e selezionare **Aggiorna**.Gli ID degli eventi flusso di lavoro sono compresi tra 100 e 199.  
  
     Gli eventi contengono annotazioni, variabili, argomenti e record di rilevamento personalizzati che possono essere visualizzati nel visualizzatore eventi.  
  
## Pulizia nel Visualizzatore eventi  
 Il canale analitico nel registro eventi può essere pulito nel Visualizzatore eventi eseguendo le operazioni seguenti.  
  
#### Per eseguire la pulizia \(facoltativo\)  
  
1.  Aprire Visualizzatore eventi.  
  
2.  Passare a **Visualizzatore eventi**, **Registri applicazioni e servizi**, **Microsoft**, **Windows**, **Server applicazioni\-Applicazioni**.Fare clic con il pulsante destro del mouse su **Analitico** e selezionare **Disattiva registro**.  
  
3.  Passare a **Visualizzatore eventi**, **Registri applicazioni e servizi**, **Microsoft**, **Windows**, **Server applicazioni\-Applicazioni**.Fare clic con il pulsante destro del mouse su **Analitico** e selezionare **Cancella log**.  
  
     Scegliere l'opzione **Cancella** per cancellare gli eventi.  
  
## Problema noto  
  
> [!NOTE]
>  Nel Visualizzatore eventi potrebbe non essere possibile decodificare gli eventi ETW.Si potrebbe visualizzare un messaggio di errore simile al seguente.  
>   
>  `Impossibile trovare la descrizione per l'ID evento <id> dall'origine Microsoft-Windows-Server applicazioni-Applicazioni.Il componente che ha generato l'evento non è installato nel computer locale oppure l'installazione è danneggiata.È possibile installare o ripristinare il componente nel computer locale.`  
>   
>  Se si rileva questo errore, fare clic su **Aggiorna** nel riquadro Azioni.La decodifica dell'evento dovrebbe ora essere eseguita in modo corretto.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Tracking\ExtractWfData`  
  
## Vedere anche  
 [Monitoraggio](http://go.microsoft.com/fwlink/?LinkId=193959)