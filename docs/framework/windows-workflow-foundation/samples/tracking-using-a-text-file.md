---
title: "Rilevamento tramite un file di testo | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 56a82682-73c2-4b91-a206-4d8bb12c561b
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# Rilevamento tramite un file di testo
In questo esempio viene illustrato come estendere il rilevamento in [!INCLUDE[wf](../../../../includes/wf-md.md)] creando un partecipante di rilevamento personalizzato.I partecipanti di rilevamento sono classi .NET Framework che ricevono record di rilevamento dal runtime man mano che vengono generati.È possibile creare un partecipante di rilevamento per trasportare gli eventi di rilevamento a qualunque destinazione necessaria per lo specifico scenario.Ad esempio, il partecipante di rilevamento Analisi eventi per Windows \(ETW\) viene fornito come parte di [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)].Il partecipante di rilevamento in questo esempio scrive i record in formato XML in un file di testo.  
  
## Dettagli dell'esempio  
 Per ottimizzare l'utilità e l'affidabilità del partecipante di rilevamento, è necessario completare alcuni passaggi aggiuntivi per collegare correttamente il partecipante di rilevamento al runtime.Nella tabella seguente vengono descritte le classi utilizzate in questo esempio per creare un partecipante di rilevamento conforme alle procedure consigliate.  
  
|Classe|Descrizione|  
|------------|-----------------|  
|`TextFileTrackingExtensionElement`|<xref:System.ServiceModel.Configuration.BehaviorExtensionElement> consente di definire la sezione di configurazione utilizzata per configurare il partecipante di rilevamento del file di testo.Gli utenti possono specificare la destinazione del file di log utilizzando file di configurazione standard di .NET Framework.|  
|`TextFileTrackingBehavior`|I comportamenti disponibili in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] consentono agli utenti di inserire estensioni nel runtime.Tramite questo comportamento il partecipante di rilevamento viene aggiunto al servizio all'avvio di quest'ultimo.|  
|`TextFileTrackingParticipant`|Il partecipante di rilevamento riceve i partecipanti di rilevamento in fase di esecuzione e li archivia in un file di log come XML.|  
  
## Configurazione degli elementi estensione di comportamento  
 Per poter utilizzare l'elemento estensione di comportamento descritto in precedenza utilizzando file di configurazione di .NET Framework, è necessario un ulteriore passaggio.La configurazione seguente deve essere inserita nei file di configurazione in cui verrà utilizzata l'estensione.  
  
```  
<system.serviceModel>  
    <extensions>  
      <behaviorExtensions>  
        <add name="textFileTracking" type="Microsoft.Samples.TextFileTracking.TextFileTrackingExtensionElement, WFStockPriceApplication, Version=1.0.0.0, Culture=neutral, PublicKeyToken=null" />  
      </behaviorExtensions>  
    </extensions>  
…  
  </system.serviceModel>  
  
```  
  
> [!NOTE]
>  Vedere il file Web.config incluso nell'esempio per un completo esempio di utilizzo della configurazione di elementi estensione di comportamento.  
  
## Record di rilevamento personalizzati  
 Il file GetStockPrices.cs illustra come creare record di rilevamento personalizzati dall'interno di <xref:System.Activities.CodeActivity>.Quando si esegue l'esempio, cercare questo record.  
  
#### Per utilizzare questo esempio  
  
1.  In [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] aprire il file della soluzione WFStockPriceApplication.sln.  
  
2.  Per compilare la soluzione, premere CTRL\+MAIUSC\+B.  
  
3.  Per eseguire la soluzione, premere CTRL\+F5.  
  
     Verrà aperta la finestra del browser in cui viene mostrata la visualizzazione directory per l'applicazione.  
  
4.  Nel browser fare clic su StockPriceService.xamlx.  
  
5.  Nel browser viene visualizzata la pagina **StockPriceService** contenente l'indirizzo wsdl del servizio locale.Copiare questo indirizzo.  
  
     L'indirizzo wsdl del servizio locale è, ad esempio, http:\/\/localhost:53797\/StockPriceService.xamlx?wsdl.  
  
6.  Da [!INCLUDE[fileExplorer](../../../../includes/fileexplorer-md.md)] passare alla cartella [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)] \(la cartella di installazione predefinita è %SystemDrive%\\Programmi\\Microsoft Visual Studio 10.0\).Individuare quindi la sottocartella Common7\\IDE\\.  
  
7.  Fare doppio clic sul file WcfTestClient.exe per avviare il client di prova WCF.  
  
8.  Nel client di prova WCF selezionare **Aggiungi servizio** dal menu **File**.  
  
9. Incollare l'URL appena copiato nella casella di testo.  
  
10. Scegliere **OK** per chiudere la finestra di dialogo.  
  
11. Eseguire il test del servizio utilizzando il client di prova WCF.  
  
    1.  Nel client di prova WCF fare doppio clic su **GetStockPrice\(\)** nel nodo **IStockPriceService**.  
  
         Il metodo **GetStockPrice\(\)** viene visualizzato nel riquadro destro con un parametro.  
  
    2.  Digitare Contoso come valore per il parametro.  
  
    3.  Fare clic su **Richiama**.  
  
12. Vedere gli eventi rilevati nel file di log presente nella directory dei dati dell'applicazione in %APPDATA%\\trackingRecords.log.  
  
    > [!NOTE]
    >  % APPDATA% è una variabile di ambiente che viene risolta in %SystemDrive%\\Users\\\<nomeutente\>\\AppData\\Roaming in [!INCLUDE[wv](../../../../includes/wv-md.md)], [!INCLUDE[lserver](../../../../includes/lserver-md.md)] o Windows Server 2008.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Tracking\TextFileTracking`  
  
## Vedere anche  
 [Monitoraggio](http://go.microsoft.com/fwlink/?LinkId=193959)