---
title: "Rilevamento SQL | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: bcaebeb1-b9e5-49e8-881b-e49af66fd341
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# Rilevamento SQL
In questo esempio viene illustrato come scrivere un partecipante del rilevamento SQL personalizzato che scrive record di rilevamento in un database SQL.[!INCLUDE[wf](../../../../includes/wf-md.md)] fornisce il rilevamento del flusso di lavoro per ottenere visibilità nell'esecuzione di un'istanza del flusso di lavoro.Il runtime di rilevamento crea record di rilevamento del flusso di lavoro durante l'esecuzione di quest'ultimo.[!INCLUDE[crabout](../../../../includes/crabout-md.md)]l rilevamento del flusso di lavoro, vedere [Rilevamento e traccia del flusso di lavoro](../../../../docs/framework/windows-workflow-foundation//workflow-tracking-and-tracing.md).  
  
#### Per utilizzare questo esempio  
  
1.  Verificare di avere installato SQL Server 2008, SQL Server 2008 Express o una versione più recente.Gli script impacchettati con l'esempio presuppongono l'utilizzo di un'istanza di SQL Express sul computer locale.Se si dispone di un'istanza diversa, modificare gli script correlati al database prima di eseguire l'esempio.  
  
2.  Creare il database di rilevamento di SQL Server eseguendo Trackingsetup.cmd nella directory degli script \(\\WF\\Basic\\Tracking\\SqlTracking\\CS\\Scripts\).Verrà creato un database denominato TrackingSample.  
  
    > [!NOTE]
    >  Lo script crea il database nell'istanza predefinita di SQL Express.Se si desidera installarlo in un'istanza di database diversa, modificare lo script Trackingsetup.cmd.  
  
3.  Aprire SqlTrackingSample.sln in [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
4.  Per compilare la soluzione, premere CTRL\+MAIUSC\+B.  
  
5.  Premere F5 per eseguire l'applicazione.  
  
     Verrà aperta la finestra del browser in cui viene mostrata la visualizzazione directory per l'applicazione.  
  
6.  Nel browser fare clic su StockPriceService.xamlx.  
  
7.  Nel browser viene visualizzata la pagina StockPriceService contenente l'indirizzo WSDL del servizio locale.Copiare questo indirizzo.  
  
     Un esempio di indirizzo WSDL del servizio locale è http:\/\/localhost:65193\/StockPriceService.xamlx?wsdl.  
  
8.  Se si utilizza [!INCLUDE[fileExplorer](../../../../includes/fileexplorer-md.md)], eseguire il client di prova WCF \(WcfTestClient.exe\).che si trova nella directory Microsoft Visual Studio 10.0\\Common7\\IDE.  
  
9. Nel client di prova WCF fare clic sul menu **File** e selezionare **Aggiungi servizio**.Incollare l'indirizzo del servizio locale nella casella di testo.Scegliere **OK** per chiudere la finestra di dialogo.  
  
10. Nel client di prova WCF fare doppio clic su **GetStockPrice**.Verrà visualizzata l'operazione `GetStockPrice` che accetta un parametro, digitare il valore `Contoso` e fare clic su **Richiama**.  
  
11. I record di rilevamento creati vengono scritti in un database SQL.Per visualizzare i record di rilevamento, aprire il database TrackingSample in SQL Management Studio e passare alle tabelle.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] SQL Server Management Studio, vedere [Introduzione a SQL Server Management Studio](http://go.microsoft.com/fwlink/?LinkId=165645).SQL Server 2008 Management Studio Express può essere scaricato [qui](http://go.microsoft.com/fwlink/?LinkId=180520).Eseguendo una query di selezione sulle tabelle vengono visualizzati i dati all'interno dei record di rilevamento archiviati nelle rispettive tabelle.  
  
#### Per disinstallare l'esempio  
  
1.  Eseguire lo script Trackingcleanup.cmd nella directory di esempio \(\\WF\\Basic\\Tracking\\SqlTracking\).  
  
    > [!NOTE]
    >  Trackingcleanup.cmd tenta di eliminare il database nel computer locale SQL Express.Se si utilizza un'altra istanza di SQL Server, modificare Trackingcleanup.cmd.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Tracking\SqlTracking`  
  
## Vedere anche  
 [Monitoraggio](http://go.microsoft.com/fwlink/?LinkId=193959)