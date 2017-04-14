---
title: "Traccia analitica WCF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6029c7c7-3515-4d36-9d43-13e8f4971790
caps.latest.revision: 21
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 21
---
# Traccia analitica WCF
In questo esempio viene descritto come aggiungere eventi di traccia nel flusso di tracce analitiche scritte da [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] in ETW in [!INCLUDE[netfx_current_long](../../../../includes/netfx-current-long-md.md)].Le tracce analitiche hanno lo scopo di semplificare la visibilità all'interno dei servizi senza un'elevata riduzione delle prestazioni.Questo esempio mostra come utilizzare le API <xref:System.Diagnostics.Eventing?displayProperty=fullName> per scrivere eventi che si integrano con i servizi di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] API <xref:System.Diagnostics.Eventing?displayProperty=fullName>, vedere <xref:System.Diagnostics.Eventing?displayProperty=fullName>.  
  
 Per ulteriori informazioni relative alla traccia di eventi in Windows, vedere [Miglioramento del debug e ottimizzazione delle prestazioni con ETW](http://go.microsoft.com/fwlink/?LinkId=166488).  
  
## Eliminazione di EventProvider  
 In questo esempio viene utilizzata la classe <xref:System.Diagnostics.Eventing.EventProvider?displayProperty=fullName>, che implementa <xref:System.IDisposable?displayProperty=fullName>.Quando si implementa la traccia per un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], è possibile utilizzare le risorse di <xref:System.Diagnostics.Eventing.EventProvider> per la durata del servizio.Per tale motivo e per ragioni di leggibilità, in questo esempio l'oggetto <xref:System.Diagnostics.Eventing.EventProvider> con wrapper non viene mai eliminato.Se per qualche motivo il servizio dispone di requisiti diversi per la traccia ed è necessario eliminare tale risorsa, occorre modificare l'esempio in base alle procedure consigliate per l'eliminazione di risorse non gestite.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] eliminazione di risorse non gestite, vedere la pagina relativa all'[implementazione di un metodo Dispose](http://go.microsoft.com/fwlink/?LinkId=166436).  
  
## Differenze tra self\-hosting ehosting Web  
 Per i servizi ospitati sul Web, le tracce analitiche di WCF forniscono un campo, denominato "HostReference", utilizzato per identificare il servizio che sta generando le tracce.Le tracce utente estensibili possono far parte di tale modello e in questo esempio vengono descritte le procedure consigliate per effettuare tale operazione.Il formato di un riferimento dell'host Web quando il carattere barra verticale \(" &#124; "\) viene visualizzato nella stringa risultante può essere uno dei seguenti:  
  
-   Se l'applicazione non è alla radice.  
  
     \<NomeSito\>\<PercorsoVirtualeApplicazione\>&#124;\<PercorsoVirtualeServizio\>&#124;\<NomeServizio\>  
  
-   Se l'applicazione è alla radice.  
  
     \<NomeSito\>&#124;\<PercorsoVirtualeServizio\>&#124;\<NomeServizio\>  
  
 Per i servizi indipendenti, le tracce analitiche di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non popolano il campo "HostReference".La classe `WCFUserEventProvider` in questo esempio si comporta coerentemente quando viene utilizzata da un servizio indipendente.  
  
## Informazioni dettagliate su eventi personalizzati  
 Il manifesto del provider di eventi ETW di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] definisce tre eventi progettati per essere generati dagli autori del servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] dall'interno del codice del servizio.Nella tabella riportata di seguito viene illustrata una suddivisione dei tre eventi.  
  
|Evento|Descrizione|ID evento|  
|------------|-----------------|---------------|  
|UserDefinedInformationEventOccurred|Generare questo evento quando nel servizio si verifica un evento degno di nota che non è tuttavia un problema.Ad esempio, è possibile generare un evento dopo avere effettuato correttamente una chiamata a un database.|301|  
|UserDefinedWarningOccurred|Generare questo evento quando si verifica un problema che potrebbe comportare un errore in futuro.Ad esempio, è possibile generare un evento di avviso quando una chiamata a un database non riesce ma è comunque possibile recuperarla eseguendo il fallback a un archivio dati ridondante.|302|  
|UserDefinedErrorOccurred|Generare questo evento quando il comportamento del servizio non è quello previsto.Ad esempio, è possibile generare un evento se una chiamata a un database non riesce e non è possibile recuperare i dati altrove.|303|  
  
#### Per utilizzare questo esempio  
  
1.  Utilizzando [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)], aprire il file della soluzione WCFAnalyticTracingExtensibility.sln.  
  
2.  Per compilare la soluzione, premere CTRL\+MAIUSC\+B.  
  
3.  Per eseguire la soluzione, premere CTRL\+F5.  
  
     Nel browser Web fare clic su **Calculator.svc**.L'URI del documento WSDL per il servizio viene visualizzato nel browser.Copiare l'URI.  
  
4.  Eseguire il client di prova [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] \(WcfTestClient.exe\).  
  
     Il client di prova [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] \(WcfTestClient.exe\) si trova nella \<directory di installazione di [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)]\>\\Common7\\IDE\\ WcfTestClient.exe \(la directory di installazione predefinita di [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] è C:\\Programmi\\Microsoft Visual Studio 10.0\).  
  
5.  All'interno del client di prova [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], aggiungere il servizio selezionando **File**, quindi **Aggiungi servizio**.  
  
     Aggiungere l'indirizzo dell'endpoint nella casella di input.  
  
6.  Scegliere **OK** per chiudere la finestra di dialogo.  
  
     Il servizio ICalculator viene aggiunto nel riquadro sinistro in **Progetti di servizi**.  
  
7.  Aprire l'applicazione Visualizzatore eventi.  
  
     Prima di richiamare il servizio, avviare Visualizzatore eventi e assicurarsi che il registro eventi sia in ascolto per rilevare eventi generati dal servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
8.  Dal menu **Start** scegliere **Strumenti di amministrazione**, quindi **Visualizzatore eventi**.Abilitare i registri **Analitico** e **Debug**.  
  
9. Nella visualizzazione struttura ad albero di Visualizzatore eventi passare a **Visualizzatore eventi**, **Registri applicazioni e servizi**, **Microsoft**, **Windows**, quindi **Server applicazioni\-Applicazioni**.Fare clic con il pulsante destro del mouse su **Server applicazioni\-Applicazioni**, scegliere **Visualizza**, quindi **Visualizza registri analitici e di debug**.  
  
     Assicurarsi che l'opzione **Visualizza registri analitici e di debug** sia selezionata.Abilitare il registro **Analitico**.  
  
     Nella visualizzazione struttura ad albero di Visualizzatore eventi, passare a **Visualizzatore eventi**, **Registri applicazioni e servizi**, **Microsoft**, **Windows**, **Server applicazioni\-Applicazioni**, quindi **Analitico**.Fare clic con il pulsante destro del mouse su **Analitico** e selezionare **Attiva registro**.  
  
10. Testare il servizio utilizzando il client di prova WCF.  
  
    1.  Nel client di prova WCF fare doppio clic su **Add\(\)** nel nodo del servizio ICalculator.  
  
         Il metodo **Add\(\)** viene visualizzato nel riquadro di destra con due parametri.  
  
    2.  Digitare 2 per il primo parametro e 3 per il secondo parametro.  
  
    3.  Fare clic su **Richiama** per richiamare il metodo.  
  
11. Andare alla finestra **Visualizzatore eventi** precedentemente aperta.Passare a **Visualizzatore eventi**, **Registri applicazioni e servizi**, **Microsoft**, **Windows**, **Server applicazioni\-Applicazioni**.  
  
12. Fare clic con il pulsante destro del mouse su **Analitico** e scegliere **Aggiorna**.  
  
     Gli eventi vengono visualizzati nel riquadro destro.  
  
13. Individuare l'evento con l'ID 303 e fare doppio clic per aprirlo e verificarne il contenuto.  
  
     Questo evento viene generato dal metodo `Add()` del servizio ICalculator e ha un payload uguale a "2\+3\=5".  
  
#### Per eseguire la pulizia \(facoltativo\)  
  
1.  Aprire **Visualizzatore eventi**.  
  
2.  Passare a **Visualizzatore eventi**, **Registri applicazioni e servizi**, **Microsoft**, **Windows**, quindi **Server applicazioni\-Applicazioni**.Fare clic con il pulsante destro del mouse su **Analitico** e scegliere **Disattiva registro**.  
  
3.  Passare a **Visualizzatore eventi**, **Registri applicazioni e servizi**, **Microsoft**, **Windows**, **Server applicazioni\-Applicazioni**, quindi **Analitico**.Fare clic con il pulsante destro del mouse su **Analitico** e selezionare **Cancella registro**.  
  
4.  Fare clic su **Cancella** per cancellare gli eventi.  
  
## Problema noto  
 Si verifica un problema noto nel **Visualizzatore eventi** per cui quest'ultimo non riesce a decodificare eventi ETW.È possibile visualizzare un messaggio di errore con il testo seguente: "Impossibile trovare la descrizione per l'ID evento \<id\> dall'origine Microsoft\-Windows\-Server applicazioni\-Applicazioni.Il componente che ha generato l'evento non è installato nel computer locale oppure l'installazione è danneggiata.È possibile installare o ripristinare il componente nel computer locale". Se si rileva questo errore, selezionare **Aggiorna** nel menu **Azioni**.L'evento dovrebbe procedere alla decodifica in modo corretto.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Management\ETWTrace`  
  
## Vedere anche  
 [Monitoraggio](http://go.microsoft.com/fwlink/?LinkId=193959)