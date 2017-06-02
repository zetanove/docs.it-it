---
title: "Utilizzo dei contatori delle prestazioni | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 00a787af-1876-473c-a48d-f52b51e28a3f
caps.latest.revision: 31
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 31
---
# Utilizzo dei contatori delle prestazioni
In questo esempio viene illustrato come accedere ai contatori delle prestazioni di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e come creare contatori delle prestazioni definiti dall'utente.Questo esempio è basato sull'[Guida introduttiva](../../../../docs/framework/wcf/samples/getting-started-sample.md).  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine dell'argomento.  
  
 In questo esempio, il client chiama i quattro metodi del servizio `ICalculator`.Questa procedura continua fino a quando il client viene interrotto dall'utente.Il servizio rimane inalterato.  
  
 I contatori delle prestazioni vengono abilitati nella sezione di diagnostica del file Web.config per il servizio, come illustrato nella configurazione di esempio seguente.  
  
```  
<configuration>  
  <system.serviceModel>  
    <diagnostics performanceCounters="All" />   
  </system.serviceModel>  
</configuration>  
```  
  
 Questa attività può anche essere eseguita mediante [Strumento Editor di configurazione \(SvcConfigEditor.exe\)](../../../../docs/framework/wcf/configuration-editor-tool-svcconfigeditor-exe.md).  
  
 Quando i contatori delle prestazioni vengono abilitati, l'intera suite di contatori delle prestazioni [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] viene abilitata per il servizio..NET Framework gestisce automaticamente i dati relativi alle prestazioni a tre livelli: `ServiceModelService`, `ServiceModelEndpoint` e `ServiceModelOperation`.Per ognuno di questi livelli sono presenti dei contatori delle prestazioni, ad esempio "Chiamate", "Chiamate al secondo" e "Chiamate di sicurezza non autorizzate".  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Assicurarsi di avere eseguito [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare l'edizione C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Per eseguire l'esempio in un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
### Per visualizzare dati relativi alle prestazioni  
  
1.  Avviare lo strumento Performance Monitor facendo clic su **Start**, **Esegui…**, immettere `perfmon` e fare clic su **OK** oppure dal Pannello di controllo selezionare **Strumenti di amministrazione** e fare doppio clic su **Prestazioni**.  
  
    > [!NOTE]
    >  Non è possibile aggiungere contatori mentre il codice di esempio è in esecuzione.  
  
2.  Rimuovere i contatori delle prestazioni elencati selezionandoli e premendo CANC.  
  
3.  Per aggiungere contatori di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], fare clic con il pulsante destro del mouse sul riquadro del grafico e scegliere **Aggiungi contatori**.Nella finestra di dialogo **Aggiungi contatori** selezionare **ServiceModelOperation 3.0.0.0, ServiceModelEndpoint 3.0.0.0 o ServiceModelService 3.0.0.0** nell'elenco a discesa Oggetto prestazioni.Selezionare i contatori che si desidera visualizzare nell'elenco.  
  
    > [!NOTE]
    >  Se nel computer non è in esecuzione alcun servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], non sono disponibili contatori delle prestazioni di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
### Per utilizzare l'editor di configurazione per abilitare i contatori  
  
1.  Aprire un'istanza di SvcConfigEditor.exe.  
  
2.  Scegliere **Apri** dal menu File e fare clic su **File di configurazione…**.  
  
3.  Passare alla cartella del servizio dell'applicazione di esempio e aprire il file Web.config.  
  
4.  Fare clic su **Diagnostica** nella struttura ad albero Configurazione.  
  
5.  Attivare\/disattivare **Contatore prestazioni** nella finestra **Diagnostica** per visualizzare "Tutto".  
  
6.  Salvare il file di configurazione e uscire dall'editor.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Management\PerfCounters`  
  
## Vedere anche  
 [Monitoraggio](http://go.microsoft.com/fwlink/?LinkId=193959)